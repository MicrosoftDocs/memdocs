---
# required metadata

title: Intune security baselines settings for Microsoft Defender Advanced Threat Protection 
titleSuffix: Microsoft Intune
description: Security baseline settings supported by Intune for managing Microsoft Defender Advanced Threat Protection
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 12/05/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology:
ms.assetid:

# optional metadata

#ROBOTS:

#audience:

ms.reviewer: shpate
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Microsoft Defender Advanced Threat Protection baseline settings for Intune

View the Microsoft Defender Advanced Threat Protection (formerly Windows Defender Advanced Threat Protection) baseline settings that are supported by Microsoft Intune. The Advanced Threat Protection (ATP) baseline defaults represent the recommended configuration for ATP, and might not match baseline defaults for other security baselines.  

The Microsoft Defender Advanced Threat Protection baseline is available when your environment meets the prerequisites for using [Microsoft Defender Advanced Threat Protection](advanced-threat-protection.md#prerequisites). 

This baseline is optimized for physical devices and is currently not recommended for use on virtual machines (VMs) or VDI endpoints. Certain baseline settings can impact remote interactive sessions on virtualized environments. For more information, see [Increase compliance to the Microsoft Defender ATP security baseline](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-machines-security-baseline) in the Windows documentation.

## Application Guard  
For more information, see [WindowsDefenderApplicationGuard CSP](https://docs.microsoft.com/windows/client-management/mdm/windowsdefenderapplicationguard-csp) in the Windows documentation.  

While using Microsoft Edge, Microsoft Defender Application Guard protects your environment from sites that aren't trusted by your organization. When users visit sites that aren’t listed in your isolated network boundary, the sites open in a Hyper-V virtual browsing session. Trusted sites are defined by a network boundary.  

- **Application Guard** - *Settings/AllowWindowsDefenderApplicationGuard*  
  Select *Yes* to turn on this feature, which opens untrusted sites in a Hyper-V virtualized browsing container. When set to *Not configured*, any site (trusted and untrusted) opens on the device, and not in a virtualized container.  

  **Default**: Yes
 
  - **External content on enterprise sites** - *Settings/BlockNonEnterpriseContent*  
    Select *Yes* to block content from unapproved websites from loading. When set to *Not configured*, non-enterprise sites can open on the device. 
 
    **Default**: Yes

  - **Clipboard behavior** - *Settings/ClipboardSettings*  
    Choose what copy and paste actions are allowed between the local PC and the Application Guard virtual browser.  Options include:
    - Not Configured  
    - Block copy and paste between PC and browser - Block both. Data can't transfer between the PC and the virtual browser.  
    - Allow copy and paste from browser to PC only - Data can't transfer from the PC into the virtual browser.
    - Allow copy and paste from PC to browser only - Data can't transfer from the virtual browser to the host PC.
    - Allow copy and paste between PC and browser - No block for content exists.  

    **Default**: Block copy and paste between PC and browser  

- **Windows network isolation policy – Enterprise network domain names**  
  For more information, see [Policy CSP - NetworkIsolation](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-networkisolation) in the Windows documentation.
  
  Specify a list of Enterprise resource as domains, IP address ranges, and network boundaries that are hosted in the cloud that Application Guard treats as enterprise sites.  

  **Default**: securitycenter.windows.com

## Application Reputation  

For more information, see [Policy CSP - SmartScreen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-smartscreen) in the Windows documentation.

- **Block execution of unverified files**  
    Block user from running unverified files. When set to *Not Configured*, employees can ignore SmartScreen warnings and run malicious files. Set to *Yes* so that employees can’t ignore SmartScreen warnings and run malicious files.  
  
    **Default**: Yes

- **Require SmartScreen for apps and files**  
  Set to *Yes* to enable SmartScreen for Windows.  

  **Default**: Yes

## Attack Surface Reduction  

- **Office apps launch child process type**  
  [Attack surface reduction rule](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#attack-surface-reduction-rules) – When set to *Block*, Office apps won’t be allowed to create child processes. Office apps include Word, Excel, PowerPoint, OneNote, and Access. Creation of a child process is a typical malware behavior, especially for macro-based attacks that attempt to use Office apps to launch or download malicious executables.  

  **Default**: Block

- **Script downloaded payload execution type**  
  [Defender/PUAProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-puaprotection) – Specify a level of detection for potentially unwanted applications that download or attempt to install.  

  **Default**: Block 

- **Prevent credential stealing type**  
  Set to *Enable* to [Protect derived domain credentials with Credential Guard](https://docs.microsoft.com/windows/security/identity-protection/credential-guard/credential-guard). Microsoft Defender Credential Guard uses virtualization-based security to isolate secrets so that only privileged system software can access them. Unauthorized access to these secrets can lead to credential theft attacks, such as Pass-the-Hash or Pass-The-Ticket. Microsoft Defender Credential Guard prevents these attacks by protecting NTLM password hashes, Kerberos Ticket Granting Tickets, and credentials stored by applications as domain credentials.  

  **Default**: Enable

- **Email content execution**  
  [Attack surface reduction rule](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#attack-surface-reduction-rules) – When set to *Block*, This rule blocks the following file types from being run or launched from an email seen in either Microsoft Outlook or webmail (such as Gmail.com or Outlook.com):  

  - Executable files (such as .exe, .dll, or .scr)  
  - Script files (such as a PowerShell .ps, VisualBasic .vbs, or JavaScript .js file)  
  - Script archive files  

  **Default**: Block

- **Adobe Reader launch in a child process**  
  [Attack surface reduction rule](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#attack-surface-reduction-rules) – *Enable* this rule to block Adobe Reader from creating a child process. Through social engineering or exploits, malware can download and launch additional payloads and break out of Adobe Reader.  

  **Default**: Enable

- **Script obfuscated macro code**  
  [Attack surface reduction rule](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#attack-surface-reduction-rules) – Malware and other threats can attempt to obfuscate or hide their malicious code in some script files. This rule prevents scripts that appear to be obfuscated from running.  
    
  **Default**: Block

- **Untrusted USB process**  
  [Attack surface reduction rule](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#attack-surface-reduction-rules) – When set to *Block*, unsigned, or untrusted executable files from USB removable drives and SD cards can't run.

  Executable files include:
  - Executable files (such as .exe, .dll, or .scr)
  - Script files (such as a PowerShell .ps, VisualBasic .vbs, or JavaScript .js file)  

  **Default**: Block

- **Office apps other process injection**  
  [Attack surface reduction rule](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#attack-surface-reduction-rules) - When set to *Block*, Office apps, including Word, Excel, PowerPoint, and OneNote, can’t inject code into other processes. Code injection is typically used by malware to run malicious code in an attempt to hide the activity from antivirus scanning engines.  

  **Default**: Block

- **Office macro code allow Win32 imports**  
  [Attack surface reduction rule](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#attack-surface-reduction-rules) - When set to *Block*, this rule attempts to block Office files that contain macro code that can import Win32 DLLs. Office files include Word, Excel, PowerPoint, and OneNote. Malware can use macro code in Office files to import and load Win32 DLLs, which are then used to make API calls to allow further infection throughout the system.  

  **Default**: Block

- **Office communication apps launch in a child process**  
  [Attack surface reduction rule](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#attack-surface-reduction-rules) – When set to *Enable*, this rule prevents Outlook from creating child processes. By blocking the creation of a child process, this rule protects against social engineering attacks and prevents exploit code from abusing a vulnerability in Outlook.  

  **Default**: Enable

- **Office apps executable content creation or launch**  
  [Attack surface reduction rule](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction#attack-surface-reduction-rules) – When set to *Block*, Office apps can’t create executable content. Office apps include Word, Excel, PowerPoint, OneNote, and Access.  

  This rule targets typical behaviors used by suspicious and malicious add-ons and scripts (extensions) that create or launch executable files. This is a typical malware technique. Extensions are blocked from being used by Office apps. Typically, these extensions use the Windows Scripting Host (.wsh files) to run scripts that automate certain tasks or provide user-created add-on features.

  **Default**: Block

## BitLocker  

For more information, [BitLocker Group Policy settings](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-group-policy-settings) in the Windows documentation.  

- **Encrypt devices**  
  Select *Yes* to enable BitLocker device encryption. Depending on device hardware and version of Windows, device users might be asked to confirm that there's no third-party encryption on the device. Turning on Windows encryption while third-party encryption is active will render the device unstable.  

   **Default**: Yes

- **Bit locker removable drive policy**  
  The values for this policy determine the strength of the cipher that BitLocker uses for encryption of removable drives. Enterprises control the encryption level for increased security (AES-256 is stronger than AES-128). If you select *Yes* to enable this setting, you can configure an encryption algorithm and key cipher strength for fixed data drives, operating system drives, and removable data drives individually. For fixed and operating system drives, we recommend that you use the XTS-AES algorithm. For removable drives, you should use AES-CBC 128-bit or AES-CBC 256-bit if the drive is used in other devices that aren't running Windows 10, version 1511 or later. Changing the encryption method has no effect if the drive is already encrypted or if encryption is in progress. In these cases, this policy setting is ignored. 

  For Bit locker removable drive policy, configure the following settings:

  - **Require encryption for write access**  
    **Default**: Yes

  - **Encryption method**  
    **Default**: AES 128bit CBC

- **Encrypt storage card (mobile only)**
  Selecting *Yes* will encrypt the storage card of the mobile device.  

   **Default**: Yes

- **Bit locker fixed drive policy**  
  The values for this policy determine the strength of the cipher that BitLocker uses for encryption of fixed drives. Enterprises can control the encryption level for increased security (AES-256 is stronger than AES-128). If you enable this setting, you can configure an encryption algorithm and key cipher strength for fixed data drives, operating system drives, and removable data drives individually. For fixed and operating system drives, we recommend that you use the XTS-AES algorithm. For removable drives, you should use AES-CBC 128-bit or AES-CBC 256-bit if the drive is used in other devices that aren't running Windows 10, version 1511 or later. Changing the encryption method has no effect if the drive is already encrypted or if encryption is in progress. In these cases, this policy setting is ignored.

  For Bit locker fixed drive policy, configure the following settings:

  - **Require encryption for write access**  
    **Default**: Yes

  - **Encryption method**  
    **Default**: AES 128bit XTS

- **Bit locker system drive policy**  
  The values for this policy determine the strength of the cipher that BitLocker uses for encryption of the system drive. Enterprises may want to control the encryption level for increased security (AES-256 is stronger than AES-128). If you enable this setting, you can configure an encryption algorithm and key cipher strength for fixed data drives, operating system drives, and removable data drives individually. For fixed and operating system drives, we recommend that you use the XTS-AES algorithm. For removable drives, you should use AES-CBC 128-bit or AES-CBC 256-bit if the drive is used in other devices that aren't running Windows 10, version 1511 or later. Changing the encryption method has no effect if the drive is already encrypted or if encryption is in progress. In these cases, this policy setting is ignored.  

  For Bit locker system drive policy, configure the following settings:  

  - **Encryption method**  
    **Default**: AES 128bit XTS

## Device Control  

- **Scan removable drives during a full scan**  
  [Defender/AllowFullScanRemovableDriveScanning](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanremovabledrivescanning) - When set to *Yes*, Defender scans for malicious and unwanted software in removable drives, like flash drives, during a full scan. Defender Antivirus scans all files on USB devices before files on the USB device can run.

  Related setting in this list: *Defender/AllowFullScanOnMappedNetworkDrives*  

  **Default**: Yes

- **Enumeration of external devices incompatible with Kernel DMA Protection**  
   See *DmaGuard/DeviceEnumerationPolicy* in [Policy CSP - DmaGuard](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy)

  This policy provides additional security against external DMA capable devices. It allows for more control over the enumeration of external DMA capable devices that are incompatible with DMA device memory isolation and sandboxing.

  This policy only takes effect when Kernel DMA Protection is supported and enabled by the system firmware. Kernel DMA Protection is a platform feature that can't be controlled by policy or by the user of a device. It must be supported by the system at the time of manufacturing. 

  To check if the system supports Kernel DMA Protection, run MSINFO32.exe on the system, and review the *Kernel DMA Protection* field on the Summary page.  

  Options include: 
  - *Device default* - After sign in or screen unlock, devices with DMA remapping compatible drivers are allowed to enumerate at any time. Devices with DMA remapping incompatible drivers will only be enumerated after the user unlocks the screen
  - *Allow all* - All external DMA capable PCIe devices will be enumerated at any time
  - *Block all* - Devices with DMA remapping compatible drivers are allowed to enumerate at any time. Devices with DMA remapping incompatible drivers will never be allowed to start and perform DMA at any time.

  **Default**: Device default

- **Hardware device installation by device identifiers**  
  [DeviceInstallation/PreventInstallationOfMatchingDeviceIDs](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-deviceinstallation#deviceinstallation-preventinstallationofmatchingdeviceids) - With this policy, you specify a list of Plug and Play hardware IDs and compatible IDs for devices that Windows is prevented from installing. This policy setting takes precedence over any other policy setting that allows Windows to install a device. If you enable this policy setting (set to *Block hardware device installation*), Windows is prevented from installing a device whose hardware ID or compatible ID appears in the list you create. If you enable this policy setting on a remote desktop server, the policy affects redirection of the specified devices from a remote desktop client to the remote desktop server. If you disable or don't configure this policy setting (set to *Allow hardware device installation*), devices can install and update as allowed or prevented by other policy settings.  

  **Default**: Block hardware device installation  

  When *Block hardware device installation* is selected, the following settings are available.
  - **Remove matching hardware devices**  
    This setting is available only when *Hardware device installation by device identifiers* is set to *Block hardware device installation*.  

    **Default**: Yes

  - **Hardware device identifiers that are blocked**  
    This setting is available only when *Hardware device installation by device identifiers* is set to *Block hardware device installation*. To configure this setting, expand the option, select **+ Add**, and then specify the hardware device identifier you want to block.  

    **Default**: PCI\CC_0C0A

- **Block direct memory access**  
  [DataProtection/AllowDirectMemoryAccess](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dataprotection#dataprotection-allowdirectmemoryaccess) - Use this policy setting to block direct memory access (DMA) for all hot pluggable PCI downstream ports on a device, until a user logs into Windows. Once a user logs in, Windows will enumerate the PCI devices connected to the host plug PCI ports. Every time the user locks the machine, DMA is blocked on hot plug PCI ports with no children devices until the user logs in again. Devices that were already enumerated when the machine was unlocked will continue to function until unplugged. 

  This policy setting is only enforced when BitLocker or device encryption is enabled.  

  **Default**: Yes


- **Hardware device installation by setup classes**  
  [DeviceInstallation/AllowInstallationOfMatchingDeviceSetupClasses](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-deviceinstallation#deviceinstallation-allowinstallationofmatchingdevicesetupclasses) - With this policy you can specify a list of device setup class globally unique identifiers (GUIDs) for device drivers that Windows is prevented from installing. This policy setting takes precedence over any other policy setting that allows Windows to install a device. If you enable this policy setting (set to *Block hardware device installation*), Windows is prevented from installing or updating device drivers whose device setup class GUIDs appear in the list you create. If you enable this policy setting on a remote desktop server, the policy setting affects redirection of the specified devices from a remote desktop client to the remote desktop server. If you disable or don't configure this policy setting (set to *Allow hardware device installation*), Windows can install and update devices as allowed or prevented by other policy settings.  

  **Default**: Block hardware device installation

  When *Block hardware device installation* is selected, the following settings are available.  

  - **Remove matching hardware devices**  
    This setting is available only when *Hardware device installation by setup classes* is set to *Block hardware device installation*.  
 
    **Default**: Yes  

  - **Hardware device identifiers that are blocked**  
    This setting is available only when Hardware device installation by setup classes is set to Block hardware device installation. To configure this setting, expand the option, select **+ Add**, and then specify the hardware device identifier you want to block.  
 
    **Default**: {d48179be-ec20-11d1-b6b8-00c04fa372a7}

## Endpoint Detection and Response  
For more information, see [WindowsAdvancedThreatProtection CSP](https://docs.microsoft.com/windows/client-management/mdm/windowsadvancedthreatprotection-csp) in the Windows documentation.  

- **Expedite telemetry reporting frequency** - *Configuration/TelemetryReportingFrequency*

  Expedite Microsoft Defender Advanced Threat Protection telemetry reporting frequency.  

  **Default**: Yes

- **Sample sharing for all files** - *Configuration/SampleSharing* 

  Returns or sets the Microsoft Defender Advanced Threat Protection Sample Sharing configuration parameter.  

  **Default**: Yes

## Exploit Protection  

- **Exploit protection XML**  
  For more information, see [Import, export, and deploy exploit protection configurations](/windows/security/threat-protection/microsoft-defender-atp/import-export-exploit-protection-emet-xml) in the Windows documentation.  

  Enables the IT admin to push out a configuration representing the desired system and application mitigation options to all the devices in the organization. The configuration is represented by an XML. 

  Exploit protection applies helps protect devices from malware that use exploits to spread and infect. You use the Windows Security app or PowerShell to create a set of mitigations (known as a configuration). You can then export this configuration as an XML file and share it with multiple machines on your network so they all have the same set of mitigation settings.
 
  You can also convert and import an existing EMET configuration XML file into an exploit protection configuration XML.

- **Block exploit protection override**  
  [WindowsDefenderSecurityCenter/DisallowExploitProtectionOverride](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-disallowexploitprotectionoverride) – Set to *Yes* to prevent users from making changes to the exploit protection settings area in the Microsoft Defender Security Center. If you disable or don't configure this setting, local users can make changes in the exploit protection settings area.  
  **Default**: Yes  

## Microsoft Defender Antivirus  

For more information, see [Policy CSP - Defender](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender) in the Windows documentation.

- **Scan scripts loaded in Microsoft web browsers**  
  [Defender/AllowScriptScanning](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowscriptscanning) – Set to *Yes* to allow Microsoft Defender Script Scanning functionality.  

  **Default**: Yes

- **Scan incoming mail messages**  
  [Defender/AllowEmailScanning](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowemailscanning) – Set to *Yes* to allow Microsoft Defender to scan email.  

  **Default**: Yes

- **Defender sample submission consent**  
  [Defender/SubmitSamplesConsent](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-submitsamplesconsent) - Checks for the user consent level in Microsoft Defender to send data. If the required consent has already been granted, Microsoft Defender submits them. If not (and if the user has specified never to ask), the UI is launched to ask for user consent (when *Cloud-delivered protection* is set to *Yes*) before sending data.  

  **Default**: Send safe samples automatically

- **Network Inspection System (NIS)**  
  [Defender/EnableNetworkProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection) - Block malicious traffic detected by signatures in the Network Inspection System (NIS).  
 
  **Default**: Yes

- **Signature update interval (in hours)**  
  [Defender/SignatureUpdateInterval](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-signatureupdateinterval) – Specify in hours, how often the device checks for new Defender signature updates.  
 
  **Default**: 4

- **Configure low CPU priority for scheduled scans**  
  [Defender/EnableLowCPUPriority](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablelowcpupriority) – When set to *Yes*, CPU priority for scans is set to low. When *Not Configured*, no changes are made to CPU priority for scheduled scans.  

    **Default**: Yes

- **Defender block on access protection**  
  [Defender/AllowOnAccessProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowonaccessprotection) – When set to *Yes*, Microsoft Defender On Access Protection is enabled.  

  **Default**: Yes

- **Type of system scan to perform**  
  [Defender/ScanParameter](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-scanparameter) - Defender scan type.  

  **Default**: Quick scan

- **Scan all downloads**  
  [Defender/AllowIOAVProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowioavprotection) - When set to *Yes*, Defender scans all downloaded files and attachments.  

  **Default**: Yes

- **Days before deleting quarantined malware**  
  [Defender/DaysToRetainCleanedMalware](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-daystoretaincleanedmalware) - Specify how many days to keep quarantine items on the system before they're automatically deleted. When set to zero, items in quarantine are never automatically deleted.  

  **Default**: 0

- **Scheduled scan start time**  
  [Defender/ScheduleScanTime](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulescantime) – Schedule a time of day for Defender to scan devices. 
  
  Related option in this list: *Defender/ScheduleScanDay*   

  **Default**: 2 AM

- **Cloud-delivered protection**  
  [Defender/AllowCloudProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection) – When set to *Yes*, Microsoft Defender sends information to Microsoft about any problems it finds. Microsoft will analyze that information, learn more about problems affecting you and other customers, and offer improved solutions.

  When this policy is set to *Yes*, you can use *Defender sample submission consent type* to give users control over sending information from their device.  

  **Default**: Yes

- **Defender potentially unwanted app action**  
  [Defender/PUAProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-puaprotection) – Microsoft Defender Antivirus can identify and block *potentially unwanted applications* (PUAs) from downloading and installing on endpoints in your network. 
 
  - When set to *Block*, Microsoft Defender blocks PUAs, and lists them in history along with other threats.
  - When set to *Audit*, Microsoft Defender detects PUAs but doesn't block them. Information about the applications Microsoft Defender would have taken action against can be found by searching for events that were created by Microsoft Defender in the Event Viewer.  
  - When set to *Device default*, PUA protection is off.  
 
  **Default**: Block

- **Defender cloud extended timeout**  
  [Defender/CloudExtendedTimeout](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-cloudextendedtimeout) - Specify the maximum amount of additional time that Microsoft Defender Antivirus should block a file while waiting for a result from the cloud. The base amount of time Microsoft Defender waits is 10 seconds. Any additional time you specify here (up to 50 seconds) is added to those 10 seconds. In most cases the scan takes less time than the maximum. Extending the time allows the cloud to thoroughly investigate suspicious files.  

  By default the expanded time value is 0 (disabled). Intune recommends that you enable this setting and specify at least 20 additional seconds.  
 
  **Default**: 0

- **Scan archive files**  
  [Defender/AllowArchiveScanning](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowarchivescanning) – Set to *Yes*  to have Microsoft Defender scan archive files.  

  **Default**: Yes

- **Defender system scan schedule**  
  [Defender/ScheduleScanDay](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulescanday) - Schedule on which day Defender scans devices. 
 
  Related option in this list: *Defender/ScheduleScanTime*

  **Default**: User defined

- **Behavior monitoring**  
  [Defender/AllowBehaviorMonitoring](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowbehaviormonitoring) – Set to *Yes* to turn on Microsoft Defender Behavior Monitoring functionality. Embedded in Windows 10, Microsoft Defender Behavior Monitoring sensors collect and process behavioral signals from the operating system and send this sensor data to your private, isolated, cloud instance of Microsoft Defender ATP.  

  **Default**: Yes

- **Scan files opened from network folders**  
  [Defender/AllowScanningNetworkFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowscanningnetworkfiles) – Set to *Yes* to have Microsoft Defender scan files on the network. The user won’t be able to remove detected malware from read-only files.  

  **Default**: Yes

- **Defender cloud block level**  
  [Defender/CloudBlockLevel](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-cloudblocklevel) – Use this policy to determine how aggressive Microsoft Defender Antivirus is in blocking and scanning suspicious files. Options include:

  - High - Aggressively block unknown files while optimizing client performance (greater chance of false positives)
  - High plus - Aggressively block unknown files and apply additional protection measures (might impact client performance)
  - Zero tolerance - Block all unknown executable files

  **Default**: Not Configured

- **Real-time monitoring**  
  [Defender/AllowRealtimeMonitoring](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring) – Set to *Yes* to allow Microsoft Defender Realtime Monitoring.  

  **Default**: Yes

- **CPU usage limit during a scan**  
  [Defender/AvgCPULoadFactor](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-avgcpuloadfactor) – Specify the maximum average CPU % usage that Microsoft Defender can use during a scan.  

  **Default**: 50

- **Scan mapped network drives during a full scan**  
  [Defender/AllowFullScanOnMappedNetworkDrives](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanonmappednetworkdrives) - Set to *Yes* to have Microsoft Defender scan files on the network. The user can't remove detected malware from read-only files,

  Related setting in this list: *Defender/AllowScanningNetworkFiles*

  **Default**: Yes

- **Block end-user access to Defender**  
  [Defender/AllowUserUIAccess](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowuseruiaccess) – Set to *Yes* to block end-users access to the Microsoft Defender UI on their device.  

  **Default**: Yes

- **Quick scan start time**  
  [Defender/ScheduleQuickScanTime](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulequickscantime) - Schedule a time of day for Defender to run a quick scan.  

  **Default**: 2 AM

## Microsoft Defender Firewall
For more information, see [Firewall CSP](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp) in the Windows documentation.

- **Security association idle time before deletion** - *MdmStore/Global/SaIdleTime*   
  Security associations are deleted after network traffic isn't seen for this number of seconds.  
  **Default**: 300

- **File Transfer Protocol** - *MdmStore/Global/DisableStatefulFtp*   
  Blocks stateful File Transfer Protocol (FTP).  
  **Default**: Yes

- **Packet queuing** - *MdmStore/Global/EnablePacketQueue*    
  Specify how scaling for the software on the receive side is enabled for the encrypted receive and clear text forward for the IPsec tunnel gateway scenario. This ensures that the packet order is preserved.  
  **Default**: Device default

- **Firewall profile domain** - *FirewallRules/FirewallRuleName/Profiles*  
  Specifies the profiles to which the rule belongs: Domain, Private, Public. This value represents the profile for networks that are connected to domains.  

  Available settings:  
  - **Unicast responses to multicast broadcasts required**  
    **Default**: Yes

  - **Authorized application rules from group policy merged**  
    **Default**: Yes

  - **Inbound notifications blocked**  
    **Default**: Yes

  - **Global port rules from group policy merged**  
    **Default**: Yes

  - **Stealth mode blocked**  
    **Default**: Yes

  - **Firewall enabled**  
    **Default**: Allowed

  - **Connection security rules from group policy not merged**  
    **Default**: Yes

  - **Policy rules from group policy not merged**  
    **Default**: Yes

- **Firewall profile public** - *FirewallRules/FirewallRuleName/Profiles*  
  Specifies the profiles to which the rule belongs: Domain, Private, Public. This value represents the profile for public networks. These networks are classified as public by the administrators in the server host. The classification happens the first time the host connects to the network. Usually these networks are at airports, coffee shops, and other public places where the peers in the network or the network administrator aren't trusted.  

  Available settings:

  - **Inbound connections blocked**  
    **Default**: Yes 

  - **Unicast responses to multicast broadcasts required**  
    **Default**: Yes  

  - **Stealth mode required**  
    **Default**: Yes 
 
  - **Outbound connections required**  
    **Default**: Yes  

  - **Authorized application rules from group policy merged**  
    **Default**: Yes  

  - **Inbound notifications blocked**  
    **Default**: Yes  

  - **Global port rules from group policy merged**  
    **Default**: Yes

  - **Stealth mode blocked**  
    **Default**: Yes

  - **Firewall enabled**  
    **Default**: Allowed  

  - **Connection security rules from group policy not merged**  
    **Default**: Yes  

  - **Incoming traffic required**  
    **Default**: Yes

  - **Policy rules from group policy not merged**  
    **Default**: Yes  

- **Firewall profile private** - *FirewallRules/FirewallRuleName/Profiles*  
  Specifies the profiles to which the rule belongs: Domain, Private, Public. This value represents the profile for private networks.  

  Available settings: 

  - **Inbound connections blocked**  
    **Default**: Yes

  - **Unicast responses to multicast broadcasts required**  
    **Default**: Yes

  - **Stealth mode required**  
    **Default**: Yes

  - **Outbound connections required**  
    **Default**: Yes

  - **Inbound notifications blocked**  
    **Default**: Yes

  - **Global port rules from group policy merged**  
    **Default**: Yes

  - **Stealth mode blocked**  
    **Default**: Yes  

  - **Firewall enabled**  
    **Default**: Allowed

  - **Authorized application rules from group policy not merged**  
    **Default**: Yes

  - **Connection security rules from group policy not merged**  
    **Default**: Yes

  - **Incoming traffic required**  
    **Default**: Yes

  - **Policy rules from group policy not merged**  
    **Default**: Yes  

- **Firewall pre shared key encoding method**  
  **Default**: UTF8

- **Certificate revocation list verification**  
  **Default**: Device default

## Web & Network Protection  

- **Network protection type**  
  [Defender/EnableNetworkProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)  - This policy allows you to turn network protection on or off in Microsoft Defender Exploit Guard. Network protection is a feature of Microsoft Defender Exploit Guard that protects employees using any app from accessing phishing scams, exploit-hosting sites, and malicious content on the Internet. This includes preventing third-party browsers from connecting to dangerous sites.  

  When set to either *Enable* or *Audit mode*, users can’t turn off network protection, and you can use the Microsoft Defender Security Center to view information about connection attempts.  
 
  - *Enable* will block users and apps from connecting to dangerous domains.  
  - *Audit mode* doesn’t block users and apps from connecting to dangerous domains.  

  When set to *User defined*, users and apps aren’t blocked from connecting to dangerous domains, and information about connections isn’t available in Microsoft Defender Security Center.  

  **Default**: Audit mode

- **Require SmartScreen for Microsoft Edge**  
  [Browser/AllowSmartScreen](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen) - Microsoft Edge uses Microsoft Defender SmartScreen (turned on) to protect users from potential phishing scams and malicious software by default. By default, this policy is enabled (set to *Yes*), and when enabled prevents users from turning off Microsoft Defender SmartScreen.  When the effective policy for a device is equal to Not configured, users can turn off Microsoft Defender SmartScreen, which leaves the device unprotected.  

  **Default**: Yes
  
- **Block malicious site access**  
  [Browser/PreventSmartScreenPromptOverride](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride) - By default, Microsoft Edge allows users to bypass (ignore) the Microsoft Defender SmartScreen warnings about potentially malicious sites, allowing users to continue to the site. With this policy enabled (set to *Yes*), Microsoft Edge prevents users from bypassing the warnings and blocks them from continuing to the site.  

  **Default**: Yes

- **Block unverified file download**  
  [Browser/PreventSmartScreenPromptOverrideForFiles](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles) - By default, Microsoft Edge allows users to bypass (ignore) the Microsoft Defender SmartScreen warnings about potentially malicious files, allowing them to continue downloading unverified files. With this policy enabled (set to *Yes*), users are prevented from bypassing the warnings and can't download unverified files.  

  **Default**: Yes

## Windows Hello for Business  

For more information, see [PassportForWork CSP](https://docs.microsoft.com/windows/client-management/mdm/passportforwork-csp) in the Windows documentation.

- **Configure Windows Hello for Business** - *TenantId/Policies/UsePassportForWork*    
  Windows Hello for Business is an alternative method for signing into Windows by replacing passwords, Smart Cards, and Virtual Smart Cards.  


  > [!IMPORTANT]
  > The options for this setting are reversed from their implied meaning. While reversed, a value of *Yes* does not enable Windows Hello and instead is treated as *Not configured*. When this setting is set to *Not configured*, Windows Hello is enabled on devices that receive this baseline.
  >
  > The following descriptions have been revised to reflect this behavior. The reversal of settings will be fixed in a future update to this security baseline.

  - When set to *Not configured*, Windows Hello is enabled, and the device provisions Windows Hello for Business.
  - When set to *Yes*, the baseline does not affect the policy setting of the device. This means that if Windows Hello for Business is disabled on a device, it remains disabled. If it's enabled, it remains enabled.
  <!-- expected behavior 
  - When set to *Yes*, you  enable this policy and the device provisions Windows Hello for Business.  
  - When set to *Not configured*, the baseline does not affect the policy setting of the device. This means that if Windows Hello for Business is disabled on a device, it remains disabled. If its enabled, it remains enabled. 
  -->

  You cannot disable Windows Hello for Business through this baseline. You can disable Windows Hello for Business when you configure [Windows enrollment](windows-hello.md), or as part of a device configuration profile for [identity protection](identity-protection-configure.md).  

Windows Hello for Business is an alternative method for signing into Windows by replacing passwords, Smart Cards, and Virtual Smart Cards.  

  If you enable or don't configure this policy setting, the device provisions Windows Hello for Business. If you disable this policy setting, the device doesn't provision Windows Hello for Business for any user.

  Intune doesn't support disabling Windows Hello. Instead, you can configure policy to enable Windows Hello for Business (Yes), or to not configure Windows Hello directly (not configured). When not configured, a device can receive configuration through other policy, which might enable or disable this feature.  

  **Default**: Yes  

- **Require lowercase letters in PIN** - *TenantId/Policies/PINComplexity/LowercaseLetters*  
  **Default**: Allowed  

- **Require special characters in PIN** - *TenantId/Policies/PINComplexity/SpecialCharacters*  
  **Default**: Allowed  

- **Require uppercase letters in PIN** - *TenantId/Policies/PINComplexity/UppercaseLetters*   
  **Default**: Allowed  

