---
title: Step 5. Create Settings Catalog policies for Microsoft Edge for Business
description: Step 5. Create Settings Catalog policies for Microsoft Edge for Business on Windows and macOS.
ms.date: 11/12/2025
ms.topic: how-to
ms.reviewer: samarti
ms.custom:
ms.collection:
- highpri
- highseo
- FocusArea_Apps_AppManagement
zone_pivot_groups: platforms-windows-macos
---

# Step 5: Settings Catalog for Microsoft Edge for Business

Settings Catalog policies provide deep device-level control for Microsoft Edge browser configuration on enrolled Windows and macOS devices. These policies complement app protection policies by providing comprehensive browser hardening and enterprise customization.

> [!NOTE]
> Settings Catalog requires device enrollment and provides device-level controls. For unmanaged devices, use App Protection Policies (Step 2) and App Configuration Policies (Step 4).

::: zone pivot="windows"

## Settings Catalog for Windows

Settings Catalog for Windows provides comprehensive browser configuration with progressive security levels aligned with NIST, DISA STIG, and CISA frameworks. Following this guide doesn't make your organization compliant with these standards; they were used as input to build the security framework.

> **Microsoft Documentation:**
>
> - [Settings Catalog Overview](../configuration/settings-catalog.md)
> - [Microsoft Edge Browser Policies](/deployedge/microsoft-edge-policies)
> - [Microsoft Edge Update Policies](/deployedge/microsoft-edge-update-policies)

**Prerequisites:**

- Windows 11 Pro or Enterprise  
- Intune enrollment  
- Microsoft Entra ID join or Hybrid  
- Microsoft Edge Stable channel  
- TPM 2.0 (for Application Bound Encryption)  
- Hyper-V (if using Application Guard for Level 3)  

### Level 1 - Enterprise basic security for Windows

Level 1 configuration provides foundational browser security controls while maintaining user productivity.

1. Go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Devices** > **Windows** > **Manage devices** > **Configuration** > **Create** > **New policy**.  
3. For **Platform**, choose **Windows 10 and later**. For **Profile type**, choose **Settings catalog**.  
4. Select **Create**.  
5. On the **Basics** tab, enter:  
   - **Name:** Level 1 – Enterprise basic security – Windows Settings Catalog  
   - **Description:** Basic browser security configuration for Microsoft Edge on Windows devices.  
6. Select **Next**.  
7. On **Configuration settings**, select **+ Add settings**.  
8. In the **Settings picker**, locate each setting using one of the following options:  
   - **Search for a setting:** Copy the **Setting** from the table and paste it into search.  
   - **Browse by category:** Select the **Category** listed for that setting.  
9. Configure the setting using the **Value** specified.

