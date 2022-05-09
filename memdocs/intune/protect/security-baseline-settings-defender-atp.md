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

# List of the settings in the Microsoft Defender for Endpoint security baseline in Intune
This article is a reference for the settings that are available in the different versions of the Microsoft Defender for Endpoint security baseline that you can deploy with Microsoft Intune. You can use the tabs below to select and view the settings in the current baseline version and a few older versions that might still be in use.

For each setting you’ll find the baselines default configuration, which is also the recommended configuration for that setting provided by the relevant security team. Because products and the security landscape evolve, the recommended defaults in one baseline version might not match the defaults you find in later versions of the same baseline. Different baseline types, like the *MDM security* and the *Defender for Endpoint* baselines, could also set different defaults.

When the Intune UI includes a *Learn more* link for a setting, you’ll find that here as well. Use that link to view the settings *policy configuration service provider* (CSP) or relevant content that explains the settings operation.

When a new version of a baseline becomes available, it replaces the previous version. Profiles instances that you’ve created prior to the availability of a new version:

- Become read-only. You can continue to use those profiles but can't edit them to change their configuration.
- Can be updated to the latest version. After you update a profile to the current baseline version, you can edit the profile to modify settings.

To learn more about using security baselines, see [Use security baselines](security-baselines.md). In that article you'll also find information about how to:

