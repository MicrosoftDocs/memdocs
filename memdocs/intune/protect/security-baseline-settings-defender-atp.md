---
# required metadata

title: Settings list for the Microsoft Defender for Endpoint security baseline in Microsoft Intune  
titleSuffix: Microsoft Intune
description: View a list of the settings in the Microsoft Intune security baseline for Microsoft Defender for Endpoint. This list includes the default values for settings as found in the default configuration of the baseline.
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/13/2022
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

<!-- Pivots and versions still in use: 

- December 2020 v6 > "atp-december-2020"
- September 2020 v5 > "atp-sept-2020"
- April 2020 v4 > "atp-april-2020"
- March 2020 v3 > "atp-march-2020"

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
::: zone pivot="atp-march-2020"
**Microsoft Defender for Endpoint baseline for March 2020 - version 3**  
::: zone-end

The Microsoft Defender for Endpoint  baseline is available when your environment meets the prerequisites for using [Microsoft Defender for Endpoint](advanced-threat-protection.md#prerequisites).

This baseline is optimized for physical devices and isn't recommended for use on virtual machines (VMs) or VDI endpoints. Certain baseline settings can affect remote interactive sessions on virtualized environments. For more information, see [Increase compliance to the Microsoft Defender for Endpoint security baseline](/windows/security/threat-protection/microsoft-defender-atp/configure-machines-security-baseline) in the Windows documentation.

::: zone pivot="atp-sept-2020,atp-december-2020"

## Attack Surface Reduction Rules

Attack surface reduction rules support a merger of settings from different policies, to create a superset of policy for each device. Only the settings that aren't in conflict are merged. Settings that are in conflict are not added to the superset of rules. Previously, if two policies included conflicts for a single setting, both policies were flagged as being in conflict, and no settings from either profile would be deployed.

Attack surface reduction rule merge behavior is as follows:  

- Attack surface reduction rules from the following profiles are evaluated for each device the rules apply to:  
  - Devices > Configuration policy > Endpoint protection profile > Microsoft Defender Exploit Guard > **Attack Surface Reduction**
  - Endpoint security > Attack surface reduction policy > **Attack surface reduction rules**
  - Endpoint security > Security baselines > Microsoft Defender for Endpoint Baseline > **Attack Surface Reduction Rules**.
- Settings that don't have conflicts are added to a superset of policy for the device.
- When two or more policies have conflicting settings, the conflicting settings aren't added to the combined policy, while settings that don’t conflict are added to the superset policy that applies to a device.
- Only the configurations for conflicting settings are held back.

To learn more, see [Attack surface reduction rules](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction) in the Microsoft Defender for Endpoint documentation.

- **Block Office communication apps from creating child processes**  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=874499)

- **Block Adobe Reader from creating child processes**  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=853979)

- **Block Office applications from injecting code into other processes**  
  Baseline default: *Block*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872974)

- **Block Office applications from creating executable content**  
  Baseline default: *Block*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872979)

- **Block JavaScript or VBScript from launching downloaded executable content**  
  Baseline default: *Block*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872979)

- **Enable network protection**  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872618)

- **Block untrusted and unsigned processes that run from USB**  
  Baseline default: *Block*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=874502)

- **Block credential stealing from the Windows local security authority subsystem (lsass.exe)**  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=874499)

- **Block executable content download from email and webmail clients**  
  Baseline default: *Block*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872980)

- **Block all Office applications from creating child processes**  
  Baseline default: *Block*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872976)

- **Block execution of potentially obfuscated scripts (js/vbs/ps)**  
  Baseline default: *Block*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872978)

- **Block Win32 API calls from Office macro**  
  Baseline default: *Block*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872977)

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

::: zone pivot="atp-march-2020,atp-april-2020" 
<!-- GOOD -->

- **Require storage cards to be encrypted (mobile only)**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/bitlocker-csp#requirestoragecardencryption)

  > [!NOTE]
  > Support for [Windows 10 Mobile](https://support.microsoft.com/help/4485197/windows-10-mobile-end-of-support-faq) and [Windows Phone 8.1](https://support.microsoft.com/help/4036480/windows-phone-8-1-end-of-support-faq) ended in August of 2020.

- **Enable full disk encryption for OS and fixed data drives**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/bitlocker-csp#requiredeviceencryption)

- **BitLocker system drive policy**  
  Baseline default: *Configure*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067025)  

  - **Configure encryption method for Operating System drives**  
    Baseline default: *Not configured*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872526)  

