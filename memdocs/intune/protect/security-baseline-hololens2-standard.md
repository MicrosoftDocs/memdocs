---
# required metadata

title: List of settings for the Microsoft HoloLense 2 standard security baseline in Intune
titleSuffix: Microsoft Intune
description: View a list of the settings in the Microsoft Intune standard security baseline for Microsoft HoloLens 2. This list includes the default values for settings as found in the default configuration of the baseline.
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/27/2025
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

---
<!-- FOR METADATA: 

zone_pivot_groups: hololens2-Standard-baselines

<!-- Pivot details:

    - id: version-1
      title: HoloLens 2 Standard (January 2025)
    - id: version-2
      title: HoloLens 2 Standard (MONTH/YEAR)
-->

# Settings reference for Microsoft HoloLens 2 standard security baseline for Microsoft Intune

This article is a reference for the settings that are available in the Microsoft HoloLens 2 standard security baseline for Microsoft Intune.

> [!TIP]
> To view settings for the Microsoft HoloLens 2 *advanced* security baseline, see [Settings reference for the Microsoft HoloLens 2 advanced security baseline for Microsoft Intune](../protect/security-baseline-hololens2-advanced.md).

## About this reference article

Each security baseline is a group of preconfigured Windows settings that help you apply and enforce granular security settings that the relevant security teams recommend. You can also customize each baseline you deploy to enforce only those settings and values you require. When you create a security baseline profile in Intune, you're creating a template that consists of multiple device configuration settings.

The details that display in this article are based on baseline version you select at the top of the article. For each version, this article displays:

- A list of each and its configuration as found in the default instance of that baseline version.
- When available, a link to the underlying configuration service provider (CSP) documentation or other related content from the relevant product group that provides context and possibly additional details for a settings use.

When a new version of a baseline becomes available, it replaces the previous version. Profile instances that you’ve created prior to the availability of a new version:

- Become read-only. You can continue to use those profiles but can't edit them to change their configuration.
- Can be updated to the current version. After you update a profile to the current baseline version, you can edit the profile to modify settings.