- [Compare baselines](../protect/security-baselines.md#compare-baseline-versions) to discover what's changed from version to version.
- [Change the baseline version for a profile](../protect/security-baselines-configure.md#change-the-baseline-version-for-a-profile) to update a profile to use the latest version of that baseline.

::: zone pivot="atp-december-2020"
**Microsoft Defender for Endpoint baseline for December 2020 - version 6**  
::: zone-end

::: zone pivot="atp-sept-2020"
**Microsoft Defender for Endpoint baseline for September 2020 - version 5**  
::: zone-end

::: zone pivot="atp-april-2020"
**Microsoft Defender for Endpoint baseline for April 2020 - version 4**  
::: zone-end

<!-- OLD >
::: zone pivot="atp-march-2020"
**Microsoft Defender for Endpoint baseline for March 2020 - version 3**  
::: zone-end
-->

The Microsoft Defender for Endpoint  baseline is available when your environment meets the prerequisites for using [Microsoft Defender for Endpoint](advanced-threat-protection.md#prerequisites).

This baseline is optimized for physical devices and isn't recommended for use on virtual machines (VMs) or VDI endpoints. Certain baseline settings can impact remote interactive sessions on virtualized environments. For more information, see [Increase compliance to the Microsoft Defender for Endpoint security baseline](/windows/security/threat-protection/microsoft-defender-atp/configure-machines-security-baseline) in the Windows documentation.

## Understand the merge behavior for Attack Surface Reduction Rules in Intune

Attack surface reduction rules support a merger of settings from different policies, to create a superset of policy for each device. Only the settings that are not in conflict are merged, while those that are in conflict are not added to the superset of rules. Previously, if two policies included conflicts for a single setting, both policies were flagged as being in conflict, and no settings from either profile would be deployed.

Attack surface reduction rule merge behavior is as follows:  

- Attack surface reduction rules from the following profiles are evaluated for each device the rules apply to:  
  - Devices > Configuration policy > Endpoint protection profile > Microsoft Defender Exploit Guard > **Attack Surface Reduction**
  - Endpoint security > Attack surface reduction policy > **Attack surface reduction rules**
  - Endpoint security > Security baselines > Microsoft Defender for Endpoint Baseline > **Attack Surface Reduction Rules**.
- Settings that do not have conflicts are added to a superset of policy for the device.
- When two or more policies have conflicting settings, the conflicting settings are not added to the combined policy, while settings that don’t conflict are added to the superset policy that applies to a device.
- Only the configurations for conflicting settings are held back.

## Attack Surface Reduction Rules

To learn more, see [Attack surface reduction rules](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction) in the Microsoft Defender for Endpoint documentation.

::: zone pivot="atp-sept-2020,atp-december-2020"

- **Block Office communication apps from creating child processes**  
  Baseline default: *Enable*
  [Learn more](https://go.microsoft.com/fwlink/?linkid=874499 )

- **Block Adobe Reader from creating child processes**  
  Baseline default: *Enable*
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

- **Block Office applications from injecting code into other processes**  
  Baseline default: *Block*  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

- **Block Office applications from creating executable content**  
  Baseline default: *Block*  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

- **Block JavaScript or VBScript from launching downloaded executable content**  
  Baseline default: *Block*  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

- **Enable network protection**  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=3D872618)

- **Block untrusted and unsigned processes that run from USB**  
  Baseline default: *Block*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=)

- **Block credential stealing from the Windows local security authority subsystem (lsass.exe)**  
  Baseline default: *Enable*  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

- **Block executable content download from email and webmail clients**  
  Baseline default: *Block*  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

- **Block all Office applications from creating child processes**  
  Baseline default: *Block*  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)


- **Block execution of potentially obfuscated scripts (js/vbs/ps)**  
  Baseline default: *Block*  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

- **Block Win32 API calls from Office macro**  
  Baseline default: *Block*  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

::: zone-end

<!-- Application Guard was removed as a category beginning with the September 2020 version -->

::: zone pivot="atp-march-2020,atp-april-2020"

## Application Guard

For more information, see [WindowsDefenderApplicationGuard CSP](/windows/client-management/mdm/windowsdefenderapplicationguard-csp) in the Windows documentation.  

When you use Microsoft Edge, Microsoft Defender Application Guard protects your environment from sites that aren't trusted by your organization. When users visit sites that aren't listed in your isolated network boundary, the sites open in a Hyper-V virtual browsing session. Trusted sites are defined by a network boundary.  

- **Turn on Application Guard for Edge (Options)**  
  Baseline default: *Enabled for Edge*  
  [Learn more](/windows/client-management/mdm/windowsdefenderapplicationguard-csp#allowwindowsdefenderapplicationguard)
  
  - **Block external content from non-enterprise approved sites**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/windowsdefenderapplicationguard-csp#blocknonenterprisecontent)

  - **Clipboard behavior**  
  Baseline default: *Block copy and paste between PC and browser*  
  [Learn more](/windows/client-management/mdm/windowsdefenderapplicationguard-csp#clipboardsettings)

- **Windows network isolation policy**  
  Baseline default: *Configure*  
  [Learn more](/windows/client-management/mdm/policy-csp-networkisolation)

  - **Network domains**  
    Baseline default: *securitycenter.windows.com*

::: zone-end

## BitLocker

For more information, [BitLocker Group Policy settings](/windows/security/information-protection/bitlocker/bitlocker-group-policy-settings) in the Windows documentation.

::: zone pivot="atp-march-2020,atp-april-2020"

- **Require storage cards to be encrypted (mobile only)**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/bitlocker-csp#requirestoragecardencryption)

  > [!NOTE]
  > Support for [Windows 10 Mobile](https://support.microsoft.com/help/4485197/windows-10-mobile-end-of-support-faq) and [Windows Phone 8.1](https://support.microsoft.com/help/4036480/windows-phone-8-1-end-of-support-faq) ended in August of 2020.

::: zone-end

::: zone pivot="atp-sept-2020,atp-december-2020"

- **Standby states when sleeping while on battery**
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-power#power-standbytimeoutonbattery)

- **Standby states when sleeping while plugged in**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-power#power-standbytimeoutpluggedin)

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020,atp-december-2020"

- **Enable full disk encryption for OS and fixed data drives**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/bitlocker-csp#requiredeviceencryption)

 
- **BitLocker system drive policy**  
  Baseline default: *Configure*  
  [Learn more](/windows/security/information-protection/bitlocker/bitlocker-group-policy-settings)

::: zone-end
::: zone pivot="atp-sept-2020,atp-december-2020"

  - **Startup authentication required**  
    Baseline default: *Yes*  
    [Learn more](/windows/client-management/mdm/bitlocker-csp#systemdrivesrequirestartupauthentication)

  - **Compatible TPM startup PIN**  
    Baseline default: *Allowed*  
    [Learn more](/windows/client-management/mdm/bitlocker-csp#systemdrivesrequirestartupauthentication)

  - **Compatible TPM startup key**  
    Baseline default: *Required*  
    [Learn more](/windows/client-management/mdm/bitlocker-csp#systemdrivesrequirestartupauthentication)

  - **Disable BitLocker on devices where TPM is incompatible**  
    Baseline default: *Yes*  
    [Learn more](/windows/client-management/mdm/bitlocker-csp#systemdrivesrequirestartupauthentication)

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020,atp-december-2020"

  - **Configure encryption method for Operating System drives**  
    Baseline default: *Not configured*  
    [Learn more](/windows/client-management/mdm/bitlocker-csp#encryptionmethodbydrivetype)  
    This setting is available when *BitLocker system drive policy* is set to *Configure*.  

- **BitLocker fixed drive policy**  
  Baseline default: *Configure*  
  [Learn more](/windows/security/information-protection/bitlocker/bitlocker-group-policy-settings)

  - **Block write access to fixed data-drives not protected by BitLocker**  
    Baseline default: *Yes*  
    [Learn more](/windows/client-management/mdm/bitlocker-csp#fixeddrivesrequireencryption)  
    This setting is available when *BitLocker fixed drive policy* is set to *Configure*.

  - **Configure encryption method for fixed data-drives**  
    Baseline default: *AES 128bit XTS*  
    [Learn more](/windows/client-management/mdm/bitlocker-csp#encryptionmethodbydrivetype)  

- **BitLocker removable drive policy**  
  Baseline default: *Configure*  
  [Learn more](/windows/security/information-protection/bitlocker/bitlocker-group-policy-settings)

  - **Configure encryption method for removable data-drives**  
    Baseline default: *AES 128bit CBC*  
    [Learn more](/windows/client-management/mdm/bitlocker-csp#encryptionmethodbydrivetype)  

  - **Block write access to removable data-drives not protected by BitLocker**  
    Baseline default: *Not configured*  
    [Learn more](/windows/client-management/mdm/bitlocker-csp#removabledrivesrequireencryption)  

::: zone-end

<!-- Browser and Data Protection are removed as categories beginning with the September 2020 version -->

::: zone pivot="atp-march-2020,atp-april-2020"

## Browser

- **Require SmartScreen for Microsoft Edge**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

- **Block malicious site access**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)  

- **Block unverified file download**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)  

## Data Protection

- **Block direct memory access**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-dataprotection#dataprotection-allowdirectmemoryaccess)  

::: zone-end

::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020,atp-december-2020"

## Device Guard  

- **Turn on credential guard**  
  Baseline default: *Enable with UEFI lock*  
  [Learn more](/windows/client-management/mdm/policy-csp-deviceguard)

## Device Installation

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

- **Hardware device installation by device identifiers**  
  Baseline default: *Block hardware device installation*  
  [Learn more](/windows/client-management/mdm/policy-csp-deviceinstallation#deviceinstallation-allowinstallationofmatchingdeviceids)

  - **Remove matching hardware devices**
    Baseline default: *Yes*  
  
  - **Hardware device identifiers that are blocked**  
    Baseline default: *Not configured by default. Manually add one or more device identifiers.*

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020"

- **Hardware device installation by setup classes**  
  Baseline default: *Block hardware device installation*  
  [Learn more](/windows/client-management/mdm/policy-csp-deviceinstallation#deviceinstallation-allowinstallationofmatchingdevicesetupclasses)  


  - **Remove matching hardware devices**
    Baseline default: *Not configured*

  - **Hardware device identifiers that are blocked**
    Baseline default: *Not configured by default. Manually add one or more device identifiers.*

::: zone-end
::: zone pivot="atp-december-2020"

- **Block hardware device installation by setup classes**:  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-deviceinstallation#deviceinstallation-allowinstallationofmatchingdevicesetupclassess)

  - **Remove matching hardware devices**:  
    Baseline default: *Yes*  
  
  - **Block list**
    Baseline default: *Not configured by default. Manually add one or more setup class globally unique identifiers.

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020,atp-december-2020"



<!-- CONTINUE HERE! -->


## DMA Guard

- **Enumeration of external devices incompatible with Kernel DMA Protection**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy)

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
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/windowsadvancedthreatprotection-csp)

  Returns or sets the Microsoft Defender for Endpoint Sample Sharing configuration parameter.
  
  - **Yes** (*default*)
  - **Not configured**

- **Expedite telemetry reporting frequency**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/windowsadvancedthreatprotection-csp)

  Expedite Microsoft Defender for Endpoint telemetry reporting frequency.  

  - **Yes** (*default*)
  - **Not configured**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020,atp-december-2020"

## Firewall

For more information, see [Firewall CSP](/windows/client-management/mdm/firewall-csp) in the Windows documentation.

- **Stateful File Transfer Protocol (FTP)**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/firewall-csp#disablestatefulftp)  

  - **Disabled** (*default*) - Stateful FTP is disabled.
  - **Allow** - The firewall performs stateful File Transfer Protocol (FTP) filtering to allow secondary connections. Disabled
  - **Not configured**

- **Number of seconds a security association can be idle before it's deleted**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/firewall-csp#saidletime)

  Specify how long the security associations are kept after network traffic is no longer seen. When not configured, the system deletes a security association after it's been idle for *300* seconds (the default).
  
  The number must be from **300** to **3600** seconds.

- **Preshared key encoding**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/firewall-csp#presharedkeyencoding)

   If you don't require UTF-8, preshared keys will initially be encoded using UTF-8. After that, device users can choose another encoding method.

  - **Not configured**
  - **None**
  - **UTF8** (*default*)

- **Certificate revocation list (CRL) verification**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/firewall-csp#crlcheck)

  Specify how certificate revocation list (CRL) verification is enforced.  

  - **Not configured** (*default*) - CRL verification is disabled.
  - **None**
  - **Attempt**
  - **Require**

- **Packet queuing**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/firewall-csp#enablepacketqueue)

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
    Baseline default: **  
    [Learn more](/windows/client-management/mdm/firewall-csp#defaultinboundaction)

    - **Yes** (*default*)
    - **Not configured**

  - **Unicast responses to multicast broadcasts required**  
    Baseline default: **  
    [Learn more](/windows/client-management/mdm/firewall-csp#disableunicastresponsestomulticastbroadcast)

    - **Yes** (*default*)
    - **Not configured**

  - **Outbound connections required**  
    Baseline default: **  
    [Learn more](/windows/client-management/mdm/firewall-csp#defaultoutboundaction)

    - **Yes** (*default*)
    - **Not configured**

  - **Inbound notifications blocked**  
    Baseline default: **  
    [Learn more](/windows/client-management/mdm/firewall-csp#disableinboundnotifications)

    - **Yes** (*default*)
    - **Not configured**

  - **Global port rules from group policy merged**  
    Baseline default: **  
    [Learn more](/windows/client-management/mdm/firewall-csp#globalportsallowuserprefmerge)

    - **Yes** (*default*)
    - **Not configured**

  - **Firewall enabled**  
    Baseline default: **  
    [Learn more](/windows/client-management/mdm/firewall-csp#enablefirewall)

    - **Not configured**
    - **Blocked**
    - **Allowed** (*default*)

  - **Authorized application rules from group policy not merged**  
    Baseline default: **  
    [Learn more](/windows/client-management/mdm/firewall-csp#authappsallowuserprefmerge)

    - **Yes** (*default*)
    - **Not configured**

  - **Connection security rules from group policy not merged**  
    Baseline default: **  
    [Learn more](/windows/client-management/mdm/firewall-csp#allowlocalipsecpolicymerge)

    - **Yes** (*default*)
    - **Not configured**

  - **Incoming traffic required**  
    Baseline default: **  
    [Learn more](/windows/client-management/mdm/firewall-csp#shielded)

    - **Yes** (*default*)
    - **Not configured**

  - **Policy rules from group policy not merged**  
    Baseline default: **  
    [Learn more](/windows/client-management/mdm/firewall-csp#allowlocalpolicymerge)

    - **Yes** (*default*)
    - **Not configured**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

  - **Stealth mode blocked**  
    Baseline default: **  
    [Learn more](/windows/client-management/mdm/firewall-csp#disablestealthmode)

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
    Baseline default: **  
    [Learn more](/windows/client-management/mdm/firewall-csp#defaultinboundaction)

    - **Yes** (*default*)
    - **Not configured**

  - **Unicast responses to multicast broadcasts required**  
    Baseline default: **  
    [Learn more](/windows/client-management/mdm/firewall-csp#disableunicastresponsestomulticastbroadcast)

    - **Yes** (*default*)
    - **Not configured**

  - **Outbound connections required**  
    Baseline default: **  
    [Learn more](/windows/client-management/mdm/firewall-csp#defaultoutboundaction)

    - **Yes** (*default*)
    - **Not configured**

  - **Authorized application rules from group policy not merged**  
    Baseline default: **  
    [Learn more](/windows/client-management/mdm/firewall-csp#authappsallowuserprefmerge)

    - **Yes** (*default*)
    - **Not configured**

  - **Inbound notifications blocked**  
    Baseline default: **  
    [Learn more](/windows/client-management/mdm/firewall-csp#disableinboundnotifications)

    - **Yes** (*default*)
    - **Not configured**

  - **Global port rules from group policy merged**  
    Baseline default: **  
    [Learn more](/windows/client-management/mdm/firewall-csp#globalportsallowuserprefmerge)

    - **Yes** (*default*)
    - **Not configured**

  - **Firewall enabled**  
    Baseline default: **  
    [Learn more](/windows/client-management/mdm/firewall-csp#enablefirewall)

    - **Not configured**
    - **Blocked**
    - **Allowed** (*default*)

  - **Connection security rules from group policy not merged**  
    Baseline default: **  
    [Learn more](/windows/client-management/mdm/firewall-csp#allowlocalipsecpolicymerge)

    - **Yes** (*default*)
    - **Not configured**

  - **Incoming traffic required**  
    Baseline default: **  
    [Learn more](/windows/client-management/mdm/firewall-csp#shielded)

    - **Yes** (*default*)
    - **Not configured**

  - **Policy rules from group policy not merged**  
    Baseline default: **  
    [Learn more](/windows/client-management/mdm/firewall-csp#allowlocalpolicymerge)

    - **Yes** (*default*)
    - **Not configured**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

  - **Stealth mode blocked**  
    Baseline default: **  
    [Learn more](/windows/client-management/mdm/firewall-csp#disablestealthmode)

    - **Yes** (*default*)
    - **Not configured**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020,atp-december-2020"

- **Firewall profile domain**  
  CSP: [2.2.2 FW_PROFILE_TYPE](/openspecs/windows_protocols/ms-fasp/7704e238-174d-4a5e-b809-5f3787dd8acc)

  - **Unicast responses to multicast broadcasts required**  
    Baseline default: **  
    [Learn more](/windows/client-management/mdm/firewall-csp#disableunicastresponsestomulticastbroadcast)

    - **Yes** (*default*)
    - **Not configured**

  - **Authorized application rules from group policy not merged**  
    Baseline default: **  
    [Learn more](/windows/client-management/mdm/firewall-csp#authappsallowuserprefmerge)

    - **Yes** (*default*)
    - **Not configured**  

  - **Inbound notifications blocked**  
    Baseline default: **  
    [Learn more](/windows/client-management/mdm/firewall-csp#disableinboundnotifications)

    - **Yes** (*default*)
    - **Not configured**

  - **Global port rules from group policy merged**  
    Baseline default: **  
    [Learn more](/windows/client-management/mdm/firewall-csp#globalportsallowuserprefmerge)

    - **Yes** (*default*)
    - **Not configured**

  - **Firewall enabled**  
    Baseline default: **  
    [Learn more](/windows/client-management/mdm/firewall-csp#enablefirewall)

    - **Not configured**
    - **Blocked**
    - **Allowed** (*default*)

  - **Connection security rules from group policy not merged**  
    Baseline default: **  
    [Learn more](/windows/client-management/mdm/firewall-csp#allowlocalipsecpolicymerge)

    - **Yes** (*default*)
    - **Not configured**

  - **Policy rules from group policy not merged**  
    Baseline default: **  
    [Learn more](/windows/client-management/mdm/firewall-csp#allowlocalpolicymerge)

    - **Yes** (*default*)
    - **Not configured**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

  - **Stealth mode blocked**  
    Baseline default: **  
    [Learn more](/windows/client-management/mdm/firewall-csp#disablestealthmode)

    - **Yes** (*default*)
    - **Not configured**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020,atp-december-2020"

## Microsoft Defender

::: zone-end
::: zone pivot="atp-sept-2020,atp-december-2020"

- **Turn on real-time protection**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

  - **Yes** (*default*) - Real-time monitoring is enforced and the user can't disable it.
  - **Not configured** - The setting is returned to client default, which is on, but the user can change it. To disable real-time monitoring, use a custom URI.

- **Additional amount of time (0-50 seconds) to extend cloud protection timeout**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-cloudextendedtimeout)

  Defender Antivirus automatically blocks suspicious files for 10 seconds so it can scan the files in the cloud to make sure they're safe. With this setting, you can add up to 50 additional seconds to this timeout.  By default, the timeout is set to zero (**0**).

- **Scan all downloaded files and attachments**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-defender)

  - **Yes** (*default*) - All downloaded files and attachments are scanned. The setting is returned to client default, which is on, but the user can change it. To disable this setting, use a custom URI.
  - **Not configured** - The setting is returned to client default, which is on, but the user can change it. To disable this setting, use a custom URI.

- **Scan type**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-scanparameter)

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
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-submitsamplesconsent)

  Checks for the user consent level in Microsoft Defender to send data. If the required consent has already been granted, Microsoft Defender submits them. If not (and if the user has specified never to ask), the UI launches to ask for user consent (when *Cloud-delivered protection* is set to *Yes*) before sending data.

  - **Send safe samples automatically** (*default*)
  - **Always prompt**
  - **Never send**
  - **Send all samples automatically**

- **Cloud-delivered protection level**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-cloudblocklevel)

  Configure how aggressive Defender Antivirus is in blocking and scanning suspicious files.
  - **Not configured** - Default Defender blocking level.
  - **High** *(default)* - Aggressively block unknowns while optimizing client performance, which includes a greater chance of false positives.
  - **High plus** - Aggressively block unknowns and apply additional protection measures that might impact client performance.
  - **Zero tolerance** - Block all unknown executable files.

- **Scan removable drives during full scan**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanremovabledrivescanning)

  - **Yes** (*default*) - During a full scan, removable drives (like USB flash drives) are scanned.
  - **Not configured** - The setting returns to client default, which scans removable drives, however the user can disable this scan.

- **Defender potentially unwanted app action**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)

  Specify the level of detection for potentially unwanted applications (PUAs). Defender alerts users when potentially unwanted software is being downloaded or attempts to install on a device.
  - **Device default**
  - **Block** (*default*) - Detected items are blocked, and show in history along with other threats.
  - **Audit** - Defender detects potentially unwanted applications, but takes no action. You can review information about the applications Defender would have taken action against by searching for events that are created by Defender in the Event Viewer.

- **Turn on cloud-delivered protection**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  By default, Defender on Windows 10/11 desktop devices sends information to Microsoft about any problems it finds. Microsoft analyzes that information to learn more about problems affecting you and other customers, to offer improved solutions.

  - **Yes** (*default*) - Cloud-delivered protection is turned on.  Device users can't change this setting.
  - **Not configured**  - The setting is restored to the system default.

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

- **Run daily quick scan at**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-schedulequickscantime)
  
   Configure when the daily quick scan runs. By default, the scan run is set to **2 AM**.

- **Scheduled scan start time**  
  
  By default, the start time is set to **2 AM**.

- **Configure low CPU priority for scheduled scans**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-enablelowcpupriority)  

  -**Yes** (*default*)
  - **Not configured**

- **Block Office communication apps from creating child processes**  
  Baseline default: **  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)  

  This ASR rule is controlled via the following GUID: 26190899-1602-49e8-8b27-eb1d0a1ce869.
  - **Not configured** - The Windows default is restored, which is to not block creation of child processes.
  - **User defined**
  - **Enable** (*default*) - Office communication applications are blocked from creating child processes.
  - **Audit mode** - Windows events are raised instead of blocking child processes.

- **Block Adobe Reader from creating child processes**  
  Baseline default: **  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)  

  - **Not configured** - The Windows default is restored, is to not block creation of child processes.
  - **User defined**
  - **Enable** (*default*) - Adobe Reader is blocked from creating child processes.
  - **Audit mode** - Windows events are raised instead of blocking child processes.

- **Scan incoming email messages**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-allowemailscanning)

  - **Yes** (*default*) - E-mail mailbox and mail files such as PST, DBX, MNX, MIME, and BINHEX are scanned.
  - **Not configured** - The setting returns to the client default of e-mail files not being scanned.

- **Turn on real-time protection**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-allowrealtimemonitoring)

  - **Yes** (*default*) - Real-time monitoring is enforced and the user can't disable it.
  - **Not configured** - The setting is returned to client default, which is on, but the user can change it. To disable real-time monitoring, use a custom URI.

- **Number of days (0-90) to keep quarantined malware**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-daystoretaincleanedmalware)

  Configure the number of days items should be kept in the quarantine folder before being removed. The default is zero (**0**), which results in quarantined files never being removed.

- **Defender system scan schedule**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-schedulescanday)

  Schedule on which day Defender scans devices. By default the scan is **User defined** but can be set to *Everyday*, any day of the week, or to have *No scheduled scan*.

- **Additional amount of time (0-50 seconds) to extend cloud protection timeout**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-cloudextendedtimeout)

  Defender Antivirus automatically blocks suspicious files for 10 seconds so it can scan the files in the cloud to make sure they're safe. With this setting, you can add up to 50 additional seconds to this timeout.  By default, the timeout is set to zero (**0**).

- **Scan mapped network drives during a full scan**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanonmappednetworkdrives)

  - **Yes** (*default*) - During a full scan, mapped network drives are included.
  - **Not configured** - The client returns to its default, which disables scanning on mapped network drives.

- **Turn on network protection**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)
  
  - **Yes** (*default*) - Block malicious traffic detected by signatures in the Network Inspection System (NIS).
  - **Not configured**

- **Scan all downloaded files and attachments**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-defender)

  - **Yes** (*default*) - All downloaded files and attachments are scanned. The setting is returned to client default, which is on, but the user can change it. To disable this setting, use a custom URI.
  - **Not configured** - The setting is returned to client default, which is on, but the user can change it. To disable this setting, use a custom URI.

::: zone-end
::: zone pivot="atp-april-2020"

- **Block on access protection**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-allowonaccessprotection)

  - **Yes**
  - **Not configured** (*default*)

::: zone-end
::: zone pivot="atp-march-2020"

- **Block on access protection**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-allowonaccessprotection)

  - **Yes** (*default*)
  - **Not configured**

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

- **Scan browser scripts**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-defender)

  - **Yes** (*default*) - The Microsoft Defender Script Scanning functionality is enforced and the user can't turn them off.
  - **Not configured** -  The setting is returned to client default, which is to enable script scanning, however the user can turn it off.

- **Block user access to Microsoft Defender app**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-allowuseruiaccess)

  - **Yes** (*default*) - The Microsoft Defender User Interface (UI) is inaccessible and notifications are surprised
  - **Not configured**
 When set to Yes, the Windows Defender User Interface (UI) will be inaccessible and notifications will be surprised. When set to Not configured, the setting will return to client default in which UI and notifications will be allowed

- **Maximum allowed CPU usage (0-100 percent) per scan**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-avgcpuloadfactor)

  Specify as a percentage the maximum amount of CPU to use for a scan. The default is **50**.

- **Scan type**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-scanparameter)

  - **User defined**
  - **Disabled**
  - **Quick scan** (*default*)
  - **Full scan**

- **Enter how often (0-24 hours) to check for security intelligence updates**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-defender)

  Specify how often to check for updated signatures, in hours. For example, a value of 1 will check each hour. A value of 2 will check every two hours, and so on.

  If no value is defined, devices use the client default of **8** hours.

- **Defender sample submission consent**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-submitsamplesconsent)

  Checks for the user consent level in Microsoft Defender to send data. If the required consent has already been granted, Microsoft Defender submits them. If not (and if the user has specified never to ask), the UI launches to ask for user consent (when *Cloud-delivered protection* is set to *Yes*) before sending data.

  - **Send safe samples automatically** (*default*)
  - **Always prompt**
  - **Never send**
  - **Send all samples automatically**

- **Cloud-delivered protection level**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-cloudblocklevel)

  Configure how aggressive Defender Antivirus is in blocking and scanning suspicious files.
  - **Not configured** (*default*) - Default Defender blocking level.
  - **High** - Aggressively block unknowns while optimizing client performance, which includes a greater chance of false positives.
  - **High plus** - Aggressively block unknowns and apply additional protection measures that might impact client performance.
  - **Zero tolerance** - Block all unknown executable files.

- **Scan archive files**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-allowarchivescanning)

  - **Yes** (*default*) - Scanning of archive files such as ZIP or CAB files is enforced.
  - **Not configured** - The setting will be returned back to client default, which is to scan archived files, however the user may disable scanning.

- **Turn on behavior monitoring**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-allowbehaviormonitoring)

  - **Yes** (*default*) - Behavior monitoring is enforced and the user can't disable it.
  - **Not configured** - The setting is returned to client default, which is on, but the user can change it. To disable real-time monitoring, use a custom URI.
  
- **Scan removable drives during full scan**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanremovabledrivescanning)

  - **Yes** (*default*) - During a full scan, removable drives (like USB flash drives) are scanned.
  - **Not configured** - The setting returns to client default, which scans removable drives, however the user can disable this scan.
  
- **Scan network files**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-allowscanningnetworkfiles)

  - **Yes** (*default*) - Microsoft Defender scans network files.
  - **Not configured** - The client returns to its default, which disables scanning of network files.

- **Defender potentially unwanted app action**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)

  Specify the level of detection for potentially unwanted applications (PUAs). Defender alerts users when potentially unwanted software is being downloaded or attempts to install on a device.
  - **Device default**
  - **Block** (*default*) - Detected items are blocked, and show in history along with other threats.
  - **Audit** - Defender detects potentially unwanted applications, but takes no action. You can review information about the applications Defender would have taken action against by searching for events that are created by Defender in the Event Viewer.

- **Turn on cloud-delivered protection**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-allowcloudprotection)

  By default, Defender on Windows 10/11 desktop devices sends information to Microsoft about any problems it finds. Microsoft analyzes that information to learn more about problems affecting you and other customers, to offer improved solutions.

  - **Yes** (*default*) - Cloud-delivered protection is turned on.  Device users can't change this setting.
  - **Not configured**  - The setting is restored to the system default.

- **Block Office applications from injecting code into other processes**  
  Baseline default: **  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  This ASR rule is controlled via the following GUID: 75668C1F-73B5-4CF0-BB93-3ECF5CB7CC84
  - **Not configured** - The setting returns to the Windows default, which is off.
  - **Block** (*default*) - Office applications are blocked from injecting code into other processes.
  - **Audit mode** - Windows events are raised instead of blocking.

- **Block Office applications from creating executable content**  
  Baseline default: **  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  This ASR rule is controlled via the following GUID: 3B576869-A4EC-4529-8536-B80A7769E899
  - **Not configured** - The setting returns to the Windows default, which is off.
  - **Block** (*default*) - Office applications are blocked from create executable content.
  - **Audit mode** - Windows events are raised instead of blocking.
  
- **Block JavaScript or VBScript from launching downloaded executable content**  
  Baseline default: **  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

   This ASR rule is controlled via the following GUID: D3E037E1-3EB8-44C8-A917-57927947596D
  - **Not configured** - The setting returns to the Windows default, which is off.
  - **Block** (*default*) - Defender blocks JavaScript or VBScript files that have been downloaded from the Internet from being executed.
  - **Audit mode** - Windows events are raised instead of blocking.
  
- **Enable network protection**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

  - **Not configured** - The setting returns to the Windows default, which is disabled.
  - **User defined**
  - **Enable** - Network protection is enabled for all users on the system.
  - **Audit mode** (*default*) - Users aren't blocked from dangerous domains and Windows events are raised instead.

- **Block untrusted and unsigned processes that run from USB**  
  Baseline default: **  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  This ASR rule is controlled via the following GUID: b2b3f03d-6a65-4f7b-a9c7-1c7ef74a9ba4
  - **Not configured** - The setting returns to the Windows default, which is off.
  - **Block** (*default*) - Untrusted and unsigned processes that run from a USB drive are blocked.
  - **Audit mode** - Windows events are raised instead of blocking.

- **Block credential stealing from the Windows local security authority subsystem (lsass.exe)**  
  Baseline default: **  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  This ASR rule is controlled via the following GUID: 9e6c4e1f-7d60-472f-ba1a-a39ef669e4b2
  - **Not configured** -The setting returns to the Windows default, which is off.
  - **User defined**
  - **Enable** (*default*) - Attempts to steal credentials via lsass.exe are blocked.
  - **Audit mode** - Users aren't blocked from dangerous domains and Windows events are raised instead.

- **Block executable content download from email and webmail clients**  
  Baseline default: **  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  - **Not configured** - The setting returns to the Windows default, which is off.
  - **Block** (*default*) - Executable content downloaded from email and webmail clients is blocked.
  - **Audit mode** - Windows events are raised instead of blocking.

- **Block all Office applications from creating child processes**  
  Baseline default: **  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  This ASR rule is controlled via the following GUID: D4F940AB-401B-4EFC-AADC-AD5F3C50688A
  - **Not configured** - The setting returns to the Windows default, which is off.
  - **Block** (*default*)
  - **Audit mode** - Windows events are raised instead of blocking.

- **Block execution of potentially obfuscated scripts (js/vbs/ps)**  
  Baseline default: **  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  This ASR rule is controlled via the following GUID: 5BEB7EFE-FD9A-4556-801D-275E5FFC04CC
  - **Not configured** - The setting returns to the Windows default, which is off.
  - **Block** (*default*) - Defender will block execution of obfuscated scripts.
  - **Audit mode** - Windows events are raised instead of blocking.

- **Block Win32 API calls from Office macro**  
  Baseline default: **  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

  This ASR rule is controlled via the following GUID: 92E97FA1-2EDF-4476-BDD6-9DD0B4DDDC7B
  - **Not configured** - The setting returns to the Windows default, which is off.
  - **Block** (*default*) - Office macro's will be blocked from using Win32 API calls.
  - **Audit mode** - Windows events are raised instead of blocking.

## Microsoft Defender Security Center

- **Block users from editing the Exploit Guard protection interface**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-disallowexploitprotectionoverride)

  - **Yes** (*default*) -  Prevent users from making changes to the exploit protection settings area in the Microsoft Defender Security Center.
  - **Not configured** - Local users can make changes in the exploit protection settings area.

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020,atp-december-2020"

## Smart Screen

::: zone-end
::: zone pivot="atp-sept-2020,atp-december-2020"

- **Block users from ignoring SmartScreen warnings**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-smartscreen#smartscreen-preventoverrideforfilesinshell)

   This setting requires the 'Turn on Windows SmartScreen' setting be set to Yes.
  - **Yes** (*default*) - SmartScreen is enabled and users can't bypass warnings for files or malicious apps.
  - **Not configured** - Users can ignore SmartScreen warnings for files and malicious apps.

- **Turn on Windows SmartScreen**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-smartscreen#smartscreen-enablesmartscreeninshell)

  - **Yes** (*default*) - Enforce the use of SmartScreen for all users.
  - **Not configured** - Return the setting to Windows default, which is to enable SmartScreen, however users may change this setting. To disable SmartScreen, use a custom URI.

- **Require SmartScreen for Microsoft Edge**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

  - **Yes** (*default*) - Enable Microsoft Edge SmartScreen for accessing site and file downloads.
  - **Not configured**

- **Block malicious site access**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)  

  - **Yes** (*default*) - Block users from ignoring the Microsoft Defender SmartScreen Filter warnings and block them from going to the site.
  - **Not configured**

- **Block unverified file download**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)  

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
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-smartscreen#smartscreen-preventoverrideforfilesinshell)

   This setting requires the 'Turn on Windows SmartScreen' setting be set to Yes.
  - **Yes** (*default*) - SmartScreen is enabled and users can't bypass warnings for files or malicious apps.
  - **Not configured** - Users can ignore SmartScreen warnings for files and malicious apps.

- **Require apps from store only**  

  - **Yes** (*default*)
  - **Not configured**

- **Turn on Windows SmartScreen**  
  Baseline default: **  
  [Learn more](/windows/client-management/mdm/policy-csp-smartscreen#smartscreen-enablesmartscreeninshell)

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
