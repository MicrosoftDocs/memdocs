---
# required metadata

title: Settings list for the Windows 10/11 MDM security baselines in Microsoft Intune
titleSuffix: Microsoft Intune
description: View the list of settings in the Microsoft Intune security baseline for Windows 10/11 MDM security. This list includes the default values for settings as found in the default configuration of the baseline.
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/11/2024
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium

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
zone_pivot_groups: windows-mdm-versions
---


# List of the settings in the Windows 10/11 MDM security baseline in Intune

This article is a reference for the settings that are available in the different versions of the Windows 10/11 MDM security baseline that you can deploy with Microsoft Intune. You can use the tabs below to select and view the settings in the current baseline version and a few older versions that might still be in use.

For each setting you’ll find the baselines default configuration, which is also the recommended configuration for that setting provided by the relevant security team. Because products and the security landscape evolve, the recommended defaults in one baseline version might not match the defaults you find in later versions of the same baseline. Different baseline types, like the *MDM security* and the *Defender for Endpoint* baselines, could also set different defaults.

When the Intune UI includes a *Learn more* link for a setting, you’ll find that here as well. Use that link to view the settings *policy configuration service provider* (CSP) or relevant content that explains the settings operation.

When a new version of a baseline becomes available, it replaces the previous version. Profiles instances that you’ve created prior to the availability of a new version:

- Become read-only. You can continue to use those profiles but can't edit them to change their configuration.
- Can be updated to the latest version. After you update a profile to the current baseline version, you can edit the profile to modify settings.

To learn more about using security baselines, see [Use security baselines](security-baselines.md). In that article you'll also find information about how to:

<!-- - [Compare baselines](../protect/security-baselines.md) to discover what's changed from version to version.  -->
- [Change the baseline version for a profile](../protect/security-baselines-configure.md#update-baselines-that-use-the-previous-format) to update a profile to use the latest version of that baseline.

::: zone pivot="mdm-november-2021"
**Security Baseline for Windows 10/11 for November 2021**
::: zone-end
::: zone pivot="mdm-december-2020"
**Security Baseline for Windows 10/11 for December 2020**
::: zone-end
::: zone pivot="mdm-august-2020"
**Security Baseline for Windows 10 and later for August 2020**
::: zone-end

## Above Lock

::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

- **Voice activate apps from locked screen**:  
  Baseline default: *Disabled*  
  [Learn More](/windows/client-management/mdm/policy-csp-privacy)

- **Block display of toast notifications**:  
  Baseline default: *Yes*  
  [Learn More](/windows/client-management/mdm/policy-csp-abovelock#abovelock-allowtoasts)  

::: zone-end

## App Runtime

::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

- **Microsoft accounts optional for Microsoft store apps**:  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-appruntime#appruntime-allowmicrosoftaccountstobeoptional)

::: zone-end

## Application Management

::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

- **Block app installations with elevated privileges**:  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-msialwaysinstallwithelevatedprivileges)

- **Block user control over installations**:  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-msiallowusercontroloverinstall)

- **Block game DVR (desktop only)**:  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowgamedvr)

::: zone-end

## Audit

::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

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

::: zone-end

## Auto Play

::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

- **Auto play default auto run behavior**:  
  Baseline default: *Do not execute*  
  [Learn more](/windows/client-management/mdm/policy-csp-autoplay#autoplay-setdefaultautorunbehavior)

- **Auto play mode**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-autoplay#autoplay-turnoffautoplay)

- **Block auto play for non-volume devices**:  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-autoplay#autoplay-disallowautoplayfornonvolumedevices) 

::: zone-end

## BitLocker

::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

- **BitLocker removable drive policy**:  
  Baseline default: *Configure*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067140)

  - **Block write access to removable data-drives not protected by BitLocker**:  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872540)

::: zone-end

## Browser

::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

- **Block Password Manager**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067128)

- **Require SmartScreen for Microsoft Edge Legacy**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067029)

- **Block malicious site access**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067040)

- **Block unverified file download**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067023)

- **Prevent user from overriding certificate errors**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067126)

::: zone-end

## Connectivity

::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

