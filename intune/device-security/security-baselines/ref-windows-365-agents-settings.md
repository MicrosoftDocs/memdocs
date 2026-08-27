---
title: Settings list for the Windows 365 for Agents security baseline in Intune
description: View the settings and default values in the Microsoft Intune Windows 365 for Agents security baseline for Cloud PCs that run agentic workloads.
ms.date: 08/13/2026
ms.topic: reference
ai-usage: ai-assisted
ms.custom: msecd-doc-authoring-1023
#customer intent: As an IT administrator, I want to review the settings and default values in the Windows 365 for Agents security baseline so that I can understand the security configuration before I deploy or customize the baseline.
---

# Windows 365 for Agents security baseline settings reference for Microsoft Intune

This article lists the settings and default values in the Windows 365 for Agents security baseline for Microsoft Intune. IT administrators can use this reference to review Windows 11, Microsoft Edge, and Microsoft Defender for Endpoint configurations. These configurations apply to Cloud PCs that run agentic workloads. Review the settings before you deploy or customize the baseline.

Windows 365 for Agents security baselines are policy templates that you can deploy with Microsoft Intune to configure and enforce recommended security settings. They include versioning features to help you update policies to the latest release, and you can customize them to meet your business needs.

## About this reference article

Each security baseline is a group of preconfigured Windows settings that help you apply and enforce granular security settings that the relevant security teams recommend. You can also customize each baseline you deploy to enforce only the settings and values you require. When you create a security baseline profile in Intune, you're creating a template that consists of multiple device configuration settings.

This article displays:

- A list of each setting with its configuration as found in the default instance of the baseline version.
- When available, a link to the underlying configuration service provider (CSP) documentation or other related content from the relevant product group that provides context and additional details about a setting's use.

When a new version of a baseline becomes available, it replaces the previous version. Profile instances that you created before the availability of a new version:

- Become read-only. You can continue to use those profiles but can't edit them to change their configuration.
- Can be updated to the current version. After you update a profile to the current baseline version, you can edit the profile to modify settings.

To learn more about using security baselines, see:

- [Use security baselines](./overview.md)
- [Change the baseline version for a profile](./configure-baselines.md#update-a-baseline-profile-to-the-latest-version)
- [Manage security baselines](./configure-baselines.md)

## Windows 365 for Agents security baseline version 24H1

The settings in this baseline apply to Cloud PCs that run agentic workloads and are managed through Intune. When available, the setting name links to the source configuration service provider (CSP), followed by the setting's default configuration in the baseline.

### Administrative Templates

#### Control Panel > Personalization

- **Prevent enabling lock screen camera**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-devicelock?WT.mc_id=Portal-fx#preventenablinglockscreencamera)

- **Prevent enabling lock screen slide show**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-devicelock?WT.mc_id=Portal-fx#preventlockscreenslideshow)

#### MS Security Guide

- **Apply UAC restrictions to local accounts on network logons**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-mssecurityguide?WT.mc_id=Portal-fx#applyuacrestrictionstolocalaccountsonnetworklogon)

- **Configure SMB v1 client driver**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-mssecurityguide?WT.mc_id=Portal-fx#configuresmbv1clientdriver)

  - **Configure MrxSmb10 driver**\
    Baseline default: *Disable driver (recommended)*

- **Configure SMB v1 server**\
  Baseline default: *Disabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-mssecurityguide?WT.mc_id=Portal-fx#configuresmbv1server)

- **Enable Structured Exception Handling Overwrite Protection (SEHOP)**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-mssecurityguide?WT.mc_id=Portal-fx#enablestructuredexceptionhandlingoverwriteprotection)

- **WDigest Authentication (disabling may require KB2871997)**\
  Baseline default: *Disabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-mssecurityguide?WT.mc_id=Portal-fx#wdigestauthentication)

#### MSS (Legacy)

- **MSS: (DisableIPSourceRouting IPv6) IP source routing protection level (protects against packet spoofing)**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-msslegacy?WT.mc_id=Portal-fx#ipv6sourceroutingprotectionlevel)

  - **DisableIPSourceRouting IPv6 (Device)**\
    Baseline default: *Highest protection, source routing is completely disabled*

- **MSS: (DisableIPSourceRouting) IP source routing protection level (protects against packet spoofing)**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-msslegacy?WT.mc_id=Portal-fx#ipsourceroutingprotectionlevel)

  - **DisableIPSourceRouting (Device)**\
    Baseline default: *Enabled*  *Highest protection, source routing is completely disabled*

- **MSS: (EnableCMPRedirect) Allow ICMP redirects to override OSPF generated routes**\
  Baseline default: *Disabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-msslegacy?WT.mc_id=Portal-fx#allowicmpredirectstooverrideospfgeneratedroutes)

- **MSS: (NoNameReleaseOnDemand) Allow the computer to ignore NetBIOS name release requests except from WINS servers**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-msslegacy?WT.mc_id=Portal-fx#allowthecomputertoignorenetbiosnamereleaserequestsexceptfromwinsservers)

#### Network > DNS Client

- **Turn off multicast name resolution**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-admx-dnsclient?WT.mc_id=Portal-fx#turn_off_multicast)

#### Network > Network Connections

- **Prohibit use of Internet Connection Sharing on your DNS domain network**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-admx-networkconnections?WT.mc_id=Portal-fx#nc-showsharedaccessui)

#### Network > Network Provider

- **Hardened UNC Paths**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-connectivity?WT.mc_id=Portal-fx#hardeneduncpaths)
  - **Hardened UNC Paths: (Device)**\
    Baseline defaults:

    | Name           | Value|
    |----------------|------|
    | `\\*\SYSVOL`   | RequireMutualAuthentication=1,RequireIntegrity=1 |
    | `\\*\NETLOGON` | RequireMutualAuthentication=1,RequireIntegrity=1 |

#### Network > Windows Connection Manager

- **Prohibit connection to non-domain networks when connected to domain authenticated network**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-windowsconnectionmanager?WT.mc_id=Portal-fx#prohitconnectiontonondomainnetworkswhenconnectedtodomainauthenticatednetwork)

#### System > Credentials Delegation

- **Encryption Oracle Remediation**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-admx-credssp?WT.mc_id=Portal-fx#allowencryptionoracle)
  - **Protection Level: (Device)**\
    Baseline default: *Force Updated Clients*

- **Remote host allows delegation of non-exportable credentials**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-credentialsdelegation?WT.mc_id=Portal-fx#remotehostallowsdelegationofnonexportablecredentials)

#### System > Device Installation > Device Installation Restrictions

- **Prevent installation of devices using drivers that match these device setup classes**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-deviceinstallation?WT.mc_id=Portal-fx#preventinstallationofmatchingdevicesetupclasses)
  - **Prevented Classes**\
    Baseline default: *{d48179be-ec20-11d1-b6b8-00c04fa372a7}*

  - **Also apply to matching devices that are already installed**\
    Baseline default: *True*

#### System > Early Launch Antimalware

- **Boot-Start Driver Initialization Policy**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-system?WT.mc_id=Portal-fx#bootstartdriverinitialization)
  - **Choose the boot-start drivers that can be initialized:**\
    Baseline default: *Good, unknown and bad but critical*

#### System > Group Policy

- **Configure registry policy processing**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-admx-grouppolicy?WT.mc_id=Portal-fx#cse-registry)

  - **Do not apply during periodic background processing (Device)**\
    Baseline default: *False*
  - **Process even if the Group Policy objects have not changed (Device)**\
    Baseline default: *True*

#### System > Internet Communication Management > Internet Communication settings

- **Turn off downloading of print drivers over HTTP**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-connectivity?WT.mc_id=Portal-fx#disabledownloadingofprintdriversoverhttp)

- **Turn off Internet download for Web publishing and online ordering wizards**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-connectivity?WT.mc_id=Portal-fx#disableinternetdownloadforwebpublishingandonlineorderingwizards)

#### System > Remote Assistance

- **Configure Solicited Remote Assistance**\
  Baseline default: *Disabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-remoteassistance?WT.mc_id=Portal-fx#solicitedremoteassistance)

#### System > Remote Procedure Call

- **Restrict Unauthenticated RPC clients**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-remoteprocedurecall?WT.mc_id=Portal-fx#restrictunauthenticatedrpcclients)
  - **RPC Runtime Unauthenticated Client Restriction to Apply:**\
    Baseline default: *Authenticated*

#### Windows Components > App runtime

- **Allow Microsoft accounts to be optional**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-appruntime?WT.mc_id=Portal-fx#allowmicrosoftaccountstobeoptional)

#### Windows Components > AutoPlay Policies

- **Disallow Autoplay for non-volume devices**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-autoplay?WT.mc_id=Portal-fx#disallowautoplayfornonvolumedevices)

- **Set the default behavior for AutoRun**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-autoplay?WT.mc_id=Portal-fx#setdefaultautorunbehavior)
  - **Default AutoRun Behavior**\
    Baseline default: *Do not execute any autorun commands*

- **Turn off Autoplay**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-autoplay?WT.mc_id=Portal-fx#turnoffautoplay)
  - **Turn off Autoplay on:**\
    Baseline default: *All drives*

#### Windows Components > Credential User Interface

- **Enumerate administrator accounts on elevation**\
  Baseline default: *Disabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-credentialsui?WT.mc_id=Portal-fx#enumerateadministrators)

#### Windows Components > Event Log Service > Application

- **Specify the maximum log file size (KB)**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-eventlogservice?WT.mc_id=Portal-fx#specifymaximumfilesizeapplicationlog)
  - **Maximum Log Size (KB)**\
    Baseline default: *32768*

#### Windows Components > Event Log Service > Security

- **Specify the maximum log file size (KB)**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-eventlogservice?WT.mc_id=Portal-fx#specifymaximumfilesizesecuritylog)
  - **Maximum Log Size (KB)**\
    Baseline default: *196608*

#### Windows Components > Event Log Service > System

- **Specify the maximum log file size (KB)**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-eventlogservice?WT.mc_id=Portal-fx#specifymaximumfilesizesystemlog)
  - **Maximum Log Size (KB)**\
    Baseline default: *32768*

#### Windows Components > File Explorer

- **Configure Windows Defender SmartScreen**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-admx-windowsexplorer?WT.mc_id=Portal-fx#enablesmartscreen)
  - **Pick one of the following settings: (Device)**\
    Baseline default: *Warn and prevent bypass*

- **Turn off Data Execution Prevention for Explorer**\
  Baseline default: *Disabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-fileexplorer?WT.mc_id=Portal-fx#turnoffdataexecutionpreventionforexplorer)

- **Turn off heap termination on corruption**\
  Baseline default: *Disabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-fileexplorer?WT.mc_id=Portal-fx#turnoffheapterminationoncorruption)

#### Windows Components > Internet Explorer > Internet Control Panel > Advanced Page

- **Allow software to run or install even if the signature is invalid**\
  Baseline default: *Disabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#allowsoftwarewhensignatureisinvalid)

- **Check for server certificate revocation**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#checkservercertificaterevocation)

- **Check for signatures on downloaded programs**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#checksignaturesondownloadedprograms)

- **Do not allow ActiveX controls to run in Protected Mode when Enhanced Protected Mode is enabled**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#donotallowactivexcontrolsinprotectedmode)

- **Turn off encryption support**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#disableencryptionsupport)
  - **Secure Protocol combinations**\
    Baseline default: *Use TLS 1.1 and TLS 1.2*

- **Turn on 64-bit tab processes when running in Enhanced Protected Mode on 64-bit versions of Windows**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#disableprocessesinenhancedprotectedmode)

- **Turn on Enhanced Protected Mode**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#allowenhancedprotectedmode)

#### Windows Components > Internet Explorer > Internet Control Panel

- **Prevent ignoring certificate errors**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#disableignoringcertificateerrors)

#### Windows Components > Internet Explorer > Internet Control Panel > Security Page > Internet Zone

- **Access data sources across domains**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowaccesstodatasources)
  - **Access data sources across domains**\
    Baseline default: *Disable*

