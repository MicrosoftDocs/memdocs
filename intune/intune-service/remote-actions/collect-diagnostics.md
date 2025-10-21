---
title: "Remote Device Action: Collect Diagnostics"
description: Learn how to collect diagnostics with Microsoft Intune.
ms.date: 09/22/2025
ms.topic: how-to
ms.reviewer: jlynn
zone_pivot_groups: d4b2a9c3-d659-4922-8403-9b50d065fc07
---

# Remote device action: collect diagnostics

Collecting diagnostics in Microsoft Intune is a powerful remote action that enables IT administrators to gather troubleshooting data from managed devices without interrupting users. This feature is essential for identifying and resolving issues related to device compliance, app performance, or enrollment failures—especially in large or distributed environments where hands-on access to devices is limited. For example, if a Windows device fails during Autopilot provisioning, Intune can automatically collect logs from the device and upload them for review, helping admins pinpoint the root cause quickly. This feature can also be used in bulk across up to 25 devices at once, streamlining diagnostics at scale.

The *collect diagnostics* remote action lets you collect and download managed device diagnostics without interrupting the user. Only nonuser locations and file types are accessed.

## Requirements

[!INCLUDE [platform-requirements](../../includes/h3/platform-requirements.md)]

> [!div class="checklist"]
> This remote action supports the following platforms:
>
> - Android (via app protection)
> - iOS/iPadOS (via app protection)
> - Windows (corporate-owned)
> - Windows Holographic

[!INCLUDE [rbac-requirements](../../includes/h3/rbac-requirements.md)]

> [!div class="checklist"]
> To run this remote action, use an account with at least one of the following roles:
>
> - [Help Desk Operator][INT-R1]
> - [School Administrator][INT-R2]
> - [Custom role][INT-RC] that includes:
>   - The permission **Remote tasks/Collect diagnostics**
>   - Permissions that provide visibility into and access to managed devices in Intune (for example, Organization/Read, Managed devices/Read)

### Connectivity requirements

For diagnostics to be able to upload successfully from the client, make sure that the URL for your region isn't blocked on the network:

- Europe: `lgmsapeweu.blob.core.windows.net`
- Americas: `lgmsapewus2.blob.core.windows.net`
- East Asia: `lgmsapesea.blob.core.windows.net`
- Australia: `lgmsapeaus.blob.core.windows.net`
- India: `lgmsapeind.blob.core.windows.net`

Devices must be online and able to communicate with the service during diagnostics.


> [!NOTE]
>  Intune App Protection logs are available to download from the diagnostics tab in the **Troubleshooting** pane. However, M365 remote application diagnostics are only available to their specific support engineers.
>
> Devices don't have to be managed by MDM (Mobile device management) to have Intune app protection or M365 app diagnostics collected, only managed by an Intune app protection policy.
>
> The data is stored in Microsoft support systems and isn't subject to Intune data management policies or protections. Some applications might collect and store data using systems other than Intune.

## How to collect diagnostics

::: zone pivot="android,ios"

The Microsoft 365 remote application diagnostics enables admins to request Intune app protection diagnostics and Microsoft 365 application diagnostics (where applicable).

Admins can find this report in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) by selecting **Troubleshooting + support** > **Troubleshoot** > *select a user* > **Summary** > *App protection**. This feature is exclusive to applications that are under Intune app protection management. If supported, the application specific logs are gathered and stored within dedicated storage solutions for each application.

Applications with support for M365 application diagnostics:

::: zone-end

::: zone pivot="android"

- Outlook
- Teams
- OneDrive
- Microsoft Edge

::: zone-end

::: zone pivot="ios"

- Outlook
- Teams
- OneDrive
- Microsoft Edge
- Microsoft Word
- Microsoft Excel
- Microsoft PowerPoint
- OneNote
- Microsoft 365 (Office)

::: zone-end

::: zone pivot="android,ios"

Requirements to collect diagnostics from an M365 application:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Navigate to **Tenant administration** > **Device diagnostics** > Make sure the third setting is enabled.
3. Create and deploy an Intune App Protection policy to a user, more information [here](../apps/app-protection-policies.md).
4. Confirm the application has been managed by Intune App Protection policy. You can check locally on the device and/or by loading the user into the Intune Troubleshooting Pane and opening the App Protection summary page.

