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
---

# Step 4: App Configuration Policies for Microsoft Edge for Business

App configuration policies allow you to customize browser behavior and features for Microsoft Edge across all platforms. These policies work with app protection policies to provide comprehensive browser management.

**Applies to:**
- Windows 11
- Android 10.0+ (8.0+ for userless management devices)
- iOS/iPadOS 17.x+

> [!NOTE]
> App configuration policies customize browser features and behavior. They complement app protection policies that focus on data protection.

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
    | Core Browser Behavior (Enterprise Foundation):Configure the home page URL | [HomepageLocation](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/homepagelocation) | HomepageLocation | https://portal.company.com |
    | Core Browser Behavior (Enterprise Foundation):Show Home button on toolbar | [ShowHomeButton](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/showhomebutton) | ShowHomeButton | Enabled |
    | Core Browser Behavior (Enterprise Foundation):Configure the new tab page URL | [NewTabPageLocation](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/newtabpageurl) | NewTabPageLocation | https://portal.company.com |
    | Core Browser Behavior (Enterprise Foundation):Action to take on startup | [RestoreOnStartup](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/restoreonstartup) | RestoreOnStartup | Open the new tab page (5) |
    | Content & Security Controls:Configure Automatic HTTPS | [HTTPSOnlyMode](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/httpsonlymode) | HTTPSOnlyMode | Enabled |
    | Content & Security Controls:Default pop-up window setting | [DefaultPopupsSetting](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/defaultpopupssetting) | DefaultPopupsSetting | Do not allow popups (2) |
    | Privacy & Data Management:Enable saving passwords to the password manager | [PasswordManagerEnabled](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/passwordmanagerenabled) | PasswordManagerEnabled | Disabled |
    | Privacy & Data Management:Enable AutoFill for addresses | [AutofillAddressEnabled](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/autofilladdressenabled) | AutofillAddressEnabled | Disabled |
    | Privacy & Data Management:Enable Autofill for payment instructions | [AutofillCreditCardEnabled](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/autofillcreditcardenabled) | AutofillCreditCardEnabled | Disabled |
    | Privacy & Data Management:Block tracking of users' web-browsing activity | [TrackingPrevention](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/trackingprevention) | TrackingPrevention | Balanced (2) |
    | Search & Navigation Enhancement:Enable the default search provider | [DefaultSearchProviderEnabled](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/defaultsearchproviderenabled) | DefaultSearchProviderEnabled | Enabled |
    | Search & Navigation Enhancement:Default search provider name | [DefaultSearchProviderName](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/defaultsearchprovidername) | DefaultSearchProviderName | Microsoft Bing |
    | Search & Navigation Enhancement:Default search provider search URL | [DefaultSearchProviderSearchURL](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/defaultsearchprovidersearchurl) | DefaultSearchProviderSearchURL | https://www.bing.com/search?q |
    | Search & Navigation Enhancement:Enable search suggestions | [SearchSuggestEnabled](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/searchsuggestenabled) | SearchSuggestEnabled | Disabled |
    | Search & Navigation Enhancement:Enable network prediction | [NetworkPredictionOptions](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/networkpredictionoptions) | NetworkPredictionOptions | Don't predict (2) |
    | Import Controls (Data Boundary):Allow importing of autofill form data | [ImportAutofillFormData](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/importautofillformdata) | ImportAutofillFormData | Disabled |
    | Import Controls (Data Boundary):Allow importing of saved passwords | [ImportSavedPasswords](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/importsavedpasswords) | ImportSavedPasswords | Disabled |
    | Import Controls (Data Boundary):Allow importing of browsing history | [ImportBrowsingHistory](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/importhistory) | ImportBrowsingHistory | Disabled |
    | Import Controls (Data Boundary):Allow importing cookies | [ImportCookies](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/importcookies) | ImportCookies | Disabled |
    | Import Controls (Data Boundary):Allow importing of extension | [ImportExtensions](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/importextensions) | ImportExtensions | Disabled |
    | Extension Management (Basic):Control which extensions cannot be installed | [ExtensionInstallBlocklist](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/extensioninstallblocklist) | ExtensionInstallBlocklist | "external_component", "external_pref", "external_registry" |
    | Extension Management (Basic):Configure allowed extension types | [ExtensionAllowedTypes](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/extensionallowedtypes) | ExtensionAllowedTypes | "extension", "theme" |
    | Extension Management (Basic):Configure extension and user script install sources | [ExtensionInstallSources](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/extensioninstallsources) | ExtensionInstallSources | https://corp.contoso.com/ |
    | Download & File Management:Set download directory | [DefaultDownloadDirectory](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/downloaddirectory) | DefaultDownloadDirectory | $ |
    | Download & File Management:Ask where to save downloaded files | [PromptForDownloadLocation](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/promptfordownloadlocation) | PromptForDownloadLocation | Enabled |
    | Download & File Management:Allow download restrictions | [DownloadRestrictions](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/downloadrestrictions) | DownloadRestrictions | Block malicious downloads and dangerous file types |
    | Feature Controls (Productivity):Show Hubs Sidebar | [HubsSidebarEnabled](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/hubssidebarenabled) | HubsSidebarEnabled | Disabled |
    | Feature Controls (Productivity):Show Microsoft Rewards experiences | [ShowMicrosoftRewards](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/showmicrosoftrewards) | ShowMicrosoftRewards | Disabled |
    | Feature Controls (Productivity):Shopping in Microsoft Edge Enabled | [EdgeShoppingAssistantEnabled](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/edgeshoppingassistantenabled) | EdgeShoppingAssistantEnabled | Disabled |
    | Feature Controls (Productivity):Edge Workspaces | [EdgeWorkspacesEnabled](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/edgeworkspacesenabled) | EdgeWorkspacesEnabled | Enabled |
    | Bookmarks & Favorites Management:Show favorites bar | [FavoritesBarEnabled](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/favoritesbarenabled) | FavoritesBarEnabled | Enabled |
    | Bookmarks & Favorites Management:Enable deleting browser and download history | [AllowDeletingBrowserHistory](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/allowdeletingbrowserhistory) | AllowDeletingBrowserHistory | Enabled |

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
    | Enhanced Security Controls:Force Microsoft Defender SmartScreen checks on downloads from trusted sources | [SmartScreenForTrustedDownloadsEnabled](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/smartscreenfortrusteddownloadsenabled) | SmartScreenForTrustedDownloadsEnabled | Enabled |
    | Enhanced Security Controls:Allow insecure content on specified sites | [InsecureContentAllowedForUrls](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/insecurecontentallowedforurls) | InsecureContentAllowedForUrls | [] |
    | Enhanced Security Controls:Block insecure content on specified sites | [InsecureContentBlockedForUrls](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/insecurecontentblockedforurls) | InsecureContentBlockedForUrls | ["*"] |
    | Advanced Extension Management:Allow specific extensions to be installed | [ExtensionInstallAllowlist](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/extensioninstallallowlist) | ExtensionInstallAllowlist | [] |
    | Advanced Extension Management:Control which extensions are installed silently | [ExtensionInstallForcelist](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/extensioninstallforcelist) | ExtensionInstallForcelist | [] |
    | Advanced Extension Management:Configure extension management settings | [ExtensionSettings](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/extensionsettings) | ExtensionSettings | {"*": {"installation_mode": "blocked"}} |
    | Advanced Extension Management:Control which native messaging hosts users can use | [NativeMessagingHostAllowlist](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/nativemessagingallowlistt) | NativeMessagingHostAllowlist | [] |
    | Advanced Extension Management:Configure native messaging block list | [NativeMessagingHostBlocklist](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/nativemessagingblocklist) | NativeMessagingHostBlocklist | ["*"] |
    | Certificate & Authentication:Automatically select client certificates for these sites | [AutoSelectCertificateForUrls](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/autoselectcertificateforurls) | AutoSelectCertificateForUrls | ["*.company.com"] |
    | Content & Media Controls:Restrict the range of local UDP ports used by WebRTC | [WebRtcUdpPortRange](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/webrtcudpportrange) | WebRtcUdpPortRange | 10000:11000 |
    | Content & Media Controls:Default images setting | [DefaultImagesSetting](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/defaultimagessetting) | DefaultImagesSetting | Allow images (1) |
    | Content & Media Controls:Default JavaScript setting | [DefaultJavaScriptSetting](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/defaultjavascriptsetting) | DefaultJavaScriptSetting | Allow JavaScript (1) |
    | Advanced Privacy Controls:Clear browsing data when Microsoft Edge closes | [ClearBrowsingDataOnExit](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/clearbrowsingdataonexit) | ClearBrowsingDataOnExit | Enabled |
    | Advanced Privacy Controls:Disable synchronization of data using Microsoft sync services | [SyncDisabled](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/syncdisabled) | SyncDisabled | Enabled |
    | Printing & Export Controls:Enable printing | [PrintingEnabled](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/printingenabled) | PrintingEnabled | Enabled |
    | Session & Storage Management:InPrivate mode availability | [InPrivateModeAvailability](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/inprivatemodeavailability) | InPrivateModeAvailability | InPrivate mode available (0) |
    | Session & Storage Management:Force synchronization of browser data and do not show the sync consent prompt | [ForceSync](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/forcesync) | ForceSync | Disabled |
    | Performance & Resource Management:Configure sleeping tabs | [SleepingTabsEnabled](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/sleepingtabsenabled) | SleepingTabsEnabled | Enabled |
    | Address Bar Suggestions Management:Enable search suggestions | [SearchSuggestEnabled](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/searchsuggestenabled) | SearchSuggestEnabled | Disabled |
    | Address Bar Suggestions Management:Allow suggestions from local providers | [LocalProvidersEnabled](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/localprovidersenabled) | LocalProvidersEnabled | Disabled |
    | Media Device Permissions:Allow or block video capture | [VideoCaptureAllowed](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/videocaptureallowed) | VideoCaptureAllowed | Disabled |
    | Notification Controls:Default notification setting | [DefaultNotificationsSetting](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/defaultnotificationssetting) | DefaultNotificationsSetting | Block (2) |
    | Location Services Management:Default geolocation setting | [DefaultGeolocationSetting](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/defaultgeolocationsetting) | DefaultGeolocationSetting | Don't allow sites to track users' physical location (2) |
    | USB/HID Device Controls:Allow WebUSB on specific sites | [UsbAllowDevicesForUrls](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/usballowdevicesforurls) | UsbAllowDevicesForUrls | [] |
    | USB/HID Device Controls:Block WebUSB on specific sites | [UsbBlockDevicesForUrls](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/usbblockdevicesforurls) | UsbBlockDevicesForUrls | [{"urls": ["*"], "devices": [{"vendor_id": "*", "product_id": "*"}]}] |
    | WebRTC Advanced Settings:Restrict exposure of local IP address by WebRTC | [WebRtcLocalhostIpHandling](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/webrtclocalhostiphandling) | WebRtcLocalhostIpHandling | Disable non-proxied UDP (default_public_interface_only) |