- **Configure secure access to UNC paths**:  
  Baseline default: *Configure Windows to only allow access to the specified UNC paths after fulfilling additional security requirements*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067243)

  - **Hardened UNC path list**:  
    Baseline default: *Not configured by default. Manually add one or more hardened UNC paths.*

- **Block downloading of print drivers over HTTP**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067141)

- **Block Internet download for web publishing and online ordering wizards**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067136)

::: zone-end

## Credentials Delegation

::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

- **Remote host delegation of non-exportable credentials**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067103)

::: zone-end

## Credentials UI

::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

- **Enumerate administrators**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067021)

::: zone-end

## Data Protection

::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

- **Block direct memory access**:  
  Baseline default: Yes  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067031)

::: zone-end

## Device Guard

::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

- **Virtualization based security**:  
  Baseline default: *Enable VBS with secure boot*

- **Enable virtualization based security**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067066)

- **Launch system guard**:  
  Baseline default: *Enabled*

- **Turn on credential guard**:  
  Baseline default: *Enable with UEFI lock*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872424)

::: zone-end

## Device Installation

::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

- **Block hardware device installation by setup classes**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067048)

  - **Remove matching hardware devices**:  
    Baseline default: *Yes*

  - **Block list**:  
    Baseline default: *Not configured by default. Manually add one or more Identifiers.*

::: zone-end
::: zone pivot="mdm-august-2020"

- **Hardware device installation by device identifiers**:  
  Baseline default: *Block hardware device installation*  
  [Learn more](/windows/client-management/mdm/policy-csp-deviceinstallation#deviceinstallation-preventinstallationofmatchingdeviceids)

  - **Remove matching hardware devices**:  
    Baseline default: *Yes*

  - **Hardware device identifiers that are blocked**:  
    Baseline default: *Yes*

- **Hardware device installation by setup classes**:  
  Baseline default: *Block hardware device installation*  
  [Learn more](/windows/client-management/mdm/policy-csp-deviceinstallation#deviceinstallation-preventinstallationofmatchingdevicesetupclasses)

  - **Remove matching hardware devices**:  
    Baseline default:  *No default configuration*

  - **Hardware device identifiers that are blocked**:  
    Baseline default: *No default configuration*

::: zone-end

## Device Lock

::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

- **Require password**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067049)  

  - **Required password**:  
    Baseline default: *Alphanumeric*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=2067027)

  - **Password expiration (days)**:  
    Baseline default: *60*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=2067028)

  - **Password minimum character set count**:  
    Baseline default: *3*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=2067055)

  - **Prevent reuse of previous passwords**:  
    Baseline default: *24*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=2066795)

  - **Minimum password length**:  
    Baseline default: *8*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=2067024)

  - **Number of sign-in failures before wiping device**:  
    Baseline default: *10*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=2067030)

  - **Block simple passwords**:  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=2067127)

- **Password minimum age in days**:  
  Baseline default: *1*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067022)

- **Prevent use of camera**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067052)

- **Prevent slide show**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067105)

::: zone-end

## DMA Guard

::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

- **Enumeration of external devices incompatible with Kernel DMA Protection**:  
  Baseline default: *Block all*

::: zone-end

## Event Log Service

::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

- **Application log maximum file size in KB**:  
  Baseline default: *32768*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067125)

- **System log maximum file size in KB**:  
  Baseline default: *32768*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2066798)

- **Security log maximum file size in KB**:  
  Baseline default: *196608*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067042)

::: zone-end

## Experience

::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

- **Block Windows Spotlight**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067037)

  - **Block third-party suggestions in Windows Spotlight**:  
    Baseline default: *Not configured*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=2067045)

  - **Block consumer specific features**:  
    Baseline default: *Not configured*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=2067054)

::: zone-end
::: zone pivot="mdm-august-2020"

## Exploit Guard

- **Upload XML**:  
  Baseline default: *Sample xml is provided*  
  [Learn more](/windows/client-management/mdm/policy-csp-exploitguard#exploitguard-exploitprotectionsettings)

::: zone-end

## File Explorer

::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

- **Block data execution prevention**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067043)

- **Block heap termination on corruption**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067107)

