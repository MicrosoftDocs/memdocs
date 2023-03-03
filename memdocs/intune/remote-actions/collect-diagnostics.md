---
# required metadata

title: Collect diagnostics from a Windows device
titleSuffix: Microsoft Intune
description: Learn how to collect diagnostics from a Windows device.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/05/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: jlynn
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Collect diagnostics from a Windows device

The **Collect diagnostics** remote action lets you collect and download Windows device logs without interrupting the user. Only non-user locations and file types are accessed.

<!--1895390-->
The **Collect diagnostics** remote action can also be configured to automatically collect and upload Windows devices logs upon an Autopilot failure on a device. When an Autopilot failure occurs, logs will be processed on the failed device and then automatically captured and uploaded to Intune.

The diagnostic collection is stored for 28 days and then deleted. Each device can have up to 10 collections stored at one time.

*Collect diagnostics* is also available as a [Bulk device action](../remote-actions/bulk-device-actions.md) that collects diagnostic logs from up to 25 Windows devices at a time.

> [!NOTE]
> Microsoft personnel may access device diagnostics to assist in troubleshooting and resolving incidents.

## Requirements

The *Collect diagnostics* remote action is supported for:

- Intune or co-managed devices.
- Windows 10 version 1909 and later.
- Windows 11
- Microsoft HoloLens 2 2004 and later.
- Global Admins, Intune Admins, or a role with **Collect diagnostics** (under **Remote tasks**) and **Read** (under **Device compliance policies**) permissions.
- Corporate-owned devices.
- Devices that are online and able to communicate with the service during diagnostics. 

> [!NOTE]
> For diagnostics to be able to upload successfully from the client, make sure that the URL `lgmsapeweu.blob.core.windows.net` is not blocked on the network.

## Collect diagnostics

To use the *Collect diagnostics* action:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431)
2. Navigate to **Devices** > **Windows** > select a supported device.
3. On the device’s **Overview** page, select **…** >  **Collect diagnostics** > **Yes**. A pending notification appears on the device’s **Overview** page.
4. To see the status of the action, select **Device diagnostics monitor**.
5. After the  action completes, select **Download** in the row for the action > **Yes**.
6. The data zip file is added to your download tray and you can save it to your computer.

## Diagnostics collection on Autopilot failure
<!--1895390-->

 For Autopilot diagnostics collection, no additional action is required. Autopilot diagnostics will be automatically captured when devices experience a failure as long as the Autopilot automatic capture diagnostic feature is enabled.

To view the diagnostics collected after an Autopilot failure:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431)
2. Navigate to **Devices** > **Monitor** > **Autopilot deployments (preview)**.
3. In the middle pane, select a device.
4. On the right hand **Properties** pane, under **Device Diagnostics**, select **Download**.
5. The data zip file is added to your download tray and you can save it to your computer.

## Data collected

<!--1895390-->
While there's no intent to collect personal data, diagnostics may include user identifiable information such as user or device name.

If you've installed [KB5011543](https://support.microsoft.com/topic/march-22-2022-kb5011543-os-builds-19042-1620-19043-1620-and-19044-1620-preview-4fe2d1c0-720f-47fe-9523-75339bc107a1) on Windows 10 or [KB5011563](https://support.microsoft.com/topic/march-28-2022-kb5011563-os-build-22000-593-preview-40df54c9-b5a9-42e5-ae1c-9a33ff91ca91) on Windows 11, the format of the zip file will be simpler including:

- A flattened structure where the logs collected are named to match the data collected
- When multiple files are collected a folder is created.  

This list below is the same order as the diagnostic zip.  Each collection contains the following data:

Registry Keys:

- HKLM\SOFTWARE\Microsoft\CloudManagedUpdate
- HKLM\SOFTWARE\Microsoft\IntuneManagementExtension
- HKLM\SOFTWARE\Microsoft\SystemCertificates\AuthRoot
- HKLM\SOFTWARE\Microsoft\Windows Advanced Threat Protection
- HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Authentication\LogonUI
- HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings
- HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall
- HKLM\SOFTWARE\Policies
- HKLM\SOFTWARE\Policies\Microsoft\Cryptography\Configuration\SSL
- HKLM\SOFTWARE\Policies\Microsoft\Windows Advanced Threat Protection
- HKLM\SOFTWARE\WOW6432Node\Microsoft\Windows\CurrentVersion\Uninstall
- HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL
- HKLM\SYSTEM\CurrentControlSet\Services\SharedAccess\Parameters\FirewallPolicy\Mdm

Commands:

