---
# required metadata

title: Intune security baselines settings for Microsoft Edge 
titleSuffix: Microsoft Intune
description: Security baseline settings supported by Intune for managing Microsoft Edge browser
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/23/2020
ms.topic: reference
ms.service: microsoft-intune
ms.localizationpriority: medium
ms.technology:
ms.assetid:
zone_pivot_groups: edge-baseline-versions

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

<!-- Pivots in use: 
::: zone pivot="edge-october-2019"
::: zone-end

::: zone pivot="edge-april-2020"
::: zone-end

::: zone pivot=edge-sept-2020
::: zone-end

::: zone pivot="edge-october-2019,edge-april-2020"
::: zone-end

::: zone pivot="edge-october-2019,edge-april-2020,edge-sept-2020"
::: zone-end
-->

# Microsoft Edge baseline settings for Intune

View the Microsoft Edge web browser baseline settings that are supported by Microsoft Intune. The Microsoft Edge baseline defaults represent the recommended configuration for Microsoft Edge browsers, and might not match baseline defaults for other security baselines.

::: zone pivot="edge-october-2019"

> [!NOTE]
> The Microsoft Edge baseline for October 2019 is in Public Preview.

To update a security baseline profile to the latest version of that baseline, see [Change the baseline version for a profile](../protect/security-baselines-configure.md#change-the-baseline-version-for-a-profile).

::: zone-end
::: zone pivot="edge-april-2020"

**Microsoft Edge baseline for April 2020 (Edge version 80)**  

::: zone-end
::: zone pivot="edge-sept-2020"

**Microsoft Edge baseline for September 2020 (Edge version 85)**  

::: zone-end
::: zone pivot="edge-october-2019,edge-april-2020,edge-sept-2020"

This version of the security baseline replaces previous versions. Profiles that were created prior to the availability of this baseline version:

- Are now read-only. You can continue to use those profiles, but can't edit them to change their configuration.
- Can be updated to the latest version. After update the current baseline version, you can edit the profile to modify settings.

To understand what's changed with this version of the baseline from previous versions, use the [Compare baselines](../protect/security-baselines.md#compare-baseline-versions) action that's available when viewing the *Versions* pane for this baseline. Be sure to select the version of the baseline that you want to view.

To update a security baseline profile to the latest version of that baseline, see [Change the baseline version for a profile](../protect/security-baselines-configure.md#change-the-baseline-version-for-a-profile).


::: zone-end
::: zone pivot="edge-october-2019,edge-april-2020,edge-sept-2020"

## Microsoft Edge

::: zone-end
::: zone pivot="edge-april-2020,edge-sept-2020"

- **Supported authentication schemes**  
  Use this setting to change the default behavior of Edge as to the HTTP authentication schemes that Edge can use. Edge supports and can use the following schemes: *basic*, *digest*, *ntlm*, and *negotiate*.

  - **Enabled** (*default*) - When set to *Enabled*, you can then configure the following setting where you specify which of the four HTTPS authentication schemes Edge can use.
  - **Disabled**
  - **Not configured** - When set to *Not configured*, Edge will support all four schemes.

  **Supported authentication schemes** - To access this setting, the previous instance of *Supported authentication schemes* must be set to *Enabled*.

  Select one or more HTTP authentication schemes for by Edge. By default, two are already selected:
  - **Basic**
  - **Digest**
  - **NTLM** *(Selected by default)*
  - **Negotiate** *(Selected by default)*

  For more information, see [AuthSchemes](/deployedge/microsoft-edge-policies#authschemes) in the Microsoft Edge policies documentation, and [Understanding HTTP authentication](/dotnet/framework/wcf/feature-details/understanding-http-authentication) in the .NET Framework documentation.

- **Default Adobe Flash setting**  
  CSP: [Browser/AllowFlash](/windows/client-management/mdm/policy-csp-browser#browser-allowflash), and [Browser/AllowFlashClickToRun](/windows/client-management/mdm/policy-csp-browser#browser-allowflashclicktorun)

  Enable access to the following setting where you can configure behavior for running the Adobe Flash plug-in.  

  - **Enabled** (*default*)
  - **Disabled**
  - **Not configured**

  When set to *Enabled* you can configure the following setting.

  - **Default Adobe Flash setting**

    - **Block the Adobe Flash plugin** (*default*) - Block Adobe Flash on all sites
    - **Click to play** - Adobe Flash runs, but the user must select the option to start it.

- **Control which extensions cannot be installed**  
  Enable use of a list that specifies extensions that users can't install in Microsoft Edge. When the list is in use, any settings on the list that were previously installed are disabled, and the user can't enable them. If you remove an item from the list of blocked extensions, that extension is automatically re-enabled anywhere it was previously installed.

  - **Enabled** (*default*) - Enable use of the list to block extensions.
  - **Disabled**
  - **Not configured** - Users can install any extension in Microsoft Edge.
  
  When set to *Enabled*, you can configure the following setting that defines the list of extensions to block.

  - **Extension IDs the user should be prevented from installing (or * for all)**

    Select **Add** and specify additional extensions. **\*** is selected by default.

- **Allow user-level native messaging hosts (installed without admin permissions)**  
  Enables user-level installation of native messaging hosts.

  - **Enabled**
  - **Disabled** (*default*) - Microsoft Edge uses only native messaging hosts installed on the system level.
  - **Not configured** - By default, Microsoft Edge allows use of user-level native messaging hosts.

- **Enable saving passwords to the password manager**  
  Microsoft Edge CSP: [Browser/AllowPasswordManager](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)  

  Enable Microsoft Edge to save user passwords.

  - **Enabled** - Users can save their passwords in Microsoft Edge. The next time they visit the site, Microsoft Edge will enter the password automatically. Users can't change or override this policy in Microsoft Edge.
  - **Disabled** (*default*) - Users can't save new passwords, but can continue to use previously saved passwords. Users can't change or override this policy in Microsoft Edge.
  - **Not configured** - Users can save passwords, and turn off this feature.

- **Prevent bypassing Microsoft Defender SmartScreen prompts for sites**  
  CSP: [Browser/PreventSmartScreenPromptOverride](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

  Decide whether users can override the Microsoft Defender SmartScreen warnings about potentially malicious websites.

  - **Enabled** (*default*) - Users can't ignore Microsoft Defender SmartScreen warnings and they're blocked from continuing to the site.
  - **Disabled** - Users can ignore Microsoft Defender SmartScreen warnings and continue to the site.
  - **Not configured** Users can ignore Microsoft Defender SmartScreen warnings and continue to the site

- **Prevent bypassing of Microsoft Defender SmartScreen warnings about downloads**  
  CSP: [Browser/PreventSmartScreenPromptOverrideForFiles](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)  

  Determine whether users can override Microsoft Defender SmartScreen warnings about unverified downloads.

  - **Enabled** (*default*) - Users can't ignore Microsoft Defender SmartScreen warnings, and they're prevented from completing the unverified downloads.
  - **Disabled** - Users can ignore Microsoft Defender SmartScreen warnings and complete unverified downloads.
  - **Not configured** - Users can ignore Microsoft Defender SmartScreen warnings and complete unverified downloads.

- **Enable site isolation for every site**  
  Configure site isolation to prevent users from opting out of the default behavior of isolating all sites.
  
  - **Enabled** (*default*) - Users can't opt out of the default behavior where each site runs in its own process.
  - **Disabled** - Users can opt out of site isolation. Site isolation is not turned off.
  - **Not configured** - Users can opt out of site isolation. Site isolation is not turned off.

  Microsoft Edge also supports [IsolateOrigins](/deployedge/microsoft-edge-policies#isolateorigins) policy that can isolate additional, finer-grained origins.  Intune doesn't support configuring the IsolateOrigins policy.
  
- **Configure Microsoft Defender SmartScreen**  
  CSP: [Browser/AllowSmartScreen](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)  
  
  Microsoft Defender SmartScreen provides warning messages to help protect users from potential phishing scams and malicious software. By default, Microsoft Defender SmartScreen is turned on.
  
  - **Enabled** (*default*) - Microsoft Defender SmartScreen is turned on and users can't turn it off.
  - **Disabled** - Microsoft Defender SmartScreen is turned off and users can't turn it on.
  - **Not configured**  Users can choose whether to use Microsoft Defender SmartScreen.

  This policy is available only on Windows instances that are joined to a Microsoft Active Director domain, or on Windows 10/11 Pro or Enterprise instances that are enrolled for device management.

- **Configure Microsoft Defender SmartScreen to block potentially unwanted apps**  
    Configure Microsoft Defender SmartScreen behavior for blocking potentially unwanted apps. Microsoft Defender SmartScreen can provide a warning messages to help protect users from adware, coin miners, bundleware, and other low-reputation apps that are hosted by websites. Potentially unwanted app blocking in Microsoft Defender SmartScreen is turned off by default.

  - **Enabled** (*default*) - Potentially unwanted apps are blocked.
  - **Disabled** - Potentially unwanted apps are not blocked.
  - **Not configured** - Users can choose whether to use potentially unwanted app blocking in Microsoft Defender SmartScreen.

  This policy is available only on Windows instances that are joined to a Microsoft Active Director domain, or on Windows 10/11 Pro or Enterprise instances that are enrolled for device management.

- **Allow users to proceed from the SSL warning page**  
   CSP: [Browser/PreventCertErrorOverrides](/windows/client-management/mdm/policy-csp-browser#browser-preventcerterroroverrides)  

  Microsoft Edge shows a warning page when users visit sites that have SSL errors.
  - **Enabled** - Users can click through the warning pages.
  - **Disabled** (*default*) - Users are blocked from clicking through any warning page.
  - **Not configured** - Users can click through these warning pages.

- **Minimum SSL version enabled**  
  Enable the option to set a minimum supported version of SSL.

  - **Enabled** (*default*) - Enable access to the next setting where you specify the  minimum version of TLS to use.
  - **Disabled**
  - **Not configured** - Microsoft Edge uses a default minimum version of *TLS 1.0*.

  When set to *Enabled*, you can configure TLS by using the following setting.

  - **Minimum SSL version enabled**
    Set the minimum version of TLS to use. Microsoft Edge won't use any version of SSL/TLS that's lower than the specified version.
    - **TLS 1.0**
    - **TLS 1.1**
    - **TLS 1.2** (*default*)

::: zone-end

::: zone pivot="edge-october-2019"

- **Prevent bypassing Microsoft Defender SmartScreen prompts for sites**  
  **Default**: Enabled  
  Microsoft Edge CSP: [Browser/PreventSmartScreenPromptOverride](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverride)

  This policy setting lets you decide whether users can override the Microsoft Defender SmartScreen warnings about potentially malicious websites. 
  - If you enable this setting, users can't ignore Microsoft Defender SmartScreen warnings and they're blocked from continuing to the site. 
  - If you disable or don't configure this setting, users can ignore Microsoft Defender SmartScreen warnings and continue to the site.

- **Minimum SSL version enabled**  
  **Default**: Enabled  

  Set a minimum supported version of SSL. If you set this policy to *Not Configured*, Microsoft Edge uses a default minimum version of *TLS 1.0*. When set to *Enabled*, you can select a minimum version from the following values:

  - TLS 1.0
  - TLS 1.1
  - TLS 1.2

  - **Minimum SSL version enabled**  
    **Default**: TLS 1.2

- **Prevent bypassing of Microsoft Defender SmartScreen warnings about downloads**  
  **Default**: Enabled  
  Microsoft Edge CSP: [Browser/PreventSmartScreenPromptOverrideForFiles](/windows/client-management/mdm/policy-csp-browser#browser-preventsmartscreenpromptoverrideforfiles)  

  This policy lets you determine whether users can override Microsoft Defender SmartScreen warnings about unverified downloads.
  - If you enable this policy, users in your organization can't ignore Microsoft Defender SmartScreen warnings, and they're prevented from completing the unverified downloads.
  - If you disable or don't configure this policy, users can ignore Microsoft Defender SmartScreen warnings and complete unverified downloads.

- **Allow users to proceed from the SSL warning page**  
  **Default**: Disabled  
  Microsoft Edge CSP: [Browser/PreventCertErrorOverrides](/windows/client-management/mdm/policy-csp-browser#browser-preventcerterroroverrides)  

  Microsoft Edge shows a warning page when users visit sites that have SSL errors. If you set this policy to *Enabled* or *Not Configured*, users can click through these warning pages. When this policy is *Disabled*, users are blocked from clicking through any warning page. 

- **Default Adobe Flash setting**  
  **Default**: Enabled  
  Microsoft Edge CSP: [Browser/AllowFlash](/windows/client-management/mdm/policy-csp-browser#browser-allowflash), and [Browser/AllowFlashClickToRun](/windows/client-management/mdm/policy-csp-browser#browser-allowflashclicktorun)  

  Determines whether websites that aren't covered by 'PluginsAllowedForUrls' or 'PluginsBlockedForUrls' can automatically run the Adobe Flash plug-in. 

  - Select 'BlockPlugins' to block Adobe Flash on all sites
  - Select 'ClickToPlay' to let Adobe Flash run but require the user to click the placeholder to start it.
  
  In any case, the 'PluginsAllowedForUrls' and 'PluginsBlockedForUrls' policies take precedence over 'DefaultPluginsSetting'. Automatic playback is only allowed for domains explicitly listed in the 'PluginsAllowedForUrls' policy. 
   If you want to enable automatic playback for all sites, consider adding http://* and https://* to this list.

  - If you set this policy to *Not Configured*, the user can change this setting manually. * 2 = Block the Adobe Flash plug-in * 3 = Click to play the former '1' option set allow-all, but this functionality is now only handled by the 'PluginsAllowedForUrls' policy. Existing policies using '1' will operate in Click-to-play mode.  

  - **Default Adobe Flash setting**  
    **Default**: Block the Adobe Flash plugin

- **Enable site isolation for every site**  
  **Default**: Enabled  

  The 'SitePerProcess' policy can be used to prevent users from opting out of the default behavior of isolating all sites. You can also use the IsolateOrigins policy to isolate additional, finer-grained origins.

  - When this policy is set to *Enabled*, users can't opt out of the default behavior where each site runs in its own process. 
  - If you use *Disabled* or *Not Configured*, a user can opt out of site isolation. (For example, by using "Disable site isolation" entry in edge://flags.) Disabling the policy or not configuring the policy doesn't turn off Site Isolation.

- **Supported authentication schemes**  
  Use this setting to change the default behavior of Edge as to the HTTP authentication schemes that Edge can use. Edge supports and can use the following schemes: *basic*, *digest*, *ntlm*, and *negotiate*.

  - **Enabled** (*default*) - When set to *Enabled*, you can then configure the following setting where you specify which of the four HTTPS authentication schemes Edge can use.
  - **Disabled**
  - **Not configured** - When set to *Not configured*, Edge will support all four schemes.

  **Supported authentication schemes** - To access this setting, the previous instance of *Supported authentication schemes* must be set to *Enabled*.

  Select one or more HTTP authentication schemes for by Edge. By default, two are already selected:
  - **Basic**
  - **Digest**
  - **NTLM** *(Selected by default)*
  - **Negotiate** *(Selected by default)*

  For more information, see [AuthSchemes](/deployedge/microsoft-edge-policies#authschemes) in the Microsoft Edge policies documentation, and [Understanding HTTP authentication](/dotnet/framework/wcf/feature-details/understanding-http-authentication) in the .NET Framework documentation.

- **Enable saving passwords to the password manager**  
  **Default**: Disabled  
  Microsoft Edge CSP: [Browser/AllowPasswordManager](/windows/client-management/mdm/policy-csp-browser#browser-allowpasswordmanager)  

  Enable Microsoft Edge to save user passwords.
  - If you enable this policy, users can save their passwords in Microsoft Edge. The next time they visit the site, Microsoft Edge will enter the password automatically.
  - If you disable this policy, users can't save new passwords, but they can still use previously saved passwords.
  
  When you set this policy to either *Enabled* or *Disabled*, users can't change or override this policy in Microsoft Edge.
  
  If you set this to *Not Configured*, users can save passwords, as well as turn off this feature.

- **Control which extensions cannot be installed**  
  **Default**: Enabled  

  List the specific extensions that users can't install in Microsoft Edge. When you deploy this policy, any extensions on this list that were previously installed are disabled, and the user won't be able to enable them. If you remove an item from the list of blocked extensions, that extension is automatically re-enabled anywhere it was previously installed.
  
  Use **\*** to block all extensions that aren't explicitly listed in the allow list. If this policy is set to *Not Configured*, users can install any extension in Microsoft Edge.
  
  Example value: extension_id1 extension_id2.  
  <br>
  - **Extension IDs the user should be prevented from installing (or * for all)**  
    Select **Add** and specify additional extensions. **\*** is selected by default.

- **Configure Microsoft Defender SmartScreen**  
  **Default**: Enabled  
  Microsoft Edge CSP: [Browser/AllowSmartScreen](/windows/client-management/mdm/policy-csp-browser#browser-allowsmartscreen)

  This policy setting lets you configure whether to turn on Microsoft Defender SmartScreen. Microsoft Defender SmartScreen provides warning messages to help protect your users from potential phishing scams and malicious software.
  
  - By default, Microsoft Defender SmartScreen is turned on. If you enable this setting, Microsoft Defender SmartScreen is turned on and users can't turn it off.
  - If you disable this setting, Microsoft Defender SmartScreen is turned off and users can't turn it on.
  - When set to *Not Configured*, users can choose whether to use Microsoft Defender SmartScreen.
  
  This policy is available only on Windows instances that are joined to a Microsoft Active Director domain, or on Windows 10/11 Pro or Enterprise instances that are enrolled for device management.

- **Allow user-level native messaging hosts (installed without admin permissions)**  
  **Default**: Disabled

  Enables user-level installation of native messaging hosts. 
  - If you disable this policy, Microsoft Edge will only use native messaging hosts installed on the system level. By default, if you don't configure this policy, Microsoft Edge will allow usage of user-level native messaging hosts.

::: zone-end
::: zone pivot="edge-sept-2020"

- **Allow certificates signed using SHA-1 when issued by local trust anchors (deprecated)**  
  **Default**: Disabled

  DEPRECATED: This policy is deprecated. It is currently supported but will become obsolete in a future release.

  By default, Microsoft Edge forbids certificates signed using SHA-1 as allowing SHA-1 chains is not a secure configuration.
This policy depends on the operating system (OS) certificate verification stack allowing SHA-1 signatures. If an OS update changes the OS handling of SHA-1 certificates, this policy might no longer have effect. Further, this policy is intended as a temporary workaround to give Enterprises more time to move away from SHA-1.

  This policy is only available on Windows instances that are joined to a Microsoft Active Directory domain or Windows 10/11 Pro or Enterprise instances enrolled for device management.

  This policy will be removed in Microsoft Edge 92 releasing in mid-2021.

  - **Enabled** - Microsoft Edge allows connections secured by SHA-1 signed certificates so long as the certificate chains to a locally installed root certificate and is otherwise valid.
  - **Disabled** (default) – When set it to *Disabled*, or the SHA-1 certificate chains to a publicly trusted certificate root, then Microsoft Edge won't allow certificates signed by SHA-1.
  - **Not configured** - Same as behavior as *Disabled*.

::: zone-end
::: zone pivot="edge-october-2019,edge-april-2020,edge-sept-2020"

## Next steps

- [Learn about security baselines](security-baselines.md)
- [Avoid conflicts](security-baselines.md#avoid-conflicts)
- [Troubleshoot policies and profiles in Intune](/troubleshoot/mem/intune/troubleshoot-policies-in-microsoft-intune)

::: zone-end