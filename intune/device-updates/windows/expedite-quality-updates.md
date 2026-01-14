---
title: Expedite Windows quality updates
description: Use Hotpatch updates to receive security updates without restarting your device
ms.date: 04/17/2025
ms.reviewer: Mounika
ms.topic: how-to
---

# Expedite Windows quality updates

Expedite policies let you accelerate the installation of a specific Windows security update on devices you manage with Microsoft Intune. Expedited updates install as soon as possible, bypassing deferral settings and normal deployment timing, without requiring you to pause or modify your existing monthly update policies.

You might use an expedite policy to quickly mitigate a critical security vulnerability when your standard update process wouldn't deploy the update soon enough. Expedite policies are designed for targeted, time‑bound scenarios and don't change how future quality updates are deployed.

Not all updates are eligible for expediting. Only supported Windows security updates can be expedited. To manage regular monthly quality updates, continue using standard Windows Update mechanisms such as update rings or Windows quality updates policies.

## Before you begin

> [!div class="checklist"]
> - Ensure your environment meets the requirements in [Windows quality updates overview](quality-updates.md#prerequisites).
> - To avoid conflicts or configurations that can block the installation of expedited updates, configure devices as follows. You can use *update rings policies* to manage these settings.
>
>    | Update ring setting       | Recommended value        |
>    |---------------------------|-------------------------------------|
>    | Enable pre-release builds | This setting should be set to **Not configured**. Preview builds, including the Beta and Dev channels, are not supported with expedited updates. |
>    | Automatic update behavior | **Reset to default**.  <br> Other values might cause a poor user experience and  slow the process to expedite updates. |
>    | Change notification update level | Use any value other than **Turn off all notifications, including restart warnings**. |
>    
>    For more information about these settings, see [Policy CSP Update](/windows/client-management/mdm/policy-csp-update).
>
> - The following list of Group Policy settings can interfere with Expedited policy. On devices where these settings were managed by Group Policy, restore them to their defaults (Not configured):
>    - **CorpWuURL** - Specify intranet Microsoft update service location.
>    - **AutoUpdateCfg** - Configure Automatic Updates.
>    - **DeferFeatureUpdates** - Select when Preview Builds and Feature Updates are received.
>    - **Disable Dual Scan** - Don't allow update deferral policies to cause scans against Windows Update.

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

When you create an expedite policy, you select a single supported Windows security update to deploy. The update is identified by its release date, which allows one policy to apply across multiple supported Windows versions without creating version‑specific policies.

After the policy is assigned, Windows Update evaluates each targeted device to determine applicability. Evaluation accounts for the device's current build, architecture, and update state, and Windows Update delivers the appropriate version of the update when required.

Only devices that need the update receive it:

- Devices that already have the same update, or a newer applicable update, don't receive the expedited update.
- For devices on earlier builds, Windows Update verifies the update remains applicable before installation.

  > [!IMPORTANT]
  > In some scenarios, Windows Update might install a newer update than the one specified in the expedite policy. This behavior ensures devices receive the latest applicable security update. For more information, see About installing the latest applicable update.

Expedited updates begin installing after the device completes its next update scan and communicates with the service. The time required for installation to start can vary based on factors such as device connectivity, scan timing, and service processing.

If a restart is required, you can configure a restart deadline that defines how long users have to restart their device before enforcement. Users can restart immediately, schedule a restart, or allow Windows to select a time outside active hours. Notifications inform users of the pending restart and deadline.

If the device doesn't restart before the deadline, the restart can occur during working hours. For more information, see [Enforcing compliance deadlines for updates](/windows/deployment/update/wufb-compliancedeadlines).

Expedite policies don't affect how future quality updates are deployed. To manage ongoing monthly servicing, use update ring policies or Windows quality updates policies and their deadline settings.

## Create and assign an expedited quality update

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > **Windows Updates**.
1. Select the **Quality updates**.
1. Select **Create** > **Expedite policy**.
1. In **Settings**, enter the following properties to identify this profile:

   - **Name**: Enter a descriptive name for the profile.
   - **Description**: Enter a description for the profile. This setting is optional but recommended.
   - From the **Select the quality update you would like to Expedite** dropdown list, select the update that you want to expedite. The list includes only the updates you can expedite.

   > [!TIP]
   > Optional Windows quality updates can't be expedited and won't be available.

   When selecting an update:

   - Updates are identified by their release date, and you can select only one update per policy.
   - Updates that include the letter **B** in their name identify updates that released as part of a *patch Tuesday* event. The letter B identifies that the update released on the second Tuesday of the month.
   - Security updates for Windows that release out of band from a *patch Tuesday* can be expedited. Instead of the letter B, *out-of-band* patch releases have different identifiers.
   - When the update deploys, Windows Update ensures that each device that receives the policy installs a version of the update that applies to that devices architecture and its current Windows version, like version 24H2, 25H2, and so on.

   **Non-Security Expedite Updates**: includes quality fixes after the previous B / Security release. Admins can expedite installation of the latest applicable quality update on devices, without waiting for the deferral period.

   - Updates without the word **SecurityUpdate** indicate that it is not a security update. Updates that include the letter **D** in their name identify updates that are released since the latest *patch Tuesday* security week. You might also see 2024.01 OOB Update (*out-of-band* patch releases). [Windows monthly update explained](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/windows-monthly-updates-explained/ba-p/3773544)
   - Non-security updates are only shown when it is the most recent release. The drop-down list is updated to display the most recent two security updates, including if one is an out-of-band update. If the most recent non-security update is newer than the newest security update, then the non-security update is also included in the drop-down list. As a result, sometimes two updates are shown, and at other times, three updates are shown.

     > [!TIP]
     > For more information, see the blog [Windows update servicing cadence - Microsoft Tech Community](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/update-servicing-cadence/ba-p/222376).

   - The non-security expedite updates apply to Windows 11 devices. If Windows 10 devices are assigned to an Expedite policy that sets a **D** release, then those devices are not expedited and show an alert in the following reports.

1. In **Settings**, configure **If a reboot is required, select the number of days before it's enforced**. For this setting, select how soon after installing the update a device will automatically restart to complete the update installation. You can select from zero to two days. The automatic restart is canceled if a device manually restarts before the deadline. If an update doesn't require a restart, this setting isn't enforced.

   - A setting of **0 days** means that as soon as the device installs the update, the user is notified about the restart and has limited time to save their work.

     > [!IMPORTANT]
     > This experience can impact user productivity. Consider using it for those devices or updates that must complete and restart the device as soon as possible.

   - A setting of **1 day** or **2 days** provides device users flexibility to manage a restart before it's forced. These settings correspond to an automatic restart delay of 24 or 48 hours after the update installs on the device.

1. In **Assignments**, select **Add groups** and then select device or user groups to assign the policy.
1. In **Review + create**, select **Create**. After the policy is created, it deploys to assigned groups.

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
1. On the February 9, the Intune admin creates policy to expedite installation of the patch Tuesday release **02/09/2025 - 2025.02 B Security Updates for Windows** to help secure company devices against a critical threat that the update resolves. The expedite policy is assigned to a group of devices that includes both *Test-1* and *Test-2*. All devices in that group that are active receive and install the expedited update policy.
1. On the March 9 patch Tuesday event, a new quality update releases as **03/09/2025 - 2025.03 B Security Updates for Windows**. There are no critical issues that require an expedited deployment of this update, but admins do find a possible conflict. To provide time to review the possible issue, admins use a Windows update ring policy to create a seven-day deferral policy. All managed devices are prevented from installing this update until March 14.
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

## Manage expedite policies

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > **Windows Updates**.
1. Select the **Quality updates** tab and then select the policy that you want to manage. The policy opens to its **Overview** pane.

From this pane, you can:

- Select **Delete** to delete the policy from Intune. Deleting a policy removes it from Intune but won't result in the update uninstalling if it has already completed installation. Windows Update will attempt to cancel any in-progress installations, but a successful cancellation of an in-progress install can't be guaranteed.
- Select **Properties** to modify the deployment. On the *Properties* pane, select **Edit** to open the *Settings*, *Scope tags*, or *Assignments*, where you can then modify the deployment.

## Monitoring and reporting

After you create an expedite policy you can monitor results, update status, and errors from the following reports. Select each tab to learn more about the reports.

# [**Summary report**](#tab/summary)

This report shows the current status of all devices targeted by an expedite policy and provides an overview of how many devices are installing the update, have completed installation, or have encountered an error.

1. In the [Microsoft Intune admin center][INT-AC], select **Reports** > **Windows Updates**.
1. On the **Summary** tab you can view the **Windows Expedited Quality updates** table.
1. To drill in for more information, select the **Reports** tab, and then **Windows Expedited Update Report**.
1. Click the link **Select an expedited update profile**.
1. From the list of profiles that is shown on the right side of the page, select a profile to see results.
1. Select the **Generate report** button.

# [**Device report**](#tab/device)

This report can help you find devices with alerts or errors and can help you troubleshoot update issues.

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > **Monitor**.
1. In the list of monitoring reports, select **Expedited quality update policies with alerts**.
1. From the list of profiles, select a profile to see results.

### Update states

| Update State | Update SubState  | Definition                                                                                                                                                       |
|--------------|------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Pending      | Validating       | The device has been added to the policy in the service and validation that the device can be expedited has begun.                                                |
| Pending      | Scheduled        | Device has passed validation and will be expedited.                                                                                                              |
| Offering     | OfferReady       | The expedite instructions have been sent to the device.                                                                                                          |
| Installing   | OfferReceived    | Device scanned against Windows Update and the update is applicable but hasn't yet begun to download.                                                             |
| Installing   | DownloadStart    | The device has begun to download the update.                                                                                                                     |
| Installing   | DownloadComplete | The device has downloaded the update.                                                                                                                            |
| Installing   | InstallStart     | The device has begun to install the update.                                                                                                                      |
| Installing   | InstallComplete  | The device has completed installing the update. Unless the update has an update error, the device should move quickly to *RestartRequired* or *UpdateInstalled*. |
| Installing   | RestartRequired  | The installation is complete and requires a restart.                                                                                                             |
| Installing   | RestartInitiated | The device has begun a restart.                                                                                                                                  |
| Installing   | RestartComplete  | The device has completed the restart.                                                                                                                            |
| Installed    | UpdateInstalled  | Update has successfully completed.                                                                                                                               |

## Next steps

- Configure [update ring policies](update-rings.md)
- Configure [feature updates policies](feature-updates.md)
- View [Windows release information](/windows/release-information/)

<!-- admin center links -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