- **Allow cut, copy or paste operations from the clipboard via script**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowcopypasteviascript)
  - **Allow paste operations via script**\
    Baseline default: *Disable*

- **Allow drag and drop or copy and paste files**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowdraganddropcopyandpastefiles)
  - **Allow drag and drop or copy and paste files**\
    Baseline default: *Disable*

- **Allow loading of XAML files**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowloadingofxamlfiles)
  - **XAML Files**\
    Baseline default: *Disable*

- **Allow only approved domains to use ActiveX controls without prompt**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowonlyapproveddomainstouseactivexcontrols)
  - **Only allow approved domains to use ActiveX controls without prompt**\
    Baseline default: *Enable*

- **Allow only approved domains to use the TDC ActiveX control**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowonlyapproveddomainstousetdcactivexcontrol)
  - **Only allow approved domains to use the TDC ActiveX control**\
    Baseline default: *Enable*

- **Allow script-initiated windows without size or position constraints**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowscriptinitiatedwindows)
  - **Allow script-initiated windows without size or position constraints**\
    Baseline default: *Disable*

- **Allow scripting of Internet Explorer WebBrowser controls**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowscriptingofinternetexplorerwebbrowsercontrols)
  - **Internet Explorer web browser control**\
    Baseline default: *Disable*

- **Allow scriptlets**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowscriptlets)
  - **Scriptlets**\
    Baseline default: *Disable*

- **Allow updates to status bar via script**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowupdatestostatusbarviascript)
  - **Status bar updates via script**\
    Baseline default: *Disable*

- **Allow VBScript to run in Internet Explorer**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowvbscripttorunininternetexplorer)
  - **Allow VBScript to run in Internet Explorer**\
    Baseline default: *Disable*

- **Automatic prompting for file downloads**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowautomaticpromptingforfiledownloads)
  - **Automatic prompting for file downloads**\
    Baseline default: *Disable*

- **Don't run antimalware programs against ActiveX controls**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzonedonotrunantimalwareagainstactivexcontrols)
  - **Don't run antimalware programs against ActiveX controls**\
    Baseline default: *Disable*

- **Download signed ActiveX controls**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzonedownloadsignedactivexcontrols)
  - **Download signed ActiveX controls**\
    Baseline default: *Disable*

- **Download unsigned ActiveX controls**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzonedownloadunsignedactivexcontrols)
  - **Download unsigned ActiveX controls**\
    Baseline default: *Disable*

