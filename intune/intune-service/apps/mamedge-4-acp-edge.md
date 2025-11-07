---
title: Step 4. Create App Configuration Policies for Microsoft Edge for Business
description: Step 4. Create app configuration policies for Microsoft Edge for Business across Windows, Android, and iOS platforms.
ms.date: 10/28/2025
ms.topic: how-to
ms.reviewer: samarti
ms.custom:
ms.collection:
- highpri
- highseo
- FocusArea_Apps_AppManagement
zone_pivot_groups: app-protection-platforms
---

# Step 4: App Configuration Policies for Microsoft Edge for Business

App configuration policies (ACP) customize Microsoft Edge for Business behavior and features on each platform. In the Secure Enterprise Browser plan, ACPs work alongside App Protection Policies (Step 2) and Conditional Access (Step 1) to deliver a layered, Zero Trust browser experience on managed and BYOD devices.

This step defines three progressive ACP configurations per platform, Level 1 (Basic), Level 2 (Enhanced), and Level 3 (High), so you can standardize user experience, lock down risky surfaces, and align restrictions to data sensitivity and user risk. These policies complement data-protection controls (APP) rather than replace them.

> [!NOTE]
> App configuration policies customize browser features and behavior. They complement app protection policies that focus on data protection.

::: zone pivot="windows"

## App configuration policies for Windows

Windows app configuration policies provide browser customization through managed app settings.

> **Microsoft Documentation:**
> - [Microsoft Edge Browser Policies](/deployedge/microsoft-edge-browser-policies)
> - [Windows App Configuration Policies](app-configuration-policies-overview.md)
> - [Managed App Configuration for Windows](app-configuration-policies-managed-app.md)

**Prerequisites:**
- Windows 10/11
- Microsoft Edge installed
- Intune enrollment or MAM managed
- User Entra ID account

### Level 1 - Basic browser configuration (Windows)

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Apps** > **Manage Apps** > **Configuration** > **Create** > **Managed apps**.

3. On the **Basics** tab:
    - **Name**: Level 1 - Basic browser configuration - Windows ACP
    - **Description**: Basic browser customization for Microsoft Edge on Windows
    - For **Target policy to**, select **Selected apps** > 
    - Select **Select public Apps** > **Microsoft Edge Windows** > **Select**.

4. Select **Next**.

5. For **Settings**, select **General configuration settings** and add:

    | Setting | Documentation | Key | Value |
    |---------|--------------|-----|-------|
    | Core Browser Behavior (Enterprise Foundation):Configure the home page URL | [HomepageLocation](/deployedge/microsoft-edge-browser-policies/homepagelocation) | HomepageLocation | https://portal.company.com |
    | Core Browser Behavior (Enterprise Foundation):Show Home button on toolbar | [ShowHomeButton](/deployedge/microsoft-edge-browser-policies/showhomebutton) | ShowHomeButton | Enabled |
    | Core Browser Behavior (Enterprise Foundation):Configure the new tab page URL | [NewTabPageLocation](/deployedge/microsoft-edge-browser-policies/newtabpageurl) | NewTabPageLocation | https://portal.company.com |
    | Core Browser Behavior (Enterprise Foundation):Action to take on startup | [RestoreOnStartup](/deployedge/microsoft-edge-browser-policies/restoreonstartup) | RestoreOnStartup | Open the new tab page (5) |
    | Content & Security Controls:Configure Automatic HTTPS | [HTTPSOnlyMode](/deployedge/microsoft-edge-browser-policies/httpsonlymode) | HTTPSOnlyMode | Enabled |
    | Content & Security Controls:Default pop-up window setting | [DefaultPopupsSetting](/deployedge/microsoft-edge-browser-policies/defaultpopupssetting) | DefaultPopupsSetting | Do not allow popups (2) |
    | Privacy & Data Management:Enable saving passwords to the password manager | [PasswordManagerEnabled](/deployedge/microsoft-edge-browser-policies/passwordmanagerenabled) | PasswordManagerEnabled | Disabled |
    | Privacy & Data Management:Enable AutoFill for addresses | [AutofillAddressEnabled](/deployedge/microsoft-edge-browser-policies/autofilladdressenabled) | AutofillAddressEnabled | Disabled |
    | Privacy & Data Management:Enable Autofill for payment instructions | [AutofillCreditCardEnabled](/deployedge/microsoft-edge-browser-policies/autofillcreditcardenabled) | AutofillCreditCardEnabled | Disabled |
    | Privacy & Data Management:Block tracking of users' web-browsing activity | [TrackingPrevention](/deployedge/microsoft-edge-browser-policies/trackingprevention) | TrackingPrevention | Balanced (2) |
    | Search & Navigation Enhancement:Enable the default search provider | [DefaultSearchProviderEnabled](/deployedge/microsoft-edge-browser-policies/defaultsearchproviderenabled) | DefaultSearchProviderEnabled | Enabled |
    | Search & Navigation Enhancement:Default search provider name | [DefaultSearchProviderName](/deployedge/microsoft-edge-browser-policies/defaultsearchprovidername) | DefaultSearchProviderName | Microsoft Bing |
    | Search & Navigation Enhancement:Default search provider search URL | [DefaultSearchProviderSearchURL](/deployedge/microsoft-edge-browser-policies/defaultsearchprovidersearchurl) | DefaultSearchProviderSearchURL | https://www.bing.com/search?q |
    | Search & Navigation Enhancement:Enable search suggestions | [SearchSuggestEnabled](/deployedge/microsoft-edge-browser-policies/searchsuggestenabled) | SearchSuggestEnabled | Disabled |
    | Search & Navigation Enhancement:Enable network prediction | [NetworkPredictionOptions](/deployedge/microsoft-edge-browser-policies/networkpredictionoptions) | NetworkPredictionOptions | Don't predict (2) |
    | Import Controls (Data Boundary):Allow importing of autofill form data | [ImportAutofillFormData](/deployedge/microsoft-edge-browser-policies/importautofillformdata) | ImportAutofillFormData | Disabled |
    | Import Controls (Data Boundary):Allow importing of saved passwords | [ImportSavedPasswords](/deployedge/microsoft-edge-browser-policies/importsavedpasswords) | ImportSavedPasswords | Disabled |
    | Import Controls (Data Boundary):Allow importing of browsing history | [ImportBrowsingHistory](/deployedge/microsoft-edge-browser-policies/importhistory) | ImportBrowsingHistory | Disabled |
    | Import Controls (Data Boundary):Allow importing cookies | [ImportCookies](/deployedge/microsoft-edge-browser-policies/importcookies) | ImportCookies | Disabled |
    | Import Controls (Data Boundary):Allow importing of extension | [ImportExtensions](/deployedge/microsoft-edge-browser-policies/importextensions) | ImportExtensions | Disabled |
    | Extension Management (Basic):Control which extensions cannot be installed | [ExtensionInstallBlocklist](/deployedge/microsoft-edge-browser-policies/extensioninstallblocklist) | ExtensionInstallBlocklist | "external_component", "external_pref", "external_registry" |
    | Extension Management (Basic):Configure allowed extension types | [ExtensionAllowedTypes](/deployedge/microsoft-edge-browser-policies/extensionallowedtypes) | ExtensionAllowedTypes | "extension", "theme" |
    | Extension Management (Basic):Configure extension and user script install sources | [ExtensionInstallSources](/deployedge/microsoft-edge-browser-policies/extensioninstallsources) | ExtensionInstallSources | https://corp.contoso.com/ |
    | Download & File Management:Set download directory | [DefaultDownloadDirectory](/deployedge/microsoft-edge-browser-policies/downloaddirectory) | DefaultDownloadDirectory | $ |
    | Download & File Management:Ask where to save downloaded files | [PromptForDownloadLocation](/deployedge/microsoft-edge-browser-policies/promptfordownloadlocation) | PromptForDownloadLocation | Enabled |
    | Download & File Management:Allow download restrictions | [DownloadRestrictions](/deployedge/microsoft-edge-browser-policies/downloadrestrictions) | DownloadRestrictions | Block malicious downloads and dangerous file types |
    | Feature Controls (Productivity):Show Hubs Sidebar | [HubsSidebarEnabled](/deployedge/microsoft-edge-browser-policies/hubssidebarenabled) | HubsSidebarEnabled | Disabled |
    | Feature Controls (Productivity):Show Microsoft Rewards experiences | [ShowMicrosoftRewards](/deployedge/microsoft-edge-browser-policies/showmicrosoftrewards) | ShowMicrosoftRewards | Disabled |
    | Feature Controls (Productivity):Shopping in Microsoft Edge Enabled | [EdgeShoppingAssistantEnabled](/deployedge/microsoft-edge-browser-policies/edgeshoppingassistantenabled) | EdgeShoppingAssistantEnabled | Disabled |
    | Feature Controls (Productivity):Edge Workspaces | [EdgeWorkspacesEnabled](/deployedge/microsoft-edge-browser-policies/edgeworkspacesenabled) | EdgeWorkspacesEnabled | Enabled |
    | Bookmarks & Favorites Management:Show favorites bar | [FavoritesBarEnabled](/deployedge/microsoft-edge-browser-policies/favoritesbarenabled) | FavoritesBarEnabled | Enabled |
    | Bookmarks & Favorites Management:Enable deleting browser and download history | [AllowDeletingBrowserHistory](/deployedge/microsoft-edge-browser-policies/allowdeletingbrowserhistory) | AllowDeletingBrowserHistory | Enabled |

