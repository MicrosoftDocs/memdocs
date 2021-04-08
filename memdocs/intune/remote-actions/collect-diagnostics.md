---
# required metadata

title: Collect diagnostics from a Windows device
titleSuffix: Microsoft Intune
description: Learn how to collect diagnostics from a Windows device.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 02/26/2021
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

## Requirements

The **Collect diagnostics** remote action is supported for:
- Intune or Co-Managed devices.
- Windows 10 version 1909 and later.
- Microsoft HoloLens 2 2004 and later.
- Global Admins, Intune Admins, or a role with **Collect diagnostics** permissions (under **Remote tasks**).
- Corporate-owned devices.
- Devices that are online and able to communicate with the service during diagnostics.

## Collect diagnostics

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Windows** > select a supported device.
2. On the device’s **Overview** page, select **…** >  **Collect diagnostics** > **Yes**. A pending notification appears on the device’s **Overview** page.
3. To see the status of the action, select **Device diagnostics monitor**.
4. After the  action completes, select **Download** in the row for the action > **Yes**.
5. The data zip file is added to your download tray and you can save it to your computer.

## Data collected

No personal information is collected. This list below is the same order as the diagnostic zip file.  Each collection contains the following data:

Registry Keys:

- HKLM\Software\Microsoft\IntuneManagementExtension
- HKLM\SOFTWARE\Microsoft\SystemCertificates\AuthRoot
- HKLM\SOFTWARE\Microsoft\Windows Advanced Threat Protection
- HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Authentication\LogonUI
- HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings
- HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall
- HKLM\Software\Policies
- HKLM\SOFTWARE\Policies\Microsoft\Cryptography\Configuration\SSL
- HKLM\SOFTWARE\Policies\Microsoft\Windows Advanced Threat Protection
- HKLM\SOFTWARE\WOW6432Node\Microsoft\Windows\CurrentVersion\Uninstall
- HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

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
- Microsoft-Windows-Bitlocker/Bitlocker Management
- Microsoft-Windows-SENSE/Operational
- Microsoft-Windows-SenseIR/Operational
- Setup
- System

Files:
 
- %ProgramData%\Microsoft\DiagnosticLogCSP\Collectors\*.etl
- %ProgramData%\Microsoft\IntuneManagementExtension\Logs\*.*
- %ProgramData%\Microsoft\Windows Defender\Support\MpSupportFiles.cab
- %ProgramData%\Microsoft\Windows\WlanReport\wlan-report-latest.html
- %temp%\MDMDiagnostics\battery-report.html
- %temp%\MDMDiagnostics\energy-report.html
- %temp%\MDMDiagnostics\mdmlogs-<Date/Time>.cab
- %temp%\MDMDiagnostics\msinfo32.log
- %windir%\ccm\logs\*.log
- %windir%\ccmsetup\logs\*.log
- %windir%\logs\CBS\cbs.log
- %windir%\logs\measuredboot\*.*
- %windir%\Logs\WindowsUpdate\*.etl

## Disable device diagnostics
You can disable the **Collect diagnostics** remote action for all devices by following these steps:
1.	Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration** > **Device diagnostics**.
2.	Change the control to **Disabled**.

## Known issues with device diagnostics
Currently there are the two main issues which may cause device diagnostics to fail:  
1. A timeout may occur on devices without patches [KB4601315](https://support.microsoft.com/topic/february-9-2021-kb4601315-os-build-18363-1377-bdd71d2f-6729-e22a-3150-64324e4ab954) or [KB4601319](https://support.microsoft.com/topic/february-9-2021-kb4601319-os-builds-19041-804-and-19042-804-87fc8417-4a81-0ebb-5baa-40cfab2fbfde).  These patches contain a fix to the DiagnosticLog CSP which prevents timeout during upload.  After installing the update please make sure to reboot your device.
2. The device wasn't able to receive the device action within a 12 hour window.  If the device is offline or turned off this may cause a failure.
