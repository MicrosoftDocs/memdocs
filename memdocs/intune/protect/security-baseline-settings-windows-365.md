---
# required metadata

title: Settings list for the Windows 365 Cloud PC security baseline in Intune
titleSuffix: Microsoft Intune
description: View a list of the settings in the Microsoft Intune security baseline for Windows 365 Cloud PC. This list includes the default values for settings as found in the default configuration of the baseline.
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
zone_pivot_groups: windows-365-baseline-versions

# optional metadata

#ROBOTS:
#audience:
ms.reviewer: laarrizz 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Windows 365 Cloud PC security baseline settings for Intune

> [!NOTE]
> This security baseline is in public preview.

View the settings that are part of the Windows 365 Cloud PC security baseline that you can deploy with Microsoft Intune. This article details the settings in the available versions of the baseline and the default values for each setting. The default baseline configuration represents the recommended configuration for applicable devices. Defaults for one baseline might not match defaults from other security baselines, or from other versions of this baseline.

Use this baseline to configure [Windows 365 devices](/windows-365/overview) with a recommended security configuration.

::: zone pivot="win365-2101"

**Windows 365 Cloud PC security baseline version 2101**

::: zone-end
::: zone pivot="win365-2110"

**Windows 365 Cloud PC security baseline version 2110**

::: zone-end
::: zone pivot="win365-2110"

This version of the security baseline replaces previous versions. Profiles that were created prior to the availability of this baseline version:

- Are now read-only. You can continue to use those profiles, but can't edit them to change their configuration.
- Can be updated to the latest version. After you update to the current baseline version, you can edit the profile to modify settings.

To understand what's changed with this version of the baseline from previous versions, use the [Compare baselines](../protect/security-baselines.md#compare-baseline-versions) action. This action is available when you view the *Versions* pane for this baseline. Be sure to select the version of the baseline that you want to view.

