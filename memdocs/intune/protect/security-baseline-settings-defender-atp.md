---
# required metadata

title: Settings list for the Microsoft Defender for Endpoint security baseline in Microsoft Intune  
titleSuffix: Microsoft Intune
description: View a list of the settings in the Microsoft Intune security baseline for Microsoft Defender for Endpoint. This list includes the default values for settings as found in the default configuration of the baseline.
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/03/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology:
ms.assetid:

# optional metadata

#ROBOTS:

#audience:

ms.reviewer: laarrizz
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
zone_pivot_groups: atp-baseline-versions
---

<!-- Pivots in use: 

December 2020 v6
::: zone pivot="atp-december-2020"
::: zone-end

September 2020 v5
::: zone pivot="atp-sept-2020"
::: zone-end

April 2020 v4
::: zone pivot="atp-april-2020"
::: zone-end

March 2020 v3
::: zone pivot="atp-march-2020"
::: zone-end

-->

# Settings in the Microsoft Defender for Endpoint security baseline in Intune

View the settings that are part of the Microsoft Defender for Endpoint baseline that ou can deploy with Microsoft Intune. This article details the settings in the available versions of the baseline and the default values for each setting. The default baseline configuration represents the recommended configuration for applicable devices. Defaults for one baseline might not match defaults from other security baselines, or from other versions of this baseline.

::: zone pivot="atp-december-2020"

**Microsoft Defender for Endpoint baseline for December 2020 - version 6**  

::: zone-end
::: zone pivot="atp-sept-2020"

**Microsoft Defender for Endpoint baseline for September 2020 - version 5**  

::: zone-end
::: zone pivot="atp-april-2020"

**Microsoft Defender for Endpoint baseline for April 2020 - version 4**  

::: zone-end
::: zone pivot="atp-april-2020,atp-sept-2020,atp-december-2020"
This version of the security baseline replaces previous versions. Profiles that were created prior to the availability of this baseline version:

- Are now read-only. You can continue to use those profiles, but can't edit them to change their configuration.
- Can be updated to the latest version. After you update to the current baseline version, you can edit the profile to modify settings.

To understand what's changed with this version of the baseline from previous versions, use the [Compare baselines](../protect/security-baselines.md#compare-baseline-versions) action. This action is available when you view the *Versions* pane for this baseline. Be sure to select the version of the baseline that you want to view.