- %programfiles%\windows defender\mpcmdrun.exe -GetFiles
- %windir%\system32\certutil.exe -store
- %windir%\system32\certutil.exe -store -user my
- %windir%\system32\Dsregcmd.exe /status
- %windir%\system32\ipconfig.exe /all
- %windir%\system32\mdmdiagnosticstool.exe 
- %windir%\system32\msinfo32.exe /report %temp%\MDMDiagnostics\msinfo32.log
- %windir%\system32\netsh.exe advfirewall show allprofiles
- %windir%\system32\netsh.exe advfirewall show global
- %windir%\system32\netsh.exe lan show profiles
- %windir%\system32\netsh.exe winhttp show proxy
- %windir%\system32\netsh.exe wlan show profiles
- %windir%\system32\netsh.exe wlan show wlanreport
- %windir%\system32\ping.exe -n 50 localhost
- %windir%\system32\powercfg.exe /batteryreport /output %temp%\MDMDiagnostics\battery-report.html
- %windir%\system32\powercfg.exe /energy /output %temp%\MDMDiagnostics\energy-report.html

Event Viewers:

- Application
- Microsoft-Windows-AppLocker/EXE and DLL
- Microsoft-Windows-AppLocker/MSI and Script
- Microsoft-Windows-AppLocker/Packaged app-Deployment
- Microsoft-Windows-AppLocker/Packaged app-Execution
- Microsoft-Windows-AppxPackaging/Operational
- Microsoft-Windows-Bitlocker/Bitlocker Management
- Microsoft-Windows-HelloForBusiness/Operational
- Microsoft-Windows-SENSE/Operational
- Microsoft-Windows-SenseIR/Operational
- Microsoft-Windows-Windows Firewall With Advanced Security/Firewall
- Microsoft-Windows-WinRM/Operational
- Microsoft-Windows-WMI-Activity/Operational
- Setup
- System

Files:

- %ProgramData%\Microsoft\DiagnosticLogCSP\Collectors\\*.etl
- %ProgramData%\Microsoft\IntuneManagementExtension\Logs\\\*.*
- %ProgramData%\Microsoft\Windows Defender\Support\MpSupportFiles.cab
- %ProgramData%\Microsoft\Windows\WlanReport\wlan-report-latest.html
- %ProgramData Microsoft Update Health Tools\Logs\\*.etl
- %temp%\MDMDiagnostics\battery-report.html
- %temp%\MDMDiagnostics\energy-report.html
- %temp%\MDMDiagnostics\mdmlogs-<Date/Time>.cab
- %temp%\MDMDiagnostics\msinfo32.log
- %windir%\ccm\logs\\*.log
- %windir%\ccmsetup\logs\\*.log
- %windir%\logs\CBS\cbs.log
- %windir%\logs\measuredboot\\\*.*
- %windir%\logs\WindowsUpdate\\*.etl
- %windir%\temp\%computername%*.log
- %windir%\temp\officeclicktorun*.log

## Disable device diagnostics

The **Collect diagnostics** remote action is enabled by default. You can disable the **Collect diagnostics** remote action for all devices by following these steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431)
2. Navigate to **Tenant administration** > **Device diagnostics**.
3. Change the control under **Device diagnostics are available for corporate-managed devices running Windows 10, version 1909 and later, or Windows 11.** to **Disabled**.

     :::image type="content" source="./media/collect-diagnostics/disable-device-diagnostics.png" alt-text="Screenshot that shows the Device diagnostics pane with the highlighted control for device diagnostics set to Disabled.":::

## Disable Autopilot automatic collection of diagnostics
<!--1895390-->

Autopilot automatic diagnostic capture is enabled by default. You can disable Autopilot automatic diagnostic capture by following these steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431)
2. Navigate to **Tenant administration** > **Device diagnostics**.
3. Change the control under **Automatically capture diagnostics when devices experience a failure during the Autopilot process on Windows 10 version 1909 or later and Windows 11. Diagnostics may include user identifiable information such as user or device name (preview).** to **Disabled**.

     :::image type="content" source="./media/collect-diagnostics/disable-autopilot-diagnostics.png" alt-text="Screenshot that shows the Device diagnostics pane with the highlighted control for Autopilot automatic diagnostics collection set to Disabled.":::

## WinGet troubleshooting using diagnostic files
[WinGet](/windows/package-manager/winget/) is a command line tool that enables you to discover, install, upgrade, remove, and configure applications on Windows 10 and Windows 11 devices. When working with [Win32 app management in Intune](../apps/apps-win32-app-management.md), you can use the following files to help troubleshoot WinGet:
- *%TEMP%\winget\defaultstate\*.log*
- *Microsoft-Windows-AppXDeployment/Operational*
- *Microsoft-Windows-AppXDeploymentServer/Operational*

## Known issues with device diagnostics

Currently there are the two main issues that may cause device diagnostics to fail:

1. A timeout may occur on devices without patches [KB4601315](https://support.microsoft.com/topic/february-9-2021-kb4601315-os-build-18363-1377-bdd71d2f-6729-e22a-3150-64324e4ab954) or [KB4601319](https://support.microsoft.com/topic/february-9-2021-kb4601319-os-builds-19041-804-and-19042-804-87fc8417-4a81-0ebb-5baa-40cfab2fbfde).  These patches contain a fix to the DiagnosticLog CSP that prevents timeout during upload.  After the update installs, make sure to reboot your device.
2. The device wasn't able to receive the device action within a 24-hour window. If the device is offline or turned off, it may cause a failure.