To learn more about using security baselines, see:
- [Use security baselines](../protect/security-baselines.md)
- [Change the baseline version for a profile](../protect/security-baselines-configure.md#update-baselines-that-use-the-previous-format)
- [Manage security baselines](../protect/security-baselines-configure.md)


## HoloLens 2 Standard security baseline (version 1) - *January 2025*

### #Accounts

- **Allow Microsoft Account Connection**  
   Baseline default: *Block*  
  [Learn more](/windows/client-management/mdm/policy-csp-Accounts#allowmicrosoftaccountconnection)

### Administrative Templates

#### System > Power Management > Video and Display Settings

- **Turn off the display (plugged in)**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-power#power-displayofftimeoutpluggedin)

  - **When plugged in, turn display off after (seconds)**  
     Baseline default: *30*

### Browser

- **Allow Cookies**  
  Baseline default: *Block only cookies from third party websites*  
  [Learn more](/windows/client-management/mdm/policy-csp-Browser#allowcookies)

- **Allow Password Manager**  
  Baseline default: *Block*  
  [Learn more](/windows/client-management/mdm/policy-csp-Browser#allowpasswordmanager)

- **Allow Smart Screen**  
  Baseline default: *Allow*  
  [Learn more](/windows/client-management/mdm/policy-csp-Browser#allowsmartscreen)

### Connectivity

- **Allow USB Connection**  
  Baseline default: *Not allowed.*  
  [Learn more](/windows/client-management/mdm/policy-csp-connectivity#allowusbconnection)

### Device Lock

- **Device Password Enabled**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-devicelock#devicepasswordenabled)

  - **Max Device Password Failed Attempts**  
    Baseline default: *Not configured*  
    [Learn more](/windows/client-management/mdm/policy-csp-devicelock#maxdevicepasswordfailedattempts)

  - **Allow Idle Return Without Password**  
    Baseline default: *Not allowed.*  
    [Learn more](/windows/client-management/mdm/policy-csp-deviceLock#allowidlereturnwithoutpassword)

  - **Alphanumeric Device Password Required**  
    Baseline default: *Password or Numeric PIN required.*  
    [Learn more](/windows/client-management/mdm/policy-csp-devicelock#alphanumericdevicepasswordrequired)

  - **Max Inactivity Time Device Lock**  
    Baseline default: *Configured*  
    Value: *3*  
    [Learn more](/windows/client-management/mdm/policy-csp-devicelock#maxinactivitytimedevicelock)

  - **Device Password History**  
    Baseline default: *Not configured*  
    [Learn more](/windows/client-management/mdm/policy-csp-devicelock#devicepasswordhistory)

  - **Allow Simple Device Password**  
    Baseline default: *Not allowed.*  
    [Learn more](/windows/client-management/mdm/policy-csp-devicelock#allowsimpledevicepassword)

  - **Device Password Expiration**  
    Baseline default: *Not configured*  
    [Learn more](/windows/client-management/mdm/policy-csp-devicelock#devicepasswordexpiration)

  - **Min Device Password Length**  
    Baseline default: *Configured*  
    Value: *8*  
    [Learn more](/windows/client-management/mdm/policy-csp-devicelock#mindevicepasswordlength)

### Experience

- **Allow Manual MDM Unenrollment**  
  Baseline default: *Block*  
  [Learn more](/windows/client-management/mdm/policy-csp-Experience#allowmanualmdmunenrollment)

### Microsoft App Store

- **Allow All Trusted Apps**  
  Baseline default: *Explicit deny.*  
  [Learn more](/windows/client-management/mdm/policy-csp-ApplicationManagement#allowalltrustedapps)

- **Allow apps from the Microsoft app store to auto update**  
  Baseline default: *Allowed.*  
  [Learn more](/windows/client-management/mdm/policy-csp-ApplicationManagement#allowappstoreautoupdate)

- **Allow Developer Unlock**  
  Baseline default: *Explicit deny.*  
  [Learn more](/windows/client-management/mdm/policy-csp-ApplicationManagement#allowdeveloperunlock)

### Microsoft Edge

- **Block third party cookies**  
  Baseline default: *Enabled*

#### Extensions

- **Control which extensions cannot be installed**  
  Baseline default: *Enabled*

  - **Extension IDs the user should be prevented from installing (or * for all) (Device)**  
    Baseline default: *

#### Password manager and protection

- **Enable saving passwords to the password manager**  
  Baseline default: *Disabled*

#### SmartScreen settings

- **Configure Microsoft Defender SmartScreen**  
  Baseline default: *Enabled*

### Mixed Reality

- **AAD Group Membership Cache Validity In Days**  
  Baseline default: *Configured*  
  Value: *7*  
  [Learn more](/windows/client-management/mdm/policy-csp-MixedReality#aadgroupmembershipcachevalidityindays)

### Settings

- **Allow VPN**  
  Baseline default: *Not allowed.*  
  [Learn more](/windows/client-management/mdm/policy-csp-Settings#allowvpn)

- **Page Visibility List**  
  Baseline default: *Configured*  
  Value: *hide:emailandaccounts;workplace;otherusers;bluetooth;usb;network-proxy;network-wifi;network-ethernet;network-airplanemode;powersleep;certificates;developers;windowsinsider;*  
  [Learn more](/windows/client-management/mdm/policy-csp-Settings#pagevisibilitylist)

### System

- **Allow Storage Card**  
  Baseline default: *SD card use is not allowed and USB drives are disabled. This setting does not prevent programmatic access to the storage card.*  
  [Learn more](/windows/client-management/mdm/policy-csp-System#allowstoragecard)

### Tenant Lockdown

- **Require Network In OOBE (Device)**  
  Baseline default: *True*

### Windows Hello For Business

- **Enable Pin Recovery**  
  Baseline default: *false*  
  [Learn more](/windows/client-management/mdm/passportforwork-csp#devicetenantidpoliciesenablepinrecovery)

- **Restrict use of TPM 1.2**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/passportforwork-csp#devicetenantidpoliciesexcludesecuritydevicestpm12)

- **Digits**  
  Baseline default: *Requires the use of at least one digits in PIN.*  
  [Learn more](/windows/client-management/mdm/passportforwork-csp#devicetenantidpoliciespincomplexitydigits)

- **Expiration**  
  Baseline default: *Configured*  
    Value: *90*  
  [Learn more](/windows/client-management/mdm/passportforwork-csp#devicetenantidpoliciespincomplexityexpiration)

- **PIN History**  
  Baseline default: *Configured*  
  Value: *10*
  [Learn more](/windows/client-management/mdm/passportforwork-csp#usertenantidpoliciespincomplexityhistory)

- **Lowercase Letters**  
  Baseline default: *Allowed*  
  [Learn more](/windows/client-management/mdm/PassportForWork-csp/#devicetenantidpoliciespincomplexitylowercaseletters)

- **Maximum PIN Length**  
  Baseline default: *Configured*  
  Value: *6*  
  [Learn more](/windows/client-management/mdm/passportforwork-csp#devicetenantidpoliciespincomplexitymaximumpinlength)

- **Minimum PIN Length**  
  Baseline default: *Configured*  
    Value: *6*  
  [Learn more](/windows/client-management/mdm/passportforwork-csp#usertenantidpoliciespincomplexityminimumpinlength)

- **Special Characters**  
  Baseline default: *Allows the use of special characters in PIN.*  
  [Learn more](/windows/client-management/mdm/passportforwork-csp#usertenantidpoliciespincomplexityspecialcharacters)

- **Uppercase Letters**  
  Baseline default: *Allowed*  
  [Learn more](/windows/client-management/mdm/passportforwork-csp#usertenantidpoliciespincomplexityuppercaseletters)

- **Require Security Device**  
  Baseline default: *true*  
  [Learn more](/windows/client-management/mdm/passportforwork-csp#devicetenantidpoliciesrequiresecuritydevice)

- **Use Certificate For On Prem Auth**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/passportforwork-csp#devicetenantidpoliciesusecertificateforonpremauth)

- **Use Hello Certificates As Smart Card Certificates**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/passportforwork-csp#devicetenantidpoliciesusehellocertificatesassmartcardcertificates)

- **Use Windows Hello For Business (Device)**  
  Baseline default: *true*  
  [Learn more](/windows/client-management/mdm/passportforwork-csp#devicetenantidpoliciesusepassportforwork)

### Windows Update For Business

- **Allow Update Service**  
  Baseline default: *Allow*  
  [Learn more](/windows/client-management/mdm/policy-csp-Update#allowupdateservice)

- **Manage Preview Builds**  
  Baseline default: *Disable Preview builds*  
  [Learn more](/windows/client-management/mdm/policy-csp-Update#managepreviewbuilds)

## Learn more

- [Learn about security baselines](security-baselines.md)
- [Avoid conflicts](security-baselines.md#avoid-conflicts)
- [Troubleshoot policies and profiles in Intune](/troubleshoot/mem/intune/troubleshoot-policies-in-microsoft-intune)
