---
title: Use Intune to expedite Windows quality updates
description: Use Microsoft Intune policy to expedite the installation of Windows updates on managed devices as soon as possible.
ms.date: 02/20/2025
ms.topic: how-to
ms.reviewer: davguy;bryanke
---

# Expedite Windows quality updates in Microsoft Intune

With Windows quality updates policies you can expedite the installation of the most recent Windows security updates on devices you manage with Microsoft Intune. Deployment of expedited updates is done without the need to pause or edit your existing monthly update policies. For example, you might expedite a specific update to mitigate a security threat when your normal update process wouldn't deploy the update for some time.

Not all updates can be expedited. Currently, only Windows security updates that can be expedited are available to deploy with Quality updates policy. To manage regular monthly quality updates, use [Windows Update ring policies](update-rings.md).

## Prerequisites

[!INCLUDE [prerequisites-network](includes/prerequisites-network.md)]
[!INCLUDE [prerequisites-tenant](includes/prerequisites-tenant.md)]
[!INCLUDE [prerequisites-licensing](includes/prerequisites-licensing.md)]
[!INCLUDE [prerequisites-platform](includes/prerequisites-platform.md)]
[!INCLUDE [prerequisites-device-configuration](includes/prerequisites-device-configuration.md)]
[!INCLUDE [prerequisites-rbac](includes/prerequisites-rbac.md)]

### Update Health Tools