6. Select **Next**.

7. For **Assignments**, assign to **SEB-Level1-Users** group.

8. Select **Next** and **Create**.

### Level 2 - Enhanced browser configuration (Windows)

1. Follow steps 1-7 from Level 1.

2. On the **Basics** tab:
    - **Name**: Level 2 - Enhanced browser configuration - Windows ACP
    - **Description**: Enhanced browser configuration with other security controls

3. Configure all Level 1 settings PLUS:

    | Setting | Documentation | Key | Value |
    |---------|--------------|-----|-------|
    | Enhanced Security Controls:Force Microsoft Defender SmartScreen checks on downloads from trusted sources | [SmartScreenForTrustedDownloadsEnabled](/deployedge/microsoft-edge-browser-policies/smartscreenfortrusteddownloadsenabled) | SmartScreenForTrustedDownloadsEnabled | Enabled |
    | Enhanced Security Controls:Allow insecure content on specified sites | [InsecureContentAllowedForUrls](/deployedge/microsoft-edge-browser-policies/insecurecontentallowedforurls) | InsecureContentAllowedForUrls | [] |
    | Enhanced Security Controls:Block insecure content on specified sites | [InsecureContentBlockedForUrls](/deployedge/microsoft-edge-browser-policies/insecurecontentblockedforurls) | InsecureContentBlockedForUrls | ["*"] |
    | Advanced Extension Management:Allow specific extensions to be installed | [ExtensionInstallAllowlist](/deployedge/microsoft-edge-browser-policies/extensioninstallallowlist) | ExtensionInstallAllowlist | [] |
    | Advanced Extension Management:Control which extensions are installed silently | [ExtensionInstallForcelist](/deployedge/microsoft-edge-browser-policies/extensioninstallforcelist) | ExtensionInstallForcelist | [] |
    | Advanced Extension Management:Configure extension management settings | [ExtensionSettings](/deployedge/microsoft-edge-browser-policies/extensionsettings) | ExtensionSettings | {"*": {"installation_mode": "blocked"}} |
    | Advanced Extension Management:Control which native messaging hosts users can use | [NativeMessagingHostAllowlist](/deployedge/microsoft-edge-browser-policies/nativemessagingallowlistt) | NativeMessagingHostAllowlist | [] |
    | Advanced Extension Management:Configure native messaging block list | [NativeMessagingHostBlocklist](/deployedge/microsoft-edge-browser-policies/nativemessagingblocklist) | NativeMessagingHostBlocklist | ["*"] |
    | Certificate & Authentication:Automatically select client certificates for these sites | [AutoSelectCertificateForUrls](/deployedge/microsoft-edge-browser-policies/autoselectcertificateforurls) | AutoSelectCertificateForUrls | ["*.company.com"] |
    | Content & Media Controls:Restrict the range of local UDP ports used by WebRTC | [WebRtcUdpPortRange](/deployedge/microsoft-edge-browser-policies/webrtcudpportrange) | WebRtcUdpPortRange | 10000:11000 |
    | Content & Media Controls:Default images setting | [DefaultImagesSetting](/deployedge/microsoft-edge-browser-policies/defaultimagessetting) | DefaultImagesSetting | Allow images (1) |
    | Content & Media Controls:Default JavaScript setting | [DefaultJavaScriptSetting](/deployedge/microsoft-edge-browser-policies/defaultjavascriptsetting) | DefaultJavaScriptSetting | Allow JavaScript (1) |
    | Advanced Privacy Controls:Clear browsing data when Microsoft Edge closes | [ClearBrowsingDataOnExit](/deployedge/microsoft-edge-browser-policies/clearbrowsingdataonexit) | ClearBrowsingDataOnExit | Enabled |
    | Advanced Privacy Controls:Disable synchronization of data using Microsoft sync services | [SyncDisabled](/deployedge/microsoft-edge-browser-policies/syncdisabled) | SyncDisabled | Enabled |
    | Printing & Export Controls:Enable printing | [PrintingEnabled](/deployedge/microsoft-edge-browser-policies/printingenabled) | PrintingEnabled | Enabled |
    | Session & Storage Management:InPrivate mode availability | [InPrivateModeAvailability](/deployedge/microsoft-edge-browser-policies/inprivatemodeavailability) | InPrivateModeAvailability | InPrivate mode available (0) |
    | Session & Storage Management:Force synchronization of browser data and do not show the sync consent prompt | [ForceSync](/deployedge/microsoft-edge-browser-policies/forcesync) | ForceSync | Disabled |
    | Performance & Resource Management:Configure sleeping tabs | [SleepingTabsEnabled](/deployedge/microsoft-edge-browser-policies/sleepingtabsenabled) | SleepingTabsEnabled | Enabled |
    | Address Bar Suggestions Management:Enable search suggestions | [SearchSuggestEnabled](/deployedge/microsoft-edge-browser-policies/searchsuggestenabled) | SearchSuggestEnabled | Disabled |
    | Address Bar Suggestions Management:Allow suggestions from local providers | [LocalProvidersEnabled](/deployedge/microsoft-edge-browser-policies/localprovidersenabled) | LocalProvidersEnabled | Disabled |
    | Media Device Permissions:Allow or block video capture | [VideoCaptureAllowed](/deployedge/microsoft-edge-browser-policies/videocaptureallowed) | VideoCaptureAllowed | Disabled |
    | Notification Controls:Default notification setting | [DefaultNotificationsSetting](/deployedge/microsoft-edge-browser-policies/defaultnotificationssetting) | DefaultNotificationsSetting | Block (2) |
    | Location Services Management:Default geolocation setting | [DefaultGeolocationSetting](/deployedge/microsoft-edge-browser-policies/defaultgeolocationsetting) | DefaultGeolocationSetting | Don't allow sites to track users' physical location (2) |
    | USB/HID Device Controls:Allow WebUSB on specific sites | [UsbAllowDevicesForUrls](/deployedge/microsoft-edge-browser-policies/usballowdevicesforurls) | UsbAllowDevicesForUrls | [] |
    | USB/HID Device Controls:Block WebUSB on specific sites | [UsbBlockDevicesForUrls](/deployedge/microsoft-edge-browser-policies/usbblockdevicesforurls) | UsbBlockDevicesForUrls | [{"urls": ["*"], "devices": [{"vendor_id": "*", "product_id": "*"}]}] |
    | WebRTC Advanced Settings:Restrict exposure of local IP address by WebRTC | [WebRtcLocalhostIpHandling](/deployedge/microsoft-edge-browser-policies/webrtclocalhostiphandling) | WebRtcLocalhostIpHandling | Disable non-proxied UDP (default_public_interface_only) |

