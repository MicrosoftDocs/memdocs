---
# required metadata

title: Settings list for the Microsoft Intune security baseline for Microsoft Defender for Endpoint
titleSuffix: Microsoft Intune
description: View the settings in the Microsoft Intune security baseline for Microsoft Defender for Endpoint and each settings default value.
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/10/2024
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.assetid:

# optional metadata
#ROBOTS:
#audience:

ms.reviewer: juidaewo
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
- sub-secure-endpoints
zone_pivot_groups: atp-baseline-versions
---

<!-- Pivots and versions still in use: 
- May 2024 v24h1    > "mde-v24h1"
- December 2020 v6  > "atp-december-2020"
- September 2020 v5 > "atp-sept-2020"
- April 2020 v4     > "atp-april-2020"
- March 2020 v3     > "atp-march-2020"

-->

# Microsoft Defender for Endpoint security baseline settings reference for Microsoft Intune

This article is a reference for the settings that are available in the Microsoft Defender for Endpoint security baseline for Microsoft Intune.

## About this reference article

Each security baseline is a group of preconfigured Windows settings that help you apply and enforce granular security settings that the relevant security teams recommend. You can also customize each baseline you deploy to enforce only those settings and values you require. When you create a security baseline profile in Intune, you're creating a template that consists of multiple device configuration settings.

The details that display in this article are based on baseline version you select at the top of the article. For each version, this article displays:

- A list of each setting and its configuration as found in the default instance of that baseline version.
- When available, a link to the underlying configuration service provider (CSP) documentation or other related content from the relevant product group that provides context and possibly additional details for a settings use.

When a new version of a baseline becomes available, it replaces the previous version. Profile instances that you’ve created prior to the availability of a new version:

- Become read-only. You can continue to use those profiles but can't edit them to change their configuration.
- Can be updated to the current version. After you update a profile to the current baseline version, you can edit the profile to modify settings.

This article is a reference for the settings that are available in the different versions of the Microsoft Defender for Endpoint security baseline that you can deploy with Microsoft Intune. Use the tabs to select and view the settings in the most recent baseline version and a few older versions that might still be in use.

