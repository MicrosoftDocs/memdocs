---
title: Step 4. Create App Configuration Policies for Microsoft Edge for Business
description: Step 4. Create app configuration policies for Microsoft Edge for Business across Windows, Android, and iOS platforms.
ms.date: 01/15/2025
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
> - [Microsoft Edge Browser Policies](/deployedge/microsoft-edge-policies)
> - [Windows App Configuration Policies](app-configuration-policies-overview.md)
> - [Managed App Configuration for Windows](app-configuration-policies-managed-app.md)

**Prerequisites:**

- Windows 11
- Microsoft Edge installed
- Intune enrollment or MAM managed
- User Entra ID account

### Level 1 - Basic browser configuration for Windows

Level 1 configuration provides foundational browser security controls while maintaining user productivity.

1. Go to the [Microsoft Intune admin center](https://intune.microsoft.com/).  
2. Select **Apps** > **Manage apps** > **Configuration** > **Create** > **Managed apps**.  
3. On the **Basics** tab, enter:  
   - **Name:** Level 1 – Basic browser configuration – Windows ACP  
   - **Description:** Basic browser customization for Microsoft Edge on Windows.
4. In **Target policy to**, select **Selected apps**.  
   - Choose **+ Select public apps**.  
   - In the **Select apps to target** panel, search for and select **Microsoft Edge Windows**, then select **Select**.  
5. Select **Next**.  
6. On the **Settings** step, expand **General configuration settings**.  
7. Configure each setting using the **Name** and **Value** specified:

| Name | Value | Documentation |
|------|--------|----------------|
| HomepageLocation | `https://portal.company.com` | [Configure the home page URL](/deployedge/microsoft-edge-browser-policies/homepagelocation) |
| ShowHomeButton | Enabled | [Show Home button on toolbar](/deployedge/microsoft-edge-browser-policies/showhomebutton) |
| NewTabPageLocation | `https://portal.company.com` | [Configure the new tab page URL](/deployedge/microsoft-edge-browser-policies/newtabpagelocation) |
| RestoreOnStartup | Open the new tab page (5) | [Action to take on startup](/deployedge/microsoft-edge-browser-policies/restoreonstartup) |
| HTTPSOnlyMode | Enabled | [Configure Automatic HTTPS](/deployedge/microsoft-edge-browser-policies/httpsonlymode) |
| DefaultPopupsSetting | Do not allow popups (2) | [Default pop-up window setting](/deployedge/microsoft-edge-browser-policies/defaultpopupssetting) |
| PasswordManagerEnabled | Disabled | [Enable saving passwords to the password manager](/deployedge/microsoft-edge-browser-policies/passwordmanagerenabled) |
| AutofillAddressEnabled | Disabled | [Enable AutoFill for addresses](/deployedge/microsoft-edge-browser-policies/autofilladdressenabled) |
| AutofillCreditCardEnabled | Disabled | [Enable Autofill for payment instructions](/deployedge/microsoft-edge-browser-policies/autofillcreditcardenabled) |
| TrackingPrevention | Balanced (2) | [Block tracking of users' web-browsing activity](/deployedge/microsoft-edge-browser-policies/trackingprevention) |
| DefaultSearchProviderEnabled | Enabled | [Enable the default search provider](/deployedge/microsoft-edge-browser-policies/defaultsearchproviderenabled) |
| DefaultSearchProviderName | Microsoft Bing | [Default search provider name](/deployedge/microsoft-edge-browser-policies/defaultsearchprovidername) |
| DefaultSearchProviderSearchURL | `https://www.bing.com/search?q={searchTerms}` | [Default search provider search URL](/deployedge/microsoft-edge-browser-policies/defaultsearchprovidersearchurl) |
| SearchSuggestEnabled | Disabled | [Enable search suggestions](/deployedge/microsoft-edge-browser-policies/searchsuggestenabled) |
| NetworkPredictionOptions | Don't predict (2) | [Enable network prediction](/deployedge/microsoft-edge-browser-policies/networkpredictionoptions) |
| ImportAutofillFormData | Disabled | [Allow importing of autofill form data](/deployedge/microsoft-edge-browser-policies/importautofillformdata) |
| ImportSavedPasswords | Disabled | [Allow importing of saved passwords](/deployedge/microsoft-edge-browser-policies/importsavedpasswords) |
| ImportBrowsingHistory | Disabled | [Allow importing of browsing history](/deployedge/microsoft-edge-browser-policies/importhistory) |
| ImportCookies | Disabled | [Allow importing cookies](/deployedge/microsoft-edge-browser-policies/importcookies) |
| ImportExtensions | Disabled | [Allow importing of extension](/deployedge/microsoft-edge-browser-policies/importextensions) |
| ExtensionInstallBlocklist | `["external_component", "external_pref", "external_registry"]` | [Control which extensions cannot be installed](/deployedge/microsoft-edge-browser-policies/extensioninstallblocklist) |
| ExtensionAllowedTypes | `["extension", "theme"]` | [Configure allowed extension types](/deployedge/microsoft-edge-browser-policies/extensionallowedtypes) |
| ExtensionInstallSources | `[https://corp.contoso.com/*]` | [Configure extension and user script install sources](/deployedge/microsoft-edge-browser-policies/extensioninstallsources) |
| DefaultDownloadDirectory | `${user_home}/Downloads/Edge` | [Set download directory](/deployedge/microsoft-edge-browser-policies/downloaddirectory) |
| PromptForDownloadLocation | Enabled | [Ask where to save downloaded files](/deployedge/microsoft-edge-browser-policies/promptfordownloadlocation) |
| DownloadRestrictions | Block malicious downloads and dangerous file types | [Allow download restrictions](/deployedge/microsoft-edge-browser-policies/downloadrestrictions) |
| HubsSidebarEnabled | Disabled | [Show Hubs Sidebar](/deployedge/microsoft-edge-browser-policies/hubssidebarenabled) |
| ShowMicrosoftRewards | Disabled | [Show Microsoft Rewards experiences](/deployedge/microsoft-edge-browser-policies/showmicrosoftrewards) |
| EdgeShoppingAssistantEnabled | Disabled | [Shopping in Microsoft Edge Enabled](/deployedge/microsoft-edge-browser-policies/edgeshoppingassistantenabled) |
| EdgeWorkspacesEnabled | Enabled | [Edge Workspaces](/deployedge/microsoft-edge-browser-policies/edgeworkspacesenabled) |
| FavoritesBarEnabled | Enabled | [Show favorites bar](/deployedge/microsoft-edge-browser-policies/favoritesbarenabled) |
| AllowDeletingBrowserHistory | Enabled | [Enable deleting browser and download history](/deployedge/microsoft-edge-browser-policies/allowdeletingbrowserhistory) |

8. Select **Next**.  
9. For **Assignments**, assign to **SEB-Level1-Users** group.  
10. Select **Next** to review the settings. Then choose **Create**.

### Level 2 - Enhanced browser configuration for Windows

Level 2 configuration adds enhanced security controls and restrictions for sensitive environments.

1. Go to the [Microsoft Intune admin center](https://intune.microsoft.com/).  
2. Select **Apps** > **Manage apps** > **Configuration** > **Create** > **Managed apps**.  
3. On the **Basics** tab, enter:  
   - **Name:** Level 2 – Enhanced browser configuration – Windows ACP  
   - **Description:** Enhanced browser configuration with additional security controls for Microsoft Edge on Windows.  
4. In **Target policy to**, select **Selected apps**.  
   - Choose **+ Select public apps**.  
   - In the **Select apps to target** panel, search for and select **Microsoft Edge Windows**, then select **Select**.  
5. Select **Next**.  
6. On the **Settings** step, expand **General configuration settings**.  
7. Configure each setting using the **Name** and **Value** specified:

| Name | Value | Documentation |
|------|-------|---------------|
| HomepageLocation | `https://portal.company.com` | [Configure the home page URL](/deployedge/microsoft-edge-browser-policies/homepagelocation) |
| ShowHomeButton | Enabled | [Show Home button on toolbar](/deployedge/microsoft-edge-browser-policies/showhomebutton) |
| NewTabPageLocation | `https://portal.company.com` | [Configure the new tab page URL](/deployedge/microsoft-edge-browser-policies/newtabpagelocation) |
| RestoreOnStartup | Open the new tab page (5) | [Action to take on startup](/deployedge/microsoft-edge-browser-policies/restoreonstartup) |
| HTTPSOnlyMode | Enabled | [Configure Automatic HTTPS](/deployedge/microsoft-edge-browser-policies/httpsonlymode) |
| DefaultPopupsSetting | Do not allow popups (2) | [Default pop-up window setting](/deployedge/microsoft-edge-browser-policies/defaultpopupssetting) |
| PasswordManagerEnabled | Disabled | [Enable saving passwords to the password manager](/deployedge/microsoft-edge-browser-policies/passwordmanagerenabled) |
| AutofillAddressEnabled | Disabled | [Enable AutoFill for addresses](/deployedge/microsoft-edge-browser-policies/autofilladdressenabled) |
| AutofillCreditCardEnabled | Disabled | [Enable Autofill for payment instructions](/deployedge/microsoft-edge-browser-policies/autofillcreditcardenabled) |
| TrackingPrevention | Balanced (2) | [Block tracking of users' web-browsing activity](/deployedge/microsoft-edge-browser-policies/trackingprevention) |
| DefaultSearchProviderEnabled | Enabled | [Enable the default search provider](/deployedge/microsoft-edge-browser-policies/defaultsearchproviderenabled) |
| DefaultSearchProviderName | Microsoft Bing | [Default search provider name](/deployedge/microsoft-edge-browser-policies/defaultsearchprovidername) |
| DefaultSearchProviderSearchURL | `https://www.bing.com/search?q={searchTerms}` | [Default search provider search URL](/deployedge/microsoft-edge-browser-policies/defaultsearchprovidersearchurl) |
| SearchSuggestEnabled | Disabled | [Enable search suggestions](/deployedge/microsoft-edge-browser-policies/searchsuggestenabled) |
| NetworkPredictionOptions | Don't predict (2) | [Enable network prediction](/deployedge/microsoft-edge-browser-policies/networkpredictionoptions) |
| ImportAutofillFormData | Disabled | [Allow importing of autofill form data](/deployedge/microsoft-edge-browser-policies/importautofillformdata) |
| ImportSavedPasswords | Disabled | [Allow importing of saved passwords](/deployedge/microsoft-edge-browser-policies/importsavedpasswords) |
| ImportBrowsingHistory | Disabled | [Allow importing of browsing history](/deployedge/microsoft-edge-browser-policies/importhistory) |
| ImportCookies | Disabled | [Allow importing cookies](/deployedge/microsoft-edge-browser-policies/importcookies) |
| ImportExtensions | Disabled | [Allow importing of extension](/deployedge/microsoft-edge-browser-policies/importextensions) |
| ExtensionInstallBlocklist | `["external_component", "external_pref", "external_registry"]` | [Control which extensions cannot be installed](/deployedge/microsoft-edge-browser-policies/extensioninstallblocklist) |
| ExtensionAllowedTypes | `["extension", "theme"]` | [Configure allowed extension types](/deployedge/microsoft-edge-browser-policies/extensionallowedtypes) |
| ExtensionInstallSources | `[https://corp.contoso.com/*]` | [Configure extension and user script install sources](/deployedge/microsoft-edge-browser-policies/extensioninstallsources) |
| DefaultDownloadDirectory | `${user_home}/Downloads/Edge` | [Set download directory](/deployedge/microsoft-edge-browser-policies/downloaddirectory) |
| PromptForDownloadLocation | Enabled | [Ask where to save downloaded files](/deployedge/microsoft-edge-browser-policies/promptfordownloadlocation) |
| DownloadRestrictions | Block malicious downloads and dangerous file types | [Allow download restrictions](/deployedge/microsoft-edge-browser-policies/downloadrestrictions) |
| HubsSidebarEnabled | Disabled | [Show Hubs Sidebar](/deployedge/microsoft-edge-browser-policies/hubssidebarenabled) |
| ShowMicrosoftRewards | Disabled | [Show Microsoft Rewards experiences](/deployedge/microsoft-edge-browser-policies/showmicrosoftrewards) |
| EdgeShoppingAssistantEnabled | Disabled | [Shopping in Microsoft Edge Enabled](/deployedge/microsoft-edge-browser-policies/edgeshoppingassistantenabled) |
| EdgeWorkspacesEnabled | Enabled | [Edge Workspaces](/deployedge/microsoft-edge-browser-policies/edgeworkspacesenabled) |
| FavoritesBarEnabled | Enabled | [Show favorites bar](/deployedge/microsoft-edge-browser-policies/favoritesbarenabled) |
| AllowDeletingBrowserHistory | Enabled | [Enable deleting browser and download history](/deployedge/microsoft-edge-browser-policies/allowdeletingbrowserhistory) |
| SmartScreenForTrustedDownloadsEnabled | Enabled | [Force Microsoft Defender SmartScreen checks on downloads from trusted sources](/deployedge/microsoft-edge-browser-policies/smartscreenfortrusteddownloadsenabled) |
| InsecureContentAllowedForUrls | `[]` | [Allow insecure content on specified sites](/deployedge/microsoft-edge-browser-policies/insecurecontentallowedforurls) |
| InsecureContentBlockedForUrls | `["*"]` | [Block insecure content on specified sites](/deployedge/microsoft-edge-browser-policies/insecurecontentblockedforurls) |
| ExtensionInstallAllowlist | `[]` | [Allow specific extensions to be installed](/deployedge/microsoft-edge-browser-policies/extensioninstallallowlist) |
| ExtensionInstallForcelist | `[]` | [Control which extensions are installed silently](/deployedge/microsoft-edge-browser-policies/extensioninstallforcelist) |
| ExtensionSettings | `{"*":{"installation_mode":"blocked"}}` | [Configure extension management settings](/deployedge/microsoft-edge-browser-policies/extensionsettings) |
| NativeMessagingAllowlist | `[]` | [Control which native messaging hosts users can use](/deployedge/microsoft-edge-browser-policies/nativemessagingallowlist) |
| NativeMessagingHostBlocklist | `["*"]` | [Configure native messaging block list](/deployedge/microsoft-edge-browser-policies/nativemessagingblocklist) |
| AutoSelectCertificateForUrls | `["*.company.com"]` | [Automatically select client certificates for these sites](/deployedge/microsoft-edge-browser-policies/autoselectcertificateforurls) |
| WebRtcUdpPortRange | 10000:11000 | [Restrict the range of local UDP ports used by WebRTC](/deployedge/microsoft-edge-browser-policies/webrtcudpportrange) |
| DefaultImagesSetting | Allow images (1) | [Default images setting](/deployedge/microsoft-edge-browser-policies/defaultimagessetting) |
| DefaultJavaScriptSetting | Allow JavaScript (1) | [Default JavaScript setting](/deployedge/microsoft-edge-browser-policies/defaultjavascriptsetting) |
| ClearBrowsingDataOnExit | Enabled | [Clear browsing data when Microsoft Edge closes](/deployedge/microsoft-edge-browser-policies/clearbrowsingdataonexit) |
| SyncDisabled | Enabled | [Disable synchronization of data using Microsoft sync services](/deployedge/microsoft-edge-browser-policies/syncdisabled) |
| PrintingEnabled | Enabled | [Enable printing](/deployedge/microsoft-edge-browser-policies/printingenabled) |
| InPrivateModeAvailability | InPrivate mode available (0) | [InPrivate mode availability](/deployedge/microsoft-edge-browser-policies/inprivatemodeavailability) |
| ForceSync | Disabled | [Force synchronization of browser data and do not show the sync consent prompt](/deployedge/microsoft-edge-browser-policies/forcesync) |
| SleepingTabsEnabled | Enabled | [Configure sleeping tabs](/deployedge/microsoft-edge-browser-policies/sleepingtabsenabled) |
| SearchSuggestEnabled | Disabled | [Enable search suggestions](/deployedge/microsoft-edge-browser-policies/searchsuggestenabled) |
| LocalProvidersEnabled | Disabled | [Allow suggestions from local providers](/deployedge/microsoft-edge-browser-policies/localprovidersenabled) |
| VideoCaptureAllowed | Disabled | [Allow or block video capture](/deployedge/microsoft-edge-browser-policies/videocaptureallowed) |
| DefaultNotificationsSetting | Block (2) | [Default notification setting](/deployedge/microsoft-edge-browser-policies/defaultnotificationssetting) |
| DefaultGeolocationSetting | Don't allow sites to track users' physical location (2) | [Default geolocation setting](/deployedge/microsoft-edge-browser-policies/defaultgeolocationsetting) |
| WebUsbAllowDevicesForUrls | `[]` | [Allow WebUSB on specific sites](/deployedge/microsoft-edge-browser-policies/webusballowdevicesforurls) |
| WebUsbBlockedForUrls | `[{"urls": ["*"], "devices": [{"vendor_id": "*", "product_id": "*"}]}]` | [Block WebUSB on specific sites](/deployedge/microsoft-edge-browser-policies/webusbblockedforurls) |
| WebRtcLocalhostIpHandling | Disable non-proxied UDP (default_public_interface_only) | [Restrict exposure of local IP address by WebRTC](/deployedge/microsoft-edge-browser-policies/webrtclocalhostiphandling) |

8. Select **Next**.  
9. For **Assignments**, assign to **SEB-Level2-Users** group.  
10. Select **Next** to review the settings. Then choose **Create**.

### Level 3 - High security configuration for Windows

Level 3 configuration enforces maximum security with zero-trust controls and comprehensive data-loss prevention.

1. Go to the [Microsoft Intune admin center](https://intune.microsoft.com/).  
2. Select **Apps** > **Manage apps** > **Configuration** > **Create** > **Managed apps**.  
3. On the **Basics** tab, enter:  
   - **Name:** Level 3 – High security configuration – Windows ACP  
   - **Description:** Maximum security browser configuration with zero-trust controls and comprehensive data-loss prevention for Microsoft Edge on Windows.  
4. In **Target policy to**, select **Selected apps**.  
   - Choose **+ Select public apps**.  
   - In the **Select apps to target** panel, search for and select **Microsoft Edge Windows**, then select **Select**.  
5. Select **Next**.  
6. On the **Settings** step, expand **General configuration settings**.  
7. Configure each setting using the **Name** and **Value** specified:

    | Name | Value | Documentation |
    |------|-------|---------------|
    | HomepageLocation | `https://portal.company.com` | [Configure the home page URL](/deployedge/microsoft-edge-browser-policies/homepagelocation) |
    | ShowHomeButton | Enabled | [Show Home button on toolbar](/deployedge/microsoft-edge-browser-policies/showhomebutton) |
    | NewTabPageLocation | `https://portal.company.com` | [Configure the new tab page URL](/deployedge/microsoft-edge-browser-policies/newtabpagelocation) |
    | RestoreOnStartup | Open the new tab page (5) | [Action to take on startup](/deployedge/microsoft-edge-browser-policies/restoreonstartup) |
    | HTTPSOnlyMode | Enabled | [Configure Automatic HTTPS](/deployedge/microsoft-edge-browser-policies/httpsonlymode) |
    | DefaultPopupsSetting | Do not allow popups (2) | [Default pop-up window setting](/deployedge/microsoft-edge-browser-policies/defaultpopupssetting) |
    | PasswordManagerEnabled | Disabled | [Enable saving passwords to the password manager](/deployedge/microsoft-edge-browser-policies/passwordmanagerenabled) |
    | AutofillAddressEnabled | Disabled | [Enable AutoFill for addresses](/deployedge/microsoft-edge-browser-policies/autofilladdressenabled) |
    | AutofillCreditCardEnabled | Disabled | [Enable Autofill for payment instructions](/deployedge/microsoft-edge-browser-policies/autofillcreditcardenabled) |
    | TrackingPrevention | Balanced (2) | [Block tracking of users' web-browsing activity](/deployedge/microsoft-edge-browser-policies/trackingprevention) |
    | DefaultSearchProviderEnabled | Enabled | [Enable the default search provider](/deployedge/microsoft-edge-browser-policies/defaultsearchproviderenabled) |
    | DefaultSearchProviderName | Microsoft Bing | [Default search provider name](/deployedge/microsoft-edge-browser-policies/defaultsearchprovidername) |
    | DefaultSearchProviderSearchURL | `https://www.bing.com/search?q={searchTerms}` | [Default search provider search URL](/deployedge/microsoft-edge-browser-policies/defaultsearchprovidersearchurl) |
    | SearchSuggestEnabled | Disabled | [Enable search suggestions](/deployedge/microsoft-edge-browser-policies/searchsuggestenabled) |
    | ImportAutofillFormData | Disabled | [Allow importing of autofill form data](/deployedge/microsoft-edge-browser-policies/importautofillformdata) |
    | ImportSavedPasswords | Disabled | [Allow importing of saved passwords](/deployedge/microsoft-edge-browser-policies/importsavedpasswords) |
    | ImportBrowsingHistory | Disabled | [Allow importing of browsing history](/deployedge/microsoft-edge-browser-policies/importhistory) |
    | ImportCookies | Disabled | [Allow importing cookies](/deployedge/microsoft-edge-browser-policies/importcookies) |
    | ImportExtensions | Disabled | [Allow importing of extension](/deployedge/microsoft-edge-browser-policies/importextensions) |
    | ExtensionInstallBlocklist | `["external_component", "external_pref", "external_registry"]` | [Control which extensions cannot be installed](/deployedge/microsoft-edge-browser-policies/extensioninstallblocklist) |
    | ExtensionAllowedTypes | `["extension", "theme"]` | [Configure allowed extension types](/deployedge/microsoft-edge-browser-policies/extensionallowedtypes) |
    | ExtensionInstallSources | `[https://corp.contoso.com/*]` | [Configure extension and user script install sources](/deployedge/microsoft-edge-browser-policies/extensioninstallsources) |
    | DefaultDownloadDirectory | `${user_home}/Downloads/Edge` | [Set download directory](/deployedge/microsoft-edge-browser-policies/downloaddirectory) |
    | PromptForDownloadLocation | Enabled | [Ask where to save downloaded files](/deployedge/microsoft-edge-browser-policies/promptfordownloadlocation) |
    | HubsSidebarEnabled | Disabled | [Show Hubs Sidebar](/deployedge/microsoft-edge-browser-policies/hubssidebarenabled) |
    | ShowMicrosoftRewards | Disabled | [Show Microsoft Rewards experiences](/deployedge/microsoft-edge-browser-policies/showmicrosoftrewards) |
    | EdgeShoppingAssistantEnabled | Disabled | [Shopping in Microsoft Edge Enabled](/deployedge/microsoft-edge-browser-policies/edgeshoppingassistantenabled) |
    | EdgeWorkspacesEnabled | Enabled | [Edge Workspaces](/deployedge/microsoft-edge-browser-policies/edgeworkspacesenabled) |
    | FavoritesBarEnabled | Enabled | [Show favorites bar](/deployedge/microsoft-edge-browser-policies/favoritesbarenabled) |
    | AllowDeletingBrowserHistory | Enabled | [Enable deleting browser and download history](/deployedge/microsoft-edge-browser-policies/allowdeletingbrowserhistory) |
    | SmartScreenForTrustedDownloadsEnabled | Enabled | [Force Microsoft Defender SmartScreen checks on downloads from trusted sources](/deployedge/microsoft-edge-browser-policies/smartscreenfortrusteddownloadsenabled) |
    | InsecureContentAllowedForUrls | [] | [Allow insecure content on specified sites](/deployedge/microsoft-edge-browser-policies/insecurecontentallowedforurls) |
    | InsecureContentBlockedForUrls | ["*"] | [Block insecure content on specified sites](/deployedge/microsoft-edge-browser-policies/insecurecontentblockedforurls) |
    | ExtensionInstallAllowlist | [] | [Allow specific extensions to be installed](/deployedge/microsoft-edge-browser-policies/extensioninstallallowlist) |
    | ExtensionInstallForcelist | [] | [Control which extensions are installed silently](/deployedge/microsoft-edge-browser-policies/extensioninstallforcelist) |
    | ExtensionSettings | {"*":{"installation_mode":"blocked"}} | [Configure extension management settings](/deployedge/microsoft-edge-browser-policies/extensionsettings) |
    | NativeMessagingAllowlist | [] | [Control which native messaging hosts users can use](/deployedge/microsoft-edge-browser-policies/nativemessagingallowlist) |
    | NativeMessagingBlocklist | ["*"] | [Configure native messaging block list](/deployedge/microsoft-edge-browser-policies/nativemessagingblocklist) |
    | AutoSelectCertificateForUrls | ["*.company.com"] | [Automatically select client certificates for these sites](/deployedge/microsoft-edge-browser-policies/autoselectcertificateforurls) |
    | WebRtcUdpPortRange | 10000:11000 | [Restrict the range of local UDP ports used by WebRTC](/deployedge/microsoft-edge-browser-policies/webrtcudpportrange) |
    | DefaultImagesSetting | Allow images (1) | [Default images setting](/deployedge/microsoft-edge-browser-policies/defaultimagessetting) |
    | DefaultJavaScriptSetting | Allow JavaScript (1) | [Default JavaScript setting](/deployedge/microsoft-edge-browser-policies/defaultjavascriptsetting) |
    | SyncDisabled | Enabled | [Disable synchronization of data using Microsoft sync services](/deployedge/microsoft-edge-browser-policies/syncdisabled) |
    | ForceSync | Disabled | [Force synchronization of browser data and do not show the sync consent prompt](/deployedge/microsoft-edge-browser-policies/forcesync) |
    | SleepingTabsEnabled | Enabled | [Configure sleeping tabs](/deployedge/microsoft-edge-browser-policies/sleepingtabsenabled) |
    | SearchSuggestEnabled | Disabled | [Enable search suggestions](/deployedge/microsoft-edge-browser-policies/searchsuggestenabled) |
    | LocalProvidersEnabled | Disabled | [Allow suggestions from local providers](/deployedge/microsoft-edge-browser-policies/localprovidersenabled) |
    | DefaultNotificationsSetting | Block (2) | [Default notification setting](/deployedge/microsoft-edge-browser-policies/defaultnotificationssetting) |
    | DefaultGeolocationSetting | Don't allow sites to track users' physical location (2) | [Default geolocation setting](/deployedge/microsoft-edge-browser-policies/defaultgeolocationsetting) |
    | WebUsbBlockedForUrls | [] | [Allow WebUSB on specific sites](/deployedge/microsoft-edge-browser-policies/webusballowdevicesforurls) |
    | WebUsbBlockDevicesForUrls | [{"urls":["*"],"devices":[{"vendor_id":"*","product_id":"*"}]}] | [Block WebUSB on specific sites](/deployedge/microsoft-edge-browser-policies/webusbblockedforurls) |
    | WebRtcLocalhostIpHandling | Disable non-proxied UDP (default_public_interface_only) | [Restrict exposure of local IP address by WebRTC](/deployedge/microsoft-edge-browser-policies/webrtclocalhostiphandling) |
    | URLAllowlist | ["*.company.com", "*.microsoft.com", "*.office.com"] | [Define a list of allowed URLs](/deployedge/microsoft-edge-browser-policies/urlallowlist) |
    | URLBlocklist | ["*"] | [Block access to a list of URLs](/deployedge/microsoft-edge-browser-policies/urlblocklist) |
    | CookiesAllowedForUrls | ["*.company.com"] | [Allow cookies on specific sites](/deployedge/microsoft-edge-browser-policies/cookiesallowedforurls) |
    | CookiesBlockedForUrls | ["*"] | [Block cookies on specific sites](/deployedge/microsoft-edge-browser-policies/cookiesblockedforurls) |
    | CookiesSessionOnlyForUrls | ["*"] | [Limit cookies from specific websites to current session](/deployedge/microsoft-edge-browser-policies/cookiessessiononlyforurls) |
    | DownloadRestrictions | Block all downloads (4) | [Download restrictions](/deployedge/microsoft-edge-browser-policies/downloadrestrictions) |
    | ScreenCaptureAllowed | Disabled | [Allow or deny screen capture](/deployedge/microsoft-edge-browser-policies/screencaptureallowed) |
    | PrintingEnabled | Disabled | [Enable printing](/deployedge/microsoft-edge-browser-policies/printingenabled) |
    | DefaultClipboardSetting | Block clipboard (2) | [Default clipboard site permission](/deployedge/microsoft-edge-browser-policies/defaultclipboardsetting) |
    | VideoCaptureAllowed | Disabled | [Allow or block video capture](/deployedge/microsoft-edge-browser-policies/videocaptureallowed) |
    | InPrivateModeAvailability | InPrivate mode forced (2) | [Configure InPrivate mode availability](/deployedge/microsoft-edge-browser-policies/inprivatemodeavailability) |
    | ClearBrowsingDataOnExit | Enabled | [Clear browsing data when Microsoft Edge closes](/deployedge/microsoft-edge-browser-policies/clearbrowsingdataonexit) |
    | SavingBrowserHistoryDisabled | Enabled | [Disable saving browser history](/deployedge/microsoft-edge-browser-policies/savingbrowserhistorydisabled) |
    | DeveloperToolsAvailability | Disallowed (2) | [Control where developer tools can be used](/deployedge/microsoft-edge-browser-policies/developertoolsavailability) |
    | NetworkPredictionOptions | Don't predict (2) | [Enable network prediction](/deployedge/microsoft-edge-browser-policies/networkpredictionoptions) |
    | EdgeCollectionsEnabled | Disabled | [Enable the Collections feature](/deployedge/microsoft-edge-browser-policies/edgecollectionsenabled) |

8. Select **Next**.  
9. For **Assignments**, assign to **SEB-Level3-Users** group.  
10. Select **Next** to review the settings. Then choose **Create**.

### Validation (All Windows Levels)

#### Policy Application

- In the Intune admin center, verify the Settings Catalog, Security Baseline, APP, and ACP policy deployment status for the targeted Windows devices.

#### Endpoint Verification

- On the client device, open Microsoft Edge and navigate to `edge://policy`.
- Confirm that all configured policy keys appear with expected values and do not show an **Error** state.

#### URL and Feature Enforcement

- **Level 1:** Confirm core security controls are active, including SmartScreen, tracking prevention, and basic restriction settings.
- **Level 2:** Validate enhanced restrictions such as extension blocking, data sync restrictions, and clear-on-exit behaviors.
- **Level 3:** Attempt to browse to non-allowlisted URLs and verify they are blocked or isolated (for example, Application Guard).

#### Update Policies

- In `edge://policy`, search for **Update** to ensure the configured update behavior (for example, daily checks, suppressed hours, version pinning) matches the assigned security level.

#### Isolation Controls (Level 3 Only)

- Verify that high-risk or unapproved URLs trigger the expected isolation behavior, such as forced application isolation or a secure browsing container.

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

Level 1 configuration provides foundational browser security controls while maintaining user productivity.

1. Go to the [Microsoft Intune admin center](https://intune.microsoft.com/).  
2. Select **Apps** > **Manage apps** > **Configuration** > **Create** > **Managed apps**.  
3. On the **Basics** tab, enter:  
   - **Name:** Level 1 – Basic mobile browser configuration – Android ACP  
   - **Description:** Basic browser configuration for Microsoft Edge on Android.  
4. In **Target policy to**, select **Selected apps**.  
   - Choose **+ Select public apps**.  
   - In the **Select apps to target** panel, search for and select **Microsoft Edge (Android)**, then select **Select**.  
5. Select **Next**.  
6. On the **Settings** step, expand **General configuration settings**.  
7. Configure each setting using the **Name** and **Value** specified:

| Name | Value | Documentation |
|------|-------|---------------|
| com.microsoft.intune.mam.managedbrowser.PasswordSSO | true | [Microsoft Entra password single sign-on](manage-microsoft-edge.md#microsoft-entra-password-single-sign-on) |
| com.microsoft.intune.mam.managedbrowser.SmartScreenEnabled | true | [Microsoft Defender SmartScreen](manage-microsoft-edge.md#microsoft-defender-smartscreen) |
| EdgeMyApps | true | [Enable EdgeMyApps](/deployedge/microsoft-edge-mobile-policies#edgemyapps) |
| EdgeDefaultHTTPS | true | [Enforce default HTTPS](/deployedge/microsoft-edge-mobile-policies#edgedefaulthttps) |
| EdgeDisableShareUsageData | true | [Disable sharing usage data](/deployedge/microsoft-edge-mobile-policies#edgedisableshareusagedata) |
| EdgeImportPasswordsDisabled | false | [Disable password import](/deployedge/microsoft-edge-mobile-policies#edgeimportpasswordsdisabled) |
| EdgeNewTabPageLayout | 0 | [Configure new tab page layout](/deployedge/microsoft-edge-mobile-policies#edgenewtabpagelayout) |
| EdgeEnableKioskMode | false | [Enable kiosk mode](/deployedge/microsoft-edge-mobile-policies#edgeenablekioskmode) |
| EdgeShowAddressBarInKioskMode | true | [Show address bar in kiosk mode](/deployedge/microsoft-edge-mobile-policies#edgeshowaddressbarinkioskmode) |
| SmartScreenEnabled | true | [Enable SmartScreen](/deployedge/microsoft-edge-mobile-policies#smartscreenenabled) |
| SearchSuggestEnabled | false | [Enable search suggestions](/deployedge/microsoft-edge-mobile-policies#searchsuggestenabled) |
| TranslateEnabled | true | [Enable translate](/deployedge/microsoft-edge-mobile-policies#translateenabled) |
| HideFirstRunExperience | true | [Hide first run experience](/deployedge/microsoft-edge-mobile-policies#hidefirstrunexperience) |
| SSLErrorOverrideAllowed | true | [Allow SSL error override](/deployedge/microsoft-edge-mobile-policies#sslerroroverrideallowed) |
| DefaultBrowserSettingEnabled | true | [Enable as default browser](/deployedge/microsoft-edge-mobile-policies#defaultbrowsersettingenabled) |
| EdgeCopilotEnabled | true | [Enable Edge Copilot](/deployedge/microsoft-edge-mobile-policies#edgecopilotenabled) |
| EdgeSharedDeviceSupportEnabled | true | [Enable shared device support](/deployedge/microsoft-edge-mobile-policies#edgeshareddevicesupportenabled) |
| ExperimentationAndConfigurationServiceControl | 1 | [Experimentation and configuration service control](/deployedge/microsoft-edge-mobile-policies#experimentationandconfigurationservicecontrol) |
| DefaultPopupsSetting | 2 | [Default pop-ups setting](/deployedge/microsoft-edge-mobile-policies#defaultpopupssetting) |
| DefaultCookiesSetting | 1 | [Default cookies setting](/deployedge/microsoft-edge-mobile-policies#defaultcookiessetting) |
| BiometricAuthenticationBeforeFilling | false | [Biometric authentication before filling](/deployedge/microsoft-edge-browser-policies/biometricauthenticationbeforefilling) |
| PasswordManagerEnabled | false | [Enable password manager](/deployedge/microsoft-edge-mobile-policies#passwordmanagerenabled) |
| EdgeBrandLogo | true | [Enable Edge brand logo](/deployedge/microsoft-edge-mobile-policies#edgebrandlogo) |
| EdgeBrandColor | `#0078d4` | [Set Edge brand color](/deployedge/microsoft-edge-mobile-policies#edgebrandcolor) |
| DefaultSearchProviderEnabled | true | [Enable default search provider](/deployedge/microsoft-edge-mobile-policies#defaultsearchproviderenabled) |
| DefaultSearchProviderName | "Preferred Company Search" | [Default search provider name](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidername) |
| DefaultSearchProviderSearchURL | "https://search.company.com?q={searchTerms}" | [Default search provider search URL](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidersearchurl) |
| DefaultSearchProviderSuggestURL | "https://search.company.com/suggest?q={searchTerms}" | [Default search provider suggest URL](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidersuggesturl) |
| DefaultSearchProviderKeyword | "company" | [Default search provider keyword](/deployedge/microsoft-edge-mobile-policies#defaultsearchproviderkeyword) |
| ProxySettings | {"ProxyServer": "IP:Port", "ProxyBypassList": "*.company.com", "ProxyMode": "direct"} | [Configure proxy settings](/deployedge/microsoft-edge-browser-policies/proxysettings) |

8. Under Microsoft Tunnel for Mobile Application Management settings:

| Name | Value |
|------|-------|
| Tunnel enabled | Not configured |
| Connection name | Not configured |
| Microsoft Tunnel site | Not configured |
| Per-App VPN (Android only) | No Per-App VPN |
| Automatic configuration script | Not configured |
| Address | Not configured |
| Port Number | Not configured |
| Root Certificate | Not configured |

9. Expand **Edge configuration settings** and configure:

| Name | Value |
|------|-------|
| Application proxy redirection | Disable |
| Homepage shortcut URL | `https://www.company.com` |
| Managed bookmarks | Company Portal &#124; `https://portal.company.com` |
| Allowed URLs | Leave empty (Level 3 uses Allowed URLs) |
| Blocked URLs | Leave empty (Level 2 uses Blocked URLs) |
| Redirect restricted sites to personal context | Disable |

10. Select **Next**
11. In **Assignments**, assign to **SEB-Level1-Users** group.  
12. Select **Next** to review the settings. Then choose **Create**.

### Level 2 – Enhanced Mobile Browser Configuration for Android

Level 2 configuration adds enhanced security controls and restrictions for sensitive environments.

1. Go to the [Microsoft Intune admin center](https://intune.microsoft.com/).  
2. Select **Apps** > **Manage apps** > **Configuration** > **Create** > **Managed apps**.  
3. On the **Basics** tab, enter:  
   - **Name:** Level 2 – Enhanced mobile browser configuration – Android ACP  
   - **Description:** Enhanced browser configuration with additional security controls for Microsoft Edge on Android.  
4. In **Target policy to**, select **Selected apps**.  
   - Choose **+ Select public apps**.  
   - In the **Select apps to target** panel, search for and select **Microsoft Edge (Android)**, then select **Select**.  
5. Select **Next**.  
6. On the **Settings** step, expand **General configuration settings**.  
7. Configure each setting using the **Name** and **Value** specified:

| Name | Value | Documentation |
|------|-------|---------------|
| com.microsoft.intune.mam.managedbrowser.PasswordSSO | true | [Microsoft Entra password single sign-on](manage-microsoft-edge.md#microsoft-entra-password-single-sign-on) |
| com.microsoft.intune.mam.managedbrowser.SmartScreenEnabled | true | [Microsoft Defender SmartScreen](manage-microsoft-edge.md#microsoft-defender-smartscreen) |
| EdgeMyApps | true | [Enable EdgeMyApps](/deployedge/microsoft-edge-mobile-policies#edgemyapps) |
| EdgeDefaultHTTPS | true | [Enforce default HTTPS](/deployedge/microsoft-edge-mobile-policies#edgedefaulthttps) |
| EdgeDisableShareUsageData | true | [Disable sharing usage data](/deployedge/microsoft-edge-mobile-policies#edgedisableshareusagedata) |
| EdgeImportPasswordsDisabled | true | [Disable password import](/deployedge/microsoft-edge-mobile-policies#edgeimportpasswordsdisabled) |
| EdgeNewTabPageLayout | 1 | [Configure new tab page layout](/deployedge/microsoft-edge-mobile-policies#edgenewtabpagelayout) |
| EdgeEnableKioskMode | false | [Enable kiosk mode](/deployedge/microsoft-edge-mobile-policies#edgeenablekioskmode) |
| EdgeShowAddressBarInKioskMode | true | [Show address bar in kiosk mode](/deployedge/microsoft-edge-mobile-policies#edgeshowaddressbarinkioskmode) |
| SmartScreenEnabled | true | [Enable SmartScreen](/deployedge/microsoft-edge-mobile-policies#smartscreenenabled) |
| SearchSuggestEnabled | false | [Enable search suggestions](/deployedge/microsoft-edge-mobile-policies#searchsuggestenabled) |
| TranslateEnabled | true | [Enable translate](/deployedge/microsoft-edge-mobile-policies#translateenabled) |
| HideFirstRunExperience | true | [Hide first run experience](/deployedge/microsoft-edge-mobile-policies#hidefirstrunexperience) |
| SSLErrorOverrideAllowed | false | [Allow SSL error override](/deployedge/microsoft-edge-mobile-policies#sslerroroverrideallowed) |
| DefaultBrowserSettingEnabled | false | [Set as default browser](/deployedge/microsoft-edge-mobile-policies#defaultbrowsersettingenabled) |
| EdgeCopilotEnabled | false | [Enable Edge Copilot](/deployedge/microsoft-edge-mobile-policies#edgecopilotenabled) |
| EdgeSharedDeviceSupportEnabled | true | [Enable shared device support](/deployedge/microsoft-edge-mobile-policies#edgeshareddevicesupportenabled) |
| ExperimentationAndConfigurationServiceControl | 0 | [Experimentation and configuration service control](/deployedge/microsoft-edge-mobile-policies#experimentationandconfigurationservicecontrol) |
| EdgeSyncDisabled | true | [Disable browser sync](/deployedge/microsoft-edge-mobile-policies#edgesyncdisabled) |
| SavingBrowserHistoryDisabled | false | [Disable browser history saving](/deployedge/microsoft-edge-mobile-policies#savingbrowserhistorydisabled) |
| DefaultPopupsSetting | 2 | [Default pop-ups setting](/deployedge/microsoft-edge-mobile-policies#defaultpopupssetting) |
| DefaultCookiesSetting | 2 | [Default cookies setting](/deployedge/microsoft-edge-browser-policies/defaultcookiessetting) |
| BiometricAuthenticationBeforeFilling | true | [Biometric authentication before filling](/deployedge/microsoft-edge-browser-policies/biometricauthenticationbeforefilling) |
| PasswordManagerEnabled | false | [Enable password manager](/deployedge/microsoft-edge-mobile-policies#passwordmanagerenabled) |
| EdgeBrandLogo | true | [Enable Edge brand logo](/deployedge/microsoft-edge-mobile-policies#edgebrandlogo) |
| EdgeBrandColor | `#0078d4` | [Set Edge brand color](/deployedge/microsoft-edge-mobile-policies#edgebrandcolor) |
| DefaultSearchProviderEnabled | true | [Enable default search provider](/deployedge/microsoft-edge-mobile-policies#defaultsearchproviderenabled) |
| DefaultSearchProviderName | "Preferred Company Search" | [Default search provider name](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidername) |
| DefaultSearchProviderSearchURL | "https://search.company.com?q={searchTerms}" | [Default search provider search URL](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidersearchurl) |
| DefaultSearchProviderSuggestURL | "https://search.company.com/suggest?q={searchTerms}" | [Default search provider suggest URL](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidersuggesturl) |
| DefaultSearchProviderKeyword | "company" | [Default search provider keyword](/deployedge/microsoft-edge-mobile-policies#defaultsearchproviderkeyword) |
| ProxySettings | {"ProxyServer": "IP:Port", "ProxyBypassList": "*.company.com", "ProxyMode": "direct"} | [Configure proxy settings](/deployedge/microsoft-edge-browser-policies/proxysettings) |
| EdgeDisabledFeatures | password&#124;autofill&#124;copilot&#124;collections&#124;readaloud | [Disable features](/deployedge/microsoft-edge-mobile-policies#edgedisabledfeatures) |

8. Expand **Edge configuration settings** and configure:

| Setting | Value |
|----------|-------|
| Allowed URLs | Leave empty (Level 2 uses blocked URLs instead – when blocked URLs are configured, allowed URLs field becomes unavailable) |
| Blocked URLs | *.facebook.com, *.twitter.com, *.instagram.com, *.tiktok.com |
| Redirect restricted sites to personal context | Enable |

9. Select **Next**
10. In **Assignments**, assign to **SEB-Level2-Users** group.  
11. Select **Next** to review the settings. Then choose **Create**.

### Level 3 – High Security Mobile Configuration for Android

Level 3 configuration enforces maximum security with zero-trust controls and comprehensive data-loss prevention.

1. Go to the [Microsoft Intune admin center](https://intune.microsoft.com/).  
2. Select **Apps** > **Manage apps** > **Configuration** > **Create** > **Managed apps**.  
3. On the **Basics** tab, enter:  
   - **Name:** Level 3 – High security mobile browser configuration – Android ACP
   - **Description:** Maximum security configuration for Microsoft Edge on Android, enforcing strict data protection and zero-trust controls.  
4. In **Target policy to**, select **Selected apps**.  
   - Choose **+ Select public apps**.  
   - In the **Select apps to target** panel, search for and select **Microsoft Edge (Android)**, then select **Select**.  
5. Select **Next**.  
6. On the **Settings** step, expand **General configuration settings**.  
7. Configure each setting using the **Name** and **Value** specified:

| Name | Value | Documentation |
|------|-------|---------------|
| com.microsoft.intune.mam.managedbrowser.PasswordSSO | false | [Microsoft Entra password single sign-on](/microsoft-365/solutions/apps-config-step-4#general-app-configuration-settings) |
| EdgeMyApps | false | [Enable EdgeMyApps](/deployedge/microsoft-edge-mobile-policies#edgemyapps) |
| EdgeDefaultHTTPS | true | [Enforce default HTTPS](/deployedge/microsoft-edge-mobile-policies#edgedefaulthttps) |
| EdgeDisableShareUsageData | true | [Disable sharing usage data](/deployedge/microsoft-edge-mobile-policies#edgedisableshareusagedata) |
| EdgeNewTabPageLayout | 2 | [Configure new tab page layout](/deployedge/microsoft-edge-mobile-policies#edgenewtabpagelayout) |
| EdgeEnableKioskMode | true | [Enable kiosk mode](/deployedge/microsoft-edge-mobile-policies#edgeenablekioskmode) |
| EdgeShowAddressBarInKioskMode | false | [Show address bar in kiosk mode](/deployedge/microsoft-edge-mobile-policies#edgeshowaddressbarinkioskmode) |
| EdgeSyncDisabled | true | [Disable browser sync](/deployedge/microsoft-edge-mobile-policies#edgesyncdisabled) |
| InPrivateModeAvailability | 1 | [Disable InPrivate mode](/deployedge/microsoft-edge-mobile-policies#inprivatemodeavailability) |
| SavingBrowserHistoryDisabled | true | [Disable browser history saving](/deployedge/microsoft-edge-mobile-policies#savingbrowserhistorydisabled) |
| TranslateEnabled | false | [Disable translate](/deployedge/microsoft-edge-mobile-policies#translateenabled) |
| EdgeSharedDeviceSupportEnabled | false | [Disable shared device support](/deployedge/microsoft-edge-mobile-policies#edgeshareddevicesupportenabled) |
| AutofillCreditCardEnabled | false | [Disable autofill for payment instructions](/deployedge/microsoft-edge-browser-policies/autofillcreditcardenabled) |
| DownloadRestrictions | 2 | [Download restrictions](/deployedge/microsoft-edge-browser-policies/downloadrestrictions) |
| ExperimentationAndConfigurationServiceControl | 0 | [Experimentation and configuration service control](/deployedge/microsoft-edge-mobile-policies#experimentationandconfigurationservicecontrol) |
| DefaultBrowserSettingEnabled | false | [Set as default browser](/deployedge/microsoft-edge-mobile-policies#defaultbrowsersettingenabled) |
| DefaultCookiesSetting | 4 | [Default cookies setting](/deployedge/microsoft-edge-browser-policies/defaultcookiessetting) |
| DefaultJavaScriptSetting | 2 | [Default JavaScript setting](/deployedge/microsoft-edge-browser-policies/defaultjavascriptsetting) |
| DefaultGeolocationSetting | 2 | [Default geolocation setting](/deployedge/microsoft-edge-browser-policies/defaultgeolocationsetting) |
| BiometricAuthenticationBeforeFilling | true | [Biometric authentication before filling](/deployedge/microsoft-edge-browser-policies/biometricauthenticationbeforefilling) |
| PasswordManagerEnabled | false | [Enable password manager](/deployedge/microsoft-edge-mobile-policies#passwordmanagerenabled) |
| EdgeDisabledFeatures | inprivate&#124;autofill&#124;password&#124;translator&#124;readaloud&#124;drop&#124;<br>coupons&#124;extensions&#124;copilot&#124;collections&#124;myapps | [Disable features](/deployedge/microsoft-edge-mobile-policies#edgedisabledfeatures) |
| EdgeBrandLogo | true | [Enable Edge brand logo](/deployedge/microsoft-edge-mobile-policies#edgebrandlogo) |
| EdgeBrandColor | `#0078d4` | [Set Edge brand color](/deployedge/microsoft-edge-mobile-policies#edgebrandcolor) |
| DefaultSearchProviderEnabled | true | [Enable default search provider](/deployedge/microsoft-edge-mobile-policies#defaultsearchproviderenabled) |
| DefaultSearchProviderName | "Preferred Company Search" | [Default search provider name](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidername) |
| DefaultSearchProviderSearchURL | "https://search.company.com?q={searchTerms}" | [Default search provider search URL](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidersearchurl) |
| DefaultSearchProviderSuggestURL | "https://search.company.com/suggest?q={searchTerms}" | [Default search provider suggest URL](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidersuggesturl) |
| DefaultSearchProviderKeyword | "company" | [Default search provider keyword](/deployedge/microsoft-edge-mobile-policies#defaultsearchproviderkeyword) |
| ProxySettings | {"ProxyServer": "IP:Port", "ProxyBypassList": "*.company.com", "ProxyMode": "fixed_servers"} | [Configure proxy settings](/deployedge/microsoft-edge-browser-policies/proxysettings) |
| EdgeBlockSignInEnabled | true | [Block sign-in enabled](/deployedge/microsoft-edge-browser-policies/edgeblocksigninenabled) |

8. Expand **Edge configuration settings** and configure:

| Setting | Value |
|----------|-------|
| Allowed URLs | *.company.com, *.microsoft.com, login.microsoftonline.com |
| Blocked URLs | Leave empty (Level 3 uses allowed URLs – when allowed URLs are configured, blocked URLs field becomes unavailable) |

9. Select **Next**
10. In **Assignments**, assign to **SEB-Level3-Users** group.  
11. Select **Next** to review the settings. Then choose **Create**.

### Validation (All Android Levels)

#### Policy Application

- In the Intune admin center, verify the ACP deployment status for assigned Android devices.

#### Browser Configuration

- On an Android device, open Microsoft Edge and go to `edge://policy` to confirm the expected configuration values are present and not marked as errors.

#### URL Filtering

- **Level 1:** Confirm allowed URLs operate as expected.  
- **Level 2:** Confirm blocked URLs (such as social media domains) are restricted.  
- **Level 3:** Confirm only allowlisted corporate URLs are accessible.

#### Feature Restrictions

- Validate restricted features based on the assigned security level, such as InPrivate mode, autofill, password import, extensions, and Copilot visibility.

#### Homepage and Bookmarks

- Confirm the managed homepage and managed bookmarks appear correctly in Microsoft Edge.

#### Security Settings

- Verify that SmartScreen, HTTPS enforcement, and data-sharing restrictions operate according to the applied policy.

#### VPN Integration (If Configured)

- For deployments using Microsoft Tunnel, ensure per-app VPN settings connect and route traffic as defined in the ACP.


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

Level 1 configuration provides foundational browser security controls while maintaining user productivity.

1. Go to the [Microsoft Intune admin center](https://intune.microsoft.com/).  
2. Select **Apps** > **Manage apps** > **Configuration** > **Create** > **Managed apps**.  
3. On the **Basics** tab, enter:  
   - **Name:** Level 1 – Basic mobile browser configuration – iOS ACP  
   - **Description:** Basic browser configuration for Microsoft Edge on iOS.  
4. In **Target policy to**, select **Selected apps**.  
   - Choose **+ Select public apps**.  
   - In the **Select apps to target** panel, search for and select **Microsoft Edge**.  
   - Choose **Microsoft Edge (iOS/iPadOS)**, then **Select**.  
5. Select **Next**.  
6. On the **Settings** step, expand **General configuration settings**.  
7. Configure each setting using the **Name** and **Value** specified:

| Name | Value | Documentation |
|------|-------|---------------|
| com.microsoft.intune.mam.managedbrowser.PasswordSSO | true | [Password single sign-on](/microsoft-365/solutions/apps-config-step-4?view=o365-worldwide#general-app-configuration-settings) |
| com.microsoft.intune.mam.managedbrowser.SmartScreenEnabled | true | [SmartScreen enabled](/microsoft-365/solutions/apps-config-step-4?view=o365-worldwide#general-app-configuration-settings) |
| EdgeMyApps | true | [Enable EdgeMyApps](/deployedge/microsoft-edge-mobile-policies#edgemyapps) |
| EdgeDefaultHTTPS | true | [Default HTTPS enforced](/deployedge/microsoft-edge-mobile-policies#edgedefaulthttps) |
| EdgeDisableShareUsageData | true | [Disable sharing usage data](/deployedge/microsoft-edge-mobile-policies#edgedisableshareusagedata) |
| EdgeImportPasswordsDisabled | false | [Disable password import](/deployedge/microsoft-edge-mobile-policies#edgeimportpasswordsdisabled) |
| EdgeProxyPacUrl |  | [Proxy PAC URL](/deployedge/microsoft-edge-mobile-policies#edgeproxypacurl) |
| BiometricAuthenticationBeforeFilling | false | [Biometric authentication before filling](/deployedge/microsoft-edge-browser-policies/biometricauthenticationbeforefilling) |
| PasswordManagerEnabled | false | [Disable password manager](/deployedge/microsoft-edge-mobile-policies#passwordmanagerenabled) |
| SmartScreenEnabled | true | [SmartScreen enabled](/deployedge/microsoft-edge-mobile-policies#smartscreenenabled) |
| SearchSuggestEnabled | false | [Disable search suggestions](/deployedge/microsoft-edge-mobile-policies#searchsuggestenabled) |
| TranslateEnabled | true | [Translate enabled](/deployedge/microsoft-edge-mobile-policies#translateenabled) |
| HideFirstRunExperience | true | [Hide first run experience](/deployedge/microsoft-edge-mobile-policies#hidefirstrunexperience) |
| SSLErrorOverrideAllowed | true | [SSL error override allowed](/deployedge/microsoft-edge-mobile-policies#sslerroroverrideallowed) |
| DefaultBrowserSettingEnabled | true | [Default browser setting enabled](/deployedge/microsoft-edge-mobile-policies#defaultbrowsersettingenabled) |
| ExperimentationAndConfigurationServiceControl | 1 | [Experimentation and configuration service control](/deployedge/microsoft-edge-mobile-policies#experimentationandconfigurationservicecontrol) |
| DefaultPopupsSetting | 2 | [Disable pop-ups](/deployedge/microsoft-edge-mobile-policies#defaultpopupssetting) |
| EdgeBrandLogo | true | [Organizational branding – logo](/deployedge/microsoft-edge-mobile-policies#edgebrandlogo) |
| EdgeBrandColor | `#0078d4` | [Organizational branding – color](/deployedge/microsoft-edge-mobile-policies#edgebrandcolor) |
| DefaultSearchProviderEnabled | true | [Default search provider enabled](/deployedge/microsoft-edge-mobile-policies#defaultsearchproviderenabled) |
| DefaultSearchProviderName | Preferred Company Search | [Default search provider name](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidername) |
| DefaultSearchProviderSearchURL | `https://search.company.com?q={searchTerms}` | [Default search provider search URL](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidersearchurl) |
| DefaultSearchProviderSuggestURL | `https://search.company.com/suggest?q={searchTerms}` | [Default search provider suggest URL](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidersuggesturl) |
| DefaultSearchProviderKeyword | company | [Default search provider keyword](/deployedge/microsoft-edge-mobile-policies#defaultsearchproviderkeyword) |
| EdgeNetworkStackPref | 0 | [Edge network stack preference](/deployedge/microsoft-edge-mobile-policies#edgenetworkstackpref) |

8. Expand **Edge configuration settings** and configure:

| Setting | Value |
|----------|-------|
| Application proxy redirection | Disable |
| Homepage shortcut URL | `https://www.company.com` |
| Managed bookmarks | Company Portal &#124; `https://portal.company.com` |
| Allowed URLs | Leave empty (Level 3 uses Allowed URLs) |
| Blocked URLs | Leave empty (Level 2 uses Blocked URLs) |
| Redirect restricted sites to personal context | Disable |


9. Select **Next**.  
10. In **Assignments**, assign to **SEB-Level1-Users** group.  
11. Select **Next** to review the settings. Then choose **Create** when you're done.  

### Level 2 – Enhanced mobile browser configuration for iOS

Level 2 configuration adds enhanced security controls and restrictions for sensitive environments.

1. Go to the [Microsoft Intune admin center](https://intune.microsoft.com/).  
2. Select **Apps** > **Manage apps** > **Configuration** > **Create** > **Managed apps**.  
3. On the **Basics** tab, enter:  
   - **Name:** Level 2 – Enhanced mobile browser configuration – iOS ACP  
   - **Description:** Enhanced browser configuration with security controls for Microsoft Edge on iOS.  
4. In **Target policy to**, select **Selected apps**.  
   - Choose **+ Select public apps**.  
   - In the **Select apps to target** panel, search for and select **Microsoft Edge**.  
   - Choose **Microsoft Edge (iOS/iPadOS)**, then **Select**.  
5. Select **Next**.  
6. On the **Settings** step, expand **General configuration settings**.  
7. Configure each setting using the **Name** and **Value** specified:

| Name | Value | Documentation |
|------|-------|---------------|
| com.microsoft.intune.mam.managedbrowser.PasswordSSO | true | [Password single sign-on](/microsoft-365/solutions/apps-config-step-4?view=o365-worldwide#general-app-configuration-settings) |
| com.microsoft.intune.mam.managedbrowser.SmartScreenEnabled | true | [SmartScreen enabled](/microsoft-365/solutions/apps-config-step-4?view=o365-worldwide#general-app-configuration-settings) |
| EdgeMyApps | true | [Enable EdgeMyApps](/deployedge/microsoft-edge-mobile-policies#edgemyapps) |
| EdgeDefaultHTTPS | true | [Default HTTPS enforced](/deployedge/microsoft-edge-mobile-policies#edgedefaulthttps) |
| EdgeDisableShareUsageData | true | [Disable sharing usage data](/deployedge/microsoft-edge-mobile-policies#edgedisableshareusagedata) |
| EdgeImportPasswordsDisabled | true | [Disable password import](/deployedge/microsoft-edge-mobile-policies#edgeimportpasswordsdisabled) |
| EdgeProxyPacUrl |  | [Proxy PAC URL](/deployedge/microsoft-edge-mobile-policies#edgeproxypacurl) |
| BiometricAuthenticationBeforeFilling | true | [Biometric authentication before filling](/deployedge/microsoft-edge-browser-policies/biometricauthenticationbeforefilling) |
| PasswordManagerEnabled | false | [Disable password manager](/deployedge/microsoft-edge-mobile-policies#passwordmanagerenabled) |
| SmartScreenEnabled | true | [SmartScreen enabled](/deployedge/microsoft-edge-mobile-policies#smartscreenenabled) |
| SearchSuggestEnabled | false | [Disable search suggestions](/deployedge/microsoft-edge-mobile-policies#searchsuggestenabled) |
| TranslateEnabled | true | [Translate enabled](/deployedge/microsoft-edge-mobile-policies#translateenabled) |
| HideFirstRunExperience | true | [Hide first run experience](/deployedge/microsoft-edge-mobile-policies#hidefirstrunexperience) |
| SSLErrorOverrideAllowed | false | [SSL error override allowed](/deployedge/microsoft-edge-mobile-policies#sslerroroverrideallowed) |
| EdgeNetworkStackPref | 0 | [Network stack preference](/deployedge/microsoft-edge-mobile-policies#edgenetworkstackpref) |
| DefaultBrowserSettingEnabled | false | [Default browser setting enabled](/deployedge/microsoft-edge-mobile-policies#defaultbrowsersettingenabled) |
| EdgeCopilotEnabled | false | [Disable Edge Copilot](/deployedge/microsoft-edge-mobile-policies#edgecopilotenabled) |
| EdgeSharedDeviceSupportEnabled | true | [Enable shared device support](/deployedge/microsoft-edge-mobile-policies#edgeshareddevicesupportenabled) |
| ExperimentationAndConfigurationServiceControl | 0 | [Experimentation and configuration service control](/deployedge/microsoft-edge-mobile-policies#experimentationandconfigurationservicecontrol) |
| EdgeSyncDisabled | true | [Disable browser sync](/deployedge/microsoft-edge-mobile-policies#edgesyncdisabled) |
| SavingBrowserHistoryDisabled | false | [Disable browser history saving](/deployedge/microsoft-edge-mobile-policies#savingbrowserhistorydisabled) |
| DefaultPopupsSetting | 2 | [Disable pop-ups](/deployedge/microsoft-edge-mobile-policies#defaultpopupssetting) |
| EdgeBrandLogo | true | [Organizational branding – logo](/deployedge/microsoft-edge-mobile-policies#edgebrandlogo) |
| EdgeBrandColor | `#0078d4` | [Organizational branding – color](/deployedge/microsoft-edge-mobile-policies#edgebrandcolor) |
| DefaultSearchProviderEnabled | true | [Default search provider enabled](/deployedge/microsoft-edge-mobile-policies#defaultsearchproviderenabled) |
| DefaultSearchProviderName | Preferred Company Search | [Default search provider name](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidername) |
| DefaultSearchProviderSearchURL | `https://search.company.com?q={searchTerms}` | [Default search provider search URL](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidersearchurl) |
| DefaultSearchProviderSuggestURL | `https://search.company.com/suggest?q={searchTerms}` | [Default search provider suggest URL](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidersuggesturl) |
| DefaultSearchProviderKeyword | company | [Default search provider keyword](/deployedge/microsoft-edge-mobile-policies#defaultsearchproviderkeyword) |
| EdgeDisabledFeatures | password\|autofill\|copilot\|collections\|readaloud | [Disable features](/deployedge/microsoft-edge-mobile-policies#edgedisabledfeatures) |
| EdgeBlockSignInEnabled | false | [Block sign-in enabled](/deployedge/microsoft-edge-mobile-policies#edgeblocksigninenabled) |

8. Expand **Edge configuration settings** and configure:

| Setting | Value |
|----------|-------|
| Allowed URLs | Leave empty (Level 2 uses blocked URLs instead – when blocked URLs are configured, allowed URLs field becomes unavailable) |
| Blocked URLs | *.facebook.com, *.twitter.com, *.instagram.com, *.tiktok.com |
| Redirect restricted sites to personal context | Enable |

9. Select **Next**.  
10. In **Assignments**, assign to **SEB-Level2-Users** group.  
11. Select **Next** to review the settings. Then choose **Create** when you're done.  

### Level 3 – High security mobile configuration for iOS

Level 3 configuration enforces maximum security with zero-trust controls and comprehensive data-loss prevention.

1. Go to the [Microsoft Intune admin center](https://intune.microsoft.com/).  
2. Select **Apps** > **Manage apps** > **Configuration** > **Create** > **Managed apps**.  
3. On the **Basics** tab, enter:  
   - **Name:** Level 3 – High security mobile configuration – iOS ACP  
   - **Description:** Maximum security browser configuration for Microsoft Edge on iOS.  
4. In **Target policy to**, select **Selected apps**.  
   - Choose **+ Select public apps**.  
   - In the **Select apps to target** panel, search for and select **Microsoft Edge (iOS/iPadOS)**, then select **Select**.  
5. Select **Next**.  
6. On the **Settings** step, expand **General configuration settings**.  
7. Configure each setting using the **Name** and **Value** specified:

| Name | Value | Documentation |
|------|-------|---------------|
| com.microsoft.intune.mam.managedbrowser.PasswordSSO | false | [Password single sign-on](/microsoft-365/solutions/apps-config-step-4?view=o365-worldwide#general-app-configuration-settings) |
| com.microsoft.intune.mam.managedbrowser.SmartScreenEnabled | true | [SmartScreen enabled](/microsoft-365/solutions/apps-config-step-4?view=o365-worldwide#general-app-configuration-settings) |
| EdgeMyApps | false | [Enable EdgeMyApps](/deployedge/microsoft-edge-mobile-policies#edgemyapps) |
| EdgeDefaultHTTPS | true | [Default HTTPS enforced](/deployedge/microsoft-edge-mobile-policies#edgedefaulthttps) |
| EdgeDisableShareUsageData | true | [Disable sharing usage data](/deployedge/microsoft-edge-mobile-policies#edgedisableshareusagedata) |
| EdgeImportPasswordsDisabled | true | [Disable password import](/deployedge/microsoft-edge-mobile-policies#edgeimportpasswordsdisabled) |
| EdgeProxyPacUrl |  | [Proxy PAC URL](/deployedge/microsoft-edge-mobile-policies#edgeproxypacurl) |
| BiometricAuthenticationBeforeFilling | true | [Biometric authentication before filling](/deployedge/microsoft-edge-browser-policies/biometricauthenticationbeforefilling) |
| PasswordManagerEnabled | false | [Disable password manager](/deployedge/microsoft-edge-mobile-policies#passwordmanagerenabled) |
| SmartScreenEnabled | true | [SmartScreen enabled](/deployedge/microsoft-edge-mobile-policies#smartscreenenabled) |
| SearchSuggestEnabled | false | [Disable search suggestions](/deployedge/microsoft-edge-mobile-policies#searchsuggestenabled) |
| TranslateEnabled | false | [Translate enabled](/deployedge/microsoft-edge-mobile-policies#translateenabled) |
| HideFirstRunExperience | true | [Hide first run experience](/deployedge/microsoft-edge-mobile-policies#hidefirstrunexperience) |
| SSLErrorOverrideAllowed | false | [SSL error override allowed](/deployedge/microsoft-edge-mobile-policies#sslerroroverrideallowed) |
| EdgeNetworkStackPref | 0 | [Network stack preference](/deployedge/microsoft-edge-mobile-policies#edgenetworkstackpref) |
| DefaultBrowserSettingEnabled | false | [Default browser setting enabled](/deployedge/microsoft-edge-mobile-policies#defaultbrowsersettingenabled) |
| EdgeCopilotEnabled | false | [Disable Edge Copilot](/deployedge/microsoft-edge-mobile-policies#edgecopilotenabled) |
| EdgeSharedDeviceSupportEnabled | false | [Disable shared device support](/deployedge/microsoft-edge-mobile-policies#edgeshareddevicesupportenabled) |
| ExperimentationAndConfigurationServiceControl | 0 | [Experimentation and configuration service control](/deployedge/microsoft-edge-mobile-policies#experimentationandconfigurationservicecontrol) |
| EdgeSyncDisabled | true | [Disable browser sync](/deployedge/microsoft-edge-mobile-policies#edgesyncdisabled) |
| SavingBrowserHistoryDisabled | true | [Disable browser history saving](/deployedge/microsoft-edge-mobile-policies#savingbrowserhistorydisabled) |
| DefaultPopupsSetting | 2 | [Disable pop-ups](/deployedge/microsoft-edge-mobile-policies#defaultpopupssetting) |
| EdgeBrandLogo | true | [Organizational branding – logo](/deployedge/microsoft-edge-mobile-policies#edgebrandlogo) |
| EdgeBrandColor | `#0078d4` | [Organizational branding – color](/deployedge/microsoft-edge-mobile-policies#edgebrandcolor) |
| DefaultSearchProviderEnabled | true | [Default search provider enabled](/deployedge/microsoft-edge-mobile-policies#defaultsearchproviderenabled) |
| DefaultSearchProviderName | Preferred Company Search | [Default search provider name](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidername) |
| DefaultSearchProviderSearchURL | `https://search.company.com?q={searchTerms}` | [Default search provider search URL](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidersearchurl) |
| DefaultSearchProviderSuggestURL | `https://search.company.com/suggest?q={searchTerms}` | [Default search provider suggest URL](/deployedge/microsoft-edge-mobile-policies#defaultsearchprovidersuggesturl) |
| DefaultSearchProviderKeyword | company | [Default search provider keyword](/deployedge/microsoft-edge-mobile-policies#defaultsearchproviderkeyword) |
| EdgeDisabledFeatures | inprivate\|autofill\|password\|translator\|readaloud\|drop\|<br>coupons\|extensions\|copilot\|collections\|myapps\|share | [Disable features](/deployedge/microsoft-edge-mobile-policies#edgedisabledfeatures) |
| EdgeBlockSignInEnabled | true | [Block sign-in enabled](/deployedge/microsoft-edge-browser-policies/edgeblocksigninenabled) |

8. Expand **Edge configuration settings** and configure:

| Setting | Value |
|----------|-------|
| Allowed URLs | *.company.com, *.microsoft.com, login.microsoftonline.com |
| Blocked URLs | Leave empty (Level 3 uses allowed URLs – when allowed URLs are configured, blocked URLs field becomes unavailable) |

9. Per-App VPN (optional): Integrate with Microsoft Tunnel if required for isolated secure traffic routing
10. Select **Next**.  
11. In **Assignments**, assign to **SEB-Level3-Users** group.  
12. Select **Next** to review the settings. Then choose **Create** when you're done.  

### Validation (All iOS Levels)

#### Policy Application

- In the Intune admin center, verify the assigned App Protection and App Configuration policies have successfully deployed to the targeted iOS devices.

#### App Configuration Verification

- On the device, open Microsoft Edge and navigate to **Settings**.
- Confirm that managed configuration values—such as homepage, search provider, password manager, and disabled features—match the applied ACP settings.

#### URL Filtering

- **Level 1:** Confirm that allowed URLs operate as expected.
- **Level 2:** Verify that blocked URL categories (for example, social media domains) cannot be accessed.
- **Level 3:** Confirm that only the configured corporate allowlisted URLs are accessible.

#### Feature Restrictions

- Validate restricted features based on the assigned level, including:
  - **Level 1:** SmartScreen, pop-up blocking, and basic security controls.
  - **Level 2:** Sync disabled, password import blocked, biometric authentication for filling enabled, InPrivate browsing controlled.
  - **Level 3:** InPrivate disabled, history saving disabled, shared device mode disabled, and advanced restrictions (such as Collections, Extensions, Drop, Copilot) enforced.

#### Homepage and Bookmarks

- Confirm that the managed homepage and any configured managed bookmarks appear correctly in Microsoft Edge.

#### Policy Dependency Check

- Ensure the user is signed into Edge using their work or school (Entra ID) account, as App Configuration settings only apply within the managed work profile context.


::: zone-end

## Next steps

Continue to [Step 5](mamedge-5-settings-catalog.md) to configure Settings Catalog policies for enrolled Windows and macOS devices.