To use the *Collect diagnostics* action:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431)
2. Navigate to **Troubleshooting + support** > **Troubleshoot** > *select a user*.
3. On the **Summary** page, select **App Protection** >  **Checked-in**.
4. Find the application to collect diagnostics on and use the **"..."** option to select **Collect diagnostics**.
5. When prompted, select **Yes**.

To check status of the *Collect diagnostics* action:

1. On the "App Protection" summary, select **refresh**.
2. Find the application you want the status for and select the hyperlink in the Diagnostic Status column.

To download diagnostics:

1. Navigate to **Troubleshooting + support** > **Troubleshoot** > *select a user*.
2. On the **Summary** page, select the **Diagnostics** page and download the diagnostics.

> [!IMPORTANT]
> Diagnostic uploads exceeding 50 diagnostics or 4 MB in diagnostic data can't be downloaded directly from the Intune portal. For access to larger diagnostic uploads, reach out to [Microsoft Intune support](/mem/get-support).

Diagnostics take approximately 30 minutes to be delivered from an end user's device. The user might be required to close and reopen the app if prompted for a pin when opening the app for the diagnostics request to prompt.

::: zone-end

::: zone pivot="windows"

<!--1895390-->

The collect diagnostics remote action can also be configured to automatically collect and upload Windows devices logs upon a Windows Autopilot failure on a device. When a Windows Autopilot failure occurs, logs are processed on the failed device and then automatically captured and uploaded to Intune. A device can automatically capture one set of logs per day.

The diagnostic collection is stored for 28 days and then deleted. Each device can have up to 10 collections stored at one time.

