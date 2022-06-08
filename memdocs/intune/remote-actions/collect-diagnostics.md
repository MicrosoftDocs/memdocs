---
# required metadata

title: Collect diagnostics from a Windows device
titleSuffix: Microsoft Intune
description: Learn how to collect diagnostics from a Windows device.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/08/2022
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
ms.collection: M365-identity-device-management
---

# Collect diagnostics from a Windows device

The **Collect diagnostics** remote action lets you collect and download Windows device logs without interrupting the user. Only non-user locations and file types can be accessed, so no personal information is collected.

The diagnostic collection is stored for 28 days and then deleted. Each device can have up to 10 collections stored at one time.

*Collect diagnostics* is also available as a [Bulk device action](../remote-actions/bulk-device-actions.md) that collects diagnostic logs from up to 25 Windows devices at a time.

## Requirements

The *Collect diagnostics* remote action is supported for:

- Intune or co-managed devices.
- Windows 10 version 1909 and later.
- Windows 11
- Microsoft HoloLens 2 2004 and later.
- Global Admins, Intune Admins, or a role with **Collect diagnostics** (under **Remote tasks**) and **Read** (under **Device compliance policies**) permissions.
- Corporate-owned devices.
- Devices that are online and able to communicate with the service during diagnostics.

## Collect diagnostics

To use the *Collect diagnostics* action:

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Windows** > select a supported device.
2. On the device’s **Overview** page, select **…** >  **Collect diagnostics** > **Yes**. A pending notification appears on the device’s **Overview** page.
3. To see the status of the action, select **Device diagnostics monitor**.
4. After the  action completes, select **Download** in the row for the action > **Yes**.
5. The data zip file is added to your download tray and you can save it to your computer.

## Data collected

No personal information is collected. If you've installed [KB5011543](https://support.microsoft.com/topic/march-22-2022-kb5011543-os-builds-19042-1620-19043-1620-and-19044-1620-preview-4fe2d1c0-720f-47fe-9523-75339bc107a1) on Windows 10 or [KB5011563](https://support.microsoft.com/topic/march-28-2022-kb5011563-os-build-22000-593-preview-40df54c9-b5a9-42e5-ae1c-9a33ff91ca91) on Windows 11, the format of the zip file will be simpler, including a flattened structure where the logs collected are named to match the data collected, and when multiple files are collected a folder is created.  

This list below is the same order as the diagnostic zip.  Each collection contains the following data:

Registry Keys:

1. HKLM\SOFTWARE\Microsoft\CloudManagedUpdate
1. HKLM\SOFTWARE\Microsoft\IntuneManagementExtension
1. HKLM\SOFTWARE\Microsoft\SystemCertificates\AuthRoot
1. HKLM\SOFTWARE\Microsoft\Windows Advanced Threat Protection
1. HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Authentication\LogonUI
1. HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings
1. HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall
1. HKLM\SOFTWARE\Policies
1. HKLM\SOFTWARE\Policies\Microsoft\Cryptography\Configuration\SSL
1. HKLM\SOFTWARE\Policies\Microsoft\Windows Advanced Threat Protection
1. HKLM\SOFTWARE\WOW6432Node\Microsoft\Windows\CurrentVersion\Uninstall
1. HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

Commands:

1. %programfiles%\windows defender\mpcmdrun.exe -GetFiles
1. %windir%\system32\certutil.exe -store
1. %windir%\system32\certutil.exe -store -user my
1. %windir%\system32\Dsregcmd.exe /status
1. %windir%\system32\ipconfig.exe /all
1. %windir%\system32\mdmdiagnosticstool.exe 
1. %windir%\system32\msinfo32.exe /report %temp%\MDMDiagnostics\msinfo32.log
1. %windir%\system32\netsh.exe advfirewall show allprofiles
1. %windir%\system32\netsh.exe advfirewall show global
1. %windir%\system32\netsh.exe lan show profiles
1. %windir%\system32\netsh.exe winhttp show proxy
1. %windir%\system32\netsh.exe wlan show profiles
1. %windir%\system32\netsh.exe wlan show wlanreport
1. %windir%\system32\ping.exe -n 50 localhost
1. %windir%\system32\powercfg.exe /batteryreport /output %temp%\MDMDiagnostics\battery-report.html
1. %windir%\system32\powercfg.exe /energy /output %temp%\MDMDiagnostics\energy-report.html

Event Viewers:

1. Application
1. Microsoft-Windows-AppLocker/EXE and DLL
1. Microsoft-Windows-AppLocker/MSI and Script
1. Microsoft-Windows-AppLocker/Packaged app-Deployment
1. Microsoft-Windows-AppLocker/Packaged app-Execution
1. Microsoft-Windows-AppxPackaging/Operational
1. Microsoft-Windows-Bitlocker/Bitlocker Management
1. Microsoft-Windows-HelloForBusiness/Operational
1. Microsoft-Windows-SENSE/Operational
1. Microsoft-Windows-SenseIR/Operational
1. Microsoft-Windows-Windows Firewall With Advanced Security/Firewall
1. Setup
1. System

Files:

1. %ProgramData%\Microsoft\DiagnosticLogCSP\Collectors\*.etl
1. %ProgramData%\Microsoft\IntuneManagementExtension\Logs\*.*
1. %ProgramData%\Microsoft\Windows Defender\Support\MpSupportFiles.cab
1. %ProgramData%\Microsoft\Windows\WlanReport\wlan-report-latest.html
1. %ProgramData Microsoft Update Health Tools\Logs\*.etl
1. %temp%\MDMDiagnostics\battery-report.html
1. %temp%\MDMDiagnostics\energy-report.html
1. %temp%\MDMDiagnostics\mdmlogs-<Date/Time>.cab
1. %temp%\MDMDiagnostics\msinfo32.log
1. %windir%\ccm\logs\*.log
1. %windir%\ccmsetup\logs\*.log
1. %windir%\logs\CBS\cbs.log
1. %windir%\logs\measuredboot\*.*
1. %windir%\Logs\WindowsUpdate\*.etl
1. %windir%\temp\%computername%*.log
1. %windir%\temp\officeclicktorun*.log

## Disable device diagnostics

You can disable the **Collect diagnostics** remote action for all devices by following these steps:

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration** > **Device diagnostics**.
2. Change the control to **Disabled**.

     :::image type="content" source="./media/collect-diagnostics/disable-device-diagnostics.png" alt-text="Screenshot that shows the Device diagnostics pane with the highlighted control set to Disabled.":::

## Known issues with device diagnostics

Currently there are the two main issues that may cause device diagnostics to fail:

1. A timeout may occur on devices without patches [KB4601315](https://support.microsoft.com/topic/february-9-2021-kb4601315-os-build-18363-1377-bdd71d2f-6729-e22a-3150-64324e4ab954) or [KB4601319](https://support.microsoft.com/topic/february-9-2021-kb4601319-os-builds-19041-804-and-19042-804-87fc8417-4a81-0ebb-5baa-40cfab2fbfde).  These patches contain a fix to the DiagnosticLog CSP that prevents timeout during upload.  After the update installs, make sure to reboot your device.
2. The device wasn't able to receive the device action within a 24-hour window. If the device is offline or turned off this may cause a failure.
