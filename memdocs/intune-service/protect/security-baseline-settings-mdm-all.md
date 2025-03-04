---
# required metadata

title: Default configuration of Intune's Windows security baselines
titleSuffix: Microsoft Intune
description: View the default setting configuration of the various Microsoft Intune security baselines for Windows.
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 02/12/2025
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
- sub-secure-endpoints
zone_pivot_groups: windows-mdm-versions
---
<!-- Pivot details: 
    - id: mdm-24h2
      title: Version 24h2
      - id: mdm-23h2
      title: Version 23H2
    
    Following are pivots for baselines that use the older settings format:
    - id: mdm-november-2021
      title: November 2021
    - id: mdm-december-2020
      title: December 2020
    - id: mdm-august-2020
      title: August 2020
-->

# Windows MDM security baseline settings reference for Microsoft Intune

This article is a reference for the settings that are available in the Windows Mobile Device Management (MDM) security baseline for Microsoft Intune.

## About this reference article

Each security baseline is a group of preconfigured Windows settings that help you apply and enforce granular security settings that the relevant security teams recommend. You can also customize each baseline you deploy to enforce only those settings and values you require. When you create a security baseline profile in Intune, you're creating a template that consists of multiple device configuration settings.

The details that display in this article are based on baseline version you select at the top of the article. For each version, this article displays:

- A list of each setting with its configuration as found in the default instance of that baseline version.
- When available, a link to the underlying configuration service provider (CSP) documentation or other related content from the relevant product group that provides context and possibly additional details for a settings use.

When a new version of a baseline becomes available, it replaces the previous version. Profile instances that you’ve created prior to the availability of a new version:

- Become read-only. You can continue to use those profiles but can't edit them to change their configuration.
- Can be updated to the current version. After you update a profile to the current baseline version, you can edit the profile to modify settings.

To learn more about using security baselines, see:
- [Use security baselines](../protect/security-baselines.md)
- [Change the baseline version for a profile](../protect/security-baselines-configure.md#update-baselines-that-use-the-previous-format)
- [Manage security baselines](../protect/security-baselines-configure.md)

::: zone pivot="mdm-24h2"
## Security Baseline for Windows, version 24H2 

The settings in this baseline are taken from the Windows 11 **version 24H2** security baseline as found in the [Security Compliance Toolkit and Baselines](https://www.microsoft.com/en-us/download/details.aspx?id=55319) from the Microsoft Download Center, and include only the settings that apply to Windows devices managed through Intune. When available, the setting name links to the source Configuration Service Provider (CSP), and then displays that settings default configuration in the baseline.

### Administrative Templates

#### Control Panel > Personalization

- **Prevent enabling lock screen camera**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-devicelock?WT.mc_id=Portal-fx#preventenablinglockscreencamera)

- **Prevent enabling lock screen slide show**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-devicelock?WT.mc_id=Portal-fx#preventlockscreenslideshow)

#### MS Security Guide

- **Apply UAC restrictions to local accounts on network logons**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-mssecurityguide?WT.mc_id=Portal-fx#applyuacrestrictionstolocalaccountsonnetworklogon)
  
- **Configure SMB v1 client driver**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-mssecurityguide?WT.mc_id=Portal-fx#configuresmbv1clientdriver)  
  - **Configure MrxSmb10 driver**  
    Baseline default: *Disable driver (recommended)*

- **Configure SMB v1 server**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-mssecurityguide?WT.mc_id=Portal-fx#configuresmbv1server)

- **Enable Structured Exception Handling Overwrite Protection (SEHOP)**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-mssecurityguide?WT.mc_id=Portal-fx#enablestructuredexceptionhandlingoverwriteprotection)

- **WDigest Authentication (disabling may require KB2871997)**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-mssecurityguide?WT.mc_id=Portal-fx#wdigestauthentication)

#### MSS (Legacy)

- **MSS: (DisableIPSourceRouting IPv6) IP source routing protection level (protects against packet spoofing)**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-msslegacy?WT.mc_id=Portal-fx#ipv6sourceroutingprotectionlevel)  
  - **DisableIPSourceRouting IPv6 (Device)**  
    Baseline default: *Highest protection, source routing is completely disabled*

- **MSS: (DisableIPSourceRouting) IP source routing protection level (protects against packet spoofing)**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-msslegacy?WT.mc_id=Portal-fx#ipsourceroutingprotectionlevel)
  - **DisableIPSourceRouting (Device)**  
    Baseline default: *Highest protection, source routing is completely disabled*

- **MSS: (EnableCMPRedirect) Allow ICMP redirects to override OSPF generated routes**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-msslegacy?WT.mc_id=Portal-fx#allowicmpredirectstooverrideospfgeneratedroutes)

- **MSS: (NoNameReleaseOnDemand) Allow the computer to ignore NetBIOS name release requests except from WINS servers**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-msslegacy?WT.mc_id=Portal-fx#allowthecomputertoignorenetbiosnamereleaserequestsexceptfromwinsservers)

#### Network > DNS Client

- **Turn off multicast name resolution**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-admx-dnsclient?WT.mc_id=Portal-fx#turn_off_multicast)

#### Network > Network Connections

- **Prohibit use of Internet Connection Sharing on your DNS domain network**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-admx-networkconnections?WT.mc_id=Portal-fx#nc-showsharedaccessui)

#### Network > Network Provider

- **Hardened UNC Paths**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-connectivity?WT.mc_id=Portal-fx#hardeneduncpaths)
  - **Hardened UNC Paths: (Device)**  
    Baseline defaults:

    | Name           | Value|
    |----------------|------|
    | `\\*\SYSVOL`   | RequireMutualAuthentication=1,RequireIntegrity=1 |
    | `\\*\NETLOGON` | RequireMutualAuthentication=1,RequireIntegrity=1 |

#### Network > Windows Connection Manager

- **Prohibit connection to non-domain networks when connected to domain authenticated network**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-windowsconnectionmanager?WT.mc_id=Portal-fx#prohitconnectiontonondomainnetworkswhenconnectedtodomainauthenticatednetwork)

#### Printers

- **Configure Redirection Guard**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-printers?WT.mc_id=Portal-fx#configureredirectionguardpolicy)
  - **Redirection Guard Options (Device)**  
    Baseline default: *Redirection Guard Enabled*

- **Configure RPC connection settings**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-printers?WT.mc_id=Portal-fx#configurerpcconnectionpolicy)
  - **Use authentication for outgoing RPC connections: (Device)**  
    Baseline default: *Default*  
  - **Protocol to allow for incoming RPC connections: (Device)**  
    Baseline default: *RPC over TCP*

- **Configure RPC listener settings**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-printers?WT.mc_id=Portal-fx#configurerpclistenerpolicy)  
  - **Protocols to allow for incoming RPC connections: (Device)**  
    Baseline default: *RCP over TCP*  
  - **Authentication protocol to use for incoming RPC connections: (Device)**  
    Baseline default: *Negotiate*

- **Configure RPC over TPC port**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-printers?WT.mc_id=Portal-fx#configurerpctcpport)  
  - **RPC over TCP port (Device)**  
    Baseline default: *0*

- **Limits print driver installation to Administrators**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-printers?WT.mc_id=Portal-fx#restrictdriverinstallationtoadministrators)

- **Manage processing of Queue-specific files**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-printers?WT.mc_id=Portal-fx#configurecopyfilespolicy)  
  - **Manage processing of Queue-specific files: (Device)**  
    Baseline default: *Limit Queue-specific files to Color profiles*

#### Start Menu and Taskbar > Notifications

- **Turn off toast notifications on the lock screen (User)**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-admx-wpn?WT.mc_id=Portal-fx#nolockscreentoastnotification)

#### System > Credentials Delegation

- **Encryption Oracle Remediation**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-admx-credssp?WT.mc_id=Portal-fx#allowencryptionoracle)
  - **Protection Level: (Device)**  
    Baseline default: *Force Updated Clients*

- **Remote host allows delegation of non-exportable credentials**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-credentialsdelegation?WT.mc_id=Portal-fx#remotehostallowsdelegationofnonexportablecredentials)

#### System > Device Installation > Device Installation Restrictions

- **Prevent installation of devices using drivers that match these device setup classes**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-deviceinstallation?WT.mc_id=Portal-fx#preventinstallationofmatchingdevicesetupclasses)
  - **Also apply to matching devices that are already installed**  
    Baseline default: *True*  
  - **Prevented Classes**  
    Baseline default: *{d48179be-ec20-11d1-b6b8-00c04fa372a7}*

#### System > Early Launch Antimalware

- **Boot-Start Driver Initialization Policy**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-system?WT.mc_id=Portal-fx#bootstartdriverinitialization)
  - **Choose the boot-start drivers that can be initialized:**  
    Baseline default: *Good, unknown and bad but critical*

#### System > Group Policy

- **Configure registry policy processing**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-admx-grouppolicy?WT.mc_id=Portal-fx#cse-registry)  
  - **Do not apply during periodic background processing (Device)**  
    Baseline default: *False*
  - **Process even if the Group Policy objects have not changed (Device)**  
    Baseline default: *True*

#### System > Internet Communication Management > Internet Communication settings

- **Turn off downloading of print drivers**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-connectivity?WT.mc_id=Portal-fx#disabledownloadingofprintdriversoverhttp)

- **Turn off Internet download for Web publishing and online ordering wizards**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-connectivity?WT.mc_id=Portal-fx#disableinternetdownloadforwebpublishingandonlineorderingwizards)

#### System > Local Security Authority

- **Allow Custom SSPs and APs to be loaded into LSASS**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-lsa#allowcustomsspsaps)

#### System > Power Management > Sleep Settings

- **Allow standby states (S1-S3) when sleeping (on battery)**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-power?WT.mc_id=Portal-fx#allowstandbystateswhensleepingonbattery)

- **Allow standby states (S1-S3) when sleeping (plugged in)**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-power?WT.mc_id=Portal-fx#allowstandbywhensleepingpluggedin)

- **Require a password when a computer wakes (on battery)**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-power?WT.mc_id=Portal-fx#requirepasswordwhencomputerwakesonbattery)

- **Require a password when a computer wakes (plugged in)**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-power?WT.mc_id=Portal-fx#requirepasswordwhencomputerwakespluggedin)

#### System > Remote Assistance

- **Configure Solicited Remote Assistance**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-remoteassistance?WT.mc_id=Portal-fx#solicitedremoteassistance)

#### System > Remote Procedure Call

- **Restrict Unauthenticated RPC clients**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-remoteprocedurecall?WT.mc_id=Portal-fx#restrictunauthenticatedrpcclients)
  - **RPC Runtime Unauthenticated Client Restriction to Apply:**  
    Baseline default: *Authenticated*

#### Windows Components > App runtime

- **Allow Microsoft accounts to be optional**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-appruntime?WT.mc_id=Portal-fx#allowmicrosoftaccountstobeoptional)

#### Windows Components > AutoPlay Policies

- **Disallow Autoplay for non-volume devices**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-autoplay?WT.mc_id=Portal-fx#disallowautoplayfornonvolumedevices)

- **Set the default behavior for AutoRun**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-autoplay?WT.mc_id=Portal-fx#setdefaultautorunbehavior)
  - **Default AutoRun Behavior**  
    Baseline default: *Do not execute any autorun commands*

- **Turn off Autoplay**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-autoplay?WT.mc_id=Portal-fx#turnoffautoplay)
  - **Turn off Autoplay on:**  
    Baseline default: *All drives*

#### Windows Components > BitLocker Drive Encryption > Fixed Data Drives

- **Deny write access to fixed drives not protected by BitLocker**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/bitlocker-csp?WT.mc_id=Portal-fx#fixeddrivesrequireencryption)

#### Windows Components > BitLocker Drive Encryption > Removable Data Drives

- **Deny write access to removable drives not protected by BitLocker**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/bitlocker-csp?WT.mc_id=Portal-fx#removabledrivesrequireencryption)
  - **Do not allow write access to devices configured in another organization**  
    Baseline default: *False*

#### Windows Components > Credential User Interface

- **Enumerate administrator accounts on elevation**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-credentialsui?WT.mc_id=Portal-fx#enumerateadministrators)

#### Windows Components > Event Log Service > Application

- **Specify the maximum log file size (KB)**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-eventlogservice?WT.mc_id=Portal-fx#specifymaximumfilesizeapplicationlog)
  - **Maximum Log Size (KB)**  
    Baseline default: *32768*

#### Windows Components > Event Log Service > Security

- **Specify the maximum log file size (KB)**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-eventlogservice?WT.mc_id=Portal-fx#specifymaximumfilesizesecuritylog)
  - **Maximum Log Size (KB)**  
    Baseline default: *196608*

#### Windows Components > Event Log Service > System

- **Specify the maximum log file size (KB)**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-eventlogservice?WT.mc_id=Portal-fx#specifymaximumfilesizesystemlog)
  - **Maximum Log Size (KB)**  
    Baseline default: *32768*

#### Windows Components > File Explorer

- **Configure Windows Defender SmartScreen**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-admx-windowsexplorer?WT.mc_id=Portal-fx#enablesmartscreen)
  - **Pick one of the following settings: (Device)**  
    Baseline default: *Warn and prevent bypass*

- **Turn off Data Execution Prevention for Explorer**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-fileexplorer?WT.mc_id=Portal-fx#turnoffdataexecutionpreventionforexplorer)

- **Turn off heap termination on corruption**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-fileexplorer?WT.mc_id=Portal-fx#turnoffheapterminationoncorruption)

#### Windows Components > Internet Explorer > Internet Control Panel > Advanced Page

- **Allow software to run or install even if the signature is invalid**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#allowsoftwarewhensignatureisinvalid)

- **Check for server certificate revocation**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#checkservercertificaterevocation)

- **Check for signatures on downloaded programs**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#checksignaturesondownloadedprograms)

- **Do not allow ActiveX controls to run in Protected Mode when Enhanced Protected Mode is enabled**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#donotallowactivexcontrolsinprotectedmode)

- **Turn off encryption support**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#disableencryptionsupport)
  - **Secure Protocol combinations**  
    Baseline default: *Use TLS 1.1 and TLS 1.2*

- **Turn on 64-bit tab processes when running in Enhanced Protected Mode on 64-bit versions of Windows**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#disableprocessesinenhancedprotectedmode)

- **Turn on Enhanced Protected Mode**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#allowenhancedprotectedmode)

#### Windows Components > Internet Explorer > Internet Control Panel

- **Prevent ignoring certificate errors**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#disableignoringcertificateerrors)

#### Windows Components > Internet Explorer > Internet Control Panel > Security Page > Internet Zone

- **Access data sources across domains**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowaccesstodatasources)
  - **Access data sources across domains**  
    Baseline default: *Disable*

- **Allow cut, copy or paste operations from the clipboard via script**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowcopypasteviascript)
  - **Allow paste operations via script**  
    Baseline default: *Disable*

- **Allow drag and drop or copy and paste files**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowdraganddropcopyandpastefiles)
  - **Allow drag and drop or copy and paste files**  
    Baseline default: *Disable*

- **Allow loading of XAML files**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowloadingofxamlfiles)
  - **XAML Files**  
    Baseline default: *Disable*

- **Allow only approved domains to use ActiveX controls without prompt**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowonlyapproveddomainstouseactivexcontrols)
  - **Only allow approved domains to use ActiveX controls without prompt**  
    Baseline default: *Enable*

- **Allow only approved domains to use the TDC ActiveX control**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowonlyapproveddomainstousetdcactivexcontrol)
  - **Only allow approved domains to use the TDC ActiveX control**  
    Baseline default: *Enable*

- **Allow script-initiated windows without size or position constraints**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowscriptinitiatedwindows)
  - **Allow script-initiated windows without size or position constraints**  
    Baseline default: *Disable*

- **Allow scripting of Internet Explorer WebBrowser controls**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowscriptingofinternetexplorerwebbrowsercontrols)
  - **Internet Explorer web browser control**  
    Baseline default: *Disable*

- **Allow scriptlets**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowscriptlets)
  - **Scriptlets**  
    Baseline default: *Disable*

- **Allow updates to status bar via script**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowupdatestostatusbarviascript)
  - **Status bar updates via script**  
    Baseline default: *Disable*

