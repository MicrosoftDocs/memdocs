---
# required metadata

title: Windows Antivirus policy settings for Microsoft Defender Antivirus for Intune | Microsoft Docs
description: See a list of the settings in the Microsoft Defender Antivirus profile for Windows devices. You can configure these settings as part of Endpoint security Antivirus policy in Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/06/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: laarrizz

---

# Settings for Microsoft Defender Antivirus policy in Microsoft Intune for Windows devices

> [!NOTE]  
> This article details the settings in the  Microsoft Defender Antivirus and Microsoft Defender Antivirus Exclusions profiles for the *Windows 10 and later* platform for endpoint security Antivirus policy. Beginning on April 5, 2022, the *Windows 10 and later* platform was replaced by the *Windows 10, Windows 11, and Windows Server* platform. Although you can no longer create new instances of the original profile, you can continue to edit and use your existing profiles. The settings details in this article apply to those deprecated profiles. 

View details about the [endpoint security](../protect/endpoint-security-policy.md) antivirus policy settings you can configure for the Microsoft Defender Antivirus profile for Windows 10 and later in Microsoft Intune.  

These settings are available in the following profiles:

- Microsoft Defender Antivirus

**Settings**:

- **Turn on cloud-delivered protection**  
  CSP: [AllowCloudProtection](/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  By default, Defender on Windows 10/11 desktop devices sends information to Microsoft about any problems it finds. Microsoft analyzes that information to learn more about problems affecting you and other customers, to offer improved solutions.

  - **Not configured** (*default*) - The setting is restored to the system default.
  - **No** - The setting is disabled. Device users can't change this setting.
  - **Yes** - Cloud-delivered protection is turned on.  Device users can't change this setting.

- **Cloud-delivered protection level**  
  CSP: [CloudBlockLevel](/windows/client-management/mdm/policy-csp-defender#defender-cloudblocklevel)

  Configure how aggressive Defender Antivirus is in blocking and scanning suspicious files.
  - **Not configured** (*default*) - Default Defender blocking level.
  - **High** - Aggressively block unknowns while optimizing client performance, which includes a greater chance of false positives.
  - **High plus** - Aggressively block unknowns and apply additional protection measures that might affect client performance.
  - **Zero tolerance** - Block all unknown executable files.

- **Defender cloud extended timeout in seconds**  
  CSP: [CloudExtendedTimeout](/windows/client-management/mdm/policy-csp-defender#defender-cloudextendedtimeout)

  Defender Antivirus automatically blocks suspicious files for 10 seconds while it scans them in the cloud to make sure they're safe. You can add up to 50 additional seconds to this timeout.

## Microsoft Defender Antivirus Exclusions

The following setting is only available in the Microsoft Defender Antivirus profile:

- **Defender local admin merge**  
  CSP: [Configuration/DisableLocalAdminMerge](/windows/client-management/mdm/defender-csp)

  This setting controls if exclusion list settings that are configured by a local administrator merge with managed settings from Intune policy. This setting applies to lists such as threats and exclusions.

  - **Not configured** *(default)* - Unique items defined in preference settings that are configured by a local administrator merge into the resulting effective policy. If there are conflicts, management settings from Intune policy override local preference settings.
  - **No** - Behavior is the same as *Not configured*.
  - **Yes** - Only items defined by management are used in the resulting effective policy. Managed settings override preference settings that are configured by the local administrator.

The following settings are available in the following profiles:

- Microsoft Defender Antivirus
- Microsoft Defender Antivirus Exclusions

For each setting in this group, you can expand the setting, select **Add**, and then specify a value for the exclusion.

- **Defender processes to exclude**  
  CSP: [ExcludedProcesses](/windows/client-management/mdm/policy-csp-defender#defender-excludedprocesses)

  Specify a list of files opened by processes to ignore during a scan. The process itself isn't excluded from the scan.

- **File extensions to exclude from scans and real-time protection**  
  CSP: [ExcludedExtensions](/windows/client-management/mdm/policy-csp-defender#defender-excludedextensions)

  Specify a list of file type extensions to ignore during a scan.

- **Defender files and folders to exclude**  
  CSP: [ExcludedPaths](/windows/client-management/mdm/policy-csp-defender#defender-excludedpaths)

  Specify a list of files and directory paths to ignore during a scan.

## Real-time protection

These settings are available in the following profiles:

- Microsoft Defender Antivirus

**Settings**:

- **Turn on real-time protection**  
  CSP: [AllowRealtimeMonitoring](/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

  Require Defender on Windows 10/11 desktop devices to use the real-time Monitoring functionality.
  - **Not configured** (*default*) - The setting is restored to the system default
  - **No** - The setting is disabled. Device users can't change this setting.
  - **Yes** - Enforce use of real-time monitoring. Device users can't change this setting.

- **Enable on access protection**  
  CSP: [AllowOnAccessProtection](/windows/client-management/mdm/policy-csp-defender#defender-allowonaccessprotection)

  Configure virus protection that's continuously active, as opposed to on demand.

  - **Not Configured** (*default*) - This policy doesn't alter the state of this setting on a device. The existing state on the device remains unchanged.
  - **No** - Block On Access Protection on devices. Device users can't change this setting.
  - **Yes** - On Access Protection is active on devices.

- **Monitoring for incoming and outgoing files**  
  CSP: [Defender/RealTimeScanDirection](/windows/client-management/mdm/policy-csp-defender)

  Configure this setting to determine which NTFS file and program activity is monitored.
  - **Monitor all files** (*default*)
  - **Only monitor incoming files**
  - **Only monitor outgoing files**

- **Turn on behavior monitoring**  
  CSP: [AllowBehaviorMonitoring](/windows/client-management/mdm/policy-csp-defender#defender-allowbehaviormonitoring)

  By default, Defender on Windows 10/11 desktop devices uses the Behavior Monitoring functionality.

  - **Not configured** (*default*) - The setting is restored to the system default.
  - **No** - The setting is disabled. Device users can't change this setting.
  - **Yes** - Enforce use of real-time behavior monitoring. Device users can't change this setting.

- **Turn on network protection**  
  CSP: [EnableNetworkProtection](/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

  Protect device users using any app from accessing phishing scams, exploit-hosting sites, and malicious content on the Internet. Protection includes preventing third-party browsers from connecting to dangerous sites.

  - **Not configured** (*default*) - The setting is restored to the system default.
  - **No** - The setting is disabled. Device users can't change this setting.
  - **Yes** - Network protection is turned on. Device users can't change this setting.

- **Scan all downloaded files and attachments**  
  CSP: [EnableNetworkProtection](/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

  Configure Defender to scan all downloaded files and attachments.

  - **Not configured** (*default*) - The setting is restored to the system default.
  - **No** - The setting is disabled. Device users can't change this setting.
  - **Yes** - Defender scans all downloaded files and attachments. Device users can't change this setting.

- **Scan scripts that are used in Microsoft browsers**  
  CSP: [AllowScriptScanning](/windows/client-management/mdm/policy-csp-defender)

  Configure Defender to scan scripts.

  - **Not configured** (*default*) - The setting is restored to the system default.
  - **No** - The setting is disabled. Device users can't change this setting.
  - **Yes** - Defender scans scripts. Device users can't change this setting.

- **Scan network files**  
  CSP: [AllowScanningNetworkFiles](/windows/client-management/mdm/policy-csp-defender#defender-allowscanningnetworkfiles)

  Configure Defender to scan network files.

  - **Not configured** (*default*) - The setting is restored to the system default.
  - **No** - The setting is disabled. Device users can't change this setting.
  - **Yes** - Turn on scanning of network files. Device users can't change this setting.

- **Scan emails**  
  CSP: [AllowEmailScanning](/windows/client-management/mdm/policy-csp-defender#defender-allowemailscanning)

  Configure Defender to scan incoming email.

  - **Not configured** (*default*) - The setting is restored to the system default.
  - **No** - The setting is disabled. Device users can't change this setting.
  - **Yes** - Turn on email scanning. Device users can't change this setting.

## Remediation

These settings are available in the following profiles:

- Microsoft Defender Antivirus

**Settings**:

- **Number of days (0-90) to keep quarantined malware**  
  CSP: [DaysToRetainCleanedMalware](/windows/client-management/mdm/policy-csp-defender#defender-daystoretaincleanedmalware)

  Specify the number of days from zero to 90 that the system stores quarantined items  before they're automatically removed. A value of zero keeps items in quarantine and doesn't automatically remove them.

- **Submit samples consent**  

  - **Not configured** (*default*)
  - **Send safe samples automatically**
  - **Always prompt**
  - **Never send**
  - **Send all samples automatically**

- **Action to take on potentially unwanted apps**  
  CSP: [PUAProtection](/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)

  Specify the level of detection for potentially unwanted applications (PUAs). Defender alerts users when potentially unwanted software is being downloaded or attempts to install on a device.

  - **Not configured** (*default*) - The setting is restored to the system default, which is PUA Protection OFF.
  - **Disable**
  - **Enable** - Detected items are blocked, and show in history along with other threats.
  - **Audit mode** - Defender detects potentially unwanted applications, but takes no action. You can review information about the applications Defender would have taken action against by searching for events that are created by Defender in the Event Viewer.

- **Actions for detected threats**  
  CSP: [ThreatSeverityDefaultAction](/windows/client-management/mdm/policy-csp-defender#defender-threatseveritydefaultaction)

  Specify the action that Defender takes for detected malware based on the malware's threat level.
  
  Defender classifies malware that it detects as one of the following severity levels:
  - **Low severity**
  - **Moderate severity**
  - **High severity**
  - **Severe severity**

  For each level, specify the action to take. The default for each severity level is *Not configured*.

  - **Not configured**
  - **Clean** - The service tries to recover files and try to disinfect.
  - **Quarantine** - Moves files to quarantine.
  - **Remove** - Removes files from the device.
  - **Allow** - Allows the file and doesn't take other actions.
  - **User defined** - The device user makes the decision on which action to take.
  - **Block** - Blocks file execution.

## Scan

These settings are available in the following profiles:

- Microsoft Defender Antivirus

**Settings**:

- **Scan archive files**  
  CSP: [AllowArchiveScanning](/windows/client-management/mdm/policy-csp-defender#defender-allowarchivescanning)

  Configure Defender to scan archive files, like ZIP or CAB files.

  - **Not configured** (*default*) - The setting returns to the client default, which is to scan archived files, however the user may disable setting.
Learn more
  - **No** - File archives aren't scanned. Device users can't change this setting.
  - **Yes** - Enable scans of archive files. Device users can't change this setting.

- **Use low CPU priority for scheduled scans**  
  CSP: [EnableLowCPUPriority](/windows/client-management/mdm/policy-csp-defender#defender-enablelowcpupriority)

  Configure CPU priority for scheduled scans.
  - **Not configured** (*default*) - The setting returns to the system default, in which no changes to CPU priority are made.
  - **No** - The setting is disabled. Device users can't change this setting.
  - **Yes** - Low CPU priority will be used during scheduled scans. Device users can't change this setting.

- **Disable catch-up full scan**  
  CSP: [DisableCatchupFullScan](/windows/client-management/mdm/policy-csp-defender#defender-disablecatchupfullscan)

  Configure catch-up scans for scheduled full scans. A catch-up scan is a scan that is run because a regularly scheduled scan was missed. Usually these scheduled scans are missed because the computer was turned off at the scheduled time.

  - **Not configured** (*default*) - The setting is returned to client default, which is to disable catch-up scans for full scans. 
  - **No** - The setting is disabled. Device users can't change this setting.
  - **Yes** - Catch-up scans for scheduled full scans are enforced and the user can't disable them. If a computer is offline for two consecutive scheduled scans, a catch-up scan is started the next time someone signs in to the computer. If there's no scheduled scan configured, there will be no catch-up scan run. Device users can't change this setting.

- **Disable catchup quick scan**  
  CSP: [DisableCatchupQuickScan](/windows/client-management/mdm/policy-csp-defender#defender-disablecatchupquickscan)

  Configure catch-up scans for scheduled quick scans. A catch-up scan is a scan that is run because a regularly scheduled scan was missed. Usually these scheduled scans are missed because the computer was turned off at the scheduled time.

  - **Not configured** (*default*) - The setting is returned to client default, which is to disable catch-up scans for full scans.
  - **No** - The setting is disabled. Device users can't change this setting.
  - **Yes** - Catch-up scans for scheduled quick scans are enforced and the user can't disable them. If a computer is offline for two consecutive scheduled scans, a catch-up scan is started the next time someone signs in to the computer. If there's no scheduled scan configured, there will be no catch-up scan run. Device users can't change this setting.

- **CPU usage limit per scan**  
  CSP: [AvgCPULoadFactor](/windows/client-management/mdm/policy-csp-defender#defender-avgcpuloadfactor)

  Specify as a percent from zero to 100, the average CPU load factor for the Defender scan.

- **Scan mapped network drives during full scan**  
  CSP: [AllowFullScanOnMappedNetworkDrives](/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanonmappednetworkdrives)

  Configure Defender to scan mapped network drives.

  - **Not configured** (*default*) - The setting is restored to the system default, which disables scanning on mapped network drives.
  - **No** - The setting is disabled. Device users can't change the setting.
  - **Yes** - Enable scans of mapped network drives. Device users can't change this setting.

- **Run daily quick scan at**  
  CSP: [ScheduleQuickScanTime](/windows/client-management/mdm/policy-csp-defender#defender-schedulequickscantime)

  Select the time of day that Defender quick scans run. This setting applies only when a device runs a quick scan and doesn't interact with the following three settings:

  - Scan type
  - Day of week to run a scheduled scan
  - Time of day to run a  scheduled scan

  By default, *Run daily quick scan at* is set to **Not configured**.

- **Scan type**  
  CSP: [ScanParameter](/windows/client-management/mdm/policy-csp-defender#defender-scanparameter)
  
  Select the type of scan that Defender runs. This setting interacts with the settings *Day of week to run a scheduled scan* and *Time of day to run a scheduled scan*.

  - **Not Configured** (*default*)
  - **Quick scan**
  - **Full scan**

- **Day of week to run a scheduled scan**  
  - **Not Configured** (*default*)

- **Time of day to run a scheduled scan**  
  - **Not Configured** (*default*)

- **Check for signature updates before running scan**  
  - **Not Configured** (*default*)
  - **No**
  - **Yes**

## Updates

These settings are available in the following profiles:

- Microsoft Defender Antivirus

**Settings**:

- **Enter how often (0-24 hours) to check for security intelligence updates**  
  CSP: [SignatureUpdateInterval](/windows/client-management/mdm/policy-csp-defender)

  Specify the interval from zero to 24 (in hours) that is used to check for signatures. A value of zero results in no check for new signatures. A value of 2 will check every two hours, and so on.

- **Define file shares for downloading definition updates**  
  CSP: [SignatureUpdateFallbackOrder](/windows/client-management/mdm/policy-csp-defender#defender-signatureupdatefallbackorder)

  Manage locations, like a UNC file share, as a download source location to get definition updates. After definition updates successfully download from a specified source, the remaining sources in the list won't be contacted.

  You can **Add** individual locations, or **Import** a list of locations as a .csv file.

- **Define the order of sources for downloading definition updates**  
  CSP: [SignatureUpdateFileSharesSources](/windows/client-management/mdm/policy-csp-defender#defender-signatureupdatefilesharessources)

  Specify in which order to contact source locations you've specified, to get definition updates. After definition updates have successfully downloaded from one specified source, the remaining sources in the list won't be contacted.

## User experience

These settings are available in the following profiles:

- Microsoft Defender Antivirus

**Settings**:

- **Allow user access to Microsoft Defender app**  
  CSP: [AllowUserUIAccess](/windows/client-management/mdm/policy-csp-defender#defender-allowuseruiaccess)  

  - **Not Configured** (*default*) - The setting returns to client default in which UI and notifications are allowed.
  - **No** - The Defender User Interface (UI) is inaccessible and notifications ware suppressed.
  - **Yes**