- **Enable dragging of content from different domains across windows**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneenabledraggingofcontentfromdifferentdomainsacrosswindows)
  - **Enable dragging of content from different domains across windows**\
    Baseline default: *Disable*

- **Enable dragging of content from different domains within a window**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneenabledraggingofcontentfromdifferentdomainsacrosswindows)
  - **Enable dragging of content from different domains within a window**\
    Baseline default: *Disable*

- **Include local path when user is uploading files to a server**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneincludelocalpathwhenuploadingfilestoserver)
  - **Include local directory path when uploading files to a server**\
    Baseline default: *Disable*

- **Initialize and script ActiveX controls not marked as safe**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneinitializeandscriptactivexcontrols)
  - **Initialize and script ActiveX controls not marked as safe**\
    Baseline default: *Disable*

- **Java permissions**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzonejavapermissions)
  - **Java permissions**\
    Baseline default: *Disable Java*

- **Launching applications and files in an IFRAME**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzonelaunchingapplicationsandfilesiniframe)
  - **Launching applications and files in an IFRAME**\
    Baseline default: *Disable*

- **Logon options**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzonelogonoptions)
  - **Logon options**\
    Baseline default: *Prompt for user name and password*

- **Navigate windows and frames across different domains**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzonenavigatewindowsandframes)
  - **Navigate windows and frames across different domains**\
    Baseline default: *Disable*

- **Run .NET Framework-reliant components not signed with Authenticode**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallownetframeworkreliantcomponents)
  - **Run .NET Framework-reliant components not signed with Authenticode**\
    Baseline default: *Disable*

- **Run .NET Framework-reliant components signed with Authenticode**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzonerunnetframeworkreliantcomponentssignedwithauthenticode)
  - **Run .NET Framework-reliant components signed with Authenticode**\
    Baseline default: *Disable*

- **Show security warning for potentially unsafe files**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneshowsecuritywarningforpotentiallyunsafefiles)
  - **Launching programs and unsafe files**\
    Baseline default: *Prompt*

- **Turn on Cross-Site Scripting Filter**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneenablecrosssitescriptingfilter)
  - **Turn on Cross-Site Scripting (XSS) Filter**\
    Baseline default: *Enable*

- **Turn on Protected Mode**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneenableprotectedmode)
  - **Protected Mode**\
    Baseline default: *Enable*

- **Turn on SmartScreen Filter scan**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowsmartscreenie)
  - **Use SmartScreen Filter**\
    Baseline default: *Enable*

- **Use Pop-up Blocker**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetexplorer-internetzoneusepopupblocker)
  - **Use Pop-up Blocker**\
    Baseline default: *Enable*

- **Userdata persistence**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowuserdatapersistence)
  - **Userdata persistence**\
    Baseline default: *Disable*

- **Web sites in less privileged Web content zones can navigate into this zone**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#internetzoneallowlessprivilegedsites)
  - **Web sites in less privileged Web content zones can navigate into this zone**\
    Baseline default: *Disable*

#### Windows Components > Internet Explorer > Internet Control Panel > Security Page

- **Intranet Sites: Include all network paths (UNCs)**\
  Baseline default: *Disabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#includeallnetworkpaths)

- **Turn on certificate address mismatch warning**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#allowcertificateaddressmismatchwarning)

#### Windows Components > Internet Explorer > Internet Control Panel > Security Page > Intranet Zone

- **Don't run antimalware programs against ActiveX controls**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#intranetzonedonotrunantimalwareagainstactivexcontrols)
  - **Don't run antimalware programs against ActiveX controls**\
    Baseline default: *Disable*

- **Initialize and script ActiveX controls not marked as safe**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#intranetzoneinitializeandscriptactivexcontrols)
  - **Initialize and script ActiveX controls not marked as safe**\
    Baseline default: *Disable*

- **Java permissions**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#intranetzonejavapermissions)
  - **Java permissions**\
    Baseline default: *High safety*

#### Windows Components > Internet Explorer > Internet Control Panel > Security Page > Local Machine Zone

- **Don't run antimalware programs against ActiveX controls**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#localmachinezonedonotrunantimalwareagainstactivexcontrols)
  - **Don't run antimalware programs against ActiveX controls**\
    Baseline default: *Disable*

- **Java permissions**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#localmachinezonejavapermissions)
  - **Java permissions**\
    Baseline default: *Disable Java*

#### Windows Components > Internet Explorer > Internet Control Panel > Security Page > Locked-Down Internet Zone

- **Turn on SmartScreen Filter scan**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#lockeddowninternetzoneallowsmartscreenie)
  - **Use SmartScreen Filter**\
    Baseline default: *Enable*

#### Windows Components > Internet Explorer > Internet Control Panel > Security Page > Locked-Down Intranet Zone

- **Java permissions**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#lockeddownintranetjavapermissions)
  - **Java permissions**\
    Baseline default: *Disable Java*

#### Windows Components > Internet Explorer > Internet Control Panel > Security Page > Locked-Down Local Machine Zone

- **Java permissions**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#lockeddownlocalmachinezonejavapermissions)
  - **Java permissions**\
    Baseline default: *Disable Java*

#### Windows Components > Internet Explorer > Internet Control Panel > Security Page > Locked-Down Restricted Sites Zone

- **Java permissions**\
  Baseline default: *Enabled*\
    [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#lockeddownrestrictedsiteszonejavapermissions)

  - **Java permissions**\
    Baseline default: *Disable Java*

- **Turn on SmartScreen Filter scan**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#lockeddownrestrictedsiteszoneallowsmartscreenie)
  - **Use SmartScreen Filter**\
      Baseline default: *Enable*

#### Windows Components > Internet Explorer > Internet Control Panel > Security Page > Locked-Down Trusted Sites Zone

- **Java permissions**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#lockeddowntrustedsiteszonejavapermissions)
  - **Java permissions**\
    Baseline default: *Disable Java*

#### Windows Components > Internet Explorer > Internet Control Panel > Security Page > Restricted Sites Zone

- **Access data sources across domains**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowaccesstodatasources)
  - **Access data sources across domains**\
    Baseline default: *Disable*

- **Allow active scripting**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowactivescripting)
  - **Allow active scripting**\
    Baseline default: *Disable*

- **Allow binary and script behaviors**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowbinaryandscriptbehaviors)
  - **Allow binary and script behaviors**\
    Baseline default: *Disable*

- **Allow cut, copy or paste operations from the clipboard via script**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowcopypasteviascript)
  - **Allow paste operations via script**\
    Baseline default: *Disable*

- **Allow drag and drop or copy and paste files**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowdraganddropcopyandpastefiles)
  - **Allow drag and drop or copy and paste files**\
    Baseline default: *Disable*

- **Allow file downloads**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowfiledownloads)
  - **Allow file downloads**\
    Baseline default: *Disable*

- **Allow loading of XAML files**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowloadingofxamlfiles)
  - **XAML Files**\
    Baseline default: *Disable*

- **Allow META REFRESH**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowmetarefresh)
  - **Allow META REFRESH**\
    Baseline default: *Disable*

