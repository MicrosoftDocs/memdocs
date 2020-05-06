---
# required metadata

title: Intune endpoint security Attack surface reduction settings | Microsoft Docs
description: Endpoint security Attack surface reduction policy settings in Microsoft Intune 
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
# Attack surface reduction policy settings for endpoint security in Intune

View the settings you can configure in profiles for *Attack surface reduction* policy in the endpoint security node of Intune as part of an [Endpoint security policy](../protect/endpoint-security-policy.md).

Supported platforms and profiles:

- **Windows 10 and later**:
  - Profile: **App and browser isolation**
  - Profile: **Web protection**
  - Profile: **Application control**
  - Profile: **Attack surface reduction rules**
  - Profile: **Device control**
  - Profile: **Exploit protection**

## App and browser isolation profile

### App and browser isolation

- **Turn on Application Guard for Edge (Options)**  
  CSP: [AllowWindowsDefenderApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872350)

  - **Not configured** (*default*)
  - **Enabled for Edge** - Application Guard opens unapproved sites in a Hyper-V virtualized browsing container.

  When set to *Enabled for Edge*, the following settings are available:
  
  - **Clipboard behavior**  
    CSP: [ClipboardSettings](https://go.microsoft.com/fwlink/?linkid=872351)

    Choose what copy and paste actions are allowed from the local PC and an Application Guard virtual browser.
    - **Not configured** (*default*)
    - **Block copy and paste between PC and browser**
    - **Allow copy and paste from browser to PC only**
    - **Allow copy and paste from PC to browser only**
    - **Allow copy and paste between PC and browser**

  - **Block external content from non-enterprise approved sites**  
    CSP: [BlockNonEnterpriseContent](https://go.microsoft.com/fwlink/?linkid=872352)

    - **Not configured** (*default*)
    - **Yes** - Block content from unapproved websites from loading.

  - **Collect logs for events that occur within an Application Guard browsing session**  
    CSP: [AuditApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872418)

    - **Not configured** (*default*)
    - **Yes** - Collect logs for events that occur within an Application Guard virtual browsing session.

  - **Allow user-generated browser data to be saved**  
    CSP: [AllowPersistence](https://go.microsoft.com/fwlink/?linkid=872419)

    - **Not configured** (*default*)
    - **Yes** - Allow user data that is created during an Application Guard virtual browsing session to be saved. Examples of user data include passwords, favorites, and cookies.

  - **Enable hardware graphics acceleration**  
    CSP: [AllowVirtualGPU](https://go.microsoft.com/fwlink/?linkid=872420)

    - **Not configured** (*default*)
    - **Yes** - Within the Application Guard virtual browsing session, use a virtual graphics processing unit to load graphics-intensive websites faster.

  - **Allow users to download files onto the host**  
    CSP: [SaveFilesToHost](https://go.microsoft.com/fwlink/?linkid=872421)

    - **Not configured** (*default*)
    - **Yes** - Allow users to download files from the virtualized browser onto the host operating system​.

- **Application guard allow print to local printers**  

  - **Not configured** (*default*)
  - **Yes** - Allow printing print to local printers.

- **Application guard allow print to network printers**  

  - **Not configured** (*default*)
  - **Yes** - Allow printing print to network printers.

- **Application guard allow print to PDF**  

  - **Not configured** (*default*)
  - **Yes**- Allow printing print to PDF.

- **Application guard allow print to XPS**  

  - **Not configured** (*default*)
  - **Yes** - - Allow printing print to XPS.

- **Windows network isolation policy**  
  
  - **Not configured** (*default*)
  - **Yes** - Configure Windows network isolation policy.  
  
  When set to *Configure*, you can configure the following settings.

  - **IP ranges**  
    Expand the dropdown, select **Add**, and then specify a *lower address* and then an *upper address*.

  - **Cloud resources**  
    Expand the dropdown, select **Add**, and then specify an *IP address or FQDN* and a *Proxy*.

  - **Network domains**  
   Expand the dropdown, select **Add**, and then specify *Network domains*.

  - **Proxy servers**  
    Expand the dropdown, select **Add**, and then specify *Proxy servers*.

  - **Internal proxy servers**  
    Expand the dropdown, select **Add**, and then specify *Internal proxy servers*.

  - **Neutral resources**  
    Expand the dropdown, select **Add**, and then specify *Neutral resources*.

  - **Disable Auto detection of other enterprise proxy servers**  
    - **Not configured** (*default*)
    - **Yes** - Disable Auto detection of other enterprise proxy servers.

  - **Disable Auto detection of other enterprise IP ranges**  
    - **Not configured** (*default*)
    - **Yes** - Disable Auto detection of other enterprise IP ranges.

## Web protection profile

### Web Protection

- **Enable network protection**  
  CSP: [EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=872618)

  - **Not configured** (*default*) - The setting returns to the Windows default, which is disabled.
  - **User defined**
  - **Enable** - Network protection is enabled for all users on the system.
  - **Audit mode** - Users aren't blocked from dangerous domains and Windows events are raised instead.

- **Require SmartScreen for Microsoft Edge**  
  CSP: [Browser/AllowSmartScreen](https://go.microsoft.com/fwlink/?linkid=2067029)

  - **Yes** - Use SmartScreen to protect users from potential phishing scams and malicious software.
  - **Not configured** (*default*)

- **Block malicious site access**  
  CSP: [Browser/PreventSmartScreenPromptOverride](https://go.microsoft.com/fwlink/?linkid=2067040)  

  - **Yes** - Block users from ignoring the Microsoft Defender SmartScreen Filter warnings and block them from going to the site.
  - **Not configured** (*default*)

- **Block unverified file download**  
  CSP: [Browser/PreventSmartScreenPromptOverrideForFiles](https://go.microsoft.com/fwlink/?linkid=2067023)  

  - **Yes** - Block users from ignoring the Microsoft Defender SmartScreen Filter warnings and block them from downloading unverified files.
  - **Not configured** (*default*)

## Application control profile

### Microsoft Defender Application Control

- **App locker application control**  
  - **Not configured** (*default*)
  - **Enforce Components and Store Apps**
  - **Audit Components and Store Apps**
  - **Enforce Components, Store Apps, and Smartlocker**
  - **Audit Components, Store Apps, and SMartlocker**

- **Block users from ignoring SmartScreen warnings**  
  [PreventOverrideForFilesInShell](https://go.microsoft.com/fwlink/?linkid=872783)

  This setting requires the 'Enforce SmartScreen for apps and files' setting be enabled.
  - **Not configured** (*default*) - Returns the setting to the Windows default, which allows the user override.
  - **Yes** - - SmartScreen won't present an option for the user to disregard the warning and run the app. The warning is presented, but the user won't able to bypass it.

- **Turn on Windows SmartScreen**  
  CSP: [SmartScreen/EnableSmartScreenInShell](https://go.microsoft.com/fwlink/?linkid=872784)

  - **Not configured** (*default*) - Return the setting to Windows default, which is to enable SmartScreen, however users may change this setting. To disable SmartScreen, use a custom URI.
  - **Yes** - Enforce the use of SmartScreen for all users.

## Attack surface reduction rules profile

### Attack Surface Reduction Rules

- **Block credential stealing from the Windows local security authority subsystem (lsass.exe)**  
  <!-- Defender ATP security baseline, Device configuration Endpoint protection profile -->
  [Protect devices from exploits](https://go.microsoft.com/fwlink/?linkid=874499)

  This attack surface reduction (ASR) rule is controlled via the following GUID: 9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2
  - **Not configured** (*default*) - The setting returns to the Windows default, which is off.
  - **User defined**
  - **Enable** - Attempts to steal credentials via lsass.exe are blocked.
  - **Audit mode** - Users aren't blocked from dangerous domains and Windows events are raised instead.

- **Block Adobe Reader from creating child processes**  
  [Reduce attack surfaces with attack surface reduction rules](https://go.microsoft.com/fwlink/?linkid=853979)
  
  This ASR rule is controlled via the following GUID: 7674ba52-37eb-4a4f-a9a1-f0f9a1619a2c
  - **Not configured** (*default*) - The Windows default is restored, is to not block creation of child processes.
  - **User defined**
  - **Enable** - Adobe Reader is blocked from creating child processes.
  - **Audit mode** - Windows events are raised instead of blocking child processes.

- **Block Office applications from injecting code into other processes**  
  [Protect devices from exploits](https://go.microsoft.com/fwlink/?linkid=872974)

  This ASR rule is controlled via the following GUID: 75668C1F-73B5-4CF0-BB93-3ECF5CB7CC84
  - **Not configured** (*default*) - The setting returns to the Windows default, which is off.
  - **Block** - Office applications are blocked from injecting code into other processes.
  - **Audit mode** - Windows events are raised instead of blocking.

- **Block Office applications from creating executable content**  
  [Protect devices from exploits](https://go.microsoft.com/fwlink/?linkid=872975)

  This ASR rule is controlled via the following GUID: 3B576869-A4EC-4529-8536-B80A7769E899
  - **Not configured** (*default*) - The setting returns to the Windows default, which is off.
  - **Block** - Office applications are blocked from creating executable content.
  - **Audit mode** - Windows events are raised instead of blocking.

- **Block all Office applications from creating child processes**  
  [Protect devices from exploits](https://go.microsoft.com/fwlink/?linkid=872976)

  This ASR rule is controlled via the following GUID: D4F940AB-401B-4EFC-AADC-AD5F3C50688A
  - **Not configured** (*default*) - The setting returns to the Windows default, which is off.
  - **Block** - Office applications are blocked from creating child processes.
  - **Audit mode** - Windows events are raised instead of blocking.

- **Block Win32 API calls from Office macro**  
  [Protect devices from exploits](https://go.microsoft.com/fwlink/?linkid=872977)

  This ASR rule is controlled via the following GUID: 92E97FA1-2EDF-4476-BDD6-9DD0B4DDDC7B
  - **Not configured** (*default*) - The setting returns to the Windows default, which is off.
  - **Block**  - Office macro's are blocked from using Win32 API calls.
  - **Audit mode** - Windows events are raised instead of blocking.

- **Block Office communication apps from creating child processes**  
  [Protect devices from exploits](https://go.microsoft.com/fwlink/?linkid=874499)  

  This ASR rule is controlled via the following GUID: 26190899-1602-49e8-8b27-eb1d0a1ce869.
  - **Not configured** (*default*) - The Windows default is restored, which is to not block creation of child processes.
  - **User defined**
  - **Enable** - Office communication applications are blocked from creating child processes.
  - **Audit mode** - Windows events are raised instead of blocking child processes.

- **Block execution of potentially obfuscated scripts (js/vbs/ps)**  
  [Protect devices from exploits](https://go.microsoft.com/fwlink/?linkid=872978)

  This ASR rule is controlled via the following GUID: 5BEB7EFE-FD9A-4556-801D-275E5FFC04CC
  - **Not configured** (*default*) - The setting returns to the Windows default, which is off.
  - **Block** - Defender blocks execution of obfuscated scripts.
  - **Audit mode** - Windows events are raised instead of blocking.

- **Block JavaScript or VBScript from launching downloaded executable content**  
  [Protect devices from exploits](https://go.microsoft.com/fwlink/?linkid=872979)

   This ASR rule is controlled via the following GUID: D3E037E1-3EB8-44C8-A917-57927947596D
  - **Not configured** (*default*) - The setting returns to the Windows default, which is off.
  - **Block** - Defender blocks JavaScript or VBScript files that have been downloaded from the Internet from being executed.
  - **Audit mode** - Windows events are raised instead of blocking.

- **Block process creations originating from PSExec and WMI commands**  
  [Protect devices from exploits](https://go.microsoft.com/fwlink/?linkid=874500)

  This ASR rule is controlled via the following GUID: d1e49aac-8f56-4280-b9ba-993a6d77406c
  - **Not configured** (*default*) - The setting returns to the Windows default, which is off.
  - **Block** - Process creation by PSExec or WMI commands is blocked.
  - **Audit mode** - Windows events are raised instead of blocking.

- **Block untrusted and unsigned processes that run from USB**  
  [Protect devices from exploits](https://go.microsoft.com/fwlink/?linkid=874502)

  This ASR rule is controlled via the following GUID: b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4
  - **Not configured** (*default*) - The setting returns to the Windows default, which is off.
  - **Block** - Untrusted and unsigned processes that run from a USB drive are blocked.
  - **Audit mode** - Windows events are raised instead of blocking.

- **Block executable files from running unless they meet a prevalence, age, or trusted list criteria**  
  [Protect devices from exploits](https://go.microsoft.com/fwlink/?linkid=874503)

  This ASR rule is controlled via the following GUID: 01443614-cd74-433a-b99e-2ecdc07bfc25e
  - **Not configured** (*default*) - The setting returns to the Windows default, which is off.
  - **Block**
  - **Audit mode** - Windows events are raised instead of blocking.

- **Block executable content download from email and webmail clients**  
  [Protect devices from exploits](https://go.microsoft.com/fwlink/?linkid=872980)

  - **Not configured** (*default*) - The setting returns to the Windows default, which is off.
  - **Block** - Executable content downloaded from email and webmail clients is blocked.
  - **Audit mode** - Windows events are raised instead of blocking.

- **Use advanced protection against ransomware**  
   [Protect devices from exploits](https://go.microsoft.com/fwlink/?linkid=874504)

  This ASR rule is controlled via the following GUID: c1db55ab-c21a-4637-bb3f-a12568109d35
  - **Not configured** (*default*) - The setting returns to the Windows default, which is off.
  - **User defined**
  - **Enable**
  - **Audit mode** - - Windows events are raised instead of blocking.

- **Enable folder protection**  
  CSP: [EnableControlledFolderAccess](https://go.microsoft.com/fwlink/?linkid=872614)

  - **Not configured** (*default*) - This setting returns to its default, which is no read or writes are blocked.
  - **Enable** - For untrusted apps, Defender blocks attempts to modify or delete files in protected folders, or write to disk sectors. Defender automatically determines which applications can be trusted. Alternatively, you can define your own list of trusted applications.
  - **Audit mode** - Windows events are raised when untrusted applications access controlled folders, but no blocks are enforced.
  - **Block disk modification** - Only attempts to write to disk sectors are blocked.
  - **Audit disk modification** - Windows events are raised instead of blocking attempts to write to disk sectors.
  
- **Exclude files and paths from attack surface reduction rules**  
  CSP: [AttackSurfaceReductionOnlyExclusions](https://go.microsoft.com/fwlink/?linkid=872981)

  Expand the dropdown and then select **Add** to define a **Path** to a file or folder to exclude from your attack surface reduction rules.

## Device control profile

### Device Control

- **Hardware device installation by device identifiers**  
  [PreventInstallationOfMatchingDeviceIDs](https://go.microsoft.com/fwlink/?linkid=2066794)  
  
  This setting allows you to specify a list of Plug and Play hardware IDs and compatible IDs for devices that Windows is prevented from installing. This policy setting takes precedence over any other policy setting that allows Windows to install a device.  If you enable this policy setting on a remote desktop server, the policy setting affects redirection of the specified devices from a remote desktop client to the remote desktop server.

  - **Not configured**
  - **Allow hardware device installation** - Devices can be installed and updated as allowed or prevented by other policy settings.
  - **Block hardware device installation** (*default*) - Windows is prevented from installing a device whose hardware ID or compatible ID appears in a list you define.

  When set to *Block hardware device installation* you can configure the following settings:

  - **Remove matching hardware devices**

    This setting is available only when *Hardware device installation by device identifiers* is set to *Block hardware device installation*.
    - **Yes**
    - **Not configured**

  - **Hardware device identifiers that are blocked**  

    This setting is available only when *Hardware device installation by device identifiers* is set to *Block hardware device installation*.

    Select **Add**, and then specify the hardware device identifier you want to block.

- **Hardware device installation by setup classes**  
  CSP: [DeviceInstallation/AllowInstallationOfMatchingDeviceSetupClasses](https://go.microsoft.com/fwlink/?linkid=2067048)  
  
  This policy setting allows you to specify a list of device setup class globally unique identifiers (GUIDs) for device drivers that Windows is prevented from installing. This policy setting takes precedence over any other policy setting that allows Windows to install a device. If you enable this policy setting on a remote desktop server, the policy setting affects redirection of the specified devices from a remote desktop client to the remote desktop server.

  - **Not configured**
  - **Allow hardware device installation** - Windows can install and update devices as allowed or prevented by other policy settings.
  - **Block hardware device installation** (*default*) - Windows is prevented from installing a device whose setup class GUIDs appear in a list you define.

  When set to *Block hardware device installation* you can configure *Remove matching hardware devices* and *Hardware device identifiers that are blocked*.

  - **Remove matching hardware devices**

    This setting is available only when *Hardware device installation by device identifiers* is set to *Block hardware device installation*.
    - **Yes**
    - **Not configured**

  - **Hardware device identifiers that are blocked**

    This setting is available only when *Hardware device installation by device identifiers* is set to *Block hardware device installation*.

    Select **Add**, and then specify the hardware device identifier you want to block.

- **Scan removable drives during full scan**  
  CSP: [Defender/AllowFullScanRemovableDriveScanning](https://go.microsoft.com/fwlink/?linkid=2113946)

  - **Not configured** (*default*) - The setting returns to client default, which scans removable drives, however the user can disable this scan.
  - **Yes** - During a full scan, removable drives (like USB flash drives) are scanned.
  
## Exploit protection profile

### Exploit protection

- **Upload XML**  
  CSP: [ExploitProtectionSettings](https://go.microsoft.com/fwlink/?linkid=2067035)

  Enables the IT admin to push out a configuration representing the desired system and application mitigation options to all the devices in the organization. The configuration is represented by an XML file. Exploit protection can help protect devices from malware that use exploits to spread and infect. You use the Windows Security app or PowerShell to create a set of mitigations (known as a configuration). You can then export this configuration as an XML file and share it with multiple machines on your network so they all have the same set of mitigation settings. You can also convert and import an existing EMET configuration XML file into an exploit protection configuration XML.

  Choose **Select XML File**, specify the XML filet upload, and then click **Select**.
  - **Not configured** (*default*)
  - **Yes**

- **Block users from editing the Exploit Guard protection interface**  
  CSP: [DisallowExploitProtectionOverride](https://go.microsoft.com/fwlink/?linkid=2067239)

  - **Not configured** (*default*) - Local users can make changes in the exploit protection settings area.
  - **Yes** - Prevent users from making changes to the exploit protection settings area in the Microsoft Defender Security Center.

## Next steps

[Endpoint security policy for ASR](../protect/endpoint-security-policy.md#attack-surface-reduction-profiles)