4. For **Assignments**, assign to **SEB-Level2-Users** group.

5. Select **Next** and **Create**.

### Level 3 - High security configuration (Windows)

1. Follow steps 1-7 from Level 1.

2. On the **Basics** tab:
    - **Name**: Level 3 - High security configuration - Windows ACP
    - **Description**: Maximum security browser configuration

3. Configure all Level 1 and Level 2 settings PLUS:

::: zone-end

::: zone pivot="android"

## App Configuration Policies for Android

Android app configuration policies customize Microsoft Edge for Business behavior on mobile devices. These policies define browser defaults, restrict risky features, and enforce privacy protections in alignment with enterprise security frameworks.

> **Microsoft Documentation:**
> - [Microsoft Edge Mobile Policies](/deployedge/microsoft-edge-mobile-policies)
> - [Android App Configuration Policies](app-configuration-policies-overview.md)
> - [Managed App Configuration for Android](app-configuration-policies-managed-app.md)

**Prerequisites:**
- Android 10.0+ (8.0+ for userless devices)  
- Microsoft Edge for Android installed  
- Company Portal or Intune app installed  
- Microsoft Intune license assigned to the user  
- Device MAM-enabled or MDM-enrolled through Intune  
- User signed in with Microsoft Entra ID account  

### Level 1 – Basic Mobile Browser Configuration (Android)

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Apps** > **Configuration** > **Create** > **Managed apps**.  
3. On the **Basics** step, in **Target policy to**, select **Selected apps**.  
   - Choose **+ Select public apps**.  
   - In the **Select apps to target** panel, search for and select **Microsoft Edge**.  
   - Choose **Microsoft Edge (Android)**, then **Select**.  
4. Select **Next**.  
5. On the **Settings catalog** step, no options are available for app configuration policies. Select **Next** to continue.  
6. On the **Settings** step, expand **General configuration settings** and **Edge configuration settings** to begin adding configuration values.  
7. Under **General configuration settings**, configure:

