---
# required metadata

title: Use Intune to expedite Windows quality updates
description: Use Microsoft Intune policy to expedite the installation of Windows updates on managed devices as soon as possible.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 02/14/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: davguy;bryanke
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection:
- tier1
- M365-identity-device-management
---

# Expedite Windows quality updates in Microsoft Intune

With *Quality updates for Windows 10 and Later* policy, you can expedite the install of the most recent Windows 10/11 security updates as quickly as possible on devices you manage with Microsoft Intune. Deployment of expedited updates is done without the need to pause or edit your existing monthly servicing policies. For example, you might expedite a specific update to mitigate a security threat when your normal update process wouldn’t deploy the update for some time.

Not all updates can be expedited. Currently, only Windows 10/11 security updates that can be expedited are available to deploy with Quality updates policy. To manage regular monthly quality updates, use [Update rings for Windows 10 and later policies](../protect/windows-10-update-rings.md).

## How expedited updates work

With expedited updates, you can speed installation of quality updates like the most recent *patch Tuesday* release or an out-of-band security update for a zero-day flaw.

To speed installation, expedite is able to check for expedited updates more frequently than the normal Windows Update scan frequency. This process enables devices to start the download and install of an expedited update as soon as possible, without having to wait for the device to check in for updates.

The actual time that a device starts to update depends on the device being online, its scan timing, whether communication channels to the device are functioning, and other factors like cloud-processing time.

- For each expedite update policy you select a single update to deploy based on its release date. By using the release date, you don’t have to create separate policies to deploy different instances of that update to devices that have different versions of Windows, like Windows 10 version 1809, 1909, and so on.

- Windows Update evaluates the build and architecture of each device, and then delivers the version of the update that applies.

