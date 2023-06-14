---
# required metadata

title: Settings list for the Windows 365 Cloud PC security baseline in Intune
titleSuffix: Microsoft Intune
description: View a list of the settings in the Microsoft Intune security baseline for Windows 365 Cloud PC. This list includes the default values for settings as found in the default configuration of the baseline.
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/13/2022
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology:
ms.assetid:
zone_pivot_groups: windows-365-baseline-versions

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
---

# List of the settings in the Windows 365 Cloud PC security baseline in Intune

This article is a reference for the settings that are available in the Windows 365 Cloud PC security baseline that you can deploy with Microsoft Intune. 

For each setting you’ll find the baselines default configuration, which is also the recommended configuration for that setting provided by the relevant security team. Because products and the security landscape evolve, the recommended defaults in one baseline version might not match the defaults you find in later versions of the same baseline. Different baseline types, like the *MDM security* and the *Defender for Endpoint* baselines, could also set different defaults.

When the Intune UI includes a *Learn more* link for a setting, you’ll find that here as well. Use that link to view the settings *policy configuration service provider* (CSP) or relevant content that explains the settings operation.

When a new version of a baseline becomes available, it replaces the previous version. Profiles instances that you’ve created prior to the availability of a new version:

- Become read-only. You can continue to use those profiles but can't edit them to change their configuration.
- Can be updated to the latest version. After you update a profile to the current baseline version, you can edit the profile to modify settings.

To learn more about using security baselines, see [Use security baselines](security-baselines.md). In that article you'll also find information about how to:

<!-- - [Compare baselines](../protect/security-baselines.md) to discover what's changed from version to version.  -->
- [Change the baseline version for a profile](../protect/security-baselines-configure.md#update-baselines-that-use-the-previous-format) to update a profile to use the latest version of that baseline.

**Windows 365 Cloud PC security baseline version 2110**

## Above Lock

- **Voice activate apps from locked screen**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-privacy?WT.mc_id=Portal-Microsoft_Intune_Workflows)  

- **Block display of toast notifications**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067101)  


## App Runtime

- **Microsoft accounts optional for Microsoft store apps**:  
  Baseline default: *Enabled*  
 [Learn more](https://go.microsoft.com/fwlink/?linkid=2067104)

## Application management

- **Block app installations with elevated privileges**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067134)

- **Block user control over installations**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067060)

- **Block game DVR (desktop only)**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067056)

## Attack Surface Reduction Rules

For general information, see [Learn about attack surface reduction rules](/microsoft-365/security/defender-endpoint/attack-surface-reduction?view=o365-worldwide&preserve-view=true).

- **Block Office communication apps from creating child processes**:  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=874499)

- **Block Adobe Reader from creating child processes**:  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=853979)

- **Block Office applications from injecting code into other processes**:  
  Baseline default: *Block*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872974)

- **Block Office applications from creating executable content**:  
  Baseline default: *Block*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872975)

- **Block JavaScript or VBScript from launching downloaded executable content**:  
  Baseline default: *Block*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872979)

- **Enable network protection**:  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872618)

- **Block untrusted and unsigned processes that run from USB**:  
  Baseline default: *Block*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=874502)

- **Block credential stealing from the Windows local security authority subsystem (lsass.exe)**:  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=874499)

- **Block all Office applications from creating child processes**:  
  Baseline default: *Block*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872976)

- **Block execution of potentially obfuscated scripts (js/vbs/ps)**:  
  Baseline default: *Block*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872978)

- **Block Win32 API calls from Office macro**:  
  Baseline default: *Block*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872977)

- **Block executable content download from email and webmail clients**:  
  Baseline default: *Block*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872980)

## Audit

Audit settings configure the events that are generated for the conditions of the setting.

- **Account Logon Audit Credential Validation (Device)**:  
  Baseline default: *Success and Failure*  

- **Account Logon Audit Kerberos Authentication Service (Device)**:  
   Baseline default: *None*  

- **Account Logon Logoff Audit Account Lockout (Device)**:  
  Baseline default: *Failure*  

- **Account Logon Logoff Audit Group Membership (Device)**:  
  Baseline default: *Success*  

- **Account Logon Logoff Audit Logon (Device)**:  
  Baseline default: *Success and Failure*  