To learn more about using security baselines, see:
- [Use security baselines](../protect/security-baselines.md)
- [Change the baseline version for a profile](../protect/security-baselines-configure.md#update-baselines-that-use-the-previous-format)
- [Manage security baselines](../protect/security-baselines-configure.md)


::: zone pivot="mde-v24h1"
## Microsoft Defender for Endpoint baseline version 24H1  
::: zone-end  
::: zone pivot="atp-december-2020"
## Microsoft Defender for Endpoint baseline for December 2020 - version 6 
::: zone-end  
::: zone pivot="atp-sept-2020"
## Microsoft Defender for Endpoint baseline for September 2020 - version 5 
::: zone-end  
::: zone pivot="atp-april-2020"
## Microsoft Defender for Endpoint baseline for April 2020 - version 4 
::: zone-end  
::: zone pivot="atp-march-2020"
## Microsoft Defender for Endpoint baseline for March 2020 - version 3 
::: zone-end

The Microsoft Defender for Endpoint baseline is available when your environment meets the prerequisites for using [Microsoft Defender for Endpoint](advanced-threat-protection.md#prerequisites).

This baseline is optimized for physical devices and isn't recommended for use on virtual machines (VMs) or VDI endpoints. Certain baseline settings can affect remote interactive sessions on virtualized environments. For more information, see [Increase compliance to the Microsoft Defender for Endpoint security baseline](/windows/security/threat-protection/microsoft-defender-atp/configure-machines-security-baseline) in the Windows documentation.

::: zone pivot="mde-v24h1"

### Administrative Templates

#### System > Device Installation > Device Installation Restrictions

- **Prevent installation of devices using drivers that match these device setup classes**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-deviceinstallation?WT.mc_id=Portal-fx#preventinstallationofmatchingdevicesetupclasses)

  - **Prevented Classes**  
    Baseline default: *d48179be-ec20-11d1-b6b8-00c04fa372a7*  

  - **Also apply to matching devices that are already installed.**  
    Baseline default: *False*  

#### Windows Components > BitLocker Drive Encryption

- **Choose drive encryption method and cipher strength (Windows 10 [Version 1511] and later)**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/bitlocker-csp?WT.mc_id=Portal-fx#encryptionmethodbydrivetype)

  - **Select the encryption method for removable data drives:**  
    Baseline default: *AES-CBC 128-bit (default)*

  - **Select the encryption method for operating system drives:**  
    Baseline default: *XTS-AES 128-bit (default)*

  - **Select the encryption method for fixed data drives:**  
    Baseline default: *XTS-AES 128-bit (default)*

#### Windows Components > BitLocker Drive Encryption > Fixed Data Drives

- **Choose how BitLocker-protected fixed drives can be recovered**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/bitlocker-csp?WT.mc_id=Portal-fx#fixeddrivesrecoveryoptions)

  - **Do not enable BitLocker until recovery information is stored to AD DS for fixed data drives**  
    Baseline default: *True*

  - **Allow data recovery agent**  
    Baseline default: *True*

  - **Configure storage of BitLocker recovery information to AD DS**  
    Baseline default: *Backup recovery passwords and key packages*

    Value: *Allow 256-bit recovery key*

  - **Save BitLocker recovery information to AD DS for fixed data drives**  
    Baseline default: *True*

  - **Omit recovery options from the BitLocker setup wizard**  
    Baseline default: *True*

  - **Configure user storage of BitLocker recovery information:**  
    Baseline default: *Allow 48-digit recovery password*

- **Deny write access to fixed drives not protected by BitLocker**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/bitlocker-csp?WT.mc_id=Portal-fx#fixeddrivesrequireencryption)

- **Enforce drive encryption type on fixed data drives**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/bitlocker-csp?WT.mc_id=Portal-fx#fixeddrivesencryptiontype)

  - **Select the encryption type: (Device)**  
    Baseline default: *Used Space Only encryption*

#### Windows Components > BitLocker Drive Encryption > Operating System Drives

- **Allow devices compliant with InstantGo or HSTI to opt out of pre-boot PIN.**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/bitlocker-csp?WT.mc_id=Portal-fx#systemdrivesenableprebootpinexceptionondecapabledevice)

- **Allow enhanced PINs for startup**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/bitlocker-csp?WT.mc_id=Portal-fx#systemdrivesenhancedpin)

- **Choose how BitLocker-protected operating system drives can be recovered**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/bitlocker-csp?WT.mc_id=Portal-fx#systemdrivesrecoveryoptions)

  - **Omit recovery options from the BitLocker setup wizard**  
    Baseline default: *True*

  - **Allow data recovery agent**  
    Baseline default: *True*

    Value: *Allow 256-bit recovery key*

  - **Configure storage of BitLocker recovery information to AD DS:**  
    Baseline default: *Store recovery passwords and key packages*

  - **Do not enable BitLocker until recovery information is stored to AD DS for operating system drives**  
    Baseline default: *True*

  - **Save BitLocker recovery information to AD DS for operating system drives**  
    Baseline default: *True*

  - **Configure user storage of BitLocker recovery information:**  
    Baseline default: *Allow 48-digit recovery password*

- **Enable use of BitLocker authentication requiring preboot keyboard input on slates**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/bitlocker-csp?WT.mc_id=Portal-fx#systemdrivesenableprebootinputprotectorsonslates)

- **Enforce drive encryption type on operating system drive**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/bitlocker-csp?WT.mc_id=Portal-fx#systemdrivesencryptiontype)

  - **Select the encryption type: (Device)**  
    Baseline default: *Used Space Only encryption*

- **Require additional authentication at startup**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/bitlocker-csp?WT.mc_id=Portal-fx#systemdrivesrequirestartupauthentication)

  - **Configure TPM startup key and PIN:**  
    Baseline default: *Do not allow startup key and PIN with TPM*

  - **Configure TPM startup:**  
    Baseline default: *Allow TPM*

  - **Allow BitLocker without a compatible TPM (requires a password or a startup key on a USB flash drive)**  
    Baseline default: *False*

  - **Configure TPM startup PIN:**  
    Baseline default: *Allow startup PIN with TPM*

  - **Configure TPM startup key:**  
    Baseline default: *Do not allow startup key with TPM*

#### Windows Components > BitLocker Drive Encryption > Removable Data Drives

- **Control use of BitLocker on removable drives**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/bitlocker-csp?WT.mc_id=Portal-fx#removabledrivesconfigurebde)

  - **Allow users to apply BitLocker protection on removable data drives (Device)**  
    Baseline default: *True*

    - **Enforce drive encryption type on removable data drives**  
      Baseline default: *Enabled*  
      [Learn more](/windows/client-management/mdm/bitlocker-csp?WT.mc_id=Portal-fx#removabledrivesencryptiontype)

      - **Select the encryption type: (Device)**  
      Baseline default: *Used Space Only encryption*

  - **Allow users to suspend and decrypt BitLocker protection on removable data drives (Device)**  
    Baseline default: *False*

- **Deny write access to removable drives not protected by BitLocker**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/bitlocker-csp?WT.mc_id=Portal-fx#removabledrivesrequireencryption)

  - **Do not allow write access to devices configured in another organization**  
    Baseline default: *False*

#### Windows Components > File Explorer

- **Configure Windows Defender SmartScreen**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-admx-windowsexplorer?WT.mc_id=Portal-fx#enablesmartscreen)

  - **Pick one of the following settings: (Device)**  
    Baseline default: *Warn and prevent bypass*

#### Windows Components > Internet Explorer

- **Prevent bypassing SmartScreen Filter warnings about files that are not commonly downloaded from the Internet**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#disablebypassofsmartscreenwarningsaboutuncommonfiles)

- **Prevent bypassing SmartScreen Filter warnings about files that are not commonly downloaded from the Internet (User)**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#disablebypassofsmartscreenwarningsaboutuncommonfiles)

- **Prevent managing SmartScreen Filter**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#preventmanagingsmartscreenfilter)

  - **Select SmartScreen Filter mode**  
    Baseline default: *On*

### BitLocker

- **Allow Warning For Other Disk Encryption**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/bitlocker-csp?WT.mc_id=Portal-fx#allowwarningforotherdiskencryption)

- **Configure Recovery Password Rotation**  
  Baseline default: *Refresh on for both Azure AD-joined and hybrid-joined devices*  
  [Learn more](/windows/client-management/mdm/bitlocker-csp?WT.mc_id=Portal-fx#configurerecoverypasswordrotation)

- **Require Device Encryption**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/bitlocker-csp?WT.mc_id=Portal-fx#requiredeviceencryption)

### Defender

- **Allow Archive Scanning**  
  Baseline default: *Allowed. Scans the archive files.*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#allowarchivescanning)

- **Allow Behavior Monitoring**  
  Baseline default: *Allowed. Turns on real-time behavior monitoring.*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#allowbehaviormonitoring)

- **Allow Cloud Protection**  
  Baseline default: *Allowed. Turns on Cloud Protection.*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#allowcloudprotection)

- **Allow Email Scanning**  
  Baseline default: *Allowed. Turns on email scanning.*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#allowemailscanning)

- **Allow Full Scan Removable Drive Scanning**  
  Baseline default: *Allowed. Scans removable drives.*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#allowfullscanremovabledrivescanning)

- **Allow On Access Protection**  
  Baseline default: *Allowed.*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#allowonaccessprotection)

- **Allow Realtime Monitoring**  
  Baseline default: *Allowed. Turns on and runs the real-time monitoring service.*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#allowrealtimemonitoring)

- **Allow Scanning Network Files**  
  Baseline default: *Allowed. Scans network files.*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#allowscanningnetworkfiles)

- **Allow scanning of all downloaded files and attachments**  
  Baseline default: *Allowed.*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#allowioavprotection)

- **Allow Script Scanning**  
  Baseline default: *Allowed.*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#allowscriptscanning)

- **Allow User UI Access**  
  Baseline default: *Allowed. Lets users access UI.*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#allowuseruiaccess)

  - **Block execution of potentially obfuscated scripts**  
  Baseline default: *Block*  
  [Learn more](/defender-endpoint/attack-surface-reduction?WT.mc_id=Portal-fx)

  - **Block Win32 API calls from Office macros**  
  Baseline default: *Block*  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)

  - **Block executable files from running unless they meet a prevalence, age, or trusted list criterion**  
  Baseline default: *Block*  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)

  - **Block Office communication application from creating child processes**  
  Baseline default: *Block*  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)

  - **Block all Office applications from creating child processes**  
  Baseline default: *Block*  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)

  - **Block Adobe Reader from creating child processes**  
  Baseline default: *Block*  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)

  - **Block credential stealing from the Windows local security authority subsystem**  
  Baseline default: *Block*  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)

  - **Block JavaScript or VBScript from launching downloaded executable content**  
  Baseline default: *Block*  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)

  - **Block Webshell creation for Servers**  
  Baseline default: *Block*  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)

  - **Block untrusted and unsigned processes that run from USB**  
  Baseline default: *Block*  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)

  - **Block persistence through WMI event subscription**  
  Baseline default: *Audit*  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)

  - **[PREVIEW] Block use of copied or impersonated system tools**  
  Baseline default: *Block*  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)

  - **Block abuse of exploited vulnerable signed drivers (Device)**  
  Baseline default: *Block*  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)

  - **Block process creations originating from PSExec and WMI commands**  
  Baseline default: *Audit*  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)

  - **Block Office applications from creating executable content**  
  Baseline default: *Block*  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)

  - **Block Office applications from injecting code into other processes**  
  Baseline default: *Block*  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)

  - **[PREVIEW] Block rebooting machine in Safe Mode**  
  Baseline default: *Block*  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)

  - **Use advanced protection against ransomware**  
  Baseline default: *Block*  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)

  - **Block executable content from email client and webmail**  
  Baseline default: *Block*  
  [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)