::: zone-end

## Firewall

::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

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
  [Learn more](/openspecs/windows_protocols/ms-fasp/7704e238-174d-4a5e-b809-5f3787dd8acc)

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

::: zone-end

## Internet Explorer
<!-- /windows/client-management/mdm/policy-csp-internetexplorer -->
::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

- **Internet Explorer encryption support**:  
  Baseline default: Two items:  *TLS v1.1* and *TLS v1.2*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#disableencryptionsupport)

- **Internet Explorer prevent managing smart screen filter**:  
  Baseline default: *Enable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetzoneallowsmartscreenie)

- **Internet Explorer restricted zone script Active X controls marked safe for scripting**:  
  Baseline default: *Disable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszoneinitializeandscriptactivexcontrols)

- **Internet Explorer restricted zone file downloads**:  
  Baseline default: *Disable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszoneallowfiledownloads)

- **Internet Explorer certificate address mismatch warning**:  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#allowcertificateaddressmismatchwarning)  

- **Internet Explorer enhanced protected mode**:  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#allowenhancedprotectedmode)

- **Internet Explorer fallback to SSL3**:  
  Baseline default: *No sites*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#allowfallbacktossl3)

- **Internet Explorer software when signature is invalid**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#allowsoftwarewhensignatureisinvalid)

- **Internet Explorer check server certificate revocation**:  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#checkservercertificaterevocation)

- **Internet Explorer check signatures on downloaded programs**:  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#checksignaturesondownloadedprograms)

- **Internet Explorer processes consistent MIME handling**:  
  Baseline default: *Enable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#consistentmimehandlinginternetexplorerprocesses)  

- **Internet Explorer bypass smart screen warnings**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#disablebypassofsmartscreenwarnings)

- **Internet Explorer bypass smart screen warnings about uncommon files**:  
  Baseline default: *Disable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#disablebypassofsmartscreenwarningsaboutuncommonfiles)

- **Internet Explorer crash detection**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#disablecrashdetection)

- **Internet Explorer download enclosures**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#disableenclosuredownloading)

- **Internet Explorer ignore certificate errors**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#disableignoringcertificateerrors)

- **Internet Explorer disable processes in enhanced protected mode**:  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#disableprocessesinenhancedprotectedmode)

- **Internet Explorer security settings check**:  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#disablesecuritysettingscheck)

- **Internet Explorer Active X controls in protected mode**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#donotallowactivexcontrolsinprotectedmode)

- **Internet Explorer users adding sites**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#donotallowuserstoaddsites)

- **Internet Explorer users changing policies**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#donotallowuserstochangepolicies)

- **Internet Explorer block outdated Active X controls**:  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#donotblockoutdatedactivexcontrols)

- **Internet Explorer include all network paths**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#includeallnetworkpaths)

- **Internet Explorer internet zone access to data sources**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetzoneallowaccesstodatasources)  

- **Internet Explorer internet zone automatic prompt for file downloads**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetzoneallowautomaticpromptingforfiledownloads)

- **Internet Explorer internet zone copy and paste via script**:  
  Baseline default: *Disable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetzoneallowcopypasteviascript)

- **Internet Explorer internet zone drag and drop or copy and paste files**:  
  Baseline default: *Disabled*.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetzoneallowdraganddropcopyandpastefiles)

- **Internet Explorer internet zone less privileged sites**:  
  Baseline default: *Disable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetzoneallowlessprivilegedsites)

- **Internet Explorer internet zone loading of XAML files**:  
  Baseline default: *Disable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetzoneallowloadingofxamlfiles)

- **Internet Explorer internet zone .NET Framework reliant components**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetzoneallownetframeworkreliantcomponents)

- **Internet Explorer internet zone allow only approved domains to use ActiveX controls**:  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetzoneallowonlyapproveddomainstouseactivexcontrols)

- **Internet Explorer internet zone allow only approved domains to use tdc ActiveX controls**:  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetzoneallowonlyapproveddomainstousetdcactivexcontrol)

- **Internet Explorer internet zone scripting of web browser controls**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetzoneallowscriptingofinternetexplorerwebbrowsercontrols)