- Only devices that need the update receive the expedited update:
  - Windows Update doesn’t try to expedite the update for devices that already have a revision that’s equal to or greater than the update version.
  - For devices with a lower build version than the update, Windows Update confirms that the device still requires the update before installing it.

  > [!IMPORTANT]
  > In some scenarios, Windows Update can install an update that is more recent than the update you specify in expedite update policy. For more information about this scenario, see [About installing the latest applicable update](#identify-the-latest-applicable-update), later in this article.

- Expedite update policies ignore and override any quality [update deferral periods](/windows/client-management/mdm/policy-csp-update#update-deferqualityupdatesperiodindays) for the update version you deploy. You can configure quality updates deferrals by using Intune [Windows update rings](../protect/windows-10-update-rings.md) and the setting for **Quality update deferral period**.

- When a restart is required to complete installation of the update, the policy helps to manage the restart. In the policy, you can configure a period that users have to restart a device before the policy forces an automatic restart. Users can also choose to schedule the restart or let the device try to find the best time outside of the devices *Active Hours*. Before reaching the restart deadline, the device displays notifications to alert device users about the deadline and includes options to schedule the restart.

  If a device doesn’t restart before the deadline, the restart can happen in the middle of the working day. For more information on restart behavior, see [Enforcing compliance deadlines for updates](/windows/deployment/update/wufb-compliancedeadlines).

- Expedite is not recommended for normal monthly quality update servicing. Instead, consider using the *deadline settings* from an Update ring for Windows 10 and later policy. For information, see *Use deadline settings* under the user experience settings in [Windows update settings](../protect/windows-update-settings.md#user-experience-settings).  

## Prerequisites

> [!IMPORTANT]
> This feature is not supported on GCC and GCC High/DoD cloud environments.

The following are requirements to qualify for installing expedited quality updates with Intune:

**Licensing**:

In addition to a license for Intune, your organization must have one of the following subscriptions that include a license for Windows Update for Business deployment service:

- Windows 10/11 Enterprise E3 or E5 (included in Microsoft 365 F3, E3, or E5)
- Windows 10/11 Education A3 or A5 (included in Microsoft 365 A3 or A5)
- Windows Virtual Desktop Access E3 or E5
- Microsoft 365 Business Premium

Beginning in November of 2022, the Windows Update for Business deployment service (WUfB DS) license will be checked and enforced.

If you’re blocked when creating new policies for capabilities that require WUfB DS and you get your licenses to use WUfB through an Enterprise Agreement (EA), contact the source of your licenses such as your Microsoft account team or the partner who sold you the licenses. The account team or partner can confirm that your tenants licenses meet the WUfB DS license requirements. See [Enable subscription activation with an existing EA](/windows/deployment/deploy-enterprise-licenses#enable-subscription-activation-with-an-existing-ea).

**Supported Windows 10/11 versions**:

- Windows 10/11 versions that remain in support for Servicing, on x86 or x64 architecture

Only update builds that are generally available are supported. Preview builds, including the Beta and Dev channels, are not supported with expedited updates.

**Supported Windows 10/11 editions**:

- Professional
- Enterprise
- Education
- Pro Education
- Pro for Workstations

**Devices must**:

- Be [enrolled in Intune](/mem/intune/fundamentals/deployment-guide-enrollment) MDM, or be [co-managed](../../configmgr/comanage/overview.md) with the [Windows Update policies](../../configmgr/comanage/workloads.md#windows-update-policies) workload set to Intune or Pilot Intune.

- Be Azure Active Directory (AD) Joined, or Hybrid Azure AD Joined. Workplace Join isn't supported.

- Have access to endpoints. To get a detailed list of endpoints required for the associated service listed here, go to [Network endpoints](../fundamentals/intune-endpoints.md#access-for-managed-devices).  

  - [Windows Update](/windows/privacy/manage-windows-1809-endpoints#windows-update)
  - Windows Update for Business -deployment service
  - [Windows Push Notification Services](/windows/uwp/design/shell/tiles-and-notifications/firewall-allowlist-config): *(Recommended, but not required. Without this access, devices might not expedite updates until their next daily check for updates.)*

- Be configured to get Quality Updates directly from the Windows Update service.

- Have the *Update Health Tools* installed, which are installed with [KB 4023057 - Update for Windows 10 Update Service components](https://support.microsoft.com/topic/kb4023057-update-for-windows-10-update-service-components-fccad0ca-dc10-2e46-9ed1-7e392450fb3a). To confirm the presence of the Update Health Tools on a device:
  - Look for the folder **C:\Program Files\Microsoft Update Health Tools** or review *Add Remove Programs* for **Microsoft Update Health Tools**.
  - As an Admin, run the following PowerShell script:

   ``` PowerShell
   $Session = New-Object -ComObject Microsoft.Update.Session
   $Searcher = $Session.CreateUpdateSearcher()
   $historyCount = $Searcher.GetTotalHistoryCount()
   $list = $Searcher.QueryHistory(0, $historyCount) | Select-Object -Property "Title"
   foreach ($update in $list)
   {
     if ($update.Title.Contains("4023057"))
     {
        return 1
     }
   }
   return 0 
   ```
  If the script returns a 1, the device has UHS client. If the script returns a 0, the device doesn’t have UHS client.



 
**Device settings**:

To help avoid conflicts or configurations that can block installation of expedited updates, configure devices as follows. You can use Intune *Update rings for Windows 10 and later* policies to manage these settings.

| Update ring setting       | Recommended value        |
|---------------------------|-------------------------------------|
| Enable pre-release builds | This setting should be set to **Not configured**. Preview builds, including the Beta and Dev channels, are not supported with expedited updates. |
| Automatic update behavior | **Reset to default**  <br><br> Other values might cause a poor user experience and  slow the process to expedite updates. |
| Change notification update level | Use any value other than **Turn off all notifications, including restart warnings** |

For more information about these settings, see [Policy CSP – Update](/windows/client-management/mdm/policy-csp-update).

Group Policy settings override mobile device management policies, and the following list of Group Policy settings can interfere with Expedited policy. On devices where these settings were managed by Group Policy, restore them to their device defaults (Not configured):

- **CorpWuURL** - Specify intranet Microsoft update service location.
- **AutoUpdateCfg** - Configure Automatic Updates.
- **DeferFeatureUpdates** - Select when Preview Builds and Feature Updates are received.
- **Disable Dual Scan** - Don't allow update deferral policies to cause scans against Windows Update.

**Enable Windows Health Monitoring**:

Before you can monitor results and update status for expedited updates, your Intune tenant must enable [Windows Health Monitoring](../configuration/windows-health-monitoring.md). While configuring Windows Health Monitoring, be sure to set the **Scope** to **Windows updates**.
 
## Create and assign an expedited quality update

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Quality updates for Windows 10 and later** > **Create profile**.

   :::image type="content" source="./media/windows-10-expedite-updates/create-quality-update-profile.png" alt-text="Screen capture of the Create profile UI":::

3. In **Settings**, enter the following properties to identify this profile:

   - **Name**: Enter a descriptive name for the profile. Name your profiles so you can easily identify them later.

   - **Description**: Enter a description for the profile. This setting is optional but recommended.

4. In **Settings**, configure **Expedite installation of quality updates if device OS version less than**. Select the update that you want to expedite from the drop-down list. The list includes only the updates you can expedite.

   > [!TIP]
   > Optional Windows quality updates can’t be expedited and won’t be available to select.

   :::image type="content" source="./media/windows-10-expedite-updates/select-update.png" alt-text="Screen capture of update selection UI":::

   When selecting an update:

   - Updates are identified by their release date, and you can select only one update per policy.

   - Updates that include the letter **B** in their name identify updates that released as part of a *patch Tuesday* event. The letter B identifies that the update released on the second Tuesday of the month.

   - Security updates for Windows 10/11 that release out of band from a *patch Tuesday* can be expedited. Instead of the letter B, *out-of-band* patch releases have different identifiers.

   - When the update deploys, Windows Update ensures that each device that receives the policy installs a version of the update that applies to that devices architecture and its current Windows version, like version 1809, 2004, and so on.

   > [!TIP]
   > For more information, see the blog [Windows 10 update servicing cadence - Microsoft Tech Community](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/windows-10-update-servicing-cadence/ba-p/222376).

5. In **Settings**, configure **Number of days to wait before forced reboot**. For this setting, select how soon after installing the update a device will automatically restart to complete the update installation. You can select from zero to two days. The automatic restart is canceled if a device manually restarts before the deadline. If an update doesn’t require a restart, this setting isn’t enforced.

   - A setting of **0 days** means that as soon as the device installs the update, the user is notified about the restart and has limited time to save their work.

   > [!IMPORTANT]
   > This experience can impact user productivity. Consider using it for those devices or updates that must complete and restart the device as soon as possible.

   - A setting of **1 day** or **2 days** provides device users flexibility to manage a restart before it’s forced. These settings correspond to an automatic restart delay of 24 or 48 hours after the update installs on the device.

     :::image type="content" source="./media/windows-10-expedite-updates/select-reboot-time.png" alt-text="Screen capture of selecting days before forced reboot":::

6. In **Assignments**, select **Add groups** and then select device or user groups to assign the policy.

7. In **Review + create**, select **Create**. After the policy is created, it deploys to assigned groups.

## Identify the latest applicable update

There are some scenarios when your policy to expedite an update results in the installation of a more recent update than specified in policy. This result occurs when the newer update includes and surpasses the specified update, and that newer update is available before a device checks in to install the update that's specified in the expedite update policy. A detailed [example](#example-of-installing-an-expedited-update) of this scenario is provided later in this article.

Installing the most recent quality update reduces disruptions to the device and user while applying the benefits of the intended update. This avoids having to install multiple updates, which each might require separate reboots.

A more recent update is deployed when the following conditions are met:

- The device isn't targeted with a deferral policy that blocks installation of a more recent update. In this case, the most recently available update that isn't deferred is the update that might install.

- During the process to expedite an update, the device runs a new scan that detects the newer update. This can occur due to the timing of:
  - When the device restarts to complete installation
  - When the device runs its daily scan
  - When a new update becomes available

  When a scan identifies a newer update, Windows Update attempts to stop installation of the original update, cancel the restart, and then starts the download and installation of the more recent update.

While expedite update policies will override an update deferral for the update version that’s specified in the policy, they don’t override deferrals that are in place for any other update version.

### Example of installing an expedited update

The following sequence of events provides an example of how two devices, named *Test-1* and *Test-2*, install an update based on a *Quality updates for Windows 10 and Later* policy that's assigned to the devices.

1. Each month, Intune administrators deploy the most recent Windows 10 quality updates on the fourth Tuesday of the month. This period gives them two weeks after the patch Tuesday event to validate the updates in their environment before they force installation of the update.

2. On January 19, 2021, device *Test-1* and *Test-2* install the latest quality update from the patch Tuesday release on January 12. The next day, both devices are turned off by their users who are each leaving on vacation.

3. On the February 9, the Intune admin creates policy to expedite installation of the patch Tuesday release **02/09/2021 – 2021.02 B Security Updates for Windows 10** to help secure company devices against a critical threat that the update resolves. The expedite policy is assigned to a group of devices that includes both *Test-1* and *Test-2*. All devices in that group that are active receive and install the expedited update policy.

4. On the March 9 patch Tuesday event, a new quality update releases as **03/09/2021 – 2021.03 B Security Updates for Windows 10**. There are no critical issues that require an expedited deployment of this update, but admins do find a possible conflict. To provide time to review the possible issue, admins use a Windows update ring policy to create a seven-day deferral policy. All managed devices are prevented from installing this update until March 14.

5. Now consider the following results for *Test-1* and *Test-2*, based on when each is turned back on:

   - **Test-1** - On March 12, *Test-1* is powered back on, connects to the network, and receives expedited update notifications:  
     1. Windows Update determines that *Test-1* still needs to expedite the update installation, per policy.
     2. Because the March 9 update supersedes the February update, Windows Update could install the March 9 update.
     3. There's an active deferral for the March update that won't expire until March 14.

     **Result**: With the deferral policy for the March update still active and blocking installation of that update, *Device-1* installs the February update as configured in policy.

   - **Test-2** - On March 20, *Test-2* is powered back on, connects to the network, and receives expedited update notifications:  
     1. Windows Update determines that *Test-2* still needs to expedite the update installation, per policy.
     2. Because the March 9 update supersedes the February update, Windows Update could install the March 9 update.
     3. There's no longer an active deferral for the March update.

     **Result**: With the deferral policy for the March update having expired, *Test-2* installs the more recent March update, skipping over the February update and installing a later update than was specified in policy.

## Manage policies to expedite quality updates

In the admin center, go to **Devices** > **Windows** > **Quality updates for Windows 10 and later** and select the policy that you want to manage. The policy opens to its **Overview** pane.

From this pane, you can:

- Select **Delete** to delete the policy from Intune. Deleting a policy removes it from Intune but won’t result in the update uninstalling if it has already completed installation. Windows Update will attempt to cancel any in-progress installations, but a successful cancellation of an in-progress install can’t be guaranteed.

- Select **Properties** to modify the deployment. On the *Properties* pane, select **Edit** to open the *Settings*, *Scope tags*, or *Assignments*, where you can then modify the deployment.

## Monitoring and reporting

Before you can monitor results and update status for expedited updates, your Intune tenant must enable [Windows Health Monitoring](../configuration/windows-health-monitoring.md).

> [!IMPORTANT]
> When you configure the Windows Health Monitoring profile, during step seven you must set the **Scope** to **Windows updates**.

After a policy has been created you can monitor results, update status, and errors from the following reports.

### Summary report

This report shows the current state of all devices in the profile and provides an overview of how many devices are in progress of installing an update, have completed the installation, or have an error.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Reports** > **Windows updates**. On the **Summary** tab you can view the **Windows Expedited Quality updates** table.

3. To drill in for more information, select the **Reports** tab, and then **Windows Expedited Update Report**.

4. Click the link **Select an expedited update profile**.

5. From the list of profiles that is shown on the right side of the page, select a profile to see results.

6. Select the **Generate report** button.

### Device report

This report can help you find devices with alerts or errors and can help you troubleshoot update issues.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431)

2. Select **Devices** > **Monitor**.

3. In the list of monitoring reports, scroll to the Software updates section and select **Windows Expedited update failures**.

4. From the list of profiles that is shown on the right side of the page, select a profile to see results.
 
   :::image type="content" source="./media/windows-10-expedite-updates/device-report.png" alt-text="Example of the device report":::

### Update states

|  Update State  |  Update SubState  |  Definition  |
|------------|------------------|-------------------|
| Pending    | Validating       | The device has been added to the policy in the service and validation that the device can be expedited has begun.  |
| Pending    | Scheduled        | Device has passed validation and will be expedited. |
| Offering   | OfferReady       | The expedite instructions have been sent to the device. |
| Installing | OfferReceived    | Device scanned against Windows Update and the update is applicable but hasn't yet begun to download. |
| Installing | DownloadStart    | The device has begun to download the update. |
| Installing | DownloadComplete | The device has downloaded the update. |
| Installing | InstallStart     | The device has begun to install the update. |
| Installing | InstallComplete  | The device has completed installing the update. Unless the update has an update error, the device should move quickly to *RestartRequired* or *UpdateInstalled*. |
| Installing | RestartRequired  | The installation is complete and requires a restart. |
| Installing | RestartInitiated | The device has begun a restart. |
| Installing | RestartComplete  | The device has completed the restart. |
| Installed  | UpdateInstalled  | Update has successfully completed. |

## Next steps

- Configure [Update rings for Windows 10 and later](../protect/windows-10-update-rings.md)
- Configure [Feature updates for Windows 10 and later](../protect/windows-10-feature-updates.md)
- Use [Windows update compatibility reports](../protect/windows-update-compatibility-reports.md)
- View [Windows release information](/windows/release-information/)