- **Check For Signatures Before Running Scan**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#checkforsignaturesbeforerunningscan)

- **Cloud Block Level**  
  Baseline default: *High*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#cloudblocklevel)

- **Cloud Extended Timeout**  
  Baseline default: *Configured*  
  Value: *50*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#cloudextendedtimeout)

- **Disable Local Admin Merge**  
  Baseline default: *Enable Local Admin Merge*  
  [Learn more](/windows/client-management/mdm/defender-csp?WT.mc_id=Portal-fx#configurationdisablelocaladminmerge)

- **Enable Network Protection**  
  Baseline default: *Enabled (block mode)*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#enablenetworkprotection)

- **Hide Exclusions From Local Admins**  
  Baseline default: *If you enable this setting, local admins will no longer be able to see the exclusion list in Windows Security App or via PowerShell.*  
  [Learn more](/windows/client-management/mdm/defender-csp?WT.mc_id=Portal-fx#configurationhideexclusionsfromlocaladmins)

- **Hide Exclusions From Local Users**  
  Baseline default: *If you enable this setting, local users will no longer be able to see the exclusion list in Windows Security App or via PowerShell.*  
  [Learn more](/windows/client-management/mdm/defender-csp?WT.mc_id=Portal-fx#configurationhideexclusionsfromlocalusers)

- **Oobe Enable Rtp And Sig Update**  
  Baseline default: *If you enable this setting, real-time protection and Security Intelligence Updates are enabled during OOBE.*  
  [Learn more](/windows/client-management/mdm/defender-csp?WT.mc_id=Portal-fx#configurationoobeenablertpandsigupdate)

- **PUA Protection**  
  Baseline default: *PUA Protection on. Detected items are blocked. They will show in history along with other threats.*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#puaprotection)

- **Real Time Scan Direction**  
  Baseline default: *Monitor all files (bi-directional).*  
  [Learn more](/windows/client-management/mdm/policy-csp-Defender?WT.mc_id=Portal-fx#realtimescandirection)

- **Scan Parameter**  
  Baseline default: *Quick scan*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#scanparameter)

- **Schedule Quick Scan Time**  
  Baseline default: *Configured*  
  Value: *120*  
  [Learn more](/windows/client-management/mdm/policy-csp-Defender?WT.mc_id=Portal-fx#schedulequickscantime)

- **Schedule Scan Day**  
  Baseline default: *Every day*  
  [Learn more](/windows/client-management/mdm/policy-csp-Defender?WT.mc_id=Portal-fx#schedulescanday)

- **Schedule Scan Time**  
  Baseline default: *Configured*  
  Value: *120*  
  [Learn more](/windows/client-management/mdm/policy-csp-Defender?WT.mc_id=Portal-fx#schedulescantime)

- **Signature Update Interval**  
  Baseline default: *Configured*  
  Value: *4*  
  [Learn more](/windows/client-management/mdm/policy-csp-Defender?WT.mc_id=Portal-fx#signatureupdateinterval)

- **Submit Samples Consent**  
  Baseline default: *Send all samples automatically.*  
  [Learn more](/windows/client-management/mdm/policy-csp-Defender?WT.mc_id=Portal-fx#submitsamplesconsent)

### Device Guard

- **Credential Guard**  
  Baseline default: *(Enabled with UEFI lock) Turns on Credential Guard with UEFI lock.*  
  [Learn more](/windows/client-management/mdm/policy-csp-deviceguard?WT.mc_id=Portal-fx#lsacfgflags)

### Dma Guard

- **Device Enumeration Policy**  
  Baseline default: *Block all (Most restrictive)*  
  [Learn more](/windows/client-management/mdm/policy-csp-dmaguard?WT.mc_id=Portal-fx#deviceenumerationpolicy)

### Firewall

- **Certificate revocation list verification**  
  Baseline default: *None*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreglobalcrlcheck)

- **Disable Stateful Ftp**  
  Baseline default: *True*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreglobaldisablestatefulftp)

- **Enable Domain Network Firewall**  
  Baseline default: *True*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoredomainprofileenablefirewall)

  - **Allow Local Ipsec Policy Merge**  
  Baseline default: *True*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoredomainprofileallowlocalipsecpolicymerge)

  - **Disable Stealth Mode**  
  Baseline default: *False*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoredomainprofiledisablestealthmode)

  - **Disable Inbound Notifications**  
  Baseline default: *True*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoredomainprofiledisableinboundnotifications)

  - **Disable Unicast Responses To Multicast Broadcast**  
  Baseline default: *False*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoredomainprofiledisableunicastresponsestomulticastbroadcast)

  - **Global Ports Allow User Pref Merge**  
  Baseline default: *True*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoredomainprofileglobalportsallowuserprefmerge)

  - **Disable Stealth Mode Ipsec Secured Packet Exemption**  
  Baseline default: *True*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoredomainprofiledisablestealthmodeipsecsecuredpacketexemption)

  - **Allow Local Policy Merge**  
  Baseline default: *True*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoredomainprofileallowlocalpolicymerge)

- **Enable Packet Queue**  
  Baseline default: *Configured*  
  Value: *Disabled*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreglobalenablepacketqueue)

- **Enable Private Network Firewall**  
  Baseline default: *True*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreprivateprofileenablefirewall)

  - **Default Inbound Action for Private Profile**  
  Baseline default: *Block*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreprivateprofiledefaultinboundaction)

  - **Disable Unicast Responses To Multicast Broadcast**  
  Baseline default: *False*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreprivateprofiledisableunicastresponsestomulticastbroadcast)

  - **Disable Stealth Mode**  
  Baseline default: *False*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreprivateprofiledisablestealthmode)

  - **Global Ports Allow User Pref Merge**  
  Baseline default: *True*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreprivateprofileglobalportsallowuserprefmerge)

  - **Allow Local Ipsec Policy Merge**  
  Baseline default: *True*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreprivateprofileallowlocalipsecpolicymerge)

  - **Disable Stealth Mode Ipsec Secured Packet Exemption**  
  Baseline default: *True*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreprivateprofiledisablestealthmodeipsecsecuredpacketexemption)

  - **Disable Inbound Notifications**  
  Baseline default: *True*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreprivateprofiledisableinboundnotifications)

  - **Allow Local Policy Merge**  
  Baseline default: *True*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreprivateprofileallowlocalpolicymerge)

  - **Default Outbound Action**  
  Baseline default: *Allow*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreprivateprofiledefaultoutboundaction)

  - **Auth Apps Allow User Pref Merge**  
  Baseline default: *True*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreprivateprofileauthappsallowuserprefmerge)