- **Internet Explorer internet zone script initiated windows**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetzoneallowscriptinitiatedwindows)

- **Internet Explorer internet zone scriptlets**:  
  Baseline default: *Disable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetzoneallowscriptlets)

- **Internet Explorer internet zone smart screen**:  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetzoneallowsmartscreenie)

- **Internet Explorer internet zone updates to status bar via script**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetzoneallowupdatestostatusbarviascript)

- **Internet Explorer internet zone user data persistence**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetzoneallowuserdatapersistence)

- **Internet Explorer internet zone allow VBscript to run**:  
  Baseline default: *Disable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetzoneallowvbscripttorunininternetexplorer)

- **Internet Explorer internet zone do not run antimalware against ActiveX controls**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetzonedonotrunantimalwareagainstactivexcontrols)

- **Internet Explorer internet zone download signed ActiveX controls**:  
  Baseline default: *Disable*Baseline default: *Disable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetzonedownloadsignedactivexcontrols)

- **Internet Explorer internet zone download unsigned ActiveX controls**:  
  Baseline default: *Disable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetzonedownloadunsignedactivexcontrols)

- **Internet Explorer internet zone cross site scripting filter**:  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetzoneenablecrosssitescriptingfilter)

- **Internet Explorer internet zone drag content from different domains across windows**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetzoneenabledraggingofcontentfromdifferentdomainsacrosswindows)

- **Internet Explorer internet zone drag content from different domains within windows**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetzoneenabledraggingofcontentfromdifferentdomainswithinwindows)

- **Internet Explorer internet zone protected mode**:  
  Baseline default: *Enable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetzoneenableprotectedmode)

- **Internet Explorer internet zone include local path when uploading files to server**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetzoneincludelocalpathwhenuploadingfilestoserver)

- **Internet Explorer internet zone initialize and script Active X controls not marked as safe**:  
  Baseline default: *Disable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetzoneinitializeandscriptactivexcontrols)

- **Internet Explorer internet zone java permissions**:  
  Baseline default: *Disable java*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetzonejavapermissions)

- **Internet Explorer internet zone launch applications and files in an iframe**:  
  Baseline default: *Disable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetzonelaunchingapplicationsandfilesiniframe)

- **Internet Explorer internet zone logon options**:  
  Baseline default: *Prompt*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetzonelogonoptions)

- **Internet Explorer internet zone navigate windows and frames across different domains**:  
  Baseline default: *Disable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetzonenavigatewindowsandframes)

- **Internet Explorer internet zone run .NET Framework reliant components signed with Authenticode**:  
  Baseline default: *Disable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetzonerunnetframeworkreliantcomponentssignedwithauthenticode)

- **Internet Explorer internet zone security warning for potentially unsafe files**:  
  Baseline default: *Prompt*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetzoneshowsecuritywarningforpotentiallyunsafefiles)

- **Internet Explorer internet zone popup blocker**:  
  Baseline default: *Enable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#internetzoneusepopupblocker)

- **Internet Explorer intranet zone do not run antimalware against Active X controls**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#intranetzonedonotrunantimalwareagainstactivexcontrols)

- **Internet Explorer intranet zone initialize and script Active X controls not marked as safe**:  
  Baseline default: *Disable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#intranetzoneinitializeandscriptactivexcontrols)

- **Internet Explorer intranet zone java permissions**:  
  Baseline default: *High safety*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#intranetzonejavapermissions)

- **Internet Explorer local machine zone do not run antimalware against Active X controls**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#localmachinezonedonotrunantimalwareagainstactivexcontrols)

- **Internet Explorer local machine zone java permissions**:  
  TBaseline default: *Disable java*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#localmachinezonejavapermissions)

- **Internet Explorer locked down internet zone smart screen**:  
  Baseline default: *Enabled*.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#lockeddowninternetzoneallowsmartscreenie)

- **Internet Explorer locked down intranet zone java permissions**:  
  Baseline default: *Disable java*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#lockeddownintranetjavapermissions)

- **Internet Explorer locked down local machine zone java permissions**:  
  Baseline default: *Disable java*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#lockeddownlocalmachinezonejavapermissions)