| Category | Setting | Value | Documentation |
|-----------|---------|-------|----------------|
| Microsoft Edge\SmartScreen settings | Configure Microsoft Defender SmartScreen | Enabled | [Configure Microsoft Defender SmartScreen](/deployedge/microsoft-edge-browser-policies/smartscreenenabled) |
| Microsoft Edge\Automatic HTTPS | Enable automatic HTTPS | Enabled | [Enable automatic HTTPS](/deployedge/microsoft-edge-browser-policies/httpsonlymode) |
| Microsoft Edge\Content settings | Block third party cookies | Enabled | [Block third party cookies](/deployedge/microsoft-edge-browser-policies/thirdpartycookiesblocked) |
| Microsoft Edge\Content settings | Configure cookies | Disabled | [Configure cookies](/deployedge/microsoft-edge-browser-policies/defaultcookiessetting) |
| Microsoft Edge\Content settings | Default pop-up window setting | Do not allow any site to show popups (2) | [Default pop-up window setting](/deployedge/microsoft-edge-browser-policies/defaultpopupssetting) |
| Microsoft Edge\Content settings | Default notification setting | Do not allow any site to show desktop notifications (2) | [Default notification setting](/deployedge/microsoft-edge-browser-policies/defaultnotificationssetting) |
| Microsoft Edge\Content settings | Default geolocation setting | Don’t allow any site to track users’ physical location (2) | [Default geolocation setting](/deployedge/microsoft-edge-browser-policies/defaultgeolocationbehavior) |
| Microsoft Edge\Content settings | Allow or block video capture | Enabled | [Allow or block video capture](/deployedge/microsoft-edge-browser-policies/videocaptureallowed) |
| Microsoft Edge\Content settings | Allow or block audio capture | Enabled | [Allow or block audio capture](/deployedge/microsoft-edge-browser-policies/audiocaptureallowed) |
| Microsoft Edge\Privacy & data protection | Block tracking of users' web-browsing activity | Strict (3) | [Block tracking of users' web-browsing activity](/deployedge/microsoft-edge-browser-policies/trackingprevention) |
| Microsoft Edge\Privacy & data protection | Allow personalization of ads, search and news by sending browsing history to Microsoft | Disabled | [Allow personalization of ads, search and news by sending browsing history to Microsoft](/deployedge/microsoft-edge-browser-policies/personalizationreportingenabled) |
| Microsoft Edge\Privacy & data protection | Enable network prediction | Don’t predict network actions on any network connection (2) | [Enable network prediction](/deployedge/microsoft-edge-browser-policies/networkpredictionoptions) |
| Microsoft Edge\Privacy & data protection | Enable search suggestions | Disabled | [Enable search suggestions](/deployedge/microsoft-edge-browser-policies/searchsuggestenabled) |
| Microsoft Edge\Privacy & data protection | Send required and optional diagnostic data about browser usage | Off (0) | [Send required and optional diagnostic data about browser usage](/deployedge/microsoft-edge-browser-policies/diagnosticdata) |
| Microsoft Edge\Privacy & data protection | Disable saving browser history | Enabled | [Disable saving browser history](/deployedge/microsoft-edge-browser-policies/savingbrowserhistorydisabled) |
| Microsoft Edge\Privacy & data protection | Enable the Collections feature | Disabled | [Enable the Collections feature](/deployedge/microsoft-edge-browser-policies/browserdatacollectionenabled) |
| Microsoft Edge\Privacy Sandbox | Configure Do Not Track | Disabled | [Configure Do Not Track](/deployedge/microsoft-edge-browser-policies/configuredonottrack) |
| Microsoft Edge\Privacy Sandbox | Enforce Google SafeSearch | Enabled | [Enforce Google SafeSearch](/deployedge/microsoft-edge-browser-policies/forcegooglesafesearch) |
| Microsoft Edge\Privacy Sandbox | Enforce Bing SafeSearch | Enabled, Configure strict search restrictions in Bing | [Enforce Bing SafeSearch](/deployedge/microsoft-edge-browser-policies/forcebingsafesearch) |
| Microsoft Edge\Privacy Sandbox | Force minimum YouTube Restricted Mode | Enabled, 1 Enforce at least Moderate Restricted Mode on YouTube | [Force minimum YouTube Restricted Mode](/deployedge/microsoft-edge-browser-policies/forceyoutuberestrict) |
| Microsoft Edge\Privacy Sandbox | Continue running background apps after Microsoft Edge closes | Disabled | [Continue running background apps after Microsoft Edge closes](/deployedge/microsoft-edge-browser-policies/backgroundmodeenabled) |
| Microsoft Edge\Privacy Sandbox | Disable synchronization of data using Microsoft sync services | Disabled | [Disable synchronization of data using Microsoft sync services](/deployedge/microsoft-edge-browser-policies/syncdisabled) |
| Microsoft Edge\Password Manager and Protection | Enable saving passwords to the password manager | Disabled | [Enable saving passwords to the password manager](/deployedge/microsoft-edge-browser-policies/passwordmanagerenabled) |
| Microsoft Edge\Password Manager and Protection | Enable AutoFill for addresses | Disabled | [Enable AutoFill for addresses](/deployedge/microsoft-edge-browser-policies/autofilladdressenabled) |
| Microsoft Edge\Password Manager and Protection | Enable AutoFill for payment instruments | Disabled | [Enable AutoFill for payment instruments](/deployedge/microsoft-edge-browser-policies/autofillcreditcardenabled) |
| Microsoft Edge\Authentication | Force synchronization of browser data and do not show the sync consent prompt | Disabled | [Force synchronization of browser data and do not show the sync consent prompt](/deployedge/microsoft-edge-browser-policies/forcesync) |
| Microsoft Edge\Authentication | Windows Hello For HTTP Auth Enabled | Enabled | [Windows Hello For HTTP Auth Enabled](/deployedge/microsoft-edge-browser-policies/windowshelloforhttpauthenabled) |
| Microsoft Edge\Import Controls | Allow importing of autofill form data | Disabled | [Allow importing of autofill form data](/deployedge/microsoft-edge-browser-policies/importautofillformdata) |
| Microsoft Edge\Import Controls | Allow importing of saved passwords | Disabled | [Allow importing of saved passwords](/deployedge/microsoft-edge-browser-policies/importsavedpasswords) |
| Microsoft Edge\Import Controls | Allow importing of browsing history | Disabled | [Allow importing of browsing history](/deployedge/microsoft-edge-browser-policies/importhistory) |
| Microsoft Edge\Import Controls | Allow importing of Cookies | Disabled | [Allow importing of Cookies](/deployedge/microsoft-edge-browser-policies/importcookies) |
| Microsoft Edge\Import Controls | Allow importing of extensions | Disabled | [Allow importing of extensions](/deployedge/microsoft-edge-browser-policies/importextensions) |
| Microsoft Edge\Import Controls | Allow importing of payment info | Disabled | [Allow importing of payment info](/deployedge/microsoft-edge-browser-policies/importpaymentinfo) |
| Microsoft Edge\Import Controls | Allow importing of open tabs | Disabled | [Allow importing of open tabs](/deployedge/microsoft-edge-browser-policies/importopentabs) |
| Microsoft Edge\Import Controls | Allow importing of home page settings | Disabled | [Allow importing of home page settings](/deployedge/microsoft-edge-browser-policies/importhomepage) |
| Microsoft Edge\Import Controls | Allow importing of browser settings |  | [Allow importing of browser settings](/deployedge/microsoft-edge-browser-policies/importbrowsersettings) |
| Microsoft Edge\Startup, home page and new tab page | Configure the home page URL | https://copilot.microsoft.com/ | [Configure the home page URL](/deployedge/microsoft-edge-browser-policies/homepagelocation) |
| Microsoft Edge\Startup, home page and new tab page | Show Home button on toolbar | Enabled | [Show Home button on toolbar](/deployedge/microsoft-edge-browser-policies/showhomebutton) |
| Microsoft Edge\Startup, home page and new tab page | Configure the new tab page URL | https://copilot.microsoft.com/ | [Configure the new tab page URL](/deployedge/microsoft-edge-browser-policies/newtabpageurl) |
| Microsoft Edge\Startup, home page and new tab page | Allow quick links on the new tab page | Enabled | [Allow quick links on the new tab page](/deployedge/microsoft-edge-browser-policies/newtabpagequicklinksenabled) |
| Microsoft Edge\Startup, home page and new tab page | Hide the First-run experience and splash screen | Enabled | [Hide the First-run experience and splash screen](/deployedge/microsoft-edge-browser-policies/hidefirstrunexperience) |
| Microsoft Edge\Network settings | Control the mode of DNS-over-HTTPS | Enable > Enable DNS-over-HTTPS without insecure fallback | [Control the mode of DNS-over-HTTPS](/deployedge/microsoft-edge-browser-policies/dnsoverhttpsmode) |
| Microsoft Edge\Network settings | Specify URI template of desired DNS-over-HTTPS resolver | https://cloudflare-dns.com/dns-query | [Specify URI template of desired DNS-over-HTTPS resolver](/deployedge/microsoft-edge-browser-policies/dnsoverhttpstemplates) |
| Microsoft Edge\Network settings | DNS interception checks enabled | Enabled | [DNS interception checks enabled](/deployedge/microsoft-edge-browser-policies/dnsinterceptionchecksenabled) |
| Microsoft Edge\Network settings | Allow QUIC protocol | Disabled | [Allow QUIC protocol](/deployedge/microsoft-edge-browser-policies/quicallowed) |
| Microsoft Edge\Extensions | Control which extensions cannot be installed | ["external_component", "external_pref", "external_registry", "external_policy_download"] | [Control which extensions cannot be installed](/deployedge/microsoft-edge-browser-policies/extensioninstallblocklist) |
| Microsoft Edge\Extensions | Configure extension management settings | {"*": {"installation_mode": "blocked"}} | [Configure extension management settings](/deployedge/microsoft-edge-browser-policies/extensionsettings) |
| Microsoft Edge\Downloads and files | Allow download restrictions | Block dangerous downloads (1) | [Allow download restrictions](/deployedge/microsoft-edge-browser-policies/downloadrestrictions) |
| Microsoft Edge\Downloads and files | Set download directory | ${user_home}/Downloads/Edge | [Set download directory](/deployedge/microsoft-edge-browser-policies/downloaddirectory) |
| Microsoft Edge\Downloads and files | Ask where to save downloaded files | Enabled | [Ask where to save downloaded files](/deployedge/microsoft-edge-browser-policies/promptfordownloadlocation) |
| Microsoft Edge\Feature controls | Show Hubs Sidebar | Disabled | [Show Hubs Sidebar](/deployedge/microsoft-edge-browser-policies/hubssidebarenabled) |
| Microsoft Edge\Feature controls | Show Microsoft Rewards experiences | Disabled | [Show Microsoft Rewards experiences](/deployedge/microsoft-edge-browser-policies/showmicrosoftrewards) |
| Microsoft Edge\Feature controls | Shopping in Microsoft Edge Enabled | Disabled | [Shopping in Microsoft Edge Enabled](/deployedge/microsoft-edge-browser-policies/edgeshoppingassistantenabled) |
| Microsoft Edge\Feature controls | Control whether Microsoft 365 Copilot Chat shows in the Microsoft Edge for Business toolbar | Disabled | [Control whether Microsoft 365 Copilot Chat shows in the Microsoft Edge for Business toolbar](/deployedge/microsoft-edge-browser-policies/microsoft365copilotchaticonenabled) |
| Microsoft Edge\Feature controls | Enable Workspaces | Enabled | [Enable Workspaces](/deployedge/microsoft-edge-browser-policies/edgeworkspacesenabled) |
| Microsoft Edge\Feature controls | Allow or deny screen capture | Disabled | [Allow or deny screen capture](/deployedge/microsoft-edge-browser-policies/screencaptureallowed) |
| Microsoft Edge\Feature controls | Default sensors setting | Block (2) | [Default sensors setting](/deployedge/microsoft-edge-browser-policies/defaultsensorssetting) |
| Microsoft Edge Update\Update policy override | Update policy override default | Always allow updates (1) | [Update policy override default](/deployedge/microsoft-edge-update-policies#updatedefault) |
| Microsoft Edge Update\Update policy override | Auto-update check period override | 1440 | [Auto-update check period override](/deployedge/microsoft-edge-update-policies#autoupdatecheckperiodminutes) |
| Microsoft Edge Update\Preferences | Target Channel override | stable | [Target Channel override](/deployedge/microsoft-edge-update-policies#targetchannel) |
| Microsoft Edge Update\Preferences | Let users update all apps on metered connections | Updates disabled (1) | [Let users update all apps on metered connections](/deployedge/microsoft-edge-update-policies#meteredupdatesdefault) |
| Microsoft Edge Update\Experimentation and Configuration Service | Control updater's communication with the Experimentation and Configuration Service | Disabled (0) | [Control updater's communication with the Experimentation and Configuration Service](/deployedge/microsoft-edge-update-policies#updaterexperimentationandconfigurationservicecontrol) |

10. Select **Next**.  
11. For **Scope tags**, select the appropriate scope tag.  
12. For **Assignments**, assign to **SEB-Level1-Devices** group.  
13. Select **Next** to review the settings. Then choose **Create**.

### Level 2 - Enterprise enhanced security for Windows

Level 2 builds on the Level 1 by duplicating its configuration and adding enhanced controls and advanced privacy protection.

1. Go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Devices** > **Windows** > **Manage devices** > **Configuration**.  
3. Locate the *Level 1 – Enterprise basic security – Windows Settings Catalog* policy.  
4. Select the context menu (**⋯**) next to that policy, and then select **Duplicate**.  
5. In the **Duplicate policy** window, enter the following:  
   - **Name:** Level 2 – Enterprise enhanced security – Windows Settings Catalog  
   - **Description:** Enhanced browser security including Application Bound Encryption, extension controls, and advanced privacy settings.  
6. Select **Save**. This action takes you back to the **Windows configuration** page.  
7. Find your new Level 2 policy in the policy list. If it doesn’t appear, select **Refresh**.  
8. When the policy appears, select the context menu (**⋯**) next to the policy name, and then select **Edit**.  
9. On the **Basics** tab, verify that the name and description are correct, and then select **Next**.  
10. On the **Settings** tab, all Level 1 settings are already included. You can locate more settings using one of the following options:  
    - **Search for a setting:** Use the **search box** to find the setting name listed in the table. When multiple results appear, choose the entry that matches the **Category**.  
    - **Browse by category:** Expand **Microsoft Edge** and select the **Category** listed for that setting.  
11. Configure each setting using the **Value** specified in the table.

| Category | Setting | Value | Documentation |
|-----------|---------|--------|----------------|
| Microsoft Edge\SmartScreen settings | Configure Microsoft Defender SmartScreen to block potentially unwanted apps | Enabled | [Configure Microsoft Defender SmartScreen to block potentially unwanted apps](/deployedge/microsoft-edge-browser-policies/smartscreenpuadetectionenabled) |
| Microsoft Edge\Additional | Enable Application Bound Encryption | Enabled | [Enable Application Bound Encryption](/deployedge/microsoft-edge-browser-policies/applicationboundencryptionenabled) |
| Microsoft Edge\Additional | Disable synchronization of data using Microsoft sync services | Enabled | [Disable synchronization of data using Microsoft sync services](/deployedge/microsoft-edge-browser-policies/syncdisabled) |
| Microsoft Edge\Additional | Limit cookies from specific websites to the current session | Enabled | [Limit cookies from specific websites to the current session](/deployedge/microsoft-edge-browser-policies/cookiessessiononlyforurls) |
| Microsoft Edge\Additional | Configure Legacy SameSite cookie behavior setting | Disabled | [Configure Legacy SameSite cookie behavior setting](/deployedge/microsoft-edge-browser-policies/legacysamesitecookiebehaviorenabled) |
| Microsoft Edge\Additional | Configure automatic client certificate selection | ["*.company.com"] | [Configure automatic client certificate selection](/deployedge/microsoft-edge-browser-policies/autoselectcertificateforurls) |
| Microsoft Edge\Additional | Allow or deny screen capture | Disabled | [Allow or deny screen capture](/deployedge/microsoft-edge-browser-policies/screencaptureallowed) |
| Microsoft Edge\Additional | Control printing | Enabled | [Control printing](/deployedge/microsoft-edge-browser-policies/printingenabled) |
| Microsoft Edge\Additional | Set the system default printer as the default printer | Enabled | [Set the system default printer as the default printer](/deployedge/microsoft-edge-browser-policies/printpreviewusesystemdefaultprinter) |
| Microsoft Edge\Additional | Control use of the WebHID API | Enabled, Do not allow any site to request access to HID devices via the WebHID API | [Control use of the WebHID API](/deployedge/microsoft-edge-browser-policies/defaultwebhidguardsetting) |
| Microsoft Edge\Additional | Switch intranet sites to a work profile | Enabled | [Switch intranet sites to a work profile](/deployedge/microsoft-edge-browser-policies/switchintranetsitestoworkprofile) |
| Microsoft Edge\Startup, home page and new tab page | Configure InPrivate mode availability | InPrivate mode available (0) | [Configure InPrivate mode availability](/deployedge/microsoft-edge-browser-policies/inprivatemodeavailability) |
| Microsoft Edge\Content settings | Control where security restrictions on insecure origins apply | *.company.com | [Control where security restrictions on insecure origins apply](/deployedge/microsoft-edge-browser-policies/overridesecurityrestrictionsoninsecureorigin) |
| Microsoft Edge\Content settings | Allow insecure content on specified sites | [*.contoso.com] | [Allow insecure content on specified sites](/deployedge/microsoft-edge-browser-policies/insecurecontentallowedforurls) |
| Microsoft Edge\Content settings | Block insecure content on specified sites | ["*"] | [Block insecure content on specified sites](/deployedge/microsoft-edge-browser-policies/insecurecontentblockedforurls) |
| Microsoft Edge\Content settings | Grant access to specific sites to connect to specific USB devices | Enabled [*.contoso.com] | [Grant access to specific sites to connect to specific USB devices](/deployedge/microsoft-edge-browser-policies/webusballowdevicesforurls) |
| Microsoft Edge\Content settings | Control use of the Web Bluetooth API | Enabled, Do not allow any site to request access to Bluetooth devices via the Web Bluetooth API | [Control use of the Web Bluetooth API](/deployedge/microsoft-edge-browser-policies/defaultwebbluetoothguardsetting) |
| Microsoft Edge\Network settings | WebRTC IP Handling Policy for URL Patterns | default_public_and_private_interfaces | [WebRTC IP Handling Policy for URL Patterns](/deployedge/microsoft-edge-browser-policies/webrtciphandlingurl) |
| Microsoft Edge\Network settings | Manage exposure of local IP addresses by WebRTC | Enabled [*.contoso.com] | [Manage exposure of local IP addresses by WebRTC](/deployedge/microsoft-edge-browser-policies/webrtclocalipsallowedurls) |
| Microsoft Edge\Network settings | Control whether TLS 1.3 Early Data is enabled in Microsoft Edge | Enabled | [Control whether TLS 1.3 Early Data is enabled in Microsoft Edge](/deployedge/microsoft-edge-browser-policies/tls13earlydataenabled) |
| Microsoft Edge\Network settings | Enable the network service sandbox | Enabled | [Enable the network service sandbox](/deployedge/microsoft-edge-browser-policies/networkservicesandboxenabled) |
| Microsoft Edge\Proxy settings | Configure proxy settings | {"mode": "system"} | [Configure proxy settings](/deployedge/microsoft-edge-browser-policies/proxysettings) |
| Microsoft Edge\Extensions | Control which extensions cannot be installed | ["*"] | [Control which extensions cannot be installed](/deployedge/microsoft-edge-browser-policies/extensioninstallblocklist) |
| Microsoft Edge | Allow specific extensions to be installed | ["*.company.com"] | [Allow specific extensions to be installed](/deployedge/microsoft-edge-browser-policies/extensioninstallallowlist) |
| Microsoft Edge | Allow user-level native messaging hosts (installed without admin permissions) | Enabled | [Allow user-level native messaging hosts (installed without admin permissions)](/deployedge/microsoft-edge-browser-policies/nativemessaginguserlevelhosts) |
| Microsoft Edge | Configure native messaging block list | Enabled, ["*"] | [Configure native messaging block list](/deployedge/microsoft-edge-browser-policies/nativemessagingblocklist) |
| Microsoft Edge | Control which extensions are installed silently | [] | [Control which extensions are installed silently](/deployedge/microsoft-edge-browser-policies/extensioninstallforcelist) |
| Microsoft Edge | Configure extension and user script install sources | [] | [Configure extension and user script install sources](/deployedge/microsoft-edge-browser-policies/extensioninstallsources) |
| Microsoft Edge | Configure allowed extension types | [] | [Configure allowed extension types](/deployedge/microsoft-edge-browser-policies/extensionallowedtypes) |
| Microsoft Edge | Control Manifest v2 extension availability | Disabled | [Control Manifest v2 extension availability](/deployedge/microsoft-edge-browser-policies/extensionmanifestv2availability) |
| Microsoft Edge | Blocks external extensions from being installed | Enabled | [Blocks external extensions from being installed](/deployedge/microsoft-edge-browser-policies/blockexternalextensions) |
| Microsoft Edge | Set download directory | ${user_home}/Downloads/EdgeControlled | [Set download directory](/deployedge/microsoft-edge-browser-policies/downloaddirectory) |
| Microsoft Edge | Show Downloads button on the toolbar | Enabled | [Show Downloads button on the toolbar](/deployedge/microsoft-edge-browser-policies/showdownloadstoolbarbutton) |
| Microsoft Edge | Enable insecure download warnings | Enabled | [Enable insecure download warnings](/deployedge/microsoft-edge-browser-policies/showdownloadsinsecurewarningsenabled) |
| Microsoft Edge | Default images setting | Enabled, Allow sites to show images (1) | [Default images setting](/deployedge/microsoft-edge-browser-policies/defaultimagessetting) |
| Microsoft Edge | Default JavaScript setting | Enabled, Allow sites to run JavaScript (1) | [Default JavaScript setting](/deployedge/microsoft-edge-browser-policies/defaultjavascriptsetting) |
| Microsoft Edge | Configure plugins policy | Click to play (3) | [Configure plugins policy](/deployedge/microsoft-edge-browser-policies/defaultpluginssetting) |
| Microsoft Edge | Allow media autoplay for websites | Disabled | [Allow media autoplay for websites](/deployedge/microsoft-edge-browser-policies/autoplayallowed) |
| Microsoft Edge | Set the background tab inactivity timeout for sleeping tabs | 6Hours (21600) = 6 hours of inactivity | [Set the background tab inactivity timeout for sleeping tabs](/deployedge/microsoft-edge-browser-policies/sleepingtabstimeout) |
| Microsoft Edge | Delay before running idle actions | 30 | [Delay before running idle actions](/deployedge/microsoft-edge-browser-policies/idletimeout) |
| Microsoft Edge | Clear browsing data when Microsoft Edge closes | Enabled | [Clear browsing data when Microsoft Edge closes](/deployedge/microsoft-edge-browser-policies/clearbrowsingdataonexit) |
| Microsoft Edge | Notify a user that a browser restart is recommended or required for pending updates | Recommended - Show a recurring prompt to the user indicating that a restart is recommended | [Notify a user that a browser restart is recommended or required for pending updates](/deployedge/microsoft-edge-browser-policies/relaunchnotification) |
| Microsoft Edge | Enable startup boost | Disabled | [Enable startup boost](/deployedge/microsoft-edge-browser-policies/startupboostenabled) |
| Microsoft Edge | Configure when efficiency mode should become active | Enabled, Efficiency mode is always active | [Configure when efficiency mode should become active](/deployedge/microsoft-edge-browser-policies/efficiencymode) |
| Microsoft Edge | Configure sleeping tabs | Enabled | [Configure sleeping tabs](/deployedge/microsoft-edge-browser-policies/sleepingtabsenabled) |
| Microsoft Edge | Configure auto discard sleeping tabs | Enabled | [Configure auto discard sleeping tabs](/deployedge/microsoft-edge-browser-policies/autodiscardsleepingtabsenabled) |
| Microsoft Edge | Let screen reader users get image descriptions from Microsoft | Enabled | [Let screen reader users get image descriptions from Microsoft](/deployedge/microsoft-edge-browser-policies/accessibilityimagelabelsenabled) |
| Microsoft Edge | Control where developer tools can be used | Enabled | [Control where developer tools can be used](/deployedge/microsoft-edge-browser-policies/developertoolsavailability) |
| Microsoft Edge | Allow remote debugging | Disabled | [Allow remote debugging](/deployedge/microsoft-edge-browser-policies/remotedebuggingallowed) |
| Microsoft Edge Update\Update scheduling | Time period in each day to suppress auto-update check | Hour: 8, Minute: 0, Duration: 600 (suppress 8 AM – 6 PM) | [Time period in each day to suppress auto-update check](/deployedge/microsoft-edge-update-policies#updatessuppressed) |
| Microsoft Edge Update\Update policy override | Auto-update check period override | 720 (12 hours) | [Auto-update check period override](/deployedge/microsoft-edge-update-policies#autoupdatecheckperiodminutes) |
| Microsoft Edge Update\Update policy override | Update policy override default | Automatic silent updates only (3) | [Update policy override default](/deployedge/microsoft-edge-update-policies#updatedefault) |

12. Select **Next**.  
13. For **Assignments**, assign to **SEB-Level2-Devices** group.  
14. Select **Next** to review the settings. Then choose **Save**.  

### Level 3 – Enterprise high security for Windows

Level 3 builds on the Level 2 configuration by duplicating its policy and applying additional high-security controls such as URL allowlisting, stricter data protection, and site isolation.

1. Go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Devices** > **Windows** > **Manage devices** > **Configuration**.  
3. Locate the *Level 2 – Enterprise enhanced security – Windows Settings Catalog* policy.  
4. Select the context menu (**⋯**) next to that policy, and then select **Duplicate**.  
5. In the **Duplicate policy** window, enter the following:  
   - **Name:** Level 3 – Enterprise high security – Windows Settings Catalog  
   - **Description:** High-security browser configuration including URL allowlisting, site isolation, and maximum data protection.  
6. Select **Save**. This action takes you back to the **Windows configuration** page.  
7. Find your new Level 3 policy in the policy list. If it doesn’t appear, select **Refresh**.  
8. When the policy appears, select the context menu (**⋯**) next to the policy name, and then select **Edit**.  
9. On the **Basics** tab, verify that the name and description are correct, and then select **Next**.  
10. On the **Settings** tab, all Level 2 settings are already included. You can locate additional or modified settings using one of the following options:  
    - **Search for a setting:** Use the **search box** to find the setting name listed in the table. When multiple results appear, choose the entry that matches the **Category**.  
    - **Browse by category:** Expand **Microsoft Edge** and select the **Category** listed for that setting.  
11. Configure each setting using the **Value** specified in the table.

| Category | Setting | Value | Documentation |
|----------|---------|--------|----------------|
| Microsoft Edge\Content settings | Define a list of allowed URLs | ["*.company.com","*.microsoft.com","*.office.com"] | [Define a list of allowed URLs](/deployedge/microsoft-edge-browser-policies/urlallowlist) |
| Microsoft Edge\Content settings | Block access to a list of URLs | ["*"] | [Block access to a list of URLs](/deployedge/microsoft-edge-browser-policies/urlblocklist) |
| Microsoft Edge\Additional | Allow download restrictions | Block all downloads (3) | [Allow download restrictions](/deployedge/microsoft-edge-browser-policies/downloadrestrictions) |
| Microsoft Edge\Additional | Control where developer tools can be used | Disallowed (2) | [Control where developer tools can be used](/deployedge/microsoft-edge-browser-policies/developertoolsavailability) |
| Microsoft Edge\Additional | Enable site isolation for every site | Enabled | [Enable site isolation for every site](/deployedge/microsoft-edge-browser-policies/siteperprocess) |
| Microsoft Edge\Additional | Send required and optional diagnostic data about browser usage | Off (0) | [Send required and optional diagnostic data about browser usage](/deployedge/microsoft-edge-browser-policies/diagnosticdata) |
| Microsoft Edge\Startup, home page and new tab page | Configure InPrivate mode availability | InPrivate mode forced (1) | [Configure InPrivate mode availability](/deployedge/microsoft-edge-browser-policies/inprivatemodeavailability) |
| Microsoft Edge\User Data & Retention | Limits the number of user data snapshots retained for use in case of emergency rollback | 1 | [Limits the number of user data snapshots retained for use in case of emergency rollback](/deployedge/microsoft-edge-browser-policies/userdatasnapshotretentionlimit) |
| Microsoft Edge\User Data & Retention | Browsing Data Lifetime Settings | [{"data_types": ["browsing_history", "download_history", "cookies_and_other_site_data", "cached_images_and_files"], "time_to_live_in_hours": 24}] | [Browsing Data Lifetime Settings](/deployedge/microsoft-edge-browser-policies/browsingdatalifetime) |
| Microsoft Edge\User Data & Retention | Enable use of ephemeral profiles | Enabled | [Enable use of ephemeral profiles](/deployedge/microsoft-edge-browser-policies/forceephemeralprofiles) |
| Microsoft Edge\Network settings | Enable network prediction | Never predict (2) | [Enable network prediction](/deployedge/microsoft-edge-browser-policies/networkpredictionoptions) |
| Microsoft Edge\Network settings | Restrict the range of local UDP ports used by WebRTC | "10000-10100" | [Restrict the range of local UDP ports used by WebRTC](/deployedge/microsoft-edge-browser-policies/webrtcudpportrange) |
| Microsoft Edge\Proxy settings | Configure proxy bypass list | [] | [Configure proxy bypass list](/deployedge/microsoft-edge-browser-policies/proxybypasslist) |
| Microsoft Edge\Proxy settings | Configure proxy pac URL | "https://proxy.company.com/proxy.pac" | [Configure proxy pac URL](/deployedge/microsoft-edge-browser-policies/proxypacurl) |
| Microsoft Edge\Network isolation | Maximum number of concurrent connections to the proxy server | Enabled, 6 | [Maximum number of concurrent connections to the proxy server](/deployedge/microsoft-edge-browser-policies/maxconnectionsperproxy) |
| Microsoft Edge\Additional | Application Guard Traffic Identification | Enabled | [Application Guard Traffic Identification](/deployedge/microsoft-edge-browser-policies/applicationguardtrafficidentificationenabled) |
| Microsoft Edge\Additional | Prevents files from being uploaded while in Application Guard | Enabled | [Prevents files from being uploaded while in Application Guard](/deployedge/microsoft-edge-browser-policies/applicationguarduploadblockingenabled) |
| Microsoft Edge\Data Loss Prevention | Allow clipboard use on specific sites | Enabled, *.company.com | [Allow clipboard use on specific sites](/deployedge/microsoft-edge-browser-policies/clipboardallowedforurls) |
| Microsoft Edge\Data Loss Prevention | Block clipboard use on specific sites | Enabled, * | [Block clipboard use on specific sites](/deployedge/microsoft-edge-browser-policies/clipboardblockedforurls) |
| Microsoft Edge\Data Loss Prevention | Control printing | Disabled | [Control printing](/deployedge/microsoft-edge-browser-policies/printingenabled) |
| Microsoft Edge\Data Loss Prevention | Force Microsoft Defender SmartScreen checks on downloads from trusted sources | Enabled | [Force Microsoft Defender SmartScreen checks on downloads from trusted sources](/deployedge/microsoft-edge-browser-policies/smartscreenpromptoverrideenabled) |
| Microsoft Edge\Content settings | Minimum TLS version enabled | TLS 1.2 | [Minimum TLS version enabled](/deployedge/microsoft-edge-browser-policies/sslversionmin) |
| Microsoft Edge\Privacy | Allow user feedback | Disabled | [Allow user feedback](/deployedge/microsoft-edge-browser-policies/userfeedbackallowed) |
| Microsoft Edge\Privacy | URL reporting in Edge diagnostic data enabled | Disabled | [URL reporting in Edge diagnostic data enabled](/deployedge/microsoft-edge-browser-policies/urldiagnosticdataenabled) |
| Microsoft Edge\Session isolation | Enable site isolation for specific origins | Disabled | [Enable site isolation for specific origins](/deployedge/microsoft-edge-browser-policies/isolateorigins) |
| Microsoft Edge Update\Update policy override | Target version override | 131.0.2903.112 | [Target version override](/deployedge/microsoft-edge-update-policies#targetversionprefix) |
| Microsoft Edge Update\Update policy override | Update policy override default | Manual updates only (2) | [Update policy override default](/deployedge/microsoft-edge-update-policies#updatedefault) |
| Microsoft Edge Update\Update policy override | Rollback to Target version | Enabled (1) | [Rollback to Target version](/deployedge/microsoft-edge-update-policies#rollbacktotargetversion) |
| Microsoft Edge Update\Update policy override | Auto-update check period override | 10080 (7 days) | [Auto-update check period override](/deployedge/microsoft-edge-update-policies#autoupdatecheckperiodminutes) |
| Microsoft Edge Update\Update scheduling | Time period in each day to suppress auto-update check | Hour: 6, Minute: 0, Duration: 840 (suppress 6 AM – 8 PM) | [Time period in each day to suppress auto-update check](/deployedge/microsoft-edge-update-policies#updatessuppressed) |
| Microsoft Edge Update\Installation behavior | Allow installation default | Always allow Machine-Wide Installs but not Per-User Installs (4) | [Allow installation default](/deployedge/microsoft-edge-update-policies#installdefault) |
| Microsoft Edge Update\Preview enrollment | Allow users in the Windows Insider Program to be enrolled in Edge Preview | Disabled (0) | [Allow users in the Windows Insider Program to be enrolled in Edge Preview](/deployedge/microsoft-edge-update-policies#edgepreview) |
| Microsoft Edge Update\Shortcuts | Remove Desktop Shortcuts upon update default | Force delete system-level and user-level Desktop Shortcuts (2) | [Remove Desktop Shortcuts upon update default](/deployedge/microsoft-edge-update-policies#removedesktopshortcutdefault) |

12. Select **Next**.  
13. For **Assignments**, assign to **SEB-Level2-Devices** group.  
14. Select **Next** to review the settings. Then choose **Save**.   

### Validation

After deploying all Windows security levels, validate that the policies have applied correctly and that each configuration behaves as expected on a test device.

- **Policy verification:**  
  In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Windows** > **Manage devices** > **Configuration**, and locate the policies for each level.  
  Select a policy, and then choose **Device assignment status** to confirm that all assigned devices show a status of *Succeeded*.  
  You can also review **Per setting status** to verify individual policy settings applied successfully.  
  On a test device, open Microsoft Edge and go to `edge://policy` to confirm that key settings appear as **Active** and not **Error**.

- **Level 1 – Basic security validation:**  
  Confirm that SmartScreen protection and Automatic HTTPS are enabled.  
  Verify that third-party cookies, pop-ups, and notifications are blocked and that password saving, autofill, and data synchronization are disabled.  
  Check that automatic updates are enabled and that browsing and download activity complies with baseline protections.

- **Level 2 – Enhanced security validation:**  
  Confirm that Application Bound Encryption (ABE) is enabled.  
  Verify that extension installation is blocked except for approved entries, InPrivate mode is available, and browser sync remains disabled.  
  Check that downloads are restricted, SmartScreen for trusted sources is active, and background apps do not continue running after Edge closes.  
  Validate that 120+ settings are applied by reviewing the *Applied policies* list in `edge://policy`.

- **Level 3 – High security validation:**  
  Confirm that URL filtering restricts browsing to approved domains (for example, `*.company.com`, `*.microsoft.com`, `*.office.com`, and `login.microsoftonline.com`).  
  Navigate to a non-allowlisted site to ensure it is blocked or automatically opened in an **Application Guard container**.  
  Verify that all downloads are blocked, printing and clipboard access are disabled, and browsing data clears automatically when Edge closes.  
  Confirm that InPrivate mode is forced, Application Guard isolation is active, and all optional features (Collections, Games, Sidebar, Drop, Wallet, Copilot) are disabled.

If any settings do not apply, sync the device from the **Company Portal** app or verify group assignments (`SEB-Level1-Devices`, `SEB-Level2-Devices`, or `SEB-Level3-Devices`).  
For additional confirmation, monitor **edge://policy** and the **Device configuration report** in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) to ensure the expected number of policies are active per level.

::: zone-end

::: zone pivot="macos"

## Settings Catalog for macOS

Settings Catalog for macOS provides foundational browser security for enrolled Mac devices.

> **Microsoft Documentation:**
> - [Settings Catalog for macOS](../configuration/settings-catalog.md)
> - [Microsoft Edge Browser Policies](/deployedge/microsoft-edge-policies)

> [!IMPORTANT]
> macOS Platform Limitations
>
> - App Protection Policies (APP): Not available for macOS
> - App Configuration Policies (ACP): Not available for macOS
> - Settings Catalog only: macOS Microsoft Edge management relies solely on Settings Catalog policies

**Prerequisites:**

- macOS 12+ (Monterey or later)  
- Device enrolled via Apple Business Manager (recommended)  
- Microsoft Edge installed  
- Administrative access  

### Level 1 – Enterprise basic security for macOS

Level 1 establishes foundational browser protections for enrolled macOS devices using Microsoft Edge. This level focuses on essential data-boundary, privacy, and network-security controls.

1. Go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Devices** > **macOS** > **Managed devices** > **Configuration** > **Create** > **New policy**.  
3. In the **Create a profile** window, verify that **Platform** is set to **macOS** (this option is pre-selected and cannot be changed).  
4. For **Profile type**, choose **Settings catalog**, and then select **Create**.  
5. On the **Basics** tab, enter:  
   - **Name:** Edge macOS Level 1 Basic  
   - **Description:** Foundational browser configuration for Microsoft Edge addressing gap analysis findings (Certificate management, network policies, system integration)
6. Select **Next**.  
7. On the **Configuration settings** tab, select **+ Add settings**.  
8. In the **Settings picker**, locate each setting using one of the following options:  
   - **Search for a setting:** Use the **search box** to find the setting name listed in the table. When multiple results appear, choose the entry that matches the **Category**.  
   - **Browse by category:** Expand **Microsoft Edge** and select the **Category** listed for that setting.  
9. Configure each setting using the **Value** specified in the table.  

| Category | Setting | Value | Documentation |
|----------|---------|--------|----------------|
| Microsoft Edge | Configure Microsoft Defender SmartScreen | Enabled | [Configure Microsoft Defender SmartScreen](/deployedge/microsoft-edge-browser-policies/smartscreenenabled) |
| Microsoft Edge | Configure Automatic HTTPS | Enabled | [Configure Automatic HTTPS](/deployedge/microsoft-edge-browser-policies/httpsonlymode) |
| Microsoft Edge | Default pop-up window setting | Do not allow any site to show popups (2) | [Default pop-up window setting](/deployedge/microsoft-edge-browser-policies/defaultpopupssetting) |
| Microsoft Edge | DNS interception checks enabled | Enabled | [DNS interception checks enabled](/deployedge/microsoft-edge-browser-policies/dnsinterceptionchecksenabled) |
| Microsoft Edge | Automatically select client certificates for these sites | ["*.company.com"] | [Automatically select client certificates](/deployedge/microsoft-edge-browser-policies/autoselectcertificateforurls) |
| Microsoft Edge | Control the mode of DNS-over-HTTPS | secure (secure) = Enable DNS-over-HTTPS without insecure fallback | [Control the mode of DNS-over-HTTPS](/deployedge/microsoft-edge-browser-policies/dnsoverhttpsmode) |
| Microsoft Edge | Allow QUIC protocol | Disabled for security | [Allow QUIC protocol](/deployedge/microsoft-edge-browser-policies/quicallowed) |
| Microsoft Edge | Configure the home page URL | https://portal.company.com | [Configure the home page URL](/deployedge/microsoft-edge-browser-policies/homepagelocation) |
| Microsoft Edge | Show Home button on toolbar | Enabled | [Show Home button on toolbar](/deployedge/microsoft-edge-browser-policies/showhomebutton) |
| Microsoft Edge | Configure the new tab page URL | https://portal.company.com | [Configure the new tab page URL](/deployedge/microsoft-edge-browser-policies/newtabpageurl) |
| Microsoft Edge | Hide the First-run experience and splash screen | Enabled | [Hide the First-run experience](/deployedge/microsoft-edge-browser-policies/hidefirstrunexperience) |
| Microsoft Edge | Enable saving passwords to the password manager | Disabled | [Enable saving passwords to the password manager](/deployedge/microsoft-edge-browser-policies/passwordmanagerenabled) |
| Microsoft Edge | Enable AutoFill for addresses | Disabled | [Enable AutoFill for addresses](/deployedge/microsoft-edge-browser-policies/autofilladdressenabled) |
| Microsoft Edge | Enable AutoFill for credit cards | Disabled | [Enable AutoFill for credit cards](/deployedge/microsoft-edge-browser-policies/autofillcreditcardenabled) |
| Microsoft Edge | Block tracking of users' web-browsing activity | Strict (3) | [Block tracking of users' web-browsing activity](/deployedge/microsoft-edge-browser-policies/trackingprevention) |
| Microsoft Edge | Allow personalization of ads, search and news | Disabled | [Allow personalization](/deployedge/microsoft-edge-browser-policies/personalizationreportingenabled) |
| Microsoft Edge | Enable network prediction | Don't predict network actions (2) | [Enable network prediction](/deployedge/microsoft-edge-browser-policies/networkpredictionoptions) |
| Microsoft Edge | Enable search suggestions | Disabled | [Enable search suggestions](/deployedge/microsoft-edge-browser-policies/searchsuggestenabled) |
| Microsoft Edge | Send required and optional diagnostic data | Off (0) | [Send required and optional diagnostic data](/deployedge/microsoft-edge-browser-policies/diagnosticdata) |
| Microsoft Edge | Allow importing of autofill form data | Disabled | [Allow importing of autofill form data](/deployedge/microsoft-edge-browser-policies/importautofillformdata) |
| Microsoft Edge | Allow importing of saved passwords | Disabled | [Allow importing of saved passwords](/deployedge/microsoft-edge-browser-policies/importsavedpasswords) |
| Microsoft Edge Update | Specifies how Microsoft Edge Update handles available updates from Microsoft Edge | automatic-silent-only (automatic-silent-only) | [UpdatePolicyOverride](/deployedge/microsoft-edge-update-policies#updatedefault) |
| Microsoft Edge Update | Enable component updates in Microsoft Edge | Enabled | [ComponentUpdatesEnabled](/deployedge/microsoft-edge-update-policies#componentupdatesenabled) |

10. Select **Next**.  
11. For **Scope tags**, select the appropriate scope tag.  
12. For **Assignments**, assign to **SEB-Level1-Devices** group.  
13. Select **Next** to review the settings. Then choose **Create**.  

### Level 2 - Enterprise enhanced security for macOS

Level 2 builds on the Level 1 by duplicating its configuration and adding enhanced controls and advanced privacy protection.

1. Go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Devices** > **macOS** > **Manage devices** > **Configuration**.  
3. Locate the *Level 1 – Enterprise basic security – macOS Settings Catalog* policy.  
4. Select the context menu (**⋯**) next to that policy, and then select **Duplicate**.  
5. In the **Duplicate policy** window, enter the following:  
   - **Name:** Level 2 – Enterprise enhanced security – macOS Settings Catalog  
   - **Description:** Enhanced security with extension blocking and privacy controls.  
6. Select **Save**. This action takes you back to the **macOS configuration** page.  
7. Find your new Level 2 policy in the policy list. If it doesn't appear, select **Refresh**.  
8. When the policy appears, select the context menu (**⋯**) next to the policy name, and then select **Edit**.  
9. On the **Basics** tab, verify that the name and description are correct, and then select **Next**.  
10. On the **Settings** tab, all Level 1 settings are already included. You can locate additional or modified settings using one of the following options:  
    - **Search for a setting:** Use the **search box** to find the setting name listed in the table. When multiple results appear, choose the entry that matches the **Category**.  
    - **Browse by category:** Expand **Microsoft Edge** and select the **Category** listed for that setting.  
11. Configure each setting using the **Value** specified in the table.

| Category | Setting | Value | Documentation |
|----------|---------|--------|----------------|
| Microsoft Edge | Enhance the security state in Microsoft Edge | Strict | [Enhance the security state in Microsoft Edge](/deployedge/microsoft-edge-browser-policies/enhancesecuritymode) |
| Microsoft Edge | Configure InPrivate mode availability | Disabled (1) | [Configure InPrivate mode availability](/deployedge/microsoft-edge-browser-policies/inprivatemodeavailability) |
| Microsoft Edge | Control which extensions cannot be installed | ["*"] | [Control which extensions cannot be installed](/deployedge/microsoft-edge-browser-policies/extensioninstallblocklist) |
| Microsoft Edge | Control use of the WebUSB API | BlockWebUsb (2) | [Control use of the WebUSB API](/deployedge/microsoft-edge-browser-policies/defaultwebusbguardsetting) |
| Microsoft Edge | Control use of the WebHID API | BlockWebHid (2) | [Control use of the WebHID API](/deployedge/microsoft-edge-browser-policies/defaultwebhidguardsetting) |
| Microsoft Edge | Control where developer tools can be used | DeveloperToolsDisallowed (2) | [Control where developer tools can be used](/deployedge/microsoft-edge-browser-policies/developertoolsavailability) |
| Microsoft Edge | Control the availability of developer mode on extensions page | Disallow (1) | [Control the availability of developer mode on extensions page](/deployedge/microsoft-edge-browser-policies/extensiondevelopermodesettings) |
| Microsoft Edge | Enable Microsoft Defender SmartScreen DNS requests | Enabled | [Enable Microsoft Defender SmartScreen DNS requests](/deployedge/microsoft-edge-browser-policies/smartscreendnsrequestsenabled) |
| Microsoft Edge | Shopping in Microsoft Edge Enabled | Disabled | [Shopping in Microsoft Edge Enabled](/deployedge/microsoft-edge-browser-policies/edgeshoppingassistantenabled) |
| Microsoft Edge | Edge Wallet E-Tree Enabled | Disabled | [Edge Wallet E-Tree Enabled](/deployedge/microsoft-edge-browser-policies/edgewalletetreeenabled) |
| Microsoft Edge | Enable Microsoft Bing trending suggestions in the address bar | Disabled | [Enable Microsoft Bing trending suggestions](/deployedge/microsoft-edge-browser-policies/addressbartrendingsuggestenabled) |

12. Select **Next**.  
13. For **Assignments**, assign to **SEB-Level2-Devices** group.  
14. Select **Next** to review the settings. Then choose **Save**.  

### Level 3 - Enterprise high security for macOS

Level 3 builds on the Level 2 configuration by duplicating its policy and applying additional high-security controls such as URL allowlisting, stricter data protection, and site isolation.

1. Go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Devices** > **macOS** > **Manage devices** > **Configuration**.  
3. Locate the *Level 2 – Enterprise enhanced security – macOS Settings Catalog* policy.  
4. Select the context menu (**⋯**) next to that policy, and then select **Duplicate**.  
5. In the **Duplicate policy** window, enter the following:  
   - **Name:** Level 3 – Enterprise high security – macOS Settings Catalog  
   - **Description:** High-security configuration with URL filtering and maximum restrictions.  
6. Select **Save**. This action takes you back to the **macOS configuration** page.  
7. Find your new Level 3 policy in the policy list. If it doesn't appear, select **Refresh**.  
8. When the policy appears, select the context menu (**⋯**) next to the policy name, and then select **Edit**.  
9. On the **Basics** tab, verify that the name and description are correct, and then select **Next**.  
10. On the **Settings** tab, all Level 2 settings are already included. You can locate additional or modified settings using one of the following options:  
    - **Search for a setting:** Use the **search box** to find the setting name listed in the table. When multiple results appear, choose the entry that matches the **Category**.  
    - **Browse by category:** Expand **Microsoft Edge** and select the **Category** listed for that setting.  
11. Configure each setting using the **Value** specified in the table.

| Category | Setting | Value | Documentation |
|----------|---------|--------|----------------|
| Microsoft Edge | Configure InPrivate mode availability | InPrivate mode forced (2) | [Configure InPrivate mode availability](/deployedge/microsoft-edge-browser-policies/inprivatemodeavailability) |
| Microsoft Edge | Define a list of allowed URLs | ["*.company.com","*.microsoft.com","*.office.com"] | [Define a list of allowed URLs](/deployedge/microsoft-edge-browser-policies/urlallowlist) |
| Microsoft Edge | Block access to a list of URLs | ["*"] | [Block access to a list of URLs](/deployedge/microsoft-edge-browser-policies/urlblocklist) |
| Microsoft Edge | Allow download restrictions | Block all downloads (4) | [Allow download restrictions](/deployedge/microsoft-edge-browser-policies/downloadrestrictions) |
| Microsoft Edge | Enable site isolation for every site | Enabled | [Enable site isolation for every site](/deployedge/microsoft-edge-browser-policies/siteperprocess) |
| Microsoft Edge | Disable synchronization of data using Microsoft sync services | Enabled | [Disable synchronization of data using Microsoft sync services](/deployedge/microsoft-edge-browser-policies/syncdisabled) |
| Microsoft Edge | Clear browsing data when Microsoft Edge closes | Enabled | [Clear browsing data when Microsoft Edge closes](/deployedge/microsoft-edge-browser-policies/clearbrowsingdataonexit) |
| Microsoft Edge | Allow or deny screen capture | Disabled | [Allow or deny screen capture](/deployedge/microsoft-edge-browser-policies/screencaptureallowed) |
| Microsoft Edge | Enable printing | Disabled | [Enable printing](/deployedge/microsoft-edge-browser-policies/printingenabled) |
| Microsoft Edge | Configure clipboard | [] | [Configure clipboard](/deployedge/microsoft-edge-browser-policies/clipboardallowedforurls) |
| Microsoft Edge | Enable use of ephemeral profiles | Enabled | [Enable use of ephemeral profiles](/deployedge/microsoft-edge-browser-policies/forceephemeralprofiles) |
| Microsoft Edge | Manage exposure of local IP addresses by WebRTC | [] | [Manage exposure of local IP addresses by WebRTC](/deployedge/microsoft-edge-browser-policies/webrtclocalipsallowedurls) |
| Microsoft Edge | Control which extensions are installed silently | [] | [Control which extensions are installed silently](/deployedge/microsoft-edge-browser-policies/extensioninstallforcelist) |
| Microsoft Edge | Configure allowed extension types | extension (extension) | [Configure allowed extension types](/deployedge/microsoft-edge-browser-policies/extensionallowedtypes) |
| Microsoft Edge | Configure tracking prevention exceptions for specific sites | *.company.com | [Configure tracking prevention exceptions for specific sites](/deployedge/microsoft-edge-browser-policies/allowtrackingforurls) |
| Microsoft Edge | Allow media autoplay for websites | Disabled | [Allow media autoplay for websites](/deployedge/microsoft-edge-browser-policies/autoplayallowed) |
| Microsoft Edge | Allow or block video capture | Disabled | [Allow or block video capture](/deployedge/microsoft-edge-browser-policies/videocaptureallowed) |
| Microsoft Edge | Allow or block audio capture | Disabled | [Allow or block audio capture](/deployedge/microsoft-edge-browser-policies/audiocaptureallowed) |
| Microsoft Edge | Default notification setting | BlockNotifications (2) | [Default notification setting](/deployedge/microsoft-edge-browser-policies/defaultnotificationssetting) |
| Microsoft Edge | Default geolocation setting | BlockGeolocation (2) | [Default geolocation setting](/deployedge/microsoft-edge-browser-policies/defaultgeolocationsetting) |
| Microsoft Edge | Default sensors setting | Do not allow any site to access sensors | [Default sensors setting](/deployedge/microsoft-edge-browser-policies/defaultsensorssetting) |

12. Select **Next**.  
13. For **Assignments**, assign to **SEB-Level3-Devices** group. 
14. Select **Next** to review the settings. Then choose **Save**.

## Validation

After deploying Settings Catalog policies:

1. **Policy Deployment**: Check Intune console for successful policy deployment  
2. **Endpoint Verification**: On device, navigate to edge://policy and verify settings  
3. **Security Testing**: Test blocked features (downloads, extensions, URLs) per level  
4. **User Experience**: Verify browser functionality meets business requirements  

::: zone-end

## Next steps

Continue to [Step 6](mamedge-6-security-baseline.md) to deploy the Microsoft Edge security baseline.