- **Audit Other Logon Logoff Events (Device)**:  
  Baseline default: *Success and Failure*  

- **Audit Special Logon (Device)**:  
  Baseline default: *Success*  

- **Audit Security Group Management (Device)**:  
  Baseline default: *Success*  

- **Audit User Account Management (Device)**:  
  Baseline default: *Success and Failure*  

- **Detailed Tracking Audit PNP Activity (Device)**:  
  Baseline default: *Success*  

- **Detailed Tracking Audit Process Creation (Device)**:  
  Baseline default: *Success*  

- **Object Access Audit Detailed File Share (Device)**:  
  Baseline default: *Failure*  

- **Audit File Share Access (Device)**:  
  Baseline default: *Success and Failure*  

- **Object Access Audit Other Object Access Events (Device)**:  
  Baseline default: *Success and Failure*  

- **Object Access Audit Removable Storage (Device)**:  
  Baseline default: *Success and Failure*  

- **Audit Authentication Policy Change (Device)**:  
  Baseline default: *Success*  

- **Policy Change Audit MPSSVC Rule Level Policy Change (Device)**:  
  Baseline default: *Success and Failure*  

- **Policy Change Audit Other Policy Change Events (Device)**:  
  Baseline default: *Failure*  

- **Audit Changes to Audit Policy (Device)**:  
  Baseline default: *Success*  

- **Privilege Use Audit Sensitive Privilege Use (Device)**:  
  Baseline default: *Success and Failure*  

- **System Audit Other System Events (Device)**:  
  Baseline default: *Success and Failure*  

- **System Audit Security State Change (Device)**:  
  Baseline default: *Success*  

- **Audit Security System Extension (Device)**:  
  Baseline default: *Success*  

- **System Audit System Integrity (Device)**:  
  Baseline default: *Success and Failure*  

## Auto Play

- **Auto play default auto run behavior**:  
  Baseline default: *Do not execute*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067133)

- **Auto play mode**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2066793)

- **Block auto play for non-volume devices**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067106)

## Browser

- **Block Password Manager**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067128)

- **Require SmartScreen for Microsoft Edge Legacy**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067029)

- **Block malicious site**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067040)

- **Block unverified file download**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067023)

- **Prevent user from overriding certificate errors**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067126)

## Connectivity

- **Configure secure access to UNC paths**:  
  Baseline default: *Configure Windows to only allow access to the specified UNC paths after fulfilling additional security requirements*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067243)  

  - **Hardened UNC path list**:  
    *Not configured by default. Manually add one or more hardened UNC paths.*

- **Block downloading of print drivers over HTTP**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067141)

- **Block Internet download for web publishing and online ordering wizards**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067136)

## Credentials Delegation

- **Remote host delegation of non-exportable credentials**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067103)

## Credentials UI

- **Enumerate administrators**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067021)

## Device Guard

- **Virtualization based security**:  
  Baseline default: *Enable VBS with secure boot*  

- **Enable virtualization based security**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067066)

- **Launch system guard**:  
  Baseline default: *Enabled*  

- **Turn on Credential Guard**:  
  Baseline default: *Enable with UEFI lock*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872424)

## Device Installation

- **Block hardware device installation by setup classes**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067048)

  - **Remove matching hardware devices**  
    Baseline default: *Yes*

  - **Block list**  
    *Not configured by default. Manually add one or more Identifiers.*

## DMA Guard

- **Enumeration of external devices incompatible with Kernel DMA Protection**  
  Baseline default: *Block all*

## Event Log Service

- **Application log maximum file size in KB**  
  Baseline default: *32768*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067125)

- **System log maximum file size in KB**  
  Baseline default: *32768*  
  [Learn more](https://www.bing.com/?ref=go&linkid=2066798)

- **Security log maximum file size in KB**  
  Baseline default: *196608*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067042)

## Experience

- **Block Windows Spotlight**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067037)


## File Explorer

- **Block data execution prevention**  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067043)

- **Block heap termination on corruption**  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067107)

## Firewall