To update a security baseline profile to the latest version of that baseline, see [Change the baseline version for a profile](../protect/security-baselines-configure.md#change-the-baseline-version-for-a-profile).

::: zone-end
::: zone pivot="win365-2110,win365-2101"

This article is a reference for the settings contained in this baseline. For each setting in this article, the default value identifies the Windows 365 Cloud PC team's recommended configuration for that setting as the setting is represented in the baseline. These defaults aren't meant to identify the default configuration of the underlying CSP. Use the provided links to view content for the setting's *policy configuration service provider* (CSP) or underlying rules like *attack surface reduction rule*. The links in this document are the same as the links available from within the baseline configuration UI in the Microsoft Endpoint Manager admin center.

You can choose to deploy this baseline in its default configuration to apply that recommended security configuration to devices. You  can also create custom instances of the baseline to meet your own security needs.

> [!TIP]  
> Before using or modifying a setting in this baseline, review the he *Information* text in the Microsoft Endpoint Manager admin center for the setting to learn about its conditions or limitations and when applicable, the CSP the setting applied so.

- To learn about using security baselines with Intune and how to upgrade the baseline version in your security baseline profiles, see [Use security baselines](security-baselines.md).
- To update the version of a baseline you've already deployed to devices, see [Change the baseline version for  profile](../protect/security-baselines-configure.md#change-the-baseline-version-for-a-profile).

## Above Lock

- **Voice activate apps from locked screen**:  
  Baseline default: *Disabled*  
  CSP: [Privacy/LetAppsActivateWithVoiceAboveLock](/windows/client-management/mdm/policy-csp-privacy?WT.mc_id=Portal-Microsoft_Intune_Workflows)  

- **Block display of toast notifications**:  
    Baseline default: *Yes*  
    CSP [AboveLock/AllowToasts](/windows/client-management/mdm/policy-csp-abovelock#abovelock-allowtoasts)  

## App Runtime

- **Microsoft accounts optional for Microsoft store apps**:  
  Baseline default: *Enabled*  
  CSP [appruntime-allowmicrosoftaccountstobeoptional](/windows/client-management/mdm/policy-csp-appruntime#appruntime-allowmicrosoftaccountstobeoptional)

## Application management

- **Block app installations with elevated privileges**:  
  Baseline default: *Yes*  
  CSP [ApplicationManagement/MSIAlwaysInstallWithElevatedPrivileges](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-msialwaysinstallwithelevatedprivileges)

- **Block user control over installations**:  
  Baseline default: *Yes*  
  CSP [ApplicationManagement/MSIAllowUserControlOverInstall](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-msiallowusercontroloverinstall)

- **Block game DVR (desktop only)**:  
  Baseline default: *Yes*  
  CSP [ApplicationManagement/AllowGameDVR](/windows/client-management/mdm/policy-csp-applicationmanagement#applicationmanagement-allowgamedvr)

## Attack Surface Reduction Rules

For general information, see [Learn about attack surface reduction rules](/microsoft-365/security/defender-endpoint/attack-surface-reduction?view=o365-worldwide&preserve-view=true).

- **Block Office communication apps from creating child processes**:  
  Baseline default: *Enable*  
  [ASR rule](/microsoft-365/security/defender-endpoint/attack-surface-reduction?view=o365-worldwide&preserve-view=true#block-office-communication-application-from-creating-child-processes)

- **Block Adobe Reader from creating child processes**:  
  Baseline default: *Enable*  
  [ASR rule](/microsoft-365/security/defender-endpoint/attack-surface-reduction?view=o365-worldwide&preserve-view=true#block-adobe-reader-from-creating-child-processes)

- **Block Office applications from injecting code into other processes**:  
    Baseline default: *Block*  
  [ASR rule](/microsoft-365/security/defender-endpoint/attack-surface-reduction?view=o365-&preserve-view=true#block-office-applications-from-injecting-code-into-other-processes)

- **Block Office applications from creating executable content**:  
  Baseline default: *Block*  
  [ASR rule](/microsoft-365/security/defender-endpoint/attack-surface-reduction?view=o365-worldwide&preserve-view=true#block-office-applications-from-creating-executable-content)

- **Block JavaScript or VBScript from launching downloaded executable content**:  
  Baseline default: *Block*  
  [ASR rule](/microsoft-365/security/defender-endpoint/attack-surface-reduction?view=o365-worldwide&preserve-view=true#block-javascript-or-vbscript-from-launching-downloaded-executable-content)

- **Enable network protection**:  
  Baseline default: *Enable*  
  CSP: [Defender/EnableNetworkProtection](/windows/client-management/mdm/policy-csp-defender#defender-enablenetworkprotection)

- **Block untrusted and unsigned processes that run from USB**:  
  Baseline default: *Block*  
  [ASR rule](/microsoft-365/security/defender-endpoint/attack-surface-reduction?view=o365-&preserve-view=true#rule-block-untrusted-and-unsigned-processes-that-run-from-usb)

- **Block credential stealing from the Windows local security authority subsystem (lsass.exe)**:  
  Baseline default: *Enable*  
  [ASR rule](/microsoft-365/security/defender-endpoint/attack-surface-reduction?view=o365-worldwide&preserve-view=true#block-credential-stealing-from-the-windows-local-security-authority-subsystem)

- **Block all Office applications from creating child processes**:  
  Baseline default: *Block*  
  [ASR rule](/microsoft-365/security/defender-endpoint/attack-surface-reduction?view=o365-worldwide&preserve-view=true#block-all-office-applications-from-creating-child-processes)

- **Block execution of potentially obfuscated scripts (js/vbs/ps)**:  
  Baseline default: *Block*  
  [ASR rule](/microsoft-365/security/defender-endpoint/attack-surface-reduction?view=o365-worldwide&preserve-view=true#block-execution-of-potentially-obfuscated-scripts)

- **Block Win32 API calls from Office macro**:  
  Baseline default: *Block*  
  [ASR rule](/microsoft-365/security/defender-endpoint/attack-surface-reduction?view=o365-worldwide&preserve-view=true#block-win32-api-calls-from-office-macros)

- **Block executable content download from email and webmail clients**:  
  Baseline default: *Block*  
  [ASR rule](/microsoft-365/security/defender-endpoint/attack-surface-reduction?view=o365-worldwide&preserve-view=true#block-executable-content-from-email-client-and-webmail)

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
  CSP [Autoplay/SetDefaultAutoRunBehavior](/windows/client-management/mdm/policy-csp-autoplay#autoplay-setdefaultautorunbehavior)

- **Auto play mode**:  
  Baseline default: *Disabled*  
  CSP [Autoplay/TurnOffAutoPlay](/windows/client-management/mdm/policy-csp-autoplay#autoplay-turnoffautoplay)

- **Block auto play for non-volume devices**:  
  Baseline default: *Enabled*  
  CSP [Autoplay/DisallowAutoplayForNonVolumeDevices](/windows/client-management/mdm/policy-csp-autoplay#autoplay-disallowautoplayfornonvolumedevices)

## Browser

- **Block Password Manager**:  
  Baseline default: *Yes*  
  CSP [Browser/AllowPasswordManager](https://go.microsoft.com/fwlink/?linkid=2067128)

- **Require SmartScreen for Microsoft Edge Legacy**:  
  Baseline default: *Yes*  
  CSP [Browser/AllowSmartScreen](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

- **Block malicious site**:  
  Baseline default: *Yes*  
  CSP [Browser/PreventSmartScreenPromptOverride](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

- **Block unverified file download**:  
  Baseline default: *Yes*  
  CSP [Browser/PreventSmartScreenPromptOverrideForFiles](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)

- **Prevent user from overriding certificate errors**:  
  Baseline default: *Yes*  
  CSP [Browser/PreventCertErrorOverrides](/windows/client-management/mdm/policy-csp-browser#browser-preventcerterroroverrides)

## Connectivity

- **Configure secure access to UNC paths**:  
  Baseline default: *Configure Windows to only allow access to the specified UNC paths after fulfilling additional security requirements*  
  CSP [Connectivity/HardenedUNCPaths](/windows/client-management/mdm/policy-csp-connectivity#connectivity-hardeneduncpaths)  

  - **Hardened UNC path list**:  
    *Not configured by default. Manually add one or more hardened UNC paths.*

- **Block downloading of print drivers over HTTP**:  
  Baseline default: *Enabled*  
  CSP [Connectivity/DisableDownloadingOfPrintDriversOverHTTP](/windows/client-management/mdm/policy-csp-connectivity#connectivity-disabledownloadingofprintdriversoverhttp)

- **Block Internet download for web publishing and online ordering wizards**:  
  Baseline default: *Enabled*  
  CSP [Connectivity/DisableInternetDownloadForWebPublishingAndOnlineOrderingWizards](/windows/client-management/mdm/policy-csp-connectivity#connectivity-disableinternetdownloadforwebpublishingandonlineorderingwizards)

## Credentials Delegation

- **Remote host delegation of non-exportable credentials**:  
  Baseline default: *Enabled*  
  CSP [CredentialsDelegation/RemoteHostAllowsDelegationOfNonExportableCredentials](/windows/client-management/mdm/policy-csp-credentialsdelegation#credentialsdelegation-remotehostallowsdelegationofnonexportablecredentials)

## Credentials UI

- **Enumerate administrators**:  
  Baseline default: *Disabled*  
  CSP [CredentialsUI/EnumerateAdministrators](/windows/client-management/mdm/policy-csp-credentialsui#credentialsui-enumerateadministrators)

## Device Guard

- **Virtualization based security**:  
  Baseline default: *Enable VBS with secure boot*  

- **Enable virtualization based security**:  
  Baseline default: *Yes*  
  CSP [DeviceGuard/EnableVirtualizationBasedSecurity](/windows/client-management/mdm/policy-csp-deviceguard#deviceguard-enablevirtualizationbasedsecurity)

- **Launch system guard**:  
  Baseline default: *Enabled*  

- **Turn on Credential Guard**:  
  Baseline default: *Enable with UEFI lock*  
  CSP [DeviceGuard](/windows/client-management/mdm/policy-csp-deviceguard#deviceguard-lsacfgflags)

## Device Installation

- **Block hardware device installation by setup classes**  
  Baseline default: *Yes*  
  CSP [DeviceInstallation/AllowInstallationOfMatchingDeviceSetupClasses](/windows/client-management/mdm/policy-csp-deviceinstallation#deviceinstallation-allowinstallationofmatchingdevicesetupclasses)

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
  CSP [EventLogService/SpecifyMaximumFileSizeApplicationLog](/windows/client-management/mdm/policy-csp-eventlogservice#eventlogservice-specifymaximumfilesizeapplicationlog)

- **System log maximum file size in KB**  
  Baseline default: *32768*  
  CSP [specifymaximumfilesizesystemlog](/windows/client-management/mdm/policy-csp-eventlogservice#eventlogservice-specifymaximumfilesizesystemlog)

- **Security log maximum file size in KB**  
  Baseline default: *196608*  
  CSP [EventLogService/SpecifyMaximumFileSizeSecurityLog](/windows/client-management/mdm/policy-csp-eventlogservice#eventlogservice-specifymaximumfilesizesecuritylog)

## Experience

- **Block Windows Spotlight**  
  Baseline default: *Yes*  
  CSP [Experience/AllowWindowsSpotlight](/windows/client-management/mdm/policy-csp-experience#experience-allowwindowsspotlight)

## File Explorer

- **Block data execution prevention**  
  Baseline default: *Disabled*  
  CSP [FileExplorer/TurnOffDataExecutionPreventionForExplorer](/windows/client-management/mdm/policy-csp-fileexplorer#fileexplorer-turnoffdataexecutionpreventionforexplorer)

- **Block heap termination on corruption**  
  Baseline default: *Disabled*  
  CSP [FileExplorer/TurnOffHeapTerminationOnCorruption](/windows/client-management/mdm/policy-csp-fileexplorer#fileexplorer-turnoffheapterminationoncorruption)

## Firewall

- **Firewall profile domain**  
  Baseline default: *Configure*  
  [2.2.2 FW_PROFILE_TYPE](/openspecs/windows_protocols/ms-fasp/7704e238-174d-4a5e-b809-5f3787dd8acc?redirectedfrom=MSDN)

  - **Inbound connections blocked**  
    Baseline default: *Yes*  
    CSP [Firewall/DefaultInboundAction](/windows/client-management/mdm/firewall-csp#defaultoutboundaction)

  - **Outbound connections required**  
    Baseline default: *Yes*  
    CSP [Firewall/DefaultOutboundAction](/windows/client-management/mdm/firewall-csp#defaultinboundaction)

  - **Inbound notifications blocked**  
    Baseline default: *Yes*  
    CSP [Firewall/DisableInboundNotifications](/windows/client-management/mdm/firewall-csp#disableinboundnotifications)

  - **Firewall enabled**  
    Baseline default: *Allowed*  
    CSP [Firewall/EnableFirewall](/windows/client-management/mdm/firewall-csp#enablefirewall)

- **Firewall profile private**  
  Baseline default: *Configure*  
  [2.2.2 FW_PROFILE_TYPE](/openspecs/windows_protocols/ms-fasp/7704e238-174d-4a5e-b809-5f3787dd8acc?redirectedfrom=MSDN)

  - **Inbound connections blocked**  
    Baseline default: *Yes*  
    CSP [Firewall/DefaultInboundAction](/windows/client-management/mdm/firewall-csp#defaultoutboundaction)

  - **Outbound connections required**  
    Baseline default: *Yes*  
    CSP [Firewall/DefaultOutboundAction](/windows/client-management/mdm/firewall-csp#defaultinboundaction)

  - **Inbound notifications blocked**  
    Baseline default: *Yes*  
    CSP [Firewall/DisableInboundNotifications](/windows/client-management/mdm/firewall-csp#disableinboundnotifications)

  - **Firewall enabled**  
    Baseline default: *Allowed*  
    CSP [Firewall/EnableFirewall](/windows/client-management/mdm/firewall-csp#enablefirewall)

- **Firewall profile public**  
  Baseline default: *Configure*  
  [2.2.2 FW_PROFILE_TYPE](/openspecs/windows_protocols/ms-fasp/7704e238-174d-4a5e-b809-5f3787dd8acc?redirectedfrom=MSDN)

  - **Inbound connections blocked**  
    Baseline default: *Yes*  
    CSP [Firewall/DefaultInboundAction](/windows/client-management/mdm/firewall-csp#defaultoutboundaction)

  - **Outbound connections required**  
    Baseline default: *Yes*  
    CSP [Firewall/DefaultOutboundAction](/windows/client-management/mdm/firewall-csp#defaultinboundaction)

  - **Inbound notifications blocked**  
    Baseline default: *Yes*  
    CSP [Firewall/DisableInboundNotifications](/windows/client-management/mdm/firewall-csp#disableinboundnotifications)

  - **Firewall enabled**  
    Baseline default: *Allowed*  
    CSP [Firewall/EnableFirewall](/windows/client-management/mdm/firewall-csp#enablefirewall)

  - **Connection security rules from group policy not merged**  
    Baseline default: *Yes*  
    CSP [Firewall/AllowLocalIpsecPolicyMerge](/windows/client-management/mdm/firewall-csp#allowlocalipsecpolicymerge)

  - **Policy rules from group policy not merged**  
    Baseline default: *Yes*  
    CSP [Firewall/AllowLocalPolicyMerge](/windows/client-management/mdm/firewall-csp#allowlocalpolicymerge)

## Internet Explorer

- **Internet Explorer encryption support**  
  Baseline defaults:  
  - *TLS v1.1*  
  - *TLS v1.2*  

  CSP [InternetExplorer/DisableEncryptionSupport](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-disableencryptionsupport)

- **Internet Explorer prevent managing smart screen filter**  
  Baseline default: *Enable*  
  CSP [InternetExplorer/PreventManagingSmartScreenFilter](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-preventmanagingsmartscreenfilter)

- **Internet Explorer restricted zone script Active X controls marked safe for scripting**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/RestrictedSitesZoneScriptActiveXControlsMarkedSafeForScripting](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszonescriptactivexcontrolsmarkedsafeforscripting)

- **Internet Explorer restricted zone file downloads**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/RestrictedSitesZoneAllowFileDownloads](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-restrictedsiteszoneallowfiledownloads)

- **Internet Explorer certificate address mismatch warning**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/AllowCertificateAddressMismatchWarning](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-allowcertificateaddressmismatchwarning)

- **Internet Explorer enhanced protected mode**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/AllowEnhancedProtectedMode](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-allowenhancedprotectedmode)

- **Internet Explorer fallback to SSL3**  
  Baseline default: *No sites*  
  CSP [InternetExplorer/AllowFallbackToSSL3](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-allowfallbacktossl3)

- **Internet Explorer software when signature is invalid**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/AllowSoftwareWhenSignatureIsInvalid](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-allowsoftwarewhensignatureisinvalid)

- **Internet Explorer check server certificate revocation**  
  Baseline default: *Enable*  
  CSP [InternetExplorer/CheckServerCertificateRevocation](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-checkservercertificaterevocation)

- **Internet Explorer check signatures on downloaded programs**  
  Baseline default: *Enable*  
  CSP [InternetExplorer/CheckSignaturesOnDownloadedPrograms](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-checksignaturesondownloadedprograms)

- **Internet Explorer processes consistent MIME handling**  
  Baseline default: *Enable*  
  CSP [InternetExplorer/ConsistentMimeHandlingInternetExplorerProcesses](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-consistentmimehandlinginternetexplorerprocesses)

- **Internet Explorer bypass smart screen warnings**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/DisableBypassOfSmartScreenWarnings](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-disablebypassofsmartscreenwarnings)

- **Internet Explorer bypass smart screen warnings about uncommon files**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/DisableBypassOfSmartScreenWarningsAboutUncommonFiles](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-disablebypassofsmartscreenwarningsaboutuncommonfiles)

- **Internet Explorer crash detection**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/DisableCrashDetection](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-disablecrashdetection)

- **Internet Explorer download enclosures**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/DisableEnclosureDownloading](https://go.microsoft.com/fwlink/?linkid=2067245)

- **Internet Explorer ignore certificate errors**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/DisableIgnoringCertificateErrors](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-disableignoringcertificateerrors)

- **Internet Explorer disable processes in enhanced protected mode**  
  Baseline default: *Enable*  
  CSP [InternetExplorer/DisableProcessesInEnhancedProtectedMode](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-disableprocessesinenhancedprotectedmode)

- **Internet Explorer security settings check**  
  Baseline default: *Enabled*  
  CSP [InternetExplorer/DisableSecuritySettingsCheck](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-disablesecuritysettingscheck)

- **Internet Explorer Active X controls in protected mode**  
  Baseline default: *Disabled*  
  CSP [InternetExplorer/DoNotAllowActiveXControlsInProtectedMode](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-donotallowactivexcontrolsinprotectedmode)

- **Internet Explorer users adding sites**  
  Baseline default: *Disabled*  
  CSP [InternetExplorer/DoNotAllowUsersToAddSites](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-donotallowuserstoaddsites)

- **Internet Explorer users changing policies**  
  Baseline default: *Disabled*  
  CSP [InternetExplorer/DoNotAllowUsersToChangePolicies](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-donotallowuserstochangepolicies)

- **Internet Explorer block outdated Active X controls**  
  Baseline default: *Enabled*  
  CSP [InternetExplorer/DoNotBlockOutdatedActiveXControls](https://go.microsoft.com/fwlink/?linkid=2067203)

- **Internet Explorer include all network paths**  
  Baseline default: *Disabled*  
  CSP [InternetExplorer/IncludeAllNetworkPaths](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-includeallnetworkpaths)

- **Internet Explorer internet zone access to data sources**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/InternetZoneAllowAccessToDataSources](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowaccesstodatasources)

- **Internet Explorer internet zone automatic prompt for file downloads**  
  Baseline default: *Disabled*  
  CSP [InternetExplorer/InternetZoneAllowAutomaticPromptingForFileDownloads](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowautomaticpromptingforfiledownloads)

- **Internet Explorer internet zone copy and paste via script**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/InternetZoneAllowCopyPasteViaScript](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowcopypasteviascript)

- **Internet Explorer internet zone drag and drop or copy and paste files**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/InternetZoneAllowDragAndDropCopyAndPasteFiles](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowdraganddropcopyandpastefiles)

- **Internet Explorer internet zone less privileged sites**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/InternetZoneAllowLessPrivilegedSites](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowlessprivilegedsites)

- **Internet Explorer internet zone loading of XAML files**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/InternetZoneAllowLoadingOfXAMLFiles](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowloadingofxamlfiles)

- **Internet Explorer internet zone .NET Framework reliant components**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/InternetZoneAllowNETFrameworkReliantComponents](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallownetframeworkreliantcomponents)

- **Internet Explorer internet zone allows only approved domains to use ActiveX controls**  
  Baseline default: *Enabled*  
  CSP [InternetExplorer/InternetZoneAllowOnlyApprovedDomainsToUseActiveXControls](https://go.microsoft.com/fwlink/?linkid=2067091)

- **Internet Explorer internet zone allows only approved domains to use tdc ActiveX controls**  
  Baseline default: *Enabled*  
  CSP [InternetExplorer/InternetZoneAllowOnlyApprovedDomainsToUseTDCActiveXControl](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowonlyapproveddomainstousetdcactivexcontrol)

- **Internet Explorer internet zone scripting of web browser controls**  
  Baseline default: *Disabled*  
  CSP [InternetExplorer/InternetZoneAllowScriptingOfInternetExplorerWebBrowserControls](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowscriptingofinternetexplorerwebbrowsercontrols)

- **Internet Explorer internet zone script initiated windows**  
  Baseline default: *Disabled*  
  CSP [InternetExplorer/InternetZoneAllowScriptInitiatedWindows](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowscriptinitiatedwindows)

- **Internet Explorer internet zone scriptlets**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/InternetZoneAllowScriptlets](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowscriptlets)

- **Internet Explorer internet zone smart screen**  
  Baseline default: *Enabled*  
  CSP [InternetExplorer/InternetZoneAllowSmartScreenIE](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowsmartscreenie)

- **Internet Explorer internet zone updates to status bar via script**  
  Baseline default: *Disabled*  
  CSP [InternetExplorer/InternetZoneAllowUpdatesToStatusBarViaScript](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowupdatestostatusbarviascript)

- **Internet Explorer internet zone user data persistence**  
  Baseline default: *Disabled*  
  CSP [InternetExplorer/InternetZoneAllowUserDataPersistence](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowuserdatapersistence)

- **Internet Explorer internet zone allows VBscript to run**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/InternetZoneAllowVBScriptToRunInInternetExplorer](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneallowvbscripttorunininternetexplorer)

- **Internet Explorer internet zone do not run antimalware against ActiveX controls**  
  Baseline default: *Disabled*  
  CSP [InternetExplorer/InternetZoneDoNotRunAntimalwareAgainstActiveXControls](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzonedonotrunantimalwareagainstactivexcontrols)

- **Internet Explorer internet zone download signed ActiveX controls**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/InternetZoneDownloadSignedActiveXControls](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzonedownloadsignedactivexcontrols)

- **Internet Explorer internet zone download unsigned ActiveX controls**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/InternetZoneDownloadUnsignedActiveXControls](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzonedownloadunsignedactivexcontrols)

- **Internet Explorer internet zone cross site scripting filter**  
  Baseline default: *Enabled*  
  CSP [InternetExplorer/InternetZoneEnableCrossSiteScriptingFilter](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneenablecrosssitescriptingfilter)

- **Internet Explorer internet zone drag content from different domains across windows**  
  Baseline default: *Disabled*  
  CSP [InternetExplorer/InternetZoneEnableDraggingOfContentFromDifferentDomainsAcrossWindows](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneenabledraggingofcontentfromdifferentdomainsacrosswindows)

- **Internet Explorer internet zone drag content from different domains within windows**  
  Baseline default: *Disabled*  
  CSP [InternetExplorer/InternetZoneEnableDraggingOfContentFromDifferentDomainsWithinWindows](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneenabledraggingofcontentfromdifferentdomainsacrosswindows)

- **Internet Explorer internet zone protected mode**  
  Baseline default: *Enable*  
  CSP [InternetExplorer/InternetZoneEnableProtectedMode](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneenableprotectedmode)

- **Internet Explorer internet zone include local path when uploading files to server**  
  Baseline default: *Disabled*  
  CSP [InternetExplorer/InternetZoneIncludeLocalPathWhenUploadingFilesToServer](https://go.microsoft.com/fwlink/?linkid=2067072)

- **Internet Explorer internet zone initialize and script Active X controls not marked as safe**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/InternetZoneInitializeAndScriptActiveXControlsNotMarkedSafe](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzoneinitializeandscriptactivexcontrolsnotmarkedsafe)

- **Internet Explorer internet zone java permissions**  
  Baseline default: *Disable java*  
  CSP [InternetExplorer/InternetZoneJavaPermissions](https://go.microsoft.com/fwlink/?linkid=2067174)

- **Internet Explorer internet zone launch applications and files in an iframe**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/InternetZoneLaunchingApplicationsAndFilesInIFRAME](https://go.microsoft.com/fwlink/?linkid=2067020)

- **Internet Explorer internet zone logon options**  
  Baseline default: *Prompt*  
  CSP [InternetExplorer/InternetZoneLogonOptions](https://go.microsoft.com/fwlink/?linkid=2067194)

- **Internet Explorer internet zone navigate windows and frames across different domains**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/InternetZoneNavigateWindowsAndFrames](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzonenavigatewindowsandframes)

- **Internet Explorer internet zone run .NET Framework reliant components signed with Authenticode**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/InternetZoneRunNETFrameworkReliantComponentsSignedWithAuthenticode](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-internetzonerunnetframeworkreliantcomponentssignedwithauthenticode)

- **Internet Explorer internet zone security warning for potentially unsafe files**  
  Baseline default: *Prompt*  
  CSP [InternetExplorer/InternetZoneShowSecurityWarningForPotentiallyUnsafeFiles](https://go.microsoft.com/fwlink/?linkid=2067204)

- **Internet Explorer internet zone popup blocker**  
  Baseline default: *Enable*  
  CSP [InternetExplorer/InternetZoneUsePopupBlocker](https://go.microsoft.com/fwlink/?linkid=2067069)

- **Internet Explorer intranet zone do not run antimalware against Active X controls**  
  Baseline default: *Disabled*  
  CSP [InternetExplorer/IntranetZoneDoNotRunAntimalwareAgainstActiveXControls](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-intranetzonedonotrunantimalwareagainstactivexcontrols)

- **Internet Explorer intranet zone initialize and script Active X controls not marked as safe**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/IntranetZoneInitializeAndScriptActiveXControls](https://go.microsoft.com/fwlink/?linkid=2067175)

- **Internet Explorer intranet zone java permissions**  
  Baseline default: *High safety*  
  CSP [InternetExplorer/IntranetZoneJavaPermissions](https://go.microsoft.com/fwlink/?linkid=2067206)

- **Internet Explorer local machine zone do not run antimalware against Active X controls**  
  Baseline default: *Disabled*  
  CSP [InternetExplorer/LocalMachineZoneDoNotRunAntimalwareAgainstActiveXControls](https://go.microsoft.com/fwlink/?linkid=2067152)

- **Internet Explorer local machine zone java permissions**  
  Baseline default: *Disable java*  
  CSP [InternetExplorer/LocalMachineZoneJavaPermissions](https://go.microsoft.com/fwlink/?linkid=2067113)

- **Internet Explorer locked down internet zone smart screen**  
  Baseline default: *Enabled*  
  CSP [InternetExplorer/LockedDownInternetZoneAllowSmartScreenIE](https://go.microsoft.com/fwlink/?linkid=2067059)

- **Internet Explorer locked down intranet zone java permissions**  
  Baseline default: *Disable java*  
  CSP [InternetExplorer/LockedDownIntranetJavaPermissions](https://go.microsoft.com/fwlink/?linkid=2067082)

- **Internet Explorer locked down local machine zone java permissions**  
  Baseline default: *Disable java*  
  CSP [InternetExplorer/LockedDownLocalMachineZoneJavaPermissions](https://go.microsoft.com/fwlink/?linkid=2067253)

- **Internet Explorer locked down restricted zone smart screen**  
  Baseline default: *Enabled*  
  CSP [InternetExplorer/RestrictedSitesZoneAllowSmartScreenIE](https://go.microsoft.com/fwlink/?linkid=2067092)

- **Internet Explorer locked down restricted zone java permissions**  
  Baseline default: *Disable java*  
  CSP [InternetExplorer/LockedDownRestrictedSitesZoneJavaPermissions](https://go.microsoft.com/fwlink/?linkid=2067181)

- **Internet Explorer locked down trusted zone java permissions**  
  Baseline default: *Disable java*  
  CSP [InternetExplorer/LockedDownTrustedSitesZoneJavaPermissions](https://go.microsoft.com/fwlink/?linkid=2067142)

- **Internet Explorer processes MIME sniffing safety feature**  
  Baseline default: *Enabled*  
  CSP [InternetExplorer/MimeSniffingSafetyFeatureInternetExplorerProcesses](https://go.microsoft.com/fwlink/?linkid=2067124)

- **Internet Explorer processes MK protocol security restriction**  
  Baseline default: *Enabled*  
  CSP [InternetExplorer/MKProtocolSecurityRestrictionInternetExplorerProcesses](https://go.microsoft.com/fwlink/?linkid=2067179)

- **Internet Explorer processes notification bar**  
  Baseline default: *Enabled*  
  CSP [InternetExplorer/NotificationBarInternetExplorerProcesses](https://go.microsoft.com/fwlink/?linkid=2067139)

- **Internet Explorer prevent per user installation of Active X controls**  
  Baseline default: *Enabled*  
  CSP [InternetExplorer/PreventPerUserInstallationOfActiveXControls](https://go.microsoft.com/fwlink/?linkid=2067058)

- **Internet Explorer processes protection from zone elevation**  
  Baseline default: *Enabled*  
  CSP [InternetExplorer/ProtectionFromZoneElevationInternetExplorerProcesses](https://go.microsoft.com/fwlink/?linkid=2067160)

- **Internet Explorer remove run this time button for outdated Active X controls**  
  Baseline default: *Enabled*  
  CSP [InternetExplorer/RemoveRunThisTimeButtonForOutdatedActiveXControls](https://go.microsoft.com/fwlink/?linkid=2067123)

- **Internet Explorer processes restrict Active X install**  
  Baseline default: *Enabled*  
  CSP [InternetExplorer/RestrictActiveXInstallInternetExplorerProcesses](https://go.microsoft.com/fwlink/?linkid=2067250)

- **Internet Explorer restricted zone access to data sources**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/RestrictedSitesZoneAllowAccessToDataSources](https://go.microsoft.com/fwlink/?linkid=2067161)

- **Internet Explorer restricted zone active scripting**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/RestrictedSitesZoneAllowActiveScripting](https://go.microsoft.com/fwlink/?linkid=2067172)

- **Internet Explorer restricted zone automatic prompt for file downloads**  
  Baseline default: *Disabled*  
  CSP [InternetExplorer/RestrictedSitesZoneAllowAutomaticPromptingForFileDownloads](https://go.microsoft.com/fwlink/?linkid=2067150)

- **Internet Explorer restricted zone binary and script behaviors**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/RestrictedSitesZoneAllowBinaryAndScriptBehaviors](https://go.microsoft.com/fwlink/?linkid=2067224)

- **Internet Explorer restricted zone copy and paste via script**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/RestrictedSitesZoneAllowCopyPasteViaScript](https://go.microsoft.com/fwlink/?linkid=2067165)

- **Internet Explorer restricted zone drag and drop or copy and paste files**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/RestrictedSitesZoneAllowDragAndDropCopyAndPasteFiles](https://go.microsoft.com/fwlink/?linkid=2067096)

- **Internet Explorer restricted zone less privileged sites**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/InternetZoneAllowLessPrivilegedSites](https://go.microsoft.com/fwlink/?linkid=2067148)

- **Internet Explorer restricted zone loading of XAML files**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/RestrictedSitesZoneAllowLoadingOfXAMLFiles](https://go.microsoft.com/fwlink/?linkid=2067070)

- **Internet Explorer restricted zone meta refresh**  
  Baseline default: *Disabled*  
  CSP [InternetExplorer/RestrictedSitesZoneAllowMETAREFRESH](https://go.microsoft.com/fwlink/?linkid=2067154)

- **Internet Explorer restricted zone .NET Framework reliant components**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/RestrictedSitesZoneAllowNETFrameworkReliantComponents](https://go.microsoft.com/fwlink/?linkid=2067077)

- **Internet Explorer restricted zone allows only approved domains to use Active X controls**  
  Baseline default: *Enabled*  
  CSP [InternetExplorer/RestrictedSitesZoneAllowOnlyApprovedDomainsToUseActiveXControls](https://go.microsoft.com/fwlink/?linkid=2067233)

- **Internet Explorer restricted zone allows only approved domains to use tdc Active X controls**  
  Baseline default: *Enabled*  
  CSP [InternetExplorer/RestrictedSitesZoneAllowOnlyApprovedDomainsToUseTDCActiveXControl](https://go.microsoft.com/fwlink/?linkid=2067032)

- **Internet Explorer restricted zone scripting of web browser controls**  
  Baseline default: *Disabled*  
  CSP [InternetExplorer/RestrictedSitesZoneAllowScriptingOfInternetExplorerWebBrowserControls](https://go.microsoft.com/fwlink/?linkid=2067098)

- **Internet Explorer restricted zone script initiated windows**  
  Baseline default: *Disabled*  
  CSP [InternetExplorer/RestrictedSitesZoneAllowScriptInitiatedWindows](https://go.microsoft.com/fwlink/?linkid=2067075)

- **Internet Explorer restricted zone scriptlets**  
  Baseline default: *Disabled*  
  CSP [InternetExplorer/RestrictedSitesZoneAllowScriptlets](https://go.microsoft.com/fwlink/?linkid=2067112)

- **Internet Explorer restricted zone smart screen**  
  Baseline default: *Enabled*  
  CSP [InternetExplorer/RestrictedSitesZoneAllowSmartScreenIE](https://go.microsoft.com/fwlink/?linkid=2067034)

- **Internet Explorer restricted zone updates to status bar via script**  
  Baseline default: *Disabled*  
  CSP [InternetExplorer/RestrictedSitesZoneAllowUserDataPersistence](https://go.microsoft.com/fwlink/?linkid=2067081)

- **Internet Explorer restricted zone user data persistence**  
  Baseline default: *Disabled*  
  CSP [InternetExplorer/RestrictedSitesZoneAllowUserDataPersistence](https://go.microsoft.com/fwlink/?linkid=2067081)

- **Internet Explorer restricted zone allows vbscript to run**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/RestrictedSitesZoneAllowVBScriptToRunInInternetExplorer](https://go.microsoft.com/fwlink/?linkid=2067173)

- **Internet Explorer restricted zone do not run antimalware against Active X controls**  
  Baseline default: *Disabled*  
  CSP [InternetExplorer/RestrictedSitesZoneDoNotRunAntimalwareAgainstActiveXControls](https://go.microsoft.com/fwlink/?linkid=2067089)

- **Internet Explorer restricted zone download signed Active X controls**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/RestrictedSitesZoneDownloadSignedActiveXControls](https://go.microsoft.com/fwlink/?linkid=2067120)

- **Internet Explorer restricted zone download unsigned Active X controls**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/RestrictedSitesZoneDownloadUnsignedActiveXControls](https://go.microsoft.com/fwlink/?linkid=2067177)

- **Internet Explorer restricted zone cross site scripting filter**  
  Baseline default: *Enabled*  
  CSP [InternetExplorer/RestrictedSitesZoneEnableCrossSiteScriptingFilter](https://go.microsoft.com/fwlink/?linkid=2067178)

- **Internet Explorer restricted zone drag content from different domains across windows**  
  Baseline default: *Disabled*  
  CSP [InternetExplorer/RestrictedSitesZoneEnableDraggingOfContentFromDifferentDomainsAcrossWindows](https://go.microsoft.com/fwlink/?linkid=2067166)

- **Internet Explorer restricted zone drag content from different domains within windows**  
  Baseline default: *Disabled*  
  CSP [InternetExplorer/RestrictedSitesZoneEnableDraggingOfContentFromDifferentDomainsWithinWindows](https://go.microsoft.com/fwlink/?linkid=2067079)

- **Internet Explorer restricted zone include local path when uploading files to server**  
  Baseline default: *Disabled*  
  CSP [InternetExplorer/RestrictedSitesZoneIncludeLocalPathWhenUploadingFilesToServer](https://go.microsoft.com/fwlink/?linkid=2067085)

- **Internet Explorer restricted zone initialize and script Active X controls not marked as safe**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/RestrictedSitesZoneInitializeAndScriptActiveXControls](https://go.microsoft.com/fwlink/?linkid=2067097)

- **Internet Explorer restricted zone java permissions**  
  Baseline default: *Disable java*  
  CSP [InternetExplorer/RestrictedSitesZoneJavaPermissions](https://go.microsoft.com/fwlink/?linkid=2067132)

- **Internet Explorer restricted zone launch applications and files in an iFrame**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/RestrictedSitesZoneLaunchingApplicationsAndFilesInIFRAME](https://go.microsoft.com/fwlink/?linkid=2067061)

- **Internet Explorer restricted zone logon options**  
  Baseline default: *Anonymous*  
  CSP [InternetExplorer/RestrictedSitesZoneLogonOptions](https://go.microsoft.com/fwlink/?linkid=2067110)

- **Internet Explorer restricted zone navigate windows and frames across different domains**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/RestrictedSitesZoneEnableDraggingOfContentFromDifferentDomainsAcrossWindows](https://go.microsoft.com/fwlink/?linkid=2067050)

- **Internet Explorer restricted zone run Active X controls and plugins**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/RestrictedSitesZoneRunActiveXControlsAndPlugins](https://go.microsoft.com/fwlink/?linkid=2067114)

- **Internet Explorer restricted zone run .NET Framework reliant components signed with Authenticode**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/RestrictedSitesZoneRunNETFrameworkReliantComponentsSignedWithAuthenticode](https://go.microsoft.com/fwlink/?linkid=2067169)

- **Internet Explorer restricted zone scripting of java applets**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/RestrictedSitesZoneScriptingOfJavaApplets](https://go.microsoft.com/fwlink/?linkid=2067202)

- **Internet Explorer restricted zone security warning for potentially unsafe files**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/RestrictedSitesZoneShowSecurityWarningForPotentiallyUnsafeFiles](https://go.microsoft.com/fwlink/?linkid=2066797)

- **Internet Explorer restricted zone protected mode**  
  Baseline default: *Enable*  
  CSP [InternetExplorer/RestrictedSitesZoneTurnOnProtectedMode](https://go.microsoft.com/fwlink/?linkid=2067080)

- **Internet Explorer restricted zone popup blocker**  
  Baseline default: *Enable*  
  CSP [InternetExplorer/RestrictedSitesZoneUsePopupBlocker](https://go.microsoft.com/fwlink/?linkid=2067180)

- **Internet Explorer processes restrict file download**  
  Baseline default: *Enabled*  
  CSP [InternetExplorer/RestrictFileDownloadInternetExplorerProcesses](https://go.microsoft.com/fwlink/?linkid=2067164)

- **Internet Explorer processes scripted window security restrictions**  
  Baseline default: *Enabled*  
  CSP [InternetExplorer/ScriptedWindowSecurityRestrictionsInternetExplorerProcesses](https://go.microsoft.com/fwlink/?linkid=2067146)

- **Internet Explorer security zones use only machine settings**  
  Baseline default: *Enabled*  
  CSP [InternetExplorer/SecurityZonesUseOnlyMachineSettings](https://go.microsoft.com/fwlink/?linkid=2067086)

- **Internet Explorer use Active X installer service**  
  Baseline default: *Enabled*  
  CSP [InternetExplorer/SpecifyUseOfActiveXInstallerService](/windows/client-management/mdm/policy-csp-internetexplorer#internetexplorer-specifyuseofactivexinstallerservice)  <!-- https://go.microsoft.com/fwlink/?linkid=2067163 -->

- **Internet Explorer trusted zone do not run antimalware against Active X controls**  
  Baseline default: *Disabled*  
  CSP [InternetExplorer/TrustedSitesZoneDoNotRunAntimalwareAgainstActiveXControls](https://go.microsoft.com/fwlink/?linkid=2067115)

- **Internet Explorer trusted zone initialize and script Active X controls not marked as safe**  
  Baseline default: *Disable*  
  CSP [InternetExplorer/InternetZoneInitializeAndScriptActiveXControlsNotMarkedSafe](https://go.microsoft.com/fwlink/?linkid=2067137)

- **Internet Explorer trusted zone java permissions**  
  Baseline default: *High safety*  
  CSP [InternetExplorer/TrustedSitesZoneJavaPermissions](https://go.microsoft.com/fwlink/?linkid=2067200)

- **Internet Explorer auto complete**  
  Baseline default: *Disabled*  
  CSP [InternetExplorer/AllowAutoComplete](https://go.microsoft.com/fwlink/?linkid=2067122)

## Local Policies Security Options

- **Block remote logon with blank password**  
  Baseline default: *Yes*  
  CSP [LocalPoliciesSecurityOptions/Accounts_LimitLocalAccountUseOfBlankPasswordsToConsoleLogonOnly](https://go.microsoft.com/fwlink/?linkid=2067219)

- **Minutes of lock screen inactivity until screen saver activates**  
  Baseline default: *15*  
  CSP [LocalPoliciesSecurityOptions/InteractiveLogon_MachineInactivityLimit](https://go.microsoft.com/fwlink/?linkid=2067210)

- **Smart card removal behavior**  
  Baseline default: *Lock workstation*  
  CSP [LocalPoliciesSecurityOptions/InteractiveLogon_SmartCardRemovalBehavior](https://go.microsoft.com/fwlink/?linkid=2067331)

- **Require client to always digitally sign communications**  
  Baseline default: *Yes*  
  CSP [LocalPoliciesSecurityOptions/MicrosoftNetworkClient_DigitallySignCommunicationsAlways](https://go.microsoft.com/fwlink/?linkid=2067187)

- **Prevent clients from sending unencrypted passwords to third party SMB servers**  
  Baseline default: *Yes*  
  CSP [LocalPoliciesSecurityOptions/MicrosoftNetworkClient_SendUnencryptedPasswordToThirdPartySMBServers](https://go.microsoft.com/fwlink/?linkid=2067235)

- **Require server digitally signing communications always**  
  Baseline default: *Yes*  
  CSP [LocalPoliciesSecurityOptions/MicrosoftNetworkServer_DigitallySignCommunicationsAlways](https://go.microsoft.com/fwlink/?linkid=2067319)

- **Prevent anonymous enumeration of SAM accounts**  
  Baseline default: *Yes*  
  CSP [LocalPoliciesSecurityOptions/NetworkAccess_DoNotAllowAnonymousEnumerationOfSAMAccounts](https://go.microsoft.com/fwlink/?linkid=2067318)

- **Block anonymous enumeration of SAM accounts and shares**  
  Baseline default: *Yes*  
  CSP [LocalPoliciesSecurityOptions/NetworkAccess_DoNotAllowAnonymousEnumerationOfSamAccountsAndShares](https://go.microsoft.com/fwlink/?linkid=2067191)

- **Restrict anonymous access to named pipes and shares**  
  Baseline default: *Yes*  
  CSP [LocalPoliciesSecurityOptions/NetworkAccess_RestrictAnonymousAccessToNamedPipesAndShares](https://go.microsoft.com/fwlink/?linkid=2067212)

- **Allow remote calls to security accounts manager**  
  Baseline default: *O:BAG:BAD:(A;;RC;;;BA)*  
  CSP [LocalPoliciesSecurityOptions/NetworkAccess_RestrictClientsAllowedToMakeRemoteCallsToSAM](https://go.microsoft.com/fwlink/?linkid=2067209)

- **Prevent storing LAN manager hash value on next password change**  
  Baseline default: *Yes*  
  CSP [LocalPoliciesSecurityOptions/NetworkSecurity_DoNotStoreLANManagerHashValueOnNextPasswordChange](https://go.microsoft.com/fwlink/?linkid=2067213)

- **Authentication level**  
  Baseline default: *Send NTLMv2 response only. Refuse LM and NTLM*  
  CSP [LocalPoliciesSecurityOptions/NetworkSecurity_LANManagerAuthenticationLevel](https://go.microsoft.com/fwlink/?linkid=2067189)

- **Minimum session security for NTLM SSP based clients**  
  Baseline default: *Require NTLM V2 and 128 bit encryption*  
  CSP [LocalPoliciesSecurityOptions/NetworkSecurity_MinimumSessionSecurityForNTLMSSPBasedClients](https://go.microsoft.com/fwlink/?linkid=2067324)

- **Minimum session security for NTLM SSP based servers**  
  Baseline default: *Require NTLM V2 and 128 bit encryption*  
  CSP [LocalPoliciesSecurityOptions/NetworkSecurity_MinimumSessionSecurityForNTLMSSPBasedServers](https://go.microsoft.com/fwlink/?linkid=2067246)

- **Administrator elevation prompt behavior**  
  Baseline default: *Prompt for consent on the secure desktop*  
  CSP [LocalPoliciesSecurityOptions/UserAccountControl_BehaviorOfTheElevationPromptForAdministrators](https://go.microsoft.com/fwlink/?linkid=2067215)

- **Standard user elevation prompt behavior**  
  Baseline default: *Automatically deny elevation requests*  
  CSP [LocalPoliciesSecurityOptions/UserAccountControl_BehaviorOfTheElevationPromptForStandardUsers](https://go.microsoft.com/fwlink/?linkid=2067183)

- **Detect application installations and prompt for elevation**  
  Baseline default: *Yes*  
  CSP [LocalPoliciesSecurityOptions/UserAccountControl_DetectApplicationInstallationsAndPromptForElevation](https://go.microsoft.com/fwlink/?linkid=2067208)

- **Only allow UI access applications for secure locations**  
  Baseline default: *Yes*  
  CSP [LocalPoliciesSecurityOptions/UserAccountControl_OnlyElevateUIAccessApplicationsThatAreInstalledInSecureLocations](https://go.microsoft.com/fwlink/?linkid=2067185)

- **Require admin approval mode for administrators**  
  Baseline default: *Yes*  
  CSP [LocalPoliciesSecurityOptions/UserAccountControl_UseAdminApprovalMode](https://go.microsoft.com/fwlink/?linkid=2067184)

- **Use admin approval mode**  
  Baseline default: *Yes*  
  CSP [LocalPoliciesSecurityOptions/UserAccountControl_RunAllAdministratorsInAdminApprovalMode](https://go.microsoft.com/fwlink/?linkid=2067186)

- **Virtualize file and registry write failures to per user locations**  
  Baseline default: *Yes*  
  CSP [LocalPoliciesSecurityOptions/UserAccountControl_VirtualizeFileAndRegistryWriteFailuresToPerUserLocations](https://go.microsoft.com/fwlink/?linkid=2067321)

## Microsoft Defender

- **Turn on real-time protection**  
  Baseline default: *Yes*  
  CSP [Defender/AllowRealtimeMonitoring](https://go.microsoft.com/fwlink/?linkid=2114050)

- **Scan scripts that are used in Microsoft browsers**  
  Baseline default: *Yes*
  CSP [Defender/AllowScriptScanning](/windows/client-management/mdm/policy-csp-defender#defender-allowscriptscanning)

- **Additional amount of time (0-50 seconds) to extend cloud protection timeout**  
  Baseline default: *50*  
  CSP [Defender/CloudExtendedTimeout](https://go.microsoft.com/fwlink/?linkid=2113940)

- **Scan all downloaded files and attachments**  
  Baseline default: *Yes*  
  CSP [Defender/AllowIOAVProtection](https://go.microsoft.com/fwlink/?linkid=2113934)

- **Scan type**  
  Baseline default: *Quick scan*  
  CSP [Defender/ScanParameter](https://go.microsoft.com/fwlink/?linkid=2114045)

- **Defender schedule scan day**  
  Baseline default: *Everyday*  

- **Scheduled scan start time**  
  Baseline default: *Not configured*  

- **Defender sample submission consent**  
  Baseline default: *Send safe samples automatically*  
  CSP [Defender/SubmitSamplesConsent](https://go.microsoft.com/fwlink/?linkid=2067131)

- **Cloud-delivered protection level**  
  Baseline default: *High*  
  CSP [Defender/CloudBlockLevel](https://go.microsoft.com/fwlink/?linkid=2113942)

- **Scan removable drives during full scan**  
  Baseline default: *Yes*  
  CSP [Defender/AllowFullScanRemovableDriveScanning](https://go.microsoft.com/fwlink/?linkid=2113946)

- **Defender potentially unwanted app action**  
  Baseline default: *Block*  
  CSP [Defender/PUAProtection](/windows/client-management/mdm/policy-csp-defender?WT.mc_id=Portal-Microsoft_Intune_Workflows#defender-puaprotection)

- **Turn on cloud-delivered protection**  
  Baseline default: *Yes*  
  CSP [Defender/AllowCloudProtection](https://go.microsoft.com/fwlink/?linkid=2113937)

## Microsoft Defender Antivirus Exclusions

- **Defender Processes to exclude**  
  Baseline defaults:  
  - *%ProgramFiles%\FSLogix\Apps\frxccd.exe*
  - *%ProgramFiles%\FSLogix\Apps\frxccds.exe*
  - *%ProgramFiles%\FSLogix\Apps\frxsvc.exe*  

- **File extensions to exclude from scans and real-time protection**  
  Baseline defaults:  
  - *%ProgramFiles%\FSLogix\Apps\frxdrv.sys*
  - *%ProgramFiles%\FSLogix\Apps\frxdrvvts.sys*
  - *%%ProgramFiles%\FSLogix\Apps\frxccd.sys*
  - *%TEMP%*.VHD*
  - *%Windir%\TEMP**.*VHD*
  - *%Windir%\TEMP**.*VHDX*
  - *\\\storageaccount.file.core.windows.net\share***.*VHD*
  - *\\\storageaccount.file.core.windows.net\share***.*VHDX*

- **Defender Files And Folders To Exclude**  
  Baseline default:  
  *This setting has no default entries.*

## Microsoft Edge

- **Control which extensions cannot be installed**  
  Baseline default: *Enabled*  

  - **Extension IDs the user should be prevented from installing (or * for all)**  
    Baseline default:
    - \*

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
    Baseline defaults:
    - *NTLM*
    - *Negotiate*

## MS Security Guide

- **SMB v1 client driver start configuration**  
  Baseline default: *Disable driver*  
  CSP [MSSecurityGuide/ConfigureSMBV1ClientDriver](https://go.microsoft.com/fwlink/?linkid=2067214)

- **Apply UAC restrictions to local accounts on network logon**  
  Baseline default: *Enabled*  
  CSP [MSSecurityGuide/ApplyUACRestrictionsToLocalAccountsOnNetworkLogon](https://go.microsoft.com/fwlink/?linkid=2067188)

- **Structured exception handling overwrite protection**  
  Baseline default: *Enabled*  
  CSP [MSSecurityGuide/EnableStructuredExceptionHandlingOverwriteProtection](https://go.microsoft.com/fwlink/?linkid=2067217)

- **SMB v1 server**  
  Baseline default: *Disabled*  
  CSP [MSSecurityGuide/ConfigureSMBV1Server](https://go.microsoft.com/fwlink/?linkid=2067190)

- **Digest authentication**  
  Baseline default: *Disabled*  
  CSP [MSSecurityGuide/WDigestAuthentication](https://go.microsoft.com/fwlink/?linkid=2067193)

## MSS Legacy

- **Network IPv6 source routing protection level**  
  Baseline default: *Highest protection*  
  CSP [MSSLegacy/IPv6SourceRoutingProtectionLevel](https://go.microsoft.com/fwlink/?linkid=2067216)

- **Network IP source routing protection level**  
  Baseline default: *Highest protection*  
  CSP [MSSLegacy/IPSourceRoutingProtectionLevel](https://go.microsoft.com/fwlink/?linkid=2067220)

- **Network ignore NetBIOS name release requests except from WINS servers**  
  Baseline default: *Enabled*  
  CSP [MSSLegacy/AllowTheComputerToIgnoreNetBIOSNameReleaseRequestsExceptFromWINSServers](https://go.microsoft.com/fwlink/?linkid=2067218)

- **Network ICMP redirects override OSPF generated routes**  
  Baseline default: *Disabled*  
  CSP [MSSLegacy/AllowICMPRedirectsToOverrideOSPFGeneratedRoutes](https://go.microsoft.com/fwlink/?linkid=2067326)

## Remote Assistance

- **Remote Assistance solicited**
   Baseline default: *Disable Remote Assistance*  
   CSP [RemoteAssistance/SolicitedRemoteAssistance](https://go.microsoft.com/fwlink/?linkid=2067198)

## Remote Desktop Services

- **Remote desktop services client connection encryption level**  
  Baseline default: *High*  
  CSP [RemoteDesktopServices/ClientConnectionEncryptionLevel](https://go.microsoft.com/fwlink/?linkid=2067222)

- **Block drive redirection**  
  Baseline default: *Enabled*  
  <!-- Not devined in UI. Possibly CSP [RemoteDesktopServices/DoNotAllowDriveRedirection](/windows/client-management/mdm/policy-csp-remotedesktopservices#remotedesktopservices-donotallowdriveredirection) -->

- **Block password saving**  
  Baseline default: *Enabled*  
  CSP [RemoteDesktopServices/DoNotAllowPasswordSaving](https://go.microsoft.com/fwlink/?linkid=2067301)

- **Prompt for password upon connection**  
  Baseline default: *Enabled*  
  CSP [RemoteDesktopServices/PromptForPasswordUponConnection](https://go.microsoft.com/fwlink/?linkid=2067328)

- **Secure RPC communication**  
  Baseline default: *Enabled*  
  CSP [RemoteDesktopServices/RequireSecureRPCCommunication](https://go.microsoft.com/fwlink/?linkid=2067248)

## Remote Management

- **Block client digest authentication**  
  Baseline default: *Enabled*  
  CSP [RemoteManagement/DisallowNegotiateAuthenticationClient](https://go.microsoft.com/fwlink/?linkid=2067302)

- **Block storing run as credentials**  
  Baseline default: *Enabled*  
  CSP [RemoteManagement/DisallowStoringOfRunAsCredentials](https://go.microsoft.com/fwlink/?linkid=2067300)

- **Client basic authentication**  
  Baseline default: *Disabled*  
  CSP [RemoteManagement/AllowBasicAuthentication_Client](https://go.microsoft.com/fwlink/?linkid=2067252)

- **Basic authentication**  
  Baseline default: *Disabled*  
  CSP [RemoteManagement/AllowBasicAuthentication_Service](https://go.microsoft.com/fwlink/?linkid=2067223)

- **Client unencrypted traffic**  
  Baseline default: *Disabled*  
  CSP [RemoteManagement/AllowUnencryptedTraffic_Client](https://go.microsoft.com/fwlink/?linkid=2067304)

- **Unencrypted traffic**  
  Baseline default: *Disabled*  
  CSP [RemoteManagement/AllowUnencryptedTraffic_Service](https://go.microsoft.com/fwlink/?linkid=2067226)

## Remote Procedure Call

- **RPC unauthenticated client options**  
  Baseline default: *Authenticated*  
  CSP [RemoteProcedureCall/RPCEndpointMapperClientAuthentication](https://go.microsoft.com/fwlink/?linkid=2067225)

## Search

- **Disable indexing encrypted items**  
  Baseline default: *Yes*  
  CSP [Search/AllowIndexingEncryptedStoresOrItems](https://go.microsoft.com/fwlink/?linkid=2067303)

## Smart Screen

- **Turn on Windows SmartScreen**  
  Baseline default: *Yes*  
  CSP [SmartScreen/EnableSmartScreenInShell](https://go.microsoft.com/fwlink/?linkid=872784)

- **Block users from ignoring SmartScreen warnings**  
  Baseline default: *Yes*  
  CSP [SmartScreen/PreventOverrideForFilesInShell](https://go.microsoft.com/fwlink/?linkid=872783)

## System

- **System boot start driver initialization**  
  Baseline default: *Good unknown and bad critical*  
  CSP [System/BootStartDriverInitialization](https://go.microsoft.com/fwlink/?linkid=2067307)

## Windows Connection Manager

- **Block connection to non-domain networks**  
  Baseline default: *Enabled*  
  CSP [WindowsConnectionManager/ProhitConnectionToNonDomainNetworksWhenConnectedToDomainAuthenticatedNetwork](https://go.microsoft.com/fwlink/?linkid=2067323)

## Windows Ink Workspace

- **Ink Workspace**  
  Baseline default: *Enabled*  
  CSP [WindowsInkWorkspace/AllowWindowsInkWorkspace](https://go.microsoft.com/fwlink/?linkid=2067241)

## Windows PowerShell

- **PowerShell script block logging**  
  Baseline default: *Enabled*  
  CSP [WindowsPowerShell/TurnOnPowerShellScriptBlockLogging](https://go.microsoft.com/fwlink/?linkid=2067330)

::: zone-end
::: zone pivot="win365-2110"

## Windows Security

- **Enable tamper protection to prevent Microsoft Defender being disabled**  
  Baseline default: *Enable*  
  [Reference for Tamper Protection](https://support.microsoft.com/windows/prevent-changes-to-security-settings-with-tamper-protection-31d51aaa-645d-408e-6ce7-8d7f8e593f87)

::: zone-end