- **Allow only approved domains to use ActiveX controls without prompt**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowonlyapproveddomainstouseactivexcontrols)
  - **Only allow approved domains to use ActiveX controls without prompt**\
    Baseline default: *Enable*

- **Allow only approved domains to use the TDC ActiveX control**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowonlyapproveddomainstousetdcactivexcontrol)
  - **Only allow approved domains to use the TDC ActiveX control**\
    Baseline default: *Enable*

- **Allow script-initiated windows without size or position constraints**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowscriptinitiatedwindows)
  - **Allow script-initiated windows without size or position constraints**\
    Baseline default: *Disable*

- **Allow scripting of Internet Explorer WebBrowser controls**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowscriptingofinternetexplorerwebbrowsercontrols)
  - **Internet Explorer web browser control**\
    Baseline default: *Disable*

- **Allow scriptlets**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowscriptlets)
  - **Scriptlets**\
    Baseline default: *Disable*

- **Allow updates to status bar via script**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowupdatestostatusbarviascript)
  - **Status bar updates via script**\
    Baseline default: *Disable*

- **Allow VBScript to run in Internet Explorer**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowvbscripttorunininternetexplorer)
  - **Allow VBScript to run in Internet Explorer**\
    Baseline default: *Disable*

- **Automatic prompting for file downloads**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowautomaticpromptingforfiledownloads)
  - **Automatic prompting for file downloads**\
    Baseline default: *Disable*

- **Don't run antimalware programs against ActiveX controls**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszonedonotrunantimalwareagainstactivexcontrols)
  - **Don't run antimalware programs against ActiveX controls**\
    Baseline default: *Disable*

- **Download signed ActiveX controls**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszonedownloadsignedactivexcontrols)
  - **Download signed ActiveX controls**\
    Baseline default: *Disable*

- **Download unsigned ActiveX controls**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszonedownloadunsignedactivexcontrols)
  - **Download unsigned ActiveX controls**\
    Baseline default: *Disable*

- **Enable dragging of content from different domains across windows**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneenabledraggingofcontentfromdifferentdomainsacrosswindows)
  - **Enable dragging of content from different domains across windows**\
    Baseline default: *Disable*

- **Enable dragging of content from different domains within a window**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneenabledraggingofcontentfromdifferentdomainswithinwindows)
  - **Enable dragging of content from different domains within a window**\
    Baseline default: *Disable*

- **Include local path when user is uploading files to a server**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneincludelocalpathwhenuploadingfilestoserver)
  - **Include local directory path when uploading files to a server**\
    Baseline default: *Disable*

- **Initialize and script ActiveX controls not marked as safe**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneinitializeandscriptactivexcontrols)
  - **Initialize and script ActiveX controls not marked as safe**\
    Baseline default: *Disable*

- **Java permissions**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszonejavapermissions)
  - **Java permissions**\
    Baseline default: *Disable Java*

- **Launching applications and files in an IFRAME**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszonelaunchingapplicationsandfilesiniframe)
  - **Launching applications and files in an IFRAME**\
    Baseline default: *Disable*

- **Logon options**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszonelogonoptions)
  - **Logon options**\
    Baseline default: *Anonymous logon*

- **Navigate windows and frames across different domains**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszonenavigatewindowsandframes)
  - **Navigate windows and frames across different domains**\
    Baseline default: *Disable*

- **Run .NET Framework-reliant components not signed with Authenticode**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallownetframeworkreliantcomponents)
  - **Run .NET Framework-reliant components not signed with Authenticode**\
    Baseline default: *Disable*

- **Run .NET Framework-reliant components signed with Authenticode**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszonerunnetframeworkreliantcomponentssignedwithauthenticode)
  - **Run .NET Framework-reliant components signed with Authenticode**\
    Baseline default: *Disable*

- **Run ActiveX controls and plugins**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszonerunactivexcontrolsandplugins)
  - **Run ActiveX controls and plugins**\
    Baseline default: *Disable*

- **Script ActiveX controls marked safe for scripting**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszonescriptactivexcontrolsmarkedsafeforscripting)

  - **Script ActiveX controls marked safe for scripting**\
    Baseline default: *Disable*

- **Scripting of Java applets**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszonescriptingofjavaapplets)
  - **Scripting of Java applets**\
    Baseline default: *Disable*

- **Show security warning for potentially unsafe files**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneshowsecuritywarningforpotentiallyunsafefiles)

  - **Launching programs and unsafe files**\
    Baseline default: *Disable*

- **Turn on Cross-Site Scripting Filter**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneenablecrosssitescriptingfilter)
  - **Turn on Cross-Site Scripting (XSS) Filter**\
    Baseline default: *Enabled*

- **Turn on Protected Mode**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneturnonprotectedmode)
  - **Protected Mode**\
    Baseline default: *Enabled*

- **Turn on SmartScreen Filter scan**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowsmartscreenie)
  - **Use SmartScreen Filter**\
    Baseline default: *Enabled*

- **Use Pop-up Blocker**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneusepopupblocker)
  - **Use Pop-up Blocker**\
    Baseline default: *Enabled*

- **Userdata persistence**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowuserdatapersistence)

  - **Userdata persistence**\
    Baseline default: *Disable*

- **Web sites in less privileged Web content zones can navigate into this zone**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictedsiteszoneallowlessprivilegedsites)
  - **Web sites in less privileged Web content zones can navigate into this zone**\
    Baseline default: *Disable*

#### Windows Components > Internet Explorer > Internet Control Panel > Security Page > Trusted Sites Zone

- **Don't run antimalware programs against ActiveX controls**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#trustedsiteszonedonotrunantimalwareagainstactivexcontrols)
  - **Don't run antimalware programs against ActiveX controls**\
    Baseline default: *Disable*

- **Initialize and script ActiveX controls not marked as safe**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#trustedsiteszoneinitializeandscriptactivexcontrols)
  - **Initialize and script ActiveX controls not marked as safe**\
    Baseline default: *Disable*

- **Java permissions**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#trustedsiteszonejavapermissions)
  - **Java permissions**\
    Baseline default: *High safety*

#### Windows Components > Internet Explorer

- **Prevent bypassing SmartScreen Filter warnings**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#disablebypassofsmartscreenwarnings)

- **Prevent bypassing SmartScreen Filter warnings about files that are not commonly downloaded from the Internet**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#disablebypassofsmartscreenwarningsaboutuncommonfiles)

- **Prevent managing SmartScreen Filter**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#preventmanagingsmartscreenfilter)
  - **Select SmartScreen Filter mode**\
    Baseline default: *On*

- **Prevent per-user installation of ActiveX controls**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#preventperuserinstallationofactivexcontrols)

- **Security Zones: Do not allow users to add/delete sites**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#donotallowuserstoaddsites)

- **Security Zones: Do not allow users to change policies**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#donotallowuserstochangepolicies)

- **Security Zones: Use only machine settings**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#securityzonesuseonlymachinesettings)

- **Specify use of ActiveX Installer Service for installation of ActiveX controls**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#specifyuseofactivexinstallerservice)

- **Turn off Crash Detection**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#disablecrashdetection)

- **Turn off the Security Settings Check feature**\
  Baseline default: *Disabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#disablesecuritysettingscheck)

#### Windows Components > Internet Explorer > Security Features > Add-on Management

