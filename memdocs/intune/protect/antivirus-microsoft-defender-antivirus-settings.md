---
# required metadata

title: Antivirus policy settings for Microsoft Defender Antivirus for Intune | Microsoft Docs
description: See a list of the settings in the Microsoft Defender Antivirus profile you can configure as part of Endpoint security Antivirus policy in Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/20/2020
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

# Settings for Microsoft Defender Antivirus policy

View the Antivirus policy settings you can configure for the Microsoft Defender Antivirus profile in Microsoft Intune.

## Cloud protection

- **Turn on cloud-delivered protection**  
  CSP: [AllowCloudProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  By default, Windows Defender on Windows 10 desktop devices sends information to Microsoft about any problems it finds. Microsoft analyzes that information to learn more about problems affecting you and other customers, to offer improved solutions.

  - **Not configured** (*default*) - The setting is restored to the system default.
  - **No** - The setting is disabled. Device users can't change this setting.
  - **Yes** - Cloud-delivered protection is turned on.  Device users can't change this setting.

- **Cloud-delivered protection level**  
  CSP: [CloudBlockLevel](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-cloudblocklevel)

  Configure how aggressive Windows Defender Antivirus is in blocking and scanning suspicious files. 
  - **Not configured** (*default*) - Default Windows Defender blocking level.
  - **High** - Aggressively block unknowns while optimizing client performance, which includes a greater chance of false positives.
  - **High plus** - Aggressively block unknowns and apply additional protection measures that might impact client performance.
  - **Zero tolerance** - Block all unknown executable files.

- **Defender cloud extended timeout in seconds**  
  CSP: [CloudExtendedTimeout](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-cloudextendedtimeout)

  Windows Defender Antivirus automatically blocks suspicious files for 10 seconds so it can scan the files in the cloud to make sure they're safe. With this setting, you can add up to 50 additional seconds to this timeout.

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

  Require Windows Defender on Windows 10 desktop devices to use the Realtime Monitoring functionality.
  - **Not configured** (*default*) - The setting is restored to the system default
  - **No** - The setting is disabled. Device users can't change this setting.
  - **Yes** - Enforce use of real-time monitoring. Device users can't change this setting.

- **Turn on behavior monitoring**  
  CSP: [AllowBehaviorMonitoring](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowbehaviormonitoring)

  By default, Windows Defender on Windows 10 desktop devices uses the Behavior Monitoring functionality.

  - **Not configured** (*default*) - The setting is restored to the system default.
  - **No** - The setting is disabled. Device users can't change this setting.
  - **Yes** - Enforce use of real-time behavior monitoring. Device users can't change this setting.

- **Turn on network protection**  
  CSP: [EnableNetworkProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

  Protect device users using any app from accessing phishing scams, exploit-hosting sites, and malicious content on the Internet. This includes preventing third-party browsers from connecting to dangerous sites.

  - **Not configured** (*default*) - The setting is restored to the system default.
  - **No** - The setting is disabled. Device users can't change this setting.
  - **Yes** - Network protection is turned on. Device users can't change this setting.

- **Scan all downloaded files and attachments**  
  CSP: [NAllowIOAVProtectionAME](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowioavprotection)

  Configure Defender to scan all downloaded files and attachments.

  - **Not configured** (*default*) - The setting is restored to the system default.
  - **No** - The setting is disabled. Device users can't change this setting.
  - **Yes** - Defender scans all downloaded files and attachments. Device users can't change this setting.

- **Scan scripts that are used in Microsoft browsers**  
  CSP: [AllowScriptScanning](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowscriptscanning)

  Configure Defender to scan scripts.

  - **Not configured** (*default*) - The setting is restored to the system default.
  - **No** - The setting is disabled. Device users can't change this setting.
  - **Yes** - Defender scans scripts. Device users can't change this setting.

- **Block user access to Microsoft Defender app**  
  CSP: [AllowUserUIAccess](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowuseruiaccess)

  Configure user access to the Windows Defender UI.

  - **Not configured** (*default*) - The setting is restored to the system default, and UI notifications are allowed.
  - **No** - Users can access the Microsoft Defender app on the device. Device users can't change this setting.
  - **Yes** - Block user access to UI and suppress notifications. Device users can't change this setting.

- **Monitoring for incoming and outgoing files**  
  CSP: [RealTimeScanDirection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-realtimescandirection)

  Configure which files are monitored by Windows Defender.

  - **Monitor all files** (*default*)
  - **Only monitor incoming files**
  - **Only monitor outgoing files**

- **Scan emails**  
  CSP: [AllowEmailScanning](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowemailscanning)

  Configure Windows Defender to scan incoming email.

  - **Not configured** (*default*) - The setting is restored to the system default.
  - **No** - The setting is disabled. Device users can't change this setting.
  - **Yes** - Turn on email scanning. Device users can't change this setting.

- **Scan network files**  
  CSP: [AllowScanningNetworkFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowscanningnetworkfiles)

  Configure Windows Defender to scan network files.

  - **Not configured** (*default*) - The setting is restored to the system default.
  - **No** - The setting is disabled. Device users can't change this setting.
  - **Yes** - Turn on scanning of network files. Device users can't change this setting.

## Remediation

- **Number of days (0-90) to keep quarantined malware**  
  CSP: [DaysToRetainCleanedMalware](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-daystoretaincleanedmalware)

  Specify a number of days from zero to 90 that quarantined items are stored on the system before they are automatically removed. A value of zero keeps items in quarantine and does not automatically remove them.

- **Defender Submit Samples Consent Type**  

  - **Send safe samples automatically** (*default*)
  - **Always prompt**
  - **Never send**
  - **Send all samples automatically**

- **Defender Potentially Unwanted App Action**  
  CSP: [PUAProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)

  Specify the level of detection for potentially unwanted applications (PUAs). Windows Defender alerts users when potentially unwanted software is being downloaded or attempts to install on a device.

  - **User defined** (*default*)
  - **Enable** - Detected items are blocked, and show in history along with other threats.
  - **Audit mode** - Windows Defender detects potentially unwanted applications, but takes no action. You can review information about the applications Windows Defender would have taken action against by searching for events created by Windows Defender in the Event Viewer.


- **Defender Submit Samples Consent Type**  
  CSP: [SubmitSamplesConsent](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-submitsamplesconsent)

  Configure the user consent level that Windows Defender uses when managing sample submissions.

  - **Send safe samples automatically** (*default*)
  - **Always prompt**
  - **Never send**
  - **Send all samples automatically**

- **Threat alert levels and actions**  <!-- This setting title remains pending -->
  CSP: [ThreatSeverityDefaultAction](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-threatseveritydefaultaction)

  Specify the action that Windows Defender takes for detected malware based on the malware's threat level.
  
  Window Defender classifies malware that it detects as one of the following severity levels:
  - **Low severity**
  - **Moderate severity**
  - **High severity**
  - **Severe severity**

  For each level, specify the action to take. The default for each severity level is *Device default*.

  - **Device default**
  - **Clean** - The service tries to recover files and try to disinfect.
  - **Quarantine** - Moves files to quarantine.
  - **Remove** - Removes files from the device.
  - **Allow** - Allows the file and doesn't take other actions.
  - **User defined** - The device user makes the decision on which action to take.
  - **Block** - Blocks file execution.

## Scan

- **Use low CPU priority for scheduled scans**  
  CSP: [EnableLowCPUPriority](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablelowcpupriority)

  Configure CPU priority for scheduled scans.
  - **Not configured** (*default*) - The setting is returned to the system default, in which no changes to CPU priority are made. 
  - **No** - The setting is disabled. Device users can't change this setting.
  - **Yes** - Low CPU priority will be used during scheduled scans. Device users can't change this setting.

- **Disable catch-up full scan**   <!-- Pending testing - these might be reversed settings -->
  CSP: [DisableCatchupFullScan](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-disablecatchupfullscan)

  Configure catch-up scans for scheduled full scans. A catch-up scan is a scan that is initiated because a regularly scheduled scan was missed. Usually these scheduled scans are missed because the computer was turned off at the scheduled time.

  - **Not configured** (*default*) - The setting is returned to client default, which is to enable catch-up scans for full scans, however the user can turn them off.
  - **No** - The setting is disabled. Device users can't change this setting.
  - **Yes** - Catch-up scans for scheduled full scans will be turned on. If a computer is offline for two consecutive scheduled scans, a catch-up scan is started the next time someone logs on to the computer. If there's no scheduled scan configured, there' will be no catch-up scan run. Device users can't change this setting.

- **Disable catchup quick scan**  
  CSP: [DisableCatchupQuickScan](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-disablecatchupquickscan)

  Configure catch-up scans for scheduled quick scans. A catch-up scan is a scan that is initiated because a regularly scheduled scan was missed. Usually these scheduled scans are missed because the computer was turned off at the scheduled time.

  - **Not configured** (*default*) - The setting is returned to client default, which is to enable catch-up quick scans, however the user can turn them off.
  - **No** - The setting is disabled. Device users can't change this setting.
  - **Yes** - Catch-up scans for scheduled quick scans will be turned on. If a computer is offline for two consecutive scheduled scans, a catch-up scan is started the next time someone logs on to the computer. If there's no scheduled scan configured, there will be no catch-up scan run. Device users can't change this setting.

- **Maximum allowed CPU usage (0-100 percent) per scan**  <!-- This setting title remains pending -->
  CSP: [AvgCPULoadFactor](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-avgcpuloadfactor)

  Specify as a percent from zero to 100, the average CPU load factor for the Windows Defender scan.

- **Scan archive files**  
  CSP: [AllowArchiveScanning](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowarchivescanning)

  Configure Windows Defender to scan archive files.

  - **Not configured** (*default*) - This policy doesn't alter the state of this setting on a device. The existing state on the device remains unchanged.
  - **No** - File archives aren't scanned.  Device users can't change this setting.
  - **Yes** - Enable scans of archive files. Device users can't change this setting.

- **Scan mapped network drives during full scan**  
  CSP: [AllowFullScanOnMappedNetworkDrives](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanonmappednetworkdrives)

  Configure Windows Defender to scan mapped network drives.

  - **Not configured** (*default*) - The setting is restored to the system default.
  - **No** - The setting is disabled. Device users can't change this setting.
  - **Yes** - Enable scans of mapped network drives. Device users can't change this setting.

- **Run daily quick scan at**  
  CSP: [ScheduleQuickScanTime](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulequickscantime)

  Select the time of day that Windows Defender quick scans run.
  By default, this is **Not configured**

- **Scan type**  
  CSP: [ScanParameter](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-scanparameter)

  Select the type of scan that Windows Defender runs.

  - **User defined** (*default*) - Device user chooses.
  - **Disabled** - No scan is run.
  - **Quick scan**
  - **Full scan**

## Updates

- **Enter how often (0-24 hours) to check for security intelligence updates**  
  CSP: [SignatureUpdateInterval](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdateinterval)

  Specify the interval from zero to 24 (in hours) that is used to check for signatures. A value of zero results in no check for new signatures. A value of 2 will check every two hours, and so on.

## User experience

- **Disable On Access Protection**  
  CSP: [AllowOnAccessProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowonaccessprotection)

  Configure Windows Defender On Access Protection functionality, which monitors file and program activity on the device.

  - **Not Configured** (*default*) - This policy doesn't alter the state of this setting on a device. The existing state on the device remains unchanged.
  - **No** - On Access Protection is active on devices.  Device users can't change this setting.
  - **Yes** - Block Windows Defender On Access Protection on devices. Device users can't change this setting.

## Next steps

[Create or manage Antivirus policies](../protect/endpoint-security-antivirus-policy.md)