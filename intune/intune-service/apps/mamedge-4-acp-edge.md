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

- Windows 11
- Microsoft Edge installed
- Intune enrollment or MAM managed
- User Entra ID account

### Level 1 - Basic browser configuration for Windows

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Apps** > **Manage apps** > **Configuration** > **Create** > **Managed apps**.  
3. On the **Basics** tab:  
   - **Name:** Level 1 – Basic browser configuration – Windows ACP  
   - **Description:** Basic browser customization for Microsoft Edge on Windows.  
4. In **Target policy to**, select **Selected apps**.  
   - Choose **+ Select public apps**.  
   - In the **Select apps to target** panel, search for and select **Microsoft Edge Windows**, then select **Select**.  
5. Select **Next**.  
6. On the **Settings** step, expand **General configuration settings** and configure:

    | Category | Setting | Name | Value |
    |---------|---------|------|-------|
    | Core Browser Behavior (Enterprise Foundation) | [Configure the home page URL](/deployedge/microsoft-edge-browser-policies/homepagelocation) | HomepageLocation | `https://portal.company.com` |
    | | [Show Home button on toolbar](/deployedge/microsoft-edge-browser-policies/showhomebutton) | ShowHomeButton | Enabled |
    | | [Configure the new tab page URL](/deployedge/microsoft-edge-browser-policies/newtabpageurl) | NewTabPageLocation | `https://portal.company.com` |
    | | [Action to take on startup](/deployedge/microsoft-edge-browser-policies/restoreonstartup) | RestoreOnStartup | Open the new tab page (5) |
    | Content & Security Controls | [Configure Automatic HTTPS](/deployedge/microsoft-edge-browser-policies/httpsonlymode) | HTTPSOnlyMode | Enabled |
    | | [Default pop-up window setting](/deployedge/microsoft-edge-browser-policies/defaultpopupssetting) | DefaultPopupsSetting | Do not allow popups (2) |
    | Privacy & Data Management | [Enable saving passwords to the password manager](/deployedge/microsoft-edge-browser-policies/passwordmanagerenabled) | PasswordManagerEnabled | Disabled |
    | | [Enable AutoFill for addresses](/deployedge/microsoft-edge-browser-policies/autofilladdressenabled) | AutofillAddressEnabled | Disabled |
    | | [Enable Autofill for payment instructions](/deployedge/microsoft-edge-browser-policies/autofillcreditcardenabled) | AutofillCreditCardEnabled | Disabled |
    | | [Block tracking of users' web-browsing activity](/deployedge/microsoft-edge-browser-policies/trackingprevention) | TrackingPrevention | Balanced (2) |
    | Search & Navigation Enhancement | [Enable the default search provider](/deployedge/microsoft-edge-browser-policies/defaultsearchproviderenabled) | DefaultSearchProviderEnabled | Enabled |
    | | [Default search provider name](/deployedge/microsoft-edge-browser-policies/defaultsearchprovidername) | DefaultSearchProviderName | Microsoft Bing |
    | | [Default search provider search URL](/deployedge/microsoft-edge-browser-policies/defaultsearchprovidersearchurl) | DefaultSearchProviderSearchURL | https://www.bing.com/search?q |
    | | [Enable search suggestions](/deployedge/microsoft-edge-browser-policies/searchsuggestenabled) | SearchSuggestEnabled | Disabled |
    | | [Enable network prediction](/deployedge/microsoft-edge-browser-policies/networkpredictionoptions) | NetworkPredictionOptions | Don't predict (2) |
    | Import Controls (Data Boundary) | [Allow importing of autofill form data](/deployedge/microsoft-edge-browser-policies/importautofillformdata) | ImportAutofillFormData | Disabled |
    | | [Allow importing of saved passwords](/deployedge/microsoft-edge-browser-policies/importsavedpasswords) | ImportSavedPasswords | Disabled |
    | | [Allow importing of browsing history](/deployedge/microsoft-edge-browser-policies/importhistory) | ImportBrowsingHistory | Disabled |
    | | [Allow importing cookies](/deployedge/microsoft-edge-browser-policies/importcookies) | ImportCookies | Disabled |
    | | [Allow importing of extension](/deployedge/microsoft-edge-browser-policies/importextensions) | ImportExtensions | Disabled |
    | Extension Management (Basic) | [Control which extensions cannot be installed](/deployedge/microsoft-edge-browser-policies/extensioninstallblocklist) | ExtensionInstallBlocklist | "external_component", "external_pref", "external_registry" |
    | | [Configure allowed extension types](/deployedge/microsoft-edge-browser-policies/extensionallowedtypes) | ExtensionAllowedTypes | "extension", "theme" |
    | | [Configure extension and user script install sources](/deployedge/microsoft-edge-browser-policies/extensioninstallsources) | ExtensionInstallSources | https://corp.contoso.com/ |
    | Download & File Management | [Set download directory](/deployedge/microsoft-edge-browser-policies/downloaddirectory) | DefaultDownloadDirectory | $ |
    | | [Ask where to save downloaded files](/deployedge/microsoft-edge-browser-policies/promptfordownloadlocation) | PromptForDownloadLocation | Enabled |
    | | [Allow download restrictions](/deployedge/microsoft-edge-browser-policies/downloadrestrictions) | DownloadRestrictions | Block malicious downloads and dangerous file types |
    | Feature Controls (Productivity) | [Show Hubs Sidebar](/deployedge/microsoft-edge-browser-policies/hubssidebarenabled) | HubsSidebarEnabled | Disabled |
    | | [Show Microsoft Rewards experiences](/deployedge/microsoft-edge-browser-policies/showmicrosoftrewards) | ShowMicrosoftRewards | Disabled |
    | | [Shopping in Microsoft Edge Enabled](/deployedge/microsoft-edge-browser-policies/edgeshoppingassistantenabled) | EdgeShoppingAssistantEnabled | Disabled |
    | | [Edge Workspaces](/deployedge/microsoft-edge-browser-policies/edgeworkspacesenabled) | EdgeWorkspacesEnabled | Enabled |
    | Bookmarks & Favorites Management | [Show favorites bar](/deployedge/microsoft-edge-browser-policies/favoritesbarenabled) | FavoritesBarEnabled | Enabled |
    | | [Enable deleting browser and download history](/deployedge/microsoft-edge-browser-policies/allowdeletingbrowserhistory) | AllowDeletingBrowserHistory | Enabled |

7. Select **Next**.  
8. For **Assignments**, assign to **SEB-Level1-Users** group.  
9. Select **Next** to review the settings. Then choose **Create**.

### Level 2 - Enhanced browser configuration for Windows

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Apps** > **Manage apps** > **Configuration** > **Create** > **Managed apps**.  
3. On the **Basics** tab:  
   - **Name:** Level 2 – Enhanced browser configuration – Windows ACP  
   - **Description:** Enhanced browser configuration with additional security controls for Microsoft Edge on Windows.  
4. In **Target policy to**, select **Selected apps**.  
   - Choose **+ Select public apps**.  
   - In the **Select apps to target** panel, search for and select **Microsoft Edge Windows**, then select **Select**.  
5. Select **Next**.  
6. On the **Settings** step, expand **General configuration settings** and configure:

    | Category | Setting | Name | Value |
    |---------|---------|------|-------|
    | Core Browser Behavior (Enterprise Foundation) | [Configure the home page URL](/deployedge/microsoft-edge-browser-policies/homepagelocation) | HomepageLocation | `https://portal.company.com` |
    | | [Show Home button on toolbar](/deployedge/microsoft-edge-browser-policies/showhomebutton) | ShowHomeButton | Enabled |
    | | [Configure the new tab page URL](/deployedge/microsoft-edge-browser-policies/newtabpageurl) | NewTabPageLocation | https://portal.company.com |
    | | [Action to take on startup](/deployedge/microsoft-edge-browser-policies/restoreonstartup) | RestoreOnStartup | Open the new tab page (5) |
    | Content & Security Controls | [Configure Automatic HTTPS](/deployedge/microsoft-edge-browser-policies/httpsonlymode) | HTTPSOnlyMode | Enabled |
    | | [Default pop-up window setting](/deployedge/microsoft-edge-browser-policies/defaultpopupssetting) | DefaultPopupsSetting | Do not allow popups (2) |
    | Privacy & Data Management | [Enable saving passwords to the password manager](/deployedge/microsoft-edge-browser-policies/passwordmanagerenabled) | PasswordManagerEnabled | Disabled |
    | | [Enable AutoFill for addresses](/deployedge/microsoft-edge-browser-policies/autofilladdressenabled) | AutofillAddressEnabled | Disabled |
    | | [Enable Autofill for payment instructions](/deployedge/microsoft-edge-browser-policies/autofillcreditcardenabled) | AutofillCreditCardEnabled | Disabled |
    | | [Block tracking of users' web-browsing activity](/deployedge/microsoft-edge-browser-policies/trackingprevention) | TrackingPrevention | Balanced (2) |
    | Search & Navigation Enhancement | [Enable the default search provider](/deployedge/microsoft-edge-browser-policies/defaultsearchproviderenabled) | DefaultSearchProviderEnabled | Enabled |
    | | [Default search provider name](/deployedge/microsoft-edge-browser-policies/defaultsearchprovidername) | DefaultSearchProviderName | Microsoft Bing |
    | | [Default search provider search URL](/deployedge/microsoft-edge-browser-policies/defaultsearchprovidersearchurl) | DefaultSearchProviderSearchURL | https://www.bing.com/search?q |
    | | [Enable search suggestions](/deployedge/microsoft-edge-browser-policies/searchsuggestenabled) | SearchSuggestEnabled | Disabled |
    | | [Enable network prediction](/deployedge/microsoft-edge-browser-policies/networkpredictionoptions) | NetworkPredictionOptions | Don't predict (2) |
    | Import Controls (Data Boundary) | [Allow importing of autofill form data](/deployedge/microsoft-edge-browser-policies/importautofillformdata) | ImportAutofillFormData | Disabled |
    | | [Allow importing of saved passwords](/deployedge/microsoft-edge-browser-policies/importsavedpasswords) | ImportSavedPasswords | Disabled |
    | | [Allow importing of browsing history](/deployedge/microsoft-edge-browser-policies/importhistory) | ImportBrowsingHistory | Disabled |
    | | [Allow importing cookies](/deployedge/microsoft-edge-browser-policies/importcookies) | ImportCookies | Disabled |
    | | [Allow importing of extension](/deployedge/microsoft-edge-browser-policies/importextensions) | ImportExtensions | Disabled |
    | Extension Management (Basic) | [Control which extensions cannot be installed](/deployedge/microsoft-edge-browser-policies/extensioninstallblocklist) | ExtensionInstallBlocklist | "external_component", "external_pref", "external_registry" |
    | | [Configure allowed extension types](/deployedge/microsoft-edge-browser-policies/extensionallowedtypes) | ExtensionAllowedTypes | "extension", "theme" |
    | | [Configure extension and user script install sources](/deployedge/microsoft-edge-browser-policies/extensioninstallsources) | ExtensionInstallSources | https://corp.contoso.com/ |
    | Download & File Management | [Set download directory](/deployedge/microsoft-edge-browser-policies/downloaddirectory) | DefaultDownloadDirectory | $ |
    | | [Ask where to save downloaded files](/deployedge/microsoft-edge-browser-policies/promptfordownloadlocation) | PromptForDownloadLocation | Enabled |
    | | [Allow download restrictions](/deployedge/microsoft-edge-browser-policies/downloadrestrictions) | DownloadRestrictions | Block malicious downloads and dangerous file types |
    | Feature Controls (Productivity) | [Show Hubs Sidebar](/deployedge/microsoft-edge-browser-policies/hubssidebarenabled) | HubsSidebarEnabled | Disabled |
    | | [Show Microsoft Rewards experiences](/deployedge/microsoft-edge-browser-policies/showmicrosoftrewards) | ShowMicrosoftRewards | Disabled |
    | | [Shopping in Microsoft Edge Enabled](/deployedge/microsoft-edge-browser-policies/edgeshoppingassistantenabled) | EdgeShoppingAssistantEnabled | Disabled |
    | | [Edge Workspaces](/deployedge/microsoft-edge-browser-policies/edgeworkspacesenabled) | EdgeWorkspacesEnabled | Enabled |
    | Bookmarks & Favorites Management | [Show favorites bar](/deployedge/microsoft-edge-browser-policies/favoritesbarenabled) | FavoritesBarEnabled | Enabled |
    | | [Enable deleting browser and download history](/deployedge/microsoft-edge-browser-policies/allowdeletingbrowserhistory) | AllowDeletingBrowserHistory | Enabled |
    | Enhanced Security Controls | [Force Microsoft Defender SmartScreen checks on downloads from trusted sources](/deployedge/microsoft-edge-browser-policies/smartscreenfortrusteddownloadsenabled) | SmartScreenForTrustedDownloadsEnabled | Enabled |
    | | [Allow insecure content on specified sites](/deployedge/microsoft-edge-browser-policies/insecurecontentallowedforurls) | InsecureContentAllowedForUrls | [] |
    | | [Block insecure content on specified sites](/deployedge/microsoft-edge-browser-policies/insecurecontentblockedforurls) | InsecureContentBlockedForUrls | ["*"] |
    | Advanced Extension Management | [Allow specific extensions to be installed](/deployedge/microsoft-edge-browser-policies/extensioninstallallowlist) | ExtensionInstallAllowlist | [] |
    | | [Control which extensions are installed silently](/deployedge/microsoft-edge-browser-policies/extensioninstallforcelist) | ExtensionInstallForcelist | [] |
    | | [Configure extension management settings](/deployedge/microsoft-edge-browser-policies/extensionsettings) | ExtensionSettings | {"*":{"installation_mode":"blocked"}} |
    | | [Control which native messaging hosts users can use](/deployedge/microsoft-edge-browser-policies/nativemessagingallowlistt) | NativeMessagingHostAllowlist | [] |
    | | [Configure native messaging block list](/deployedge/microsoft-edge-browser-policies/nativemessagingblocklist) | NativeMessagingHostBlocklist | ["*"] |
    | Certificate & Authentication | [Automatically select client certificates for these sites](/deployedge/microsoft-edge-browser-policies/autoselectcertificateforurls) | AutoSelectCertificateForUrls | ["*.company.com"] |
    | Content & Media Controls | [Restrict the range of local UDP ports used by WebRTC](/deployedge/microsoft-edge-browser-policies/webrtcudpportrange) | WebRtcUdpPortRange | 10000:11000 |
    | | [Default images setting](/deployedge/microsoft-edge-browser-policies/defaultimagessetting) | DefaultImagesSetting | Allow images (1) |
    | | [Default JavaScript setting](/deployedge/microsoft-edge-browser-policies/defaultjavascriptsetting) | DefaultJavaScriptSetting | Allow JavaScript (1) |
    | Advanced Privacy Controls | [Clear browsing data when Microsoft Edge closes](/deployedge/microsoft-edge-browser-policies/clearbrowsingdataonexit) | ClearBrowsingDataOnExit | Enabled |
    | | [Disable synchronization of data using Microsoft sync services](/deployedge/microsoft-edge-browser-policies/syncdisabled) | SyncDisabled | Enabled |
    | Printing & Export Controls | [Enable printing](/deployedge/microsoft-edge-browser-policies/printingenabled) | PrintingEnabled | Enabled |
    | Session & Storage Management | [InPrivate mode availability](/deployedge/microsoft-edge-browser-policies/inprivatemodeavailability) | InPrivateModeAvailability | InPrivate mode available (0) |
    | | [Force synchronization of browser data and do not show the sync consent prompt](/deployedge/microsoft-edge-browser-policies/forcesync) | ForceSync | Disabled |
    | Performance & Resource Management | [Configure sleeping tabs](/deployedge/microsoft-edge-browser-policies/sleepingtabsenabled) | SleepingTabsEnabled | Enabled |
    | Address Bar Suggestions Management | [Enable search suggestions](/deployedge/microsoft-edge-browser-policies/searchsuggestenabled) | SearchSuggestEnabled | Disabled |
    | | [Allow suggestions from local providers](/deployedge/microsoft-edge-browser-policies/localprovidersenabled) | LocalProvidersEnabled | Disabled |
    | Media Device Permissions | [Allow or block video capture](/deployedge/microsoft-edge-browser-policies/videocaptureallowed) | VideoCaptureAllowed | Disabled |
    | Notification Controls | [Default notification setting](/deployedge/microsoft-edge-browser-policies/defaultnotificationssetting) | DefaultNotificationsSetting | Block (2) |
    | Location Services Management | [Default geolocation setting](/deployedge/microsoft-edge-browser-policies/defaultgeolocationsetting) | DefaultGeolocationSetting | Don't allow sites to track users' physical location (2) |
    | USB/HID Device Controls | [Allow WebUSB on specific sites](/deployedge/microsoft-edge-browser-policies/usballowdevicesforurls) | UsbAllowDevicesForUrls | [] |
    | | [Block WebUSB on specific sites](/deployedge/microsoft-edge-browser-policies/usbblockdevicesforurls) | UsbBlockDevicesForUrls | [{"urls":["*"],"devices":[{"vendor_id":"*","product_id":"*"}]}] |
    | WebRTC Advanced Settings | [Restrict exposure of local IP address by WebRTC](/deployedge/microsoft-edge-browser-policies/webrtclocalhostiphandling) | WebRtcLocalhostIpHandling | Disable non-proxied UDP (default_public_interface_only) |

7. Select **Next**.  
8. For **Assignments**, assign to **SEB-Level2-Users** group.  
9. Select **Next** to review the settings. Then choose **Create**.

### Level 3 - High security configuration for Windows

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Apps** > **Manage apps** > **Configuration** > **Create** > **Managed apps**.  
3. On the **Basics** tab:  
   - **Name:** Level 3 – High security configuration – Windows ACP  
   - **Description:** Maximum security browser configuration with zero-trust controls and comprehensive data-loss prevention for Microsoft Edge on Windows.  
4. In **Target policy to**, select **Selected apps**.  
   - Choose **+ Select public apps**.  
   - In the **Select apps to target** panel, search for and select **Microsoft Edge Windows**, then select **Select**.  
5. Select **Next**.  
6. On the **Settings** step, expand **General configuration settings** and configure:

    | Category | Setting | Name | Value |
    |---------|---------|------|-------|
    | Core Browser Behavior (Enterprise Foundation) | [Configure the home page URL](/deployedge/microsoft-edge-browser-policies/homepagelocation) | HomepageLocation | `https://portal.company.com` |
    | | [Show Home button on toolbar](/deployedge/microsoft-edge-browser-policies/showhomebutton) | ShowHomeButton | Enabled |
    | | [Configure the new tab page URL](/deployedge/microsoft-edge-browser-policies/newtabpageurl) | NewTabPageLocation | https://portal.company.com |
    | | [Action to take on startup](/deployedge/microsoft-edge-browser-policies/restoreonstartup) | RestoreOnStartup | Open the new tab page (5) |
    | Content & Security Controls | [Configure Automatic HTTPS](/deployedge/microsoft-edge-browser-policies/httpsonlymode) | HTTPSOnlyMode | Enabled |
    | | [Default pop-up window setting](/deployedge/microsoft-edge-browser-policies/defaultpopupssetting) | DefaultPopupsSetting | Do not allow popups (2) |
    | Privacy & Data Management | [Enable saving passwords to the password manager](/deployedge/microsoft-edge-browser-policies/passwordmanagerenabled) | PasswordManagerEnabled | Disabled |
    | | [Enable AutoFill for addresses](/deployedge/microsoft-edge-browser-policies/autofilladdressenabled) | AutofillAddressEnabled | Disabled |
    | | [Enable Autofill for payment instructions](/deployedge/microsoft-edge-browser-policies/autofillcreditcardenabled) | AutofillCreditCardEnabled | Disabled |
    | | [Block tracking of users' web-browsing activity](/deployedge/microsoft-edge-browser-policies/trackingprevention) | TrackingPrevention | Balanced (2) |
    | Search & Navigation Enhancement | [Enable the default search provider](/deployedge/microsoft-edge-browser-policies/defaultsearchproviderenabled) | DefaultSearchProviderEnabled | Enabled |
    | | [Default search provider name](/deployedge/microsoft-edge-browser-policies/defaultsearchprovidername) | DefaultSearchProviderName | Microsoft Bing |
    | | [Default search provider search URL](/deployedge/microsoft-edge-browser-policies/defaultsearchprovidersearchurl) | DefaultSearchProviderSearchURL | `https://www.bing.com/search?q` |
    | | [Enable search suggestions](/deployedge/microsoft-edge-browser-policies/searchsuggestenabled) | SearchSuggestEnabled | Disabled |
    | | [Enable network prediction](/deployedge/microsoft-edge-browser-policies/networkpredictionoptions) | NetworkPredictionOptions | Don't predict (2) |
    | Import Controls (Data Boundary) | [Allow importing of autofill form data](/deployedge/microsoft-edge-browser-policies/importautofillformdata) | ImportAutofillFormData | Disabled |
    | | [Allow importing of saved passwords](/deployedge/microsoft-edge-browser-policies/importsavedpasswords) | ImportSavedPasswords | Disabled |
    | | [Allow importing of browsing history](/deployedge/microsoft-edge-browser-policies/importhistory) | ImportBrowsingHistory | Disabled |
    | | [Allow importing cookies](/deployedge/microsoft-edge-browser-policies/importcookies) | ImportCookies | Disabled |
    | | [Allow importing of extension](/deployedge/microsoft-edge-browser-policies/importextensions) | ImportExtensions | Disabled |
    | Extension Management (Basic) | [Control which extensions cannot be installed](/deployedge/microsoft-edge-browser-policies/extensioninstallblocklist) | ExtensionInstallBlocklist | "external_component", "external_pref", "external_registry" |
    | | [Configure allowed extension types](/deployedge/microsoft-edge-browser-policies/extensionallowedtypes) | ExtensionAllowedTypes | "extension", "theme" |
    | | [Configure extension and user script install sources](/deployedge/microsoft-edge-browser-policies/extensioninstallsources) | ExtensionInstallSources | `https://corp.contoso.com/` |
    | Download & File Management | [Set download directory](/deployedge/microsoft-edge-browser-policies/downloaddirectory) | DefaultDownloadDirectory | $ |
    | | [Ask where to save downloaded files](/deployedge/microsoft-edge-browser-policies/promptfordownloadlocation) | PromptForDownloadLocation | Enabled |
    | | [Allow download restrictions](/deployedge/microsoft-edge-browser-policies/downloadrestrictions) | DownloadRestrictions | Block malicious downloads and dangerous file types |
    | Feature Controls (Productivity) | [Show Hubs Sidebar](/deployedge/microsoft-edge-browser-policies/hubssidebarenabled) | HubsSidebarEnabled | Disabled |
    | | [Show Microsoft Rewards experiences](/deployedge/microsoft-edge-browser-policies/showmicrosoftrewards) | ShowMicrosoftRewards | Disabled |
    | | [Shopping in Microsoft Edge Enabled](/deployedge/microsoft-edge-browser-policies/edgeshoppingassistantenabled) | EdgeShoppingAssistantEnabled | Disabled |
    | | [Edge Workspaces](/deployedge/microsoft-edge-browser-policies/edgeworkspacesenabled) | EdgeWorkspacesEnabled | Enabled |
    | Bookmarks & Favorites Management | [Show favorites bar](/deployedge/microsoft-edge-browser-policies/favoritesbarenabled) | FavoritesBarEnabled | Enabled |
    | | [Enable deleting browser and download history](/deployedge/microsoft-edge-browser-policies/allowdeletingbrowserhistory) | AllowDeletingBrowserHistory | Enabled |
    | Enhanced Security Controls | [Force Microsoft Defender SmartScreen checks on downloads from trusted sources](/deployedge/microsoft-edge-browser-policies/smartscreenfortrusteddownloadsenabled) | SmartScreenForTrustedDownloadsEnabled | Enabled |
    | | [Allow insecure content on specified sites](/deployedge/microsoft-edge-browser-policies/insecurecontentallowedforurls) | InsecureContentAllowedForUrls | [] |
    | | [Block insecure content on specified sites](/deployedge/microsoft-edge-browser-policies/insecurecontentblockedforurls) | InsecureContentBlockedForUrls | ["*"] |
    | Advanced Extension Management | [Allow specific extensions to be installed](/deployedge/microsoft-edge-browser-policies/extensioninstallallowlist) | ExtensionInstallAllowlist | [] |
    | | [Control which extensions are installed silently](/deployedge/microsoft-edge-browser-policies/extensioninstallforcelist) | ExtensionInstallForcelist | [] |
    | | [Configure extension management settings](/deployedge/microsoft-edge-browser-policies/extensionsettings) | ExtensionSettings | {"*":{"installation_mode":"blocked"}} |
    | | [Control which native messaging hosts users can use](/deployedge/microsoft-edge-browser-policies/nativemessagingallowlistt) | NativeMessagingHostAllowlist | [] |
    | | [Configure native messaging block list](/deployedge/microsoft-edge-browser-policies/nativemessagingblocklist) | NativeMessagingHostBlocklist | ["*"] |
    | Certificate & Authentication | [Automatically select client certificates for these sites](/deployedge/microsoft-edge-browser-policies/autoselectcertificateforurls) | AutoSelectCertificateForUrls | ["*.company.com"] |
    | Content & Media Controls | [Restrict the range of local UDP ports used by WebRTC](/deployedge/microsoft-edge-browser-policies/webrtcudpportrange) | WebRtcUdpPortRange | 10000:11000 |
    | | [Default images setting](/deployedge/microsoft-edge-browser-policies/defaultimagessetting) | DefaultImagesSetting | Allow images (1) |
    | | [Default JavaScript setting](/deployedge/microsoft-edge-browser-policies/defaultjavascriptsetting) | DefaultJavaScriptSetting | Allow JavaScript (1) |
    | Advanced Privacy Controls | [Clear browsing data when Microsoft Edge closes](/deployedge/microsoft-edge-browser-policies/clearbrowsingdataonexit) | ClearBrowsingDataOnExit | Enabled |
    | | [Disable synchronization of data using Microsoft sync services](/deployedge/microsoft-edge-browser-policies/syncdisabled) | SyncDisabled | Enabled |
    | Printing & Export Controls | [Enable printing](/deployedge/microsoft-edge-browser-policies/printingenabled) | PrintingEnabled | Enabled |
    | Session & Storage Management | [InPrivate mode availability](/deployedge/microsoft-edge-browser-policies/inprivatemodeavailability) | InPrivateModeAvailability | InPrivate mode available (0) |
    | | [Force synchronization of browser data and do not show the sync consent prompt](/deployedge/microsoft-edge-browser-policies/forcesync) | ForceSync | Disabled |
    | Performance & Resource Management | [Configure sleeping tabs](/deployedge/microsoft-edge-browser-policies/sleepingtabsenabled) | SleepingTabsEnabled | Enabled |
    | Address Bar Suggestions Management | [Enable search suggestions](/deployedge/microsoft-edge-browser-policies/searchsuggestenabled) | SearchSuggestEnabled | Disabled |
    | | [Allow suggestions from local providers](/deployedge/microsoft-edge-browser-policies/localprovidersenabled) | LocalProvidersEnabled | Disabled |
    | Media Device Permissions | [Allow or block video capture](/deployedge/microsoft-edge-browser-policies/videocaptureallowed) | VideoCaptureAllowed | Disabled |
    | Notification Controls | [Default notification setting](/deployedge/microsoft-edge-browser-policies/defaultnotificationssetting) | DefaultNotificationsSetting | Block (2) |
    | Location Services Management | [Default geolocation setting](/deployedge/microsoft-edge-browser-policies/defaultgeolocationsetting) | DefaultGeolocationSetting | Don't allow sites to track users' physical location (2) |
    | USB/HID Device Controls | [Allow WebUSB on specific sites](/deployedge/microsoft-edge-browser-policies/usballowdevicesforurls) | UsbAllowDevicesForUrls | [] |
    | | [Block WebUSB on specific sites](/deployedge/microsoft-edge-browser-policies/usbblockdevicesforurls) | UsbBlockDevicesForUrls | [{"urls":["*"],"devices":[{"vendor_id":"*","product_id":"*"}]}] |
    | WebRTC Advanced Settings | [Restrict exposure of local IP address by WebRTC](/deployedge/microsoft-edge-browser-policies/webrtclocalhostiphandling) | WebRtcLocalhostIpHandling | Disable non-proxied UDP (default_public_interface_only) |
    | Zero-Trust URL Management | [Define a list of allowed URLs](/deployedge/microsoft-edge-browser-policies/urlallowlist) | URLAllowlist | ["*.company.com",".microsoft.com",".office.com"] |
    | | [Block access to a list of URLs](/deployedge/microsoft-edge-browser-policies/urlblocklist) | URLBlocklist | ["*"] |
    | | [Allow cookies on specific sites](/deployedge/microsoft-edge-browser-policies/cookiesallowedforurls) | CookiesAllowedForUrls | ["*.company.com"] |
    | | [Block cookies on specific sites](/deployedge/microsoft-edge-browser-policies/cookiesblockedforurls) | CookiesBlockedForUrls | ["*"] |
    | | [Limit cookies from specific websites to current session](/deployedge/microsoft-edge-browser-policies/cookiessessiononlyforurls) | CookiesSessionOnlyForUrls | ["*"] |
    | Complete Data Loss Prevention | [Download restrictions](/deployedge/microsoft-edge-browser-policies/downloadrestrictions) | DownloadRestrictions | Block all downloads (4) |
    | | [Allow or deny screen capture](/deployedge/microsoft-edge-browser-policies/screencaptureallowed) | ScreenCaptureAllowed | Disabled |
    | | [Enable printing](/deployedge/microsoft-edge-browser-policies/printingenabled) | PrintingEnabled | Disabled |
    | | [Default clipboard site permission](/deployedge/microsoft-edge-browser-policies/defaultclipboardsetting) | DefaultClipboardSetting | Block clipboard (2) |
    | | [Allow or block video capture](/deployedge/microsoft-edge-browser-policies/videocaptureallowed) | VideoCaptureAllowed | Disabled |
    | High Privacy Enforcement | [Configure InPrivate mode availability](/deployedge/microsoft-edge-browser-policies/inprivatemodeavailability) | InPrivateModeAvailability | InPrivate mode forced (2) |
    | | [Clear browsing data when Microsoft Edge closes](/deployedge/microsoft-edge-browser-policies/clearbrowsingdataonexit) | ClearBrowsingDataOnExit | Enabled |
    | | [Disable saving browser history](/deployedge/microsoft-edge-browser-policies/savingbrowserhistorydisabled) | SavingBrowserHistoryDisabled | Enabled |
    | | [Enable saving passwords to the password manager](/deployedge/microsoft-edge-browser-policies/passwordmanagerenabled) | PasswordManagerEnabled | Disabled |
    | Developer Tools Lockdown | [Control where developer tools can be used](/deployedge/microsoft-edge-browser-policies/developertoolsavailability) | DeveloperToolsAvailability | Disallowed (2) |
    | Network Security | [Enable network prediction](/deployedge/microsoft-edge-browser-policies/networkpredictionoptions) | NetworkPredictionOptions | Don't predict (2) |
    | Feature Restrictions | [Enable the Collections feature](/deployedge/microsoft-edge-browser-policies/edgecollectionsenabled) | EdgeCollectionsEnabled | Disabled |
    | | [Allow users to access the games menu](/deployedge/microsoft-edge-browser-policies/gamemenuenabled) | GameMenuEnabled | Disabled |

7. Select **Next**.  
8. For **Assignments**, assign to **SEB-Level3-Users** group.  
9. Select **Next** to review the settings. Then choose **Create**.

### Validation (All Windows Levels)

#### Policy Application

In the Intune admin center, navigate to **Devices** > **Windows** > select a device > **Device configuration** > **View report**.
Confirm the policy status shows **Succeeded**.

#### Endpoint Verification

On the client device, open Microsoft Edge and navigate to `edge://policy`

Confirm that the configured policy keys (for example, **URLAllowlist**, **DownloadRestrictions**, **InPrivateModeAvailability**) appear and show a **Not Error** status.

#### Feature Testing

- Level 1: Verify homepage, SmartScreen, pop-up blocking, and tracking prevention are active.
- Level 2: Test blocked extensions, clear-on-exit behavior, and restricted media capture.
- Level 3: Attempt to access a non-allowlisted site—confirm that it’s blocked or opens in **Application Guard**.

#### Update Policies

In `edge://policy`, search for **Update** to verify the correct update cadence (daily, 12-hour, or weekly) matches the configured security level.

#### Isolation Check (Level 3 only)

Ensure that browsing to unapproved URLs either fails or triggers an isolated container session (for example, App Guard or virtual sandbox).

::: zone-end

::: zone pivot="android"

## App Configuration Policies for Android

Android app configuration policies customize Microsoft Edge for Business behavior on mobile devices. These policies define browser defaults, restrict risky features, and enforce privacy protections in alignment with enterprise security frameworks.

> **Microsoft Documentation:**
>
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

### Level 1 – Basic Mobile Browser Configuration for Android

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Apps** > **Manage apps** > **Configuration** > **Create** > **Managed apps**.  
3. On the **Basics** tab:  
   - **Name:** Level 1 – Basic mobile browser configuration – Android ACP  
   - **Description:** Basic browser configuration for Microsoft Edge on Android.  
4. In **Target policy to**, select **Selected apps**.  
   - Choose **+ Select public apps**.  
   - In the **Select apps to target** panel, search for and select **Microsoft Edge (Android)**, then select **Select**.  
5. Select **Next**.  
6. On the **Settings** step, expand **General configuration settings** and configure:

| Category | Setting | Name | Value |
|---------|---------|------|-------|
| General configuration settings | [Microsoft Entra password single sign-on](manage-microsoft-edge.md#microsoft-entra-password-single-sign-on) | com.microsoft.intune.mam.managedbrowser.PasswordSSO | true |
| | [Microsoft Defender SmartScreen](manage-microsoft-edge.md#microsoft-defender-smartscreen) | com.microsoft.intune.mam.managedbrowser.SmartScreenEnabled | true |
| | [Enable EdgeMyApps](/deployedge/microsoft-edge-mobile-policies#edgemyapps) | EdgeMyApps | true |
| | [Enforce default HTTPS](/deployedge/microsoft-edge-mobile-policies#edgedefaulthttps) | EdgeDefaultHTTPS | true |
| | [Disable sharing usage data](/deployedge/microsoft-edge-mobile-policies#edgedisableshareusagedata) | EdgeDisableShareUsageData | true |
| | [Disable password import](/deployedge/microsoft-edge-mobile-policies#edgeimportpasswordsdisabled) | EdgeImportPasswordsDisabled | false |
| | [Configure new tab page layout](/deployedge/microsoft-edge-mobile-policies#edgenewtabpagelayout) | EdgeNewTabPageLayout | 0 |
| | [Enable kiosk mode](/deployedge/microsoft-edge-mobile-policies#edgeenablekioskmode) | EdgeEnableKioskMode | false |
| | [Show address bar in kiosk mode](/deployedge/microsoft-edge-mobile-policies#edgeshowaddressbarinkioskmode) | EdgeShowAddressBarInKioskMode | true |
| General configuration settings - Smartscreen | [Enable SmartScreen](/deployedge/microsoft-edge-mobile-policies#smartscreenenabled) | SmartScreenEnabled | true |
| General configuration settings - Additional | [Enable search suggestions](/deployedge/microsoft-edge-mobile-policies#searchsuggestenabled) | SearchSuggestEnabled | false |
| | [Enable translate](/deployedge/microsoft-edge-mobile-policies#translateenabled) | TranslateEnabled | true |
| | [Hide first run experience](/deployedge/microsoft-edge-mobile-policies#hidefirstrunexperience) | HideFirstRunExperience | true |
| | [Allow SSL error override](/deployedge/microsoft-edge-mobile-policies#sslerroroverrideallowed) | SSLErrorOverrideAllowed | true |
| | [Enable as default browser](/deployedge/microsoft-edge-mobile-policies#defaultbrowsersettingenabled) | DefaultBrowserSettingEnabled | true |
| | [Enable Edge Copilot](/deployedge/microsoft-edge-mobile-policies#edgecopilotenabled) | EdgeCopilotEnabled | true |
| | [Enable shared device support](/deployedge/microsoft-edge-mobile-policies#edgeshareddevicesupportenabled) | EdgeSharedDeviceSupportEnabled | true |
| | [Experimentation and configuration service control](/deployedge/microsoft-edge-mobile-policies#experimentationandconfigurationservicecontrol) | ExperimentationAndConfigurationServiceControl | 1 |
| General configuration settings - Content | [Default pop-ups setting](/deployedge/microsoft-edge-mobile-policies#defaultpopupssetting) | DefaultPopupsSetting | 2 |
| | [Default cookies setting](/deployedge/microsoft-edge-mobile-policies#defaultcookiessetting) | DefaultCookiesSetting | 1 |
| General configuration settings - Password Manager and Protection | [Biometric authentication before filling](/deployedge/microsoft-edge-browser-policies/biometricauthenticationbeforefilling) | BiometricAuthenticationBeforeFilling | false |
| | [Enable password manager](/deployedge/microsoft-edge-mobile-policies#passwordmanagerenabled) | PasswordManagerEnabled | false |
| General configuration settings - Organizational Branding | [Enable Edge brand logo](/deployedge/microsoft-edge-mobile-policies#edgebrandlogo) | EdgeBrandLogo | true |
| | [Set Edge brand color](/deployedge/microsoft-edge-mobile-policies#edgebrandcolor) | EdgeBrandColor | `#0078d4` |
| General configuration settings - Default Search Provider | [Enable default search provider](/deployedge/microsoft-edge-mobile-policies#defaultsearchproviderenabled) | DefaultSearchProviderEnabled | true |
| | [Default search provider name](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidername) | DefaultSearchProviderName | "Preferred Company Search" |
| | [Default search provider search URL](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidersearchurl) | DefaultSearchProviderSearchURL | "https://search.company.com?q={searchTerms}" |
| | [Default search provider suggest URL](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidersuggesturl) | DefaultSearchProviderSuggestURL | "https://search.company.com/suggest?q={searchTerms}" |
| | [Default search provider keyword](/deployedge/microsoft-edge-mobile-policies#defaultsearchproviderkeyword) | DefaultSearchProviderKeyword | "company" |
| General configuration settings - Proxy Configuration | [Configure proxy settings](/deployedge/microsoft-edge-browser-policies/proxysettings) | ProxySettings | {"ProxyServer": "IP:Port", "ProxyBypassList": "*.company.com", "ProxyMode": "direct"} |

7. Under Microsoft Tunnel for Mobile Application Management settings:

| Category | Setting | Value |
|-----------|----------|-------|
| Microsoft Tunnel for Mobile Application Management settings | Tunnel enabled | Not configured |
|  | Connection name | Not configured |
|  | Microsoft Tunnel site | Not configured |
|  | Per-App VPN (Android only) | No Per-App VPN |
|  | Automatic configuration script | Not configured |
|  | Address | Not configured |
|  | Port Number | Not configured |
|  | Root Certificate | Not configured |

8. Expand **Edge configuration settings** and configure:

| Category | Setting | Value |
|-----------|----------|-------|
| Edge configuration settings | Application proxy redirection | Disable |
|  | Homepage shortcut URL | `https://www.company.com` |
|  | Managed bookmarks | Company Portal &#124; `https://portal.company.com` |
|  | Allowed URLs | Leave empty (Level 3 uses Allowed URLs) |
|  | Blocked URLs | Leave empty (Level 2 uses Blocked URLs) |
|  | Redirect restricted sites to personal context | Disable |

9. Select **Next**
10. In **Assignments**, assign to **SEB-Level1-Users** group.  
11. Select **Next** to review the settings. Then choose **Create**.

### Level 2 – Enhanced Mobile Browser Configuration for Android

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Apps** > **Manage apps** > **Configuration** > **Create** > **Managed apps**.  
3. On the **Basics** tab:  
   - **Name:** Level 2 – Enhanced mobile browser configuration – Android ACP  
   - **Description:** Enhanced browser configuration with additional security controls for Microsoft Edge on Android.  
4. In **Target policy to**, select **Selected apps**.  
   - Choose **+ Select public apps**.  
   - In the **Select apps to target** panel, search for and select **Microsoft Edge (Android)**, then select **Select**.  
5. Select **Next**.  
6. On the **Settings** step, expand **General configuration settings** and configure:

| Category | Setting | Name | Value |
|---------|---------|------|-------|
| General configuration settings | [Microsoft Entra password single sign-on](manage-microsoft-edge.md#microsoft-entra-password-single-sign-on) | com.microsoft.intune.mam.managedbrowser.PasswordSSO | true |
| | [Microsoft Defender SmartScreen](manage-microsoft-edge.md#microsoft-defender-smartscreen) | com.microsoft.intune.mam.managedbrowser.SmartScreenEnabled | true |
| | [Enable EdgeMyApps](/deployedge/microsoft-edge-mobile-policies#edgemyapps) | EdgeMyApps | true |
| | [Enforce default HTTPS](/deployedge/microsoft-edge-mobile-policies#edgedefaulthttps) | EdgeDefaultHTTPS | true |
| | [Disable sharing usage data](/deployedge/microsoft-edge-mobile-policies#edgedisableshareusagedata) | EdgeDisableShareUsageData | true |
| | [Disable password import](/deployedge/microsoft-edge-mobile-policies#edgeimportpasswordsdisabled) | EdgeImportPasswordsDisabled | true |
| | [Configure new tab page layout](/deployedge/microsoft-edge-mobile-policies#edgenewtabpagelayout) | EdgeNewTabPageLayout | 1 |
| | [Enable kiosk mode](/deployedge/microsoft-edge-mobile-policies#edgeenablekioskmode) | EdgeEnableKioskMode | false |
| | [Show address bar in kiosk mode](/deployedge/microsoft-edge-mobile-policies#edgeshowaddressbarinkioskmode) | EdgeShowAddressBarInKioskMode | true |
| General configuration settings – Enhanced | [Disable browser sync](/deployedge/microsoft-edge-mobile-policies#edgesyncdisabled) | EdgeSyncDisabled | true |
| General configuration settings – Smartscreen | [Enable SmartScreen](/deployedge/microsoft-edge-mobile-policies#smartscreenenabled) | SmartScreenEnabled | true |
| General configuration settings – Additional | [Disable browser history saving](/deployedge/microsoft-edge-mobile-policies#savingbrowserhistorydisabled) | SavingBrowserHistoryDisabled | false |
| | [Allow SSL error override](/deployedge/microsoft-edge-mobile-policies#sslerroroverrideallowed) | SSLErrorOverrideAllowed | false |
| | [Disable Edge Copilot](/deployedge/microsoft-edge-mobile-policies#edgecopilotenabled) | EdgeCopilotEnabled | false |
| | [Experimentation and configuration service control](/deployedge/microsoft-edge-mobile-policies#experimentationandconfigurationservicecontrol) | ExperimentationAndConfigurationServiceControl | 0 |
| | [Set as default browser](/deployedge/microsoft-edge-mobile-policies#defaultbrowsersettingenabled) | DefaultBrowserSettingEnabled | false |
| General configuration settings – Content | [Default cookies setting](/deployedge/microsoft-edge-browser-policies/defaultcookiessetting) | DefaultCookiesSetting | 2 |
| General configuration settings – Password Manager and Protection | [Biometric authentication before filling](/deployedge/microsoft-edge-browser-policies/biometricauthenticationbeforefilling) | BiometricAuthenticationBeforeFilling | true |
| | [Enable password manager](/deployedge/microsoft-edge-mobile-policies#passwordmanagerenabled) | PasswordManagerEnabled | false |
| General configuration settings – Manageability | [Disable features](/deployedge/microsoft-edge-mobile-policies#edgedisabledfeatures) | EdgeDisabledFeatures | password&#124;autofill&#124;copilot&#124;collections&#124;readaloud |
| General configuration settings – Identity and sign-in | [Block sign-in enabled](/deployedge/microsoft-edge-mobile-policies#edgeblocksigninenabled) | EdgeBlockSignInEnabled | false |
| General configuration settings – Organizational Branding | [Enable Edge brand logo](/deployedge/microsoft-edge-mobile-policies#edgebrandlogo) | EdgeBrandLogo | true |
| | [Set Edge brand color](/deployedge/microsoft-edge-mobile-policies#edgebrandcolor) | EdgeBrandColor | `#0078d4` |
| General configuration settings – Default Search Provider | [Enable default search provider](/deployedge/microsoft-edge-mobile-policies#defaultsearchproviderenabled) | DefaultSearchProviderEnabled | true |
| | [Default search provider name](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidername) | DefaultSearchProviderName | "Preferred Company Search" |
| | [Default search provider search URL](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidersearchurl) | DefaultSearchProviderSearchURL | "https://search.company.com?q={searchTerms}" |
| | [Default search provider suggest URL](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidersuggesturl) | DefaultSearchProviderSuggestURL | "https://search.company.com/suggest?q={searchTerms}" |
| | [Default search provider keyword](/deployedge/microsoft-edge-mobile-policies#defaultsearchproviderkeyword) | DefaultSearchProviderKeyword | "company" |
| General configuration settings – Proxy Configuration | [Configure proxy settings](/deployedge/microsoft-edge-browser-policies/proxysettings) | ProxySettings | {"ProxyServer": "IP:Port", "ProxyBypassList": "*.company.com", "ProxyMode": "direct"} |

7. Expand **Edge configuration settings** and configure:

| Category | Setting | Value |
|-----------|----------|-------|
| Edge Configuration Settings | Allowed URLs | Leave empty (Level 2 uses blocked URLs instead – when blocked URLs are configured, allowed URLs field becomes unavailable) |
|  | Blocked URLs | *.facebook.com, *.twitter.com, *.instagram.com, *.tiktok.com |
|  | Redirect restricted sites to personal context | Enable |

8. Select **Next**
9. In **Assignments**, assign to **SEB-Level2-Users** group.  
10. Select **Next** to review the settings. Then choose **Create**.

### Level 3 – High Security Mobile Configuration for Android

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Apps** > **Manage apps** > **Configuration** > **Create** > **Managed apps**.  
3. On the **Basics** tab:  
   - **Name:** Level 3 – High security mobile browser configuration – Android ACP
   - **Description:** Maximum security configuration for Microsoft Edge on Android, enforcing strict data protection and zero-trust controls.  
4. In **Target policy to**, select **Selected apps**.  
   - Choose **+ Select public apps**.  
   - In the **Select apps to target** panel, search for and select **Microsoft Edge (Android)**, then select **Select**.  
5. Select **Next**.
6. On the **Settings** step, expand **General configuration settings** and configure:

| Category | Setting | Name | Value |
|---------|---------|------|-------|
| General configuration settings | [Microsoft Entra password single sign-on](/microsoft-365/solutions/apps-config-step-4#general-app-configuration-settings) | com.microsoft.intune.mam.managedbrowser.PasswordSSO | false |
| | [Enable EdgeMyApps](/deployedge/microsoft-edge-mobile-policies#edgemyapps) | EdgeMyApps | false |
| | [Enforce default HTTPS](/deployedge/microsoft-edge-mobile-policies#edgedefaulthttps) | EdgeDefaultHTTPS | true |
| | [Disable sharing usage data](/deployedge/microsoft-edge-mobile-policies#edgedisableshareusagedata) | EdgeDisableShareUsageData | true |
| | [Configure new tab page layout](/deployedge/microsoft-edge-mobile-policies#edgenewtabpagelayout) | EdgeNewTabPageLayout | 2 |
| | [Enable kiosk mode](/deployedge/microsoft-edge-mobile-policies#edgeenablekioskmode) | EdgeEnableKioskMode | true |
| | [Show address bar in kiosk mode](/deployedge/microsoft-edge-mobile-policies#edgeshowaddressbarinkioskmode) | EdgeShowAddressBarInKioskMode | false |
| General configuration settings – Enhanced | [Disable browser sync](/deployedge/microsoft-edge-mobile-policies#edgesyncdisabled) | EdgeSyncDisabled | true |
| General configuration settings – Additional | [Disable InPrivate mode](/deployedge/microsoft-edge-mobile-policies#inprivatemodeavailability) | InPrivateModeAvailability | 1 |
| | [Disable browser history saving](/deployedge/microsoft-edge-mobile-policies#savingbrowserhistorydisabled) | SavingBrowserHistoryDisabled | true |
| | [Disable translate](/deployedge/microsoft-edge-mobile-policies#translateenabled) | TranslateEnabled | false |
| | [Disable shared device support](/deployedge/microsoft-edge-mobile-policies#edgeshareddevicesupportenabled) | EdgeSharedDeviceSupportEnabled | false |
| | [Disable autofill for payment instructions](/deployedge/microsoft-edge-browser-policies/autofillcreditcardenabled) | AutofillCreditCardEnabled | false |
| | [Download restrictions](/deployedge/microsoft-edge-browser-policies/downloadrestrictions) | DownloadRestrictions | 2 |
| | [Experimentation and configuration service control](/deployedge/microsoft-edge-mobile-policies#experimentationandconfigurationservicecontrol) | ExperimentationAndConfigurationServiceControl | 0 |
| | [Set as default browser](/deployedge/microsoft-edge-mobile-policies#defaultbrowsersettingenabled) | DefaultBrowserSettingEnabled | false |
| General configuration settings – Content | [Default cookies setting](/deployedge/microsoft-edge-browser-policies/defaultcookiessetting) | DefaultCookiesSetting | 4 |
| | [Default JavaScript setting](/deployedge/microsoft-edge-browser-policies/defaultjavascriptsetting) | DefaultJavaScriptSetting | 2 |
| | [Default geolocation setting](/deployedge/microsoft-edge-browser-policies/defaultgeolocationsetting) | DefaultGeolocationSetting | 2 |
| General configuration settings – Password Manager and Protection | [Biometric authentication before filling](/deployedge/microsoft-edge-browser-policies/biometricauthenticationbeforefilling) | BiometricAuthenticationBeforeFilling | true |
| | [Enable password manager](/deployedge/microsoft-edge-mobile-policies#passwordmanagerenabled) | PasswordManagerEnabled | false |
| General configuration settings – Manageability | [Disable features](/deployedge/microsoft-edge-mobile-policies#edgedisabledfeatures) | EdgeDisabledFeatures | inprivate&#124;autofill&#124;password&#124;translator&#124;readaloud&#124;drop&#124;coupons&#124;extensions&#124;copilot&#124;collections&#124;myapps |
| General configuration settings – Organizational Branding | [Enable Edge brand logo](/deployedge/microsoft-edge-mobile-policies#edgebrandlogo) | EdgeBrandLogo | true |
| | [Set Edge brand color](/deployedge/microsoft-edge-mobile-policies#edgebrandcolor) | EdgeBrandColor | `#0078d4` |
| General configuration settings – Default Search Provider | [Enable default search provider](/deployedge/microsoft-edge-mobile-policies#defaultsearchproviderenabled) | DefaultSearchProviderEnabled | true |
| | [Default search provider name](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidername) | DefaultSearchProviderName | "Preferred Company Search" |
| | [Default search provider search URL](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidersearchurl) | DefaultSearchProviderSearchURL | "https://search.company.com?q={searchTerms}" |
| | [Default search provider suggest URL](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidersuggesturl) | DefaultSearchProviderSuggestURL | "https://search.company.com/suggest?q={searchTerms}" |
| | [Default search provider keyword](/deployedge/microsoft-edge-mobile-policies#defaultsearchproviderkeyword) | DefaultSearchProviderKeyword | "company" |
| General configuration settings – Proxy Configuration | [Configure proxy settings](/deployedge/microsoft-edge-browser-policies/proxysettings) | ProxySettings | {"ProxyServer": "IP:Port", "ProxyBypassList": "*.company.com", "ProxyMode": "fixed_servers"} |
| General configuration settings – Identity and sign-in | [Block sign-in enabled](/deployedge/microsoft-edge-browser-policies/edgeblocksigninenabled) | EdgeBlockSignInEnabled | true |

7. Expand **Edge configuration settings** and configure:

| Category | Setting | Value |
|-----------|----------|-------|
| Edge Configuration Settings | Allowed URLs | *.company.com, *.microsoft.com, login.microsoftonline.com |
|  | Blocked URLs | Leave empty (Level 3 uses allowed URLs – when allowed URLs are configured, blocked URLs field becomes unavailable) |

8. Select **Next**
9. In **Assignments**, assign to **SEB-Level3-Users** group.  
10. Select **Next** to review the settings. Then choose **Create**.

### Validation (All Levels)

- **Policy application:** Verify in Intune under **Monitor > Device configuration** that the ACP shows *Succeeded*.  
- **On device:** Open Edge > **Settings** > confirm homepage, privacy restrictions, and URL enforcement.  
- **Blocked content:** Attempt to open restricted sites (e.g., facebook.com) on Level 2/3 — ensure redirection or blocking.  
- **Zero-trust enforcement:** Verify InPrivate, Autofill, Copilot, and password features are disabled under Level 3.  
- **Security confirmation:** Run `edge://policy` (in desktop simulation or Android enterprise debug build) to confirm policy key deployment.

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

### Level 1 – Basic mobile browser configuration for iOS

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Apps** > **Manage apps** > **Configuration** > **Create** > **Managed apps**.  
3. On the **Basics** tab:  
   - **Name:** Level 1 – Basic mobile browser configuration – iOS ACP  
   - **Description:** Basic browser configuration for Microsoft Edge on iOS.  
4. In **Target policy to**, select **Selected apps**.  
   - Choose **+ Select public apps**.  
   - In the **Select apps to target** panel, search for and select **Microsoft Edge**.  
   - Choose **Microsoft Edge (iOS/iPadOS)**, then **Select**.  
5. Select **Next**.  
6. On the **Settings** step, expand **General configuration settings** and configure:

| Category | Setting | Name | Value |
|---------|---------|------|-------|
| General Configuration Settings | [Password single sign-on](https://learn.microsoft.com/en-us/microsoft-365/solutions/apps-config-step-4?view=o365-worldwide#general-app-configuration-settings) | com.microsoft.intune.mam.managedbrowser.PasswordSSO | true |
|  | [SmartScreen enabled](https://learn.microsoft.com/en-us/microsoft-365/solutions/apps-config-step-4?view=o365-worldwide#general-app-configuration-settings) | com.microsoft.intune.mam.managedbrowser.SmartScreenEnabled | true |
|  | [Enable EdgeMyApps](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-mobile-policies#edgemyapps) | EdgeMyApps | true |
|  | [Default HTTPS enforced](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-mobile-policies#edgedefaulthttps) | EdgeDefaultHTTPS | true |
|  | [Disable sharing usage data](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-mobile-policies#edgedisableshareusagedata) | EdgeDisableShareUsageData | true |
|  | [Disable password import](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-mobile-policies#edgeimportpasswordsdisabled) | EdgeImportPasswordsDisabled | false |
|  | [Proxy PAC URL](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-mobile-policies#edgeproxypacurl) | EdgeProxyPacUrl |  |
| General Configuration Settings – Password Manager and Protection | [Biometric authentication before filling](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/biometricauthenticationbeforefilling) | BiometricAuthenticationBeforeFilling | false |
|  | [Disable password manager](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-mobile-policies#passwordmanagerenabled) | PasswordManagerEnabled | false |
| General Configuration Settings – Smartscreen | [SmartScreen enabled](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-mobile-policies#smartscreenenabled) | SmartScreenEnabled | true |
| General Configuration Settings – Additional | [Disable search suggestions](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-mobile-policies#searchsuggestenabled) | SearchSuggestEnabled | false |
|  | [Translate enabled](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-mobile-policies#translateenabled) | TranslateEnabled | true |
|  | [Hide first run experience](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-mobile-policies#hidefirstrunexperience) | HideFirstRunExperience | true |
|  | [SSL error override allowed](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-mobile-policies#sslerroroverrideallowed) | SSLErrorOverrideAllowed | true |
|  | [Default browser setting enabled](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-mobile-policies#defaultbrowsersettingenabled) | DefaultBrowserSettingEnabled | true |
|  | [Experimentation and configuration service control](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-mobile-policies#experimentationandconfigurationservicecontrol) | ExperimentationAndConfigurationServiceControl | 1 |
| General Configuration Settings – Content | [Disable pop-ups](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-mobile-policies#defaultpopupssetting) | DefaultPopupsSetting | 2 |
| General Configuration Settings – Organizational Branding | [Organizational branding – logo](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-mobile-policies#edgebrandlogo) | EdgeBrandLogo | true |
|  | [Organizational branding – color](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-mobile-policies#edgebrandcolor) | EdgeBrandColor | `#0078d4` |
| General Configuration Settings – Default Search Provider | [Default search provider enabled](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-mobile-policies#defaultsearchproviderenabled) | DefaultSearchProviderEnabled | true |
|  | [Default search provider name](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidername) | DefaultSearchProviderName | Preferred Company Search |
|  | [Default search provider search URL](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidersearchurl) | DefaultSearchProviderSearchURL | `https://search.company.com?q={searchTerms}` |
|  | [Default search provider suggest URL](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidersuggesturl) | DefaultSearchProviderSuggestURL | `https://search.company.com/suggest?q={searchTerms}` |
|  | [Default search provider keyword](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-mobile-policies#defaultsearchproviderkeyword) | DefaultSearchProviderKeyword | company |

7. Expand **Edge configuration settings** and configure:

| Category | Setting | Value |
|-----------|----------|-------|
| Edge configuration settings | Application proxy redirection | Disable |
|  | Homepage shortcut URL | `https://www.company.com` |
|  | Managed bookmarks | Company Portal &#124; `https://portal.company.com` |
|  | Allowed URLs | Leave empty (Level 3 uses Allowed URLs) |
|  | Blocked URLs | Leave empty (Level 2 uses Blocked URLs) |
|  | Redirect restricted sites to personal context | Disable |


8. Select **Next**.  
9. In **Assignments**, assign to **SEB-Level1-Users** group.  
10. Select **Next** to review the settings. Then choose **Create** when you're done.  

### Level 2 – Enhanced mobile browser configuration for iOS

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Apps** > **Manage apps** > **Configuration** > **Create** > **Managed apps**.  
3. On the **Basics** tab:  
   - **Name:** Level 2 – Enhanced mobile browser configuration – iOS ACP  
   - **Description:** Enhanced browser configuration with security controls for Microsoft Edge on iOS.  
4. In **Target policy to**, select **Selected apps**.  
   - Choose **+ Select public apps**.  
   - In the **Select apps to target** panel, search for and select **Microsoft Edge**.  
   - Choose **Microsoft Edge (iOS/iPadOS)**, then **Select**.  
5. Select **Next**.  
6. On the **Settings** step, expand **General configuration settings** and configure:

| Category | Setting | Name | Value |
|---------|---------|------|-------|
| General Configuration Settings | [Password single sign-on](/deployedge/microsoft-edge-mobile-policies#passwordsso) | com.microsoft.intune.mam.managedbrowser.PasswordSSO | true |
|  | [SmartScreen enabled](/deployedge/microsoft-edge-mobile-policies#smartscreenenabled) | com.microsoft.intune.mam.managedbrowser.SmartScreenEnabled | true |
|  | [Enable EdgeMyApps](/deployedge/microsoft-edge-mobile-policies#edgemyapps) | EdgeMyApps | true |
|  | [Default HTTPS enforced](/deployedge/microsoft-edge-mobile-policies#edgedefaulthttps) | EdgeDefaultHTTPS | true |
|  | [Disable sharing usage data](/deployedge/microsoft-edge-mobile-policies#edgedisableshareusagedata) | EdgeDisableShareUsageData | true |
|  | [Disable password manager](/deployedge/microsoft-edge-mobile-policies#passwordmanagerenabled) | PasswordManagerEnabled | false |
|  | [Disable search suggestions](/deployedge/microsoft-edge-mobile-policies#searchsuggestenabled) | SearchSuggestEnabled | false |
|  | [Hide first run experience](/deployedge/microsoft-edge-mobile-policies#hidefirstrunexperience) | HideFirstRunExperience | true |
|  | [Disable pop-ups](/deployedge/microsoft-edge-mobile-policies#defaultpopupssetting) | DefaultPopupsSetting | 2 |
|  | [Disable sync](/deployedge/microsoft-edge-mobile-policies#edgesyncdisabled) | EdgeSyncDisabled | true |
|  | [Disable password import](/deployedge/microsoft-edge-mobile-policies#edgeimportpasswordsdisabled) | EdgeImportPasswordsDisabled | true |
|  | [Disable Copilot](/deployedge/microsoft-edge-mobile-policies#edgecopilotenabled) | EdgeCopilotEnabled | false |
|  | [Disable browser setting](/deployedge/microsoft-edge-mobile-policies#defaultbrowsersettingenabled) | DefaultBrowserSettingEnabled | false |
|  | [Experimentation and configuration service control](/deployedge/microsoft-edge-mobile-policies#experimentationandconfigurationservicecontrol) | ExperimentationAndConfigurationServiceControl | 0 |
| General Configuration Settings – Additional | [Disable saving browser history](/deployedge/microsoft-edge-mobile-policies#savingbrowserhistorydisabled) | SavingBrowserHistoryDisabled | false |
|  | [Disable SSL error override](/deployedge/microsoft-edge-mobile-policies#sslerroroverrideallowed) | SSLErrorOverrideAllowed | false |
| General Configuration Settings – Password Manager and Protection | [Biometric authentication before filling](/deployedge/microsoft-edge-browser-policies/biometricauthenticationbeforefilling) | BiometricAuthenticationBeforeFilling | true |
| General Configuration Settings – Organizational Branding Configuration | [Organizational branding – logo](/deployedge/microsoft-edge-mobile-policies#edgebrandlogo) | EdgeBrandLogo | true |
| General Configuration Settings – Manageability | [Disable features](/deployedge/microsoft-edge-mobile-policies#edgedisabledfeatures) | EdgeDisabledFeatures | password\|autofill\|copilot\|collections\|readaloud |
| General Configuration Settings – Identity and Sign-in | [Block Edge sign-in](/deployedge/microsoft-edge-mobile-policies#edgeblocksigninenabled) | EdgeBlockSignInEnabled | false |
| General Configuration Settings – Default Search Provider | [Default search provider enabled](/deployedge/microsoft-edge-mobile-policies#defaultsearchproviderenabled) | DefaultSearchProviderEnabled | true |
|  | [Default search provider name](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidername) | DefaultSearchProviderName | Preferred Company Search |
|  | [Default search provider search URL](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidersearchurl) | DefaultSearchProviderSearchURL | `https://search.company.com?q={searchTerms}` |
|  | [Default search provider suggest URL](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidersuggesturl) | DefaultSearchProviderSuggestURL | `https://search.company.com/suggest?q={searchTerms}` |
|  | [Default search provider keyword](/deployedge/microsoft-edge-mobile-policies#defaultsearchproviderkeyword) | DefaultSearchProviderKeyword | company |

7. Expand **Edge configuration settings** and configure:

| Category | Setting | Value |
|-----------|----------|-------|
| Edge Configuration Settings | Allowed URLs | Leave empty (Level 2 uses blocked URLs instead – when blocked URLs are configured, allowed URLs field becomes unavailable) |
|  | Blocked URLs | *.facebook.com, *.twitter.com, *.instagram.com, *.tiktok.com |
|  | Redirect restricted sites to personal context | Enable |

7. Select **Next**.  
8. In **Assignments**, assign to **SEB-Level2-Users** group.  
9. Select **Next** to review the settings. Then choose **Create** when you're done.  

### Level 3 – High security mobile configuration for iOS

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Apps** > **Manage apps** > **Configuration** > **Create** > **Managed apps**.  
3. On the **Basics** tab:  
   - **Name:** Level 3 – High security mobile configuration – iOS ACP  
   - **Description:** Maximum security browser configuration for Microsoft Edge on iOS.  
4. In **Target policy to**, select **Selected apps**.  
   - Choose **+ Select public apps**.  
   - In the **Select apps to target** panel, search for and select **Microsoft Edge (iOS/iPadOS)**, then select **Select**.  
5. Select **Next**.  
6. On the **Settings** step, expand **General configuration settings** and configure:

#### General configuration settings

| Category | Setting | Name | Value |
|---------|---------|------|-------|
| General Configuration Settings | [Password single sign-on](https://learn.microsoft.com/en-us/microsoft-365/solutions/apps-config-step-4?view=o365-worldwide#general-app-configuration-settings) | com.microsoft.intune.mam.managedbrowser.PasswordSSO | false |
|  | [SmartScreen enabled](/deployedge/microsoft-edge-mobile-policies#smartscreenenabled) | com.microsoft.intune.mam.managedbrowser.SmartScreenEnabled | true |
|  | [Enable EdgeMyApps](/deployedge/microsoft-edge-mobile-policies#edgemyapps) | EdgeMyApps | false |
|  | [Default HTTPS enforced](/deployedge/microsoft-edge-mobile-policies#edgedefaulthttps) | EdgeDefaultHTTPS | true |
|  | [Disable sharing usage data](/deployedge/microsoft-edge-mobile-policies#edgedisableshareusagedata) | EdgeDisableShareUsageData | true |
|  | [Disable password manager](/deployedge/microsoft-edge-mobile-policies#passwordmanagerenabled) | PasswordManagerEnabled | false |
|  | [Disable search suggestions](/deployedge/microsoft-edge-mobile-policies#searchsuggestenabled) | SearchSuggestEnabled | false |
|  | [Hide first run experience](/deployedge/microsoft-edge-mobile-policies#hidefirstrunexperience) | HideFirstRunExperience | true |
|  | [Disable pop-ups](/deployedge/microsoft-edge-mobile-policies#defaultpopupssetting) | DefaultPopupsSetting | 2 |
|  | [Disable sync](/deployedge/microsoft-edge-mobile-policies#edgesyncdisabled) | EdgeSyncDisabled | true |
|  | [Disable password import](/deployedge/microsoft-edge-mobile-policies#edgeimportpasswordsdisabled) | EdgeImportPasswordsDisabled | true |
|  | [Disable Copilot](/deployedge/microsoft-edge-mobile-policies#edgecopilotenabled) | EdgeCopilotEnabled | false |
|  | [Default browser setting enabled](/deployedge/microsoft-edge-mobile-policies#defaultbrowsersettingenabled) | DefaultBrowserSettingEnabled | false |
|  | [Experimentation and configuration service control](/deployedge/microsoft-edge-mobile-policies#experimentationandconfigurationservicecontrol) | ExperimentationAndConfigurationServiceControl | 0 |
| General Configuration Settings – Additional | [Disable InPrivate mode](/deployedge/microsoft-edge-mobile-policies#inprivatemodeavailability) | InPrivateModeAvailability | 1 |
|  | [Disable browser history saving](/deployedge/microsoft-edge-mobile-policies#savingbrowserhistorydisabled) | SavingBrowserHistoryDisabled | true |
|  | [Translate enabled](/deployedge/microsoft-edge-mobile-policies#translateenabled) | TranslateEnabled | false |
|  | [Disable shared device support](/deployedge/microsoft-edge-mobile-policies#edgeshareddevicesupportenabled) | EdgeSharedDeviceSupportEnabled | false |
|  | [Disable SSL error override](/deployedge/microsoft-edge-mobile-policies#sslerroroverrideallowed) | SSLErrorOverrideAllowed | false |
| General Configuration Settings – Password Manager and Protection | [Biometric authentication before filling](/deployedge/microsoft-edge-browser-policies/biometricauthenticationbeforefilling) | BiometricAuthenticationBeforeFilling | true |
| General Configuration Settings – Organizational Branding Configuration | [Organizational branding – logo](/deployedge/microsoft-edge-mobile-policies#edgebrandlogo) | EdgeBrandLogo | true |
|  | [Organizational branding – color](/deployedge/microsoft-edge-mobile-policies#edgebrandcolor) | EdgeBrandColor | #0078d4 |
| General Configuration Settings – Manageability | [Disable features](/deployedge/microsoft-edge-mobile-policies#edgedisabledfeatures) | EdgeDisabledFeatures | inprivate\|autofill\|password\|translator\|readaloud\|drop\|coupons\|extensions\|copilot\|collections\|myapps\|share |
| General Configuration Settings – Identity and Sign-in | [Block Edge sign-in](/deployedge/microsoft-edge-browser-policies/edgeblocksigninenabled) | EdgeBlockSignInEnabled | true |
| General Configuration Settings – Default Search Provider | [Default search provider enabled](/deployedge/microsoft-edge-mobile-policies#defaultsearchproviderenabled) | DefaultSearchProviderEnabled | true |
|  | [Default search provider name](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidername) | DefaultSearchProviderName | Preferred Company Search |
|  | [Default search provider search URL](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidersearchurl) | DefaultSearchProviderSearchURL | `https://search.company.com?q={searchTerms}` |
|  | [Default search provider suggest URL](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidersuggesturl) | DefaultSearchProviderSuggestURL | `https://search.company.com/suggest?q={searchTerms}` |
|  | [Default search provider keyword](/deployedge/microsoft-edge-mobile-policies#defaultsearchproviderkeyword) | DefaultSearchProviderKeyword | company |

8. Expand **Edge configuration settings** and configure:

| Category | Setting | Value |
|-----------|----------|-------|
| Edge Configuration Settings | Allowed URLs | *.company.com, *.microsoft.com, login.microsoftonline.com |
|  | Blocked URLs | Leave empty (Level 3 uses allowed URLs – when allowed URLs are configured, blocked URLs field becomes unavailable) |

9. Per-App VPN (optional): Integrate with Microsoft Tunnel if required for isolated secure traffic routing
10. Select **Next**.  
11. In **Assignments**, assign to **SEB-Level3-Users** group.  
12. Select **Next** to review the settings. Then choose **Create** when you're done.  

### Validation (All iOS Levels)

#### Policy Application

In the Intune admin center, navigate to **Devices** > **Apple mobile** > select a device > **Device configuration** > **View report**.
Confirm the policy status shows **Succeeded**.

#### Device Verification

On an iOS device:

1. Open the **Company Portal** app.  
2. Tap **Devices** > select the managed device > **Check status** to force a sync.  
3. After syncing, open **Microsoft Edge**.  
4. Tap the **ellipsis (···)** menu > **Settings**.  
5. Verify that managed configurations—such as homepage, search provider, password manager, and default browser setting—match the applied policy.

> **Note:** App configuration policies only apply when the user signs into Edge with their work or school (Entra ID) account. If settings haven’t applied, confirm the correct account is in use.

#### Feature Testing

- **Level 1:**  
  - Verify homepage and search provider match corporate settings.  
  - Confirm **SmartScreen** is active and pop-ups are blocked.  
  - Confirm users can sign in and general browsing functions normally.  

- **Level 2:**  
  - Verify that **sync**, **password import**, and **Copilot** are disabled.  
  - Attempt to autofill or save passwords—confirm it’s blocked.  
  - Confirm **Biometric authentication before filling** works as intended.  
  - Validate **InPrivate** browsing reflects the configured policy state.  

- **Level 3:**  
  - Attempt to open a non-allowlisted site—confirm it’s blocked or redirected.  
  - Confirm **InPrivate** browsing is unavailable.  
  - Validate **browser history saving**, **shared device support**, and **Copilot** are disabled.  
  - Confirm that disabled features (for example, **Extensions**, **Collections**, or **Drop**) don’t appear in Settings.

::: zone-end

## Next steps

Continue to [Step 5](mamedge-5-settings-catalog.md) to configure Settings Catalog policies for enrolled Windows and macOS devices.