- **Allow VBScript to run in Internet Explorer**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowvbscripttorunininternetexplorer)
  - **Allow VBScript to run in Internet Explorer**  
    Baseline default: *Disable*

- **Automatic prompting for file downloads**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowautomaticpromptingforfiledownloads)
  - **Automatic prompting for file downloads**  
    Baseline default: *Disable*

- **Don't run antimalware programs against ActiveX controls**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzonedonotrunantimalwareagainstactivexcontrols)
  - **Don't run antimalware programs against ActiveX controls**  
    Baseline default: *Disable*

- **Download signed ActiveX controls**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzonedownloadsignedactivexcontrols)
  - **Download signed ActiveX controls**  
    Baseline default: *Disable*

- **Download unsigned ActiveX controls**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzonedownloadunsignedactivexcontrols)
  - **Download unsigned ActiveX controls**  
    Baseline default: *Disable*

- **Enable dragging of content from different domains across windows**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneenabledraggingofcontentfromdifferentdomainsacrosswindows)
  - **Enable dragging of content from different domains across windows**  
    Baseline default: *Disable*

- **Enable dragging of content from different domains within a window**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneenabledraggingofcontentfromdifferentdomainsacrosswindows)
  - **Enable dragging of content from different domains within a window**  
    Baseline default: *Disable*

- **Include local path when user is uploading files to a server**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneincludelocalpathwhenuploadingfilestoserver)
  - **Include local path when user is uploading files to a server**  
    Baseline default: *Disable*

- **Initialize and script ActiveX controls not marked as safe**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneinitializeandscriptactivexcontrols)
  - **Initialize and script ActiveX controls not marked as safe**  
    Baseline default: *Disable*

- **Java permissions**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzonejavapermissions)
  - **Java permissions**  
    Baseline default: *Disable Java*

- **Launching applications and files in an IFRAME**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzonelaunchingapplicationsandfilesiniframe)
  - **Launching applications and files in an IFRAME**  
    Baseline default: *Disable*

- **Logon options**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzonelogonoptions)
  - **Logon options**  
    Baseline default: *Prompt for user name and password*

- **Navigate windows and frames across different domains**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzonenavigatewindowsandframes)
  - **Navigate windows and frames across different domains**  
    Baseline default: *Disable*

- **Run .NET Framework-reliant components not signed with Authenticode**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallownetframeworkreliantcomponents)
  - **Run .NET Framework-reliant components not signed with Authenticode**  
    Baseline default: *Disable*

- **Run .NET Framework-reliant components signed with Authenticode**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzonerunnetframeworkreliantcomponentssignedwithauthenticode)
  - **Run .NET Framework-reliant components signed with Authenticode**  
    Baseline default: *Disable*

- **Show security warning for potentially unsafe files**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneshowsecuritywarningforpotentiallyunsafefiles)
  - **Launching programs and unsafe files**  
    Baseline default: *Prompt*

- **Turn on Cross-Site Scripting Filter**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneenablecrosssitescriptingfilter)
  - **Turn on Cross-Site Scripting (XSS) Filter**  
    Baseline default: *Enable*

- **Turn on Protected Mode**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneenableprotectedmode)
  - **Protected Mode**  
    Baseline default: *Enable*

- **Turn on SmartScreen Filter scan**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowsmartscreenie)
  - **Use SmartScreen Filter**  
    Baseline default: *Enable*

- **Use Pop-up Blocker**
  Baseline default: *Enable*
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetexplorer-internetzoneusepopupblocker)
  - **Use Pop-up Blocker**
    Baseline default: *Enable*

- **Userdata persistence**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowuserdatapersistence)
  - **Userdata persistence**  
    Baseline default: *Disable*

- **Web sites in less privileged Web content zones can navigate into this zone**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowlessprivilegedsites)
  - **Web sites in less privileged Web content zones can navigate into this zone**  
    Baseline default: *Disable*

#### Windows Components > Internet Explorer > Internet Control Panel > Security Page

- **Intranet Sites: Include all network paths (UNCs)**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#includeallnetworkpaths)

- **Turn on certificate address mismatch warning**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#allowcertificateaddressmismatchwarning)

#### Windows Components > Internet Explorer > Internet Control Panel > Security Page > Intranet Zone

- **Don't run antimalware programs against ActiveX controls**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#intranetzonedonotrunantimalwareagainstactivexcontrols)
  - **Don't run antimalware programs against ActiveX controls**  
    Baseline default: *Disable*

- **Initialize and script ActiveX controls not marked as safe**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#intranetzoneinitializeandscriptactivexcontrols)
  - **Initialize and script ActiveX controls not marked as safe**  
    Baseline default: *Disable*

- **Java permissions**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#intranetzonejavapermissions)
  - **Java permissions**  
    Baseline default: *High safety*

#### Windows Components > Internet Explorer > Internet Control Panel > Security Page > Local Machine Zone

- **Don't run antimalware programs against ActiveX controls**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#localmachinezonedonotrunantimalwareagainstactivexcontrols)
  - **Don't run antimalware programs against ActiveX controls**  
    Baseline default: *Disable*

- **Java permissions**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#localmachinezonejavapermissions)
  - **Java permissions**  
    Baseline default: *Disable Java*

#### Windows Components > Internet Explorer > Internet Control Panel > Security Page > Locked-Down Internet Zone

- **Turn on SmartScreen Filter scan**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#lockeddowninternetzoneallowsmartscreenie)
  - **Use SmartScreen Filter**  
    Baseline default: *Enable*

#### Windows Components > Internet Explorer > Internet Control Panel > Security Page > Locked-Down Intranet Zone

- **Java permissions**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#lockeddownintranetjavapermissions)
  - **Java permissions**  
    Baseline default: *Disable Java*

#### Windows Components > Internet Explorer > Internet Control Panel > Security Page > Locked-Down Local Machine Zone

- **Java permissions**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#lockeddownlocalmachinezonejavapermissions)
  - **Java permissions**  
    Baseline default: *Disable Java*

#### Windows Components > Internet Explorer > Internet Control Panel > Security Page > Locked-Down Restricted Sites Zone

- **Java permissions**  
  Baseline default: *Enabled*  
    [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#lockeddownlocalmachinezonejavapermissions)  
  - **Java permissions**  
    Baseline default: *Disable Java*

- **Turn on SmartScreen Filter scan**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#lockeddownrestrictedsiteszoneallowsmartscreenie)
  - **Use SmartScreen Filter**  
      Baseline default: *Enable*

#### Windows Components > Internet Explorer > Internet Control Panel > Security Page > Locked-Down Trusted Sites Zone

- **Java permissions**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#lockeddowntrustedsiteszonejavapermissions)
  - **Java permissions**  
    Baseline default: *Disable Java*

#### Windows Components > Internet Explorer > Internet Control Panel > Security Page > Restricted Sites Zone

- **Access data sources across domains**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowaccesstodatasources)
  - **Access data sources across domains**  
    Baseline default: *Disable*

- **Allow active scripting**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowactivescripting)
  - **Allow active scripting**  
    Baseline default: *Disable*

- **Allow binary and script behaviors**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowbinaryandscriptbehaviors)
  - **Allow binary and script behaviors**  
    Baseline default: *Disable*

- **Allow cut, copy or paste operations from the clipboard via script**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowcopypasteviascript)
  - **Allow paste operations via script**  
    Baseline default: *Disable*

- **Allow drag and drop or copy and paste files**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowdraganddropcopyandpastefiles)
  - **Allow drag and drop or copy and paste files**  
    Baseline default: *Disable*

- **Allow file downloads**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowfiledownloads)
  - **Allow file downloads**  
    Baseline default: *Disable*

- **Allow loading of XAML files**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowloadingofxamlfiles)
  - **XAML Files**  
    Baseline default: *Disable*

- **Allow META REFRESH**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowmetarefresh)
  - **Allow META REFRESH**  
    Baseline default: *Disable*

- **Allow only approved domains to use ActiveX controls without prompt**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowonlyapproveddomainstouseactivexcontrols)
  - **Only allow approved domains to use ActiveX controls without prompt**  
    Baseline default: *Enable*

- **Allow only approved domains to use the TDC ActiveX control**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowonlyapproveddomainstousetdcactivexcontrol)
  - **Only allow approved domains to use the TDC ActiveX control**  
    Baseline default: *Enable*

- **Allow script-initiated windows without size or position constraints**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowscriptinitiatedwindows)
  - **Allow script-initiated windows without size or position constraints**  
    Baseline default: *Disable*

- **Allow scripting of Internet Explorer WebBrowser controls**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowscriptingofinternetexplorerwebbrowsercontrols)
  - **Internet Explorer web browser control**  
    Baseline default: *Disable*

- **Allow scriptlets**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowscriptlets)
  - **Scriptlets**  
    Baseline default: *Disable*

- **Allow updates to status bar via script**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowupdatestostatusbarviascript)
  - **Status bar updates via script**  
    Baseline default: *Disable*

- **Allow VBScript to run in Internet Explorer**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowvbscripttorunininternetexplorer)
  - **Allow VBScript to run in Internet Explorer**  
    Baseline default: *Disable*

- **Automatic prompting for file downloads**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowautomaticpromptingforfiledownloads)
  - **Automatic prompting for file downloads**  
    Baseline default: *Disable*

- **Don't run antimalware programs against ActiveX controls**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszonedonotrunantimalwareagainstactivexcontrols)
  - **Don't run antimalware programs against ActiveX controls**  
    Baseline default: *Disable*

- **Download signed ActiveX controls**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszonedownloadsignedactivexcontrols)
  - **Download signed ActiveX controls**  
    Baseline default: *Disable*

- **Download unsigned ActiveX controls**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszonedownloadunsignedactivexcontrols)
  - **Download unsigned ActiveX controls**  
    Baseline default: *Disable*

- **Enable dragging of content from different domains across windows**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneenabledraggingofcontentfromdifferentdomainsacrosswindows)
  - **Enable dragging of content from different domains across windows**  
    Baseline default: *Disable*

- **Enable dragging of content from different domains within a window**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneenabledraggingofcontentfromdifferentdomainswithinwindows)
  - **Enable dragging of content from different domains within a window**  
    Baseline default: *Disable*

- **Include local path when user is uploading files to a server**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneincludelocalpathwhenuploadingfilestoserver)
  - **Include local directory path when uploading files to a server**  
    Baseline default: *Disable*

- **Initialize and script ActiveX controls not marked as safe**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneinitializeandscriptactivexcontrols)
  - **Initialize and script ActiveX controls not marked as safe**  
    Baseline default: *Disable*

- **Java permissions**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszonejavapermissions)
  - **Java permissions**  
    Baseline default: *Disable Java*

- **Launching applications and files in an IFRAME**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszonelaunchingapplicationsandfilesiniframe)
  - **Launching applications and files in an IFRAME**  
    Baseline default: *Disable*

- **Logon options**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszonelogonoptions)
  - **Logon options**  
    Baseline default: *Anonymous logon*

- **Navigate windows and frames across different domains**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszonenavigatewindowsandframes)
  - **Navigate windows and frames across different domains**  
    Baseline default: *Disable*

- **Run .NET Framework-reliant components not signed with Authenticode**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallownetframeworkreliantcomponents)
  - **Run .NET Framework-reliant components not signed with Authenticode**  
    Baseline default: *Disable*

- **Run .NET Framework-reliant components signed with Authenticode**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszonerunnetframeworkreliantcomponentssignedwithauthenticode)
  - **Run .NET Framework-reliant components signed with Authenticode**  
    Baseline default: *Disable*

- **Run ActiveX controls and plugins**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszonerunactivexcontrolsandplugins)
  - **Run ActiveX controls and plugins**  
    Baseline default: *Disable*

- **Script ActiveX controls marked safe for scripting**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszonescriptactivexcontrolsmarkedsafeforscripting)  
  - **Script ActiveX controls marked safe for scripting**  
    Baseline default: *Disable*

- **Scripting of Java applets**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszonescriptingofjavaapplets)
  - **Scripting of Java applets**  
    Baseline default: *Disable*

- **Show security warning for potentially unsafe files**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneshowsecuritywarningforpotentiallyunsafefiles)  
  - **Launching programs and unsafe files**  
    Baseline default: *Disable*

- **Turn on Cross-Site Scripting Filter**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneenablecrosssitescriptingfilter)
  - **Turn on Cross-Site Scripting (XSS) Filter**  
    Baseline default: *Enabled*

- **Turn on Protected Mode**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneturnonprotectedmode)
  - **Protected Mode**  
    Baseline default: *Enabled*

- **Turn on SmartScreen Filter scan**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowsmartscreenie)
  - **Use SmartScreen Filter**  
    Baseline default: *Enabled*

- **Use Pop-up Blocker**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneusepopupblocker)
  - **Use Pop-up Blocker**  
    Baseline default: *Enabled*

- **Userdata persistence**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowuserdatapersistence)
  - **Userdata persistence**  
    Baseline default: *Disable*

- **Web sites in less privileged Web content zones can navigate into this zone**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowlessprivilegedsites)
  - **Web sites in less privileged Web content zones can navigate into this zone**  
    Baseline default: *Disable*

#### Windows Components > Internet Explorer > Internet Control Panel > Security Page > Trusted Sites Zone

- **Don't run antimalware programs against ActiveX controls**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#trustedsiteszonedonotrunantimalwareagainstactivexcontrols)
  - **Don't run antimalware programs against ActiveX controls**  
    Baseline default: *Disable*

- **Initialize and script ActiveX controls not marked as safe**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#trustedsiteszoneinitializeandscriptactivexcontrols)
  - **Initialize and script ActiveX controls not marked as safe**  
    Baseline default: *Disable*

- **Java permissions**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#trustedsiteszonejavapermissions)
  - **Java permissions**  
    Baseline default: *High safety*

#### Windows Components > Internet Explorer

- **Prevent bypassing SmartScreen Filter warnings**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#disablebypassofsmartscreenwarnings)

- **Prevent bypassing SmartScreen Filter warnings about files that are not commonly downloaded from the Internet**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#disablebypassofsmartscreenwarningsaboutuncommonfiles)

- **Prevent managing SmartScreen Filter**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#preventmanagingsmartscreenfilter)
  - **Select SmartScreen Filter mode**  
    Baseline default: *On*

- **Prevent per-user installation of ActiveX controls**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#preventperuserinstallationofactivexcontrols)

- **Security Zones: Do not allow users to add/delete sites**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#donotallowuserstoaddsites)

- **Security Zones: Do not allow users to change policies**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#donotallowuserstochangepolicies)

- **Security Zones: Use only machine settings**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#securityzonesuseonlymachinesettings)

- **Specify use of ActiveX Installer Service for installation of ActiveX controls**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#specifyuseofactivexinstallerservice)

- **Turn off Crash Detection**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#disablecrashdetection)

- **Turn off the Security Settings Check feature**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#disablesecuritysettingscheck)

- **Turn on the auto-complete feature for user names and passwords on forms (User)**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#allowautocomplete)

#### Windows Components > Internet Explorer > Security Features > Add-on Management

- **Remove "Run this time" button for outdated ActiveX controls in Internet Explorer**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#removerunthistimebuttonforoutdatedactivexcontrols)

- **Turn off blocking of outdated ActiveX controls for Internet Explorer**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#donotblockoutdatedactivexcontrols)

#### Windows Components > Internet Explorer > Security Features

- **Allow fallback to SSL 3.0 (Internet Explorer)**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#allowfallbacktossl3)
  - **Allow insecure fallback for:**  
    Baseline default: *No Sites*

#### Windows Components > Internet Explorer > Security Features > Consistent Mime Handling

- **Internet Explorer Processes**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#consistentmimehandlinginternetexplorerprocesses)

#### Windows Components > Internet Explorer > Security Features > Mime Sniffing Safety Feature

- **Internet Explorer Processes**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#mimesniffingsafetyfeatureinternetexplorerprocesses)

#### Windows Components > Internet Explorer > Security Features > MK Protocol Security Restriction

- **Internet Explorer Processes**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#mkprotocolsecurityrestrictioninternetexplorerprocesses)

#### Windows Components > Internet Explorer > Security Features > Notification bar

- **Internet Explorer Processes**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#notificationbarinternetexplorerprocesses)

#### Windows Components > Internet Explorer > Security Features > Protection From Zone Elevation

