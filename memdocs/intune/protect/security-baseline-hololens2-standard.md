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

To view settings for the Microsoft HoloLens 2 *advanced* security baseline, see [Settings reference for the Microsoft HoloLens 2 advanced security baseline for Microsoft Intune](../protect/security-baseline-hololens2-advanced.md).

## About this reference article

Each security baseline is a group of preconfigured Windows settings that help you apply and enforce granular security settings that the relevant security teams recommend. You can also customize each baseline you deploy to enforce only those settings and values you require. When you create a security baseline profile in Intune, you're creating a template that consists of multiple device configuration profiles.

<!-- THIS is the only version of this baseline at this time. The following is for use when there are multiple versions:

The details in this article are based on the baseline version that you select at the top of this article. For each selection, this article displays:
	
- A list of each setting in that baseline version.
- The default configuration of each setting in that baseline version.
- When available, a link to the underlying configuration service provider (CSP) documentation, or other related content from the relevant product group that provides context and possibly additional details for the settings use.
-->

When a new version of this baseline becomes available, the new version replaces the previous version. Profile instances that were created before the availability of a new version:

- Become read-only. You can continue to use those profiles but can't edit them to change their configuration.
- Can be updated to the latest version. After you update a profile to the current baseline version, you can edit that updated profile to modify settings.

To learn more about using security baselines, see:

- [Use security baselines](../protect/security-baselines.md)
- [Manage security baselines](../protect/security-baselines-configure.md).

**HoloLens 2 Standard security baseline (version 1)** - *January 2025*

<!-- This baseline isn't available via the security compliance toolkit at this time. Remove this, or add something similar with a link to the source baseline if one is available: 