4. For **Assignments**, assign to **SEB-Level2-Users** group.

5. Select **Next** and **Create**.

### Level 3 - High security configuration (Windows)

1. Follow steps 1-7 from Level 1.

2. On the **Basics** tab:
    - **Name**: Level 3 - High security configuration - Windows ACP
    - **Description**: Maximum security browser configuration

3. Configure all Level 1 and Level 2 settings PLUS:

## App configuration policies for Android

Android app configuration policies customize browser behavior on mobile devices.

> **Microsoft Documentation:**
> - [Microsoft Edge Mobile Policies](/deployedge/microsoft-edge-mobile-policies)
> - [Android App Configuration Policies](app-configuration-policies-overview.md)

**Prerequisites:**
- Android 6.0+
- Microsoft Edge for Android installed
- Company Portal or MAM managed
- User Entra ID account

### Level 1 - Basic mobile browser configuration (Android)

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Apps** > **Configuration** > **Create** > **Managed apps**.

3. On the **Basics** tab:
    - **Name**: Level 1 - Basic mobile browser configuration - Android ACP
    - **Description**: Basic browser configuration for Microsoft Edge on Android

4. Select **Target policy to** > **Select apps** > **Microsoft Edge for Android** > **Select**.

5. For **General configuration settings**, configure:
    - com.microsoft.intune.mam.managedbrowser.PasswordSSO: true
    - com.microsoft.intune.mam.managedbrowser.SmartScreenEnabled: true
    - EdgeMyApps: true
    - EdgeDefaultHTTPS: true
    - EdgeDisableShareUsageData: true
    - PasswordManagerEnabled: false
    - SearchSuggestEnabled: false
    - HideFirstRunExperience: true
    - DefaultPopupsSetting: 2