- **BitLocker fixed drive policy**  
  Baseline default: *Configure*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067018)

  - **Block write access to fixed data-drives not protected by BitLocker**  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872534)  
    This setting is available when *BitLocker fixed drive policy* is set to *Configure*.

  - **Configure encryption method for fixed data-drives**  
    Baseline default: *AES 128bit XTS*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872526)  

- **BitLocker removable drive policy**  
  Baseline default: *Configure*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067140)

  - **Configure encryption method for removable data-drives**  
    Baseline default: *AES 128bit CBC*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872526)  

  - **Block write access to removable data-drives not protected by BitLocker**  
    Baseline default: *Not configured*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872540)  

::: zone-end  
::: zone pivot="atp-sept-2020"

- **Standby states when sleeping while on battery**
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-power#power-standbytimeoutonbattery)

- **Standby states when sleeping while plugged in**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-power#power-standbytimeoutpluggedin)

- **Enable full disk encryption for OS and fixed data drives**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/bitlocker-csp#requiredeviceencryption)

- **BitLocker system drive policy**  
  Baseline default: *Configure*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067025)  

  - **Startup authentication required**  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872527)

  - **Compatible TPM startup PIN**  
    Baseline default: *Allowed*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872527)

  - **Compatible TPM startup key**  
    Baseline default: *Required*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872527)

  - **Disable BitLocker on devices where TPM is incompatible**  
    Baseline default: *Yes*  
    [Learn more](/windows/client-management/mdm/bitlocker-csp#systemdrivesrequirestartupauthentication)  


  - **Configure encryption method for Operating System drives**  
    Baseline default: *Not configured*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872526)  

- **BitLocker fixed drive policy**  
  Baseline default: *Configure*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067018)

  - **Block write access to fixed data-drives not protected by BitLocker**  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872534)  
    This setting is available when *BitLocker fixed drive policy* is set to *Configure*.

  - **Configure encryption method for fixed data-drives**  
    Baseline default: *AES 128bit XTS*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872526)  

- **BitLocker removable drive policy**  
  Baseline default: *Configure*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067140)

  - **Configure encryption method for removable data-drives**  
    Baseline default: *AES 128bit CBC*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872526)  

  - **Block write access to removable data-drives not protected by BitLocker**  
    Baseline default: *Not configured*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872540)  

::: zone-end  
::: zone pivot="atp-december-2020"

- **BitLocker system drive policy**  
  Baseline default: *Configure*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067025)  

  - **Startup authentication required**  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872527)

  - **Compatible TPM startup PIN**  
    Baseline default: *Allowed*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872527)

  - **Compatible TPM startup key**  
    Baseline default: *Required*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872527)

  - **Disable BitLocker on devices where TPM is incompatible**  
    Baseline default: *Yes*  
    [Learn more](/windows/client-management/mdm/bitlocker-csp#systemdrivesrequirestartupauthentication)  

  - **Configure encryption method for Operating System drives**  
    Baseline default: *Not configured*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872526)  

- **Standby states when sleeping while on battery**
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-power#power-standbytimeoutonbattery)

- **Standby states when sleeping while plugged in**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-power#power-standbytimeoutpluggedin)

- **Enable full disk encryption for OS and fixed data drives**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/bitlocker-csp#requiredeviceencryption)

- **BitLocker fixed drive policy**  
  Baseline default: *Configure*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067018)

  - **Block write access to fixed data-drives not protected by BitLocker**  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872534)  
    This setting is available when *BitLocker fixed drive policy* is set to *Configure*.

  - **Configure encryption method for fixed data-drives**  
    Baseline default: *AES 128bit XTS*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872526)  

- **BitLocker removable drive policy**  
  Baseline default: *Configure*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067140)

  - **Configure encryption method for removable data-drives**  
    Baseline default: *AES 128bit CBC*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872526)  

  - **Block write access to removable data-drives not protected by BitLocker**  
    Baseline default: *Not configured*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872540)  

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
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872424)

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
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067048)

  - **Remove matching hardware devices**:  
    Baseline default: *Yes*  
  
  - **Block list**  
    Baseline default: *Not configured by default. Manually add one or more setup class globally unique identifiers.*