For information about the most recent baseline versions and settings from Microsoft, including versions of this baseline that might not be available through Intune, download the [Microsoft Security Compliance Toolkit](https://www.microsoft.com/download/details.aspx?id=55319) from the Microsoft Download Center.
-->

## Account Management

- **Deletion Policy**  
  Baseline default: *Delete at both storage capacity threshold and profile inactivity threshold*  
  [Learn more](/windows/client-management/mdm/AccountManagement-csp/#userprofilemanagementdeletionpolicy)

- **Enable Profile Manager**  
  Baseline default: *True*  
  [Learn more](/windows/client-management/mdm/accountmanagement-csp#userprofilemanagementenableprofilemanager)

- **Profile Inactivity Threshold**  
  Baseline default: *Configured*  
  [Learn more](/windows/client-management/mdm/accountmanagement-csp#userprofilemanagementprofileinactivitythreshold)

- **Storage Capacity Start Deletion**  
  Baseline default: *Configured*  
  [Learn more](/windows/client-management/mdm/accountmanagement-csp#userprofilemanagementstoragecapacitystartdeletion)

- **Storage Capacity Stop Deletion**  
  Baseline default: *Configured*  
  [Learn more](/windows/client-management/mdm/accountmanagement-csp#userprofilemanagementstoragecapacitystopdeletion)

## Accounts

- **Allow Microsoft Account Connection**  
   Baseline default: *Block*  
  [Learn more](/windows/client-management/mdm/policy-csp-Accounts#allowmicrosoftaccountconnection)

## Administrative Templates

### System > Power Management > Video and Display Settings

- **Turn off the display (plugged in)**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-power#power-displayofftimeoutpluggedin)

  - **When plugged in, turn display off after (seconds)**  
     Baseline default: *30*

## Browser

- **Allow Autofill**  
  Baseline default: *Block*  
  [Learn more](/windows/client-management/mdm/policy-csp-Browser#allowautofill)

- **Allow Cookies**  
  Baseline default: *Block only cookies from third party websites*  
  [Learn more](/windows/client-management/mdm/policy-csp-Browser#allowcookies)

- **Allow Do Not Track**  
  Baseline default: *Block*  
  [Learn more](/windows/client-management/mdm/policy-csp-Browser#allowdonottrack)

- **Allow Password Manager**  
  Baseline default: *Block*  
  [Learn more](/windows/client-management/mdm/policy-csp-Browser#allowpasswordmanager)

- **Allow Popups**  
  Baseline default: *Block*  
  [Learn more](/windows/client-management/mdm/policy-csp-Browser#allowpopups)

- **Allow Search Suggestions in Address Bar**  
  Baseline default: *Block*  
  [Learn more](/windows/client-management/mdm/policy-csp-Browser#allowsearchsuggestionsinaddressbar)

- **Allow Smart Screen**  
  Baseline default: *Allow*  
  [Learn more](/windows/client-management/mdm/policy-csp-Browser#allowsmartscreen)

## Connectivity

- **Allow Bluetooth**  
   Baseline default: *Disallow Bluetooth. The radio in the Bluetooth control panel will be grayed out and the user will not be able to turn Bluetooth on.*  
  [Learn more](/windows/client-management/mdm/policy-csp-connectivity#allowbluetooth)

- **Allow USB Connection**  
  Baseline default: *Not allowed.*  
  [Learn more](/windows/client-management/mdm/policy-csp-connectivity#allowusbconnection)

## Device Lock

- **Device Password Enabled**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-devicelock#devicepasswordenabled)

  - **Max Device Password Failed Attempts**  
    Baseline default: *Configured*  
    Value: *10*  
    [Learn more](/windows/client-management/mdm/policy-csp-devicelock#maxdevicepasswordfailedattempts)

  - **Allow Idle Return Without Password**  
    Baseline default: *Not allowed.*  
    [Learn more](/windows/client-management/mdm/policy-csp-deviceLock#allowidlereturnwithoutpassword)

  - **Alphanumeric Device Password Required**  
    Baseline default: *Password or Numeric PIN required.*  
    [Learn more](/windows/client-management/mdm/policy-csp-devicelock#alphanumericdevicepasswordrequired)

  - **Max Inactivity Time Device Lock**  
    Baseline default: *Configured*  
    Value: *10*  
    [Learn more](/windows/client-management/mdm/policy-csp-devicelock#maxinactivitytimedevicelock)

  - **Device Password History**  
     Baseline default: *Configured*  
    Value: *15*  
    [Learn more](/windows/client-management/mdm/policy-csp-devicelock#devicepasswordhistory)

  - **Allow Simple Device Password**  
    Baseline default: *Not allowed.*  
    [Learn more](/windows/client-management/mdm/policy-csp-devicelock#allowsimpledevicepassword)

  - **Device Password Expiration**  
    Baseline default: *Not configured*  
    [Learn more](/windows/client-management/mdm/policy-csp-devicelock#devicepasswordexpiration)

  - **Min Device Password Length**  
    Baseline default: *Configured*  
    Value: *12*  
    [Learn more](/windows/client-management/mdm/policy-csp-devicelock#mindevicepasswordlength)

## Experience

- **Allow Manual MDM Unenrollment**  
  Baseline default: *Block*  
  [Learn more](/windows/client-management/mdm/policy-csp-Experience#allowmanualmdmunenrollment)

## Microsoft App Store

- **Allow All Trusted Apps**  
  Baseline default: *Explicit deny.*  
  [Learn more](/windows/client-management/mdm/policy-csp-ApplicationManagement#allowalltrustedapps)

- **Allow apps from the Microsoft app store to auto update**  
  Baseline default: *Allowed.*  
  [Learn more](/windows/client-management/mdm/policy-csp-ApplicationManagement#allowappstoreautoupdate)

- **Allow Developer Unlock**  
  Baseline default: *Explicit deny.*  
  [Learn more](/windows/client-management/mdm/policy-csp-ApplicationManagement#allowdeveloperunlock)

## Microsoft Edge

- **Block third party cookies**  
  Baseline default: *Enabled*

- **Configure Do Not Track**  
  Baseline default: *Disabled*

- **Enable AutoFill for addresses**  
  Baseline default: *Disabled*

- **Enable AutoFill for payment instruments**  
  Baseline default: *Disabled*

- **Enable search suggestions**  
  Baseline default: *Disabled*

- **Default pop-up window setting**  
  Baseline default: *Enabled*

  - **Default pop-up window setting (Device)**
    Baseline default: *Do not allow any site to show popups*

### Extensions

- **Control which extensions cannot be installed**  
  Baseline default: *Enabled*

  - **Extension IDs the user should be prevented from installing (or * for all) (Device)**  
    Baseline default: *

### Password manager and protection

- **Configures a setting that asks users to enter their device password while using password autofill**  
  Baseline default: *Enabled*

  - **Configures a setting that asks users to enter their device password while using password autofill (Device)**  
    Baseline default: *Autofill off*

- **Enable saving passwords to the password manager**  
  Baseline default: *Disabled*

### SmartScreen settings

- **Configure Microsoft Defender SmartScreen**  
  Baseline default: *Enabled*

## Mixed Reality

- **AAD Group Membership Cache Validity In Days**  
  Baseline default: *Configured*  
  Value: *7*  
  [Learn more](/windows/client-management/mdm/policy-csp-MixedReality#aadgroupmembershipcachevalidityindays)

## Privacy

- **Let Apps Access Account Info**  
  Baseline default: *Force deny.*  
  [Learn more](/windows/client-management/mdm/policy-csp-Privacy#letappsaccessaccountinfo)

- **Let Apps Access Account Info Force Allow These Apps**  
  Baseline default: *Configured*  
  Values:  
  - *Microsoft.Dynamics365.Guides_8wekyb3d8bbwe*
  - *Microsoft.MicrosoftRemoteAssist_8wekyb3d8bbwe*
  
  [Learn more](/windows/client-management/mdm/policy-csp-Privacy#letappsaccessaccountinfo_forceallowtheseapps)

- **Let Apps Access Background Spatial Perception**  
  Baseline default: *Force deny.*  
  [Learn more](/windows/client-management/mdm/policy-csp-Privacy#letappsaccessbackgroundspatialperception)

- **Let Apps Access Background Spatial Perception Force Allow These Apps**  
  Baseline default: *Configured*  
  - *Microsoft.Dynamics365.Guides_8wekyb3d8bbwe*
  - *Microsoft.MicrosoftRemoteAssist_8wekyb3d8bbwe*

  [Learn more](/windows/client-management/mdm/policy-csp-Privacy#letappsaccessbackgroundspatialperception_forceallowtheseapps)

- **Let Apps Access Camera**  
  Baseline default: *Force deny.*  
  [Learn more](/windows/client-management/mdm/policy-csp-Privacy#letappsaccesscamera)

- **Let Apps Access Camera Force Allow These Apps**  
  Baseline default: *Configured*  
  Values:  
  - *Microsoft.Dynamics365.Guides_8wekyb3d8bbwe*
  - *Microsoft.MicrosoftRemoteAssist_8wekyb3d8bbwe*

  [Learn more](/windows/client-management/mdm/policy-csp-Privacy#letappsaccesscamera_forceallowtheseapps)

- **Let Apps Access Microphone**  
  Baseline default: *Force deny.*  
  [Learn more](/windows/client-management/mdm/policy-csp-Privacy#letappsaccessmicrophone)

- **Let Apps Access Microphone Force Allow These Apps**  
  Baseline default: *Configured*  
  Values:  
  - *Microsoft.Dynamics365.Guides_8wekyb3d8bbwe*
  - *Microsoft.MicrosoftRemoteAssist_8wekyb3d8bbwe*

  [Learn more](/windows/client-management/mdm/policy-csp-Privacy#letappsaccessmicrophone_forceallowtheseapps)

## Search

- **Allow Search To Use Location**  
  Baseline default: *Block*  
  [Learn more](/windows/client-management/mdm/policy-csp-Search#allowsearchtouselocation)

## Security

- **Allow Add Provisioning Package**  
  Baseline default: *Block*  
  [Learn more](/windows/client-management/mdm/policy-csp-Security#allowaddprovisioningpackage)

## Settings

- **Allow VPN**  
  Baseline default: *Not allowed.*  
  [Learn more](/windows/client-management/mdm/policy-csp-Settings#allowvpn)

- **Page Visibility List**  
  Baseline default: *Configured*  
  [Learn more](/windows/client-management/mdm/policy-csp-Settings#pagevisibilitylist)

## System

- **Allow Storage Card**  
  Baseline default: *SD card use is not allowed and USB drives are disabled. This setting does not prevent programmatic access to the storage card.*  
  [Learn more](/windows/client-management/mdm/policy-csp-System#allowstoragecard)

- **Allow Telemetry**  
  Baseline default: *Security*  
  [Learn more](/windows/client-management/mdm/policy-csp-System#allowtelemetry)

## Tenant Lockdown

- **Require Network In OOBE (Device)**  
  Baseline default: *True*

## Wi-Fi Settings

- **Allow Manual Wi Fi Configuration**  
  Baseline default: *Allow*  
  [Learn more](/windows/client-management/mdm/policy-csp-wifi#allowmanualwificonfiguration)

> [!IMPORTANT]
>
> Allow or block connections to Wi-Fi outside of MDM server-installed networks. If you change this setting to Block, you must deploy enterprise Wi-Fi profiles to the device using the Wi-Fi CSP before you apply this setting. Otherwise, the device will go offline since it won't be able to connect to Wi-Fi. Note that choosing to block Wi-Fi connections will delete any previously installed user-configured Wi-Fi profiles from the device, though not all non-MDM profiles will be deleted. Learn more

## Windows Hello For Business

- **Lowercase Letters**  
  Baseline default: *Required*  
  [Learn more](/windows/client-management/mdm/PassportForWork-csp/#devicetenantidpoliciespincomplexitylowercaseletters)

- **Require Security Device**  
  Baseline default: *true*  
  [Learn more](/windows/client-management/mdm/passportforwork-csp#devicetenantidpoliciesrequiresecuritydevice)

- **Maximum PIN Length**  
  Baseline default: *Configured*  
  Value: *6*  
  [Learn more](/windows/client-management/mdm/passportforwork-csp#devicetenantidpoliciespincomplexitymaximumpinlength)

- **Disable Post Logon Provisioning (Windows Insiders only)**  
  Baseline default: *Not configured*  
  [Learn more](/windows/client-management/mdm/passportforwork-csp#devicetenantidpoliciesdisablepostlogonprovisioning)

- **Restrict use of TPM 1.2**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/passportforwork-csp#devicetenantidpoliciesexcludesecuritydevicestpm12)

- **PIN History**  
  Baseline default: *Configured*  
  [Learn more](/windows/client-management/mdm/passportforwork-csp#usertenantidpoliciespincomplexityhistory)

- **Special Characters**  
  Baseline default: *Requires the use of at least one special characters in PIN.*  
  [Learn more](/windows/client-management/mdm/passportforwork-csp#usertenantidpoliciespincomplexityspecialcharacters)

- **Minimum PIN Length**  
  Baseline default: *Configured*  
    Value: *6*  
  [Learn more](/windows/client-management/mdm/passportforwork-csp#usertenantidpoliciespincomplexityminimumpinlength)

- **Uppercase Letters**  
  Baseline default: *Required*  
  [Learn more](/windows/client-management/mdm/passportforwork-csp#usertenantidpoliciespincomplexityuppercaseletters)

- **Enable Windows Hello Provisioning For Security Keys (Windows Insiders only)**  
  Baseline default: *Not configured*  
  [Learn more](/windows/client-management/mdm/passportforwork-csp#devicetenantidpoliciesenablewindowshelloprovisioningforsecuritykeys)

- **Use Windows Hello For Business (Device)**  
  Baseline default: *true*  
  [Learn more](/windows/client-management/mdm/passportforwork-csp#devicetenantidpoliciesusepassportforwork)

- **Use Cloud Trust For On Prem Auth**  
  Baseline default: *Not configured*  
  [Learn more](/windows/client-management/mdm/passportforwork-csp#devicetenantidpoliciesusecloudtrustforonpremauth)

- **Expiration**  
  Baseline default: *Configured*  
    Value: *90*  
  [Learn more](/windows/client-management/mdm/passportforwork-csp#devicetenantidpoliciespincomplexityexpiration)

- **Use Remote Passport**  
  Baseline default: *Not configured*  
  [Learn more](/windows/client-management/mdm/passportforwork-csp#devicetenantidpoliciesremoteuseremotepassport)

- **Disable Post Logon Credential Caching (Windows Insiders only)**  
  Baseline default: *Not configured*  
  [Learn more](/windows/client-management/mdm/passportforwork-csp)

- **Use Hello Certificates As Smart Card Certificates**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/passportforwork-csp#devicetenantidpoliciesusehellocertificatesassmartcardcertificates)

- **Use Certificate For On Prem Auth**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/passportforwork-csp#devicetenantidpoliciesusecertificateforonpremauth)

- **Enable Pin Recovery**  
  Baseline default: *false*  
  [Learn more](/windows/client-management/mdm/passportforwork-csp#devicetenantidpoliciesenablepinrecovery)

- **Digits**  
  Baseline default: *Requires the use of at least one digits in PIN.*  
  [Learn more](/windows/client-management/mdm/passportforwork-csp#devicetenantidpoliciespincomplexitydigits)

## Windows Update For Business

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