- **Internet Explorer Processes**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#protectionfromzoneelevationinternetexplorerprocesses)

#### Windows Components > Internet Explorer > Security Features > Restrict ActiveX Install

- **Internet Explorer Processes**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictactivexinstallinternetexplorerprocesses)

#### Windows Components > Internet Explorer > Security Features > Restrict File Download

- **Internet Explorer Processes**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictfiledownloadinternetexplorerprocesses)

#### Windows Components > Internet Explorer > Security Features > Scripted Window Security Restrictions

- **Internet Explorer Processes**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#scriptedwindowsecurityrestrictionsinternetexplorerprocesses)

#### Windows Components > Microsoft Defender Antivirus > MAPS

- **Configure the 'Block at First Sight' feature**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-admx-microsoftdefenderantivirus?WT.mc_id=Portal-fx#disableblockatfirstseen)

#### Windows Components > Microsoft Defender Antivirus > Real-time Protection

- **Turn on process scanning whenever real-time protection is enabled**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-admx-microsoftdefenderantivirus?WT.mc_id=Portal-fx#realtimeprotection-disablescanonrealtimeenable)

#### Windows Components > Microsoft Defender Antivirus > Scan

- **Scan packed executables**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-admx-microsoftdefenderantivirus?WT.mc_id=Portal-fx#scan-disablepackedexescanning)

#### Windows Components > Microsoft Defender Antivirus

- **Turn off routine remediation**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-admx-microsoftdefenderantivirus?WT.mc_id=Portal-fx#disableroutinelytakingaction)

#### Windows Components > Remote Desktop Services > Remote Desktop Connection Client

- **Do not allow passwords to be saved**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-remotedesktopservices?WT.mc_id=Portal-fx#donotallowpasswordsaving)

#### Windows Components > Remote Desktop Services > Remote Desktop Session Host > Device and Resource Redirection

- **Do not allow drive redirection**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-remotedesktopservices?WT.mc_id=Portal-fx#donotallowdriveredirection)

#### Windows Components > Remote Desktop Services > Remote Desktop Session Host > Security

- **Always prompt for password upon connection**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-remotedesktopservices?WT.mc_id=Portal-fx#promptforpassworduponconnection)

- **Require secure RPC communication**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-remotedesktopservices?WT.mc_id=Portal-fx#requiresecurerpccommunication)

- **Set client connection encryption level**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-remotedesktopservices?WT.mc_id=Portal-fx#clientconnectionencryptionlevel)
  - **Encryption Level**  
    Baseline default: *High Level*  

#### Windows Components > RSS Feeds

- **Prevent downloading of enclosures**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#disableenclosuredownloading)

#### Windows Components > Windows Logon Options

- **Enable MPR notifications for the system**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-windowslogon?WT.mc_id=Portal-fx#enablemprnotifications)

- **Sign-in and lock last interactive user automatically after a restart**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-windowslogon?WT.mc_id=Portal-fx#allowautomaticrestartsignon)

#### Windows Components > Windows PowerShell

- **Turn on PowerShell Script Block Logging**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-windowspowershell?WT.mc_id=Portal-fx#turnonpowershellscriptblocklogging)
  - **Log script block invocation start / stop events:**  
    Baseline default: *False*  

#### Windows Components > Windows Remote Management (WinRM) > WinRM Client

- **Allow Basic authentication**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-remotemanagement?WT.mc_id=Portal-fx#allowbasicauthentication-service)

- **Allow unencrypted traffic**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-remotemanagement?WT.mc_id=Portal-fx#allowunencryptedtraffic-client)

- **Disallow Digest authentication**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-remotemanagement?WT.mc_id=Portal-fx#disallowdigestauthentication)

#### Windows Components > Windows Remote Management (WinRM) > WinRM Service

- **Allow Basic authentication**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-remotemanagement?WT.mc_id=Portal-fx#allowbasicauthentication-service)

- **Allow unencrypted traffic**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-remotemanagement?WT.mc_id=Portal-fx#allowunencryptedtraffic-service)

- **Disallow WinRM from storing RunAs credentials**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-remotemanagement?WT.mc_id=Portal-fx#disallowstoringofrunascredentials)

### Auditing

- **Account Logon Audit Credential Validation**  
  Baseline default: *Success+ Failure*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#accountlogon_auditcredentialvalidation)

- **Account Logon Logoff Audit Account Lockout**  
  Baseline default: *Failure*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#accountlogonlogoff_auditaccountlockout)

- **Account Logon Logoff Audit Group Membership**  
  Baseline default: *Success*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#accountlogonlogoff_auditgroupmembership)

- **Account Logon Logoff Audit Logon**  
  Baseline default: *Success+ Failure*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#accountlogonlogoff_auditlogon)

- **Audit Authentication Policy Change**  
  Baseline default: *Success*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#policychange_auditauthenticationpolicychange)

- **Audit Changes to Audit Policy**  
  Baseline default: *Success*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#policychange_auditpolicychange)

- **Audit File Share Access**  
  Baseline default: *Success+ Failure*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#objectaccess_auditfileshare)

- **Audit Other Logon Logoff Events**  
  Baseline default: *Success+ Failure*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#accountlogonlogoff_auditotherlogonlogoffevents)

- **Audit Security Group Management**  
  Baseline default: *Success*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#accountmanagement_auditsecuritygroupmanagement)

- **Audit Security System Extension**  
  Baseline default: *Success*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#system_auditsecuritysystemextension)

- **Audit Special Logon**  
  Baseline default: *Success*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#accountlogonlogoff_auditspeciallogon)

- **Audit User Account Management**  
  Baseline default: *Success+ Failure*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#accountmanagement_audituseraccountmanagement)

- **Detailed Tracking Audit PNP Activity**  
  Baseline default: *Success*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#detailedtracking_auditpnpactivity)

- **Detailed Tracking Audit Process Creation**  
  Baseline default: *Success*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#detailedtracking_auditprocesscreation)

- **Object Access Audit Detailed File Share**  
  Baseline default: *Failure*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#objectaccess_auditdetailedfileshare)

- **Object Access Audit Other Object Access Events**  
  Baseline default: *Success+ Failure*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#objectaccess_auditotherobjectaccessevents)

- **Object Access Audit Removable Storage**  
  Baseline default: *Success+ Failure*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#objectaccess_auditremovablestorage)

- **Policy Change Audit MPSSVC Rule Level Policy Change**  
  Baseline default: *Success+ Failure*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#policychange_auditmpssvcrulelevelpolicychange)

- **Policy Change Audit Other Policy Change Events**  
  Baseline default: *Failure*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#policychange_auditotherpolicychangeevents)

- **Privilege Use Audit Sensitive Privilege Use**  
  Baseline default: *Success*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#privilegeuse_auditsensitiveprivilegeuse)

- **System Audit Other System Events**  
  Baseline default: *Success+ Failure*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#system_auditothersystemevents)

- **System Audit Security State Change**  
  Baseline default: *Success*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#system_auditsecuritystatechange)

- **System Audit System Integrity**  
  Baseline default: *Success+ Failure*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#system_auditsystemintegrity)

### Browser

