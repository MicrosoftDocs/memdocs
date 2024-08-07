---
# required metadata

title: Windows Antivirus policy settings from Microsoft Defender Antivirus for tenant attached devices | Microsoft Docs
description: See a list of the settings in the Microsoft Defender Antivirus profile for Windows devices managed by Configuration Manager. You can configure these settings as part of Endpoint security Antivirus policy in Microsoft Intune after you configure tenant attach for Configuration Manager.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/11/2024
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier3
- M365-identity-device-management
- sub-secure-endpoints
ms.reviewer: mattcall

---

# Settings for Microsoft Defender Antivirus policy for tenant attached devices in Microsoft Intune

View the Microsoft Defender Antivirus settings you can manage with the **Microsoft Defender Antivirus Policy (ConfigMgr)** profile from Intune. The profile is available when you configure Intune [Endpoint security Antivirus policy](../protect/endpoint-security-antivirus-policy.md), and the policy deploys to devices you manage with Configuration Manager when you've configured the [tenant attach](../protect/tenant-attach-intune.md) scenario.

## Cloud protection

- **Turn on cloud-delivered protection**  
  CSP: [AllowCloudProtection](/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  By default, Defender on Windows 10/11 desktop devices sends information to Microsoft about any problems it finds. Microsoft analyzes that information to learn more about problems affecting you and other customers, to offer improved solutions.

  - **Not Configured** (*default*) - The setting is restored to the system default.
  - **No** Turns off the Microsoft Active Protection Service.
  - **Yes**  Turns on the Microsoft Active Protection Service.

- **Cloud-delivered protection level**  
  CSP: [CloudBlockLevel](/windows/client-management/mdm/policy-csp-defender#defender-cloudblocklevel)

  Configure how aggressive Defender Antivirus is in blocking and scanning suspicious files.
  - **Not Configured** (*default*) - Default Defender blocking level.
  - **High** - Aggressively block unknowns while optimizing client performance, which includes a greater chance of false positives.
  - **High Plus** - Aggressively block unknowns and apply extra protection measures that might impact client performance.
  - **Zero Tolerance** - Block all unknown executable files.

- **Defender Cloud Extended Timeout in Seconds**  
  CSP: [CloudExtendedTimeout](/windows/client-management/mdm/policy-csp-defender#defender-cloudextendedtimeout)

  Defender Antivirus automatically blocks suspicious files for 10 seconds so it can scan the files in the cloud to make sure they're safe. With this setting, you can add up to 50 more seconds to this timeout.

## Microsoft Defender Antivirus Exclusions

For each setting in this group, you can expand the setting, select **Add**, and then specify a value for the exclusion.

- **Defender Processes To Exclude**  
  CSP: [ExcludedProcesses](/windows/client-management/mdm/policy-csp-defender#defender-excludedprocesses)

  Specify a list of files opened by processes to ignore during a scan. The process itself isn't excluded from the scan.

- **File extensions to exclude from scans and real-time protection**  
  CSP: [ExcludedExtensions](/windows/client-management/mdm/policy-csp-defender#defender-excludedextensions)

  Specify a list of file type extensions to ignore during a scan.

- **Defender Files And Folders To Exclude**  
  CSP: [ExcludedPaths](/windows/client-management/mdm/policy-csp-defender#defender-excludedpaths)

  Specify a list of files and directory paths to ignore during a scan.

## Real-time protection

- **Turn on real-time protection**  
  CSP: [AllowRealtimeMonitoring](/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

  Require Defender on Windows 10/11 desktop devices to use the real-time Monitoring functionality.
  - **Not Configured** (*default*) - The setting is restored to the system default
  - **No** Turns off the real-time monitoring service.
  - **Yes** Turns on and runs the real-time monitoring service.

- **Enable on access protection**  
  CSP: [AllowOnAccessProtection](/windows/client-management/mdm/policy-csp-defender#defender-allowonaccessprotection)

  Configure virus protection that's continuously active, as opposed to on demand.

  - **Not Configured** (*default*) - This policy doesn't alter the state of this setting on a device. The existing state on the device remains unchanged.
  - **No** Turns off the real-time monitoring service.
  - **Yes**

- **Monitoring for incoming and outgoing files**  
  CSP: [Defender/RealTimeScanDirection](/windows/client-management/mdm/policy-csp-defender)

  Configure this setting to determine which NTFS file and program activity is monitored.
  - **Monitor all files (bi-directional)** (*default*)
  - **Monitor incoming files**
  - **Monitor outgoing files**

- **Turn on behavior monitoring**  
  CSP: [AllowBehaviorMonitoring](/windows/client-management/mdm/policy-csp-defender#defender-allowbehaviormonitoring)

  By default, Defender on Windows 10/11 desktop devices uses the Behavior Monitoring functionality.

  - **Not Configured** (*default*) - The setting is restored to the system default.
  - **No** Turns off behavior monitoring.
  - **Yes** Turns on real-time behavior monitoring.

- **Allow Intrusion Prevention System**  

  Configure Defender to allow or disallow Intrusion Prevention functionality.

  - **Not Configured** (*default*) - The setting is restored to the system default.
  - **No** - Intrusion Prevention System is not allowed.
  - **Yes** - Intrusion Prevention System is allowed.

- **Scan all downloaded files and attachments**  
  CSP: [EnableNetworkProtection](/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

  Configure Defender to scan all downloaded files and attachments.

  - **Not Configured** (*default*) - The setting is restored to the system default.
  - **No**
  - **Yes**

- **Scan scripts that are used in Microsoft browsers**  
  CSP: [AllowScriptScanning](/windows/client-management/mdm/policy-csp-defender)

  Configure Defender to scan scripts.

  - **Not Configured** (*default*) - The setting is restored to the system default.
  - **No**
  - **Yes**

- **Scan network files**  
  CSP: [AllowScanningNetworkFiles](/windows/client-management/mdm/policy-csp-defender#defender-allowscanningnetworkfiles)

  Configure Defender to scan network files.

  - **Not Configured** (*default*) - The setting is restored to the system default.
  - **No** Turns off scanning of network files.
  - **Yes** Scans network files.

- **Scan emails**  
  CSP: [AllowEmailScanning](/windows/client-management/mdm/policy-csp-defender#defender-allowemailscanning)

  Configure Defender to scan incoming email.

  - **Not Configured** (*default*) - The setting is restored to the system default.
  - **No** Turns off email scanning.
  - **Yes** Turns on email scanning.

## Remediation

- **Number of days (0-90) to keep quarantined malware**  
  CSP: [DaysToRetainCleanedMalware](/windows/client-management/mdm/policy-csp-defender#defender-daystoretaincleanedmalware)

  Specify a number of days from zero to 90 that the system stores quarantined items  before they're automatically removed. A value of zero keeps items in quarantine and does not automatically remove them.

- **Submit Samples Consent**  

  - **Not Configured** (*default*)
  - **Always prompt**
  - **Send safe samples automatically**
  - **Never send**
  - **Send all samples automatically**

- **Action to take on potentially unwanted apps**  
  CSP: [PUAProtection](/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)

  Specify the level of detection for potentially unwanted applications (PUAs). Defender alerts users when potentially unwanted software is being downloaded or attempts to install on a device.

  - **Not Configured** (*default*) - The setting is restored to the system default, which is PUA Protection OFF.
  - **Disabled** - Windows Defender will not protect against potentially unwanted applications.
  - **Enabled** - Detected items are blocked. They will show in history along with other threats.
  - **Audit mode** - Defender detects potentially unwanted applications, but takes no action. You can review information about the applications Defender would have taken action against by searching for events that are created by Defender in the Event Viewer.

- **Create a system restore point before computers are cleaned**  
  - **Not Configured** (*default*)
  - **No**
  - **Yes**

- **Actions for detected threats**  
  CSP: [ThreatSeverityDefaultAction](/windows/client-management/mdm/policy-csp-defender#defender-threatseveritydefaultaction)

  Specify the action that Defender takes for detected malware based on the malware's threat level.
  
  Defender classifies malware that it detects as one of the following severity levels:
  - **Low threat**
  - **Moderate threat**
  - **High threat**
  - **Severe threat**

  For each level, specify the action to take. The default for each severity level is *Not configured*.

  - **Not Configured** (*default*)
  - **Clean** - The service tries to recover files and try to disinfect.
  - **Quarantine** - Moves files to quarantine.
  - **Remove** - Removes files from the device.
  - **Allow** - Allows the file and doesn't take other actions.
  - **User defined** - The device user makes the decision on which action to take.
  - **Block** - Blocks file execution.

## Scan

- **Scan archive files**  
  CSP: [AllowArchiveScanning](/windows/client-management/mdm/policy-csp-defender#defender-allowarchivescanning)

  Configure Defender to scan archive files, like ZIP or CAB files.

  - **Not Configured** (*default*) - The setting returns to the client default, which is to scan archived files, however the user may disable the scan.
Learn more
  - **No** Turns off scanning on archived files.
  - **Yes** Scans the archive files.

- **Enable low CPU priority for scheduled scans**  
  CSP: [EnableLowCPUPriority](/windows/client-management/mdm/policy-csp-defender#defender-enablelowcpupriority)

  Configure CPU priority for scheduled scans.
  - **Not Configured** (*default*) - The setting returns to the system default, in which no changes to CPU priority are made.
  - **No**
  - **Yes**

- **Disable Catch-up Full Scan**  
  CSP: [DisableCatchupFullScan](/windows/client-management/mdm/policy-csp-defender#defender-disablecatchupfullscan)

  Configure catch-up scans for scheduled full scans. A catch-up scan is a scan that starts because a regularly scheduled scan was missed. Usually these scheduled scans are missed because the computer was turned off at the scheduled time.

  - **Not Configured** (*default*) - The setting is returned to client default, which is to enable catch-up scans for full scans, however the user can turn them off.
  - **No**
  - **Yes**

- **Disable Catchup Quick Scan**  
  CSP: [DisableCatchupQuickScan](/windows/client-management/mdm/policy-csp-defender#defender-disablecatchupquickscan)

  Configure catch-up scans for scheduled quick scans. A catch-up scan is a scan that starts because a regularly scheduled scan was missed. Usually these scheduled scans are missed because the computer was turned off at the scheduled time.

  - **Not Configured** (*default*) - The setting is returned to client default, which is to enable catch-up quick scans, however the user can turn them off.
  - **No**
  - **Yes**

- **CPU usage limit (0-100 percent) per scan**  
  CSP: [AvgCPULoadFactor](/windows/client-management/mdm/policy-csp-defender#defender-avgcpuloadfactor)

  Specify as a percent from zero to 100, the average CPU load factor for the Defender scan.

- **Enable mapped network drives be scanned during a full scan**  
  CSP: [AllowFullScanOnMappedNetworkDrives](/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanonmappednetworkdrives)

  Configure Defender to scan mapped network drives.

  - **Not Configured** (*default*) - The setting is restored to the system default, which disables scanning on mapped network drives.
  - **Not allowed** Disables scanning on mapped network drives.
  - **Allowed** Scans mapped network drives.

- **Run daily quick scan at**  
  CSP: [ScheduleQuickScanTime](/windows/client-management/mdm/policy-csp-defender#defender-schedulequickscantime)

  Select the time of day that Defender quick scans run.
  By default, this option is **Not Configured**

- **Scan Type**  
  CSP: [ScanParameter](/windows/client-management/mdm/policy-csp-defender#defender-scanparameter)

  Select the type of scan that Defender runs.

  - **Not Configured** (*default*)
  - **Quick scan**
  - **Full scan**

- **Day of week to run a scheduled scan**  
  - **Not Configured** (*default*)

- **Time of day to run a scheduled scan**  
  - **Not Configured** (*default*)

- **Check For Signature Updates Before Running Scan**  
  - **Not Configured** (*default*)
  - **No**
  - **Yes**

- **Randomize scheduled scan and security intelligence update start times**  
  -**Not Configured** (*default*)
  -**Yes**
  -**No**

- **Scan removable drives during full scan**
  - **Not Configured** (*default*)
  - **No** Turns off scanning on removable drives.
  - **Yes** Scans removable drives.

## Updates

- **Enter how often (0-24 hours) to check for security intelligence updates**  
  CSP: [SignatureUpdateInterval](/windows/client-management/mdm/policy-csp-defender)

  Specify the interval from zero to 24 (in hours) that is used to check for signatures. A value of zero results in no check for new signatures. A value of 2 will check every two hours, and so on.

- **Signature Update Fallback Order (Device)**

- **Signature Update File Shares Sources (Device)**

- **Security Intelligence Location (Device)**  

## User experience

- **Block user access to Microsoft Defender app**  
  - **Not Configured** (*default*)
  - **Not allowed** Prevents users from accessing UI.
  - **Allowed** Lets users access UI.

- **Show notifications messages on the client computer when the user needs to run a full scan, update security intelligence, or run Windows Defender Offline**  
  - **Not Configured** (*default*)
  - **Yes**
  - **No**

- **Disable the client user interface**  
  - **Not Configured** (*default*)
  - **Yes**
  - **No**