For more information, see [2.2.2 FW_PROFILE_TYPE](https://go.microsoft.com/fwlink/?linkid=2066796) in the Windows Protocols documentation.

- **Firewall profile domain**:  
  Baseline default: *Configure*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2066796)

  - **Inbound connections blocked**:  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872564)

  - **Outbound connections required**:  
    Baseline default: *Yes*  
    [Learn more](https://aka.ms/intune-firewall-outboundaction)

  - **Inbound notifications blocked**:  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872563)

  - **Firewall enabled**:  
    Baseline default: *Allowed*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872558)

- **Firewall profile private**:  
  Baseline default: *Configure*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067041)

  - **Inbound connections blocked**:  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872564)

  - **Outbound connections required**:  
    Baseline default: *Yes*  
    [Learn more](https://aka.ms/intune-firewall-outboundaction)

  - **Inbound notifications blocked**:  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872563)

  - **Firewall enabled**:  
    Baseline default: *Allowed*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872558)

- **Firewall profile public**:  
  Baseline default: *Configure*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067143)

  - **Inbound connections blocked**:  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872564)

  - **Outbound connections required**:  
    Baseline default: *Yes*  
    [Learn more](https://aka.ms/intune-firewall-outboundaction)

  - **Inbound notifications blocked**:  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872563)

  - **Firewall enabled**:  
    Baseline default: *Allowed*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872558)

  - **Connection security rules from group policy not merged**:  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872568)

  - **Policy rules from group policy not merged**:  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872567)

## Internet Explorer

View the full list of [Internet Explorer CSPs](/windows/client-management/mdm/policy-csp-internetexplorer).

- **Internet Explorer encryption support**  
  Baseline defaults: Two items: *TLS v1.1* and *TLS v1.2*

  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067057)

- **Internet Explorer prevent managing smart screen filter**  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067135)

- **Internet Explorer restricted zone script Active X controls marked safe for scripting**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067062)

- **Internet Explorer restricted zone file downloads**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067038)

- **Internet Explorer certificate address mismatch warning**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067153)

- **Internet Explorer enhanced protected mode**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067158)

- **Internet Explorer fallback to SSL3**  
  Baseline default: *No sites*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067118)

- **Internet Explorer software when signature is invalid**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067201)

- **Internet Explorer check server certificate revocation**  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067046)

- **Internet Explorer check signatures on downloaded programs**  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067051)

- **Internet Explorer processes consistent MIME handling**  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067144)

- **Internet Explorer bypass smart screen warnings**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067159)

- **Internet Explorer bypass smart screen warnings about uncommon files**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067068)

- **Internet Explorer crash detection**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067094)

- **Internet Explorer download enclosures**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067245)

- **Internet Explorer ignore certificate errors**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067071)

- **Internet Explorer disable processes in enhanced protected mode**  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067149)

- **Internet Explorer security settings check**  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067182)

- **Internet Explorer Active X controls in protected mode**  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067145)

- **Internet Explorer users adding sites**  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067167)

- **Internet Explorer users changing policies**  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067155)

- **Internet Explorer block outdated Active X controls**  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067203)

- **Internet Explorer include all network paths**  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067090)

- **Internet Explorer internet zone access to data sources**  
  Baseline default: *Disable*  
  [Learn more](https://www.bing.com/?ref=go&linkid=2067078)

- **Internet Explorer internet zone automatic prompt for file downloads**  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067117)

- **Internet Explorer internet zone copy and paste via script**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067084)

- **Internet Explorer internet zone drag and drop or copy and paste files**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067076)

- **Internet Explorer internet zone less privileged sites**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067109)

- **Internet Explorer internet zone loading of XAML files**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067147)

- **Internet Explorer internet zone .NET Framework reliant components**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067073)

- **Internet Explorer internet zone allows only approved domains to use ActiveX controls**  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067091)

- **Internet Explorer internet zone allows only approved domains to use tdc ActiveX controls**  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067091)

- **Internet Explorer internet zone scripting of web browser controls**  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067157)

- **Internet Explorer internet zone script initiated windows**  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067088)

- **Internet Explorer internet zone scriptlets**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067176)

- **Internet Explorer internet zone smart screen**  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067047)

- **Internet Explorer internet zone updates to status bar via script**  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067087)

- **Internet Explorer internet zone user data persistence**  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067156)

- **Internet Explorer internet zone allows VBscript to run**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067119)

- **Internet Explorer internet zone do not run antimalware against ActiveX controls**  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067162)