- **Enable Public Network Firewall**  
  Baseline default: *True*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofileenablefirewall)

  - **Disable Stealth Mode**  
  Baseline default: *False*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofiledisablestealthmode)

  - **Default Outbound Action**  
  Baseline default: *Allow*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofiledefaultoutboundaction)

  - **Disable Inbound Notifications**  
  Baseline default: *True*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofiledisableinboundnotifications)

  - **Disable Stealth Mode Ipsec Secured Packet Exemption**  
  Baseline default: *True*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofiledisablestealthmodeipsecsecuredpacketexemption)

  - **Allow Local Policy Merge**  
  Baseline default: *True*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofileallowlocalpolicymerge)

  - **Auth Apps Allow User Pref Merge**  
  Baseline default: *True*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofileauthappsallowuserprefmerge)

  - **Default Inbound Action for Public Profile**  
  Baseline default: *Block*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofiledefaultinboundaction)

  - **Disable Unicast Responses To Multicast Broadcast**  
  Baseline default: *False*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofiledisableunicastresponsestomulticastbroadcast)

  - **Global Ports Allow User Pref Merge**  
  Baseline default: *True*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofileglobalportsallowuserprefmerge)

  - **Allow Local Ipsec Policy Merge**  
  Baseline default: *True*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofileallowlocalipsecpolicymerge)

- **Preshared Key Encoding**  
  Baseline default: *UTF8*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreglobalpresharedkeyencoding)

- **Security association idle time**  
  Baseline default: *Configured*  
  Value: *300*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreglobalsaidletime)

### Microsoft Edge

- **Configure Microsoft Defender SmartScreen**  
  Baseline default: *Enabled*  

- **Configure Microsoft Defender SmartScreen to block potentially unwanted apps**  
  Baseline default: *Enabled*  

- **Enable Microsoft Defender SmartScreen DNS requests**  
  Baseline default: *Enabled*  

- **Enable new SmartScreen library**  
  Baseline default: *Enabled*  

- **Force Microsoft Defender SmartScreen checks on downloads from trusted sources**  
  Baseline default: *Enabled*  

- **Prevent bypassing Microsoft Defender SmartScreen prompts for sites**  
  Baseline default: *Enabled*  

- **Prevent bypassing of Microsoft Defender SmartScreen warnings about downloads**  
  Baseline default: *Enabled*  

::: zone-end
::: zone pivot="atp-sept-2020,atp-december-2020"

### Attack Surface Reduction Rules

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

### Application Guard

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
::: zone pivot="atp-december-2020,atp-sept-2020,atp-march-2020,atp-april-2020"

### BitLocker

::: zone-end  
::: zone pivot="atp-march-2020,atp-april-2020"

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