| Setting | Documentation | Key | Value |
|----------|---------------|-----|-------|
| Password single sign-on | [PasswordSSO](/deployedge/microsoft-edge-mobile-policies#passwordsso) | com.microsoft.intune.mam.managedbrowser.PasswordSSO | true |
| SmartScreen enabled | [SmartScreenEnabled](/deployedge/microsoft-edge-mobile-policies#smartscreenenabled) | com.microsoft.intune.mam.managedbrowser.SmartScreenEnabled | true |
| Enable EdgeMyApps | [EdgeMyApps](/deployedge/microsoft-edge-mobile-policies#edgemyapps) | EdgeMyApps | true |
| Default HTTPS enforced | [EdgeDefaultHTTPS](/deployedge/microsoft-edge-mobile-policies#edgedefaulthttps) | EdgeDefaultHTTPS | true |
| Disable sharing usage data | [EdgeDisableShareUsageData](/deployedge/microsoft-edge-mobile-policies#edgedisableshareusagedata) | EdgeDisableShareUsageData | true |
| Disable password manager | [PasswordManagerEnabled](/deployedge/microsoft-edge-mobile-policies#passwordmanagerenabled) | PasswordManagerEnabled | false |
| Disable search suggestions | [SearchSuggestEnabled](/deployedge/microsoft-edge-mobile-policies#searchsuggestenabled) | SearchSuggestEnabled | false |
| Hide first run experience | [HideFirstRunExperience](/deployedge/microsoft-edge-mobile-policies#hidefirstrunexperience) | HideFirstRunExperience | true |
| Disable popups | [DefaultPopupsSetting](/deployedge/microsoft-edge-mobile-policies#defaultpopupssetting) | DefaultPopupsSetting | 2 |

8. Under **Edge configuration settings**:
   - **Homepage shortcut URL:** https://www.company.com  
   - **Managed bookmarks:** Company Portal\|https://portal.company.com  

9. **Assignments:** Assign to **SEB-Level1-Users** group.  
10. **Select Next** and **Create**.

**Framework Compliance (Level 1):** Meets NIST basic controls for mobile data protection with essential privacy and browser safety settings.

### Level 2 – Enhanced Mobile Browser Configuration (Android)

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Apps** > **Configuration** > **Create** > **Managed apps**.  
3. On the **Basics** step, in **Target policy to**, select **Selected apps**.  
   - Choose **+ Select public apps**.  
   - In the **Select apps to target** panel, search for and select **Microsoft Edge**.  
   - Choose **Microsoft Edge (Android)**, then **Select**.  
4. Select **Next**.  
5. On the **Settings catalog** step, no options are available for app configuration policies. Select **Next** to continue.  
6. On the **Settings** step, expand **General configuration settings** and **Edge configuration settings** to begin adding configuration values.  
7. Under **General configuration settings**, configure the following settings:

| Setting | Documentation | Key | Value |
|----------|---------------|-----|-------|
| Password single sign-on | [PasswordSSO](/deployedge/microsoft-edge-mobile-policies#passwordsso) | com.microsoft.intune.mam.managedbrowser.PasswordSSO | true |
| SmartScreen enabled | [SmartScreenEnabled](/deployedge/microsoft-edge-mobile-policies#smartscreenenabled) | com.microsoft.intune.mam.managedbrowser.SmartScreenEnabled | true |
| Enable EdgeMyApps | [EdgeMyApps](/deployedge/microsoft-edge-mobile-policies#edgemyapps) | EdgeMyApps | true |
| Default HTTPS enforced | [EdgeDefaultHTTPS](/deployedge/microsoft-edge-mobile-policies#edgedefaulthttps) | EdgeDefaultHTTPS | true |
| Disable sharing usage data | [EdgeDisableShareUsageData](/deployedge/microsoft-edge-mobile-policies#edgedisableshareusagedata) | EdgeDisableShareUsageData | true |
| Disable password manager | [PasswordManagerEnabled](/deployedge/microsoft-edge-mobile-policies#passwordmanagerenabled) | PasswordManagerEnabled | false |
| Disable search suggestions | [SearchSuggestEnabled](/deployedge/microsoft-edge-mobile-policies#searchsuggestenabled) | SearchSuggestEnabled | false |
| Hide first run experience | [HideFirstRunExperience](/deployedge/microsoft-edge-mobile-policies#hidefirstrunexperience) | HideFirstRunExperience | true |
| Disable popups | [DefaultPopupsSetting](/deployedge/microsoft-edge-mobile-policies#defaultpopupssetting) | DefaultPopupsSetting | 2 |
| Disable sync | [EdgeSyncDisabled](/deployedge/microsoft-edge-mobile-policies#edgesyncdisabled) | EdgeSyncDisabled | true |
| Disable password import | [EdgeImportPasswordsDisabled](/deployedge/microsoft-edge-mobile-policies#edgeimportpasswordsdisabled) | EdgeImportPasswordsDisabled | true |
| Disable features | [EdgeDisabledFeatures](/deployedge/microsoft-edge-mobile-policies#edgedisabledfeatures) | EdgeDisabledFeatures | "password\|autofill\|copilot\|collections" |
| Disable SSL error override | [SSLErrorOverrideAllowed](/deployedge/microsoft-edge-mobile-policies#sslerroroverrideallowed) | SSLErrorOverrideAllowed | false |

8. Under **Edge configuration settings**:
   - **Homepage shortcut URL:** https://www.company.com  
   - **Managed bookmarks:** Company Portal\|https://portal.company.com  
   - **Blocked URLs:** *.facebook.com, *.twitter.com, *.instagram.com, *.tiktok.com  
   - **Redirect restricted sites to personal context:** Enable  

9. **Assignments:** Assign to **SEB-Level2-Users** group.  
10. **Select Next** and **Create**.

**Framework Compliance (Level 2):** Meets DISA STIG CAT II and CISA enhanced privacy requirements; expands coverage to include blocked URLs, disabled sync, and controlled web behavior.

### Level 3 – High Security Mobile Configuration (Android)

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Apps** > **Configuration** > **Create** > **Managed apps**.  
3. On the **Basics** step, in **Target policy to**, select **Selected apps**.  
   - Choose **+ Select public apps**.  
   - In the **Select apps to target** panel, search for and select **Microsoft Edge**.  
   - Choose **Microsoft Edge (Android)**, then **Select**.  
4. Select **Next**.  
5. On the **Settings catalog** step, no options are available for app configuration policies. Select **Next** to continue.  
6. On the **Settings** step, expand **General configuration settings** and **Edge configuration settings** to begin adding configuration values.  
7. Under **General configuration settings**, configure the following settings:

| Setting | Documentation | Key | Value |
|----------|---------------|-----|-------|
| Password single sign-on | [PasswordSSO](/deployedge/microsoft-edge-mobile-policies#passwordsso) | com.microsoft.intune.mam.managedbrowser.PasswordSSO | true |
| SmartScreen enabled | [SmartScreenEnabled](/deployedge/microsoft-edge-mobile-policies#smartscreenenabled) | com.microsoft.intune.mam.managedbrowser.SmartScreenEnabled | true |
| Enable EdgeMyApps | [EdgeMyApps](/deployedge/microsoft-edge-mobile-policies#edgemyapps) | EdgeMyApps | false |
| Default HTTPS enforced | [EdgeDefaultHTTPS](/deployedge/microsoft-edge-mobile-policies#edgedefaulthttps) | EdgeDefaultHTTPS | true |
| Disable sharing usage data | [EdgeDisableShareUsageData](/deployedge/microsoft-edge-mobile-policies#edgedisableshareusagedata) | EdgeDisableShareUsageData | true |
| Disable password manager | [PasswordManagerEnabled](/deployedge/microsoft-edge-mobile-policies#passwordmanagerenabled) | PasswordManagerEnabled | false |
| Disable search suggestions | [SearchSuggestEnabled](/deployedge/microsoft-edge-mobile-policies#searchsuggestenabled) | SearchSuggestEnabled | false |
| Hide first run experience | [HideFirstRunExperience](/deployedge/microsoft-edge-mobile-policies#hidefirstrunexperience) | HideFirstRunExperience | true |
| Disable popups | [DefaultPopupsSetting](/deployedge/microsoft-edge-mobile-policies#defaultpopupssetting) | DefaultPopupsSetting | 2 |
| Disable sync | [EdgeSyncDisabled](/deployedge/microsoft-edge-mobile-policies#edgesyncdisabled) | EdgeSyncDisabled | true |
| Disable password import | [EdgeImportPasswordsDisabled](/deployedge/microsoft-edge-mobile-policies#edgeimportpasswordsdisabled) | EdgeImportPasswordsDisabled | true |
| Disable features | [EdgeDisabledFeatures](/deployedge/microsoft-edge-mobile-policies#edgedisabledfeatures) | EdgeDisabledFeatures | "inprivate\|autofill\|password\|translator\|copilot\|collections\|readaloud\|drop" |
| Disable SSL error override | [SSLErrorOverrideAllowed](/deployedge/microsoft-edge-mobile-policies#sslerroroverrideallowed) | SSLErrorOverrideAllowed | false |
| Disable InPrivate mode | [InPrivateModeAvailability](/deployedge/microsoft-edge-browser-policies/inprivatemodeavailability) | InPrivateModeAvailability | 1 |
| Disable browser history saving | [SavingBrowserHistoryDisabled](/deployedge/microsoft-edge-mobile-policies#savingbrowserhistorydisabled) | SavingBrowserHistoryDisabled | true |
| Block Edge sign-in | [EdgeBlockSignInEnabled](/deployedge/microsoft-edge-mobile-policies#edgeblocksigninenabled) | EdgeBlockSignInEnabled | true |
| Disable shared device support | [EdgeSharedDeviceSupportEnabled](/deployedge/microsoft-edge-mobile-policies#edgeshareddevicesupportenabled) | EdgeSharedDeviceSupportEnabled | false |
| Disable Copilot | [EdgeCopilotEnabled](/deployedge/microsoft-edge-mobile-policies#edgecopilotenabled) | EdgeCopilotEnabled | false |

8. Under **Edge configuration settings**:
   - **Homepage shortcut URL:** https://www.company.com  
   - **Managed bookmarks:** Company Portal\|https://portal.company.com  
   - **Allowed URLs:** *.company.com, *.microsoft.com, login.microsoftonline.com  
   - *(When Allowed URLs are configured, the Blocked URLs field becomes unavailable.)*  
   - **Proxy configuration (optional):**  
     ```
     ProxySettings: {"ProxyServer": "proxy.company.com:8080", "ProxyBypassList": "*.company.com", "ProxyMode": "fixed_servers"}
     ```  
   - **Per-App VPN (optional):** Integrate with Microsoft Tunnel if required for isolated secure traffic routing.  

9. **Assignments:** Assign to **SEB-Level3-Users** group.  
10. **Select Next** and **Create**.

**Framework Compliance (Level 3):** Meets DISA STIG CAT I and CISA Critical Controls for Android — enforces strict isolation, URL allowlist-only navigation, and feature lockdown with enhanced network protection and optional VPN integration.

### Validation (All Levels)

- **Policy application:** Verify in Intune under **Monitor > Device configuration** that the ACP shows *Succeeded*.  
- **On device:** Open Edge > **Settings** > confirm homepage, privacy restrictions, and URL enforcement.  
- **Blocked content:** Attempt to open restricted sites (e.g., facebook.com) on Level 2/3 — ensure redirection or blocking.  
- **Zero-trust enforcement:** Verify InPrivate, Autofill, Copilot, and password features are disabled under Level 3.  
- **Security confirmation:** Run `edge://policy` (in desktop simulation or Android enterprise debug build) to confirm policy key deployment.

**Result:** Android ACPs deliver a progressive Zero Trust enforcement model—basic data protection at Level 1, enhanced DLP and content filtering at Level 2, and full isolation with framework compliance at Level 3.

::: zone-end

::: zone pivot="ios-ipados"

## App Configuration Policies for iOS/iPadOS

iOS app configuration policies define and enforce browser behavior for Microsoft Edge for Business on iPhone and iPad devices. These policies provide progressive control over privacy, security, and data protection while aligning with Zero Trust principles.

> **Microsoft Documentation:**
> - [Microsoft Edge Mobile Policies](/deployedge/microsoft-edge-mobile-policies)
> - [iOS App Configuration Policies](app-configuration-policies-overview.md)
> - [Managed App Configuration for iOS](app-configuration-policies-managed-app.md)

**Prerequisites:**
- iOS/iPadOS 17+  
- Microsoft Edge for iOS installed  
- Company Portal or Intune app installed  
- Microsoft Intune license assigned to the user  
- Device MAM-enabled or MDM-enrolled through Intune  
- User signed in with Microsoft Entra ID account  

> [!IMPORTANT]
> In iOS App Configuration Policies, **Allowed URLs** and **Blocked URLs** are mutually exclusive. When you configure one, the other becomes unavailable.

### Level 1 – Basic mobile browser configuration (iOS)

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Apps** > **Configuration** > **Create** > **Managed apps**.  
3. On the **Basics** tab:  
   - **Name:** Level 1 – Basic mobile browser configuration – iOS ACP  
   - **Description:** Basic browser configuration for Microsoft Edge on iOS.  
4. In **Target policy to**, select **Selected apps**.  
   - Choose **+ Select public apps**.  
   - In the **Select apps to target** panel, search for and select **Microsoft Edge**.  
   - Choose **Microsoft Edge (iOS/iPadOS)**, then **Select**.  
5. Select **Next**.  
6. On the **Settings catalog** step, no options are available for app configuration policies. Select **Next** to continue.  
7. On the **Settings** step, expand **General configuration settings** and **Edge configuration settings** to begin adding configuration values. Configure the following settings.

#### General configuration settings

| Setting | Documentation | Key | Value |
|----------|----------------|-----|-------|
| Password single sign-on | [PasswordSSO](/deployedge/microsoft-edge-mobile-policies#passwordsso) | com.microsoft.intune.mam.managedbrowser.PasswordSSO | true |
| SmartScreen enabled | [SmartScreenEnabled](/deployedge/microsoft-edge-mobile-policies#smartscreenenabled) | com.microsoft.intune.mam.managedbrowser.SmartScreenEnabled | true |
| Enable EdgeMyApps | [EdgeMyApps](/deployedge/microsoft-edge-mobile-policies#edgemyapps) | EdgeMyApps | true |
| Default HTTPS enforced | [EdgeDefaultHTTPS](/deployedge/microsoft-edge-mobile-policies#edgedefaulthttps) | EdgeDefaultHTTPS | true |
| Disable sharing usage data | [EdgeDisableShareUsageData](/deployedge/microsoft-edge-mobile-policies#edgedisableshareusagedata) | EdgeDisableShareUsageData | true |
| Disable password import | [EdgeImportPasswordsDisabled](/deployedge/microsoft-edge-mobile-policies#edgeimportpasswordsdisabled) | EdgeImportPasswordsDisabled | false |
| Disable password manager | [PasswordManagerEnabled](/deployedge/microsoft-edge-mobile-policies#passwordmanagerenabled) | PasswordManagerEnabled | false |
| Disable search suggestions | [SearchSuggestEnabled](/deployedge/microsoft-edge-mobile-policies#searchsuggestenabled) | SearchSuggestEnabled | false |
| Hide first run experience | [HideFirstRunExperience](/deployedge/microsoft-edge-mobile-policies#hidefirstrunexperience) | HideFirstRunExperience | true |
| Disable pop-ups | [DefaultPopupsSetting](/deployedge/microsoft-edge-mobile-policies#defaultpopupssetting) | DefaultPopupsSetting | 2 |
| Translate enabled | [TranslateEnabled](/deployedge/microsoft-edge-mobile-policies#translateenabled) | TranslateEnabled | true |
| SSL error override allowed | [SSLErrorOverrideAllowed](/deployedge/microsoft-edge-mobile-policies#sslerroroverrideallowed) | SSLErrorOverrideAllowed | true |
| Default browser setting enabled | [DefaultBrowserSettingEnabled](/deployedge/microsoft-edge-mobile-policies#defaultbrowsersettingenabled) | DefaultBrowserSettingEnabled | true |
| Organizational branding – logo | [EdgeBrandLogo](/deployedge/microsoft-edge-mobile-policies#edgebrandlogo) | EdgeBrandLogo | true |
| Organizational branding – color | [EdgeBrandColor](/deployedge/microsoft-edge-mobile-policies#edgebrandcolor) | EdgeBrandColor | #0078d4 |
| Default search provider enabled | [DefaultSearchProviderEnabled](/deployedge/microsoft-edge-mobile-policies#defaultsearchproviderenabled) | DefaultSearchProviderEnabled | true |
| Default search provider name | [DefaultSearchProviderName](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidername) | DefaultSearchProviderName | "Preferred Company Search" |
| Default search provider search URL | [DefaultSearchProviderSearchURL](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidersearchurl) | DefaultSearchProviderSearchURL | "https://search.company.com?q={searchTerms}" |
| Default search provider suggest URL | [DefaultSearchProviderSuggestURL](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidersuggesturl) | DefaultSearchProviderSuggestURL | "https://search.company.com/suggest?q={searchTerms}" |
| Default search keyword | [DefaultSearchProviderKeyword](/deployedge/microsoft-edge-mobile-policies#defaultsearchproviderkeyword) | DefaultSearchProviderKeyword | "company" |

#### Edge configuration settings

| Setting | Documentation | Key | Value |
|----------|----------------|-----|-------|
| Application proxy redirection | — | — | Disable |
| Homepage shortcut URL | — | — | https://www.company.com |
| Managed bookmarks | — | — | Company Portal \| https://portal.company.com |
| Allowed URLs | — | — | Leave empty (Level 3 uses Allowed URLs) |
| Blocked URLs | — | — | Leave empty (Level 2 uses Blocked URLs) |
| Redirect restricted sites to personal context | — | — | Disable |

8. Select **Next**.  
9. For **Assignments**, assign to **SEB-Level1-Users** group.  
10. Select **Next** and **Create**.  

> **Validation (iOS Level 1)**  
> - **Policy application:** Verify in Intune that the ACP status shows *Succeeded*.  
> - **Device behavior:** Open Edge > **Settings** and confirm homepage and basic privacy settings are applied.  
> - **Policy verification:** Run `edge://policy` (in desktop simulation or debug build) to confirm key deployment.


### Level 2 – Enhanced mobile browser configuration (iOS)

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Apps** > **Configuration** > **Create** > **Managed apps**.  
3. On the **Basics** tab:  
   - **Name:** Level 2 – Enhanced mobile browser configuration – iOS ACP  
   - **Description:** Enhanced browser configuration with security controls for Microsoft Edge on iOS.  
4. In **Target policy to**, select **Selected apps**.  
   - Choose **+ Select public apps**.  
   - In the **Select apps to target** panel, search for and select **Microsoft Edge**.  
   - Choose **Microsoft Edge (iOS/iPadOS)**, then **Select**.  
5. Select **Next**.  
6. On the **Settings catalog** step, no options are available for app configuration policies. Select **Next** to continue.  
7. On the **Settings** step, expand **General configuration settings** and **Edge configuration settings** to begin adding configuration values. Configure all of the following settings:

#### General configuration settings

| Setting | Documentation | Key | Value |
|----------|----------------|-----|-------|
| Password single sign-on | [PasswordSSO](/deployedge/microsoft-edge-mobile-policies#passwordsso) | com.microsoft.intune.mam.managedbrowser.PasswordSSO | true |
| SmartScreen enabled | [SmartScreenEnabled](/deployedge/microsoft-edge-mobile-policies#smartscreenenabled) | com.microsoft.intune.mam.managedbrowser.SmartScreenEnabled | true |
| Enable EdgeMyApps | [EdgeMyApps](/deployedge/microsoft-edge-mobile-policies#edgemyapps) | EdgeMyApps | true |
| Default HTTPS enforced | [EdgeDefaultHTTPS](/deployedge/microsoft-edge-mobile-policies#edgedefaulthttps) | EdgeDefaultHTTPS | true |
| Disable sharing usage data | [EdgeDisableShareUsageData](/deployedge/microsoft-edge-mobile-policies#edgedisableshareusagedata) | EdgeDisableShareUsageData | true |
| Disable password manager | [PasswordManagerEnabled](/deployedge/microsoft-edge-mobile-policies#passwordmanagerenabled) | PasswordManagerEnabled | false |
| Disable search suggestions | [SearchSuggestEnabled](/deployedge/microsoft-edge-mobile-policies#searchsuggestenabled) | SearchSuggestEnabled | false |
| Hide first run experience | [HideFirstRunExperience](/deployedge/microsoft-edge-mobile-policies#hidefirstrunexperience) | HideFirstRunExperience | true |
| Disable pop-ups | [DefaultPopupsSetting](/deployedge/microsoft-edge-mobile-policies#defaultpopupssetting) | DefaultPopupsSetting | 2 |
| Disable sync | [EdgeSyncDisabled](/deployedge/microsoft-edge-mobile-policies#edgesyncdisabled) | EdgeSyncDisabled | true |
| Disable password import | [EdgeImportPasswordsDisabled](/deployedge/microsoft-edge-mobile-policies#edgeimportpasswordsdisabled) | EdgeImportPasswordsDisabled | true |
| Disable features | [EdgeDisabledFeatures](/deployedge/microsoft-edge-mobile-policies#edgedisabledfeatures) | EdgeDisabledFeatures | "password|autofill|copilot|collections|readaloud" |
| Disable SSL error override | [SSLErrorOverrideAllowed](/deployedge/microsoft-edge-mobile-policies#sslerroroverrideallowed) | SSLErrorOverrideAllowed | false |
| Biometric authentication before filling | [BiometricAuthenticationBeforeFilling](/deployedge/microsoft-edge-browser-policies/biometricauthenticationbeforefilling) | BiometricAuthenticationBeforeFilling | true |
| Experimentation and configuration service control | [ExperimentationAndConfigurationServiceControl](/deployedge/microsoft-edge-mobile-policies#experimentationandconfigurationservicecontrol) | ExperimentationAndConfigurationServiceControl | 0 |
| Default browser setting enabled | [DefaultBrowserSettingEnabled](/deployedge/microsoft-edge-mobile-policies#defaultbrowsersettingenabled) | DefaultBrowserSettingEnabled | false |
| Organizational branding – logo | [EdgeBrandLogo](/deployedge/microsoft-edge-mobile-policies#edgebrandlogo) | EdgeBrandLogo | true |
| Default search provider enabled | [DefaultSearchProviderEnabled](/deployedge/microsoft-edge-mobile-policies#defaultsearchproviderenabled) | DefaultSearchProviderEnabled | true |
| Default search provider name | [DefaultSearchProviderName](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidername) | DefaultSearchProviderName | "Preferred Company Search" |
| Default search provider search URL | [DefaultSearchProviderSearchURL](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidersearchurl) | DefaultSearchProviderSearchURL | "https://search.company.com?q={searchTerms}" |

#### Edge configuration settings

| Setting | Documentation | Key | Value |
|----------|----------------|-----|-------|
| Allowed URLs | — | — | (Leave empty – Level 3 uses Allowed URLs instead.) |
| Blocked URLs | — | — | *.facebook.com, *.twitter.com, *.instagram.com, *.tiktok.com |
| Redirect restricted sites to personal context | — | — | Enable |

8. Select **Next**.  
9. For **Assignments**, assign to **SEB-Level2-Users** group.  
10. Select **Next** and **Create**.  

> **Validation (iOS Level 2)**  
> - **Policy application:** Verify in Intune that the ACP status shows *Succeeded*.  
> - **Device behavior:** Open Edge > **Settings** and confirm privacy and blocked URL behavior are applied.  
> - **Blocked content:** Attempt to open restricted sites (e.g., facebook.com) and verify they’re blocked or redirected.  
> - **Policy verification:** Run `edge://policy` (in desktop simulation or debug build) to confirm key deployment.

### Level 3 – High security mobile configuration (iOS)

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Apps** > **Configuration** > **Create** > **Managed apps**.  
3. On the **Basics** tab:  
   - **Name:** Level 3 – High security mobile configuration – iOS ACP  
   - **Description:** Maximum security browser configuration  
4. In **Target policy to**, select **Selected apps**.  
5. Choose **+ Select public apps**.  
6. In the **Select apps to target** panel, search for and select **Microsoft Edge (iOS/iPadOS)**, then choose **Select**.  
7. Select **Next**.  
8. On the **Settings catalog** step, no options are available for app configuration policies. Select **Next** to continue.  
9. On the **Settings** step, expand **General configuration settings** and **Edge configuration settings** to begin adding configuration values. Configure all of the following (Level 1 + Level 2 + Level 3 settings combined).

#### General configuration settings

| Setting | Documentation | Key | Value |
|----------|----------------|-----|-------|
| Password single sign-on | [PasswordSSO](/deployedge/microsoft-edge-mobile-policies#passwordsso) | com.microsoft.intune.mam.managedbrowser.PasswordSSO | true |
| SmartScreen enabled | [SmartScreenEnabled](/deployedge/microsoft-edge-mobile-policies#smartscreenenabled) | com.microsoft.intune.mam.managedbrowser.SmartScreenEnabled | true |
| Enable EdgeMyApps | [EdgeMyApps](/deployedge/microsoft-edge-mobile-policies#edgemyapps) | EdgeMyApps | false |
| Default HTTPS enforced | [EdgeDefaultHTTPS](/deployedge/microsoft-edge-mobile-policies#edgedefaulthttps) | EdgeDefaultHTTPS | true |
| Disable sharing usage data | [EdgeDisableShareUsageData](/deployedge/microsoft-edge-mobile-policies#edgedisableshareusagedata) | EdgeDisableShareUsageData | true |
| Disable password manager | [PasswordManagerEnabled](/deployedge/microsoft-edge-mobile-policies#passwordmanagerenabled) | PasswordManagerEnabled | false |
| Disable search suggestions | [SearchSuggestEnabled](/deployedge/microsoft-edge-mobile-policies#searchsuggestenabled) | SearchSuggestEnabled | false |
| Hide first run experience | [HideFirstRunExperience](/deployedge/microsoft-edge-mobile-policies#hidefirstrunexperience) | HideFirstRunExperience | true |
| Disable pop-ups | [DefaultPopupsSetting](/deployedge/microsoft-edge-mobile-policies#defaultpopupssetting) | DefaultPopupsSetting | 2 |
| Disable sync | [EdgeSyncDisabled](/deployedge/microsoft-edge-mobile-policies#edgesyncdisabled) | EdgeSyncDisabled | true |
| Disable password import | [EdgeImportPasswordsDisabled](/deployedge/microsoft-edge-mobile-policies#edgeimportpasswordsdisabled) | EdgeImportPasswordsDisabled | true |
| Disable features | [EdgeDisabledFeatures](/deployedge/microsoft-edge-mobile-policies#edgedisabledfeatures) | EdgeDisabledFeatures | "inprivate|autofill|password|translator|copilot|share|collections|readaloud|drop" |
| Disable SSL error override | [SSLErrorOverrideAllowed](/deployedge/microsoft-edge-mobile-policies#sslerroroverrideallowed) | SSLErrorOverrideAllowed | false |
| Disable InPrivate mode | [InPrivateModeAvailability](/deployedge/microsoft-edge-mobile-policies#inprivatemodeavailability) | InPrivateModeAvailability | 1 |
| Disable browser history saving | [SavingBrowserHistoryDisabled](/deployedge/microsoft-edge-mobile-policies#savingbrowserhistorydisabled) | SavingBrowserHistoryDisabled | true |
| Block Edge sign-in | [EdgeBlockSignInEnabled](/deployedge/microsoft-edge-mobile-policies#edgeblocksigninenabled) | EdgeBlockSignInEnabled | true |
| Disable shared device support | [EdgeSharedDeviceSupportEnabled](/deployedge/microsoft-edge-mobile-policies#edgeshareddevicesupportenabled) | EdgeSharedDeviceSupportEnabled | false |
| Disable Copilot | [EdgeCopilotEnabled](/deployedge/microsoft-edge-mobile-policies#edgecopilotenabled) | EdgeCopilotEnabled | false |
| Translate enabled | [TranslateEnabled](/deployedge/microsoft-edge-mobile-policies#translateenabled) | TranslateEnabled | false |
| Biometric authentication before filling | [BiometricAuthenticationBeforeFilling](/deployedge/microsoft-edge-browser-policies/biometricauthenticationbeforefilling) | BiometricAuthenticationBeforeFilling | true |
| Experimentation and configuration service control | [ExperimentationAndConfigurationServiceControl](/deployedge/microsoft-edge-mobile-policies#experimentationandconfigurationservicecontrol) | ExperimentationAndConfigurationServiceControl | 0 |
| Default browser setting enabled | [DefaultBrowserSettingEnabled](/deployedge/microsoft-edge-mobile-policies#defaultbrowsersettingenabled) | DefaultBrowserSettingEnabled | false |
| Organizational branding – logo | [EdgeBrandLogo](/deployedge/microsoft-edge-mobile-policies#edgebrandlogo) | EdgeBrandLogo | true |
| Organizational branding – color | [EdgeBrandColor](/deployedge/microsoft-edge-mobile-policies#edgebrandcolor) | EdgeBrandColor | #0078d4 |
| Default search provider enabled | [DefaultSearchProviderEnabled](/deployedge/microsoft-edge-mobile-policies#defaultsearchproviderenabled) | DefaultSearchProviderEnabled | true |
| Default search provider name | [DefaultSearchProviderName](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidername) | DefaultSearchProviderName | "Preferred Company Search" |
| Default search provider search URL | [DefaultSearchProviderSearchURL](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidersearchurl) | DefaultSearchProviderSearchURL | "https://search.company.com?q={searchTerms}" |
| Default search provider suggest URL | [DefaultSearchProviderSuggestURL](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidersuggesturl) | DefaultSearchProviderSuggestURL | "https://search.company.com/suggest?q={searchTerms}" |
| Default search keyword | [DefaultSearchProviderKeyword](/deployedge/microsoft-edge-mobile-policies#defaultsearchproviderkeyword) | DefaultSearchProviderKeyword | "company" |

#### Edge configuration settings

| Setting | Documentation | Key | Value |
|----------|----------------|-----|-------|
| Application proxy redirection | — | — | Disable |
| Homepage shortcut URL | — | — | https://www.company.com |
| Managed bookmarks | — | — | Company Portal \| https://portal.company.com |
| Allowed URLs | — | — | *.company.com, *.microsoft.com, login.microsoftonline.com |
| Blocked URLs | — | — | (When Allowed URLs are configured, the Blocked URLs field becomes unavailable.) |
| Redirect restricted sites to personal context | — | — | Enable |
| Proxy configuration (optional) | — | ProxySettings | {"ProxyServer":"proxy.company.com:8080","ProxyBypassList":"*.company.com","ProxyMode":"fixed_servers"} |
| Per-App VPN (optional) | — | — | Integrate with Microsoft Tunnel if required for isolated secure traffic routing |

10. Select **Next**.  
11. For **Assignments**, assign to **SEB-Level3-Users** group.  
12. Select **Next** and **Create**.  

> **Validation (iOS Level 3)**  
> - **Policy application:** Verify in Intune that the ACP status shows *Succeeded*.  
> - **Device behavior:** Open Edge > **Settings** and confirm homepage, privacy restrictions, and URL enforcement are applied.  
> - **Blocked content:** Attempt to open restricted sites (for example, facebook.com) and verify they’re blocked or redirected.  
> - **Zero-trust enforcement:** Confirm InPrivate, Autofill, Copilot, and password features are disabled.  
> - **Policy verification:** Run `edge://policy` (in desktop simulation or debug build) to confirm key deployment.

::: zone-end

## Validation

After deploying app configuration policies:

1. **Policy Application**: Check Intune console for successful ACP deployment
2. **Browser Behavior**: Verify configured homepage, blocked features, and URL restrictions
3. **User Experience**: Test browsing functionality and confirm policy enforcement
4. **Mobile Testing**: On mobile devices, verify Microsoft Edge > Menu > Settings reflects corporate policies

## Next steps

Continue to [Step 5](mamedge-5-settings-catalog.md) to configure Settings Catalog policies for enrolled Windows and macOS devices.
