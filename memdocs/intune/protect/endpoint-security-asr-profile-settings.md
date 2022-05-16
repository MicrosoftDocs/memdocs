---
# required metadata

title: Intune endpoint security Attack surface reduction settings | Microsoft Docs
description: Details about the settings in the endpoint security Attack surface reduction policies in Microsoft Intune. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/06/2022
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
ms.reviewer: mattcall

---
# Attack surface reduction policy settings for endpoint security in Intune

View the settings you can configure in profiles for *Attack surface reduction* policy in the endpoint security node of Intune as part of an [Endpoint security policy](../protect/endpoint-security-policy.md).

Applies to:

- Windows 11
- Windows 10

Supported platforms and profiles:

- **Windows 10 and later** - Use this platform for policy you deploy to devices managed with Intune.

  - Profile: **App and browser isolation**
  - Profile: **Application control**
  - Profile: **Attack surface reduction rules**
  - Profile: **Device control**
  - Profile: **Exploit protection**
  - Profile: **Web protection (Microsoft Edge Legacy)**

- **Windows 10 and later (ConfigMgr)**: Use this platform for policy you deploy to devices managed by Configuration Manager.

  - Profile: **Exploit Protection(ConfigMgr)(preview)**
  - Profile: **Web Protection (ConfigMgr)(preview)**

## Attack surface reduction (MDM)

### App and browser isolation profile

#### App and browser isolation