- **Allow Password Manager**  
  Baseline default: *Block*  
  [Learn more](/windows/client-management/mdm/policy-csp-Browser?WT.mc_id=Portal-fx#allowpasswordmanager)
 
- **Allow Smart Screen**  
  Baseline default: *Allow*  
  [Learn more](/windows/client-management/mdm/policy-csp-Browser?WT.mc_id=Portal-fx#allowsmartscreen)

- **Prevent Cert Error Overrides**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-Browser?WT.mc_id=Portal-fx#preventcerterroroverrides)

- **Prevent Smart Screen Prompt Override**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-Browser?WT.mc_id=Portal-fx#preventsmartscreenpromptoverride)

- **Prevent Smart Screen Prompt Override For Files**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-Browser?WT.mc_id=Portal-fx#preventsmartscreenpromptoverrideforfiles)

### Data Protection

- **Allow Direct Memory Access**  
  Baseline default: *Block*  
  [Learn more](/windows/client-management/mdm/policy-csp-dataprotection?WT.mc_id=Portal-fx#allowdirectmemoryaccess)

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

- **Allow Full Scan Removable Drive Scanning**  
  Baseline default: *Allowed. Scans removable drives.*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#allowfullscanremovabledrivescanning)

- **Allow On Access Protection**  
  Baseline default: *Allowed.*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#allowonaccessprotection)

- **Allow Realtime Monitoring**  
  Baseline default: *Allowed. Turns on and runs the real-time monitoring service.*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#allowrealtimemonitoring)

- **Allow scanning of all downloaded files and attachments**  
  Baseline default: *Allowed.*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#allowioavprotection)

- **Allow Script Scanning**  
  Baseline default: *Allowed.*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#allowscriptscanning)
  - **Block execution of potentially obfuscated scripts**  
    Baseline default: *Block*  
    [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)
  - **Block Win32 API calls from Office macros**  
    Baseline default: *Block*  
    [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)
  - **Block Office communication application from creating child processes**  
    Baseline default: *Block*  
    [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)
  - **Block all Office applications from creating child processes**  
    Baseline default: *Block*  
    [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)
  - **Block JavaScript or VBScript from launching downloaded executable content**  
    Baseline default: *Block*  
    [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)
  - **Block untrusted and unsigned processes that run from USB**  
    Baseline default: *Block*  
    [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)
  - **Block Adobe Reader from creating child processes**  
    Baseline default: *Block*  
    [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)
  - **Block credential stealing from the Windows local security authority subsystem**  
    Baseline default: *Block*  
    [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)
  - **Block Office applications from creating executable content**  
    Baseline default: *Block*  
    [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)
  - **Block Office applications from injecting code into other processes**  
    Baseline default: *Block*  
    [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)
  - **Block executable content from email client and webmail**  
    Baseline default: *Block*  
    [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)

- **Cloud Block Level**  
  Baseline default: *High*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#cloudblocklevel)

- **Cloud Extended Timeout**  
  Baseline default: *Configured*  
  Value: *50*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#cloudextendedtimeout)

- **Disable Local Admin Merge**  
  Baseline default: *Disable Local Admin Merge*  
  [Learn more](/windows/client-management/mdm/Defender-csp/?WT.mc_id=Portal-fx#configurationdisablelocaladminmerge)

- **Enable File Hash Computation**  
  Baseline default: *Enable*  
  [Learn more](/windows/client-management/mdm/Defender-csp/?WT.mc_id=Portal-fx#configurationenablefilehashcomputation)

- **Enable Network Protection**  
  Baseline default: *Enabled (block mode)*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#enablenetworkprotection)

- **Hide Exclusions From Local Admins**  
  Baseline default: *If you enable this setting, local admins will no longer be able to see the exclusion list in Windows Security App or via PowerShell.*  
  [Learn more](/windows/client-management/mdm/Defender-csp/?WT.mc_id=Portal-fx#configurationhideexclusionsfromlocaladmins)

- **PUA Protection**  
  Baseline default: *PUA Protection on. Detected items are blocked. They will show in history along with other threats.*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#puaprotection)

- **Real Time Scan Direction**  
  Baseline default: *Monitor all files (bi-directional).*  
  [Learn more](/windows/client-management/mdm/policy-csp-Defender?WT.mc_id=Portal-fx##realtimescandirection)

- **Submit Samples Consent**  
  Baseline default: *Send all samples automatically.*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#submitsamplesconsent)

- **Enable Convert Warn To Block**  
  Baseline default: *Warn verdicts are converted to block*  
  [Learn more](/windows/client-management/mdm/Defender-csp/?WT.mc_id=Portal-fx#configurationenableconvertwarntoblock)

- **Hide Exclusions From Local Users**  
  Baseline default: *If you enable this setting, local users will no longer be able to see the exclusion list in Windows Security App or via PowerShell.*  
  [Learn more](/windows/client-management/mdm/Defender-csp/?WT.mc_id=Portal-fx#configurationhideexclusionsfromlocalusers)

- **Oobe Enable Rtp And Sig Update**  
  Baseline default: *If you enable this setting, real-time protection and Security Intelligence Updates are enabled during OOBE.*  
  [Learn more](/windows/client-management/mdm/defender-csp?WT.mc_id=Portal-fx#configurationoobeenablertpandsigupdate)

- **Passive Remediation**  
  Baseline default: *Configured*  
  Value: *PASSIVEREMEDIATIONFLAGSENSEAUTOREMEDIATION: Passive Remediation Sense AutoRemediation*  
  [Learn more](/windows/client-management/mdm/Defender-csp/?WT.mc_id=Portal-fx#configurationpassiveremediation)

- **Quick Scan Include Exclusions**  
  Baseline default: *If you set this setting to 1, all files and directories that are excluded from real-time protection using contextual exclusions are scanned during a quick scan.*  
  [Learn more](/windows/client-management/mdm/Defender-csp/?WT.mc_id=Portal-fx#configurationquickscanincludeexclusions)

### Device Guard

- **Configure System Guard Launch**  
  Baseline default: *Unmanaged Enables Secure Launch if supported by hardware*  
  [Learn more](/windows/client-management/mdm/policy-csp-deviceguard?WT.mc_id=Portal-fx#configuresystemguardlaunch)

- **Credential Guard**  
  Baseline default: *(Enabled with UEFI lock) Turns on Credential Guard with UEFI lock.*  
  [Learn more](/windows/client-management/mdm/policy-csp-deviceguard?WT.mc_id=Portal-fx#lsacfgflags)

- **Enable Virtualization Based Security**  
  Baseline default: *Enable virtualization based security.*  
  [Learn more](/windows/client-management/mdm/policy-csp-deviceguard?WT.mc_id=Portal-fx#enablevirtualizationbasedsecurity)

- **Require Platform Security Features**  
  Baseline default: *Turns on VBS with Secure Boot.*  
  [Learn more](/windows/client-management/mdm/policy-csp-deviceguard?WT.mc_id=Portal-fx#requireplatformsecurityfeatures)

- **Machine Identity Isolation**  
  Baseline default: *(Disabled) Machine password is only LSASS-bound and stored in $MACHINE.ACC registry key.*  
  [Learn more](/windows/client-management/mdm/policy-csp-DeviceGuard?WT.mc_id=Portal-fx#machineidentityisolation)

### Device Lock

- **Device Password Enabled**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-devicelock?WT.mc_id=Portal-fx#devicepasswordenabled)
  - **Device Password History**  
    Baseline default: *Configured*  
    Value: *24*  
    [Learn more](/windows/client-management/mdm/policy-csp-devicelock?WT.mc_id=Portal-fx#devicepasswordhistory)
  - **Min Device Password Length**  
    Baseline default: *Configured*  
    Value: *14*  
    [Learn more](/windows/client-management/mdm/policy-csp-devicelock?WT.mc_id=Portal-fx#mindevicepasswordlength)

### Dma Guard

- **Device Enumeration Policy**  
  Baseline default: *Block all (Most restrictive)*  
  [Learn more](/windows/client-management/mdm/policy-csp-dmaguard?WT.mc_id=Portal-fx#deviceenumerationpolicy)

### Experience

- **Allow Windows Spotlight (User)**  
  Baseline default: *Allow*  
  [Learn more](/windows/client-management/mdm/policy-csp-Experience?WT.mc_id=Portal-fx#allowwindowsspotlight)
  - **Allow Windows Consumer Features**  
    Baseline default: *Block*  
    [Learn more](/windows/client-management/mdm/policy-csp-experience?WT.mc_id=Portal-fx#allowwindowsconsumerfeatures)
  - **Allow Third Party Suggestions In Windows Spotlight (User)**  
    Baseline default: *Block*  
    [Learn more](/windows/client-management/mdm/policy-csp-Experience?WT.mc_id=Portal-fx#allowthirdpartysuggestionsinwindowsspotlight)

### Firewall

- **Enable Domain Network Firewall**  
  Baseline default: *True*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoredomainprofileenablefirewall)
  - **Enable Log Success Connections**  
    Baseline default: *Enable Logging Of Successful Connections*  
    [Learn more](/windows/client-management/mdm/Firewall-csp/?WT.mc_id=Portal-fx#mdmstoredomainprofileenablelogsuccessconnections)
  - **Default Outbound Action**  
    Baseline default: *Allow*  
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoredomainprofiledefaultoutboundaction)
  - **Enable Log Dropped Packets**  
    Baseline default: *Enable Logging Of Dropped Packets*  
    [Learn more](/windows/client-management/mdm/Firewall-csp/?WT.mc_id=Portal-fx#mdmstoredomainprofileenablelogdroppedpackets)
  - **Disable Inbound Notifications**  
    Baseline default: *True*  
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoredomainprofiledisableinboundnotifications)
  - **Log Max File Size**  
    Baseline default: *16384*  
    [Learn more](/windows/client-management/mdm/Firewall-csp/?WT.mc_id=Portal-fx#mdmstoredomainprofilelogmaxfilesize)
  - **Default Inbound Action for Domain Profile**  
    Baseline default: *Block*  
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoredomainprofiledefaultinboundaction)

- **Enable Private Network Firewall**  
  Baseline default: *True*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreprivateprofileenablefirewall)
  - **Log Max File Size**  
    Baseline default: *16384*  
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreprivateprofilelogmaxfilesize)
  - **Default Inbound Action for Private Profile**  
    Baseline default: *Block*  
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreprivateprofiledefaultinboundaction)
  - **Enable Log Success Connections**  
    Baseline default: *Enable Logging Of Successful Connections*  
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreprivateprofileenablelogsuccessconnections)
  - **Enable Log Dropped Packets**  
    Baseline default: *Enable Logging Of Dropped Packets*  
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreprivateprofileenablelogdroppedpackets)
  - **Default Outbound Action**  
    Baseline default: *Allow*  
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreprivateprofiledefaultoutboundaction)
  - **Disable Inbound Notifications**  
    Baseline default: *True*  
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreprivateprofiledisableinboundnotifications)

- **Enable Public Network Firewall**  
  Baseline default: *True*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofileenablefirewall)
  - **Enable Log Dropped Packets**  
    Baseline default: *Enable Logging Of Dropped Packets*  
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofileenablelogdroppedpackets)
  - **Log Max File Size**  
    Baseline default: *16384*  
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofilelogmaxfilesize)
  - **Default Outbound Action**  
    Baseline default: *Allow*  
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofiledefaultoutboundaction)
  - **Disable Inbound Notifications**  
    Baseline default: *True*  
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofiledisableinboundnotifications)
  - **Default Inbound Action for Public Profile**  
    Baseline default: *Block*  
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofiledefaultinboundaction)
  - **Allow Local Policy Merge**  
    Baseline default: *False*  
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofileallowlocalpolicymerge)
  - **Enable Log Success Connections**  
    Baseline default: *Enable Logging Of Successful Connections*  
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofileenablelogsuccessconnections)
  - **Allow Local Ipsec Policy Merge**  
    Baseline default: *False*  
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofileallowlocalipsecpolicymerge)

### Lanman Workstation

- **Enable Insecure Guest Logons**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-LanmanWorkstation?WT.mc_id=Portal-fx#enableinsecureguestlogons)

### Local Policies Security Options
  <!-- UI Links add - in place of url which uses _ -->
- **Accounts Limit Local Account Use Of Blank Passwords To Console Logon Only**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#accounts_limitlocalaccountuseofblankpasswordstoconsolelogononly)

- **Interactive Logon Machine Inactivity Limit**  
  Baseline default: *Configured*  
  Value: *900*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#interactivelogon_machineinactivitylimit)

- **Interactive Logon Smart Card Removal Behavior**  
  Baseline default: *Lock Workstation*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#interactivelogon_smartcardremovalbehavior)

- **Microsoft Network Client Digitally Sign Communications Always**  
  Baseline default: *Enable*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#microsoftnetworkclient_digitallysigncommunicationsalways)

- **Microsoft Network Client Send Unencrypted Password To Third Party SMB Servers**  
  Baseline default: *Disable*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#microsoftnetworkclient_sendunencryptedpasswordtothirdpartysmbservers)

- **Microsoft Network Server Digitally Sign Communications Always**  
  Baseline default: *Enable*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#microsoftnetworkserver_digitallysigncommunicationsalways)

- **Network Access Do Not Allow Anonymous Enumeration Of SAM Accounts**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#networkaccess_donotallowanonymousenumerationofsamaccounts)

- **Network Access Do Not Allow Anonymous Enumeration Of Sam Accounts And Shares**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#networkaccess_donotallowanonymousenumerationofsamaccountsandshares)

- **Network Access Restrict Anonymous Access To Named Pipes And Shares**  
  Baseline default: *Enable*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#networkaccess-restrictanonymousaccesstonamedpipesandshares)

- **Network Access Restrict Clients Allowed To Make Remote Calls To SAM**  
  Baseline default: *Configured*  
  Value: *O:BAG:BAD:(A;;RC;;;BA)*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#networkaccess_restrictclientsallowedtomakeremotecallstosam)

- **Network Security Do Not Store LAN Manager Hash Value On Next Password Change**  
  Baseline default: *Enable*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#networksecurity_donotstorelanmanagerhashvalueonnextpasswordchange)

- **Network Security LAN Manager Authentication Level**  
  Baseline default: *Send LM and NTLMv2 responses only. Refuse LM and NTLM*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#networksecurity_lanmanagerauthenticationlevel)

- **Network Security Minimum Session Security For NTLMSSP Based Clients**  
  Baseline default: *Require NTLM and 128-bit encryption*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#networksecurity_minimumsessionsecurityforntlmsspbasedclients)

- **Network Security Minimum Session Security For NTLMSSP Based Servers**  
  Baseline default: *Require NTLM and 128-bit encryption*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#networksecurity_minimumsessionsecurityforntlmsspbasedservers)

- **User Account Control Behavior Of The Elevation Prompt For Administrators**  
  Baseline default: *Prompt for consent on the secure desktop*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#useraccountcontrol_behavioroftheelevationpromptforadministrators)

- **User Account Control Behavior Of The Elevation Prompt For Standard Users**  
  Baseline default: *Automatically deny elevation requests*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#useraccountcontrol_behavioroftheelevationpromptforstandardusers)

- **User Account Control Detect Application Installations And Prompt For Elevation**  
  Baseline default: *Enable*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#useraccountcontrol-detectapplicationinstallationsandpromptforelevation)

- **User Account Control Only Elevate UI Access Applications That Are Installed In Secure Locations**
  Baseline default: *Enabled: Application runs with UIAccess integrity only if it resides in secure location.*
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#useraccountcontrol-onlyelevateuiaccessapplicationsthatareinstalledinsecurelocations)

- **User Account Control Run All Administrators In Admin Approval Mode**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#useraccountcontrol_runalladministratorsinadminapprovalmode)

- **User Account Control Use Admin Approval Mode**  
  Baseline default: *Enable*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#useraccountcontrol_useadminapprovalmode)

- **User Account Control Virtualize File And Registry Write Failures To Per User Locations**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#useraccountcontrol_virtualizefileandregistrywritefailurestoperuserlocations)

### Local Security Authority

- **Configure Lsa Protected Process**  
  Baseline default: *Enabled with UEFI lock. LSA will run as protected process and this configuration is UEFI locked.*  
  [Learn more](/windows/client-management/mdm/policy-csp-lsa#configurelsaprotectedprocess)
  <!-- UI Link is a 404 -->

### Microsoft App Store

- **Allow Game DVR**  
  Baseline default: *Block*  
  [Learn more](/windows/client-management/mdm/policy-csp-ApplicationManagement?WT.mc_id=Portal-fx#allowgamedvr)

- **MSI Allow User Control Over Install**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-ApplicationManagement?WT.mc_id=Portal-fx#msiallowusercontroloverinstall)

- **MSI Always Install With Elevated Privileges**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-ApplicationManagement?WT.mc_id=Portal-fx#msialwaysinstallwithelevatedprivileges)

### Microsoft Edge

#### SmartScreen settings

- **Configure Microsoft Defender SmartScreen**  
  Baseline default: *Enabled*

- **Prevent bypassing Microsoft Defender SmartScreen prompts for sites**  
  Baseline default: *Enabled*

### Privacy

- **Let Apps Activate With Voice Above Lock**  
  Baseline default: *Force deny. Windows apps cannot be activated by voice while the screen is locked, and users cannot change it.*  
  [Learn more](/windows/client-management/mdm/policy-csp-Privacy?WT.mc_id=Portal-fx#letappsactivatewithvoiceabovelock)

### Search

- **Allow Indexing Encrypted Stores Or Items**  
  Baseline default: *Block*  
  [Learn more](/windows/client-management/mdm/policy-csp-Search?WT.mc_id=Portal-fx#allowindexingencryptedstoresoritems)

### Smart Screen

- **Enable Smart Screen In Shell**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-smartscreen?WT.mc_id=Portal-fx#enablesmartscreeninshell)

- **Prevent Override For Files In Shell**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-smartscreen?WT.mc_id=Portal-fx#preventoverrideforfilesinshell)

#### Enhanced Phishing Protection

- **Notify Malicious**  
  Baseline default: *Enabled*

- **Notify Password Reuse**  
  Baseline default: *Enabled*

- **Notify Unsafe App**  
  Baseline default: *Enabled*

- **Service Enabled**  
  Baseline default: *Enabled*

### System Services

- **Configure Xbox Accessory Management Service Startup Mode**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-SystemServices?WT.mc_id=Portal-fx#configurexboxaccessorymanagementservicestartupmode)

- **Configure Xbox Live Auth Manager Service Startup Mode**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-SystemServices?WT.mc_id=Portal-fx#configurexboxliveauthmanagerservicestartupmode)

- **Configure Xbox Live Game Save Service Startup Mode**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-SystemServices?WT.mc_id=Portal-fx#configurexboxlivegamesaveservicestartupmode)

- **Configure Xbox Live Networking Service Startup Mode**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-SystemServices?WT.mc_id=Portal-fx#configurexboxlivenetworkingservicestartupmode)

### Task Scheduler

- **Enable Xbox Game Save Task**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-TaskScheduler?WT.mc_id=Portal-fx#enablexboxgamesavetask)

### User Rights

- **Access From Network**  
  Baseline default: *Configured*  
  Values: *Administrators* (*S-1-5-32-544), *Remote Desktop Users* (*S-1-5-32-555)  
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#accessfromnetwork)

- **Allow Local Log On**  
  Baseline default: *Configured*  
  Values: *Administrators* (*S-1-5-32-544), *Users* (*S-1-5-32-545)  
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#allowlocallogon)

- **Backup Files And Directories**  
  Baseline default: *Configured*  
  Value: *Administrators* (*S-1-5-32-544)  
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#backupfilesanddirectories)

- **Create Global Objects**  
  Baseline default: *Configured*  
  Values: *Administrators* (*S-1-5-32-544), *Local Service*  (*S-1-5-19), *Network Service* (*S-1-5-20), *Service* (*S-1-5-6)  
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#createglobalobjects)

- **Create Page File**  
  Baseline default: *Configured*  
  Value: *Administrators* (*S-1-5-32-544)  
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#createpagefile)

- **Debug Programs**  
  Baseline default: *Configured*  
  Value: *Administrators* (*S-1-5-32-544)  
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#debugprograms)

- **Deny Access From Network**  
  Baseline default: *Configured*  
  Value: *NT AUTHORITY\Local Account* (*S-1-5-113)  
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#denyaccessfromnetwork)

- **Deny Remote Desktop Services Log On**  
  Baseline default: *Configured*  
  Value: *NT AUTHORITY\Local Account* (*S-1-5-113)  
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#denyremotedesktopserviceslogon)

- **Impersonate Client**  
  Baseline default: *Configured*  
  Values: *Administrators* (*S-1-5-32-544), *Service* (*S-1-5-6), *Local Service* (*S-1-5-19), *Network Service* (*S-1-5-20)  
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#impersonateclient)

- **Load Unload Device Drivers**  
  Baseline default: *Configured*  
  Value: *Administrators* (*S-1-5-32-544)  
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#loadunloaddevicedrivers)

- **Manage Auditing And Security Log**  
  Baseline default: *Configured*  
  Value: *Administrators* (*S-1-5-32-544)  
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#manageauditingandsecuritylog)

- **Manage Volume**  
  Baseline default: *Configured*  
  Value: *Administrators* (*S-1-5-32-544)  
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#managevolume)

- **Modify Firmware Environment**  
  Baseline default: *Configured*  
  Value: *Administrators* (*S-1-5-32-544)  
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#modifyfirmwareenvironment)

- **Profile Single Process**  
  Baseline default: *Configured*  
  Value: *Administrators* (*S-1-5-32-544)  
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#profilesingleprocess)

- **Remote Shutdown**  
  Baseline default: *Configured*  
  Value: *Administrators* (*S-1-5-32-544)  
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#remoteshutdown)

- **Restore Files And Directories**  
  Baseline default: *Configured*  
  Value: *Administrators* (*S-1-5-32-544)  
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#restorefilesanddirectories)

- **Take Ownership**  
  Baseline default: *Configured*  
  Value: *Administrators* (*S-1-5-32-544)  
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#takeownership)

### Virtualization Based Technology

- **Hypervisor Enforced Code Integrity**  
  Baseline default: *(Enabled with UEFI lock) Turns on Hypervisor-Protected Code Integrity with UEFI lock.*  
  [Learn more](/windows/client-management/mdm/policy-csp-VirtualizationBasedTechnology?WT.mc_id=Portal-fx#hypervisorenforcedcodeintegrity)

### Wi-Fi Settings

- **Allow Auto Connect To Wi Fi Sense Hotspots**  
  Baseline default: *Block*  
  [Learn more](/windows/client-management/mdm/policy-csp-wifi?WT.mc_id=Portal-fx#allowautoconnecttowifisensehotspots)

- **Allow Internet Sharing**  
  Baseline default: *Block*  
  [Learn more](/windows/client-management/mdm/policy-csp-wifi?WT.mc_id=Portal-fx#allowinternetsharing)

### Windows Hello For Business

- **Facial Features Use Enhanced Anti Spoofing**  
  Baseline default: *true*  
  [Learn more](/windows/client-management/mdm/PassportForWork-csp/?WT.mc_id=Portal-fx#devicebiometricsfacialfeaturesuseenhancedantispoofing)

### Windows Ink Workspace

- **Allow Windows Ink Workspace**  
  Baseline default: *Ink workspace is enabled (feature is turned on), but the user cannot access it above the lock screen.*  
  [Learn more](/windows/client-management/mdm/policy-csp-WindowsInkWorkspace?WT.mc_id=Portal-fx#allowwindowsinkworkspace)

### LAPS
<!-- UI option uses 'Azure AD`, as does the CSP for options while the CSP description uses Microsoft Entra ID -->
- **Backup Directory**  
  Baseline default: *Backup the password to Azure AD only*  
  [Learn more](/windows/client-management/mdm/LAPS-csp/?WT.mc_id=Portal-fx#policiesbackupdirectory)

### Kerberos

- **PK Init Hash Algorithm Configuration**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-Kerberos?WT.mc_id=Portal-fx#pkinithashalgorithmconfiguration)

  - **PK Init Hash Algorithm SHA256**  
  Baseline default: *Supported*  
  [Learn more](/windows/client-management/mdm/policy-csp-Kerberos?WT.mc_id=Portal-fx#pkinithashalgorithmsha256)

  - **PK Init Hash Algorithm SHA384**  
  Baseline default: *Supported*  
  [Learn more](/windows/client-management/mdm/policy-csp-Kerberos?WT.mc_id=Portal-fx#pkinithashalgorithmsha384)

  - **PK Init Hash Algorithm SHA512**  
  Baseline default: *Supported*  
  [Learn more](/windows/client-management/mdm/policy-csp-Kerberos?WT.mc_id=Portal-fx#pkinithashalgorithmsha512)

  - **PK Init Hash Algorithm SHA1 PK Init Hash Algorithm SHA1**  
  Baseline default: *Not Supported*  
  [Learn more](/windows/client-management/mdm/policy-csp-Kerberos?WT.mc_id=Portal-fx#pkinithashalgorithmsha1)

### Sudo

- **Enable Sudo**  
  Baseline default: *Sudo is disabled.*  
  [Learn more](/windows/client-management/mdm/policy-csp-sudo)

::: zone-end

::: zone pivot="mdm-23h2"
## Security Baseline for Windows, version 23H2 

The settings in this baseline are taken from the **version 23H2** of the Group Policy security baseline as found in the [Security Compliance Toolkit and Baselines](https://www.microsoft.com/en-us/download/details.aspx?id=55319) from the Microsoft Download Center, and include only the settings that apply to Windows devices managed through Intune. When available, the setting name links to the source Configuration Service Provider (CSP), and then displays that settings default configuration in the baseline.

### Administrative Templates

#### Control Panel > Personalization

- **Prevent enabling lock screen camera**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-devicelock?WT.mc_id=Portal-fx#preventenablinglockscreencamera)

- **Prevent enabling lock screen slide show**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-devicelock?WT.mc_id=Portal-fx#preventlockscreenslideshow)

#### MS Security Guide

- **Apply UAC restrictions to local accounts on network logons**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-mssecurityguide?WT.mc_id=Portal-fx#applyuacrestrictionstolocalaccountsonnetworklogon)
  
- **Configure SMB v1 client driver**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-mssecurityguide?WT.mc_id=Portal-fx#configuresmbv1clientdriver)  
  - **Configure MrxSmb10 driver**  
    Baseline default: *Disable driver (recommended)*

- **Configure SMB v1 server**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-mssecurityguide?WT.mc_id=Portal-fx#configuresmbv1server)

- **Enable Structured Exception Handling Overwrite Protection (SEHOP)**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-mssecurityguide?WT.mc_id=Portal-fx#enablestructuredexceptionhandlingoverwriteprotection)

- **WDigest Authentication (disabling may require KB2871997)**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-mssecurityguide?WT.mc_id=Portal-fx#wdigestauthentication)

#### MSS (Legacy)

- **MSS: (DisableIPSourceRouting IPv6) IP source routing protection level (protects against packet spoofing)**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-msslegacy?WT.mc_id=Portal-fx#ipv6sourceroutingprotectionlevel)  
  - **DisableIPSourceRouting IPv6 (Device)**  
    Baseline default: *Highest protection, source routing is completely disabled*

- **MSS: (DisableIPSourceRouting) IP source routing protection level (protects against packet spoofing)**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-msslegacy?WT.mc_id=Portal-fx#ipsourceroutingprotectionlevel)
  - **DisableIPSourceRouting (Device)**  
    Baseline default: *Highest protection, source routing is completely disabled*

- **MSS: (EnableCMPRedirect) Allow ICMP redirects to override OSPF generated routes**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-msslegacy?WT.mc_id=Portal-fx#allowicmpredirectstooverrideospfgeneratedroutes)

- **MSS: (NoNameReleaseOnDemand) Allow the computer to ignore NetBIOS name release requests except from WINS servers**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-msslegacy?WT.mc_id=Portal-fx#allowthecomputertoignorenetbiosnamereleaserequestsexceptfromwinsservers)

#### Network > DNS Client

- **Turn off multicast name resolution**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-admx-dnsclient?WT.mc_id=Portal-fx#turn_off_multicast)

#### Network > Network Connections

- **Prohibit use of Internet Connection Sharing on your DNS domain network**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-admx-networkconnections?WT.mc_id=Portal-fx#nc-showsharedaccessui)

#### Network > Network Provider

- **Hardened UNC Paths**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-connectivity?WT.mc_id=Portal-fx#hardeneduncpaths)
  - **Hardened UNC Paths: (Device)**  
    Baseline defaults:

    | Name           | Value|
    |----------------|------|
    | `\\*\SYSVOL`   | RequireMutualAuthentication=1,RequireIntegrity=1 |
    | `\\*\NETLOGON` | RequireMutualAuthentication=1,RequireIntegrity=1 |

#### Network > Windows Connection Manager

- **Prohibit connection to non-domain networks when connected to domain authenticated network**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-windowsconnectionmanager?WT.mc_id=Portal-fx#prohitconnectiontonondomainnetworkswhenconnectedtodomainauthenticatednetwork)

#### Printers

- **Configure Redirection Guard**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-printers?WT.mc_id=Portal-fx#configureredirectionguardpolicy)
  - **Redirection Guard Options (Device)**  
    Baseline default: *Redirection Guard Enabled*

- **Configure RPC connection settings**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-printers?WT.mc_id=Portal-fx#configurerpcconnectionpolicy)
  - **Use authentication for outgoing RPC connections: (Device)**  
    Baseline default: *Default*  
  - **Protocol to allow for incoming RPC connections: (Device)**  
    Baseline default: *RPC over TCP*

- **Configure RPC listener settings**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-printers?WT.mc_id=Portal-fx#configurerpclistenerpolicy)  
  - **Protocols to allow for incoming RPC connections: (Device)**  
    Baseline default: *RCP over TCP*  
  - **Authentication protocol to use for incoming RPC connections: (Device)**  
    Baseline default: *Negotiate*

- **Configure RPC over TPC port**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-printers?WT.mc_id=Portal-fx#configurerpctcpport)  
  - **RPC over TCP port (Device)**  
    Baseline default: *0*

- **Limits print driver installation to Administrators**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-printers?WT.mc_id=Portal-fx#restrictdriverinstallationtoadministrators)

- **Manage processing of Queue-specific files**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-printers?WT.mc_id=Portal-fx#configurecopyfilespolicy)  
  - **Manage processing of Queue-specific files: (Device)**  
    Baseline default: *Limit Queue-specific files to Color profiles*

#### Start Menu and Taskbar > Notifications

- **Turn off toast notifications on the lock screen (User)**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-admx-wpn?WT.mc_id=Portal-fx#nolockscreentoastnotification)

#### System > Credentials Delegation

- **Encryption Oracle Remediation**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-admx-credssp?WT.mc_id=Portal-fx#allowencryptionoracle)
  - **Protection Level: (Device)**  
    Baseline default: *Force Updated Clients*

- **Remote host allows delegation of non-exportable credentials**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-credentialsdelegation?WT.mc_id=Portal-fx#remotehostallowsdelegationofnonexportablecredentials)

#### System > Device Installation > Device Installation Restrictions

- **Prevent installation of devices using drivers that match these device setup classes**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-deviceinstallation?WT.mc_id=Portal-fx#preventinstallationofmatchingdevicesetupclasses)
  - **Also apply to matching devices that are already installed**  
    Baseline default: *True*  
  - **Prevented Classes**  
    Baseline default: *{d48179be-ec20-11d1-b6b8-00c04fa372a7}*

#### System > Early Launch Antimalware

- **Boot-Start Driver Initialization Policy**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-system?WT.mc_id=Portal-fx#bootstartdriverinitialization)
  - **Choose the boot-start drivers that can be initialized:**  
    Baseline default: *Good, unknown and bad but critical*

#### System > Group Policy

- **Configure registry policy processing**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-admx-grouppolicy?WT.mc_id=Portal-fx#cse-registry)  
  - **Do not apply during periodic background processing (Device)**  
    Baseline default: *False*
  - **Process even if the Group Policy objects have not changed (Device)**  
    Baseline default: *True*

#### System > Internet Communication Management > Internet Communication settings

- **Turn off downloading of print drivers**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-connectivity?WT.mc_id=Portal-fx#disabledownloadingofprintdriversoverhttp)

- **Turn off Internet download for Web publishing and online ordering wizards**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-connectivity?WT.mc_id=Portal-fx#disableinternetdownloadforwebpublishingandonlineorderingwizards)

#### System > Local Security Authority

- **Allow Custom SSPs and APs to be loaded into LSASS**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-lsa#allowcustomsspsaps)

#### System > Power Management > Sleep Settings

- **Allow standby states (S1-S3) when sleeping (on battery)**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-power?WT.mc_id=Portal-fx#allowstandbystateswhensleepingonbattery)

- **Allow standby states (S1-S3) when sleeping (plugged in)**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-power?WT.mc_id=Portal-fx#allowstandbywhensleepingpluggedin)

- **Require a password when a computer wakes (on battery)**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-power?WT.mc_id=Portal-fx#requirepasswordwhencomputerwakesonbattery)

- **Require a password when a computer wakes (plugged in)**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-power?WT.mc_id=Portal-fx#requirepasswordwhencomputerwakespluggedin)

#### System > Remote Assistance

- **Configure Solicited Remote Assistance**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-remoteassistance?WT.mc_id=Portal-fx#solicitedremoteassistance)

#### System > Remote Procedure Call

- **Restrict Unauthenticated RPC clients**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-remoteprocedurecall?WT.mc_id=Portal-fx#restrictunauthenticatedrpcclients)
  - **RPC Runtime Unauthenticated Client Restriction to Apply:**  
    Baseline default: *Authenticated*

#### Windows Components > App runtime

- **Allow Microsoft accounts to be optional**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-appruntime?WT.mc_id=Portal-fx#allowmicrosoftaccountstobeoptional)

#### Windows Components > AutoPlay Policies

- **Disallow Autoplay for non-volume devices**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-autoplay?WT.mc_id=Portal-fx#disallowautoplayfornonvolumedevices)

- **Set the default behavior for AutoRun**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-autoplay?WT.mc_id=Portal-fx#setdefaultautorunbehavior)
  - **Default AutoRun Behavior**  
    Baseline default: *Do not execute any autorun commands*

- **Turn off Autoplay**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-autoplay?WT.mc_id=Portal-fx#turnoffautoplay)
  - **Turn off Autoplay on:**  
    Baseline default: *All drives*

#### Windows Components > BitLocker Drive Encryption > Fixed Data Drives

- **Deny write access to fixed drives not protected by BitLocker**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/bitlocker-csp?WT.mc_id=Portal-fx#fixeddrivesrequireencryption)

#### Windows Components > BitLocker Drive Encryption > Removable Data Drives

- **Deny write access to removable drives not protected by BitLocker**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/bitlocker-csp?WT.mc_id=Portal-fx#removabledrivesrequireencryption)
  - **Do not allow write access to devices configured in another organization**  
    Baseline default: *False*

#### Windows Components > Credential User Interface

- **Enumerate administrator accounts on elevation**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-credentialsui?WT.mc_id=Portal-fx#enumerateadministrators)

#### Windows Components > Event Log Service > Application

- **Specify the maximum log file size (KB)**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-eventlogservice?WT.mc_id=Portal-fx#specifymaximumfilesizeapplicationlog)
  - **Maximum Log Size (KB)**  
    Baseline default: *32768*

#### Windows Components > Event Log Service > Security

- **Specify the maximum log file size (KB)**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-eventlogservice?WT.mc_id=Portal-fx#specifymaximumfilesizesecuritylog)
  - **Maximum Log Size (KB)**  
    Baseline default: *196608*

#### Windows Components > Event Log Service > System

- **Specify the maximum log file size (KB)**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-eventlogservice?WT.mc_id=Portal-fx#specifymaximumfilesizesystemlog)
  - **Maximum Log Size (KB)**  
    Baseline default: *32768*

#### Windows Components > File Explorer

- **Configure Windows Defender SmartScreen**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-admx-windowsexplorer?WT.mc_id=Portal-fx#enablesmartscreen)
  - **Pick one of the following settings: (Device)**  
    Baseline default: *Warn and prevent bypass*

- **Turn off Data Execution Prevention for Explorer**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-fileexplorer?WT.mc_id=Portal-fx#turnoffdataexecutionpreventionforexplorer)

- **Turn off heap termination on corruption**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-fileexplorer?WT.mc_id=Portal-fx#turnoffheapterminationoncorruption)

#### Windows Components > Internet Explorer > Internet Control Panel > Advanced Page

- **Allow software to run or install even if the signature is invalid**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#allowsoftwarewhensignatureisinvalid)

- **Check for server certificate revocation**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#checkservercertificaterevocation)

- **Check for signatures on downloaded programs**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#checksignaturesondownloadedprograms)

- **Do not allow ActiveX controls to run in Protected Mode when Enhanced Protected Mode is enabled**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#donotallowactivexcontrolsinprotectedmode)

- **Turn off encryption support**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#disableencryptionsupport)
  - **Secure Protocol combinations**  
    Baseline default: *Use TLS 1.1 and TLS 1.2*

- **Turn on 64-bit tab processes when running in Enhanced Protected Mode on 64-bit versions of Windows**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#disableprocessesinenhancedprotectedmode)

- **Turn on Enhanced Protected Mode**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#allowenhancedprotectedmode)

#### Windows Components > Internet Explorer > Internet Control Panel

- **Prevent ignoring certificate errors**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#disableignoringcertificateerrors)

#### Windows Components > Internet Explorer > Internet Control Panel > Security Page > Internet Zone

- **Access data sources across domains**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowaccesstodatasources)
  - **Access data sources across domains**  
    Baseline default: *Disable*

- **Allow cut, copy or paste operations from the clipboard via script**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowcopypasteviascript)
  - **Allow paste operations via script**  
    Baseline default: *Disable*

- **Allow drag and drop or copy and paste files**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowdraganddropcopyandpastefiles)
  - **Allow drag and drop or copy and paste files**  
    Baseline default: *Disable*

- **Allow loading of XAML files**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowloadingofxamlfiles)
  - **XAML Files**  
    Baseline default: *Disable*

- **Allow only approved domains to use ActiveX controls without prompt**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowonlyapproveddomainstouseactivexcontrols)
  - **Only allow approved domains to use ActiveX controls without prompt**  
    Baseline default: *Enable*

- **Allow only approved domains to use the TDC ActiveX control**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowonlyapproveddomainstousetdcactivexcontrol)
  - **Only allow approved domains to use the TDC ActiveX control**  
    Baseline default: *Enable*

- **Allow script-initiated windows without size or position constraints**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowscriptinitiatedwindows)
  - **Allow script-initiated windows without size or position constraints**  
    Baseline default: *Disable*

- **Allow scripting of Internet Explorer WebBrowser controls**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowscriptingofinternetexplorerwebbrowsercontrols)
  - **Internet Explorer web browser control**  
    Baseline default: *Disable*

- **Allow scriptlets**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowscriptlets)
  - **Scriptlets**  
    Baseline default: *Disable*

- **Allow updates to status bar via script**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowupdatestostatusbarviascript)
  - **Status bar updates via script**  
    Baseline default: *Disable*

- **Allow VBScript to run in Internet Explorer**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowvbscripttorunininternetexplorer)
  - **Allow VBScript to run in Internet Explorer**  
    Baseline default: *Disable*

- **Automatic prompting for file downloads**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowautomaticpromptingforfiledownloads)
  - **Automatic prompting for file downloads**  
    Baseline default: *Disable*

- **Don't run antimalware programs against ActiveX controls**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzonedonotrunantimalwareagainstactivexcontrols)
  - **Don't run antimalware programs against ActiveX controls**  
    Baseline default: *Disable*

- **Download signed ActiveX controls**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzonedownloadsignedactivexcontrols)
  - **Download signed ActiveX controls**  
    Baseline default: *Disable*

- **Download unsigned ActiveX controls**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzonedownloadunsignedactivexcontrols)
  - **Download unsigned ActiveX controls**  
    Baseline default: *Disable*

- **Enable dragging of content from different domains across windows**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneenabledraggingofcontentfromdifferentdomainsacrosswindows)
  - **Enable dragging of content from different domains across windows**  
    Baseline default: *Disable*

- **Enable dragging of content from different domains within a window**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneenabledraggingofcontentfromdifferentdomainsacrosswindows)
  - **Enable dragging of content from different domains within a window**  
    Baseline default: *Disable*

- **Include local path when user is uploading files to a server**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneincludelocalpathwhenuploadingfilestoserver)
  - **Include local path when user is uploading files to a server**  
    Baseline default: *Disable*

- **Initialize and script ActiveX controls not marked as safe**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneinitializeandscriptactivexcontrols)
  - **Initialize and script ActiveX controls not marked as safe**  
    Baseline default: *Disable*

- **Java permissions**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzonejavapermissions)
  - **Java permissions**  
    Baseline default: *Disable Java*

- **Launching applications and files in an IFRAME**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzonelaunchingapplicationsandfilesiniframe)
  - **Launching applications and files in an IFRAME**  
    Baseline default: *Disable*

- **Logon options**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzonelogonoptions)
  - **Logon options**  
    Baseline default: *Prompt for user name and password*

