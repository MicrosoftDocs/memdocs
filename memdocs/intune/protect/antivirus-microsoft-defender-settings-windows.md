---
# required metadata

title: Windows 10 Antivirus policy settings for Microsoft Defender Antivirus for Intune | Microsoft Docs
description: See a list of the settings in the Microsoft Defender Antivirus profile for Windows 10. You can configure these settings as part of Endpoint security Antivirus policy in Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/15/2020
ms.topic: reference
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
ms.reviewer: mattsha

---

# Settings for Windows 10 Microsoft Defender Antivirus policy in Microsoft Intune

View the Endpoint security antivirus policy settings you can configure for the Microsoft Defender Antivirus profile for Windows 10 in Microsoft Intune as part of an [Endpoint security policy](../protect/endpoint-security-policy.md).

## Cloud protection

- **Turn on cloud-delivered protection**  
  CSP: [AllowCloudProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  By default, Defender on Windows 10 desktop devices sends information to Microsoft about any problems it finds. Microsoft analyzes that information to learn more about problems affecting you and other customers, to offer improved solutions.

  - **Not configured** (*default*) - The setting is restored to the system default.
  - **No** - The setting is disabled. Device users can't change this setting.
  - **Yes** - Cloud-delivered protection is turned on.  Device users can't change this setting.

- **Cloud-delivered protection level**  
  CSP: [CloudBlockLevel](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-cloudblocklevel)

  Configure how aggressive Defender Antivirus is in blocking and scanning suspicious files.
  - **Not configured** (*default*) - Default Defender blocking level.
  - **High** - Aggressively block unknowns while optimizing client performance, which includes a greater chance of false positives.
  - **High plus** - Aggressively block unknowns and apply additional protection measures that might impact client performance.
  - **Zero tolerance** - Block all unknown executable files.

- **Defender cloud extended timeout in seconds**  
  CSP: [CloudExtendedTimeout](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-cloudextendedtimeout)

  Defender Antivirus automatically blocks suspicious files for 10 seconds so it can scan the files in the cloud to make sure they're safe. With this setting, you can add up to 50 additional seconds to this timeout.

## Microsoft Defender Antivirus Exclusions

For each setting in this group, you can expand the setting, select **Add**, and then specify a value for the exclusion.

- **Defender processes to exclude**  
  CSP: [ExcludedProcesses](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-excludedprocesses)

  Specify a list of files opened by processes to ignore during a scan. The process itself isn't excluded from the scan.

- **File extensions to exclude from scans and real-time protection**  
  CSP: [ExcludedExtensions](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-excludedextensions)

  Specify a list of file type extensions to ignore during a scan.

- **Defender files and folders to exclude**  
  CSP: [ExcludedPaths](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-excludedpaths)

  Specify a list of files and directory paths to ignore during a scan.

## Real-time protection

- **Turn on real-time protection**  
  CSP: [AllowRealtimeMonitoring](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

  Require Defender on Windows 10 desktop devices to use the real-time Monitoring functionality.
  - **Not configured** (*default*) - The setting is restored to the system default
  - **No** - The setting is disabled. Device users can't change this setting.
  - **Yes** - Enforce use of real-time monitoring. Device users can't change this setting.

- **Enable on access protection**  
  CSP: [AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935)

  Configure virus protection that's continuously active, as opposed to on demand.

  - **Not Configured** (*default*) - This policy doesn't alter the state of this setting on a device. The existing state on the device remains unchanged.
  - **No** - Block On Access Protection on devices. Device users can't change this setting.
  - **Yes** - On Access Protection is active on devices.

- **Monitoring for incoming and outgoing files**  
  CSP: [Defender/RealTimeScanDirection](https://go.microsoft.com/fwlink/?linkid=2113943)

  Configure this setting to determine which NTFS file and program activity is monitored.
  - **Monitor all files** (*default*)
  - **Only monitor incoming files**
  - **Only monitor outgoing files**

- **Turn on behavior monitoring**  
  CSP: [AllowBehaviorMonitoring](https://go.microsoft.com/fwlink/?linkid=2114048)

  By default, Defender on Windows 10 desktop devices uses the Behavior Monitoring functionality.

  - **Not configured** (*default*) - The setting is restored to the system default.
  - **No** - The setting is disabled. Device users can't change this setting.
  - **Yes** - Enforce use of real-time behavior monitoring. Device users can't change this setting.

- **Turn on network protection**  
  CSP: [EnableNetworkProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

  Protect device users using any app from accessing phishing scams, exploit-hosting sites, and malicious content on the Internet. Protection includes preventing third-party browsers from connecting to dangerous sites.

  - **Not configured** (*default*) - The setting is restored to the system default.
  - **No** - The setting is disabled. Device users can't change this setting.
  - **Yes** - Network protection is turned on. Device users can't change this setting.

- **Scan all downloaded files and attachments**  
  CSP: [EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=2113939)

  Configure Defender to scan all downloaded files and attachments.

  - **Not configured** (*default*) - The setting is restored to the system default.
  - **No** - The setting is disabled. Device users can't change this setting.
  - **Yes** - Defender scans all downloaded files and attachments. Device users can't change this setting.

- **Scan scripts that are used in Microsoft browsers**  
  CSP: [AllowScriptScanning](https://go.microsoft.com/fwlink/?linkid=2114054)

  Configure Defender to scan scripts.

  - **Not configured** (*default*) - The setting is restored to the system default.
  - **No** - The setting is disabled. Device users can't change this setting.
  - **Yes** - Defender scans scripts. Device users can't change this setting.

- **Scan network files**  
  CSP: [AllowScanningNetworkFiles](https://go.microsoft.com/fwlink/?linkid=2114049&)

  Configure Defender to scan network files.

  - **Not configured** (*default*) - The setting is restored to the system default.
  - **No** - The setting is disabled. Device users can't change this setting.
  - **Yes** - Turn on scanning of network files. Device users can't change this setting.

- **Scan emails**  
  CSP: [AllowEmailScanning](https://go.microsoft.com/fwlink/?linkid=2114052)

  Configure Defender to scan incoming email.

  - **Not configured** (*default*) - The setting is restored to the system default.
  - **No** - The setting is disabled. Device users can't change this setting.
  - **Yes** - Turn on email scanning. Device users can't change this setting.

## Remediation

- **Number of days (0-90) to keep quarantined malware**  
  CSP: [DaysToRetainCleanedMalware](https://go.microsoft.com/fwlink/?linkid=2114055)

  Specify a number of days from zero to 90 that the system stores quarantined items  before they're automatically removed. A value of zero keeps items in quarantine and does not automatically remove them.

- **Submit samples consent**  

  - **Not configured** (*default*)
  - **Send safe samples automatically**
  - **Always prompt**
  - **Never send**
  - **Send all samples automatically**

- **Action to take on potentially unwanted apps**  
  CSP: [PUAProtection](https://go.microsoft.com/fwlink/?linkid=2114051)

  Specify the level of detection for potentially unwanted applications (PUAs). Defender alerts users when potentially unwanted software is being downloaded or attempts to install on a device.

  - **Not configured** (*default*) - The setting is restored to the system default, which is PUA Protection OFF.
  - **Disable**
  - **Enable** - Detected items are blocked, and show in history along with other threats.
  - **Audit mode** - Defender detects potentially unwanted applications, but takes no action. You can review information about the applications Defender would have taken action against by searching for events that are created by Defender in the Event Viewer.

- **Actions for detected threats**  
  CSP: [ThreatSeverityDefaultAction](https://go.microsoft.com/fwlink/?linkid=2113938)

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

- **Scan archive files**  
  CSP: [AllowArchiveScanning](https://go.microsoft.com/fwlink/?linkid=2114047)

  Configure Defender to scan archive files, like ZIP or CAB files.

  - **Not configured** (*default*) - The setting returns to the client default, which is to scan archived files, however the user may disable this.
Learn more
  - **No** - File archives aren't scanned. Device users can't change this setting.
  - **Yes** - Enable scans of archive files. Device users can't change this setting.

- **Use low CPU priority for scheduled scans**  
  CSP: [EnableLowCPUPriority](https://go.microsoft.com/fwlink/?linkid=2113944)

  Configure CPU priority for scheduled scans.
  - **Not configured** (*default*) - The setting returns to the system default, in which no changes to CPU priority are made.
  - **No** - The setting is disabled. Device users can't change this setting.
  - **Yes** - Low CPU priority will be used during scheduled scans. Device users can't change this setting.

- **Disable catch-up full scan**  
  CSP: [DisableCatchupFullScan](https://go.microsoft.com/fwlink/?linkid=2114042)

  Configure catch-up scans for scheduled full scans. A catch-up scan is a scan that is initiated because a regularly scheduled scan was missed. Usually these scheduled scans are missed because the computer was turned off at the scheduled time.

  - **Not configured** (*default*) - The setting is returned to client default, which is to enable catch-up scans for full scans, however the user can turn them off.
  - **No** - The setting is disabled. Device users can't change this setting.
  - **Yes** - Catch-up scans for scheduled full scans are enforced and the user can't disable them. If a computer is offline for two consecutive scheduled scans, a catch-up scan is started the next time someone logs on to the computer. If there's no scheduled scan configured, there will be no catch-up scan run. Device users can't change this setting.

- **Disable catchup quick scan**  
  CSP: [DisableCatchupQuickScan](https://go.microsoft.com/fwlink/?linkid=2113941)

  Configure catch-up scans for scheduled quick scans. A catch-up scan is a scan that is initiated because a regularly scheduled scan was missed. Usually these scheduled scans are missed because the computer was turned off at the scheduled time.

  - **Not configured** (*default*) - The setting is returned to client default, which is to enable catch-up quick scans, however the user can turn them off.
  - **No** - The setting is disabled. Device users can't change this setting.
  - **Yes** - Catch-up scans for scheduled quick scans are enforced and the user can't disable them. If a computer is offline for two consecutive scheduled scans, a catch-up scan is started the next time someone logs on to the computer. If there's no scheduled scan configured, there will be no catch-up scan run. Device users can't change this setting.

- **CPU usage limit per scan**  
  CSP: [AvgCPULoadFactor](https://go.microsoft.com/fwlink/?linkid=2114046)

  Specify as a percent from zero to 100, the average CPU load factor for the Defender scan.

- **Scan mapped network drives during full scan**  
  CSP: [AllowFullScanOnMappedNetworkDrives](https://go.microsoft.com/fwlink/?linkid=2113945)

  Configure Defender to scan mapped network drives.

  - **Not configured** (*default*) - The setting is restored to the system default, which disables scanning on mapped network drives.
  - **No** - The setting is disabled. Device users can't change this setting.
  - **Yes** - Enable scans of mapped network drives. Device users can't change this setting.

- **Run daily quick scan at**  
  CSP: [ScheduleQuickScanTime](https://go.microsoft.com/fwlink/?linkid=2114053)

  Select the time of day that Defender quick scans run.
  By default, this is **Not configured**

- **Scan type**  
  CSP: [ScanParameter](https://go.microsoft.com/fwlink/?linkid=2114045)

  Select the type of scan that Defender runs.

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

- **Enter how often (0-24 hours) to check for security intelligence updates**  
  CSP: [SignatureUpdateInterval](https://go.microsoft.com/fwlink/?linkid=2113936)

  Specify the interval from zero to 24 (in hours) that is used to check for signatures. A value of zero results in no check for new signatures. A value of 2 will check every two hours, and so on.

## User experience

- **Allow user access to Microsoft Defender app**  
  CSP: [AllowUserUIAccess](https://go.microsoft.com/fwlink/?linkid=2114043)  

  - **Not Configured** (*default*) - The setting returns to client default in which UI and notifications are allowed.
  - **No** - The Defender User Interface (UI) is inaccessible and notifications ware suppressed.
  - **Yes**