::: zone-end

## DMA Guard

::: zone pivot="atp-sept-2020,atp-december-2020"

- **Enumeration of external devices incompatible with Kernel DMA Protection**  
  Baseline default: *Block all*  
  [Learn more](/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy)

::: zone-end  
::: zone pivot="atp-march-2020,atp-april-2020"

- **Enumeration of external devices incompatible with Kernel DMA Protection**  
  Baseline default: *Not configured*  
  [Learn more](/windows/client-management/mdm/policy-csp-dmaguard#dmaguard-deviceenumerationpolicy)

::: zone-end
::: zone pivot="atp-march-2020,atp-april-2020"

<!-- Endpoint Detection and Response is removed as categories beginning with the September 2020 version -->

## Endpoint Detection and Response

- **Sample sharing for all files**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/windowsadvancedthreatprotection-csp)

- **Expedite telemetry reporting frequency**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/windowsadvancedthreatprotection-csp)

::: zone-end

## Firewall

::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020,atp-december-2020"

- **Stateful File Transfer Protocol (FTP)**  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872536)  

- **Number of seconds a security association can be idle before it's deleted**  
  Baseline default: *300*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872539)

- **Preshared key encoding**  
  Baseline default: *UTF8*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872541)

- **Certificate revocation list (CRL) verification**  
  Baseline default: *Not configured*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872548)

- **Packet queuing**  
  Baseline default: *Not configured*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872551)

- **Firewall profile private**  
  Baseline default: *Configure*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067041)

  - **Inbound connections blocked**  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872564)

  - **Unicast responses to multicast broadcasts required**  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872562)

  - **Outbound connections required**  
    Baseline default: *Yes*  
    [Learn more](https://aka.ms/intune-firewall-outboundaction)

  - **Inbound notifications blocked**  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872563)

  - **Global port rules from group policy merged**  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872566)

  - **Firewall enabled**  
    Baseline default: *Allowed*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872558)

  - **Authorized application rules from group policy not merged**  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872565)

  - **Connection security rules from group policy not merged**  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872568)

  - **Incoming traffic required**  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872561)

  - **Policy rules from group policy not merged**  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872567)  
::: zone-end  
::: zone pivot="atp-march-2020,atp-april-2020"  
  - **Stealth mode blocked**  
    Baseline default: *Yes*  
    [Learn more](/windows/client-management/mdm/firewall-csp#disablestealthmode)

::: zone-end  
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020,atp-december-2020"

- **Firewall profile public**  
  Baseline default: *Configure*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067143)

  - **Inbound connections blocked**  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872564)

  - **Unicast responses to multicast broadcasts required**  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872562)

  - **Outbound connections required**  
    Baseline default: *Yes*  
    [Learn more](https://aka.ms/intune-firewall-outboundaction)

  - **Authorized application rules from group policy not merged**  
    Baseline default: Yes**  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872565)

  - **Inbound notifications blocked**  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872563)

  - **Global port rules from group policy merged**  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872566)

  - **Firewall enabled**  
    Baseline default: *Allowed*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872558)

  - **Connection security rules from group policy not merged**  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872568)

  - **Incoming traffic required**  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872561)

  - **Policy rules from group policy not merged**  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872567)  
::: zone-end  
::: zone pivot="atp-march-2020,atp-april-2020"  
  - **Stealth mode blocked**  
    Baseline default: *Yes*  
    [Learn more](/windows/client-management/mdm/firewall-csp#disablestealthmode)

::: zone-end  
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020,atp-december-2020"

- **Firewall profile domain**  
  Baseline default: *Configure*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2066796)

  - **Unicast responses to multicast broadcasts required**  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872562)

  - **Authorized application rules from group policy not merged**  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872565)

  - **Inbound notifications blocked**  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872563)

  - **Global port rules from group policy merged**  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872566)

  - **Firewall enabled**  
    Baseline default: *Allowed*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872558)

  - **Connection security rules from group policy not merged**  
    Baseline default: *Yes*  
    [Learn more](/windows/client-management/mdm/firewall-csp#allowlocalipsecpolicymerge)

  - **Policy rules from group policy not merged**  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872567)  