- **Navigate windows and frames across different domains**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzonenavigatewindowsandframes)
  - **Navigate windows and frames across different domains**  
    Baseline default: *Disable*

- **Run .NET Framework-reliant components not signed with Authenticode**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallownetframeworkreliantcomponents)
  - **Run .NET Framework-reliant components not signed with Authenticode**  
    Baseline default: *Disable*

- **Run .NET Framework-reliant components signed with Authenticode**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzonerunnetframeworkreliantcomponentssignedwithauthenticode)
  - **Run .NET Framework-reliant components signed with Authenticode**  
    Baseline default: *Disable*

- **Show security warning for potentially unsafe files**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneshowsecuritywarningforpotentiallyunsafefiles)
  - **Launching programs and unsafe files**  
    Baseline default: *Prompt*

- **Turn on Cross-Site Scripting Filter**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneenablecrosssitescriptingfilter)
  - **Turn on Cross-Site Scripting (XSS) Filter**  
    Baseline default: *Enable*

- **Turn on Protected Mode**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneenableprotectedmode)
  - **Protected Mode**  
    Baseline default: *Enable*

- **Turn on SmartScreen Filter scan**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowsmartscreenie)
  - **Use SmartScreen Filter**  
    Baseline default: *Enable*

- **Userdata persistence**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowuserdatapersistence)
  - **Userdata persistence**  
    Baseline default: *Disable*