6. For **Edge configuration settings**:
    - Homepage shortcut URL: https://www.company.com
    - Managed bookmarks: Company Portal|https://portal.company.com

7. For **Assignments**, assign to **SEB-Level1-Users** group.

8. Select **Next** and **Create**.

### Level 2 - Enhanced mobile browser configuration (Android)

1. Follow steps 1-4 from Level 1.

2. On the **Basics** tab:
    - **Name**: Level 2 - Enhanced mobile browser configuration - Android ACP
    - **Description**: Enhanced browser configuration with data protection

3. Configure all Level 1 settings PLUS:
    - EdgeSyncDisabled: true
    - EdgeImportPasswordsDisabled: true
    - EdgeDisabledFeatures: "password|autofill|copilot"
    - SSLErrorOverrideAllowed: false

4. For **Edge configuration settings**:
    - Blocked URLs: *.facebook.com, *.twitter.com, *.instagram.com
    - Redirect restricted sites to personal context: Enable

5. For **Assignments**, assign to **SEB-Level2-Users** group.

6. Select **Next** and **Create**.

### Level 3 - High security mobile configuration (Android)

1. Follow steps 1-4 from Level 1.

2. On the **Basics** tab:
    - **Name**: Level 3 - High security mobile configuration - Android ACP
    - **Description**: Maximum security browser configuration for Android