::: zone-end  
::: zone pivot="atp-march-2020,atp-april-2020"  
  - **Stealth mode blocked**  
    Baseline default: *Yes*  
    [Learn more](/windows/client-management/mdm/firewall-csp#disablestealthmode)

::: zone-end  

## Microsoft Defender

::: zone pivot="atp-december-2020"

- **Turn on real-time protection**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2114050)

- **Additional amount of time (0-50 seconds) to extend cloud protection timeout**  
  Baseline default: *0*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2113940)

- **Scan all downloaded files and attachments**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2113934)

- **Scan type**  
  Baseline default: *Quick scan*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2114045)

- **Defender schedule scan day**:  
  Baseline default: *Everyday*

- **Defender scan start time**:  
  Baseline default: *Not configured*

- **Defender sample submission consent**  
  Baseline default: *Send safe samples automatically*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067131)

- **Cloud-delivered protection level**  
  Baseline default: *High*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2113942)

- **Scan removable drives during full scan**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2113946)

- **Defender potentially unwanted app action**  
  Baseline default: *Block*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-Microsoft_Intune_Workflows#defender-puaprotection)

- **Turn on cloud-delivered protection**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2113937)

::: zone-end  
::: zone pivot="atp-sept-2020"

- **Turn on real-time protection**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2114050)

- **Additional amount of time (0-50 seconds) to extend cloud protection timeout**  
  Baseline default: *0*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2113940)

- **Scan all downloaded files and attachments**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2113934)

- **Scan type**  
  Baseline default: *Quick scan*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2114045)

- **Defender sample submission consent**  
  Baseline default: *Send safe samples automatically*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067131)

- **Cloud-delivered protection level**  
  Baseline default: *High*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2113942)

- **Scan removable drives during full scan**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2113946)

- **Defender potentially unwanted app action**  
  Baseline default: *Block*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-Microsoft_Intune_Workflows#defender-puaprotection)

- **Turn on cloud-delivered protection**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2113937)

::: zone-end  
::: zone pivot="atp-april-2020"

- **Run daily quick scan at**  
  Baseline default: *2 AM*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-schedulequickscantime)
  
- **Scheduled scan start time**  
  Baseline default: *2 AM*  
  
- **Configure low CPU priority for scheduled scans**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-enablelowcpupriority)  

- **Block Office communication apps from creating child processes**  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=874499)  

- **Block Adobe Reader from creating child processes**  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=853979)  

- **Scan incoming email messages**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-allowemailscanning)

- **Turn on real-time protection**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2114050)

- **Number of days (0-90) to keep quarantined malware**  
  Baseline default: *0*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-daystoretaincleanedmalware)

- **Defender system scan schedule**  
  Baseline default: *User defined*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-schedulescanday)

- **Additional amount of time (0-50 seconds) to extend cloud protection timeout**  
  Baseline default: *0*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2113940)

- **Scan mapped network drives during a full scan**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanonmappednetworkdrives)

- **Turn on network protection**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

- **Scan all downloaded files and attachments**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2113934)

- **Block on access protection**  
  Baseline default: *Not configured*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-allowonaccessprotection)

- **Scan browser scripts**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender)

- **Block user access to Microsoft Defender app**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-allowuseruiaccess)

- **Maximum allowed CPU usage (0-100 percent) per scan**  
  Baseline default: *50*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-avgcpuloadfactor)

- **Scan type**  
  Baseline default: *Quick scan*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2114045)

- **Enter how often (0-24 hours) to check for security intelligence updates**  
  Baseline default: *8*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender)

- **Defender sample submission consent**  
  Baseline default: *Send safe samples automatically*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067131)

- **Cloud-delivered protection level**  
  Baseline default: **Not configured*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2113942)

- **Scan archive files**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-allowarchivescanning)

- **Turn on behavior monitoring**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-allowbehaviormonitoring)

- **Scan removable drives during full scan**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2113946)

- **Scan network files**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-allowscanningnetworkfiles)

- **Defender potentially unwanted app action**  
  Baseline default: *Block*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-puaprotection)

- **Turn on cloud-delivered protection**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2113937)

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
  Baseline default: *Audit mode*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

- **Block untrusted and unsigned processes that run from USB**  
  Baseline default: *Block*  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

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
::: zone pivot="atp-march-2020"  

- **Run daily quick scan at**  
  Baseline default: *2 AM*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-schedulequickscantime)
  
- **Scheduled scan start time**  
  Baseline default: *2 AM*  
  