- **Web sites in less privileged Web content zones can navigate into this zone**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowlessprivilegedsites)
  - **Web sites in less privileged Web content zones can navigate into this zone**  
    Baseline default: *Disable*

#### Windows Components > Internet Explorer > Internet Control Panel > Security Page

- **Intranet Sites: Include all network paths (UNCs)**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#includeallnetworkpaths)

- **Turn on certificate address mismatch warning**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#allowcertificateaddressmismatchwarning)

#### Windows Components > Internet Explorer > Internet Control Panel > Security Page > Intranet Zone

- **Don't run antimalware programs against ActiveX controls**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#intranetzonedonotrunantimalwareagainstactivexcontrols)
  - **Don't run antimalware programs against ActiveX controls**  
    Baseline default: *Disable*

- **Initialize and script ActiveX controls not marked as safe**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#intranetzoneinitializeandscriptactivexcontrols)
  - **Initialize and script ActiveX controls not marked as safe**  
    Baseline default: *Disable*

- **Java permissions**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#intranetzonejavapermissions)
  - **Java permissions**  
    Baseline default: *High safety*

#### Windows Components > Internet Explorer > Internet Control Panel > Security Page > Local Machine Zone

- **Don't run antimalware programs against ActiveX controls**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#localmachinezonedonotrunantimalwareagainstactivexcontrols)
  - **Don't run antimalware programs against ActiveX controls**  
    Baseline default: *Disable*

- **Java permissions**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#localmachinezonejavapermissions)
  - **Java permissions**  
    Baseline default: *Disable Java*

#### Windows Components > Internet Explorer > Internet Control Panel > Security Page > Locked-Down Internet Zone

- **Turn on SmartScreen Filter scan**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#lockeddowninternetzoneallowsmartscreenie)
  - **Use SmartScreen Filter**  
    Baseline default: *Enable*

#### Windows Components > Internet Explorer > Internet Control Panel > Security Page > Locked-Down Intranet Zone

- **Java permissions**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#lockeddownintranetjavapermissions)
  - **Java permissions**  
    Baseline default: *Disable Java*

#### Windows Components > Internet Explorer > Internet Control Panel > Security Page > Locked-Down Local Machine Zone

- **Java permissions**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#lockeddownlocalmachinezonejavapermissions)
  - **Java permissions**  
    Baseline default: *Disable Java*

#### Windows Components > Internet Explorer > Internet Control Panel > Security Page > Locked-Down Restricted Sites Zone

- **Java permissions**  
  Baseline default: *Enabled*  
    [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#lockeddownlocalmachinezonejavapermissions)  
  - **Java permissions**  
    Baseline default: *Disable Java*

- **Turn on SmartScreen Filter scan**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#lockeddownrestrictedsiteszoneallowsmartscreenie)
  - **Use SmartScreen Filter**  
      Baseline default: *Enable*

#### Windows Components > Internet Explorer > Internet Control Panel > Security Page > Locked-Down Trusted Sites Zone

- **Java permissions**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#lockeddowntrustedsiteszonejavapermissions)
  - **Java permissions**  
    Baseline default: *Disable Java*

#### Windows Components > Internet Explorer > Internet Control Panel > Security Page > Restricted Sites Zone

- **Access data sources across domains**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowaccesstodatasources)
  - **Access data sources across domains**  
    Baseline default: *Disable*

- **Allow active scripting**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowactivescripting)
  - **Allow active scripting**  
    Baseline default: *Disable*

- **Allow binary and script behaviors**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowbinaryandscriptbehaviors)
  - **Allow binary and script behaviors**  
    Baseline default: *Disable*

- **Allow cut, copy or paste operations from the clipboard via script**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowcopypasteviascript)
  - **Allow paste operations via script**  
    Baseline default: *Disable*

- **Allow drag and drop or copy and paste files**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowdraganddropcopyandpastefiles)
  - **Allow drag and drop or copy and paste files**  
    Baseline default: *Disable*

- **Allow file downloads**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowfiledownloads)
  - **Allow file downloads**  
    Baseline default: *Disable*

- **Allow loading of XAML files**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowloadingofxamlfiles)
  - **XAML Files**  
    Baseline default: *Disable*

- **Allow META REFRESH**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowmetarefresh)
  - **Allow META REFRESH**  
    Baseline default: *Disable*

- **Allow only approved domains to use ActiveX controls without prompt**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowonlyapproveddomainstouseactivexcontrols)
  - **Only allow approved domains to use ActiveX controls without prompt**  
    Baseline default: *Enable*

- **Allow only approved domains to use the TDC ActiveX control**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowonlyapproveddomainstousetdcactivexcontrol)
  - **Only allow approved domains to use the TDC ActiveX control**  
    Baseline default: *Enable*

- **Allow script-initiated windows without size or position constraints**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowscriptinitiatedwindows)
  - **Allow script-initiated windows without size or position constraints**  
    Baseline default: *Disable*

- **Allow scripting of Internet Explorer WebBrowser controls**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowscriptingofinternetexplorerwebbrowsercontrols)
  - **Internet Explorer web browser control**  
    Baseline default: *Disable*

- **Allow scriptlets**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowscriptlets)
  - **Scriptlets**  
    Baseline default: *Disable*

- **Allow updates to status bar via script**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowupdatestostatusbarviascript)
  - **Status bar updates via script**  
    Baseline default: *Disable*

- **Allow VBScript to run in Internet Explorer**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowvbscripttorunininternetexplorer)
  - **Allow VBScript to run in Internet Explorer**  
    Baseline default: *Disable*

- **Automatic prompting for file downloads**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowautomaticpromptingforfiledownloads)
  - **Automatic prompting for file downloads**  
    Baseline default: *Disable*

- **Don't run antimalware programs against ActiveX controls**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszonedonotrunantimalwareagainstactivexcontrols)
  - **Don't run antimalware programs against ActiveX controls**  
    Baseline default: *Disable*

- **Download signed ActiveX controls**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszonedownloadsignedactivexcontrols)
  - **Download signed ActiveX controls**  
    Baseline default: *Disable*

- **Download unsigned ActiveX controls**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszonedownloadunsignedactivexcontrols)
  - **Download unsigned ActiveX controls**  
    Baseline default: *Disable*

- **Enable dragging of content from different domains across windows**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneenabledraggingofcontentfromdifferentdomainsacrosswindows)
  - **Enable dragging of content from different domains across windows**  
    Baseline default: *Disable*

- **Enable dragging of content from different domains within a window**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneenabledraggingofcontentfromdifferentdomainswithinwindows)
  - **Enable dragging of content from different domains within a window**  
    Baseline default: *Disable*

- **Include local path when user is uploading files to a server**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneincludelocalpathwhenuploadingfilestoserver)
  - **Include local directory path when uploading files to a server**  
    Baseline default: *Disable*

- **Initialize and script ActiveX controls not marked as safe**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneinitializeandscriptactivexcontrols)
  - **Initialize and script ActiveX controls not marked as safe**  
    Baseline default: *Disable*

- **Java permissions**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszonejavapermissions)
  - **Java permissions**  
    Baseline default: *Disable Java*

- **Launching applications and files in an IFRAME**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszonelaunchingapplicationsandfilesiniframe)
  - **Launching applications and files in an IFRAME**  
    Baseline default: *Disable*

- **Logon options**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszonelogonoptions)
  - **Logon options**  
    Baseline default: *Anonymous logon*

- **Navigate windows and frames across different domains**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszonenavigatewindowsandframes)
  - **Navigate windows and frames across different domains**  
    Baseline default: *Disable*

- **Run .NET Framework-reliant components not signed with Authenticode**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallownetframeworkreliantcomponents)
  - **Run .NET Framework-reliant components not signed with Authenticode**  
    Baseline default: *Disable*

- **Run .NET Framework-reliant components signed with Authenticode**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszonerunnetframeworkreliantcomponentssignedwithauthenticode)
  - **Run .NET Framework-reliant components signed with Authenticode**  
    Baseline default: *Disable*

- **Run ActiveX controls and plugins**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszonerunactivexcontrolsandplugins)
  - **Run ActiveX controls and plugins**  
    Baseline default: *Disable*

- **Script ActiveX controls marked safe for scripting**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszonescriptactivexcontrolsmarkedsafeforscripting)  
  - **Script ActiveX controls marked safe for scripting**  
    Baseline default: *Disable*

- **Scripting of Java applets**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszonescriptingofjavaapplets)
  - **Scripting of Java applets**  
    Baseline default: *Disable*

- **Show security warning for potentially unsafe files**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneshowsecuritywarningforpotentiallyunsafefiles)  
  - **Launching programs and unsafe files**  
    Baseline default: *Disable*

- **Turn on Cross-Site Scripting Filter**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneenablecrosssitescriptingfilter)
  - **Turn on Cross-Site Scripting (XSS) Filter**  
    Baseline default: *Enabled*

- **Turn on Protected Mode**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneturnonprotectedmode)
  - **Protected Mode**  
    Baseline default: *Enabled*

- **Turn on SmartScreen Filter scan**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowsmartscreenie)
  - **Use SmartScreen Filter**  
    Baseline default: *Enabled*

- **Use Pop-up Blocker**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneusepopupblocker)
  - **Use Pop-up Blocker**  
    Baseline default: *Enabled*

- **Userdata persistence**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowuserdatapersistence)
  - **Userdata persistence**  
    Baseline default: *Disable*

- **Web sites in less privileged Web content zones can navigate into this zone**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowlessprivilegedsites)
  - **Web sites in less privileged Web content zones can navigate into this zone**  
    Baseline default: *Disable*

#### Windows Components > Internet Explorer > Internet Control Panel > Security Page > Trusted Sites Zone

- **Don't run antimalware programs against ActiveX controls**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#trustedsiteszonedonotrunantimalwareagainstactivexcontrols)
  - **Don't run antimalware programs against ActiveX controls**  
    Baseline default: *Disable*

- **Initialize and script ActiveX controls not marked as safe**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#trustedsiteszoneinitializeandscriptactivexcontrols)
  - **Initialize and script ActiveX controls not marked as safe**  
    Baseline default: *Disable*

- **Java permissions**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#trustedsiteszonejavapermissions)
  - **Java permissions**  
    Baseline default: *High safety*

#### Windows Components > Internet Explorer

- **Prevent bypassing SmartScreen Filter warnings**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#disablebypassofsmartscreenwarnings)

- **Prevent bypassing SmartScreen Filter warnings about files that are not commonly downloaded from the Internet**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#disablebypassofsmartscreenwarningsaboutuncommonfiles)

- **Prevent managing SmartScreen Filter**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#preventmanagingsmartscreenfilter)
  - **Select SmartScreen Filter mode**  
    Baseline default: *On*

- **Prevent per-user installation of ActiveX controls**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#preventperuserinstallationofactivexcontrols)

- **Security Zones: Do not allow users to add/delete sites**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#donotallowuserstoaddsites)

- **Security Zones: Do not allow users to change policies**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#donotallowuserstochangepolicies)

- **Security Zones: Use only machine settings**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#securityzonesuseonlymachinesettings)

- **Specify use of ActiveX Installer Service for installation of ActiveX controls**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#specifyuseofactivexinstallerservice)

- **Turn off Crash Detection**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#disablecrashdetection)

- **Turn off the Security Settings Check feature**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#disablesecuritysettingscheck)

- **Turn on the auto-complete feature for user names and passwords on forms (User)**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#allowautocomplete)

#### Windows Components > Internet Explorer > Security Features > Add-on Management

- **Remove "Run this time" button for outdated ActiveX controls in Internet Explorer**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#removerunthistimebuttonforoutdatedactivexcontrols)

- **Turn off blocking of outdated ActiveX controls for Internet Explorer**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#donotblockoutdatedactivexcontrols)

#### Windows Components > Internet Explorer > Security Features

- **Allow fallback to SSL 3.0 (Internet Explorer)**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#allowfallbacktossl3)
  - **Allow insecure fallback for:**  
    Baseline default: *No Sites*

#### Windows Components > Internet Explorer > Security Features > Consistent Mime Handling

- **Internet Explorer Processes**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#consistentmimehandlinginternetexplorerprocesses)

#### Windows Components > Internet Explorer > Security Features > Mime Sniffing Safety Feature

- **Internet Explorer Processes**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#mimesniffingsafetyfeatureinternetexplorerprocesses)

#### Windows Components > Internet Explorer > Security Features > MK Protocol Security Restriction

- **Internet Explorer Processes**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#mkprotocolsecurityrestrictioninternetexplorerprocesses)

#### Windows Components > Internet Explorer > Security Features > Notification bar

- **Internet Explorer Processes**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#notificationbarinternetexplorerprocesses)

#### Windows Components > Internet Explorer > Security Features > Protection From Zone Elevation

- **Internet Explorer Processes**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#protectionfromzoneelevationinternetexplorerprocesses)

#### Windows Components > Internet Explorer > Security Features > Restrict ActiveX Install

- **Internet Explorer Processes**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictactivexinstallinternetexplorerprocesses)

#### Windows Components > Internet Explorer > Security Features > Restrict File Download

- **Internet Explorer Processes**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictfiledownloadinternetexplorerprocesses)

#### Windows Components > Internet Explorer > Security Features > Scripted Window Security Restrictions

- **Internet Explorer Processes**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#scriptedwindowsecurityrestrictionsinternetexplorerprocesses)

#### Windows Components > Microsoft Defender Antivirus > MAPS

- **Configure the 'Block at First Sight' feature**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-admx-microsoftdefenderantivirus?WT.mc_id=Portal-fx#disableblockatfirstseen)

#### Windows Components > Microsoft Defender Antivirus > Real-time Protection

- **Turn on process scanning whenever real-time protection is enabled**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-admx-microsoftdefenderantivirus?WT.mc_id=Portal-fx#realtimeprotection-disablescanonrealtimeenable)

#### Windows Components > Microsoft Defender Antivirus > Scan

- **Scan packed executables**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-admx-microsoftdefenderantivirus?WT.mc_id=Portal-fx#scan-disablepackedexescanning)

#### Windows Components > Microsoft Defender Antivirus

- **Turn off routine remediation**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-admx-microsoftdefenderantivirus?WT.mc_id=Portal-fx#disableroutinelytakingaction)

#### Windows Components > Remote Desktop Services > Remote Desktop Connection Client

- **Do not allow passwords to be saved**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-remotedesktopservices?WT.mc_id=Portal-fx#donotallowpasswordsaving)

#### Windows Components > Remote Desktop Services > Remote Desktop Session Host > Device and Resource Redirection

- **Do not allow drive redirection**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-remotedesktopservices?WT.mc_id=Portal-fx#donotallowdriveredirection)

#### Windows Components > Remote Desktop Services > Remote Desktop Session Host > Security

- **Always prompt for password upon connection**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-remotedesktopservices?WT.mc_id=Portal-fx#promptforpassworduponconnection)

- **Require secure RPC communication**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-remotedesktopservices?WT.mc_id=Portal-fx#requiresecurerpccommunication)