3. Configure all Level 1 and Level 2 settings PLUS:
    - EdgeMyApps: false
    - EdgeDisabledFeatures: "inprivate|autofill|password|translator|copilot"
    - InPrivateModeAvailability: 1
    - SavingBrowserHistoryDisabled: true
    - EdgeBlockSignInEnabled: true

4. For **Edge configuration settings**:
    - Allowed URLs: *.company.com, *.microsoft.com, login.microsoftonline.com
    - (Blocked URLs field becomes unavailable when Allowed URLs are configured)

5. For **Assignments**, assign to **SEB-Level3-Users** group.

6. Select **Next** and **Create**.

## App configuration policies for iOS/iPadOS

iOS app configuration policies provide comprehensive mobile browser management.

> **Microsoft Documentation:**
> - [Microsoft Edge Mobile Policies](/deployedge/microsoft-edge-mobile-policies)
> - [iOS App Configuration Policies](app-configuration-policies-overview.md)

**Prerequisites:**
- iOS/iPadOS 15+
- Microsoft Edge for iOS installed
- Company Portal or MAM managed
- User Entra ID account

> [!IMPORTANT]
> In iOS App Configuration Policies, **Allowed URLs** and **Blocked URLs** are mutually exclusive. Configure one or the other based on security level requirements.