### Browser

- **Require SmartScreen for Microsoft Edge**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

- **Block malicious site access**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)  

- **Block unverified file download**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)  

### Data Protection

- **Block direct memory access**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-dataprotection#dataprotection-allowdirectmemoryaccess)  

::: zone-end  
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020,atp-december-2020"

### Device Guard

- **Turn on credential guard**  
  Baseline default: *Enable with UEFI lock*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872424)

### Device Installation

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
::: zone pivot="atp-sept-2020,atp-december-2020"

### DMA Guard

::: zone-end  
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

### Endpoint Detection and Response

- **Sample sharing for all files**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/windowsadvancedthreatprotection-csp)

- **Expedite telemetry reporting frequency**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/windowsadvancedthreatprotection-csp)

::: zone-end  
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020,atp-december-2020"

### Firewall

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
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020,atp-december-2020"

### Microsoft Defender

::: zone-end  
::: zone pivot="atp-december-2020"

- **Turn on real-time protection**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2114050)

- **Additional amount of time (0-50 seconds) to extend cloud protection timeout**  
  Baseline default: *50*  
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
  Baseline default: *50*  
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
  Baseline default: *50*  
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
  Baseline default: *50*  
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

### Microsoft Defender Security Center

- **Block users from editing the Exploit Guard protection interface**  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-windowsdefendersecuritycenter#windowsdefendersecuritycenter-disallowexploitprotectionoverride)

::: zone-end  
::: zone pivot="atp-march-2020,atp-april-2020,atp-sept-2020,atp-december-2020"

### Smart Screen

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

### Windows Hello for Business

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