- **Set client connection encryption level**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-remotedesktopservices?WT.mc_id=Portal-fx#clientconnectionencryptionlevel)
  - **Encryption Level**  
    Baseline default: *High Level*  

#### Windows Components > RSS Feeds

- **Prevent downloading of enclosures**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#disableenclosuredownloading)

#### Windows Components > Windows Logon Options

- **Enable MPR notifications for the system**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-windowslogon?WT.mc_id=Portal-fx#enablemprnotifications)

- **Sign-in and lock last interactive user automatically after a restart**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-windowslogon?WT.mc_id=Portal-fx#allowautomaticrestartsignon)

#### Windows Components > Windows PowerShell

- **Turn on PowerShell Script Block Logging**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-windowspowershell?WT.mc_id=Portal-fx#turnonpowershellscriptblocklogging)
  - **Log script block invocation start / stop events:**  
    Baseline default: *False*  

#### Windows Components > Windows Remote Management (WinRM) > WinRM Client

- **Allow Basic authentication**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-remotemanagement?WT.mc_id=Portal-fx#allowbasicauthentication-service)

- **Allow unencrypted traffic**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-remotemanagement?WT.mc_id=Portal-fx#allowunencryptedtraffic-client)

- **Disallow Digest authentication**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-remotemanagement?WT.mc_id=Portal-fx#disallowdigestauthentication)

#### Windows Components > Windows Remote Management (WinRM) > WinRM Service

- **Allow Basic authentication**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-remotemanagement?WT.mc_id=Portal-fx#allowbasicauthentication-service)

- **Allow unencrypted traffic**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-remotemanagement?WT.mc_id=Portal-fx#allowunencryptedtraffic-service)

- **Disallow WinRM from storing RunAs credentials**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-remotemanagement?WT.mc_id=Portal-fx#disallowstoringofrunascredentials)

### Auditing

- **Account Logon Audit Credential Validation**  
  Baseline default: *Success+ Failure*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#accountlogon_auditcredentialvalidation)

- **Account Logon Logoff Audit Account Lockout**  
  Baseline default: *Failure*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#accountlogonlogoff_auditaccountlockout)

- **Account Logon Logoff Audit Group Membership**  
  Baseline default: *Success*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#accountlogonlogoff_auditgroupmembership)

- **Account Logon Logoff Audit Logon**  
  Baseline default: *Success+ Failure*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#accountlogonlogoff_auditlogon)

- **Audit Authentication Policy Change**  
  Baseline default: *Success*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#policychange_auditauthenticationpolicychange)

- **Audit Changes to Audit Policy**  
  Baseline default: *Success*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#policychange_auditpolicychange)

- **Audit File Share Access**  
  Baseline default: *Success+ Failure*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#objectaccess_auditfileshare)

- **Audit Other Logon Logoff Events**  
  Baseline default: *Success+ Failure*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#accountlogonlogoff_auditotherlogonlogoffevents)

- **Audit Security Group Management**  
  Baseline default: *Success*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#accountmanagement_auditsecuritygroupmanagement)

- **Audit Security System Extension**  
  Baseline default: *Success*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#system_auditsecuritysystemextension)

- **Audit Special Logon**  
  Baseline default: *Success*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#accountlogonlogoff_auditspeciallogon)

- **Audit User Account Management**  
  Baseline default: *Success+ Failure*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#accountmanagement_audituseraccountmanagement)

- **Detailed Tracking Audit PNP Activity**  
  Baseline default: *Success*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#detailedtracking_auditpnpactivity)

- **Detailed Tracking Audit Process Creation**  
  Baseline default: *Success*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#detailedtracking_auditprocesscreation)

- **Object Access Audit Detailed File Share**  
  Baseline default: *Failure*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#objectaccess_auditdetailedfileshare)

- **Object Access Audit Other Object Access Events**  
  Baseline default: *Success+ Failure*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#objectaccess_auditotherobjectaccessevents)

- **Object Access Audit Removable Storage**  
  Baseline default: *Success+ Failure*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#objectaccess_auditremovablestorage)

- **Policy Change Audit MPSSVC Rule Level Policy Change**  
  Baseline default: *Success+ Failure*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#policychange_auditmpssvcrulelevelpolicychange)

- **Policy Change Audit Other Policy Change Events**  
  Baseline default: *Failure*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#policychange_auditotherpolicychangeevents)

- **Privilege Use Audit Sensitive Privilege Use**  
  Baseline default: *Success*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#privilegeuse_auditsensitiveprivilegeuse)

- **System Audit Other System Events**  
  Baseline default: *Success+ Failure*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#system_auditothersystemevents)

- **System Audit Security State Change**  
  Baseline default: *Success*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#system_auditsecuritystatechange)

- **System Audit System Integrity**  
  Baseline default: *Success+ Failure*  
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#system_auditsystemintegrity)

### Browser

- **Allow Password Manager**  
  Baseline default: *Block*  
  [Learn more](/windows/client-management/mdm/policy-csp-Browser?WT.mc_id=Portal-fx#allowpasswordmanager)
 
- **Allow Smart Screen**  
  Baseline default: *Allow*  
  [Learn more](/windows/client-management/mdm/policy-csp-Browser?WT.mc_id=Portal-fx#allowsmartscreen)

- **Prevent Cert Error Overrides**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-Browser?WT.mc_id=Portal-fx#preventcerterroroverrides)

- **Prevent Smart Screen Prompt Override**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-Browser?WT.mc_id=Portal-fx#preventsmartscreenpromptoverride)

- **Prevent Smart Screen Prompt Override For Files**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-Browser?WT.mc_id=Portal-fx#preventsmartscreenpromptoverrideforfiles)

### Data Protection

- **Allow Direct Memory Access**  
  Baseline default: *Block*  
  [Learn more](/windows/client-management/mdm/policy-csp-dataprotection?WT.mc_id=Portal-fx#allowdirectmemoryaccess)

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

- **Allow Full Scan Removable Drive Scanning**  
  Baseline default: *Allowed. Scans removable drives.*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#allowfullscanremovabledrivescanning)

- **Allow On Access Protection**  
  Baseline default: *Allowed.*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#allowonaccessprotection)

- **Allow Realtime Monitoring**  
  Baseline default: *Allowed. Turns on and runs the real-time monitoring service.*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#allowrealtimemonitoring)

- **Allow scanning of all downloaded files and attachments**  
  Baseline default: *Allowed.*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#allowioavprotection)

- **Allow Script Scanning**  
  Baseline default: *Allowed.*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#allowscriptscanning)
  - **Block execution of potentially obfuscated scripts**  
    Baseline default: *Block*  
    [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)
  - **Block Win32 API calls from Office macros**  
    Baseline default: *Block*  
    [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)
  - **Block Office communication application from creating child processes**  
    Baseline default: *Block*  
    [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)
  - **Block all Office applications from creating child processes**  
    Baseline default: *Block*  
    [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)
  - **Block JavaScript or VBScript from launching downloaded executable content**  
    Baseline default: *Block*  
    [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)
  - **Block untrusted and unsigned processes that run from USB**  
    Baseline default: *Block*  
    [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)
  - **Block Adobe Reader from creating child processes**  
    Baseline default: *Block*  
    [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)
  - **Block credential stealing from the Windows local security authority subsystem**  
    Baseline default: *Block*  
    [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)
  - **Block Office applications from creating executable content**  
    Baseline default: *Block*  
    [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)
  - **Block Office applications from injecting code into other processes**  
    Baseline default: *Block*  
    [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)
  - **Block executable content from email client and webmail**  
    Baseline default: *Block*  
    [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)

- **Cloud Block Level**  
  Baseline default: *High*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#cloudblocklevel)

- **Cloud Extended Timeout**  
  Baseline default: *Configured*  
  Value: *50*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#cloudextendedtimeout)

- **Disable Local Admin Merge**  
  Baseline default: *Disable Local Admin Merge*  
  [Learn more](/windows/client-management/mdm/Defender-csp/?WT.mc_id=Portal-fx#configurationdisablelocaladminmerge)

- **Enable File Hash Computation**  
  Baseline default: *Enable*  
  [Learn more](/windows/client-management/mdm/Defender-csp/?WT.mc_id=Portal-fx#configurationenablefilehashcomputation)

- **Enable Network Protection**  
  Baseline default: *Enabled (block mode)*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#enablenetworkprotection)

- **Hide Exclusions From Local Admins**  
  Baseline default: *If you enable this setting, local admins will no longer be able to see the exclusion list in Windows Security App or via PowerShell.*  
  [Learn more](/windows/client-management/mdm/Defender-csp/?WT.mc_id=Portal-fx#configurationhideexclusionsfromlocaladmins)

- **PUA Protection**  
  Baseline default: *PUA Protection on. Detected items are blocked. They will show in history along with other threats.*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#puaprotection)

- **Real Time Scan Direction**  
  Baseline default: *Monitor all files (bi-directional).*  
  [Learn more](/windows/client-management/mdm/policy-csp-Defender?WT.mc_id=Portal-fx##realtimescandirection)

- **Submit Samples Consent**  
  Baseline default: *Send all samples automatically.*  
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#submitsamplesconsent)

### Device Guard

- **Configure System Guard Launch**  
  Baseline default: *Unmanaged Enables Secure Launch if supported by hardware*  
  [Learn more](/windows/client-management/mdm/policy-csp-deviceguard?WT.mc_id=Portal-fx#configuresystemguardlaunch)

- **Credential Guard**  
  Baseline default: *(Enabled with UEFI lock) Turns on Credential Guard with UEFI lock.*  
  [Learn more](/windows/client-management/mdm/policy-csp-deviceguard?WT.mc_id=Portal-fx#lsacfgflags)

- **Enable Virtualization Based Security**  
  Baseline default: *Enable virtualization based security.*  
  [Learn more](/windows/client-management/mdm/policy-csp-deviceguard?WT.mc_id=Portal-fx#enablevirtualizationbasedsecurity)

- **Require Platform Security Features**  
  Baseline default: *Turns on VBS with Secure Boot.*  
  [Learn more](/windows/client-management/mdm/policy-csp-deviceguard?WT.mc_id=Portal-fx#requireplatformsecurityfeatures)

### Device Lock

- **Device Password Enabled**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-devicelock?WT.mc_id=Portal-fx#devicepasswordenabled)
  - **Device Password History**  
    Baseline default: *Configured*  
    Value: *24*  
    [Learn more](/windows/client-management/mdm/policy-csp-devicelock?WT.mc_id=Portal-fx#devicepasswordhistory)
  - **Min Device Password Length**  
    Baseline default: *Configured*  
    Value: *14*  
    [Learn more](/windows/client-management/mdm/policy-csp-devicelock?WT.mc_id=Portal-fx#mindevicepasswordlength)

### Dma Guard

- **Device Enumeration Policy**  
  Baseline default: *Block all (Most restrictive)*  
  [Learn more](/windows/client-management/mdm/policy-csp-dmaguard?WT.mc_id=Portal-fx#deviceenumerationpolicy)

### Experience

- **Allow Windows Spotlight (User)**  
  Baseline default: *Allow*  
  [Learn more](/windows/client-management/mdm/policy-csp-Experience?WT.mc_id=Portal-fx#allowwindowsspotlight)
  - **Allow Windows Consumer Features**  
    Baseline default: *Block*  
    [Learn more](/windows/client-management/mdm/policy-csp-experience?WT.mc_id=Portal-fx#allowwindowsconsumerfeatures)
  - **Allow Third Party Suggestions In Windows Spotlight (User)**  
    Baseline default: *Block*  
    [Learn more](/windows/client-management/mdm/policy-csp-Experience?WT.mc_id=Portal-fx#allowthirdpartysuggestionsinwindowsspotlight)

### Firewall

- **Enable Domain Network Firewall**  
  Baseline default: *True*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoredomainprofileenablefirewall)
  - **Enable Log Success Connections**  
    Baseline default: *Enable Logging Of Successful Connections*  
    [Learn more](/windows/client-management/mdm/Firewall-csp/?WT.mc_id=Portal-fx#mdmstoredomainprofileenablelogsuccessconnections)
  - **Default Outbound Action**  
    Baseline default: *Allow*  
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoredomainprofiledefaultoutboundaction)
  - **Enable Log Dropped Packets**  
    Baseline default: *Enable Logging Of Dropped Packets*  
    [Learn more](/windows/client-management/mdm/Firewall-csp/?WT.mc_id=Portal-fx#mdmstoredomainprofileenablelogdroppedpackets)
  - **Disable Inbound Notifications**  
    Baseline default: *True*  
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoredomainprofiledisableinboundnotifications)
  - **Log Max File Size**  
    Baseline default: *16384*  
    [Learn more](/windows/client-management/mdm/Firewall-csp/?WT.mc_id=Portal-fx#mdmstoredomainprofilelogmaxfilesize)
  - **Default Inbound Action for Domain Profile**  
    Baseline default: *Block*  
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoredomainprofiledefaultinboundaction)

- **Enable Private Network Firewall**  
  Baseline default: *True*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreprivateprofileenablefirewall)
  - **Log Max File Size**  
    Baseline default: *16384*  
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreprivateprofilelogmaxfilesize)
  - **Default Inbound Action for Private Profile**  
    Baseline default: *Block*  
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreprivateprofiledefaultinboundaction)
  - **Enable Log Success Connections**  
    Baseline default: *Enable Logging Of Successful Connections*  
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreprivateprofileenablelogsuccessconnections)
  - **Enable Log Dropped Packets**  
    Baseline default: *Enable Logging Of Dropped Packets*  
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreprivateprofileenablelogdroppedpackets)
  - **Default Outbound Action**  
    Baseline default: *Allow*  
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreprivateprofiledefaultoutboundaction)
  - **Disable Inbound Notifications**  
    Baseline default: *True*  
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreprivateprofiledisableinboundnotifications)

- **Enable Public Network Firewall**  
  Baseline default: *True*  
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofileenablefirewall)
  - **Enable Log Dropped Packets**  
    Baseline default: *Enable Logging Of Dropped Packets*  
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofileenablelogdroppedpackets)
  - **Log Max File Size**  
    Baseline default: *16384*  
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofilelogmaxfilesize)
  - **Default Outbound Action**  
    Baseline default: *Allow*  
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofiledefaultoutboundaction)
  - **Disable Inbound Notifications**  
    Baseline default: *True*  
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofiledisableinboundnotifications)
  - **Default Inbound Action for Public Profile**  
    Baseline default: *Block*  
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofiledefaultinboundaction)
  - **Allow Local Policy Merge**  
    Baseline default: *False*  
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofileallowlocalpolicymerge)
  - **Enable Log Success Connections**  
    Baseline default: *Enable Logging Of Successful Connections*  
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofileenablelogsuccessconnections)
  - **Allow Local Ipsec Policy Merge**  
    Baseline default: *False*  
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofileallowlocalipsecpolicymerge)

### Lanman Workstation

- **Enable Insecure Guest Logons**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-LanmanWorkstation?WT.mc_id=Portal-fx#enableinsecureguestlogons)

### Local Policies Security Options
  <!-- UI Links add - in place of url which uses _ -->
- **Accounts Limit Local Account Use Of Blank Passwords To Console Logon Only**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#accounts_limitlocalaccountuseofblankpasswordstoconsolelogononly)

- **Interactive Logon Machine Inactivity Limit**  
  Baseline default: *Configured*  
  Value: *900*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#interactivelogon_machineinactivitylimit)

- **Interactive Logon Smart Card Removal Behavior**  
  Baseline default: *Lock Workstation*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#interactivelogon_smartcardremovalbehavior)

- **Microsoft Network Client Digitally Sign Communications Always**  
  Baseline default: *Enable*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#microsoftnetworkclient_digitallysigncommunicationsalways)

- **Microsoft Network Client Send Unencrypted Password To Third Party SMB Servers**  
  Baseline default: *Disable*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#microsoftnetworkclient_sendunencryptedpasswordtothirdpartysmbservers)

- **Microsoft Network Server Digitally Sign Communications Always**  
  Baseline default: *Enable*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#microsoftnetworkserver_digitallysigncommunicationsalways)

- **Network Access Do Not Allow Anonymous Enumeration Of SAM Accounts**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#networkaccess_donotallowanonymousenumerationofsamaccounts)