### Level 1 - Basic mobile browser configuration (iOS)

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Apps** > **Configuration** > **Create** > **Managed apps**.

3. On the **Basics** tab:
    - **Name**: Level 1 - Basic mobile browser configuration - iOS ACP
    - **Description**: Basic browser configuration for Microsoft Edge on iOS

4. Select **Target policy to** > **Select apps** > **Microsoft Edge iOS/iPadOS** > **Select**.

5. For **General configuration settings**, configure:
    - com.microsoft.intune.mam.managedbrowser.PasswordSSO: true
    - com.microsoft.intune.mam.managedbrowser.SmartScreenEnabled: true
    - EdgeMyApps: true
    - EdgeDefaultHTTPS: true
    - EdgeDisableShareUsageData: true
    - PasswordManagerEnabled: false
    - SearchSuggestEnabled: false
    - HideFirstRunExperience: true
    - DefaultPopupsSetting: 2
    - EdgeCopilotEnabled: true

6. For **Edge configuration settings**:
    - Homepage shortcut URL: https://www.company.com
    - Managed bookmarks: Company Portal|https://portal.company.com

7. For **Assignments**, assign to **SEB-Level1-Users** group.

8. Select **Next** and **Create**.

### Level 2 - Enhanced mobile browser configuration (iOS)

1. Follow steps 1-4 from Level 1.

2. On the **Basics** tab:
    - **Name**: Level 2 - Enhanced mobile browser configuration - iOS ACP
    - **Description**: Enhanced browser configuration with security controls

3. Configure all Level 1 settings PLUS:
    - EdgeSyncDisabled: true
    - EdgeImportPasswordsDisabled: true
    - EdgeCopilotEnabled: false
    - EdgeDisabledFeatures: "password|autofill|copilot|collections"
    - BiometricAuthenticationBeforeFilling: true
    - SSLErrorOverrideAllowed: false

4. For **Edge configuration settings**:
    - Blocked URLs: *.facebook.com, *.twitter.com, *.instagram.com, *.tiktok.com
    - (Allowed URLs field becomes unavailable when Blocked URLs are configured)
    - Redirect restricted sites to personal context: Enable

5. For **Assignments**, assign to **SEB-Level2-Users** group.

6. Select **Next** and **Create**.

### Level 3 - High security mobile configuration (iOS)

1. Follow steps 1-4 from Level 1.

2. On the **Basics** tab:
    - **Name**: Level 3 - High security mobile configuration - iOS ACP
    - **Description**: Maximum security browser configuration for iOS

3. Configure all Level 1 and Level 2 settings PLUS:
    - com.microsoft.intune.mam.managedbrowser.PasswordSSO: false
    - EdgeMyApps: false
    - EdgeDisabledFeatures: "inprivate|autofill|password|translator|copilot|share"
    - InPrivateModeAvailability: 1
    - SavingBrowserHistoryDisabled: true
    - TranslateEnabled: false
    - EdgeBlockSignInEnabled: true

4. For **Edge configuration settings**:
    - Allowed URLs: *.company.com, *.microsoft.com, login.microsoftonline.com
    - (Blocked URLs field becomes unavailable when Allowed URLs are configured)

5. For **Assignments**, assign to **SEB-Level3-Users** group.

6. Select **Next** and **Create**.

## Validation

After deploying app configuration policies:

1. **Policy Application**: Check Intune console for successful ACP deployment
2. **Browser Behavior**: Verify configured homepage, blocked features, and URL restrictions
3. **User Experience**: Test browsing functionality and confirm policy enforcement
4. **Mobile Testing**: On mobile devices, verify Microsoft Edge > Menu > Settings reflects corporate policies

## Next steps

Continue to [Step 5](mamedge-5-settings-catalog.md) to configure Settings Catalog policies for enrolled Windows and macOS devices.