- **Internet Explorer locked down restricted zone smart screen**:  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#lockeddownrestrictedsiteszoneallowsmartscreenie)

- **Internet Explorer locked down restricted zone java permissions**:  
  Baseline default: *Disable Java*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#lockeddownrestrictedsiteszonejavapermissions)

- **Internet Explorer locked down trusted zone java permissions**:  
  Baseline default: *Disable java*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#lockeddowntrustedsiteszonejavapermissions)

- **Internet Explorer processes MIME sniffing safety feature**:  
  Baseline default: *Enable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#mimesniffingsafetyfeatureinternetexplorerprocesses)

- **Internet Explorer processes MK protocol security restriction**:  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#mkprotocolsecurityrestrictioninternetexplorerprocesses)

- **Internet Explorer processes notification bar**:  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#notificationbarinternetexplorerprocesses)

- **Internet Explorer prevent per user installation of Active X controls**:  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#preventperuserinstallationofactivexcontrols)

- **Internet Explorer processes protection from zone elevation**:  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#protectionfromzoneelevationinternetexplorerprocesses)

- **Internet Explorer remove run this time button for outdated Active X controls**:  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#removerunthistimebuttonforoutdatedactivexcontrols)

- **Internet Explorer processes restrict Active X install**:  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictactivexinstallinternetexplorerprocesses)

- **Internet Explorer restricted zone access to data sources**:  
  Baseline default: *Disable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszoneallowaccesstodatasources)

- **Internet Explorer restricted zone active scripting**:  
  Baseline default: *Disable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszoneallowactivescripting)

- **Internet Explorer restricted zone automatic prompt for file downloads**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszoneallowautomaticpromptingforfiledownloads)

- **Internet Explorer restricted zone binary and script behaviors**:  
  Baseline default: *Disable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszoneallowbinaryandscriptbehaviors)

- **Internet Explorer restricted zone copy and paste via script**:  
  Baseline default: *Disable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszoneallowcopypasteviascript)

- **Internet Explorer restricted zone drag and drop or copy and paste files**:  
  Baseline default: *Disable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszoneallowdraganddropcopyandpastefiles)

- **Internet Explorer restricted zone less privileged sites**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszoneallowlessprivilegedsites)

- **Internet Explorer restricted zone loading of XAML files**:  
  Baseline default: *Disable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszoneallowloadingofxamlfiles)

- **Internet Explorer restricted zone meta refresh**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszoneallowmetarefresh)

- **Internet Explorer restricted zone .NET Framework reliant components**:  
   Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszoneallownetframeworkreliantcomponents)

- **Internet Explorer restricted zone allow only approved domains to use Active X controls**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067233)

- **Internet Explorer restricted zone allow only approved domains to use tdc Active X controls**:  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszoneallowonlyapproveddomainstousetdcactivexcontrol)

- **Internet Explorer restricted zone scripting of web browser controls**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszoneallowscriptingofinternetexplorerwebbrowsercontrols)

- **Internet Explorer restricted zone script initiated windows**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszoneallowscriptinitiatedwindows)

- **Internet Explorer restricted zone scriptlets**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszoneallowscriptlets)

- **Internet Explorer restricted zone smart screen**:  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszoneallowsmartscreenie)

- **Internet Explorer restricted zone updates to status bar via script**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszoneallowupdatestostatusbarviascript)

- **Internet Explorer restricted zone user data persistence**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszoneallowuserdatapersistence)

- **Internet Explorer restricted zone allow vbscript to run**:  
  Baseline default: *Disable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszoneallowvbscripttorunininternetexplorer)

- **Internet Explorer restricted zone do not run antimalware against Active X controls**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszonedonotrunantimalwareagainstactivexcontrols)

- **Internet Explorer restricted zone download signed Active X controls**:  
  Baseline default: *Disable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszonedownloadsignedactivexcontrols)

- **Internet Explorer restricted zone download unsigned Active X controls**:  
  Baseline default: *Disable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszonedownloadunsignedactivexcontrols)

- **Internet Explorer restricted zone cross site scripting filter**:  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszoneenablecrosssitescriptingfilter)

- **Internet Explorer restricted zone drag content from different domains across windows**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszoneenabledraggingofcontentfromdifferentdomainsacrosswindows)

- **Internet Explorer restricted zone drag content from different domains within windows**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszoneenabledraggingofcontentfromdifferentdomainswithinwindows)  

- **Internet Explorer restricted zone include local path when uploading files to server**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszoneincludelocalpathwhenuploadingfilestoserver)

- **Internet Explorer restricted zone initialize and script Active X controls not marked as safe**:  
  Baseline default: *Disable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszoneinitializeandscriptactivexcontrols)

- **Internet Explorer restricted zone java permissions**:  
  Baseline default: *Disable java*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszonejavapermissions)

- **Internet Explorer restricted zone launch applications and files in an iFrame**:  
  Baseline default: *Disable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszonelaunchingapplicationsandfilesiniframe)

- **Internet Explorer restricted zone logon options**:  
  Baseline default: *Anonymous*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszonelogonoptions)

- **Internet Explorer restricted zone navigate windows and frames across different domains**:  
  Baseline default: *Disable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszonenavigatewindowsandframes)

- **Internet Explorer restricted zone run Active X controls and plugins**:  
  Baseline default: *Disable*.  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszonerunactivexcontrolsandplugins)

- **Internet Explorer restricted zone run .NET Framework reliant components signed with Authenticode**:  
  Baseline default: *Disable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszonerunnetframeworkreliantcomponentssignedwithauthenticode)

- **Internet Explorer restricted zone scripting of java applets**:  
  Baseline default: *Disable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszonescriptingofjavaapplets)

- **Internet Explorer restricted zone security warning for potentially unsafe files**:  
  Baseline default: *Disable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszoneshowsecuritywarningforpotentiallyunsafefiles)

- **Internet Explorer restricted zone protected mode**:  
  Baseline default: *Enable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszoneturnonprotectedmode)

- **Internet Explorer restricted zone popup blocker**:  
  Baseline default: *Enable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictedsiteszoneusepopupblocker)

- **Internet Explorer processes restrict file download**:  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#restrictfiledownloadinternetexplorerprocesses)

- **Internet Explorer processes scripted window security restrictions**:  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#scriptedwindowsecurityrestrictionsinternetexplorerprocesses)

- **Internet Explorer security zones use only machine settings**:  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#securityzonesuseonlymachinesettings)

- **Internet Explorer use Active X installer service**:  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#specifyuseofactivexinstallerservice)

- **Internet Explorer trusted zone do not run antimalware against Active X controls**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#trustedsiteszonedonotrunantimalwareagainstactivexcontrols)

- **Internet Explorer trusted zone initialize and script Active X controls not marked as safe**:  
  Baseline default: *Disable*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#trustedsiteszoneinitializeandscriptactivexcontrols)

- **Internet Explorer trusted zone java permissions**:  
  Baseline default: *High safety*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#trustedsiteszonejavapermissions)

- **Internet Explorer auto complete**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer#allowautocomplete)

::: zone-end

## Local Policies Security Options
<!-- https://learn.microsoft.com/windows/client-management/mdm/policy-csp-localpoliciessecurityoptions -->

::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

- **Block remote logon with blank password**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067219)

- **Minutes of lock screen inactivity until screen saver activates**:  
  Baseline default: *15*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067210)

- **Smart card removal behavior**:  
  Baseline default: *Lock workstation*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067331)

- **Require client to always digitally sign communications**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067187)

- **Prevent clients from sending unencrypted passwords to third party SMB servers**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067235)

- **Require server digitally signing communications always**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067319)

- **Prevent anonymous enumeration of SAM accounts**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067318)

- **Block anonymous enumeration of SAM accounts and shares**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067191)

- **Restrict anonymous access to named pipes and shares**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067212)

- **Allow remote calls to security accounts manager**:  
  Baseline default: *O:BAG:BAD:(A;;RC;;;BA)*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067209)

- **Prevent storing LAN manager hash value on next password change**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067213)

- **Authentication level**:  
  Baseline default: *Send NTLMv2 response only. Refuse LM and NTLM*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067189)