To update a security baseline profile to the latest version of that baseline, see [Change the baseline version for a profile](../protect/security-baselines-configure.md#change-the-baseline-version-for-a-profile).

::: zone-end
::: zone pivot="atp-march-2020"

**Microsoft Defender for Endpoint baseline for March 2020 - version 3**  
This version of the security baseline replaces previous versions. Profiles that were created prior to the availability of this baseline version:

- Are now read-only. You can continue to use those profiles, but can't edit them to change their configuration.
- Can be updated to the latest version. After you update the current baseline version, you can edit the profile to modify settings.

To understand what's changed with this version of the baseline from previous versions, use the [Compare baselines](../protect/security-baselines.md#compare-baseline-versions) action. This action is available when you view the *Versions* pane for this baseline. Be sure to select the version of the baseline that you want to view.

To update a security baseline profile to the latest version of that baseline, see [Change the baseline version for a profile](../protect/security-baselines-configure.md#change-the-baseline-version-for-a-profile).

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020,atp-december-2020"

The Microsoft Defender for Endpoint  baseline is available when your environment meets the prerequisites for using [Microsoft Defender for Endpoint](advanced-threat-protection.md#prerequisites).

This baseline is optimized for physical devices and isn't recommended for use on virtual machines (VMs) or VDI endpoints. Certain baseline settings can impact remote interactive sessions on virtualized environments. For more information, see [Increase compliance to the Microsoft Defender for Endpoint security baseline](/windows/security/threat-protection/microsoft-defender-atp/configure-machines-security-baseline) in the Windows documentation.

::: zone-end
::: zone pivot="atp-sept-2020,atp-december-2020"

## Attack Surface Reduction Rules

To learn more, see [Attack surface reduction rules](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction) in the Microsoft Defender for Endpoint documentation.

**Merge behavior for Attack surface reduction rules in Intune**:

  Attack surface reduction rules support a merger of settings from different policies, to create a superset of policy for each device. Only the settings that are not in conflict are merged, while those that are in conflict are not added to the superset of rules. Previously, if two policies included conflicts for a single setting, both policies were flagged as being in conflict, and no settings from either profile would be deployed.

  Attack surface reduction rule merge behavior is as follows:
  - Attack surface reduction rules from the following profiles are evaluated for each device the rules apply to:  
    - Devices > Configuration policy > Endpoint protection profile > Microsoft Defender Exploit Guard > **Attack Surface Reduction**
    - Endpoint security > Attack surface reduction policy > **Attack surface reduction rules**
    - Endpoint security > Security baselines > Microsoft Defender for Endpoint Baseline > **Attack Surface Reduction Rules**.
  - Settings that do not have conflicts are added to a superset of policy for the device.
  - When two or more policies have conflicting settings, the conflicting settings are not added to the combined policy, while settings that don’t conflict are added to the superset policy that applies to a device.
  - Only the configurations for conflicting settings are held back.

**Settings in this profile**:


- **Block Office communication apps from creating child processes**  
  ASR rule: [26190899-1602-49e8-8b27-eb1d0a1ce869](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  - **Enable** *(default)* - Office communication applications are blocked from creating child processes.
  - **Not configured** - Return the setting to Windows default, which is off.
  - **User defined**
  - **Audit mode** - Windows events are raised instead of blocking.

- **Block Adobe Reader from creating child processes**  
  ASR rule: [7674ba52-37eb-4a4f-a9a1-f0f9a1619a2c](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  - **Enable** *(default)* - Adobe Reader is blocked from creating child processes.
  - **Not configured** - Return the setting to Windows default, which is off.
  - **User defined**
  - **Audit mode** - Windows events are raised instead of blocking.

- **Block Office applications from injecting code into other processes**  
  ASR rule: [75668C1F-73B5-4CF0-BB93-3ECF5CB7CC84](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  - **Block** *(default)* - Office applications are blocked from injecting code into other processes.
  - **Not configured** - Return the setting to Windows default, which is off.
  - **Audit mode** - Windows events are raised instead of blocking.

- **Block Office applications from creating executable content**  
  ASR rule: [3B576869-A4EC-4529-8536-B80A7769E899](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  - **Block** *(default)* - Office applications aren't allowed to create executable content.
  - **Not configured** - Return the setting to Windows default, which is off.
  - **Audit mode** - Windows events are raised instead of blocking.

- **Block JavaScript or VBScript from launching downloaded executable content**  
  ASR rule: [D3E037E1-3EB8-44C8-A917-57927947596D](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  - **Block** *(default)*
  - **Not configured** - Return the setting to Windows default, which is off.
  - **Audit mode** - Windows events are raised instead of blocking.

- **Enable network protection**  
  CSP: [Defender/EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=3D872618)

  - **Enable** *(default)*
  - **Not configured** - Return the setting to Windows default, which is off.
  - **User defined**
  - **Audit mode** - Windows events are raised instead of blocking.

- **Block untrusted and unsigned processes that run from USB**  
  ASR rule: [b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4](https://go.microsoft.com/fwlink/?linkid=)

  - **Block** *(default)* - Untrusted/unsigned processes executing from a USB drive are blocked.
  - **Not configured** - Return the setting to Windows default, which is off.
  - **Audit mode** - Windows events are raised instead of blocking.

- **Block credential stealing from the Windows local security authority subsystem (lsass.exe)**  
  ASR rule: [9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  - **Enable** *(default)* - Attempts to steal credentials via lsass.exe are blocked.
  - **Not configured** - Return the setting to Windows default, which is off.
  - **User defined**
  - **Audit mode** - Windows events are raised instead of blocking.

- **Block executable content download from email and webmail clients**  
  ASR rule: [BE9BA2D9-53EA-4CDC-84E5-9B1EEEE46550](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  - **Block** *(default)* - Executable content downloaded from email and webmail clients is blocked. 
  - **Not configured** - Return the setting to Windows default, which is off.
  - **Audit mode** - Windows events are raised instead of blocking.

- **Block all Office applications from creating child processes**  
  ASR rule: [D4F940AB-401B-4EFC-AADC-AD5F3C50688A](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  - **Block** *(default)* - Office apps are blocked from creating child processes. Blocked apps include Word, Excel, PowerPoint, OneNote, and Access.
  - **Not configured** - Return the setting to Windows default, which is off.
  - **Audit mode** - Windows events are raised instead of blocking.

- **Block execution of potentially obfuscated scripts (js/vbs/ps)**  
  ASR rule: [5BEB7EFE-FD9A-4556-801D-275E5FFC04CC](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  - **Block** *(default)* - Defender blocks execution of obfuscated scripts.
  - **Not configured** - Return the setting to Windows default, which is off.
  - **Audit mode** - Windows events are raised instead of blocking.

- **Block Win32 API calls from Office macro**  
  ASR rule: [92E97FA1-2EDF-4476-BDD6-9DD0B4DDDC7B](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  - **Block** *(default)* - Office macro's are blocked from using Win32 API calls.
  - **Not configured** - Return the setting to Windows default, which is off.
  - **Audit mode** - Windows events are raised instead of blocking.

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

## Application Guard

For more information, see [WindowsDefenderApplicationGuard CSP](/windows/client-management/mdm/windowsdefenderapplicationguard-csp) in the Windows documentation.  

When you use Microsoft Edge, Microsoft Defender Application Guard protects your environment from sites that aren't trusted by your organization. When users visit sites that aren't listed in your isolated network boundary, the sites open in a Hyper-V virtual browsing session. Trusted sites are defined by a network boundary.  

- **Turn on Application Guard for Edge (Options)**  
  CSP: [Settings/AllowWindowsDefenderApplicationGuard](/windows/client-management/mdm/windowsdefenderapplicationguard-csp#allowwindowsdefenderapplicationguard)
  
  - **Enabled for Edge** (*default*) - Application Guard opens unapproved sites in a Hyper-V virtualized browsing container.
  - **Not configured** - Any site (trusted and untrusted) opens on the device, and not in a virtualized container.  
  
  When set to *Enable for Edge*, you can configure *Block external content from non-enterprise approved sites* and *Clipboard behavior*.

  - **Block external content from non-enterprise approved sites**  
    CSP: [Settings/BlockNonEnterpriseContent](/windows/client-management/mdm/windowsdefenderapplicationguard-csp#blocknonenterprisecontent)

    - **Yes** (*default*) - Block content from unapproved websites from loading.
    - **Not configured** - Non-enterprise sites can open on the device

  - **Clipboard behavior**  
    CSP: [Settings/ClipboardSettings](/windows/client-management/mdm/windowsdefenderapplicationguard-csp#clipboardsettings)

    Choose what copy and paste actions are allowed between the local PC and the Application Guard virtual browser. Options include:
    - **Not Configured**  
    - **Block copy and paste between PC and browser** (*default*) - Block both. Data can't transfer between the PC and the virtual browser.
    - **Allow copy and paste from browser to PC only** - Data can't transfer from the PC into the virtual browser.
    - **Allow copy and paste from PC to browser only** - Data can't transfer from the virtual browser to the host PC.
    - **Allow copy and paste between PC and browser** - No block for content exists.

- **Windows network isolation policy**  
  CSP: [Policy CSP - NetworkIsolation](/windows/client-management/mdm/policy-csp-networkisolation)

  Specify a list of *Network domains*, which are Enterprise resources that are hosted in the cloud that Application Guard treats as enterprise sites
  - **Configure** (*default*)
  - **Not configured**

  When set to *Configure* you can then define *Network domains*.

  - **Network domains**  
    Select **Add** and specify domains, IP address ranges, and network boundaries. By default, *securitycenter.windows.com* is configured.

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020,atp-december-2020"

## BitLocker

For more information, [BitLocker Group Policy settings](/windows/security/information-protection/bitlocker/bitlocker-group-policy-settings) in the Windows documentation.

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

- **Require storage cards to be encrypted (mobile only)**  
  CSP: [RequireStorageCardEncryption](/windows/client-management/mdm/bitlocker-csp#requirestoragecardencryption)

  This setting only applies to Windows Mobile and Mobile Enterprise SKU devices.
  - **Yes** (*default*) - Encryption on storage cards is required for mobile devices.
  - **Not configured** - The setting returns to the OS default, which is to not require storage card encryption.

  > [!NOTE]
  > Support for [Windows 10 Mobile](https://support.microsoft.com/help/4485197/windows-10-mobile-end-of-support-faq) and [Windows Phone 8.1](https://support.microsoft.com/help/4036480/windows-phone-8-1-end-of-support-faq) ended in August of 2020.

::: zone-end
::: zone pivot="atp-sept-2020,atp-december-2020"

- **Standby states when sleeping while on battery**
  CSP: [Power/StandbyTimeoutOnBattery](/windows/client-management/mdm/policy-csp-power#power-standbytimeoutonbattery)

  This policy setting manages whether or not Windows can use standby states when putting the computer in a sleep state.
  - **Disabled** *(default)* - Standby states (S1-S3) aren't allowed.
  - **Enabled** - Windows uses standby states to put the computer in a sleep state.
  - **Not configured** - Same behavior as *Enabled*.

- **Standby states when sleeping while plugged in**  
  CSP: [Power/StandbyTimeoutPluggedIn](/windows/client-management/mdm/policy-csp-power#power-standbytimeoutpluggedin)

  This policy setting manages if Windows can use standby states when putting the computer in a sleep state.
  - **Disabled** *(default)* - Standby states (S1-S3) aren't allowed.
  - **Enabled** - Windows uses standby states to put the computer in a sleep state.
  - **Not configured** - Same behavior as *Enabled*.

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020,atp-december-2020"

- **Enable full disk encryption for OS and fixed data drives**  
  CSP: [RequireDeviceEncryption](/windows/client-management/mdm/bitlocker-csp#requiredeviceencryption)

  If the drive was encrypted before this policy applied, no extra action is taken. If the encryption method and options match that of this policy, configuration should return success. If an in-place BitLocker configuration option doesn't match this policy, configuration will likely return an error.
  
  To apply this policy to a disk already encrypted, decrypt the drive and reapply the MDM policy. Windows default is to not require BitLocker drive encryption, however on Azure AD Join and Microsoft Account (MSA) registration/login automatic encryption may apply enabling BitLocker at XTS-AES 128-bit encryption.

  - **Yes** (*default*) - Enforce use of BitLocker.
  - **Not configured** - No BitLocker enforcement takes place.

- **BitLocker system drive policy**  
  [BitLocker Group Policy settings](/windows/security/information-protection/bitlocker/bitlocker-group-policy-settings)

  - **Configure** (*default*)
  - **Not configured**

  When set to *Configure*, you can then configure the following settings:

::: zone-end
::: zone pivot="atp-sept-2020,atp-december-2020"

- **Startup authentication required**  
  CSP: [SystemDrivesRequireStartupAuthentication](/windows/client-management/mdm/bitlocker-csp#systemdrivesrequirestartupauthentication)

  - **Yes** *(default)* - You can configure the additional authentication requirements at system startup, including utilizing the use of Trusted Platform Module (TPM) or startup PIN requirements:
  - **Not configured**

    - **Compatible TPM startup PIN**  
      CSP: [SystemDrivesRequireStartupAuthentication](/windows/client-management/mdm/bitlocker-csp#systemdrivesrequirestartupauthentication)
      This setting is available when *Startup authentication required* is set to *Yes*.

      - **Blocked** - Block the use of a PIN. 
      - **Required** - Require BitLocker have a PIN and TPM present to return success. For silent enable scenarios (including Autopilot) this setting can't be successful, as user interaction is required. It's recommended that PIN is disabled where silent enablement of BitLocker is required.
      - **Allowed** *(default)* - Enable BitLocker using the TPM if present, and allow a startup PIN be configured by the user.
      - **Not configured**

    - **Compatible TPM startup key**  
      CSP: [SystemDrivesRequireStartupAuthentication](/windows/client-management/mdm/bitlocker-csp#systemdrivesrequirestartupauthentication)
      This setting is available when *Startup authentication required* is set to *Yes*.

      - **Blocked** - Block the use of startup keys.
      - **Required** *(default)* - Require BitLocker have a startup key and TPM present to enable BitLocker. For silent enable scenarios (including Autopilot) this setting can't be successful, as user interaction is required. It's recommended that startup keys be disabled where silent enablement of BitLocker is required.
      - **Allowed** - Enable BitLocker using the TPM if present, and allow a startup key (such as a USB drive) be present to unlock the drives.
      - **Not configured**

    - **Disable BitLocker on devices where TPM is incompatible**  
      CSP: [SystemDrivesRequireStartupAuthentication](/windows/client-management/mdm/bitlocker-csp#systemdrivesrequirestartupauthentication)
      This setting is available when *Startup authentication required* is set to *Yes*.

      - **Yes** *(default)* - Disable BitLocker from being configured without a compatible TPM chip. This setting may be helpful for testing, but it isn't suggested to enable BitLocker without a TPM. If no TPM is present, BitLocker will require a password or USB drive for startup. This setting only applies when first enabling BitLocker. If BitLocker is already enabled before applying this setting, it will have no effect.
      - **Not configured**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020,atp-december-2020"

  - **Configure encryption method for Operating System drives**  
    CSP: [EncryptionMethodByDriveType](/windows/client-management/mdm/bitlocker-csp#encryptionmethodbydrivetype)  
    This setting is available when *BitLocker system drive policy* is set to *Configure*.  

    Configure the encryption method and cipher strength for system drives.  

    - **Not configured** (*default*)
    - **AES 128bit CBC**
    - **AES 256bit CBC**
    - **AES 128bit XTS**
    - **AES 256bit XTS**

- **BitLocker fixed drive policy**  
  [BitLocker Group Policy settings](/windows/security/information-protection/bitlocker/bitlocker-group-policy-settings)

  - **Configure** (*default*)
  - **Not configured**

  When set to *Configure*, you can then configure *Block write access to fixed data-drives not protected by BitLocker* and *Configure encryption method for fixed data-drives*.

  - **Block write access to fixed data-drives not protected by BitLocker**  
    CSP: [FixedDrivesRequireEncryption](/windows/client-management/mdm/bitlocker-csp#fixeddrivesrequireencryption)  
    This setting is available when *BitLocker fixed drive policy* is set to *Configure*.

    - **Not configured** - Data can be written to non-encrypted fixed drives.
    - **Yes** (*default*) - Windows won't allow any data to be written to fixed drives that aren't BitLocker protected. If a fixed drive isn't encrypted, the user will need to complete the BitLocker setup wizard for the drive before write access is granted.

  - **Configure encryption method for fixed data-drives**  
    CSP: [EncryptionMethodByDriveType](/windows/client-management/mdm/bitlocker-csp#encryptionmethodbydrivetype)  
    This setting is available when *BitLocker fixed drive policy* is set to *Configure*.

    Configure the encryption method and cipher strength for fixed data-drives disks. *XTS- AES 128-bit* is the Windows default encryption method and the recommended value.

    - **Not configured**
    - **AES 128bit CBC**
    - **AES 256bit CBC**
    - **AES 128bit XTS** (*default*)
    - **AES 256bit XTS**

- **BitLocker removable drive policy**  
  [BitLocker Group Policy settings](/windows/security/information-protection/bitlocker/bitlocker-group-policy-settings)

  - **Configure** (*default*)
  - **Not configured**

  When set to *Configure*, you can then configure *Configure encryption method for removable data-drives* and *Block write access to removable data-drives not protected by BitLocker*.

  - **Configure encryption method for removable data-drives**  
    CSP: [EncryptionMethodByDriveType](/windows/client-management/mdm/bitlocker-csp#encryptionmethodbydrivetype)  
    This setting is available when *BitLocker removable drive policy* is set to *Configure*.

    Configure the encryption method and cipher strength for removable data-drives disks.

    - **Not configured**
    - **AES 128bit CBC** (*default*)
    - **AES 256bit CBC**
    - **AES 128bit XTS**
    - **AES 256bit XTS**

  - **Block write access to removable data-drives not protected by BitLocker**  
    CSP: [RemovableDrivesRequireEncryption](/windows/client-management/mdm/bitlocker-csp#removabledrivesrequireencryption)  
    This setting is available when *BitLocker removable drive policy* is set to *Configure*.

    - **Not configured** (*default*) - Data can be written to non-encrypted removable drives.  
    - **Yes** - Windows won't allow any data to be written to removable drives that are not BitLocker protected. If a removable drive isn't encrypted, the user must complete the BitLocker setup wizard for the drive before write access is granted.

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

## Browser

- **Require SmartScreen for Microsoft Edge**  
  CSP: [Browser/AllowSmartScreen](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

  - **Yes** (*default*) - Use SmartScreen to protect users from potential phishing scams and malicious software.
  - **Not configured**

- **Block malicious site access**  
  CSP: [Browser/PreventSmartScreenPromptOverride](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)  

  - **Yes** (*default*) - Block users from ignoring the Microsoft Defender SmartScreen Filter warnings and block them from going to the site.
  - **Not configured**

- **Block unverified file download**  
  CSP: [Browser/PreventSmartScreenPromptOverrideForFiles](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)  

  - **Yes** (*default*) - Block users from ignoring the Microsoft Defender SmartScreen Filter warnings and block them from downloading unverified files.
  - **Not configured**

## Data Protection

- **Block direct memory access**  
  CSP: [DataProtection/AllowDirectMemoryAccess](/windows/client-management/mdm/policy-csp-dataprotection#dataprotection-allowdirectmemoryaccess)  

  This policy setting is only enforced when BitLocker or device encryption is enabled.

  - **Yes** (*default*) - Block direct memory access (DMA) for all hot pluggable PCI downstream ports until a user logs into Windows. After a user logs in, Windows enumerates the PCI devices connected to the host plug PCI ports. Every time the user locks the machine, DMA is blocked on hot plug PCI ports with no children devices until the user logs in again. Devices that were already enumerated when the machine was unlocked will continue to function until unplugged.
  - **Not configured**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020,atp-december-2020"

## Device Guard  

- **Turn on credential guard**  
  CSP: [DeviceGuard/ConfigureSystemGuardLaunch](/windows/client-management/mdm/policy-csp-deviceguard)

  Credential Guard uses Windows Hypervisor to provide protections, which requires Secure Boot and DMA protections to function, which requires that hardware requirements are met.

  - **Not configured**
  - **Enable with UEFI lock** (*default*) - Enable Credential Guard and not allow it to be disabled remotely, as the UEFI persisted configuration must be manually cleared.
  - **Enable without UEFI lock** - Enable Credential Guard and allow it to be turned off without physical access to the machine.
  - **Disable** - Disable the use of Credential Guard, which is the Windows default.

## Device Installation

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

- **Hardware device installation by device identifiers**  
  [DeviceInstallation/PreventInstallationOfMatchingDeviceIDs](/windows/client-management/mdm/policy-csp-deviceinstallation#deviceinstallation-allowinstallationofmatchingdeviceids)

  This policy setting allows you to specify a list of Plug and Play hardware IDs and compatible IDs for devices that Windows is prevented from installing. This policy setting takes precedence over any other policy setting that allows Windows to install a device.  If you enable this policy setting on a remote desktop server, the policy setting affects redirection of the specified devices from a remote desktop client to the remote desktop server.

  - **Not configured**
  - **Allow hardware device installation** - Devices can be installed and updated as allowed or prevented by other policy settings.
  - **Block hardware device installation** (*default*) - Windows is prevented from installing a device whose hardware ID or compatible ID appears in a list you define.

  When set to *Block hardware device installation* you can configure *Remove matching hardware devices* and *Hardware device identifiers that are blocked*.

  - **Remove matching hardware devices**

    This setting is available only when *Hardware device installation by device identifiers* is set to *Block hardware device installation*.
    - **Yes** *(default)*
    - **Not configured**

  - **Hardware device identifiers that are blocked**  

    This setting is available only when *Hardware device installation by device identifiers* is set to *Block hardware device installation*.

    Select **Add**, and then specify the hardware device identifier you want to block.

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020"

- **Hardware device installation by setup classes**  
  CSP: [DeviceInstallation/AllowInstallationOfMatchingDeviceSetupClasses](/windows/client-management/mdm/policy-csp-deviceinstallation#deviceinstallation-allowinstallationofmatchingdevicesetupclasses)  
  
  This policy setting allows you to specify a list of device setup class globally unique identifiers (GUIDs) for device drivers that Windows is prevented from installing. This policy setting takes precedence over any other policy setting that allows Windows to install a device. If you enable this policy setting on a remote desktop server, the policy setting affects redirection of the specified devices from a remote desktop client to the remote desktop server.

  - **Not configured**
  - **Allow hardware device installation** - Windows can install and update devices as allowed or prevented by other policy settings.
  - **Block hardware device installation** (*default*) - Windows is prevented from installing a device whose setup class GUIDs appear in a list you define.

  When set to *Block hardware device installation* you can configure *Remove matching hardware devices* and *Hardware device identifiers that are blocked*.

  - **Remove matching hardware devices**

    This setting is available only when *Hardware device installation by device identifiers* is set to *Block hardware device installation*.
    - **Yes**
    - **Not configured** *(default)*

  - **Hardware device identifiers that are blocked**

    This setting is available only when *Hardware device installation by device identifiers* is set to *Block hardware device installation*.

    Select **Add**, and then specify the hardware device identifier you want to block.

::: zone-end
::: zone pivot="atp-december-2020"

- **Block hardware device installation by setup classes**:  
  This policy setting allows you to specify a list of device setup class globally unique identifiers (GUIDs) for device drivers that Windows is prevented from installing. This policy setting takes precedence over any other policy setting that allows Windows to install a device. If you block installation, Windows is prevented from installing or updating device drivers whose device setup class GUIDs appear in the list you create. If you enable this policy setting on a remote desktop server, the policy setting affects redirection of the specified devices from a remote desktop client to the remote desktop server. If you allow installation, Windows can install and update devices as allowed or prevented by other policy settings.  
  [Learn more](/windows/client-management/mdm/policy-csp-deviceinstallation#deviceinstallation-allowinstallationofmatchingdevicesetupclassess)

  **Default**: Yes
  
  When *Yes* is selected, the following settings are available.

  - **Remove matching hardware devices**:  
    This setting is available only when *Block hardware device installation by setup classes* is set to *Yes*.

    **Default**: Yes

  - **Block list**
    Manage a list of device setup class globally unique identifiers that for device drivers that Windows is prevented from installing. 

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020,atp-december-2020"
## DMA Guard

- **Enumeration of external devices incompatible with Kernel DMA Protection**  
  CSP: [DmaGuard/DeviceEnumerationPolicy](/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy)

  This policy can provide additional security against external DMA capable devices. It allows for more control over the enumeration of external DMA capable devices incompatible with DMA Remapping/device memory isolation and sandboxing.

  This policy only takes effect when Kernel DMA Protection is supported and enabled by the system firmware. Kernel DMA Protection is a platform feature that must be supported by the system at the time of manufacturing. To check if the system supports Kernel DMA Protection, check the Kernel DMA Protection field in the Summary page of MSINFO32.exe.

::: zone-end
::: zone pivot="atp-sept-2020,atp-december-2020"

  - **Not configured**  
  - **Block all** *(default)*
  - **Allow all**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

  - **Not configured** - (*default*)
  - **Block all**
  - **Allow all**

## Endpoint Detection and Response

For more information about the following settings, see [WindowsAdvancedThreatProtection](/windows/client-management/mdm/windowsadvancedthreatprotection-csp) CSP in the Windows documentation.

- **Sample sharing for all files**  
  CSP: [Configuration/SampleSharing](/windows/client-management/mdm/windowsadvancedthreatprotection-csp)

  Returns or sets the Microsoft Defender for Endpoint Sample Sharing configuration parameter.
  
  - **Yes** (*default*)
  - **Not configured**

- **Expedite telemetry reporting frequency**  
  CSP: [Configuration/TelemetryReportingFrequency](/windows/client-management/mdm/windowsadvancedthreatprotection-csp)

  Expedite Microsoft Defender for Endpoint telemetry reporting frequency.  

  - **Yes** (*default*)
  - **Not configured**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020,atp-december-2020"

## Firewall

For more information, see [Firewall CSP](/windows/client-management/mdm/firewall-csp) in the Windows documentation.

- **Stateful File Transfer Protocol (FTP)**  
  CSP: [MdmStore/Global/DisableStatefulFtp](/windows/client-management/mdm/firewall-csp#disablestatefulftp)  

  - **Disabled** (*default*) - Stateful FTP is disabled.
  - **Allow** - The firewall performs stateful File Transfer Protocol (FTP) filtering to allow secondary connections. Disabled
  - **Not configured**

- **Number of seconds a security association can be idle before it's deleted**  
  CSP: [MdmStore/Global/SaIdleTime](/windows/client-management/mdm/firewall-csp#saidletime)

  Specify how long the security associations are kept after network traffic is no longer seen. When not configured, the system deletes a security association after it's been idle for *300* seconds (the default).
  
  The number must be from **300** to **3600** seconds.

- **Preshared key encoding**  
  CSP: [MdmStore/Global/PresharedKeyEncoding](/windows/client-management/mdm/firewall-csp#presharedkeyencoding)

   If you don't require UTF-8, preshared keys will initially be encoded using UTF-8. After that, device users can choose another encoding method.

  - **Not configured**
  - **None**
  - **UTF8** (*default*)

- **Certificate revocation list (CRL) verification**  
  CSP: [MdmStore/Global/CRLcheck](/windows/client-management/mdm/firewall-csp#crlcheck)

  Specify how certificate revocation list (CRL) verification is enforced.  

  - **Not configured** (*default*) - CRL verification is disabled.
  - **None**
  - **Attempt**
  - **Require**

- **Packet queuing**  
  CSP: [MdmStore/Global/EnablePacketQueue](/windows/client-management/mdm/firewall-csp#enablepacketqueue)

  Specify how scaling for the software on the receive side is enabled for the encrypted receive and clear text forward for the IPsec tunnel gateway scenario. This setting ensures that the packet order is preserved.

  - **Not configured** (*default*) - Packet queuing returns to the client default, which is disabled.
  - **Disabled**
  - **Queue Inbound**
  - **Queue Outbound**
  - **Queue Both**

- **Firewall profile private**  
  [2.2.2 FW_PROFILE_TYPE](/openspecs/windows_protocols/ms-fasp/7704e238-174d-4a5e-b809-5f3787dd8acc)

  - **Configure** (*default*)
  - **Not configured**

  When set to *Configure*, you can configure the following additional settings.

  - **Inbound connections blocked**  
    CSP: [/DefaultInboundAction](/windows/client-management/mdm/firewall-csp#defaultinboundaction)

    - **Yes** (*default*)
    - **Not configured**

  - **Unicast responses to multicast broadcasts required**  
    CSP: [/DisableUnicastResponsesToMulticastBroadcast](/windows/client-management/mdm/firewall-csp#disableunicastresponsestomulticastbroadcast)

    - **Yes** (*default*)
    - **Not configured**

  - **Outbound connections required**  
    CSP: [/DefaultOutboundAction](/windows/client-management/mdm/firewall-csp#defaultoutboundaction)

    - **Yes** (*default*)
    - **Not configured**

  - **Inbound notifications blocked**  
    CSP: [/DisableInboundNotifications](/windows/client-management/mdm/firewall-csp#disableinboundnotifications)

    - **Yes** (*default*)
    - **Not configured**

  - **Global port rules from group policy merged**  
    CSP: [/GlobalPortsAllowUserPrefMerge](/windows/client-management/mdm/firewall-csp#globalportsallowuserprefmerge)

    - **Yes** (*default*)
    - **Not configured**

  - **Firewall enabled**  
    CSP: [/EnableFirewall](/windows/client-management/mdm/firewall-csp#enablefirewall)

    - **Not configured**
    - **Blocked**
    - **Allowed** (*default*)

  - **Authorized application rules from group policy not merged**  
    CSP: [/AuthAppsAllowUserPrefMerge](/windows/client-management/mdm/firewall-csp#authappsallowuserprefmerge)

    - **Yes** (*default*)
    - **Not configured**

  - **Connection security rules from group policy not merged**  
    CSP: [/AllowLocalIpsecPolicyMerge](/windows/client-management/mdm/firewall-csp#allowlocalipsecpolicymerge)

    - **Yes** (*default*)
    - **Not configured**

  - **Incoming traffic required**  
    CSP: [/Shielded](/windows/client-management/mdm/firewall-csp#shielded)

    - **Yes** (*default*)
    - **Not configured**

  - **Policy rules from group policy not merged**  
    CSP: [/AllowLocalPolicyMerge](/windows/client-management/mdm/firewall-csp#allowlocalpolicymerge)

    - **Yes** (*default*)
    - **Not configured**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

  - **Stealth mode blocked**  
    CSP: [/DisableStealthMode](/windows/client-management/mdm/firewall-csp#disablestealthmode)

    - **Yes** (*default*)
    - **Not configured**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020,atp-december-2020"

- **Firewall profile public**  
  [2.2.2 FW_PROFILE_TYPE](/openspecs/windows_protocols/ms-fasp/7704e238-174d-4a5e-b809-5f3787dd8acc)

  - **Configure** (*default*)
  - **Not configured**

  When set to *Configure*, you can configure the following additional settings.

  - **Inbound connections blocked**  
    CSP: [/DefaultInboundAction](/windows/client-management/mdm/firewall-csp#defaultinboundaction)

    - **Yes** (*default*)
    - **Not configured**

  - **Unicast responses to multicast broadcasts required**  
    CSP: [/DisableUnicastResponsesToMulticastBroadcast](/windows/client-management/mdm/firewall-csp#disableunicastresponsestomulticastbroadcast)

    - **Yes** (*default*)
    - **Not configured**

  - **Outbound connections required**  
    CSP: [/DefaultOutboundAction](/windows/client-management/mdm/firewall-csp#defaultoutboundaction)

    - **Yes** (*default*)
    - **Not configured**

  - **Authorized application rules from group policy not merged**  
    CSP: [/AuthAppsAllowUserPrefMerge](/windows/client-management/mdm/firewall-csp#authappsallowuserprefmerge)

    - **Yes** (*default*)
    - **Not configured**

  - **Inbound notifications blocked**  
    CSP: [/DisableInboundNotifications](/windows/client-management/mdm/firewall-csp#disableinboundnotifications)

    - **Yes** (*default*)
    - **Not configured**

  - **Global port rules from group policy merged**  
    CSP: [/GlobalPortsAllowUserPrefMerge](/windows/client-management/mdm/firewall-csp#globalportsallowuserprefmerge)

    - **Yes** (*default*)
    - **Not configured**

  - **Firewall enabled**  
    CSP: [/EnableFirewall](/windows/client-management/mdm/firewall-csp#enablefirewall)

    - **Not configured**
    - **Blocked**
    - **Allowed** (*default*)

  - **Connection security rules from group policy not merged**  
    CSP: [/AllowLocalIpsecPolicyMerge](/windows/client-management/mdm/firewall-csp#allowlocalipsecpolicymerge)

    - **Yes** (*default*)
    - **Not configured**

  - **Incoming traffic required**  
    CSP: [/Shielded](/windows/client-management/mdm/firewall-csp#shielded)

    - **Yes** (*default*)
    - **Not configured**

  - **Policy rules from group policy not merged**  
    CSP: [/AllowLocalPolicyMerge](/windows/client-management/mdm/firewall-csp#allowlocalpolicymerge)

    - **Yes** (*default*)
    - **Not configured**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

  - **Stealth mode blocked**  
    CSP: [/DisableStealthMode](/windows/client-management/mdm/firewall-csp#disablestealthmode)

    - **Yes** (*default*)
    - **Not configured**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020,atp-december-2020"

- **Firewall profile domain**  
  CSP: [2.2.2 FW_PROFILE_TYPE](/openspecs/windows_protocols/ms-fasp/7704e238-174d-4a5e-b809-5f3787dd8acc)

  - **Unicast responses to multicast broadcasts required**  
    CSP: [/DisableUnicastResponsesToMulticastBroadcast](/windows/client-management/mdm/firewall-csp#disableunicastresponsestomulticastbroadcast)

    - **Yes** (*default*)
    - **Not configured**

  - **Authorized application rules from group policy not merged**  
    CSP: [/AuthAppsAllowUserPrefMerge](/windows/client-management/mdm/firewall-csp#authappsallowuserprefmerge)

    - **Yes** (*default*)
    - **Not configured**  

  - **Inbound notifications blocked**  
    CSP: [/DisableInboundNotifications](/windows/client-management/mdm/firewall-csp#disableinboundnotifications)

    - **Yes** (*default*)
    - **Not configured**

  - **Global port rules from group policy merged**  
    CSP: [/GlobalPortsAllowUserPrefMerge](/windows/client-management/mdm/firewall-csp#globalportsallowuserprefmerge)

    - **Yes** (*default*)
    - **Not configured**

  - **Firewall enabled**  
    CSP: [/EnableFirewall](/windows/client-management/mdm/firewall-csp#enablefirewall)

    - **Not configured**
    - **Blocked**
    - **Allowed** (*default*)

  - **Connection security rules from group policy not merged**  
    CSP: [/AllowLocalIpsecPolicyMerge](/windows/client-management/mdm/firewall-csp#allowlocalipsecpolicymerge)

    - **Yes** (*default*)
    - **Not configured**

  - **Policy rules from group policy not merged**  
    CSP: [/AllowLocalPolicyMerge](/windows/client-management/mdm/firewall-csp#allowlocalpolicymerge)

    - **Yes** (*default*)
    - **Not configured**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

  - **Stealth mode blocked**  
    CSP: [/DisableStealthMode](/windows/client-management/mdm/firewall-csp#disablestealthmode)

    - **Yes** (*default*)
    - **Not configured**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020,atp-december-2020"

## Microsoft Defender

::: zone-end
::: zone pivot="atp-sept-2020,atp-december-2020"

- **Turn on real-time protection**  
  CSP: [Defender/AllowRealtimeMonitoring](/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

  - **Yes** (*default*) - Real-time monitoring is enforced and the user can't disable it.
  - **Not configured** - The setting is returned to client default, which is on, but the user can change it. To disable real-time monitoring, use a custom URI.

- **Additional amount of time (0-50 seconds) to extend cloud protection timeout**  
  CSP: [Defender/CloudExtendedTimeout](/windows/client-management/mdm/policy-csp-defender#defender-cloudextendedtimeout)

  Defender Antivirus automatically blocks suspicious files for 10 seconds so it can scan the files in the cloud to make sure they're safe. With this setting, you can add up to 50 additional seconds to this timeout.  By default, the timeout is set to zero (**0**).

- **Scan all downloaded files and attachments**  
  CSP: [Defender/AllowIOAVProtection](/windows/client-management/mdm/policy-csp-defender)

  - **Yes** (*default*) - All downloaded files and attachments are scanned. The setting is returned to client default, which is on, but the user can change it. To disable this setting, use a custom URI.
  - **Not configured** - The setting is returned to client default, which is on, but the user can change it. To disable this setting, use a custom URI.

- **Scan type**  
  CSP: [Defender/ScanParameter](/windows/client-management/mdm/policy-csp-defender#defender-scanparameter)

  - **User defined**
  - **Disabled**
  - **Quick scan** (*default*)
  - **Full scan**

::: zone-end
::: zone pivot="atp-december-2020"

- **Defender schedule scan day**:  
  Defender schedule scan day.

  **Default**: Everyday

- **Defender scan start time**:  
  Defender schedule scan time.

  **Default**: Not configured

::: zone-end
::: zone pivot="atp-sept-2020,atp-december-2020"

- **Defender sample submission consent**  
  CSP: [Defender/SubmitSamplesConsent](/windows/client-management/mdm/policy-csp-defender#defender-submitsamplesconsent)

  Checks for the user consent level in Microsoft Defender to send data. If the required consent has already been granted, Microsoft Defender submits them. If not (and if the user has specified never to ask), the UI launches to ask for user consent (when *Cloud-delivered protection* is set to *Yes*) before sending data.

  - **Send safe samples automatically** (*default*)
  - **Always prompt**
  - **Never send**
  - **Send all samples automatically**

- **Cloud-delivered protection level**  
  CSP: [CloudBlockLevel](/windows/client-management/mdm/policy-csp-defender#defender-cloudblocklevel)

  Configure how aggressive Defender Antivirus is in blocking and scanning suspicious files.
  - **Not configured** - Default Defender blocking level.
  - **High** *(default)* - Aggressively block unknowns while optimizing client performance, which includes a greater chance of false positives.
  - **High plus** - Aggressively block unknowns and apply additional protection measures that might impact client performance.
  - **Zero tolerance** - Block all unknown executable files.

- **Scan removable drives during full scan**  
  CSP: [Defender/AllowFullScanRemovableDriveScanning](/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanremovabledrivescanning)

  - **Yes** (*default*) - During a full scan, removable drives (like USB flash drives) are scanned.
  - **Not configured** - The setting returns to client default, which scans removable drives, however the user can disable this scan.

- **Defender potentially unwanted app action**  
  CSP: [Defender/PUAProtection](/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)

  Specify the level of detection for potentially unwanted applications (PUAs). Defender alerts users when potentially unwanted software is being downloaded or attempts to install on a device.
  - **Device default**
  - **Block** (*default*) - Detected items are blocked, and show in history along with other threats.
  - **Audit** - Defender detects potentially unwanted applications, but takes no action. You can review information about the applications Defender would have taken action against by searching for events that are created by Defender in the Event Viewer.

- **Turn on cloud-delivered protection**  
  CSP: [AllowCloudProtection](/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  By default, Defender on Windows 10/11 desktop devices sends information to Microsoft about any problems it finds. Microsoft analyzes that information to learn more about problems affecting you and other customers, to offer improved solutions.

  - **Yes** (*default*) - Cloud-delivered protection is turned on.  Device users can't change this setting.
  - **Not configured**  - The setting is restored to the system default.

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

- **Run daily quick scan at**  
  CSP: [Defender/ScheduleQuickScanTime](/windows/client-management/mdm/policy-csp-defender#defender-schedulequickscantime)
  
   Configure when the daily quick scan runs. By default, the scan run is set to **2 AM**.

- **Scheduled scan start time**  
  
  By default, the start time is set to **2 AM**.

- **Configure low CPU priority for scheduled scans**  
  CSP: [Defender/EnableLowCPUPriority](/windows/client-management/mdm/policy-csp-defender#defender-enablelowcpupriority)  

  -**Yes** (*default*)
  - **Not configured**

- **Block Office communication apps from creating child processes**  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)  

  This ASR rule is controlled via the following GUID: 26190899-1602-49e8-8b27-eb1d0a1ce869.
  - **Not configured** - The Windows default is restored, which is to not block creation of child processes.
  - **User defined**
  - **Enable** (*default*) - Office communication applications are blocked from creating child processes.
  - **Audit mode** - Windows events are raised instead of blocking child processes.

- **Block Adobe Reader from creating child processes**  
  [Reduce attack surfaces with attack surface reduction rules](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)  

  - **Not configured** - The Windows default is restored, is to not block creation of child processes.
  - **User defined**
  - **Enable** (*default*) - Adobe Reader is blocked from creating child processes.
  - **Audit mode** - Windows events are raised instead of blocking child processes.

- **Scan incoming email messages**  
  CSP: [Defender/AllowEmailScanning](/windows/client-management/mdm/policy-csp-defender#defender-allowemailscanning)

  - **Yes** (*default*) - E-mail mailbox and mail files such as PST, DBX, MNX, MIME, and BINHEX are scanned.
  - **Not configured** - The setting returns to the client default of e-mail files not being scanned.

- **Turn on real-time protection**  
  CSP: [Defender/AllowRealtimeMonitoring](/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

  - **Yes** (*default*) - Real-time monitoring is enforced and the user can't disable it.
  - **Not configured** - The setting is returned to client default, which is on, but the user can change it. To disable real-time monitoring, use a custom URI.

- **Number of days (0-90) to keep quarantined malware**  
  CSP: [Defender/DaysToRetainCleanedMalware](/windows/client-management/mdm/policy-csp-defender#defender-daystoretaincleanedmalware)

  Configure the number of days items should be kept in the quarantine folder before being removed. The default is zero (**0**), which results in quarantined files never being removed.

- **Defender system scan schedule**  
  CSP: [Defender/ScheduleScanDay](/windows/client-management/mdm/policy-csp-defender#defender-schedulescanday)

  Schedule on which day Defender scans devices. By default the scan is **User defined** but can be set to *Everyday*, any day of the week, or to have *No scheduled scan*.

- **Additional amount of time (0-50 seconds) to extend cloud protection timeout**  
  CSP: [Defender/CloudExtendedTimeout](/windows/client-management/mdm/policy-csp-defender#defender-cloudextendedtimeout)

  Defender Antivirus automatically blocks suspicious files for 10 seconds so it can scan the files in the cloud to make sure they're safe. With this setting, you can add up to 50 additional seconds to this timeout.  By default, the timeout is set to zero (**0**).

- **Scan mapped network drives during a full scan**  
  CSP: [Defender/AllowFullScanOnMappedNetworkDrives](/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanonmappednetworkdrives)

  - **Yes** (*default*) - During a full scan, mapped network drives are included.
  - **Not configured** - The client returns to its default, which disables scanning on mapped network drives.

- **Turn on network protection**  
  CSP: [Defender/EnableNetworkProtection](/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)
  
  - **Yes** (*default*) - Block malicious traffic detected by signatures in the Network Inspection System (NIS).
  - **Not configured**

- **Scan all downloaded files and attachments**  
  CSP: [Defender/AllowIOAVProtection](/windows/client-management/mdm/policy-csp-defender)

  - **Yes** (*default*) - All downloaded files and attachments are scanned. The setting is returned to client default, which is on, but the user can change it. To disable this setting, use a custom URI.
  - **Not configured** - The setting is returned to client default, which is on, but the user can change it. To disable this setting, use a custom URI.

::: zone-end
::: zone pivot="atp-april-2020"

- **Block on access protection**  
  CSP: [Defender/AllowOnAccessProtection](/windows/client-management/mdm/policy-csp-defender#defender-allowonaccessprotection)

  - **Yes**
  - **Not configured** (*default*)

::: zone-end
::: zone pivot="atp-march-2020"

- **Block on access protection**  
  CSP: [Defender/AllowOnAccessProtection](/windows/client-management/mdm/policy-csp-defender#defender-allowonaccessprotection)

  - **Yes** (*default*)
  - **Not configured**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

- **Scan browser scripts**  
  CSP: [Defender/AllowScriptScanning](/windows/client-management/mdm/policy-csp-defender)

  - **Yes** (*default*) - The Microsoft Defender Script Scanning functionality is enforced and the user can't turn them off.
  - **Not configured** -  The setting is returned to client default, which is to enable script scanning, however the user can turn it off.

- **Block user access to Microsoft Defender app**  
  CSP: [Defender/AllowUserUIAccess](/windows/client-management/mdm/policy-csp-defender#defender-allowuseruiaccess)

  - **Yes** (*default*) - The Microsoft Defender User Interface (UI) is inaccessible and notifications are surprised
  - **Not configured**
 When set to Yes, the Windows Defender User Interface (UI) will be inaccessible and notifications will be surprised. When set to Not configured, the setting will return to client default in which UI and notifications will be allowed

- **Maximum allowed CPU usage (0-100 percent) per scan**  
  CSP: [Defender/AvgCPULoadFactor](/windows/client-management/mdm/policy-csp-defender#defender-avgcpuloadfactor)

  Specify as a percentage the maximum amount of CPU to use for a scan. The default is **50**.

- **Scan type**  
  CSP: [Defender/ScanParameter](/windows/client-management/mdm/policy-csp-defender#defender-scanparameter)

  - **User defined**
  - **Disabled**
  - **Quick scan** (*default*)
  - **Full scan**

- **Enter how often (0-24 hours) to check for security intelligence updates**  
  CSP: [Defender/SignatureUpdateInterval](/windows/client-management/mdm/policy-csp-defender)

  Specify how often to check for updated signatures, in hours. For example, a value of 1 will check each hour. A value of 2 will check every two hours, and so on.

  If no value is defined, devices use the client default of **8** hours.

- **Defender sample submission consent**  
  CSP: [Defender/SubmitSamplesConsent](/windows/client-management/mdm/policy-csp-defender#defender-submitsamplesconsent)

  Checks for the user consent level in Microsoft Defender to send data. If the required consent has already been granted, Microsoft Defender submits them. If not (and if the user has specified never to ask), the UI launches to ask for user consent (when *Cloud-delivered protection* is set to *Yes*) before sending data.

  - **Send safe samples automatically** (*default*)
  - **Always prompt**
  - **Never send**
  - **Send all samples automatically**

- **Cloud-delivered protection level**  
  CSP: [CloudBlockLevel](/windows/client-management/mdm/policy-csp-defender#defender-cloudblocklevel)

  Configure how aggressive Defender Antivirus is in blocking and scanning suspicious files.
  - **Not configured** (*default*) - Default Defender blocking level.
  - **High** - Aggressively block unknowns while optimizing client performance, which includes a greater chance of false positives.
  - **High plus** - Aggressively block unknowns and apply additional protection measures that might impact client performance.
  - **Zero tolerance** - Block all unknown executable files.

- **Scan archive files**  
  CSP: [Defender/AllowArchiveScanning](/windows/client-management/mdm/policy-csp-defender#defender-allowarchivescanning)

  - **Yes** (*default*) - Scanning of archive files such as ZIP or CAB files is enforced.
  - **Not configured** - The setting will be returned back to client default, which is to scan archived files, however the user may disable scanning.

- **Turn on behavior monitoring**  
  CSP: [Defender/AllowBehaviorMonitoring](/windows/client-management/mdm/policy-csp-defender#defender-allowbehaviormonitoring)

  - **Yes** (*default*) - Behavior monitoring is enforced and the user can't disable it.
  - **Not configured** - The setting is returned to client default, which is on, but the user can change it. To disable real-time monitoring, use a custom URI.
  
- **Scan removable drives during full scan**  
  CSP: [Defender/AllowFullScanRemovableDriveScanning](/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanremovabledrivescanning)

  - **Yes** (*default*) - During a full scan, removable drives (like USB flash drives) are scanned.
  - **Not configured** - The setting returns to client default, which scans removable drives, however the user can disable this scan.
  
- **Scan network files**  
  CSP: [Defender/AllowScanningNetworkFiles](/windows/client-management/mdm/policy-csp-defender#defender-allowscanningnetworkfiles)

  - **Yes** (*default*) - Microsoft Defender scans network files.
  - **Not configured** - The client returns to its default, which disables scanning of network files.

- **Defender potentially unwanted app action**  
  CSP: [Defender/PUAProtection](/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)

  Specify the level of detection for potentially unwanted applications (PUAs). Defender alerts users when potentially unwanted software is being downloaded or attempts to install on a device.
  - **Device default**
  - **Block** (*default*) - Detected items are blocked, and show in history along with other threats.
  - **Audit** - Defender detects potentially unwanted applications, but takes no action. You can review information about the applications Defender would have taken action against by searching for events that are created by Defender in the Event Viewer.

- **Turn on cloud-delivered protection**  
  CSP: [AllowCloudProtection](/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  By default, Defender on Windows 10/11 desktop devices sends information to Microsoft about any problems it finds. Microsoft analyzes that information to learn more about problems affecting you and other customers, to offer improved solutions.

  - **Yes** (*default*) - Cloud-delivered protection is turned on.  Device users can't change this setting.
  - **Not configured**  - The setting is restored to the system default.

- **Block Office applications from injecting code into other processes**  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  This ASR rule is controlled via the following GUID: 75668C1F-73B5-4CF0-BB93-3ECF5CB7CC84
  - **Not configured** - The setting returns to the Windows default, which is off.
  - **Block** (*default*) - Office applications are blocked from injecting code into other processes.
  - **Audit mode** - Windows events are raised instead of blocking.

- **Block Office applications from creating executable content**  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  This ASR rule is controlled via the following GUID: 3B576869-A4EC-4529-8536-B80A7769E899
  - **Not configured** - The setting returns to the Windows default, which is off.
  - **Block** (*default*) - Office applications are blocked from create executable content.
  - **Audit mode** - Windows events are raised instead of blocking.
  
- **Block JavaScript or VBScript from launching downloaded executable content**  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

   This ASR rule is controlled via the following GUID: D3E037E1-3EB8-44C8-A917-57927947596D
  - **Not configured** - The setting returns to the Windows default, which is off.
  - **Block** (*default*) - Defender blocks JavaScript or VBScript files that have been downloaded from the Internet from being executed.
  - **Audit mode** - Windows events are raised instead of blocking.
  
- **Enable network protection**  
  CSP: [Defender/EnableNetworkProtection](/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

  - **Not configured** - The setting returns to the Windows default, which is disabled.
  - **User defined**
  - **Enable** - Network protection is enabled for all users on the system.
  - **Audit mode** (*default*) - Users aren't blocked from dangerous domains and Windows events are raised instead.

- **Block untrusted and unsigned processes that run from USB**  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  This ASR rule is controlled via the following GUID: b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4
  - **Not configured** - The setting returns to the Windows default, which is off.
  - **Block** (*default*) - Untrusted and unsigned processes that run from a USB drive are blocked.
  - **Audit mode** - Windows events are raised instead of blocking.

- **Block credential stealing from the Windows local security authority subsystem (lsass.exe)**  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  This ASR rule is controlled via the following GUID: 9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2
  - **Not configured** -The setting returns to the Windows default, which is off.
  - **User defined**
  - **Enable** (*default*) - Attempts to steal credentials via lsass.exe are blocked.
  - **Audit mode** - Users aren't blocked from dangerous domains and Windows events are raised instead.

- **Block executable content download from email and webmail clients**  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  - **Not configured** - The setting returns to the Windows default, which is off.
  - **Block** (*default*) - Executable content downloaded from email and webmail clients is blocked.
  - **Audit mode** - Windows events are raised instead of blocking.

- **Block all Office applications from creating child processes**  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  This ASR rule is controlled via the following GUID: D4F940AB-401B-4EFC-AADC-AD5F3C50688A
  - **Not configured** - The setting returns to the Windows default, which is off.
  - **Block** (*default*)
  - **Audit mode** - Windows events are raised instead of blocking.

- **Block execution of potentially obfuscated scripts (js/vbs/ps)**  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  This ASR rule is controlled via the following GUID: 5BEB7EFE-FD9A-4556-801D-275E5FFC04CC
  - **Not configured** - The setting returns to the Windows default, which is off.
  - **Block** (*default*) - Defender will block execution of obfuscated scripts.
  - **Audit mode** - Windows events are raised instead of blocking.

- **Block Win32 API calls from Office macro**  
  [Protect devices from exploits](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  This ASR rule is controlled via the following GUID: 92E97FA1-2EDF-4476-BDD6-9DD0B4DDDC7B
  - **Not configured** - The setting returns to the Windows default, which is off.
  - **Block** (*default*) - Office macro's will be blocked from using Win32 API calls.
  - **Audit mode** - Windows events are raised instead of blocking.

## Microsoft Defender Security Center

- **Block users from editing the Exploit Guard protection interface**  
  CSP: [WindowsDefenderSecurityCenter/DisallowExploitProtectionOverride](/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-disallowexploitprotectionoverride)

  - **Yes** (*default*) -  Prevent users from making changes to the exploit protection settings area in the Microsoft Defender Security Center.
  - **Not configured** - Local users can make changes in the exploit protection settings area.

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020,atp-december-2020"

## Smart Screen

::: zone-end
::: zone pivot="atp-sept-2020,atp-december-2020"

- **Block users from ignoring SmartScreen warnings**  
  CSP: [SmartScreen/PreventOverrideForFilesInShell](/windows/client-management/mdm/policy-csp-smartscreen#smartscreen-preventoverrideforfilesinshell)

   This setting requires the 'Turn on Windows SmartScreen' setting be set to Yes.
  - **Yes** (*default*) - SmartScreen is enabled and users can't bypass warnings for files or malicious apps.
  - **Not configured** - Users can ignore SmartScreen warnings for files and malicious apps.

- **Turn on Windows SmartScreen**  
  CSP: [SmartScreen/EnableSmartScreenInShell](/windows/client-management/mdm/policy-csp-smartscreen#smartscreen-enablesmartscreeninshell)

  - **Yes** (*default*) - Enforce the use of SmartScreen for all users.
  - **Not configured** - Return the setting to Windows default, which is to enable SmartScreen, however users may change this setting. To disable SmartScreen, use a custom URI.

- **Require SmartScreen for Microsoft Edge**  
  CSP: [Browser/AllowSmartScreen](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

  - **Yes** (*default*) - Enable Microsoft Edge SmartScreen for accessing site and file downloads.
  - **Not configured**

- **Block malicious site access**  
  CSP: [Browser/PreventSmartScreenPromptOverride](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)  

  - **Yes** (*default*) - Block users from ignoring the Microsoft Defender SmartScreen Filter warnings and block them from going to the site.
  - **Not configured**

- **Block unverified file download**  
  CSP: [Browser/PreventSmartScreenPromptOverrideForFiles](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)  

  - **Yes** (*default*) - Block users from ignoring the Microsoft Defender SmartScreen Filter warnings and block them from downloading unverified files.
  - **Not configured**

- **Configure Microsoft Defender SmartScreen**  
  This policy is available only on Windows instances that are joined to a Microsoft Active Director domain; or on Windows 10/11 Pro or Enterprise instances that are enrolled for device management.

  Microsoft Defender SmartScreen provides warning messages to help protect your users from potential phishing scams and malicious software. By default, Microsoft Defender SmartScreen is turned on.

  - **Enabled** *(default)* - Microsoft Defender SmartScreen is turned on and users can't turn it off.
  - **Disabled** - Microsoft Defender SmartScreen is turned off and users can't turn it on.
  - **Not configured** -  Users can choose whether to use Microsoft Defender SmartScreen.

- **Prevent bypassing Microsoft Defender SmartScreen prompts for sites**  
  This policy setting lets you decide whether users can override the Microsoft Defender SmartScreen warnings about potentially malicious websites.

  - **Enabled** *(default)* - If you enable this setting, users can't ignore Microsoft Defender SmartScreen warnings and they are blocked from continuing to the site.
  - **Disabled** - Users can ignore Microsoft Defender SmartScreen warnings and continue to the site.
  - **Not configured** - Same behavior as *Disabled*.

- **Prevent bypassing of Microsoft Defender SmartScreen warnings about downloads**  
  This policy lets you determine whether users can override Microsoft Defender SmartScreen warnings about unverified downloads.

  - **Enabled** *(default)* - Users in your organization can't ignore Microsoft Defender SmartScreen warnings, and they're prevented from completing the unverified downloads.
  - **Disabled** - Users can ignore Microsoft Defender SmartScreen warnings and complete unverified downloads.
  - **Not configured** - Same behavior as *Disabled*.

- **Configure Microsoft Defender SmartScreen to block potentially unwanted apps**  
  This policy is available only on Windows instances that are joined to a Microsoft Active Directory domain; or on Windows 10/11 Pro or Enterprise instances that are enrolled for device management.

  This policy setting lets you configure whether to turn on blocking for potentially unwanted apps in Microsoft Defender SmartScreen. Potentially unwanted app blocking in Microsoft Defender SmartScreen provides warning messages to help protect users from adware, coin miners, bundleware, and other low-reputation apps that are hosted by websites. Potentially unwanted app blocking in Microsoft Defender SmartScreen is turned off by default.

  - **Enabled** *(default)* - Potentially unwanted app blocking in Microsoft Defender SmartScreen is turned on.
  - **Disabled** - Potentially unwanted app blocking in Microsoft Defender SmartScreen is turned off.
  - **Not configured** - If you don't configure this setting, users can choose whether to use potentially unwanted app blocking in Microsoft Defender SmartScreen.

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

- **Block users from ignoring SmartScreen warnings**  
  CSP: [SmartScreen/PreventOverrideForFilesInShell](/windows/client-management/mdm/policy-csp-smartscreen#smartscreen-preventoverrideforfilesinshell)

   This setting requires the 'Turn on Windows SmartScreen' setting be set to Yes.
  - **Yes** (*default*) - SmartScreen is enabled and users can't bypass warnings for files or malicious apps.
  - **Not configured** - Users can ignore SmartScreen warnings for files and malicious apps.

- **Require apps from store only**  

  - **Yes** (*default*)
  - **Not configured**

- **Turn on Windows SmartScreen**  
  CSP: [SmartScreen/EnableSmartScreenInShell](/windows/client-management/mdm/policy-csp-smartscreen#smartscreen-enablesmartscreeninshell)

  - **Yes** (*default*) - Enforce the use of SmartScreen for all users.
  - **Not configured** - Return the setting to Windows default, which is to enable SmartScreen, however users may change this setting. To disable SmartScreen, use a custom URI.

## Windows Hello for Business

For more information, see [PassportForWork CSP](/windows/client-management/mdm/passportforwork-csp) in the Windows documentation.

- **Block Windows Hello for Business**  

   Windows Hello for Business is an alternative method for signing into Windows by replacing passwords, Smart Cards, and Virtual Smart Cards.

  - **Not configured** - Devices device provision Windows Hello for Business, which is the Windows default.
  - **Disabled** (*default*) - Devices provision Windows Hello for Business.
  - **Enabled** - Devices don't provision Windows Hello for Business for any user.

  When set to *Disabled*, you can configure the following settings:

  - **Lowercase letters in PIN**  
    - **Not allowed**
    - **Required**
    - **Allowed** (*default*)

  - **Special characters in PIN**
    - **Not allowed**
    - **Required**
    - **Allowed** (*default*)

  - **Uppercase letters in PIN**
    - **Not allowed**
    - **Required**
    - **Allowed** (*default*)

::: zone-end

## Next steps

- [Learn about security baselines](security-baselines.md)
- [Avoid conflicts](security-baselines.md#avoid-conflicts)
- [Troubleshoot policies and profiles in Intune](/troubleshoot/mem/intune/troubleshoot-policies-in-microsoft-intune)
