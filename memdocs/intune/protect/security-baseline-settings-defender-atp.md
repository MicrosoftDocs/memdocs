---
# required metadata

title: Intune security baselines settings for Microsoft Defender Advanced Threat Protection 
titleSuffix: Microsoft Intune
description: Security baseline settings supported by Intune for managing Microsoft Defender Advanced Threat Protection
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/01/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology:
ms.assetid:


# optional metadata

#ROBOTS:

#audience:

ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
zone_pivot_groups: edge-baseline-versions
---

<!-- Pivots in use: 
::: zone pivot="atp-april-2020"
::: zone-end

::: zone pivot="atp-march-2020"
::: zone-end

::: zone pivot="atp-march-2020,atp-april-2020"
::: zone-end
-->

# Microsoft Defender Advanced Threat Protection baseline settings for Intune

View the Microsoft Defender Advanced Threat Protection baseline settings that are supported by Microsoft Intune. The Advanced Threat Protection (ATP) baseline defaults represent the recommended configuration for ATP, and might not match baseline defaults for other security baselines.

The details in this article apply to version 4 of the Microsoft Defender ATP baseline, which released on April 21, 2020. To understand what's changed with this version of the baseline from previous versions, use the [Compare baselines](../protect/security-baselines.md#compare-baseline-versions) action that's available when viewing the *Versions* pane for this baseline.