- **Minimum session security for NTLM SSP based clients**:  
  Baseline default: *Require NTLM V2 128 encryption*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067324)

- **Minimum session security for NTLM SSP based servers**:  
  Baseline default: *Require NTLM V2 and 128 bit encryption*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067246)

- **Administrator elevation prompt behavior**:  
  Baseline default: *Prompt for consent on the secure desktop*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067215)

- **Standard user elevation prompt behavior**:  
  Baseline default: *Automatically deny elevation requests*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067183)

- **Detect application installations and prompt for elevation**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067208)

- **Only allow UI access applications for secure locations**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067185)

- **Require admin approval mode for administrators**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067184)

- **Use admin approval mode**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067186)

- **Virtualize file and registry write failures to per user locations**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067321)

::: zone-end

## Microsoft Defender

::: zone pivot="mdm-december-2020,mdm-november-2021"

- **Block Adobe Reader from creating child processes**:  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=853979)

- **Block Office communication apps launch in a child process**:  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=874499)

- **Enter how often (0-24 hours) to check for security intelligence updates**  
  Baseline default: *4*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2113936)
  
- **Scan type**  
  Baseline default: *Quick scan*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2114045)

- **Defender schedule scan day**:  
  Baseline default: *Everyday*

- **Defender scan start time**:  
  Baseline default: *Not configured*

- **Cloud-delivered protection level**:  
  Baseline default: *Not Configured*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2113942)

- **Scan network files**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2114049)

- **Turn on real-time protection**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2114050)

- **Scan scripts that are used in Microsoft browsers**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2114054)

- **Scan archive files**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2114047)

- **Turn on behavior monitoring**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2114048)

- **Turn on cloud-delivered protection**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2113937)

- **Scan incoming mail messages**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2114052)

- **Scan removable drives during a full scan**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2113946)

- **Block Office applications from injecting code into other processes**:  
  Baseline default: *Block*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2113946)

- **Block Office applications from creating executable content**  
  Baseline default: *Block*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872975)

- **Block all Office applications from creating child processes**  
  Baseline default: *Block*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872976)

- **Block Win32 API calls from Office macro**:  
  Baseline default: *Block*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872977)

- **Block execution of potentially obfuscated scripts (js/vbs/ps)**:  
  Baseline default: *Block*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872978)

- **Block JavaScript or VBScript from launching downloaded executable content**:  
  Baseline default: *Block*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872979)

- **Block executable content download from email and webmail clients**:  
  Baseline default: *Block*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872980)

- **Block credential stealing from the Windows local security authority subsystem (lsass.exe)**:  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=874499)

- **Defender potentially unwanted app action**:  
  Baseline default: *Block*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-Microsoft_Intune_Workflows#defender-puaprotection)

- **Block untrusted and unsigned processes that run from USB**:  
  Baseline default: *Block*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=874502)

- **Enable network protection**:  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872618)

- **Defender sample submission consent type**:  
  Baseline default: *Send safe samples automatically*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067131)

::: zone-end
::: zone pivot="mdm-august-2020"

- **Block Adobe Reader from creating child processes**:  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=853979)

- **Block Office communication apps launch in a child process**:  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=874499)

- **Enter how often (0-24 hours) to check for security intelligence updates**  
  Baseline default: *4*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2113936)
  
- **Scan type**  
  Baseline default: *Quick scan*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2114045)

- **Defender schedule scan day**:  
  Baseline default: *Everyday*

- **Cloud-delivered protection level**:  
  Baseline default: *Not Configured*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2113942)

- **Scan network files**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2114049)

- **Turn on real-time protection**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2114050)

- **Scan scripts that are used in Microsoft browsers**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2114054)

- **Scan archive files**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2114047)

- **Turn on behavior monitoring**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2114048)

- **Turn on cloud-delivered protection**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2113937)

- **Scan incoming mail messages**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2114052)

- **Scan removable drives during a full scan**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2113946)

- **Block Office applications from injecting code into other processes**:  
  Baseline default: *Block*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2113946)

- **Block Office applications from creating executable content**  
  Baseline default: *Block*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872975)