- **Internet Explorer internet zone download signed ActiveX controls**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067064)

- **Internet Explorer internet zone download unsigned ActiveX controls**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067325)
- **Internet Explorer internet zone cross site scripting filter**  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067053)

- **Internet Explorer internet zone drag content from different domains across windows**  
  Baseline default: *Disabled*  
  [Learn more](https://www.bing.com/?ref=go&linkid=2067093)

- **Internet Explorer internet zone drag content from different domains within windows**  
  Baseline default: *Disabled*  
 [Learn more](https://www.bing.com/?ref=go&linkid=2067095)

- **Internet Explorer internet zone protected mode**  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067171)

- **Internet Explorer internet zone include local path when uploading files to server**  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067072)

- **Internet Explorer internet zone initialize and script Active X controls not marked as safe**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067170)

- **Internet Explorer internet zone java permissions**  
  Baseline default: *Disable java*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067174)

- **Internet Explorer internet zone launch applications and files in an iframe**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067020)

- **Internet Explorer internet zone logon options**  
  Baseline default: *Prompt*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067194)

- **Internet Explorer internet zone navigate windows and frames across different domains**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067083)

- **Internet Explorer internet zone run .NET Framework reliant components signed with Authenticode**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067033)

- **Internet Explorer internet zone security warning for potentially unsafe files**  
  Baseline default: *Prompt*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067204)

- **Internet Explorer internet zone popup blocker**  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067069)

- **Internet Explorer intranet zone do not run antimalware against Active X controls**  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067138)

- **Internet Explorer intranet zone initialize and script Active X controls not marked as safe**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067175)

- **Internet Explorer intranet zone java permissions**  
  Baseline default: *High safety*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067206)

- **Internet Explorer local machine zone do not run antimalware against Active X controls**  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067152)

- **Internet Explorer local machine zone java permissions**  
  Baseline default: *Disable java*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067113)

- **Internet Explorer locked down internet zone smart screen**  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067059)

- **Internet Explorer locked down intranet zone java permissions**  
  Baseline default: *Disable java*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067082)

- **Internet Explorer locked down local machine zone java permissions**  
  Baseline default: *Disable java*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067253)

- **Internet Explorer locked down restricted zone smart screen**  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067092)

- **Internet Explorer locked down restricted zone java permissions**  
  Baseline default: *Disable java*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067181)

- **Internet Explorer locked down trusted zone java permissions**  
  Baseline default: *Disable java*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067142)

- **Internet Explorer processes MIME sniffing safety feature**  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067124)

- **Internet Explorer processes MK protocol security restriction**  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067179)

- **Internet Explorer processes notification bar**  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067139)

- **Internet Explorer prevent per user installation of Active X controls**  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067058)

- **Internet Explorer processes protection from zone elevation**  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067160)

- **Internet Explorer remove run this time button for outdated Active X controls**  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067123)

- **Internet Explorer processes restrict Active X install**  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067250)

- **Internet Explorer restricted zone access to data sources**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067161)

- **Internet Explorer restricted zone active scripting**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067172)

- **Internet Explorer restricted zone automatic prompt for file downloads**  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067150)

- **Internet Explorer restricted zone binary and script behaviors**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067224)

- **Internet Explorer restricted zone copy and paste via script**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067165)

- **Internet Explorer restricted zone drag and drop or copy and paste files**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067096)

- **Internet Explorer restricted zone less privileged sites**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067148)

- **Internet Explorer restricted zone loading of XAML files**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067070)

- **Internet Explorer restricted zone meta refresh**  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067154)

- **Internet Explorer restricted zone .NET Framework reliant components**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067077)

- **Internet Explorer restricted zone allows only approved domains to use Active X controls**  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067233)

- **Internet Explorer restricted zone allows only approved domains to use tdc Active X controls**  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067032)

- **Internet Explorer restricted zone scripting of web browser controls**  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067098)

- **Internet Explorer restricted zone script initiated windows**  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067075)

- **Internet Explorer restricted zone scriptlets**  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067112)

- **Internet Explorer restricted zone smart screen**  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067034)

- **Internet Explorer restricted zone updates to status bar via script**  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067081)

- **Internet Explorer restricted zone user data persistence**  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067081)