The Microsoft Defender Advanced Threat Protection baseline is available when your environment meets the prerequisites for using [Microsoft Defender Advanced Threat Protection](advanced-threat-protection.md#prerequisites).

This baseline is optimized for physical devices and is currently not recommended for use on virtual machines (VMs) or VDI endpoints. Certain baseline settings can impact remote interactive sessions on virtualized environments. For more information, see [Increase compliance to the Microsoft Defender ATP security baseline](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/configure-machines-security-baseline) in the Windows documentation.

::: zone pivot="atp-march-2020,atp-april-2020"

## Application Guard

For more information, see [WindowsDefenderApplicationGuard CSP](https://docs.microsoft.com/windows/client-management/mdm/windowsdefenderapplicationguard-csp) in the Windows documentation.  

While using Microsoft Edge, Microsoft Defender Application Guard protects your environment from sites that aren't trusted by your organization. When users visit sites that aren't listed in your isolated network boundary, the sites open in a Hyper-V virtual browsing session. Trusted sites are defined by a network boundary.  

- **Turn on Application Guard for Edge (Options)**  
  CSP: [Settings/AllowWindowsDefenderApplicationGuard](https://go.microsoft.com/fwlink/?linkid=872350)
  
  - **Enabled for Edge** (*default*) - Application Guard opens unapproved sites in a Hyper-V virtualized browsing container.
  - **Not configured** - Any site (trusted and untrusted) opens on the device, and not in a virtualized container.  
  
  When set to *Enable for Edge*, you can configure *Block external content from non-enterprise approved sites* and *Clipboard behavior*.

  - **Block external content from non-enterprise approved sites**  
    CSP: [Settings/BlockNonEnterpriseContent](https://go.microsoft.com/fwlink/?linkid=872352)

    - **Yes** (*default*) - Block content from unapproved websites from loading.
    - **Not configured** - Non-enterprise sites can open on the device

  - **Clipboard behavior**  
    CSP: [Settings/ClipboardSettings](https://go.microsoft.com/fwlink/?linkid=872351)

    Choose what copy and paste actions are allowed between the local PC and the Application Guard virtual browser. Options include:
    - **Not Configured**  
    - **Block copy and paste between PC and browser** (*default*) - Block both. Data can't transfer between the PC and the virtual browser.
    - **Allow copy and paste from browser to PC only** - Data can't transfer from the PC into the virtual browser.
    - **Allow copy and paste from PC to browser only** - Data can't transfer from the virtual browser to the host PC.
    - **Allow copy and paste between PC and browser** - No block for content exists.

- **Windows network isolation policy**  
  CSP: [Policy CSP - NetworkIsolation](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-networkisolation)

  Specify a list of *Network domains*, which are Enterprise resources that are hosted in the cloud that Application Guard treats as enterprise sites
  - **Configure** (*default*)
  - **Not configured**

  When set to *Configure* you can then define *Network domains*.

  - **Network domains**  
    Select **Add** and specify domains, IP address ranges, and network boundaries. By default, *securitycenter.windows.com* is configured.

## BitLocker

For more information, [BitLocker Group Policy settings](https://docs.microsoft.com/windows/security/information-protection/bitlocker/bitlocker-group-policy-settings) in the Windows documentation.

- **Require storage cards to be encrypted (mobile only)**  
  CSP: [RequireStorageCardEncryption](https://go.microsoft.com/fwlink/?linkid=872524)

  This setting only applies to Windows Mobile and Mobile Enterprise SKU devices.
  - **Yes** (*default*) - Encryption on storage cards is required for mobile devices.
  - **Not configured** - The setting returns to the OS default, which is to not require storage card encryption.

- **Enable full disk encryption for OS and fixed data drives**  
  CSP: [RequireDeviceEncryption](https://go.microsoft.com/fwlink/?linkid=872523)

  If the drive was encrypted before this policy applied, no extra action is taken. If the encryption method and options match that of this policy, configuration should return success. If an in-place BitLocker configuration option doesn't match this policy, configuration will likely return an error.
  
  To apply this policy to a disk already encrypted, decrypt the drive and reapply the MDM policy. Windows default is to not require BitLocker drive encryption, however on Azure AD Join and Microsoft Account (MSA) registration/login automatic encryption may apply enabling BitLocker at XTS-AES 128-bit encryption.

  - **Yes** (*default*) - Enforce use of BitLocker.
  - **Not configured** - No BitLocker enforcement takes place.

- **BitLocker system drive policy**  
  [BitLocker Group Policy settings](https://go.microsoft.com/fwlink/?linkid=2067025)

  - **Configure** (*default*)
  - **Not configured**

  When set to *Configure*, you can then configure *Configure encryption method for Operating System drives*.

  - **Configure encryption method for Operating System drives**  
    CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  
    This setting is available when *BitLocker system drive policy* is set to *Configure*.  

    Configure the encryption method and cipher strength for system drives.  *XTS- AES 128-bit* is the Windows default encryption method and the recommended value.

    - **Not configured** (*default*)
    - **AES 128bit CBC**
    - **AES 256bit CBC**
    - **AES 128bit XTS**
    - **AES 256bit XTS**

- **BitLocker fixed drive policy**  
  [BitLocker Group Policy settings](https://go.microsoft.com/fwlink/?linkid=2067018)

  - **Configure** (*default*)
  - **Not configured**

  When set to *Configure*, you can then configure *Block write access to fixed data-drives not protected by BitLocker* and *Configure encryption method for fixed data-drives*.

  - **Block write access to fixed data-drives not protected by BitLocker**  
    CSP: [FixedDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872534)  
    This setting is available when *BitLocker fixed drive policy* is set to *Configure*.

    - **Not configured** (*default*) - Data can be written to non-encrypted fixed drives.
    - **Yes** - Windows will not allow any data to be written to fixed drives that are not BitLocker protected. If a fixed drive is not encrypted, the user will need to complete the BitLocker setup wizard for the drive before write access is granted.

  - **Configure encryption method for fixed data-drives**  
    CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  
    This setting is available when *BitLocker fixed drive policy* is set to *Configure*.

    Configure the encryption method and cipher strength for fixed data-drives disks. *XTS- AES 128-bit* is the Windows default encryption method and the recommended value.

    - **Not configured** (*default*)
    - **AES 128bit CBC**
    - **AES 256bit CBC**
    - **AES 128bit XTS**
    - **AES 256bit XTS**

- **BitLocker removable drive policy**  
  [BitLocker Group Policy settings](https://go.microsoft.com/fwlink/?linkid=2067140)

  - **Configure** (*default*)
  - **Not configured**

  When set to *Configure*, you can then configure *Configure encryption method for removable data-drives* and *Block write access to removable data-drives not protected by BitLocker*.

  - **Configure encryption method for removable data-drives**  
    CSP: [EncryptionMethodByDriveType](https://go.microsoft.com/fwlink/?linkid=872526)  
    This setting is available when *BitLocker removable drive policy* is set to *Configure*.

    Configure the encryption method and cipher strength for removable data-drives disks. *XTS- AES 128-bit* is the Windows default encryption method and the recommended value.

    - **Not configured**
    - **AES 128bit CBC**
    - **AES 256bit CBC** (*default*)
    - **AES 128bit XTS**
    - **AES 256bit XTS**

  - **Block write access to removable data-drives not protected by BitLocker**  
    CSP: [RemovableDrivesRequireEncryption](https://go.microsoft.com/fwlink/?linkid=872540)  
    This setting is available when *BitLocker removable drive policy* is set to *Configure*.

    - **Not configured** (*default*) - Data can be written to non-encrypted removable drives.  
    - **Yes** - Windows will not allow any data to be written to removable drives that are not BitLocker protected. If a removable drive is not encrypted, the user must complete the BitLocker setup wizard for the drive before write access is granted.

## Browser

- **Require SmartScreen for Microsoft Edge**  
  CSP: [Browser/AllowSmartScreen](https://go.microsoft.com/fwlink/?linkid=2067029)

  - **Yes** (*default*) - Use SmartScreen to protect users from potential phishing scams and malicious software.
  - **Not configured**

- **Block malicious site access**  
  CSP: [Browser/PreventSmartScreenPromptOverride](https://go.microsoft.com/fwlink/?linkid=2067040)  

  - **Yes** (*default*) - Block users from ignoring the Microsoft Defender SmartScreen Filter warnings and block them from going to the site.
  - **Not configured**

- **Block unverified file download**  
  CSP: [Browser/PreventSmartScreenPromptOverrideForFiles](https://go.microsoft.com/fwlink/?linkid=2067023)  

  - **Yes** (*default*) - Block users from ignoring the Microsoft Defender SmartScreen Filter warnings and block them from downloading unverified files.
  - **Not configured**

## Data Protection

- **Block direct memory access**  
  CSP: [DataProtection/AllowDirectMemoryAccess](https://go.microsoft.com/fwlink/?linkid=2067031)  

  This policy setting is only enforced when BitLocker or device encryption is enabled.

  - **Yes** (*default*) - Block direct memory access (DMA) for all hot pluggable PCI downstream ports until a user logs into Windows. After a user logs in, Windows enumerates the PCI devices connected to the host plug PCI ports. Every time the user locks the machine, DMA is blocked on hot plug PCI ports with no children devices until the user logs in again. Devices that were already enumerated when the machine was unlocked will continue to function until unplugged.
  - **Not configured**

## Device Guard  

- **Turn on credential guard**  
  CSP: [DeviceGuard/ConfigureSystemGuardLaunch](https://go.microsoft.com/fwlink/?linkid=872424)

  Credential Guard uses Windows Hypervisor to provide protections, which requires Secure Boot and DMA protections to function, which requires that hardware requirements are met.

  - **Not configured** - Disable the use of Credential Guard, which is the Windows default.
  - **Enable with UEFI lock** (*default*) - Enable Credential Guard and not allow it to be disabled remotely, as the UEFI persisted configuration must be manually cleared.
  - **Enable without UEFI lock** - Enable Credential Guard and allow it to be turned off without physical access to the machine.

## Device Installation

- **Hardware device installation by device identifiers**  
  [DeviceInstallation/PreventInstallationOfMatchingDeviceIDs](https://go.microsoft.com/fwlink/?linkid=2066794)  
  
  This policy setting allows you to specify a list of Plug and Play hardware IDs and compatible IDs for devices that Windows is prevented from installing. This policy setting takes precedence over any other policy setting that allows Windows to install a device.  If you enable this policy setting on a remote desktop server, the policy setting affects redirection of the specified devices from a remote desktop client to the remote desktop server.

  - **Not configured**
  - **Allow hardware device installation** - Devices can be installed and updated as allowed or prevented by other policy settings.
  - **Block hardware device installation** (*default*) - Windows is prevented from installing a device whose hardware ID or compatible ID appears in a list you define.

  When set to *Block hardware device installation* you can configure *Remove matching hardware devices* and *Hardware device identifiers that are blocked*.

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

## DMA Guard

- **Enumeration of external devices incompatible with Kernel DMA Protection**  
  CSP: [DmaGuard/DeviceEnumerationPolicy](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy)

  This policy can provide additional security against external DMA capable devices. It allows for more control over the enumeration of external DMA capable devices incompatible with DMA Remapping/device memory isolation and sandboxing.
  
  This policy only takes effect when Kernel DMA Protection is supported and enabled by the system firmware. Kernel DMA Protection is a platform feature that must be supported by the system at the time of manufacturing. To check if the system supports Kernel DMA Protection, check the Kernel DMA Protection field in the Summary page of MSINFO32.exe.

  - **Not configured** - (*default*)
  - **Block all**
  - **Allow all**

## Endpoint Detection and Response

For more information about the following settings, see [WindowsAdvancedThreatProtection](https://docs.microsoft.com/windows/client-management/mdm/windowsadvancedthreatprotection-csp) CSP in the Windows documentation.

- **Sample sharing for all files**  
  CSP: [Configuration/SampleSharing](https://docs.microsoft.com/windows/client-management/mdm/windowsadvancedthreatprotection-csp)

  Returns or sets the Microsoft Defender Advanced Threat Protection Sample Sharing configuration parameter.  
  
  - **Yes** (*default*)
  - **Not configured**

- **Expedite telemetry reporting frequency**  
  CSP: [Configuration/TelemetryReportingFrequency](https://docs.microsoft.com/windows/client-management/mdm/windowsadvancedthreatprotection-csp)

  Expedite Microsoft Defender Advanced Threat Protection telemetry reporting frequency.  

  - **Yes** (*default*)
  - **Not configured**

## Firewall

For more information, see [Firewall CSP](https://docs.microsoft.com/windows/client-management/mdm/firewall-csp) in the Windows documentation.

- **Disable stateful File Transfer Protocol (FTP)**  
  CSP: [MdmStore/Global/DisableStatefulFtp](https://go.microsoft.com/fwlink/?linkid=872536)  

  - **Yes** (*default*)
  - **Not configured** - The firewall will use FTP to inspect and filter secondary network connections, which could cause your firewall rules to be ignored.

- **Number of seconds a security association can be idle before it's deleted**  
CSP: [MdmStore/Global/SaIdleTime](https://go.microsoft.com/fwlink/?linkid=872539)

  Specify how long the security associations are kept after network traffic is no longer seen. When not configured, the system deletes a security association after it's been idle for *300* seconds (the default).
  
  The number must be from **300** to **3600** seconds.

- **Preshared key encoding**  
  CSP: [MdmStore/Global/PresharedKeyEncoding](https://go.microsoft.com/fwlink/?linkid=872541)

   If you don't require UTF-8, preshared keys will initially be encoded using UTF-8. After that, device users can choose another encoding method.

  - **Not configured**
  - **None**
  - **UTF8** (*default*)

- **Certificate revocation list (CRL) verification**  
  CSP: [MdmStore/Global/CRLcheck](https://go.microsoft.com/fwlink/?linkid=872548)

  Specify how certificate revocation list (CRL) verification is enforced.  

  - **Not configured** (*default*) - CRL verification is disabled.
  - **None**
  - **Attempt**
  - **Require**

- **Packet queuing**  
  CSP: [MdmStore/Global/EnablePacketQueue](https://go.microsoft.com/fwlink/?linkid=872551)

  Specify how scaling for the software on the receive side is enabled for the encrypted receive and clear text forward for the IPsec tunnel gateway scenario. This setting ensures that the packet order is preserved.

  - **Not configured** (*default*) - Packet queuing returns to the client default, which is disabled.
  - **Disabled**
  - **Queue Inbound**
  - **Queue Outbound**
  - **Queue Both**

- **Firewall profile private**  
  [2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2067041)

  - **Configure** (*default*)
  - **Not configured**

  When set to *Configure*, you can configure the following additional settings.

  - **Inbound connections blocked**  
    CSP: [/DefaultInboundAction](https://go.microsoft.com/fwlink/?linkid=872564)

    - **Yes** (*default*)
    - **Not configured**

  - **Unicast responses to multicast broadcasts required**  
    CSP: [/DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

    - **Yes** (*default*)
    - **Not configured**

  - **Stealth mode required**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Yes** (*default*)
    - **Not configured**

  - **Outbound connections required**  
    CSP: [/DefaultOutboundAction](https://aka.ms/intune-firewall-outboundaction)

    - **Yes** (*default*)
    - **Not configured**

  - **Inbound notifications blocked**  
    CSP: [/DisableInboundNotifications](https://go.microsoft.com/fwlink/?linkid=872563)

    - **Yes** (*default*)
    - **Not configured**

  - **Global port rules from group policy merged**  
    CSP: [/GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **Yes** (*default*)
    - **Not configured**

  - **Stealth mode blocked**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Yes** (*default*)
    - **Not configured**

  - **Firewall enabled**  
    CSP: [/EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

    - **Not configured**
    - **Blocked**
    - **Allowed** (*default*)

  - **Authorized application rules from group policy not merged**  
    CSP: [/AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **Yes** (*default*)
    - **Not configured**

  - **Connection security rules from group policy not merged**  
    CSP: [/AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **Yes** (*default*)
    - **Not configured**

  - **Incoming traffic required**  
    CSP: [/Shielded](https://go.microsoft.com/fwlink/?linkid=872561)

    - **Yes** (*default*)
    - **Not configured**

  - **Policy rules from group policy not merged**  
    CSP: [/AllowLocalPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872567)

    - **Yes** (*default*)
    - **Not configured**

- **Firewall profile public**  
  [2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2067143)

  - **Configure** (*default*)
  - **Not configured**

  When set to *Configure*, you can configure the following additional settings.

  - **Inbound connections blocked**  
    CSP: [/DefaultInboundAction](https://go.microsoft.com/fwlink/?linkid=872564)

    - **Yes** (*default*)
    - **Not configured**

  - **Unicast responses to multicast broadcasts required**  
    CSP: [/DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

    - **Yes** (*default*)
    - **Not configured**

  - **Stealth mode required**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Yes** (*default*)
    - **Not configured**

  - **Outbound connections required**  
    CSP: [/DefaultOutboundAction](https://aka.ms/intune-firewall-outboundaction)

    - **Yes** (*default*)
    - **Not configured**

  - **Authorized application rules from group policy not merged**  
    CSP: [/AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **Yes** (*default*)
    - **Not configured**

  - **Inbound notifications blocked**  
    CSP: [/DisableInboundNotifications](https://go.microsoft.com/fwlink/?linkid=872563)

    - **Yes** (*default*)
    - **Not configured**

  - **Global port rules from group policy merged**  
    CSP: [/GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **Yes** (*default*)
    - **Not configured**

  - **Stealth mode blocked**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Yes** (*default*)
    - **Not configured**

  - **Firewall enabled**  
    CSP: [/EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

    - **Not configured**
    - **Blocked**
    - **Allowed** (*default*)

  - **Connection security rules from group policy not merged**  
    CSP: [/AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **Yes** (*default*)
    - **Not configured**

  - **Incoming traffic required**  
    CSP: [/Shielded](https://go.microsoft.com/fwlink/?linkid=872561)

    - **Yes** (*default*)
    - **Not configured**

  - **Policy rules from group policy not merged**  
    CSP: [/AllowLocalPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872567)

    - **Yes** (*default*)
    - **Not configured**

- **Firewall profile domain**  
  CSP: [2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2066796)

  - **Unicast responses to multicast broadcasts required**  
    CSP: [/DisableUnicastResponsesToMulticastBroadcast](https://go.microsoft.com/fwlink/?linkid=872562)

  - **Authorized application rules from group policy not merged**  
    CSP: [/AuthAppsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872565)

    - **Yes** (*default*)
    - **Not configured**  

  - **Inbound notifications blocked**  
    CSP: [/DisableInboundNotifications](https://go.microsoft.com/fwlink/?linkid=872563)

    - **Yes** (*default*)
    - **Not configured**

  - **Global port rules from group policy merged**  
    CSP: [/GlobalPortsAllowUserPrefMerge](https://go.microsoft.com/fwlink/?linkid=872566)

    - **Yes** (*default*)
    - **Not configured**

  - **Stealth mode blocked**  
    CSP: [/DisableStealthMode](https://go.microsoft.com/fwlink/?linkid=872559)

    - **Yes** (*default*)
    - **Not configured**

  - **Firewall enabled**  
    CSP: [/EnableFirewall](https://go.microsoft.com/fwlink/?linkid=872558)

    - **Not configured**
    - **Blocked**
    - **Allowed** (*default*)

  - **Connection security rules from group policy not merged**  
    CSP: [/AllowLocalIpsecPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872568)

    - **Yes** (*default*)
    - **Not configured**

  - **Policy rules from group policy not merged**  
    CSP: [/AllowLocalPolicyMerge](https://go.microsoft.com/fwlink/?linkid=872567)

    - **Yes** (*default*)
    - **Not configured**

## Microsoft Defender

- **Run daily quick scan at**  
  CSP: [Defender/ScheduleQuickScanTime](https://go.microsoft.com/fwlink/?linkid=2114053&clcid=0x409)
  
   Configure when the daily quick scan runs. By default, the scan run is set to **2 AM**.

- **Scheduled scan start time**  
  
  By default, this is set to **2 AM**.

- **Configure low CPU priority for scheduled scans**  
  CSP: [Defender/EnableLowCPUPriority](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-enablelowcpupriority)  

  -**Yes** (*default*)
  - **Not configured**

- **Block Office communication apps from creating child processes**  
  [Protect devices from exploits](https://go.microsoft.com/fwlink/?linkid=874499)  

  This ASR rule is controlled via the following GUID: 26190899-1602-49e8-8b27-eb1d0a1ce869.
  - **Not configured** - The Windows default is restored, is to not block creation of child processes.
  - **User defined**
  - **Enable** (*default*) - Office communication applications are blocked from creating child processes.
  - **Audit mode** - Windows events are raised instead of blocking child processes.

- **Block Adobe Reader from creating child processes**  
  [Reduce attack surfaces with attack surface reduction rules](https://go.microsoft.com/fwlink/?linkid=853979)  

  - **Not configured** - The Windows default is restored, is to not block creation of child processes.
  - **User defined**
  - **Enable** (*default*) - Adobe Reader is blocked from creating child processes.
  - **Audit mode** - Windows events are raised instead of blocking child processes.

- **Scan incoming email messages**  
  CSP: [Defender/AllowEmailScanning](https://go.microsoft.com/fwlink/?linkid=2114052&clcid=0x409)

  - **Yes** (*default*) - E-mail mailbox and mail files such as PST, DBX, MNX, MIME, and BINHEX are scanned.
  - **Not configured** - The setting returns to the client default of e-mail files not being scanned.

- **Turn on real-time protection**  
  CSP: [Defender/AllowRealtimeMonitoring](https://go.microsoft.com/fwlink/?linkid=2114050&clcid=0x409)

  - **Yes** (*default*) - Real-time monitoring is enforced and the user cannot disable it.
  - **Not configured** - The setting is returned to client default, which is on, but the user can change it. To disable real-time monitoring, use a custom URI.

- **Number of days (0-90) to keep quarantined malware**  
  CSP: [Defender/DaysToRetainCleanedMalware](https://go.microsoft.com/fwlink/?linkid=2114055&clcid=0x409)

  Configure the number of days items should be kept in the quarantine folder before being removed. The default is zero (**0**), which results in quarantined files never being removed.

- **Defender system scan schedule**  
  CSP: [Defender/ScheduleScanDay](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-schedulescanday)

  Schedule on which day Defender scans devices. By default the scan is **User defined** but can be set to *Everyday*, any day of the week, or to have *No scheduled scan*.

- **Additional amount of time (0-50 seconds) to extend cloud protection timeout**  
  CSP: [Defender/CloudExtendedTimeout](https://go.microsoft.com/fwlink/?linkid=2113940&clcid=0x409)

  Defender Antivirus automatically blocks suspicious files for 10 seconds so it can scan the files in the cloud to make sure they're safe. With this setting, you can add up to 50 additional seconds to this timeout.  By default, the timeout is set to zero (**0**).

- **Scan mapped network drives during a full scan**  
  CSP: [Defender/AllowFullScanOnMappedNetworkDrives](https://go.microsoft.com/fwlink/?linkid=2113945&clcid=0x409)

  - **Yes** (*default*) - During a full scan, mapped network drives are included.
  - **Not configured** - The client returns to its default, which disables scanning on mapped network drives.

- **Turn on network protection**  
  CSP: [Defender/EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=2113939&clcid=0x409)
  
  - **Yes** (*default*) - Block malicious traffic detected by signatures in the Network Inspection System (NIS).
  - **Not configured**

- **Scan all downloaded files and attachments**  
  CSP: [Defender/AllowIOAVProtection](https://go.microsoft.com/fwlink/?linkid=2113934&clcid=0x409)

  - **Yes** (*default*) - All downloaded files and attachments are scanned. The setting is returned to client default, which is on, but the user can change it. To disable this setting, use a custom URI.
  - **Not configured** - The setting is returned to client default, which is on, but the user can change it. To disable this setting, use a custom URI.

::: zone-end
::: zone pivot="atp-april-2020"

- **Block on access protection**  
  CSP: [Defender/AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935&clcid=0x409)

  - **Yes**
  - **Not configured** (*default*)

::: zone-end
::: zone pivot="atp-march-2020"

- **Block on access protection**  
  CSP: [Defender/AllowOnAccessProtection](https://go.microsoft.com/fwlink/?linkid=2113935&clcid=0x409)

  - **Yes** (*default*)
  - **Not configured**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

- **Scan browser scripts**  
  CSP: [Defender/AllowScriptScanning](https://go.microsoft.com/fwlink/?linkid=2114054&clcid=0x409)

  - **Yes** (*default*) - The Microsoft Defender Script Scanning functionality is enforced and the user cannot turn them off.
  - **Not configured** -  The setting is returned to client default, which is to enable script scanning, however the user can turn it off.

- **Block user access to Microsoft Defender app**  
  CSP: [Defender/AllowUserUIAccess](https://go.microsoft.com/fwlink/?linkid=2114043&clcid=0x409)

  - **Yes** (*default*) - The Microsoft Defender User Interface (UI) is inaccessible and notifications are surprised
  - **Not configured**
 When set to Yes, the Windows Defender User Interface (UI) will be inaccessible and notifications will be surprised. When set to Not configured, the setting will return to client default in which UI and notifications will be allowed

- **Maximum allowed CPU usage (0-100 percent) per scan**  
  CSP: [Defender/AvgCPULoadFactor](https://go.microsoft.com/fwlink/?linkid=2114046&clcid=0x409)

  Specify as a percentage the maximum amount of CPU to use for a scan. The default is **50**.

- **Scan type**  
  CSP: [Defender/ScanParameter](https://go.microsoft.com/fwlink/?linkid=2114045&clcid=0x409)

  - **User defined**
  - **Disabled**
  - **Quick scan** (*default*)
  - **Full scan**

- **Enter how often (0-24 hours) to check for security intelligence updates**  
  CSP: [Defender/SignatureUpdateInterval](https://go.microsoft.com/fwlink/?linkid=2113936&clcid=0x409)

  Specify how often to check for updated signatures, in hours. For example, a value of 1 will check each hour. A value of 2 will check every two hours, and so on.

  If no value is defined, devices use the client default of **8** hours.

- **Defender sample submission consent**  
  CSP: [Defender/SubmitSamplesConsent](https://go.microsoft.com/fwlink/?linkid=2067131)

  Checks for the user consent level in Microsoft Defender to send data. If the required consent has already been granted, Microsoft Defender submits them. If not (and if the user has specified never to ask), the UI is launched to ask for user consent (when *Cloud-delivered protection* is set to *Yes*) before sending data.

  - **Send safe samples automatically** (*default*)
  - **Always prompt**
  - **Never send**
  - **Send all samples automatically**

- **Cloud-delivered protection level**  
  CSP: [CloudBlockLevel](https://go.microsoft.com/fwlink/?linkid=2113942)

  Configure how aggressive Defender Antivirus is in blocking and scanning suspicious files.
  - **Not configured** (*default*) - Default Defender blocking level.
  - **High** - Aggressively block unknowns while optimizing client performance, which includes a greater chance of false positives.
  - **High plus** - Aggressively block unknowns and apply additional protection measures that might impact client performance.
  - **Zero tolerance** - Block all unknown executable files.

- **Scan archive files**  
  CSP: [Defender/AllowArchiveScanning](https://go.microsoft.com/fwlink/?linkid=2114047&clcid=0x409)

  - **Yes** (*default*) - Scanning of archive files such as ZIP or CAB files is enforced.
  - **Not configured** - The setting will be returned back to client default, which is to scan archived files, however the user may disable scanning.

- **Turn on behavior monitoring**  
  CSP: [Defender/AllowBehaviorMonitoring](https://go.microsoft.com/fwlink/?linkid=2114048&clcid=0x409)

  - **Yes** (*default*) - Behavior monitoring is enforced and the user cannot disable it.
  - **Not configured** - The setting is returned to client default, which is on, but the user can change it. To disable real-time monitoring, use a custom URI.
  
- **Scan removable drives during full scan**  
  CSP: [Defender/AllowFullScanRemovableDriveScanning](https://go.microsoft.com/fwlink/?linkid=2113946&clcid=0x409)

  - **Yes** (*default*) - During a full scan, removable drives (like USB flash drives) are scanned.
  - **Not configured** - The setting returns to client default, which scans removable drives, however the user can disable this scan.
  
- **Scan network files**  
  CSP: [Defender/AllowScanningNetworkFiles](https://go.microsoft.com/fwlink/?linkid=2114049&clcid=0x409)

  - **Yes** (*default*) - Microsoft Defender scans network files.
  - **Not configured** - The client returns to its default, which disables scanning of network files.
  
- **Defender potentially unwanted app action**  
  CSP: [Defender/PUAProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)

  Specify the level of detection for potentially unwanted applications (PUAs). Defender alerts users when potentially unwanted software is being downloaded or attempts to install on a device.
  - **Device default**
  - **Block** (*default*) - Detected items are blocked, and show in history along with other threats.
  - **Audit** - Defender detects potentially unwanted applications, but takes no action. You can review information about the applications Defender would have taken action against by searching for events that are created by Defender in the Event Viewer.

- **Turn on cloud-delivered protection**  
  CSP: [AllowCloudProtection](https://docs.microsoft.com/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  By default, Defender on Windows 10 desktop devices sends information to Microsoft about any problems it finds. Microsoft analyzes that information to learn more about problems affecting you and other customers, to offer improved solutions.

  - **Yes** (*default*) - Cloud-delivered protection is turned on.  Device users can't change this setting.
  - **Not configured**  - The setting is restored to the system default.

- **Block Office applications from injecting code into other processes**  
  [Protect devices from exploits](https://go.microsoft.com/fwlink/?linkid=872974)

  This ASR rule is controlled via the following GUID: 75668C1F-73B5-4CF0-BB93-3ECF5CB7CC84
  - **Not configured** - The setting returns to the Windows default, which is off.
  - **Block** (*default*) - Office applications are blocked from injecting code into other processes.
  - **Audit mode** - Windows events are raised instead of blocking.

- **Block Office applications from creating executable content**  
  [Protect devices from exploits](https://go.microsoft.com/fwlink/?linkid=872975)

  This ASR rule is controlled via the following GUID: 3B576869-A4EC-4529-8536-B80A7769E899
  - **Not configured** - The setting returns to the Windows default, which is off.
  - **Block** (*default*) - Office applications are blocked from create executable content.
  - **Audit mode** - Windows events are raised instead of blocking.
  
- **Block JavaScript or VBScript from launching downloaded executable content**  
  [Protect devices from exploits](https://go.microsoft.com/fwlink/?linkid=872979)

   This ASR rule is controlled via the following GUID: D3E037E1-3EB8-44C8-A917-57927947596D
  - **Not configured** - The setting returns to the Windows default, which is off.
  - **Block** (*default*) - Defender blocks JavaScript or VBScript files that have been downloaded from the Internet from being executed.
  - **Audit mode** - Windows events are raised instead of blocking.
  
- **Enable network protection**  
  CSP: [Defender/EnableNetworkProtection](https://go.microsoft.com/fwlink/?linkid=872618)

  - **Not configured** -The setting returns to the Windows default, which is disabled.
  - **User defined**
  - **Enable** - Network protection is enabled for all users on the system.
  - **Audit mode** (*default*) - Users aren't blocked from dangerous domains and Windows events are raised instead.

- **Block untrusted and unsigned processes that run from USB**  
  [Protect devices from exploits](https://go.microsoft.com/fwlink/?linkid=874502)

  This ASR rule is controlled via the following GUID: b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4
  - **Not configured** - The setting returns to the Windows default, which is off.
  - **Block** (*default*) - Untrusted and unsigned processes that run from a USB drive are blocked.
  - **Audit mode** - Windows events are raised instead of blocking.

- **Block credential stealing from the Windows local security authority subsystem (lsass.exe)**  
  [Protect devices from exploits](https://go.microsoft.com/fwlink/?linkid=874499)

  This ASR rule is controlled via the following GUID: 9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2
  - **Not configured** -The setting returns to the Windows default, which is off.
  - **User defined**
  - **Enable** (*default*) - Attempts to steal credentials via lsass.exe are blocked.
  - **Audit mode** - Users aren't blocked from dangerous domains and Windows events are raised instead.

- **Block executable content download from email and webmail clients**  
  [Protect devices from exploits](https://go.microsoft.com/fwlink/?linkid=872980)

  - **Not configured** - The setting returns to the Windows default, which is off.
  - **Block** (*default*) - Executable content downloaded from email and webmail clients is blocked.
  - **Audit mode** - Windows events are raised instead of blocking.

- **Block all Office applications from creating child processes**  
  [Protect devices from exploits](https://go.microsoft.com/fwlink/?linkid=872976)

  This ASR rule is controlled via the following GUID: D4F940AB-401B-4EFC-AADC-AD5F3C50688A
  - **Not configured** - The setting returns to the Windows default, which is off.
  - **Block** (*default*)
  - **Audit mode** - Windows events are raised instead of blocking.

- **Block execution of potentially obfuscated scripts (js/vbs/ps)**  
  [Protect devices from exploits](https://go.microsoft.com/fwlink/?linkid=872978)

  This ASR rule is controlled via the following GUID: 5BEB7EFE-FD9A-4556-801D-275E5FFC04CC
  - **Not configured** - The setting returns to the Windows default, which is off.
  - **Block** (*default*) - Defender will block execution of obfuscated scripts.
  - **Audit mode** - Windows events are raised instead of blocking.

- **Block Win32 API calls from Office macro**  
  [Protect devices from exploits](https://go.microsoft.com/fwlink/?linkid=872977)

  This ASR rule is controlled via the following GUID: 92E97FA1-2EDF-4476-BDD6-9DD0B4DDDC7B
  - **Not configured** - The setting returns to the Windows default, which is off.
  - **Block** (*default*) - Office macro's will be blocked from using Win32 API calls.
  - **Audit mode** - Windows events are raised instead of blocking.

## Microsoft Defender Security Center

- **Block users from editing the Exploit Guard protection interface**  
  CSP: [WindowsDefenderSecurityCenter/DisallowExploitProtectionOverride](https://go.microsoft.com/fwlink/?linkid=2067239)

  - **Yes** (*default*) -  Prevent users from making changes to the exploit protection settings area in the Microsoft Defender Security Center.
  - **Not configured** - Local users can make changes in the exploit protection settings area.

## Smart Screen

- **Block users from ignoring SmartScreen warnings**  
  CSP: [SmartScreen/PreventOverrideForFilesInShell](https://go.microsoft.com/fwlink/?linkid=872783)

   This setting requires the 'Enforce SmartScreen for apps and files' setting be enabled.
  - **Yes** (*default*) - SmartScreen will not present an option for the user to disregard the warning and run the app. The warning will be presented, but the user will be able to bypass it.
  - **Not configured** - Returns the setting to the Windows default, which allows the user override.

- **Require apps from store only**  

  - **Yes** (*default*)
  - **Not configured**

- **Turn on Windows SmartScreen**  
  CSP: [SmartScreen/EnableSmartScreenInShell](https://go.microsoft.com/fwlink/?linkid=872784)

  - **Yes** (*default*) - Enforce the use of SmartScreen for all users.
  - **Not configured** - Return the setting to Windows default, which is to enable SmartScreen, however users may change this setting. To disable SmartScreen, use a custom URI.

## Windows Hello for Business

For more information, see [PassportForWork CSP](https://docs.microsoft.com/windows/client-management/mdm/passportforwork-csp) in the Windows documentation.

- **Block Windows Hello for Business**  

   Windows Hello for Business is an alternative method for signing into Windows by replacing passwords, Smart Cards, and Virtual Smart Cards.

  - **Not configured** - Devices device provision Windows Hello for Business, which is the Windows default.
  - **Disabled** (*default*) - Devices provision Windows Hello for Business.
  - **Enabled** - Devices do not provision Windows Hello for Business for any user.

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
- [Troubleshoot policies and profiles in Intune](../configuration/troubleshoot-policies-in-microsoft-intune.md)