- **Turn on Application Guard**  
  CSP: [AllowWindowsDefenderApplicationGuard](/windows/client-management/mdm/windowsdefenderapplicationguard-csp#allowwindowsdefenderapplicationguard)

  - **Not configured** (*default*) - Microsoft Defender Application Guard is not configured for Microsoft Edge or isolated Windows environments.
  - **Enabled for Edge** - Application Guard opens unapproved sites in a Hyper-V virtualized browsing container.
  - **Enabled for isolated Windows environments** - Application Guard is turned on for any applications enabled for App Guard within Windows.
  - **Enabled for Edge AND isolated Windows environments** - Application Guard is configured for both scenarios.
  
  > [!NOTE]
  > If you are deploying Application Guard for Microsoft Edge via Intune, **Windows network isolation** policy must be configured as a prerequisite. Network isolation may be configured via various profiles, including **App and broswer isolation** under the **Windows network isolation** setting. 

  When set to *Enabled for Edge* or *Enabled for Edge AND isolated Windows environments*, the following settings are available, which apply to Edge:
  
  - **Clipboard behavior**  
    CSP: [ClipboardSettings](/windows/client-management/mdm/windowsdefenderapplicationguard-csp#clipboardsettings)

    Choose what copy and paste actions are allowed from the local PC and an Application Guard virtual browser.
    - **Not configured** (*default*)
    - **Block copy and paste between PC and browser**
    - **Allow copy and paste from browser to PC only**
    - **Allow copy and paste from PC to browser only**
    - **Allow copy and paste between PC and browser**

  - **Block external content from non-enterprise approved sites**  
    CSP: [BlockNonEnterpriseContent](/windows/client-management/mdm/windowsdefenderapplicationguard-csp#blocknonenterprisecontent)

    - **Not configured** (*default*)
    - **Yes** - Block content from unapproved websites from loading.

  - **Collect logs for events that occur within an Application Guard browsing session**  
    CSP: [AuditApplicationGuard](/windows/client-management/mdm/windowsdefenderapplicationguard-csp#auditapplicationguard)

    - **Not configured** (*default*)
    - **Yes** - Collect logs for events that occur within an Application Guard virtual browsing session.

  - **Allow user-generated browser data to be saved**  
    CSP: [AllowPersistence](/windows/client-management/mdm/windowsdefenderapplicationguard-csp#allowpersistence)

    - **Not configured** (*default*)
    - **Yes** - Allow user data that is created during an Application Guard virtual browsing session to be saved. Examples of user data include passwords, favorites, and cookies.

  - **Enable hardware graphics acceleration**  
    CSP: [AllowVirtualGPU](/windows/client-management/mdm/windowsdefenderapplicationguard-csp#allowvirtualgpu)

    - **Not configured** (*default*)
    - **Yes** - Within the Application Guard virtual browsing session, use a virtual graphics processing unit to load graphics-intensive websites faster.

  - **Allow users to download files onto the host**  
    CSP: [SaveFilesToHost](/windows/client-management/mdm/windowsdefenderapplicationguard-csp#savefilestohost)

    - **Not configured** (*default*)
    - **Yes** - Allow users to download files from the virtualized browser onto the host operating system​.

  - **Application Guard allow camera and microphone access**  
    CSP: [AllowCameraMicrophoneRedirection](/windows/client-management/mdm/windowsdefenderapplicationguard-csp#allowcameramicrophoneredirection)

    - **Not configured** (*default*) - Applications inside Microsoft Defender Application Guard can't access the camera and microphone on the user’s device.
    - **Yes** - Applications inside Microsoft Defender Application Guard can access the camera and microphone on the user’s device.
    - **No** - Applications inside Microsoft Defender Application Guard can't access the camera and microphone on the user’s device. This is the same behavior as *Not configured*.



- **Application guard allow print to local printers**  

  - **Not configured** (*default*)
  - **Yes** - Allow printing to local printers.

- **Application guard allow print to network printers**  

  - **Not configured** (*default*)
  - **Yes** - Allow printing print to network printers.

- **Application guard allow print to PDF**  

  - **Not configured** (*default*)
  - **Yes**- Allow printing print to PDF.

- **Application guard allow print to XPS**  

  - **Not configured** (*default*)
  - **Yes** - - Allow printing print to XPS.

- **Application Guard allow use of Root Certificate Authorities from the user's device**  
  CSP: [CertificateThumbprints](/windows/client-management/mdm/windowsdefenderapplicationguard-csp#certificatethumbprints)

  Configure certificate thumbprints to automatically transfer the matching root certificate to the  Microsoft Defender Application Guard container.

  To add thumbprints one at a time, select **Add**. You can use **Import** to specify a .CSV file that contains multiple thumbprint entries that are all added to the profile at the same time. When you use a .CSV file, each thumbprint must be separated by a comma. For example: `b4e72779a8a362c860c36a6461f31e3aa7e58c14,1b1d49f06d2a697a544a1059bd59a7b058cda924`

  All entries that are listed in the profile are active. You do not need to select a checkbox for a thumbprint entry to make it active. Instead, use the checkboxes to help you manage the entries that have been added to the profile. For example, you can select the checkbox of one or more certificate thumbprint entries and then **Delete** those entries from the profile with a single action.

- **Windows network isolation policy**  
  
  - **Not configured** (*default*)
  - **Yes** - Configure Windows network isolation policy.  
  
  When set to *Yes*, you can configure the following settings:

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

### Application control profile

#### Microsoft Defender Application Control

- **App locker application control**  
  CSP: [AppLocker](/windows/client-management/mdm/applocker-csp)

  - **Not configured** (*default*)
  - **Enforce Components and Store Apps**
  - **Audit Components and Store Apps**
  - **Enforce Components, Store Apps, and Smartlocker**
  - **Audit Components, Store Apps, and Smartlocker**

- **Block users from ignoring SmartScreen warnings**  
  CSP: [SmartScreen/PreventOverrideForFilesInShell](/windows/client-management/mdm/policy-csp-smartscreen#smartscreen-preventoverrideforfilesinshell)

  - **Not configured** (*default*) - Users can ignore SmartScreen warnings for files and malicious apps.
  - **Yes** - SmartScreen is enabled and users can't bypass warnings for files or malicious apps.

- **Turn on Windows SmartScreen**  
  CSP: [SmartScreen/EnableSmartScreenInShell](/windows/client-management/mdm/policy-csp-smartscreen#smartscreen-enablesmartscreeninshell)

  - **Not configured** (*default*) - Return the setting to Windows default, which is to enable SmartScreen, however users may change this setting. To disable SmartScreen, use a custom URI.
  - **Yes** - Enforce the use of SmartScreen for all users.

### Attack surface reduction rules profile

#### Attack Surface Reduction Rules

> [!NOTE]  
> This section details the settings in Attack Surface Reduction Rules profiles created before April 5, 2022. Profiles created after that date use a new settings format as found in the Settings Catalog. Although you can no longer create new instances of the original profile, you can continue to edit and use your existing profiles.  

- **Block persistence through WMI event subscription**  
  [Reduce attack surfaces with attack surface reduction rules](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  This attack surface reduction (ASR) rule is controlled via the following GUID: 9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2

  This rule prevents malware from abusing WMI to attain persistence on a device. Fileless threats employ various tactics to stay hidden, to avoid being seen in the file system, and to gain periodic execution control. Some threats can abuse the WMI repository and event model to stay hidden.

  - **Not configured** (default) – The setting returns to the Windows default, which is off and persistence is not blocked.
  - **Block** – Persistence through WMI is blocked.
  - **Audit** – Evaluate how this rule affects your organization if it's enabled (set to Block).
  - **Disable** - Turn this rule off. Persistence is not blocked.

  To learn more about this setting, see [Block persistence through WMI event subscription](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx#block-persistence-through-wmi-event-subscription).

- **Block credential stealing from the Windows local security authority subsystem (lsass.exe)**  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  This attack surface reduction (ASR) rule is controlled via the following GUID: 9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2
  - **Not configured** (*default*) - The setting returns to the Windows default, which is off.
  - **User defined**
  - **Enable** - Attempts to steal credentials via lsass.exe are blocked.
  - **Audit mode** - Users aren't blocked from dangerous domains and Windows events are raised instead.
  - **Warn** - For Windows 10 version 1809 or later and Windows 11, the device user receives a message that they can bypass *Block* of the setting. On devices that run earlier versions of Windows 10, the rule enforces the *Enable* behavior.

- **Block Adobe Reader from creating child processes**  
  [Reduce attack surfaces with attack surface reduction rules](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)
  
  This ASR rule is controlled via the following GUID: 7674ba52-37eb-4a4f-a9a1-f0f9a1619a2c
  - **Not configured** (*default*) - The Windows default is restored, is to not block creation of child processes.
  - **User defined**
  - **Enable** - Adobe Reader is blocked from creating child processes.
  - **Audit mode** - Windows events are raised instead of blocking child processes.
  - **Warn** - For Windows 10 version 1809 or later and Windows 11, the device user receives a message that they can bypass *Block* of the setting. On devices that run earlier versions of Windows 10, the rule enforces the *Enable* behavior.

- **Block Office applications from injecting code into other processes**  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  This ASR rule is controlled via the following GUID: 75668C1F-73B5-4CF0-BB93-3ECF5CB7CC84
  - **Not configured** (*default*) - The setting returns to the Windows default, which is off.
  - **Block** - Office applications are blocked from injecting code into other processes.
  - **Audit mode** - Windows events are raised instead of blocking.
  - **Warn** - For Windows 10 version 1809 or later and Windows 11, the device user receives a message that they can bypass *Block* of the setting. On devices that run earlier versions of Windows 10, the rule enforces the *Enable* behavior.
  - **Disable** - This setting is turned off.

- **Block Office applications from creating executable content**  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  This ASR rule is controlled via the following GUID: 3B576869-A4EC-4529-8536-B80A7769E899
  - **Not configured** (*default*) - The setting returns to the Windows default, which is off.
  - **Block** - Office applications are blocked from creating executable content.
  - **Audit mode** - Windows events are raised instead of blocking.
  - **Warn** - For Windows 10 version 1809 or later and Windows 11, the device user receives a message that they can bypass *Block* of the setting. On devices that run earlier versions of Windows 10, the rule enforces the *Enable* behavior.
  - **Disable** - This setting is turned off.

- **Block all Office applications from creating child processes**  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  This ASR rule is controlled via the following GUID: D4F940AB-401B-4EFC-AADC-AD5F3C50688A
  - **Not configured** (*default*) - The setting returns to the Windows default, which is off.
  - **Block** - Office applications are blocked from creating child processes.
  - **Audit mode** - Windows events are raised instead of blocking.
  - **Warn** - For Windows 10 version 1809 or later and Windows 11, the device user receives a message that they can bypass *Block* of the setting. On devices that run earlier versions of Windows 10, the rule enforces the *Enable* behavior.
  - **Disable** - This setting is turned off.

- **Block Win32 API calls from Office macro**  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  This ASR rule is controlled via the following GUID: 92E97FA1-2EDF-4476-BDD6-9DD0B4DDDC7B
  - **Not configured** (*default*) - The setting returns to the Windows default, which is off.
  - **Block**  - Office macro's are blocked from using Win32 API calls.
  - **Audit mode** - Windows events are raised instead of blocking.
  - **Warn** - For Windows 10 version 1809 or later and Windows 11, the device user receives a message that they can bypass *Block* of the setting. On devices that run earlier versions of Windows 10, the rule enforces the *Enable* behavior.
  - **Disable** - This setting is turned off.

- **Block Office communication apps from creating child processes**  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)  

  This ASR rule is controlled via the following GUID: 26190899-1602-49e8-8b27-eb1d0a1ce869.
  - **Not configured** (*default*) - The Windows default is restored, which is to not block creation of child processes.
  - **User defined**
  - **Enable** - Office communication applications are blocked from creating child processes.
  - **Audit mode** - Windows events are raised instead of blocking child processes.
  - **Warn** - For Windows 10 version 1809 or later and Windows 11, the device user receives a message that they can bypass *Block* of the setting. On devices that run earlier versions of Windows 10, the rule enforces the *Enable* behavior.

- **Block execution of potentially obfuscated scripts (js/vbs/ps)**  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  This ASR rule is controlled via the following GUID: 5BEB7EFE-FD9A-4556-801D-275E5FFC04CC
  - **Not configured** (*default*) - The setting returns to the Windows default, which is off.
  - **Block** - Defender blocks execution of obfuscated scripts.
  - **Audit mode** - Windows events are raised instead of blocking.
  - **Warn** - For Windows 10 version 1809 or later and Windows 11, the device user receives a message that they can bypass *Block* of the setting. On devices that run earlier versions of Windows 10, the rule enforces the *Enable* behavior.
  - **Disable** - This setting is turned off.

- **Block JavaScript or VBScript from launching downloaded executable content**  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

   This ASR rule is controlled via the following GUID: D3E037E1-3EB8-44C8-A917-57927947596D
  - **Not configured** (*default*) - The setting returns to the Windows default, which is off.
  - **Block** - Defender blocks JavaScript or VBScript files that have been downloaded from the Internet from being executed.
  - **Audit mode** - Windows events are raised instead of blocking.
  - **Disable** - This setting is turned off.

- **Block process creations originating from PSExec and WMI commands**  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  This ASR rule is controlled via the following GUID: d1e49aac-8f56-4280-b9ba-993a6d77406c
  - **Not configured** (*default*) - The setting returns to the Windows default, which is off.
  - **Block** - Process creation by PSExec or WMI commands is blocked.
  - **Audit mode** - Windows events are raised instead of blocking.
  - **Warn** - For Windows 10 version 1809 or later and Windows 11, the device user receives a message that they can bypass *Block* of the setting. On devices that run earlier versions of Windows 10, the rule enforces the *Enable* behavior.
  - **Disable** - This setting is turned off.

- **Block untrusted and unsigned processes that run from USB**  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  This ASR rule is controlled via the following GUID: b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4
  - **Not configured** (*default*) - The setting returns to the Windows default, which is off.
  - **Block** - Untrusted and unsigned processes that run from a USB drive are blocked.
  - **Audit mode** - Windows events are raised instead of blocking.
  - **Warn** - For Windows 10 version 1809 or later and Windows 11, the device user receives a message that they can bypass *Block* of the setting. On devices that run earlier versions of Windows 10, the rule enforces the *Enable* behavior.
  - **Disable** - This setting is turned off.

- **Block executable files from running unless they meet a prevalence, age, or trusted list criteria**  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  This ASR rule is controlled via the following GUID: 01443614-cd74-433a-b99e-2ecdc07bfc25e
  - **Not configured** (*default*) - The setting returns to the Windows default, which is off.
  - **Block**
  - **Audit mode** - Windows events are raised instead of blocking.
  - **Warn** - For Windows 10 version 1809 or later and Windows 11, the device user receives a message that they can bypass *Block* of the setting. On devices that run earlier versions of Windows 10, the rule enforces the *Enable* behavior.
  - **Disable** - This setting is turned off.

- **Block executable content download from email and webmail clients**  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  - **Not configured** (*default*) - The setting returns to the Windows default, which is off.
  - **Block** - Executable content downloaded from email and webmail clients is blocked.
  - **Audit mode** - Windows events are raised instead of blocking.
  - **Warn** - For Windows 10 version 1809 or later and Windows 11, the device user receives a message that they can bypass *Block* of the setting. On devices that run earlier versions of Windows 10, the rule enforces the *Enable* behavior.
  - **Disable** - This setting is turned off.

- **Use advanced protection against ransomware**  
   [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  This ASR rule is controlled via the following GUID: c1db55ab-c21a-4637-bb3f-a12568109d35
  - **Not configured** (*default*) - The setting returns to the Windows default, which is off.
  - **User defined**
  - **Enable**
  - **Audit mode** - - Windows events are raised instead of blocking.

- **Enable folder protection**  
  CSP: [EnableControlledFolderAccess](/windows/client-management/mdm/policy-csp-defender#defender-enablecontrolledfolderaccess)

  - **Not configured** (*default*) - This setting returns to its default, which is no read or writes are blocked.
  - **Enable** - For untrusted apps, Defender blocks attempts to modify or delete files in protected folders, or write to disk sectors. Defender automatically determines which applications can be trusted. Alternatively, you can define your own list of trusted applications.
  - **Audit mode** - Windows events are raised when untrusted applications access controlled folders, but no blocks are enforced.
  - **Block disk modification** - Only attempts to write to disk sectors are blocked.
  - **Audit disk modification** - Windows events are raised instead of blocking attempts to write to disk sectors.
  
- **List of additional folders that need to be protected**  
  CSP: [ControlledFolderAccessProtectedFolders](/windows/client-management/mdm/policy-csp-defender#defender-controlledfolderaccessprotectedfolders)

  Define a list of disk locations that will be protected from untrusted applications.

- **List of apps that have access to protected folders**  
  CSP: [ControlledFolderAccessAllowedApplications](/windows/client-management/mdm/policy-csp-defender#defender-controlledfolderaccessallowedapplications)

  Define a list of apps that have access to read/write to controlled locations.

- **Exclude files and paths from attack surface reduction rules**  
  CSP: [AttackSurfaceReductionOnlyExclusions](/windows/client-management/mdm/policy-csp-defender#defender-attacksurfacereductiononlyexclusions)

  Expand the dropdown and then select **Add** to define a **Path** to a file or folder to exclude from your attack surface reduction rules.

### Device control profile

#### Device Control

> [!NOTE]  
> This section details the settings found in Device control profile created before May 23, 2022. Profiles created after that date use a new settings format as found in the Settings Catalog. Although you can no longer create new instances of the original profile, you can continue to edit and use your existing profiles.  

- **Allow hardware device installation by device identifiers**  
  - **Not configured** *(default)*
  - **Yes** - Windows can install or update any device whose Plug and Play hardware ID or compatible ID appears in the list you create unless another policy setting specifically prevents that installation. If you enable this policy setting on a remote desktop server, the policy setting affects redirection of the specified devices from a remote desktop client to the remote desktop server.
  - **No**

  When set to *Yes* you can configure the following options:
  - **Allow list** - Use *Add*, *Import*, and *Export* to manage a list of device identifiers.

- **Block hardware device installation by device identifiers**  
  CSP: [AllowInstallationOfMatchingDeviceIDs](/windows/client-management/mdm/policy-csp-deviceinstallation#deviceinstallation-allowinstallationofmatchingdeviceids)

  - **Not configured** *(default)*
  - **Yes** - Specify a list of Plug and Play hardware IDs and compatible IDs for devices that Windows is prevented from installing. This policy takes precedence over any other policy setting that allows Windows to install a device. If you enable this policy setting on a remote desktop server, the policy setting affects redirection of the specified devices from a remote desktop client to the remote desktop server.
  - **No**

  When set to *Yes* you can configure the following options:  
  - **Remove matching hardware devices**  
    - **Yes**
    - **Not configured** *(default)*

  - **Block list** - Use *Add*, *Import*, and *Export* to manage a list of device identifiers.

- **Allow hardware device installation by setup class**  
  - **Not configured** *(default)*
  - **Yes** - Windows can install or update device drivers whose device setup class GUIDs appear in the list you create unless another policy setting specifically prevents that installation. If you enable this policy setting on a remote desktop server, the policy setting affects redirection of the specified devices from a remote desktop client to the remote desktop server.
  - **No**

  When set to *Yes* you can configure the following options:
  - **Allow list** - Use *Add*, *Import*, and *Export* to manage a list of device identifiers.

- **Block hardware device installation by setup classes**  
  CSP: [AllowInstallationOfMatchingDeviceSetupClasses](/windows/client-management/mdm/policy-csp-deviceinstallation)

  - **Not configured** *(default)*
  - **Yes** - Specify a list of device setup class globally unique identifiers (GUIDs) for device drivers that Windows is prevented from installing. This policy setting takes precedence over any other policy setting that allows Windows to install a device. If you enable this policy setting on a remote desktop server, the policy setting affects redirection of the specified devices from a remote desktop client to the remote desktop server.
  - **No**

  When set to *Yes* you can configure the following options:  
  - **Remove matching hardware devices**  
    - **Yes**
    - **Not configured** *(default)*

  - **Block list** - Use *Add*, *Import*, and *Export* to manage a list of device identifiers.

- **Allow hardware device installation by device instance identifiers**  
  - **Not configured** *(default)*
  - **Yes** - Windows is allowed to install or update any device whose Plug and Play device instance ID appears in the list you create unless another policy setting specifically prevents that installation. If you enable this policy setting on a remote desktop server, the policy setting affects redirection of the specified devices from a remote desktop client to the remote desktop server.
  - **No**

  When set to *Yes* you can configure the following options:
  - **Allow list** - Use *Add*, *Import*, and *Export* to manage a list of device identifiers.

- **Block hardware device installation by device instance identifiers**  
  If you enable this policy setting on a remote desktop server, the policy setting affects redirection of the specified devices from a remote desktop client to the remote desktop server.
  - **Not configured** *(default)*
  - **Yes** - Specify a list of Plug and Play hardware IDs and compatible IDs for devices that Windows is prevented from installing. This policy takes precedence over any other policy setting that allows Windows to install a device. If you enable this policy setting on a remote desktop server, the policy setting affects redirection of the specified devices from a remote desktop client to the remote desktop server.
  - **No**

  When set to *Yes* you can configure the following options:  
  - **Remove matching hardware devices**  
    - **Yes**
    - **Not configured** *(default)*

  - **Block list** - Use *Add*, *Import*, and *Export* to manage a list of device identifiers.

- **Block write access to removable storage**  
  CSP: [RemovableDiskDenyWriteAccess](/windows/client-management/mdm/policy-csp-storage#storage-removablediskdenywriteaccess)

  - **Not configured** *(default)*
  - **Yes** - Write access is denied to removable storage.
  - **No** - Write access is allowed.

- **Scan removable drives during full scan**  
  CSP: [Defender/AllowFullScanRemovableDriveScanning](/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanremovabledrivescanning)

  - **Not configured** (*default*) - The setting returns to client default, which scans removable drives, however the user can disable this scan.
  - **Yes** - During a full scan, removable drives (like USB flash drives) are scanned.

- **Block direct memory access**  
  CSP: [DataProtection/AllowDirectMemoryAccess](/windows/client-management/mdm/policy-csp-dataprotection#dataprotection-allowdirectmemoryaccess)

  This policy setting is only enforced when BitLocker or device encryption is enabled.

  - **Not configured** (*default*)
  - **Yes** - block direct memory access (DMA) for all hot pluggable PCI downstream ports until a user logs into Windows. After a user logs in, Windows enumerates the PCI devices connected to the host plug PCI ports. Every time the user locks the machine, DMA is blocked on hot plug PCI ports with no children devices until the user logs in again. Devices that were already enumerated when the machine was unlocked will continue to function until unplugged.

- **Enumeration of external devices incompatible with Kernel DMA Protection**  
  CSP: [DmaGuard/DeviceEnumerationPolicy](/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy)

  This policy can provide additional security against external DMA capable devices. It allows for more control over the enumeration of external DMA capable devices incompatible with DMA Remapping/device memory isolation and sandboxing.

  This policy only takes effect when Kernel DMA Protection is supported and enabled by the system firmware. Kernel DMA Protection is a platform feature that must be supported by the system at the time of manufacturing. To check if the system supports Kernel DMA Protection, check the Kernel DMA Protection field in the Summary page of MSINFO32.exe.

  - **Not configured** - (*default*)
  - **Block all**
  - **Allow all**

- **Block bluetooth connections**  
  CSP: [Bluetooth/AllowDiscoverableMode](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

  - **Not configured** (*default*)
  - **Yes** - Block bluetooth connections to and from the device.

- **Block bluetooth discoverability**  
  CSP: [Bluetooth/AllowDiscoverableMode](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowdiscoverablemode)

  - **Not configured** (*default*)
  - **Yes** - Prevents the device from being discoverable by other Bluetooth-enabled devices.

- **Block bluetooth pre-pairing**  
  CSP: [Bluetooth/AllowPrepairing](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowprepairing)

  - **Not configured** (*default*)
  - **Yes** - Prevents specific Bluetooth devices from automatically pairing with the host device.

- **Block bluetooth advertising**  
  CSP: [Bluetooth/AllowAdvertising](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowadvertising)

  - **Not configured** (*default*)
  - **Yes** - Prevents the device from sending out Bluetooth advertisements.  

- **Block bluetooth proximal connections**  
  CSP: [Bluetooth/AllowPromptedProximalConnections](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowpromptedproximalconnections)
  Block users from using Swift Pair and other proximity-based scenarios

  - **Not configured** (*default*)
  - **Yes** - Prevents a device user from using Swift Pair and other proximity-based scenarios.  

  [Bluetooth/AllowPromptedProximalConnections CSP](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-allowpromptedproximalconnections)

- **Bluetooth allowed services**  
  CSP: [Bluetooth/ServicesAllowedList](/windows/client-management/mdm/policy-csp-bluetooth#bluetooth-servicesallowedlist).  
  For more information on the service list, see [ServicesAllowedList usage guide](/windows/client-management/mdm/policy-csp-bluetooth#servicesallowedlist-usage-guide)

  - **Add** - Specify allowed Bluetooth services and profiles as hex strings, such as `{782AFCFC-7CAA-436C-8BF0-78CD0FFBD4AF}`.
  - **Import** - Import a .csv file that contains a list of bluetooth services and profiles, as hex strings, such as `{782AFCFC-7CAA-436C-8BF0-78CD0FFBD4AF}`

- **Removable storage**  
  CSP: [Storage/RemovableDiskDenyWriteAccess](/windows/client-management/mdm/policy-csp-storage#storage-removablediskdenywriteaccess) 

  - **Block** (*default*) - Prevent users from using external storage devices, like SD cards with the device.
  - **Not configured**

- **USB connections (HoloLens only)**  
  CSP: [Connectivity/AllowUSBConnection](/windows/client-management/mdm/policy-csp-connectivity#connectivity-allowusbconnection)

  - **Block** - Prevent use of a USB connection between the device and a computer to sync files, or to use developer tools to deploy or debug applications. USB charging isn't affected.
  - **Not configured** (*default*)

### Exploit protection profile

#### Exploit protection

  > [!NOTE]  
  > This  section details the settings you can find in Exploit protection profiles created before April 5, 2022. Profiles created after that date use a new settings format as found in the Settings Catalog. Although you can no longer create new instances of the original profile, you can continue to edit and use your existing profiles.

- **Upload XML**  
  CSP: [ExploitProtectionSettings](/windows/client-management/mdm/policy-csp-exploitguard#exploitguard-exploitprotectionsettings)

  Enables the IT admin to push out a configuration representing the desired system and application mitigation options to all the devices in the organization. The configuration is represented by an XML file. Exploit protection can help protect devices from malware that use exploits to spread and infect. You use the Windows Security app or PowerShell to create a set of mitigations (known as a configuration). You can then export this configuration as an XML file and share it with multiple machines on your network so they all have the same set of mitigation settings. You can also convert and import an existing EMET configuration XML file into an exploit protection configuration XML.

  Choose **Select XML File**, specify the XML filet upload, and then click **Select**.
  - **Not configured** (*default*)
  - **Yes**

- **Block users from editing the Exploit Guard protection interface**  
  CSP: [DisallowExploitProtectionOverride](/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-disallowexploitprotectionoverride)

  - **Not configured** (*default*) - Local users can make changes in the exploit protection settings area.
  - **Yes** - Prevent users from making changes to the exploit protection settings area in the Microsoft Defender Security Center.

### Web protection (Microsoft Edge Legacy) profile

#### Web Protection (Microsoft Edge Legacy)

- **Enable network protection**  
  CSP: [EnableNetworkProtection](/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

  - **Not configured** (*default*) - The setting returns to the Windows default, which is disabled.
  - **User defined**
  - **Enable** - Network protection is enabled for all users on the system.
  - **Audit mode** - Users aren't blocked from dangerous domains and Windows events are raised instead.

- **Require SmartScreen for Microsoft Edge**  
  CSP: [Browser/AllowSmartScreen](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

  - **Yes** - Use SmartScreen to protect users from potential phishing scams and malicious software.
  - **Not configured** (*default*)

- **Block malicious site access**  
  CSP: [Browser/PreventSmartScreenPromptOverride](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)  

  - **Yes** - Block users from ignoring the Microsoft Defender SmartScreen Filter warnings and block them from going to the site.
  - **Not configured** (*default*)

- **Block unverified file download**  
  CSP: [Browser/PreventSmartScreenPromptOverrideForFiles](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)  

  - **Yes** - Block users from ignoring the Microsoft Defender SmartScreen Filter warnings and block them from downloading unverified files.
  - **Not configured** (*default*)

## Attack surface reduction (ConfigMgr)

### Exploit Protection (ConfigMgr)(Preview) profile

#### Exploit Protection

- **Upload XML**  
  CSP: [ExploitProtectionSettings](/windows/client-management/mdm/policy-csp-exploitguard#exploitguard-exploitprotectionsettings)

  Enables the IT admin to push out a configuration representing the desired system and application mitigation options to all the devices in the organization. The configuration is represented by an XML file. Exploit protection can help protect devices from malware that use exploits to spread and infect. You use the Windows Security app or PowerShell to create a set of mitigations (known as a configuration). You can then export this configuration as an XML file and share it with multiple machines on your network so they all have the same set of mitigation settings. You can also convert and import an existing EMET configuration XML file into an exploit protection configuration XML.

  Choose **Select XML File**, specify the XML filet upload, and then click **Select**.

- **Disallow Exploit Protection Override**  
  CSP: [DisallowExploitProtectionOverride](/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-disallowexploitprotectionoverride)

  - **Not configured** (default)
  - **(Disable) Local users are allowed to make changes in the exploit protection settings area**.
  - **(Enable) Local users cannot make changes to the exploit protection settings area**

### Web Protection (ConfigMgr)(Preview) profile

#### Web Protection

- **Enable Network Protection (Device)**  
  CSP: [EnableNetworkProtection](/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

  - **Not configured** (*default*)
  - **Disabled**
  - **Enabled (block mode)**
  - **Enabled (audit mode)**

- **Allow Smart Screen (Device)**  
  CSP: [Browser/AllowSmartScreen](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

  - **Not configured** (*default*)
  - **Block**
  - **Allow**

- **Prevent Smart Screen Prompt Override For Files (Device)**  
  CSP: [Browser/PreventSmartScreenPromptOverride](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)  

  - **Not configured** (*default*)
  - **Disabled**
  - **Enabled**

- **Prevent Smart Screen Prompt Override (Device)**  
  CSP: [Browser/PreventSmartScreenPromptOverrideForFiles](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)  

  - **Not configured** (*default*)
  - **Disabled**
  - **Enabled**

## Next steps

[Endpoint security policy for ASR](../protect/endpoint-security-asr-policy.md)