*Collect diagnostics* is also available as a [bulk device action](../remote-actions/index.md#bulk-device-actions) that collects diagnostic logs from up to 25 Windows devices at a time.

> [!NOTE]
> Microsoft personnel might access device diagnostics to help troubleshooting and resolving incidents.

To use the *Collect diagnostics* action:

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of remote action icons. Select **Collect diagnostics**.
1. To confirm, select **Yes**. A pending notification appears on the device's **Overview** page.
1. To check the status of the action, select **Monitor** > **Device diagnostics**.
1. After the action completes, select **...** > **Download** in the row for the action > **Yes**.
1. The data zip file is added to your download tray and you can save it to your computer.

### Diagnostics collection on Windows Autopilot failure
<!--1895390-->

Windows Autopilot diagnostics are automatically captured when devices experience a failure as long as the Windows Autopilot automatic capture diagnostic feature is enabled.

To view the diagnostics collected after a Windows Autopilot failure:

1. In the [Microsoft Intune admin center][INT-AC], select **Devices** > [**All devices**][INT-ALLD].
1. From the devices list, select a device.
1. At the top of the device overview pane, find the row of remote action icons. Select **Diagnostics** > **Download**.
1. The data zip file is added to your download tray and you can save it to your computer.

### Data collected

<!--1895390-->
While there's no intent to collect personal data, diagnostics might include user identifiable information such as user or device name.

If you install [KB5011543](https://support.microsoft.com/topic/march-22-2022-kb5011543-os-builds-19042-1620-19043-1620-and-19044-1620-preview-4fe2d1c0-720f-47fe-9523-75339bc107a1) on Windows 10 or [KB5011563](https://support.microsoft.com/topic/march-28-2022-kb5011563-os-build-22000-593-preview-40df54c9-b5a9-42e5-ae1c-9a33ff91ca91) on Windows 11, the format of the zip file is simpler including:

- A flattened structure where the logs collected are named to match the data collected
- When multiple files are collected, a folder is created.

This following list is the same order as the diagnostic zip. Each collection contains the following data:

# [:::image type="icon" source="../../media/icons/windows/registry.svg"::: **Registry keys**](#tab/reg)

|Registry key|
|-|
|`HKLM\SOFTWARE\Microsoft\CloudManagedUpdate`|
|`HKLM\SOFTWARE\Microsoft\EPMAgent`|
|`HKLM\SOFTWARE\Microsoft\PolicyManager\current\device\DeviceHealthMonitoring`|
|`HKLM\SOFTWARE\Microsoft\IntuneManagementExtension`|
|`HKLM\SOFTWARE\Microsoft\SystemCertificates\AuthRoot`|
|`HKLM\SOFTWARE\Microsoft\Windows Advanced Threat Protection`|
|`HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Authentication\LogonUI`|
|`HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings`|
|`HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall`|
|`HKLM\SOFTWARE\Microsoft\DeviceInventory`|
|`HKLM\SOFTWARE\Policies`|
|`HKLM\SOFTWARE\Policies\Microsoft\Cryptography\Configuration\SSL`|
|`HKLM\SOFTWARE\Policies\Microsoft\Windows Advanced Threat Protection`|
|`HKLM\SOFTWARE\WOW6432Node\Microsoft\Windows\CurrentVersion\Uninstall`|
|`HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL`|
|`HKLM\SYSTEM\CurrentControlSet\Services\SharedAccess\Parameters\FirewallPolicy\Mdm`|
|`HKLM\SYSTEM\Setup\SetupDiag\Results`|

# [:::image type="icon" source="../../media/icons/windows/cmd.svg"::: **Commands**](#tab/cmds)

|Command|
|-|
|`%programfiles%\windows defender\mpcmdrun.exe -GetFiles`|
|`%windir%\system32\certutil.exe -store`|
|`%windir%\system32\certutil.exe -store -user my`|
|`%windir%\system32\Dsregcmd.exe /status`|
|`%windir%\system32\ipconfig.exe /all`|
|`%windir%\system32\mdmdiagnosticstool.exe`|
|`%windir%\system32\msinfo32.exe /report %temp%\MDMDiagnostics\msinfo32.log`|
|`%windir%\system32\netsh.exe advfirewall show allprofiles`|
|`%windir%\system32\netsh.exe advfirewall show global`|
|`%windir%\system32\netsh.exe lan show profiles`|
|`%windir%\system32\netsh.exe winhttp show proxy`|
|`%windir%\system32\netsh.exe wlan show profiles`|
|`%windir%\system32\netsh.exe wlan show wlanreport`|
|`%windir%\system32\ping.exe -n 50 localhost`|
|`%windir%\system32\pnputil.exe /enum-drivers`|
|`%windir%\system32\powercfg.exe /batteryreport /output %temp%\MDMDiagnostics\battery-report.html`|
|`%windir%\system32\powercfg.exe /energy /output %temp%\MDMDiagnostics\energy-report.html`|

# [:::image type="icon" source="../../media/icons/windows/eventvwr.svg"::: **Event Viewer**](#tab/events)

|Event|
|-|
|`Application`|
|`Microsoft-Windows-AppLocker/EXE and DLL`|
|`Microsoft-Windows-AppLocker/MSI and Script`|
|`Microsoft-Windows-AppLocker/Packaged app-Deployment`|
|`Microsoft-Windows-AppLocker/Packaged app-Execution`|
|`Microsoft-Windows-AppxPackaging/Operational`|
|`Microsoft-Windows-Bitlocker/Bitlocker Management`|
|`Microsoft-Windows-HelloForBusiness/Operational`|
|`Microsoft-Windows-SENSE/Operational`|
|`Microsoft-Windows-SenseIR/Operational`|
|`Microsoft-Windows-Windows Firewall With Advanced Security/Firewall`|
|`Microsoft-Windows-WinRM/Operational`|
|`Microsoft-Windows-WMI-Activity/Operational`|
|`Microsoft-Windows-AppXDeployment/Operational`|
|`Microsoft-Windows-AppXDeploymentServer/Operational`|
|`Setup`|
|`System`|

# [:::image type="icon" source="../../media/icons/windows/explorer.svg"::: **Files**](#tab/files)

|Path|
|-|
|`%ProgramData%\Microsoft\DiagnosticLogCSP\Collectors\*.etl`|
|`%ProgramFiles%\Microsoft EPM Agent\Logs\*.*`|
|`%Program Files%\Microsoft Device Inventory Agent\Logs`|
|`%ProgramData%\Microsoft\IntuneManagementExtension\Logs\*.*`|
|`%ProgramData%\Microsoft\Windows Defender\Support\MpSupportFiles.cab`|
|`%ProgramData%\Microsoft\Windows\WlanReport\wlan-report-latest.html`|
|`%ProgramData%\USOShared\logs\system\*.etl`|
|`%ProgramData Microsoft Update Health Tools\Logs\*.etl`|
|`%temp%\CloudDesktop\*.log`|
|`%temp%\MDMDiagnostics\battery-report.html`|
|`%temp%\MDMDiagnostics\energy-report.html`|
|`%temp%\MDMDiagnostics\mdmlogs-<Date/Time>.cab`|
|`%temp%\MDMDiagnostics\msinfo32.log`|
|`%windir%\ccm\logs\*.log`|
|`%windir%\ccmsetup\logs\*.log`|
|`%windir%\logs\CBS\cbs.log`|
|`%windir%\logs\measuredboot\*.*`|
|`%windir%\logs\Panther\unattendgc\setupact.log`|
|`%windir%\logs\SoftwareDistribution\ReportingEvent\measuredboot\*.log`|
|`%windir%\Logs\SetupDiag\SetupDiagResults.xml`|
|`%windir%\logs\WindowsUpdate\*.etl`|
|`%windir%\SensorFramework\*.etl`|
|`%windir%\system32\config\systemprofile\AppData\Local\mdm\*.log`|
|`%windir%\temp\%computername%*.log`|
|`%windir%\temp\officeclicktorun*.log`|
|`%TEMP%\winget\defaultstate*.log`|

---

### Disable device diagnostics

The *collect diagnostics* remote action is enabled by default. You can disable the **Collect diagnostics** remote action for all devices by following these steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431)
2. Navigate to **Tenant administration** > **Device diagnostics**.
3. Change the control under **Device diagnostics are available for corporate-managed devices running Windows 10, version 1909 and later, or Windows 11.** to **Disabled**.

     :::image type="content" source="images/disable-device-diagnostics.png" alt-text="Screenshot that shows the Device diagnostics pane with the highlighted control for device diagnostics set to Disabled." lightbox="images/disable-device-diagnostics.png":::

### Disable Windows Autopilot automatic collection of diagnostics
<!--1895390-->

Windows Autopilot automatic diagnostic capture is enabled by default. You can disable Windows Autopilot automatic diagnostic capture by following these steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431)
2. Navigate to **Tenant administration** > **Device diagnostics**.
3. Change the control under **Automatically capture diagnostics when devices experience a failure during the Autopilot process on Windows 10 version 1909 or later and Windows 11. Diagnostics may include user identifiable information such as user or device name (preview).** to **Disabled**.

     :::image type="content" source="images/disable-autopilot-diagnostics.png" alt-text="Screenshot that shows the Device diagnostics pane with the highlighted control for Windows Autopilot automatic diagnostics collection set to Disabled." lightbox="images/disable-autopilot-diagnostics.png":::