- **Remove "Run this time" button for outdated ActiveX controls in Internet Explorer**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#removerunthistimebuttonforoutdatedactivexcontrols)

- **Turn off blocking of outdated ActiveX controls for Internet Explorer**\
  Baseline default: *Disabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#donotblockoutdatedactivexcontrols)

#### Windows Components > Internet Explorer > Security Features

- **Allow fallback to SSL 3.0 (Internet Explorer)**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#allowfallbacktossl3)
  - **Allow insecure fallback for:**\
    Baseline default: *No Sites*

#### Windows Components > Internet Explorer > Security Features > Consistent Mime Handling

- **Internet Explorer Processes**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#consistentmimehandlinginternetexplorerprocesses)

#### Windows Components > Internet Explorer > Security Features > Mime Sniffing Safety Feature

- **Internet Explorer Processes**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#mimesniffingsafetyfeatureinternetexplorerprocesses)

#### Windows Components > Internet Explorer > Security Features > MK Protocol Security Restriction

- **Internet Explorer Processes**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#mkprotocolsecurityrestrictioninternetexplorerprocesses)

#### Windows Components > Internet Explorer > Security Features > Notification bar

- **Internet Explorer Processes**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#notificationbarinternetexplorerprocesses)

#### Windows Components > Internet Explorer > Security Features > Protection From Zone Elevation

- **Internet Explorer Processes**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#protectionfromzoneelevationinternetexplorerprocesses)

#### Windows Components > Internet Explorer > Security Features > Restrict ActiveX Install

- **Internet Explorer Processes**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictactivexinstallinternetexplorerprocesses)

#### Windows Components > Internet Explorer > Security Features > Restrict File Download

- **Internet Explorer Processes**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#restrictfiledownloadinternetexplorerprocesses)

#### Windows Components > Internet Explorer > Security Features > Scripted Window Security Restrictions

- **Internet Explorer Processes**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#scriptedwindowsecurityrestrictionsinternetexplorerprocesses)

#### Windows Components > Microsoft Defender Antivirus > MAPS

- **Configure the 'Block at First Sight' feature**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-admx-microsoftdefenderantivirus?WT.mc_id=Portal-fx#disableblockatfirstseen)

#### Windows Components > Microsoft Defender Antivirus > Real-time Protection

- **Turn on process scanning whenever real-time protection is enabled**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-admx-microsoftdefenderantivirus?WT.mc_id=Portal-fx#realtimeprotection-disablescanonrealtimeenable)

#### Windows Components > Microsoft Defender Antivirus > Scan

- **Scan packed executables**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-admx-microsoftdefenderantivirus?WT.mc_id=Portal-fx#scan-disablepackedexescanning)

#### Windows Components > Microsoft Defender Antivirus

- **Turn off routine remediation**\
  Baseline default: *Disabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-admx-microsoftdefenderantivirus?WT.mc_id=Portal-fx#disableroutinelytakingaction)

#### Windows Components > Remote Desktop Services > Remote Desktop Connection Client

- **Do not allow passwords to be saved**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-remotedesktopservices?WT.mc_id=Portal-fx#donotallowpasswordsaving)

#### Windows Components > Remote Desktop Services > Remote Desktop Session Host > Device and Resource Redirection

- **Do not allow drive redirection**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-remotedesktopservices?WT.mc_id=Portal-fx#donotallowdriveredirection)

#### Windows Components > Remote Desktop Services > Remote Desktop Session Host > Security

- **Always prompt for password upon connection**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-remotedesktopservices?WT.mc_id=Portal-fx#promptforpassworduponconnection)

- **Require secure RPC communication**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-remotedesktopservices?WT.mc_id=Portal-fx#requiresecurerpccommunication)

- **Set client connection encryption level**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-remotedesktopservices?WT.mc_id=Portal-fx#clientconnectionencryptionlevel)
  - **Encryption Level**\
    Baseline default: *High Level*

#### Windows Components > RSS Feeds

- **Prevent downloading of enclosures**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-internetexplorer?WT.mc_id=Portal-fx#disableenclosuredownloading)

#### Windows Components > Windows Logon Options

- **Sign-in and lock last interactive user automatically after a restart**\
  Baseline default: *Disabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-windowslogon?WT.mc_id=Portal-fx#allowautomaticrestartsignon)

#### Windows Components > Windows PowerShell

- **Turn on PowerShell Script Block Logging**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-windowspowershell?WT.mc_id=Portal-fx#turnonpowershellscriptblocklogging)
  - **Log script block invocation start / stop events:**\
    Baseline default: *False*

#### Windows Components > Windows Remote Management (WinRM) > WinRM Client

- **Allow Basic authentication**\
  Baseline default: *Disabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-remotemanagement?WT.mc_id=Portal-fx#allowbasicauthentication-service)

- **Allow unencrypted traffic**\
  Baseline default: *Disabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-remotemanagement?WT.mc_id=Portal-fx#allowunencryptedtraffic-client)

- **Disallow Digest authentication**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-remotemanagement?WT.mc_id=Portal-fx#disallowdigestauthentication)

#### Windows Components > Windows Remote Management (WinRM) > WinRM Service

- **Allow Basic authentication**\
  Baseline default: *Disabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-remotemanagement?WT.mc_id=Portal-fx#allowbasicauthentication-service)

- **Allow unencrypted traffic**\
  Baseline default: *Disabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-remotemanagement?WT.mc_id=Portal-fx#allowunencryptedtraffic-service)

- **Disallow WinRM from storing RunAs credentials**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-remotemanagement?WT.mc_id=Portal-fx#disallowstoringofrunascredentials)

### Auditing

- **Account Logon Audit Credential Validation**\
  Baseline default: *Success+ Failure*\
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#accountlogon_auditcredentialvalidation)

- **Account Logon Logoff Audit Account Lockout**\
  Baseline default: *Failure*\
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#accountlogonlogoff_auditaccountlockout)

- **Account Logon Logoff Audit Group Membership**\
  Baseline default: *Success*\
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#accountlogonlogoff_auditgroupmembership)

- **Account Logon Logoff Audit Logon**\
  Baseline default: *Success+ Failure*\
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#accountlogonlogoff_auditlogon)

- **Audit Authentication Policy Change**\
  Baseline default: *Success*\
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#policychange_auditauthenticationpolicychange)

- **Audit Changes to Audit Policy**\
  Baseline default: *Success*\
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#policychange_auditpolicychange)

- **Audit File Share Access**\
  Baseline default: *Success+ Failure*\
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#objectaccess_auditfileshare)

- **Audit Other Logon Logoff Events**\
  Baseline default: *Success+ Failure*\
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#accountlogonlogoff_auditotherlogonlogoffevents)

- **Audit Security Group Management**\
  Baseline default: *Success*\
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#accountmanagement_auditsecuritygroupmanagement)

- **Audit Security System Extension**\
  Baseline default: *Success*\
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#system_auditsecuritysystemextension)

- **Audit Special Logon**\
  Baseline default: *Success*\
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#accountlogonlogoff_auditspeciallogon)

- **Audit User Account Management**\
  Baseline default: *Success+ Failure*\
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#accountmanagement_audituseraccountmanagement)

- **Detailed Tracking Audit PNP Activity**\
  Baseline default: *Success*\
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#detailedtracking_auditpnpactivity)

