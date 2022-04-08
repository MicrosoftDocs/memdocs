---
# required metadata

title: Collect diagnostics from a Windows device
titleSuffix: Microsoft Intune
description: Learn how to collect diagnostics from a Windows device.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 12/07/2021
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

No personal information is collected. This list below is the same order as the diagnostic zip.  Each collection contains the following data:

Registry Keys:

1. HKLM\Software\Microsoft\IntuneManagementExtension
2. HKLM\SOFTWARE\Microsoft\SystemCertificates\AuthRoot
3. HKLM\SOFTWARE\Microsoft\Windows Advanced Threat Protection
4. HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Authentication\LogonUI
5. HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Internet Settings
6. HKLM\Software\Microsoft\Windows\CurrentVersion\Uninstall
7. HKLM\Software\Policies
8. HKLM\SOFTWARE\Policies\Microsoft\Cryptography\Configuration\SSL
9. HKLM\SOFTWARE\Policies\Microsoft\Windows Advanced Threat Protection
10. HKLM\SOFTWARE\WOW6432Node\Microsoft\Windows\CurrentVersion\Uninstall
11. HKLM\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL

Commands:

12. %programfiles%\windows defender\mpcmdrun.exe -GetFiles
13. %windir%\system32\certutil.exe -store
14. %windir%\system32\certutil.exe -store -user my
15. %windir%\system32\Dsregcmd.exe /status
16. %windir%\system32\ipconfig.exe /all
17. %windir%\system32\mdmdiagnosticstool.exe 
18. %windir%\system32\msinfo32.exe /report %temp%\MDMDiagnostics\msinfo32.log
19. %windir%\system32\netsh.exe advfirewall show allprofiles
20. %windir%\system32\netsh.exe advfirewall show global
21. %windir%\system32\netsh.exe lan show profiles
22. %windir%\system32\netsh.exe winhttp show proxy
23. %windir%\system32\netsh.exe wlan show profiles
24. %windir%\system32\netsh.exe wlan show wlanreport
25. %windir%\system32\ping.exe -n 50 localhost
26. %windir%\system32\powercfg.exe /batteryreport /output %temp%\MDMDiagnostics\battery-report.html
27. %windir%\system32\powercfg.exe /energy /output %temp%\MDMDiagnostics\energy-report.html

Event Viewers:

28. Application
29. Microsoft-Windows-AppLocker/EXE and DLL
30. Microsoft-Windows-AppLocker/MSI and Script
31. Microsoft-Windows-AppLocker/Packaged app-Deployment
32. Microsoft-Windows-AppLocker/Packaged app-Execution
33. Microsoft-Windows-AppxPackaging/Operational
34. Microsoft-Windows-Bitlocker/Bitlocker Management
35. Microsoft-Windows-HelloForBusiness/Operational
36. Microsoft-Windows-SENSE/Operational
37. Microsoft-Windows-SenseIR/Operational
38. Microsoft-Windows-Windows Firewall With Advanced Security/Firewall
39. Setup
40. System

Files:

41. %ProgramData%\Microsoft\DiagnosticLogCSP\Collectors\*.etl
42. %ProgramData%\Microsoft\IntuneManagementExtension\Logs\*.*
43. %ProgramData%\Microsoft\Windows Defender\Support\MpSupportFiles.cab
44. %ProgramData%\Microsoft\Windows\WlanReport\wlan-report-latest.html
45. %temp%\MDMDiagnostics\battery-report.html
46. %temp%\MDMDiagnostics\energy-report.html
47. %temp%\MDMDiagnostics\mdmlogs-<Date/Time>.cab
48. %temp%\MDMDiagnostics\msinfo32.log
49. %windir%\ccm\logs\*.log
50. %windir%\ccmsetup\logs\*.log
51. %windir%\logs\CBS\cbs.log
52. %windir%\logs\measuredboot\*.*
53. %windir%\Logs\WindowsUpdate\*.etl
54. %windir%\temp\%computername%*.log
55. %windir%\temp\officeclicktorun*.log

## Disable device diagnostics

You can disable the **Collect diagnostics** remote action for all devices by following these steps:

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Tenant administration** > **Device diagnostics**.
2. Change the control to **Disabled**.

     :::image type="content" source="./media/collect-diagnostics/disable-device-diagnostics.png" alt-text="Screenshot that shows the Device diagnostics pane with the highlighted control set to Disabled.":::

## Known issues with device diagnostics

Currently there are the two main issues that may cause device diagnostics to fail:

1. A timeout may occur on devices without patches [KB4601315](https://support.microsoft.com/topic/february-9-2021-kb4601315-os-build-18363-1377-bdd71d2f-6729-e22a-3150-64324e4ab954) or [KB4601319](https://support.microsoft.com/topic/february-9-2021-kb4601319-os-builds-19041-804-and-19042-804-87fc8417-4a81-0ebb-5baa-40cfab2fbfde).  These patches contain a fix to the DiagnosticLog CSP that prevents timeout during upload.  After the update installs, make sure to reboot your device.
2. The device wasn't able to receive the device action within a 24-hour window. If the device is offline or turned off this may cause a failure.