### Known issues with device diagnostics

Currently there are the two main issues that could cause device diagnostics to fail:

1. A time-out could occur on devices without patches [KB4601315](https://support.microsoft.com/topic/february-9-2021-kb4601315-os-build-18363-1377-bdd71d2f-6729-e22a-3150-64324e4ab954) or [KB4601319](https://support.microsoft.com/topic/february-9-2021-kb4601319-os-builds-19041-804-and-19042-804-87fc8417-4a81-0ebb-5baa-40cfab2fbfde). These patches contain a fix to the DiagnosticLog CSP that prevents time out during upload. After the update installs, make sure to reboot your device.
1. The device wasn't able to receive the device action within a 24-hour window. If the device is offline or turned off, it could cause a failure.

::: zone-end

## Reference links

- Microsoft Graph API:
  - [createDeviceLogCollectionRequest action][GRAPH-1]
  - [createDownloadUrl action][GRAPH-2]
  - [downloadAppDiagnostics action][GRAPH-3]
  - [appDiagnostics function][GRAPH-4]

<!--links-->

<!-- graph -->

[GRAPH-1]: /graph/api/intune-devices-manageddevice-createdevicelogcollectionrequest
[GRAPH-2]: /graph/api/intune-devices-applogcollectionrequest-createdownloadurl
[GRAPH-3]: /graph/api/intune-devices-manageddevice-downloadappdiagnostics
[GRAPH-4]: /graph/api/intune-devices-manageddevice-appdiagnostics

<!-- admin center -->

[INT-AC]: https://go.microsoft.com/fwlink/?linkid=2109431
[INT-ALLD]: https://go.microsoft.com/fwlink/?linkid=2333814


<!-- roles -->

[ENT-R1]: /entra/identity/role-based-access-control/permissions-reference#intune-administrator

[INT-R1]: /intune/intune-service/fundamentals/role-based-access-control-reference#help-desk-operator
[INT-R2]: /intune/intune-service/fundamentals/role-based-access-control-reference#school-administrator
[INT-R4]: /intune/intune-service/fundamentals/role-based-access-control-reference#endpoint-security-manager
[INT-RC]: /intune/intune-service/fundamentals/create-custom-role