- **Detailed Tracking Audit Process Creation**\
  Baseline default: *Success*\
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#detailedtracking_auditprocesscreation)

- **Object Access Audit Detailed File Share**\
  Baseline default: *Failure*\
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#objectaccess_auditdetailedfileshare)

- **Object Access Audit Other Object Access Events**\
  Baseline default: *Success+ Failure*\
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#objectaccess_auditotherobjectaccessevents)

- **Object Access Audit Removable Storage**\
  Baseline default: *Success+ Failure*\
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#objectaccess_auditremovablestorage)

- **Policy Change Audit MPSSVC Rule Level Policy Change**\
  Baseline default: *Success+ Failure*\
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#policychange_auditmpssvcrulelevelpolicychange)

- **Policy Change Audit Other Policy Change Events**\
  Baseline default: *Failure*\
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#policychange_auditotherpolicychangeevents)

- **Privilege Use Audit Sensitive Privilege Use**\
  Baseline default: *Success*\
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#privilegeuse_auditsensitiveprivilegeuse)

- **System Audit Other System Events**\
  Baseline default: *Success+ Failure*\
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#system_auditothersystemevents)

- **System Audit Security State Change**\
  Baseline default: *Success*\
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#system_auditsecuritystatechange)

- **System Audit System Integrity**\
  Baseline default: *Success+ Failure*\
  [Learn more](/windows/client-management/mdm/policy-csp-Audit?WT.mc_id=Portal-fx#system_auditsystemintegrity)

### Data Protection

- **Allow Direct Memory Access**\
  Baseline default: *Block*\
  [Learn more](/windows/client-management/mdm/policy-csp-dataprotection?WT.mc_id=Portal-fx#allowdirectmemoryaccess)

### Defender

- **Allow Archive Scanning**\
  Baseline default: *Allowed. Scans the archive files.*\
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#allowarchivescanning)

- **Allow Behavior Monitoring**\
  Baseline default: *Allowed. Turns on real-time behavior monitoring.*\
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#allowbehaviormonitoring)

- **Allow Cloud Protection**\
  Baseline default: *Allowed. Turns on Cloud Protection.*\
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#allowcloudprotection)

- **Allow Full Scan Removable Drive Scanning**\
  Baseline default: *Allowed. Scans removable drives.*\
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#allowfullscanremovabledrivescanning)

- **Allow On Access Protection**\
  Baseline default: *Allowed.*\
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#allowonaccessprotection)

- **Allow Realtime Monitoring**\
  Baseline default: *Allowed. Turns on and runs the real-time monitoring service.*\
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#allowrealtimemonitoring)

- **Allow scanning of all downloaded files and attachments**\
  Baseline default: *Allowed.*\
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#allowioavprotection)

- **Allow Script Scanning**\
  Baseline default: *Allowed.*\
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#allowscriptscanning)

  - **Block execution of potentially obfuscated scripts**\
    Baseline default: *Block*\
    [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)

  - **Block Win32 API calls from Office macros**\
    Baseline default: *Block*\
    [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)

  - **Block Office communication application from creating child processes**\
    Baseline default: *Block*\
    [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)

  - **Block all Office applications from creating child processes**\
    Baseline default: *Block*\
    [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)

  - **Block Adobe Reader from creating child processes**\
    Baseline default: *Block*\
    [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)

  - **Block credential stealing from the Windows local security authority subsystem**\
    Baseline default: *Block*\
    [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)

  - **Block JavaScript or VBScript from launching downloaded executable content**\
    Baseline default: *Block*\
    [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)

  - **Block untrusted and unsigned processes that run from USB**\
    Baseline default: *Block*\
    [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)

  - **Block Office applications from creating executable content**\
    Baseline default: *Block*\
    [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)

  - **Block Office applications from injecting code into other processes**\
    Baseline default: *Block*\
    [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)

  - **Block executable content from email client and webmail**\
    Baseline default: *Block*\
    [Learn more](/windows/security/threat-protection/microsoft-defender-atp/attack-surface-reduction?WT.mc_id=Portal-fx)

- **Cloud Block Level**\
  Baseline default: *High*\
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#cloudblocklevel)

- **Cloud Extended Timeout**\
  Baseline default: *Configured*\
  Value: *50*\
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#cloudextendedtimeout)

- **Disable Local Admin Merge**\
  Baseline default: *Disable Local Admin Merge*\
  [Learn more](/windows/client-management/mdm/Defender-csp?WT.mc_id=Portal-fx#configurationdisablelocaladminmerge)

- **Enable File Hash Computation**\
  Baseline default: *Enable*\
  [Learn more](/windows/client-management/mdm/Defender-csp?WT.mc_id=Portal-fx#configurationenablefilehashcomputation)

- **Enable Network Protection**\
  Baseline default: *Enabled (block mode)*\
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#enablenetworkprotection)

- **Hide Exclusions From Local Admins**\
  Baseline default: *If you enable this setting, local admins will no longer be able to see the exclusion list in Windows Security App or via PowerShell.*\
  [Learn more](/windows/client-management/mdm/Defender-csp?WT.mc_id=Portal-fx#configurationhideexclusionsfromlocaladmins)

- **PUA Protection**\
  Baseline default: *PUA Protection on. Detected items are blocked. They will show in history along with other threats.*\
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#puaprotection)

- **Real Time Scan Direction**\
  Baseline default: *Monitor all files (bi-directional).*\
  [Learn more](/windows/client-management/mdm/policy-csp-Defender?WT.mc_id=Portal-fx##realtimescandirection)

- **Submit Samples Consent**\
  Baseline default: *Send all samples automatically.*\
  [Learn more](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-fx#submitsamplesconsent)

### Device Guard

- **Configure System Guard Launch**\
  Baseline default: *Unmanaged Enables Secure Launch if supported by hardware*\
  [Learn more](/windows/client-management/mdm/policy-csp-deviceguard?WT.mc_id=Portal-fx#configuresystemguardlaunch)

- **Credential Guard**\
  Baseline default: *(Enabled with UEFI lock) Turns on Credential Guard with UEFI lock.*\
  [Learn more](/windows/client-management/mdm/policy-csp-deviceguard?WT.mc_id=Portal-fx#lsacfgflags)

- **Enable Virtualization Based Security**\
  Baseline default: *Enable virtualization based security.*\
  [Learn more](/windows/client-management/mdm/policy-csp-deviceguard?WT.mc_id=Portal-fx#enablevirtualizationbasedsecurity)

- **Require Platform Security Features**\
  Baseline default: *Turns on VBS with Secure Boot.*\
  [Learn more](/windows/client-management/mdm/policy-csp-deviceguard?WT.mc_id=Portal-fx#requireplatformsecurityfeatures)

### Device Lock

- **Device Password Enabled**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-devicelock?WT.mc_id=Portal-fx#devicepasswordenabled)

  - **Device Password History**\
    Baseline default: *Configured*\
    Value: *24*\
    [Learn more](/windows/client-management/mdm/policy-csp-devicelock?WT.mc_id=Portal-fx#devicepasswordhistory)

  - **Min Device Password Length**\
    Baseline default: *Configured*\
    Value: *14*\
    [Learn more](/windows/client-management/mdm/policy-csp-devicelock?WT.mc_id=Portal-fx#mindevicepasswordlength)

### Dma Guard

- **Device Enumeration Policy**\
  Baseline default: *Block all (Most restrictive)*\
  [Learn more](/windows/client-management/mdm/policy-csp-dmaguard?WT.mc_id=Portal-fx#deviceenumerationpolicy)

### Firewall

- **Enable Domain Network Firewall**\
  Baseline default: *True*\
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoredomainprofileenablefirewall)

  - **Enable Log Dropped Packets**\
    Baseline default: *Enable Logging Of Dropped Packets*\
    [Learn more](/windows/client-management/mdm/Firewall-csp?WT.mc_id=Portal-fx#mdmstoredomainprofileenablelogdroppedpackets)

  - **Default Outbound Action**\
    Baseline default: *Allow*\
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoredomainprofiledefaultoutboundaction)

  - **Disable Inbound Notifications**\
    Baseline default: *True*\
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoredomainprofiledisableinboundnotifications)

  - **Log Max File Size**\
    Baseline default: *Configured*\
    Value: *16384*\
    [Learn more](/windows/client-management/mdm/Firewall-csp?WT.mc_id=Portal-fx#mdmstoredomainprofilelogmaxfilesize)

  - **Default Inbound Action for Domain Profile**\
    Baseline default: *Block*\
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoredomainprofiledefaultinboundaction)

  - **Enable Log Success Connections**\
    Baseline default: *Enable Logging Of Successful Connections*\
    [Learn more](/windows/client-management/mdm/Firewall-csp?WT.mc_id=Portal-fx#mdmstoredomainprofileenablelogsuccessconnections)

- **Enable Private Network Firewall**\
  Baseline default: *True*\
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreprivateprofileenablefirewall)

  - **Log Max File Size**\
    Baseline default: *Configured*\
    Value: *16384*\
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreprivateprofilelogmaxfilesize)

  - **Default Inbound Action for Private Profile**\
    Baseline default: *Block*\
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreprivateprofiledefaultinboundaction)

  - **Enable Log Success Connections**\
    Baseline default: *Enable Logging Of Successful Connections*\
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreprivateprofileenablelogsuccessconnections)

  - **Enable Log Dropped Packets**\
    Baseline default: *Enable Logging Of Dropped Packets*\
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreprivateprofileenablelogdroppedpackets)

  - **Disable Inbound Notifications**\
    Baseline default: *True*\
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreprivateprofiledisableinboundnotifications)

  - **Default Outbound Action**\
    Baseline default: *Allow*\
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstoreprivateprofiledefaultoutboundaction)

- **Enable Public Network Firewall**\
  Baseline default: *True*\
  [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofileenablefirewall)

  - **Enable Log Dropped Packets**\
    Baseline default: *Enable Logging Of Dropped Packets*\
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofileenablelogdroppedpackets)

  - **Log Max File Size**\
    Baseline default: *Configured*\
    Value: *16384*\
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofilelogmaxfilesize)

  - **Default Outbound Action**\
    Baseline default: *Allow*\
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofiledefaultoutboundaction)

  - **Disable Inbound Notifications**\
    Baseline default: *True*\
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofiledisableinboundnotifications)

  - **Allow Local Policy Merge**\
    Baseline default: *False*\
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofileallowlocalpolicymerge)

  - **Default Inbound Action for Public Profile**\
    Baseline default: *Block*\
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofiledefaultinboundaction)

  - **Enable Log Success Connections**\
    Baseline default: *Enable Logging Of Successful Connections*\
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofileenablelogsuccessconnections)

  - **Allow Local Ipsec Policy Merge**\
    Baseline default: *False*\
    [Learn more](/windows/client-management/mdm/firewall-csp?WT.mc_id=Portal-fx#mdmstorepublicprofileallowlocalipsecpolicymerge)

### Lanman Workstation

- **Enable Insecure Guest Logons**\
  Baseline default: *Disabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-LanmanWorkstation?WT.mc_id=Portal-fx#enableinsecureguestlogons)

### Local Security Authority

- **Configure Lsa Protected Process**\
  Baseline default: *Enabled with UEFI lock. LSA will run as protected process and this configuration is UEFI locked.*\
  [Learn more](/windows/client-management/mdm/policy-csp-lsa#configurelsaprotectedprocess)

### Microsoft App Store

- **Allow Game DVR**\
  Baseline default: *Block*\
  [Learn more](/windows/client-management/mdm/policy-csp-ApplicationManagement?WT.mc_id=Portal-fx#allowgamedvr)

- **MSI Allow User Control Over Install**\
  Baseline default: *Disabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-ApplicationManagement?WT.mc_id=Portal-fx#msiallowusercontroloverinstall)

- **MSI Always Install With Elevated Privileges**\
  Baseline default: *Disabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-ApplicationManagement?WT.mc_id=Portal-fx#msialwaysinstallwithelevatedprivileges)

### Microsoft Edge

#### Content settings

- **Default Adobe Flash setting**\
  Baseline default: *Disabled*

- **Minimum TLS version enabled**\
  Baseline default: *Enabled*

  - **Minimum TLS version enabled (Device)**\
    Baseline default: *TlS 1.2*

#### SmartScreen settings

- **Configure Microsoft Defender SmartScreen**\
  Baseline default: *Enabled*

- **Prevent bypassing Microsoft Defender SmartScreen prompts for sites**\
  Baseline default: *Enabled*

### Privacy

- **Let Apps Activate With Voice Above Lock**\
  Baseline default: *Force deny. Windows apps cannot be activated by voice while the screen is locked, and users cannot change it.*\
  [Learn more](/windows/client-management/mdm/policy-csp-Privacy?WT.mc_id=Portal-fx#letappsactivatewithvoiceabovelock)

### Search

- **Allow Indexing Encrypted Stores Or Items**\
  Baseline default: *Block*\
  [Learn more](/windows/client-management/mdm/policy-csp-Search?WT.mc_id=Portal-fx#allowindexingencryptedstoresoritems)

### Smart Screen

- **Enable Smart Screen In Shell**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-smartscreen?WT.mc_id=Portal-fx#enablesmartscreeninshell)

- **Prevent Override For Files In Shell**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-smartscreen?WT.mc_id=Portal-fx#preventoverrideforfilesinshell)

#### Enhanced Phishing Protection

- **Notify Malicious**\
  Baseline default: *Enabled*

- **Notify Password Reuse**\
  Baseline default: *Enabled*

- **Notify Unsafe App**\
  Baseline default: *Enabled*

- **Service Enabled**\
  Baseline default: *Enabled*

### User Rights

- **Access From Network**\
  Baseline default: *Configured*\
  Values:
  - `*S-1-5-32-544`
  - `*S-1-5-32-555`
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#accessfromnetwork)

- **Allow Local Log On**\
  Baseline default: *Configured*\
  Values:
  - `*S-1-5-32-544`
  - `*S-1-5-32-545`
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#allowlocallogon)

- **Backup Files And Directories**\
  Baseline default: *Configured*\
  Value:
  - `*S-1-5-32-544`
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#backupfilesanddirectories)

- **Create Global Objects**\
  Baseline default: *Configured*\
   Values:
  - `*S-1-5-32-544`
  - `*S-1-5-19`
  - `*S-1-5-20`
  - `*S-1-5-6`
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#createglobalobjects)

- **Create Page File**\
  Baseline default: *Configured*\
  Value:
  - `*S-1-5-32-544`
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#createpagefile)

- **Debug Programs**\
  Baseline default: *Configured*\
  Value:
  - `*S-1-5-32-544`
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#debugprograms)

- **Deny Access From Network**\
  Baseline default: *Configured*\
  Value:
  - `*S-1-5-113`
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#denyaccessfromnetwork)

- **Deny Remote Desktop Services Log On**\
  Baseline default: *Configured*\
  Value:
  - `*S-1-5-113`
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#denyremotedesktopserviceslogon)

- **Impersonate Client**\
  Baseline default: *Configured*\
  Values:
  - `*S-1-5-32-544`
  - `*S-1-5-6`
  - `*S-1-5-19`
  - `*S-1-5-20`
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#impersonateclient)

- **Load Unload Device Drivers**\
  Baseline default: *Configured*\
  Value:
  - `*S-1-5-32-544`
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#loadunloaddevicedrivers)

- **Manage Auditing And Security Log**\
  Baseline default: *Configured*\
  Value:
  - `*S-1-5-32-544`
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#manageauditingandsecuritylog)

- **Manage Volume**\
  Baseline default: *Configured*\
  Value:
  - `*S-1-5-32-544`
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#managevolume)

- **Modify Firmware Environment**\
  Baseline default: *Configured*\
  Value:
  - `*S-1-5-32-544`
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#modifyfirmwareenvironment)

- **Profile Single Process**\
  Baseline default: *Configured*\
  Value:
  - `*S-1-5-32-544`
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#profilesingleprocess)

- **Remote Shutdown**\
  Baseline default: *Configured*\
  Value:
  - `*S-1-5-32-544`
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#remoteshutdown)

- **Restore Files And Directories**\
  Baseline default: *Configured*\
  Value:
  - `*S-1-5-32-544`
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#restorefilesanddirectories)

- **Take Ownership**\
  Baseline default: *Configured*\
  Value:
  - `*S-1-5-32-544`
  [Learn more](/windows/client-management/mdm/policy-csp-UserRights?WT.mc_id=Portal-fx#takeownership)

### Virtualization Based Technology

- **Hypervisor Enforced Code Integrity**\
  Baseline default: *(Enabled with UEFI lock) Turns on Hypervisor-Protected Code Integrity with UEFI lock.*\
  [Learn more](/windows/client-management/mdm/policy-csp-VirtualizationBasedTechnology?WT.mc_id=Portal-fx#hypervisorenforcedcodeintegrity)

### Windows Ink Workspace

- **Allow Windows Ink Workspace**\
  Baseline default: *Ink workspace is enabled (feature is turned on), but the user cannot access it above the lock screen.*\
  [Learn more](/windows/client-management/mdm/policy-csp-WindowsInkWorkspace?WT.mc_id=Portal-fx#allowwindowsinkworkspace)

### Local Policies Security Options

- **Accounts Limit Local Account Use Of Blank Passwords To Console Logon Only**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#accounts_limitlocalaccountuseofblankpasswordstoconsolelogononly)

- **Interactive Logon Machine Inactivity Limit**\
  Baseline default: *Configured*\
  Value: *900*\
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#interactivelogon_machineinactivitylimit)

- **Interactive Logon Smart Card Removal Behavior**\
  Baseline default: *Lock Workstation*\
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#interactivelogon_smartcardremovalbehavior)

- **Microsoft Network Client Digitally Sign Communications Always**\
  Baseline default: *Enable*\
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#microsoftnetworkclient_digitallysigncommunicationsalways)

- **Microsoft Network Client Send Unencrypted Password To Third Party SMB Servers**\
  Baseline default: *Disable*\
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#microsoftnetworkclient_sendunencryptedpasswordtothirdpartysmbservers)

- **Microsoft Network Server Digitally Sign Communications Always**\
  Baseline default: *Enable*\
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#microsoftnetworkserver_digitallysigncommunicationsalways)

- **Network Access Do Not Allow Anonymous Enumeration Of SAM Accounts**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#networkaccess_donotallowanonymousenumerationofsamaccounts)

- **Network Access Do Not Allow Anonymous Enumeration Of Sam Accounts And Shares**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#networkaccess_donotallowanonymousenumerationofsamaccountsandshares)

- **Network Access Restrict Anonymous Access To Named Pipes And Shares**\
  Baseline default *Enable*\
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#networkaccess-restrictanonymousaccesstonamedpipesandshares)

- **Network Access Restrict Clients Allowed To Make Remote Calls To SAM**\
  Baseline default: *Configured*\
  Value: *O:BAG:BAD:(A;;RC;;;BA)*\
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#networkaccess_restrictclientsallowedtomakeremotecallstosam)

- **Network Security Do Not Store LAN Manager Hash Value On Next Password Change**\
  Baseline default: *Enable*\
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#networksecurity_donotstorelanmanagerhashvalueonnextpasswordchange)

- **Network Security LAN Manager Authentication Level**\
  Baseline default: *Send LM and NTLMv2 responses only. Refuse LM and NTLM*\
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#networksecurity_lanmanagerauthenticationlevel)

- **Network Security Minimum Session Security For NTLMSSP Based Clients**\
  Baseline default: *Require NTLM and 128-bit encryption*\
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#networksecurity_minimumsessionsecurityforntlmsspbasedclients)

- **Network Security Minimum Session Security For NTLMSSP Based Servers**\
  Baseline default: *Require NTLM and 128-bit encryption*\
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#networksecurity_minimumsessionsecurityforntlmsspbasedservers)

- **User Account Control Behavior Of The Elevation Prompt For Administrators**\
  Baseline default: *Prompt for consent on the secure desktop*\
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#useraccountcontrol_behavioroftheelevationpromptforadministrators)

- **User Account Control Behavior Of The Elevation Prompt For Standard Users**\
  Baseline default: *Automatically deny elevation requests*\
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#useraccountcontrol_behavioroftheelevationpromptforstandardusers)

- **User Account Control Detect Application Installations And Prompt For Elevation**\
  Baseline default: *Enable*\
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#useraccountcontrol-detectapplicationinstallationsandpromptforelevation)

- **User Account Control Only Elevate UI Access Applications That Are Installed In Secure Locations**\
  Baseline default: *Enabled: Application runs with UIAccess integrity only if it resides in secure location.*\
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#useraccountcontrol-onlyelevateuiaccessapplicationsthatareinstalledinsecurelocations)

- **User Account Control Run All Administrators In Admin Approval Mode**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#useraccountcontrol_runalladministratorsinadminapprovalmode)

- **User Account Control Use Admin Approval Mode**\
  Baseline default: *Enable*\
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#useraccountcontrol_useadminapprovalmode)

- **User Account Control Virtualize File And Registry Write Failures To Per User Locations**\
  Baseline default: *Enabled*\
  [Learn more](/windows/client-management/mdm/policy-csp-LocalPoliciesSecurityOptions?WT.mc_id=Portal-fx#useraccountcontrol_virtualizefileandregistrywritefailurestoperuserlocations)