- **Internet Explorer restricted zone allows vbscript to run**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067173)

- **Internet Explorer restricted zone do not run antimalware against Active X controls**  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067089)

- **Internet Explorer restricted zone download signed Active X controls**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067120)

- **Internet Explorer restricted zone download unsigned Active X controls**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067177)

- **Internet Explorer restricted zone cross site scripting filter**  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067178)

- **Internet Explorer restricted zone drag content from different domains across windows**  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067166)

- **Internet Explorer restricted zone drag content from different domains within windows**  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067079)

- **Internet Explorer restricted zone include local path when uploading files to server**  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067085)

- **Internet Explorer restricted zone initialize and script Active X controls not marked as safe**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067097)

- **Internet Explorer restricted zone java permissions**  
  Baseline default: *Disable java*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067132)

- **Internet Explorer restricted zone launch applications and files in an iFrame**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067061)

- **Internet Explorer restricted zone logon options**  
  Baseline default: *Anonymous*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067110)

- **Internet Explorer restricted zone navigate windows and frames across different domains**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067050)

- **Internet Explorer restricted zone run Active X controls and plugins**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067114)

- **Internet Explorer restricted zone run .NET Framework reliant components signed with Authenticode**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067169)

- **Internet Explorer restricted zone scripting of java applets**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067202)

- **Internet Explorer restricted zone security warning for potentially unsafe files**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2066797)

- **Internet Explorer restricted zone protected mode**  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067080)

- **Internet Explorer restricted zone popup blocker**  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067180)

- **Internet Explorer processes restrict file download**  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067164)

- **Internet Explorer processes scripted window security restrictions**  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067146)

- **Internet Explorer security zones use only machine settings**  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067086)

- **Internet Explorer use Active X installer service**  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067163)

- **Internet Explorer trusted zone do not run antimalware against Active X controls**  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067115)

- **Internet Explorer trusted zone initialize and script Active X controls not marked as safe**  
  Baseline default: *Disable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067137)

- **Internet Explorer trusted zone java permissions**  
  Baseline default: *High safety*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067200)

- **Internet Explorer auto complete**  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067122)

## Local Policies Security Options

- **Block remote logon with blank password**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067219)

- **Minutes of lock screen inactivity until screen saver activates**  
  Baseline default: *15*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067210)

- **Smart card removal behavior**  
  Baseline default: *Lock workstation*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067331)

- **Require client to always digitally sign communications**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067187)

- **Prevent clients from sending unencrypted passwords to third party SMB servers**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067235)

- **Require server digitally signing communications always**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067319)

- **Prevent anonymous enumeration of SAM accounts**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067318)

- **Block anonymous enumeration of SAM accounts and shares**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067191)

- **Restrict anonymous access to named pipes and shares**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067212)

- **Allow remote calls to security accounts manager**  
  Baseline default: *O:BAG:BAD:(A;;RC;;;BA)*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067209)

- **Prevent storing LAN manager hash value on next password change**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067213)

- **Authentication level**  
  Baseline default: *Send NTLMv2 response only. Refuse LM and NTLM*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067189)

- **Minimum session security for NTLM SSP based clients**  
  Baseline default: *Require NTLM V2 and 128 bit encryption*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067324)

- **Minimum session security for NTLM SSP based servers**  
  Baseline default: *Require NTLM V2 and 128 bit encryption*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067246)

- **Administrator elevation prompt behavior**  
  Baseline default: *Prompt for consent on the secure desktop*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067215)

- **Standard user elevation prompt behavior**  
  Baseline default: *Automatically deny elevation requests*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067183)

- **Detect application installations and prompt for elevation**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067208)

- **Only allow UI access applications for secure locations**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067185)

- **Require admin approval mode for administrators**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067184)

- **Use admin approval mode**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067186)

- **Virtualize file and registry write failures to per user locations**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067321)

## Microsoft Defender

- **Turn on real-time protection**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2114050)

- **Scan scripts that are used in Microsoft browsers**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2114054)

- **Additional amount of time (0-50 seconds) to extend cloud protection timeout**  
  Baseline default: *50*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2113940)

- **Scan all downloaded files and attachments**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2113934)

- **Scan type**  
  Baseline default: *Quick scan*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2114045)