- **Configure low CPU priority for scheduled scans**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-enablelowcpupriority)  

- **Block Office communication apps from creating child processes**  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=874499)  

- **Block Adobe Reader from creating child processes**  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=853979)

- **Scan incoming email messages**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-allowemailscanning)

- **Turn on real-time protection**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2114050)

- **Number of days (0-90) to keep quarantined malware**  
  Baseline default: *0*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-daystoretaincleanedmalware)

- **Defender system scan schedule**  
  Baseline default: *User defined*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-schedulescanday)

- **Additional amount of time (0-50 seconds) to extend cloud protection timeout**  
  Baseline default: *0*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2113940)

- **Scan mapped network drives during a full scan**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-allowfullscanonmappednetworkdrives)

- **Turn on network protection**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

- **Scan all downloaded files and attachments**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2113934)

- **Block on access protection**  
  Baseline default: *Not configured*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-allowonaccessprotection)

- **Scan browser scripts**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender)

- **Block user access to Microsoft Defender app**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-allowuseruiaccess)

- **Maximum allowed CPU usage (0-100 percent) per scan**  
  Baseline default: *50*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-avgcpuloadfactor)

- **Scan type**  
  Baseline default: *Quick scan*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2114045)

- **Enter how often (0-24 hours) to check for security intelligence updates**  
  Baseline default: *8*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender)

- **Defender sample submission consent**  
  Baseline default: *Send safe samples automatically*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067131)

- **Cloud-delivered protection level**  
  Baseline default: **Not configured*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2113942)

- **Scan archive files**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-allowarchivescanning)

- **Turn on behavior monitoring**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-allowbehaviormonitoring)

- **Scan removable drives during full scan**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2113946)

- **Scan network files**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-allowscanningnetworkfiles)

- **Defender potentially unwanted app action**  
  Baseline default: *Block*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-Microsoft_Intune_Workflows#defender-puaprotection)

- **Turn on cloud-delivered protection**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2113937)

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
  Baseline default: *Audit mode*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

- **Block untrusted and unsigned processes that run from USB**  
  Baseline default: *Block*  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction)

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
::: zone pivot="atp-march-2020,atp-april-2020"

<!-- Microsoft Defender Security Center was removed with the September 2020 baseline -->

## Microsoft Defender Security Center

- **Block users from editing the Exploit Guard protection interface**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-disallowexploitprotectionoverride)

::: zone-end

## Smart Screen

::: zone pivot="atp-sept-2020,atp-december-2020"

- **Block users from ignoring SmartScreen warnings**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872783)

- **Turn on Windows SmartScreen**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872784)

- **Require SmartScreen for Microsoft Edge**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067029)

- **Block malicious site access**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067040)  

- **Block unverified file download**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067023)  

- **Configure Microsoft Defender SmartScreen**  
  Baseline default: *Enabled*  

- **Prevent bypassing Microsoft Defender SmartScreen prompts for sites**  
  Baseline default: *Enabled*

- **Prevent bypassing of Microsoft Defender SmartScreen warnings about downloads**  
  Baseline default: *Enabled*

- **Configure Microsoft Defender SmartScreen to block potentially unwanted apps**  
  Baseline default: *Enabled*

::: zone-end  
::: zone pivot="atp-march-2020,atp-april-2020"

- **Require apps from store only**  
  Baseline default: *Yes*  

- **Turn on Windows SmartScreen**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-smartscreen#smartscreen-enablesmartscreeninshell)

::: zone-end  
::: zone pivot="atp-march-2020,atp-april-2020"

<!-- Windows Hello for Business was removed with the September 2020 baseline -->

## Windows Hello for Business

For more information, see [PassportForWork CSP](/windows/client-management/mdm/passportforwork-csp) in the Windows documentation.

- **Block Windows Hello for Business**  
  Baseline default: *Disabled*

  - **Lowercase letters in PIN**
    Baseline default: *Allowed*  

  - **Special characters in PIN**
    Baseline default: *Allowed*  

  - **Uppercase letters in PIN**
    Baseline default: *Allowed*  

::: zone-end

## Next steps

- [Learn about security baselines](security-baselines.md)
- [Avoid conflicts](security-baselines.md#avoid-conflicts)
- [Troubleshoot policies and profiles in Intune](/troubleshoot/mem/intune/troubleshoot-policies-in-microsoft-intune)