For **Windows versions earlier than 24H2**, the Update Health Tools are required on devices to support expedited updates. The tools can be installed through [KB4023057](https://support.microsoft.com/topic/fccad0ca-dc10-2e46-9ed1-7e392450fb3a) or manually from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=103324).

To confirm the presence of the Update Health Tools on a device:

- Look for the folder **C:\Program Files\Microsoft Update Health Tools** or review *Services* or *Add Remove Programs* for **Microsoft Update Health Tools**.
- As an Admin (or from Intune), run the following PowerShell script:

```PowerShell
### Check for the Microsoft Update Health Service; if found, no remediation is needed.
if (Get-Service -Name "Microsoft Update Health Service" -ErrorAction SilentlyContinue) {
    Write-Host "Microsoft Update Health Service is present."
    Exit 0
} else {
    Write-Host "Microsoft Update Health Service is missing."
    Exit 1
}
```

If the script returns a `1`, the device has UHS client. If the script returns a `0`, the device doesn't have UHS client.

## How expedited updates work

With expedited updates, you can expedite the installation of quality updates like the most recent *patch Tuesday* release or an out-of-band security update for a zero-day flaw.

Expedited update policies temporarily override deferrals and other settings to install updates as quickly as possible. This process enables devices to start the download and installation of an expedited update without having to wait for the device to check in for updates.

The actual time required for a device to start an update depends on the device internet connectivity, its scan timing, whether communication channels to the device are functioning, and other factors like cloud-processing time.

- For each expedited update policy, you select a single update to deploy based on its release date. By using the release date, you don't have to create separate policies to deploy different instances of that update to devices that have different versions of Windows.

- Windows Update evaluates the build and architecture of each device, and then delivers the version of the update that applies.

- Only devices that need the update receive the expedited update:
  - Windows Update doesn't try to expedite the update for devices that already have a revision that's equal to or greater than the update version.
  - For devices with a lower build version than the update, Windows Update confirms that the device still requires the update before installing it.

  > [!IMPORTANT]
  > In some scenarios, Windows Update can install an update that is more recent than the update you specify in expedite update policy. For more information about this scenario, see [About installing the latest applicable update](#identify-the-latest-applicable-update), later in this article.

- Expedite update policies ignore and override any quality [update deferral periods](/windows/client-management/mdm/policy-csp-update#update-deferqualityupdatesperiodindays) for the update version you deploy. You can configure quality updates deferrals by using Intune [Windows update rings](update-rings.md) and the setting for **Quality update deferral period**.

- When a restart is required to complete installation of the update, the policy helps to manage the restart. In the policy, you can configure a period that users have to restart a device before the policy forces an automatic restart. Users can also choose to schedule the restart or let the device try to find the best time outside of the devices *Active Hours*. Before reaching the restart deadline, the device displays notifications to alert device users about the deadline and includes options to schedule the restart.

  If a device doesn't restart before the deadline, the restart can happen in the middle of the working day. For more information on restart behavior, see [Enforcing compliance deadlines for updates](/windows/deployment/update/wufb-compliancedeadlines).

- Expedited updates are not recommended for normal monthly quality update servicing. Instead, consider using the *deadline settings* from an update ring policy. For information, see *Use deadline settings* under the user experience settings in [Windows update settings](settings.md#user-experience-settings).

## Create and assign an expedited quality update

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Manage updates** > **Windows updates**> **Quality updates** tab > **Create profile**.

   :::image type="content" source="./images/expedite-updates/create-quality-update-profile.png" alt-text="Screen capture of the Create profile UI.":::

3. In **Settings**, enter the following properties to identify this profile:

   - **Name**: Enter a descriptive name for the profile. Name your profiles so you can easily identify them later.

   - **Description**: Enter a description for the profile. This setting is optional but recommended.

4. In **Settings**, configure **Expedite installation of quality updates if device OS version less than**. Select the update that you want to expedite from the drop-down list. The list includes only the updates you can expedite.

   > [!TIP]
   > Optional Windows quality updates can't be expedited and won't be available to select.

   :::image type="content" alt-text="Screen capture of update selection UI." source="./images/expedite-updates/select-update.png" lightbox="./images/expedite-updates/select-update.png":::

   When selecting an update:

   - Updates are identified by their release date, and you can select only one update per policy.

   - Updates that include the letter **B** in their name identify updates that released as part of a *patch Tuesday* event. The letter B identifies that the update released on the second Tuesday of the month.

   - Security updates for Windows that release out of band from a *patch Tuesday* can be expedited. Instead of the letter B, *out-of-band* patch releases have different identifiers.

   - When the update deploys, Windows Update ensures that each device that receives the policy installs a version of the update that applies to that devices architecture and its current Windows version, like version 1809, 2004, and so on.

   **Non-Security Expedite Updates**: includes quality fixes after the previous B / Security release. Admins can expedite installation of the latest applicable quality update on devices, without waiting for the deferral period.

   - Updates without the word **SecurityUpdate** indicate that it is not a security update. Updates that include the letter **D** in their name identify updates that are released since the latest *patch Tuesday* security week. You might also see 2024.01 OOB Update (*out-of-band* patch releases). [Windows monthly update explained](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/windows-monthly-updates-explained/ba-p/3773544)

   - Non-security updates are only shown when it is the most recent release. The drop-down list is updated to display the most recent two security updates, including if one is an out-of-band update. If the most recent non-security update is newer than the newest security update, then the non-security update is also included in the drop-down list. As a result, sometimes two updates are shown, and at other times, three updates are shown.

     > [!TIP]
     > For more information, see the blog [Windows update servicing cadence - Microsoft Tech Community](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/update-servicing-cadence/ba-p/222376).

   - The non-security expedite updates apply to Windows 11 devices. If Windows 10 devices are assigned to an Expedite policy that sets a **D** release, then those devices are not expedited and show an alert in the following reports.
     - **Reports** > **Windows Updates** > **Reports** Tab > **Windows Expedited Update Report**
     - **Devices** > **Manage updates** > **Windows updates** > **Monitor** tab > **Expedited quality update policies** with alerts tile, and click the title.

5. In **Settings**, configure **Number of days to wait before forced reboot**. For this setting, select how soon after installing the update a device will automatically restart to complete the update installation. You can select from zero to two days. The automatic restart is canceled if a device manually restarts before the deadline. If an update doesn't require a restart, this setting isn't enforced.

   - A setting of **0 days** means that as soon as the device installs the update, the user is notified about the restart and has limited time to save their work.

     > [!IMPORTANT]
     > This experience can impact user productivity. Consider using it for those devices or updates that must complete and restart the device as soon as possible.

   - A setting of **1 day** or **2 days** provides device users flexibility to manage a restart before it's forced. These settings correspond to an automatic restart delay of 24 or 48 hours after the update installs on the device.

     :::image type="content" alt-text="Screen capture of selecting days before forced reboot." source="./images/expedite-updates/select-reboot-time.png" lightbox="./images/expedite-updates/select-reboot-time.png":::

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

While expedite update policies will override an update deferral for the update version that's specified in the policy, they don't override deferrals that are in place for any other update version.

### Example of installing an expedited update

The following sequence of events provides an example of how two devices, named *Test-1* and *Test-2*, install an update based on a *quality updates policy* that's assigned to the devices.

1. Each month, Intune administrators deploy the most recent Windows quality updates on the fourth Tuesday of the month. This period gives them two weeks after the patch Tuesday event to validate the updates in their environment before they force installation of the update.
1. On January 19, device *Test-1* and *Test-2* install the latest quality update from the patch Tuesday release on January 12. The next day, both devices are turned off by their users who are each leaving on vacation.
1. On the February 9, the Intune admin creates policy to expedite installation of the patch Tuesday release **02/09/2025 – 2025.02 B Security Updates for Windows** to help secure company devices against a critical threat that the update resolves. The expedite policy is assigned to a group of devices that includes both *Test-1* and *Test-2*. All devices in that group that are active receive and install the expedited update policy.
1. On the March 9 patch Tuesday event, a new quality update releases as **03/09/2025 – 2025.03 B Security Updates for Windows**. There are no critical issues that require an expedited deployment of this update, but admins do find a possible conflict. To provide time to review the possible issue, admins use a Windows update ring policy to create a seven-day deferral policy. All managed devices are prevented from installing this update until March 14.
1. Now consider the following results for *Test-1* and *Test-2*, based on when each is turned back on:

   - **Test-1** - On March 12, *Test-1* is powered back on, connects to the network, and receives expedited update notifications:
     1. Windows Update determines that *Test-1* still needs to expedite the update installation, per policy.
     1. Because the March 9 update supersedes the February update, Windows Update could install the March 9 update.
     1. There's an active deferral for the March update that won't expire until March 14.

     **Result**: With the deferral policy for the March update still active and blocking installation of that update, *Device-1* installs the February update as configured in policy.

   - **Test-2** - On March 20, *Test-2* is powered back on, connects to the network, and receives expedited update notifications:
     1. Windows Update determines that *Test-2* still needs to expedite the update installation, per policy.
     1. Because the March 9 update supersedes the February update, Windows Update could install the March 9 update.
     1. There's no longer an active deferral for the March update.

     **Result**: With the deferral policy for the March update having expired, *Test-2* installs the more recent March update, skipping over the February update and installing a later update than was specified in policy.

## Manage policies to expedite quality updates

In the admin center, go to **Devices** > **By platform** > **Windows** > **Manage updates** > **Windows updates** > **Quality updates** tab and select the policy that you want to manage. The policy opens to its **Overview** pane.

From this pane, you can:

- Select **Delete** to delete the policy from Intune. Deleting a policy removes it from Intune but won't result in the update uninstalling if it has already completed installation. Windows Update will attempt to cancel any in-progress installations, but a successful cancellation of an in-progress install can't be guaranteed.

- Select **Properties** to modify the deployment. On the *Properties* pane, select **Edit** to open the *Settings*, *Scope tags*, or *Assignments*, where you can then modify the deployment.

## Monitoring and reporting

After a policy has been created you can monitor results, update status, and errors from the following reports.

### Summary report

This report shows the current state of all devices in the profile and provides an overview of how many devices are in progress of installing an update, have completed the installation, or have an error.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Select **Reports** > **Windows updates**. On the **Summary** tab you can view the **Windows Expedited Quality updates** table.
1. To drill in for more information, select the **Reports** tab, and then **Windows Expedited Update Report**.
1. Click the link **Select an expedited update profile**.
1. From the list of profiles that is shown on the right side of the page, select a profile to see results.
1. Select the **Generate report** button.

### Device report

This report can help you find devices with alerts or errors and can help you troubleshoot update issues.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431)
1. Select **Devices** > **Monitor**.
1. In the list of monitoring reports, scroll to the Software updates section and select **Windows Expedited update failures**.
1. From the list of profiles that is shown on the right side of the page, select a profile to see results.

   :::image type="content" alt-text="Example of the device report." source="./images/expedite-updates/device-report.png" lightbox="./images/expedite-updates/device-report.png":::

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

- Configure [update ring policies](update-rings.md)
- Configure [feature updates policies](feature-updates.md)
- Use [compatibility reports](compatibility-reports.md)
- View [Windows release information](/windows/release-information/)