- **Network Access Do Not Allow Anonymous Enumeration Of Sam Accounts And Shares**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#networkaccess_donotallowanonymousenumerationofsamaccountsandshares)

- **Network Access Restrict Anonymous Access To Named Pipes And Shares**  
  Baseline default *Enable*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#networkaccess-restrictanonymousaccesstonamedpipesandshares)

- **Network Access Restrict Clients Allowed To Make Remote Calls To SAM**  
  Baseline default: *Configured*  
  Value: *O:BAG:BAD:(A;;RC;;;BA)*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#networkaccess_restrictclientsallowedtomakeremotecallstosam)

- **Network Security Do Not Store LAN Manager Hash Value On Next Password Change**  
  Baseline default: *Enable*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#networksecurity_donotstorelanmanagerhashvalueonnextpasswordchange)

- **Network Security LAN Manager Authentication Level**  
  Baseline default: *Send LM and NTLMv2 responses only. Refuse LM and NTLM*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#networksecurity_lanmanagerauthenticationlevel)

- **Network Security Minimum Session Security For NTLMSSP Based Clients**  
  Baseline default: *Require NTLM and 128-bit encryption*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#networksecurity_minimumsessionsecurityforntlmsspbasedclients)

- **Network Security Minimum Session Security For NTLMSSP Based Servers**  
  Baseline default: *Require NTLM and 128-bit encryption*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#networksecurity_minimumsessionsecurityforntlmsspbasedservers)

- **User Account Control Behavior Of The Elevation Prompt For Administrators**  
  Baseline default: *Prompt for consent on the secure desktop*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#useraccountcontrol_behavioroftheelevationpromptforadministrators)

- **User Account Control Behavior Of The Elevation Prompt For Standard Users**  
  Baseline default: *Automatically deny elevation requests*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#useraccountcontrol_behavioroftheelevationpromptforstandardusers)

- **User Account Control Detect Application Installations And Prompt For Elevation**  
  Baseline default: *Enable*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#useraccountcontrol-detectapplicationinstallationsandpromptforelevation)

- **User Account Control Only Elevate UI Access Applications That Are Installed In Secure Locations**
  Baseline default: *Enabled: Application runs with UIAccess integrity only if it resides in secure location.*
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#useraccountcontrol-onlyelevateuiaccessapplicationsthatareinstalledinsecurelocations)

- **User Account Control Run All Administrators In Admin Approval Mode**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#useraccountcontrol_runalladministratorsinadminapprovalmode)

- **User Account Control Use Admin Approval Mode**  
  Baseline default: *Enable*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#useraccountcontrol_useadminapprovalmode)

- **User Account Control Virtualize File And Registry Write Failures To Per User Locations**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#useraccountcontrol_virtualizefileandregistrywritefailurestoperuserlocations)

### Local Security Authority

- **Configure Lsa Protected Process**  
  Baseline default: *Enabled with UEFI lock. LSA will run as protected process and this configuration is UEFI locked.*  
  [Learn more](/windows/client-management/mdm/policy-csp-lsa#configurelsaprotectedprocess)
  <!-- UI Link is a 404 -->

### Microsoft App Store

- **Allow Game DVR**  
  Baseline default: *Block*  
  [Learn more](/windows/client-management/mdm/policy-csp-ApplicationManagement?WT.mc_id=Portal-fx#allowgamedvr)

- **MSI Allow User Control Over Install**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-ApplicationManagement?WT.mc_id=Portal-fx#msiallowusercontroloverinstall)

- **MSI Always Install With Elevated Privileges**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-ApplicationManagement?WT.mc_id=Portal-fx#msialwaysinstallwithelevatedprivileges)

### Microsoft Edge

#### SmartScreen settings

- **Configure Microsoft Defender SmartScreen**  
  Baseline default: *Enabled*

- **Prevent bypassing Microsoft Defender SmartScreen prompts for sites**  
  Baseline default: *Enabled*

### Privacy

- **Let Apps Activate With Voice Above Lock**  
  Baseline default: *Force deny. Windows apps cannot be activated by voice while the screen is locked, and users cannot change it.*  
  [Learn more](/windows/client-management/mdm/policy-csp-Privacy?WT.mc_id=Portal-fx#letappsactivatewithvoiceabovelock)

### Search

- **Allow Indexing Encrypted Stores Or Items**  
  Baseline default: *Block*  
  [Learn more](/windows/client-management/mdm/policy-csp-Search?WT.mc_id=Portal-fx#allowindexingencryptedstoresoritems)

### Smart Screen

- **Enable Smart Screen In Shell**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-smartscreen?WT.mc_id=Portal-fx#enablesmartscreeninshell)

- **Prevent Override For Files In Shell**  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-smartscreen?WT.mc_id=Portal-fx#preventoverrideforfilesinshell)

#### Enhanced Phishing Protection

- **Notify Malicious**  
  Baseline default: *Enabled*

- **Notify Password Reuse**  
  Baseline default: *Enabled*

- **Notify Unsafe App**  
  Baseline default: *Enabled*

- **Service Enabled**  
  Baseline default: *Enabled*

### System Services

- **Configure Xbox Accessory Management Service Startup Mode**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-SystemServices?WT.mc_id=Portal-fx#configurexboxaccessorymanagementservicestartupmode)

- **Configure Xbox Live Auth Manager Service Startup Mode**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-SystemServices?WT.mc_id=Portal-fx#configurexboxliveauthmanagerservicestartupmode)

- **Configure Xbox Live Game Save Service Startup Mode**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-SystemServices?WT.mc_id=Portal-fx#configurexboxlivegamesaveservicestartupmode)

- **Configure Xbox Live Networking Service Startup Mode**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-SystemServices?WT.mc_id=Portal-fx#configurexboxlivenetworkingservicestartupmode)

### Task Scheduler

- **Enable Xbox Game Save Task**  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-TaskScheduler?WT.mc_id=Portal-fx#enablexboxgamesavetask)

### User Rights

- **Access From Network**  
  Baseline default: *Configured*  
  Values: *Administrators* (*S-1-5-32-544), *Remote Desktop Users* (*S-1-5-32-555)  
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#accessfromnetwork)

- **Allow Local Log On**  
  Baseline default: *Configured*  
  Values: *Administrators* (*S-1-5-32-544), *Users* (*S-1-5-32-545)  
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#allowlocallogon)

- **Backup Files And Directories**  
  Baseline default: *Configured*  
  Value: *Administrators* (*S-1-5-32-544)  
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#backupfilesanddirectories)

- **Create Global Objects**  
  Baseline default: *Configured*  
  Values: *Administrators* (*S-1-5-32-544), *Local Service*  (*S-1-5-19), *Network Service* (*S-1-5-20), *Service* (*S-1-5-6)  
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#createglobalobjects)

- **Create Page File**  
  Baseline default: *Configured*  
  Value: *Administrators* (*S-1-5-32-544)  
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#createpagefile)

- **Debug Programs**  
  Baseline default: *Configured*  
  Value: *Administrators* (*S-1-5-32-544)  
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#debugprograms)

- **Deny Access From Network**  
  Baseline default: *Configured*  
  Value: *NT AUTHORITY\Local Account* (*S-1-5-113)  
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#denyaccessfromnetwork)

- **Deny Remote Desktop Services Log On**  
  Baseline default: *Configured*  
  Value: *NT AUTHORITY\Local Account* (*S-1-5-113)  
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#denyremotedesktopserviceslogon)

- **Impersonate Client**  
  Baseline default: *Configured*  
  Values: *Administrators* (*S-1-5-32-544), *Service* (*S-1-5-6), *Local Service* (*S-1-5-19), *Network Service* (*S-1-5-20)  
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#impersonateclient)

- **Load Unload Device Drivers**  
  Baseline default: *Configured*  
  Value: *Administrators* (*S-1-5-32-544)  
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#loadunloaddevicedrivers)

- **Manage Auditing And Security Log**  
  Baseline default: *Configured*  
  Value: *Administrators* (*S-1-5-32-544)  
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#manageauditingandsecuritylog)

- **Manage Volume**  
  Baseline default: *Configured*  
  Value: *Administrators* (*S-1-5-32-544)  
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#managevolume)

- **Modify Firmware Environment**  
  Baseline default: *Configured*  
  Value: *Administrators* (*S-1-5-32-544)  
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#modifyfirmwareenvironment)

- **Profile Single Process**  
  Baseline default: *Configured*  
  Value: *Administrators* (*S-1-5-32-544)  
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#profilesingleprocess)

- **Remote Shutdown**  
  Baseline default: *Configured*  
  Value: *Administrators* (*S-1-5-32-544)  
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#remoteshutdown)

- **Restore Files And Directories**  
  Baseline default: *Configured*  
  Value: *Administrators* (*S-1-5-32-544)  
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#restorefilesanddirectories)

- **Take Ownership**  
  Baseline default: *Configured*  
  Value: *Administrators* (*S-1-5-32-544)  
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#takeownership)

### Virtualization Based Technology

- **Hypervisor Enforced Code Integrity**  
  Baseline default: *(Enabled with UEFI lock) Turns on Hypervisor-Protected Code Integrity with UEFI lock.*  
  [Learn more](/windows/client-management/mdm/policy-csp-VirtualizationBasedTechnology?WT.mc_id=Portal-fx#hypervisorenforcedcodeintegrity)

### Wi-Fi Settings

- **Allow Auto Connect To Wi Fi Sense Hotspots**  
  Baseline default: *Block*  
  [Learn more](/windows/client-management/mdm/policy-csp-wifi?WT.mc_id=Portal-fx#allowautoconnecttowifisensehotspots)

- **Allow Internet Sharing**  
  Baseline default: *Block*  
  [Learn more](/windows/client-management/mdm/policy-csp-wifi?WT.mc_id=Portal-fx#allowinternetsharing)

### Windows Hello For Business

- **Facial Features Use Enhanced Anti Spoofing**  
  Baseline default: *true*  
  [Learn more](/windows/client-management/mdm/PassportForWork-csp/?WT.mc_id=Portal-fx#devicebiometricsfacialfeaturesuseenhancedantispoofing)

### Windows Ink Workspace

- **Allow Windows Ink Workspace**  
  Baseline default: *Ink workspace is enabled (feature is turned on), but the user cannot access it above the lock screen.*  
  [Learn more](/windows/client-management/mdm/policy-csp-WindowsInkWorkspace?WT.mc_id=Portal-fx#allowwindowsinkworkspace)

### LAPS
<!-- UI option uses 'Azure AD`, as does the CSP for options while the CSP description uses Microsoft Entra ID -->
- **Backup Directory**  
  Baseline default: *Backup the password to Azure AD only*  
  [Learn more](/windows/client-management/mdm/LAPS-csp/?WT.mc_id=Portal-fx#policiesbackupdirectory)


::: zone-end


<!-- Begin older baselines that share similar category structures
-->

::: zone pivot="mdm-november-2021"
## Security Baseline for Windows, November 2021
::: zone-end
::: zone pivot="mdm-december-2020"
## Security Baseline for Windows, December 2020
::: zone-end
::: zone pivot="mdm-august-2020"
## Security Baseline for Windows, August 2020
::: zone-end

::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"
### Above Lock

- **Voice activate apps from locked screen**:  
  Baseline default: *Disabled*  
  [Learn More](/windows/client-management/mdm/policy-csp-privacy)

- **Block display of toast notifications**:  
  Baseline default: *Yes*  
  [Learn More](/windows/client-management/mdm/policy-csp-abovelock#abovelock-allowtoasts)  

### App Runtime

- **Microsoft accounts optional for Microsoft store apps**:  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-appruntime#appruntime-allowmicrosoftaccountstobeoptional)

::: zone-end
::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

### Application Management

- **Block app installations with elevated privileges**:  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-msialwaysinstallwithelevatedprivileges)

- **Block user control over installations**:  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-msiallowusercontroloverinstall)

- **Block game DVR (desktop only)**:  
  Baseline default: *Yes*  
  [Learn more](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowgamedvr)

### Audit

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

### Auto Play

- **Auto play default auto run behavior**:  
  Baseline default: *Do not execute*  
  [Learn more](/windows/client-management/mdm/policy-csp-autoplay#autoplay-setdefaultautorunbehavior)

- **Auto play mode**:  
  Baseline default: *Disabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-autoplay#autoplay-turnoffautoplay)

- **Block auto play for non-volume devices**:  
  Baseline default: *Enabled*  
  [Learn more](/windows/client-management/mdm/policy-csp-autoplay#autoplay-disallowautoplayfornonvolumedevices) 

### BitLocker

- **BitLocker removable drive policy**:  
  Baseline default: *Configure*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067140)

  - **Block write access to removable data-drives not protected by BitLocker**:  
    Baseline default: *Yes*  
    [Learn more](https://go.microsoft.com/fwlink/?linkid=872540)

### Browser

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

### Connectivity

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

### Credentials Delegation

- **Remote host delegation of non-exportable credentials**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067103)

### Credentials UI

- **Enumerate administrators**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067021)

### Data Protection

- **Block direct memory access**:  
  Baseline default: Yes  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067031)

### Device Guard

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

### Device Installation

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
    Baseline default: *No default configuration*

  - **Hardware device identifiers that are blocked**:  
    Baseline default: *No default configuration*

### Device Lock

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

### DMA Guard

- **Enumeration of external devices incompatible with Kernel DMA Protection**:  
  Baseline default: *Block all*

### Event Log Service

- **Application log maximum file size in KB**:  
  Baseline default: *32768*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067125)

- **System log maximum file size in KB**:  
  Baseline default: *32768*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2066798)

- **Security log maximum file size in KB**:  
  Baseline default: *196608*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067042)

### Experience

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

### Exploit Guard

- **Upload XML**:  
  Baseline default: *Sample xml is provided*  
  [Learn more](/windows/client-management/mdm/policy-csp-exploitguard#exploitguard-exploitprotectionsettings)

::: zone-end
::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

### File Explorer

- **Block data execution prevention**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067043)

- **Block heap termination on corruption**:  
  Baseline default: *Disabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067107)

### Firewall

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

### Internet Explorer
<!-- /windows/client-management/mdm/policy-csp-internetexplorer -->

- **Internet Explorer encryption support**:  
  Baseline default: Two items: *TLS v1.1* and *TLS v1.2*  
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
  Baseline default: *Disable java*  
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

### Local Policies Security Options
<!-- /windows/client-management/mdm/policy-csp-localpoliciessecurityoptions -->

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
::: zone pivot="mdm-december-2020,mdm-november-2021"

### Microsoft Defender

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
::: zone pivot="mdm-august-2020,mdm-december-2020,mdm-november-2021"

### MS Security Guide

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

### MSS Legacy

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

### Power

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

### Remote Assistance

- **Remote Assistance solicited**:  
  Baseline default: *Disable Remote Assistance*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067198)

### Remote Desktop Services

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

### Remote Management

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

### Remote Procedure Call

- **RPC unauthenticated client options**:  
  Baseline default: *Authenticated*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067225)

### Search

- **Disable indexing encrypted items**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067303)

### Smart Screen

- **Turn on Windows SmartScreen**  
  Baseline default: *Yes*  
   [Learn more](/windows/client-management/mdm/policy-csp-smartscreen#smartscreen-enablesmartscreeninshell)

- **Block users from ignoring SmartScreen warnings**  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=872783)

### System

- **System boot start driver initialization**:  
  Baseline default: *Good unknown and bad critical*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067307)

### Wi-Fi

- **Block Automatically connecting to Wi-Fi hotspots**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067320)

- **Block Internet sharing**:  
  Baseline default: *Yes*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067327)

### Windows Connection Manager

- **Block connection to non-domain networks**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067323)

### Windows Ink Workspace

- **Ink Workspace**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067241)

### Windows PowerShell

- **PowerShell script block logging**:  
  Baseline default: *Enabled*  
  [Learn more](https://go.microsoft.com/fwlink/?linkid=2067330)

::: zone-end

## Next steps

- [Learn about security baselines](security-baselines.md)
- [Avoid conflicts](security-baselines.md#avoid-conflicts)
- [Troubleshoot policies and profiles in Intune](/troubleshoot/mem/intune/troubleshoot-policies-in-microsoft-intune)