- **Block all Office applications from creating child processes**  
  Baseline default: *Block*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872976)

- **Block Win32 API calls from Office macro**:  
  Baseline default: *Block*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872977)

- **Block execution of potentially obfuscated scripts (js/vbs/ps)**:  
  Baseline default: *Block*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872978)

- **Block JavaScript or VBScript from launching downloaded executable content**:  
  Baseline default: *Block*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872979)

- **Block executable content download from email and webmail clients**:  
  Baseline default: *Block*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872980)

- **Block credential stealing from the Windows local security authority subsystem (lsass.exe)**:  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=874499)

- **Defender potentially unwanted app action**:  
  Baseline default: *Block*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-Microsoft_Intune_Workflows#defender-puaprotection)

- **Block untrusted and unsigned processes that run from USB**:  
  Baseline default: *Block*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=874502)

- **Enable network protection**:  
  Baseline default: *Enable*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872618)

- **Defender sample submission consent type**:  
  Baseline default: *Send safe samples automatically*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067131)

::: zone-end

## MS Security Guide

::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

- **SMB v1 client driver start configuration**:  
  Baseline default: *Disabled driver*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067214)

- **Apply UAC restrictions to local accounts on network logon**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067188)

- **Structured exception handling overwrite protection**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067217)

- **SMB v1 server**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067190)

- **Digest authentication**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067193)

::: zone-end

## MSS Legacy

::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

- **Network IPv6 source routing protection level**:  
  Baseline default: *Highest protection*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067216)

- **Network IP source routing protection level**:  
  Baseline default: *Highest protection*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067220)

- **Network ignore NetBIOS name release requests except from WINS servers**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067218)

- **Network ICMP redirects override OSPF generated routes**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067326)

::: zone-end

## Power

::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

- **Require password on wake while on battery**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067322)

- **Require password on wake while plugged in**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067221)

- **Standby states when sleeping while on battery**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067195)

- **Standby states when sleeping while plugged in**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067196)

::: zone-end

## Remote Assistance

::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

- **Remote Assistance solicited**:  
  Baseline default: *Disable Remote Assistance*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067198)

::: zone-end

## Remote Desktop Services

::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

- **Remote desktop services client connection encryption level**:  
  Baseline default: *High*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067222)

- **Block drive redirection**:  
  Baseline default: *Enabled*  

- **Block password saving**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067301)

- **Prompt for password upon connection**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067328)

- **Secure RPC communication**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067248)

::: zone-end

## Remote Management

::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

- **Block client digest authentication**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067302)

- **Block storing run as credentials**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067300)

- **Client basic authentication**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067252)

- **Basic authentication**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067223)

- **Client unencrypted traffic**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067304)

- **Unencrypted traffic**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067226)

::: zone-end

## Remote Procedure Call

::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

- **RPC unauthenticated client options**:  
  Baseline default: *Authenticated*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067225)

::: zone-end

## Search

::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

- **Disable indexing encrypted items**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067303)

::: zone-end

## Smart Screen

::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

- **Turn on Windows SmartScreen**  
  Baseline default: *Yes*  
   [Learn more](/windows/client-management/mdm/policy-csp-smartscreen#smartscreen-enablesmartscreeninshell)

- **Block users from ignoring SmartScreen warnings**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872783)

::: zone-end

## System

::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

- **System boot start driver initialization**:  
  Baseline default: *Good unknown and bad critical*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067307)

::: zone-end

## Wi-Fi

::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

- **Block Automatically connecting to Wi-Fi hotspots**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067320)

- **Block Internet sharing**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067327)

::: zone-end

## Windows Connection Manager

::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

- **Block connection to non-domain networks**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067323)

::: zone-end

## Windows Ink Workspace

::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

- **Ink Workspace**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067241)

::: zone-end

## Windows PowerShell

::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

- **PowerShell script block logging**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067330)

::: zone-end

## Next steps

- [Learn about security baselines](security-baselines.md)
- [Avoid conflicts](security-baselines.md#avoid-conflicts)
- [Troubleshoot policies and profiles in Intune](/troubleshoot/mem/intune/troubleshoot-policies-in-microsoft-intune)