- **Defender schedule scan day**  
  Baseline default: *Everyday*  

- **Scheduled scan start time**  
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

## Microsoft Defender Antivirus Exclusions

- **Defender Processes to exclude**  
  Baseline defaults:  *Not configured by default. Manually add one or more entries.*

- **File extensions to exclude from scans and real-time protection**  
  Baseline defaults:  *Not configured by default. Manually add one or more entries.*

- **Defender Files And Folders To Exclude**  
  Baseline default:  *Not configured by default. Manually add one or more entries.*

## Microsoft Edge

- **Control which extensions cannot be installed**  
  Baseline default: *Enabled*  

  - **Extension IDs the user should be prevented from installing (or * for all)**  
    Baseline default: *Not configured by default. Manually add one or more IDs*  

- **Allow user-level native messaging hosts (installed without admin permissions)**  
  Baseline default: *Disabled*  

- **Minimum SSL version enabled**  
  Baseline default: *Enabled*  

  - **Minimum SSL version enabled**  
    Baseline default: *TLS 1.2*  

- **Allow users to proceed from the SSL warning page**  
  Baseline default: *Disabled*  

- **Configure Microsoft Defender SmartScreen**  
  Baseline default: *Enabled*  

- **Prevent bypassing Microsoft Defender SmartScreen prompts for sites**  
  Baseline default: *Enabled*  

- **Prevent bypassing of Microsoft Defender SmartScreen warnings about downloads**  
  Baseline default: *Enabled*  

- **Configure Microsoft Defender SmartScreen to block potentially unwanted apps**  
  Baseline default: *Enabled*  

- **Default Adobe Flash setting**  
  Baseline default: *Enabled*  

  - **Default Adobe Flash setting**  
    Baseline default: *Block the Adobe Flash plugin*  

- **Enable saving passwords to the password manager**  
  Baseline default: *Disabled*  

- **Enable site isolation for every site**  
  Baseline default: *Enabled*  

- **Supported authentication schemes**  
  Baseline default: *Enabled*  

  - **Supported authentication schemes**  
    Baseline defaults: Two items: *NTLM* and *Negotiate*

## MS Security Guide

- **SMB v1 client driver start configuration**  
  Baseline default: *Disable driver*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067214)

- **Apply UAC restrictions to local accounts on network logon**  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067188)

- **Structured exception handling overwrite protection**  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067217)

- **SMB v1 server**  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067190)

- **Digest authentication**  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067193)

## MSS Legacy

- **Network IPv6 source routing protection level**  
  Baseline default: *Highest protection*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067216)

- **Network IP source routing protection level**  
  Baseline default: *Highest protection*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067220)

- **Network ignore NetBIOS name release requests except from WINS servers**  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067218)

- **Network ICMP redirects override OSPF generated routes**  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067326)

## Remote Assistance

- **Remote Assistance solicited**
   Baseline default: *Disable Remote Assistance*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067198)

## Remote Desktop Services

- **Remote desktop services client connection encryption level**  
  Baseline default: *High*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067222)

- **Block drive redirection**  
  Baseline default: *Enabled*  

- **Block password saving**  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067301)

- **Prompt for password upon connection**  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067328)

- **Secure RPC communication**  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067248)

## Remote Management

- **Block client digest authentication**  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067302)

- **Block storing run as credentials**  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067300)

- **Client basic authentication**  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067252)

- **Basic authentication**  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067223)

- **Client unencrypted traffic**  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067304)

- **Unencrypted traffic**  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067226)

## Remote Procedure Call

- **RPC unauthenticated client options**  
  Baseline default: *Authenticated*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067225)

## Search

- **Disable indexing encrypted items**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067303)

## Smart Screen

- **Turn on Windows SmartScreen**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872784)

- **Block users from ignoring SmartScreen warnings**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872783)

## System

- **System boot start driver initialization**  
  Baseline default: *Good unknown and bad critical*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067307)
## Windows Connection Manager

- **Block connection to non-domain networks**  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067323)

## Windows Ink Workspace

- **Ink Workspace**  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067241)

## Windows PowerShell

- **PowerShell script block logging**  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067330)

## Windows Security

- **Enable tamper protection to prevent Microsoft Defender being disabled**  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2066083)
