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

1. Go to the [Microsoft Intune admin center](https://intune.microsoft.com).  
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
|-----------|----------|-------|----------------|
| Microsoft Edge\SmartScreen settings | Configure Microsoft Defender<br>SmartScreen to protect users<br>from malicious sites | Enabled | [Configure Microsoft Defender<br>SmartScreen to protect users<br>from malicious sites](/deployedge/microsoft-edge-browser-policies/smartscreenenabled) |
| Microsoft Edge\Automatic HTTPS | Enable automatic<br>HTTPS upgrades | Enabled | [Enable automatic<br>HTTPS upgrades](/deployedge/microsoft-edge-browser-policies/httpsonlymode) |
| Microsoft Edge\Content settings | Block tracking of users’<br>web-browsing activity | Strict (3) | [Block tracking of users’<br>web-browsing activity](/deployedge/microsoft-edge-browser-policies/trackingprevention) |
| Microsoft Edge\Network settings | Enable network prediction | Don’t predict (2) | [Enable network prediction](/deployedge/microsoft-edge-browser-policies/networkpredictionoptions) |
| Microsoft Edge\Search experience | Enable search suggestions<br>for the address bar | Disabled | [Enable search suggestions<br>for the address bar](/deployedge/microsoft-edge-browser-policies/searchsuggestenabled) |
| Microsoft Edge\Diagnostics | Send required and optional<br>diagnostic data about browser usage | Off (0) | [Send required and optional<br>diagnostic data about browser usage](/deployedge/microsoft-edge-browser-policies/diagnosticdata) |
| Microsoft Edge\Privacy Sandbox | Configure Do Not Track setting<br>to signal user preference | Enabled | [Configure Do Not Track setting<br>to signal user preference](/deployedge/microsoft-edge-browser-policies/configuredonottrack) |
| Microsoft Edge\Content settings | Default pop-up window setting (Device) | Don’t allow any site to show pop-ups (2) | [Default pop-up window setting (Device)](/deployedge/microsoft-edge-browser-policies/defaultpopupssetting) |
| Microsoft Edge\Content settings | Default geolocation setting (Device) | Don’t allow any site to track location (2) | [Default geolocation setting (Device)](/deployedge/microsoft-edge-browser-policies/defaultgeolocationbehavior) |
| Microsoft Edge\Content settings | Default sensors setting (Device) | Don’t allow sites to access sensors (2) | [Default sensors setting (Device)](/deployedge/microsoft-edge-browser-policies/defaultsensorssetting) |
| Microsoft Edge\Content settings | Default notification setting (Device) | Don’t allow any site to show notifications (2) | [Default notification setting (Device)](/deployedge/microsoft-edge-browser-policies/defaultnotificationssetting) |
| Microsoft Edge\Content settings | Default media stream setting (Device) | Don’t allow access to camera / mic (2) | [Default media stream setting (Device)](/deployedge/microsoft-edge-browser-policies/mediastreamsettings) |
| Microsoft Edge\Content settings | Block third-party cookies to improve privacy | Enabled | [Block third-party cookies to improve privacy](/deployedge/microsoft-edge-browser-policies/thirdpartycookiesblocked) |
| Microsoft Edge\Password Manager and Protection | Enable saving passwords to the password manager | Disabled | [Enable saving passwords to the password manager](/deployedge/microsoft-edge-browser-policies/passwordmanagerenabled) |
| Microsoft Edge\Password Manager and Protection | Enable AutoFill for addresses and contact information | Disabled | [Enable AutoFill for addresses and contact information](/deployedge/microsoft-edge-browser-policies/autofilladdressenabled) |
| Microsoft Edge\Password Manager and Protection | Enable AutoFill for payment instruments and cards | Disabled | [Enable AutoFill for payment instruments and cards](/deployedge/microsoft-edge-browser-policies/autofillcreditcardenabled) |
| Microsoft Edge\Password Manager and Protection | Biometric authentication for local data storage reauth | Disabled | [Biometric authentication for local data storage reauth](/deployedge/microsoft-edge-browser-policies/biometricauthenticationbeforefilling) |
| Microsoft Edge\Import Controls | Allow importing of autofill form data | Disabled | [Allow importing of autofill form data](/deployedge/microsoft-edge-browser-policies/importautofillformdata) |
| Microsoft Edge\Import Controls | Allow importing of saved passwords | Disabled | [Allow importing of saved passwords](/deployedge/microsoft-edge-browser-policies/importsavedpasswords) |
| Microsoft Edge\Import Controls | Allow importing of browsing history | Disabled | [Allow importing of browsing history](/deployedge/microsoft-edge-browser-policies/importhistory) |
| Microsoft Edge\Import Controls | Allow importing of payment information | Disabled | [Allow importing of payment information](/deployedge/microsoft-edge-browser-policies/importpaymentinfo) |
| Microsoft Edge\Startup, home page and new tab page | Configure the home page URL | https://portal.office.com | [Configure the home page URL](/deployedge/microsoft-edge-browser-policies/homepagelocation) |
| Microsoft Edge\Startup, home page and new tab page | Show Home button on toolbar for user convenience | Enabled | [Show Home button on toolbar for user convenience](/deployedge/microsoft-edge-browser-policies/showhomebutton) |
| Microsoft Edge\Startup, home page and new tab page | Hide the First-run experience and splash screen for users | Enabled | [Hide the First-run experience and splash screen for users](/deployedge/microsoft-edge-browser-policies/hidefirstrunexperience) |
| Microsoft Edge\Shopping and Commerce | Shopping in Microsoft Edge feature | Disabled | [Shopping in Microsoft Edge feature](/deployedge/microsoft-edge-browser-policies/edgeshoppingassistantenabled) |
| Microsoft Edge\Wallet and Payments | Allow users to be prompted for Microsoft Wallet password | Disabled | [Allow users to be prompted for Microsoft Wallet password](/deployedge/microsoft-edge-browser-policies/walletserviceenabled) |
| Microsoft Edge\Feature Recommendations | Show feature and merchandise recommendations in Edge | Disabled | [Show feature and merchandise recommendations in Edge](/deployedge/microsoft-edge-browser-policies/showfeatureandmerchandiserecommendationsenabled) |
| Microsoft Edge\Feature Recommendations | Allow feature suggestions in sidebar | Disabled | [Allow feature suggestions in sidebar](/deployedge/microsoft-edge-browser-policies/sidebarfeaturesuggestionsenabled) |
| Microsoft Edge\Sidebar Management | Enable Microsoft Search integration in sidebar | Disabled | [Enable Microsoft Search integration in sidebar](/deployedge/microsoft-edge-browser-policies/sidebarmicrosoftsearchenabled) |
| Microsoft Edge\Sidebar Management | Allow side panel sites list customization | Disabled | [Allow side panel sites list customization](/deployedge/microsoft-edge-browser-policies/sidebarcustomizationsettings) |
| Microsoft Edge\Network Security | Control the mode of DNS-over-HTTPS | Enabled, fallback to insecure DNS allowed | [Control the mode of DNS-over-HTTPS](/deployedge/microsoft-edge-browser-policies/dnsoverhttpsmode) |
| Microsoft Edge\Network Security | DNS interception checks for validation | Enabled | [DNS interception checks for validation](/deployedge/microsoft-edge-browser-policies/dnsinterceptionchecksenabled) |
| Microsoft Edge\Network Security | Allow QUIC protocol for connectivity | Disabled | [Allow QUIC protocol for connectivity](/deployedge/microsoft-edge-browser-policies/quicallowed) |
| Microsoft Edge\Search Provider | Enable the default search provider | Enabled | [Enable the default search provider](/deployedge/microsoft-edge-browser-policies/defaultsearchproviderenabled) |
| Microsoft Edge\Search Provider | Default search provider name | Microsoft Bing | [Default search provider name](/deployedge/microsoft-edge-browser-policies/defaultsearchprovidername) |
| Microsoft Edge\Search Provider | Default search provider search URL | https://www.bing.com/search?q={searchTerms} | [Default search provider search URL](/deployedge/microsoft-edge-browser-policies/defaultsearchprovidersearchurl) |
| Microsoft Edge\Search Provider | Default search provider keyword | bing | [Default search provider keyword](/deployedge/microsoft-edge-browser-policies/defaultsearchproviderkeyword) |
| Microsoft Edge\Privacy Sandbox | Privacy Sandbox Ad measurement feature | Disabled | [Privacy Sandbox Ad measurement feature](/deployedge/microsoft-edge-browser-policies/privacysandboxadmeasurementenabled) |
| Microsoft Edge\Privacy Sandbox | Privacy Sandbox Topics feature | Disabled | [Privacy Sandbox Topics feature](/deployedge/microsoft-edge-browser-policies/privacysandboxtopicsenabled) |
| Microsoft Edge\Privacy Sandbox | Privacy Sandbox Fledge feature | Disabled | [Privacy Sandbox Fledge feature](/deployedge/microsoft-edge-browser-policies/privacysandboxfledgeenabled) |
| Microsoft Edge\Translation | Personalize detected languages for website translation | Disabled | [Personalize detected languages for website translation](/deployedge/microsoft-edge-browser-policies/translateenabled) |
| Microsoft Edge Update\Experimentation and Configuration Service | Experimentation and Configuration Service Control | Retrieve configurations (1) | [Experimentation and Configuration Service Control](/deployedge/microsoft-edge-update-policies#updaterexperimentationandconfigurationservicecontrol) |
| Microsoft Edge Update\Experimentation and Configuration Service | Control updater’s communication with the Experimentation and Configuration Service | Disabled (0) | [Control updater’s communication with the Experimentation and Configuration Service](/deployedge/microsoft-edge-update-policies#updaterexperimentationandconfigurationservicecontrol) |

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
|-----------|----------|-------|----------------|
| Microsoft Edge\Additional | Configure Legacy<br>SameSite cookie<br>behavior setting | Disabled | [Configure Legacy<br>SameSite cookie<br>behavior setting](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/legacysamesitecookiebehaviorenabled) |
| Microsoft Edge\Additional | Configure automatic<br>client certificate<br>selection | ["*.company.com"] | [Configure automatic<br>client certificate<br>selection](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/autoselectcertificateforurls) |
| Microsoft Edge\Additional | Control printing | Enabled | [Control printing](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/printingenabled) |
| Microsoft Edge\Additional | Control use of<br>the WebHID API | Enabled, Do not allow any site to request access to HID devices via the WebHID API | [Control use of<br>the WebHID API](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/defaultwebhidguardsetting) |
| Microsoft Edge\Additional | Disable synchronization<br>of data using<br>Microsoft sync services | Enabled | [Disable synchronization<br>of data using<br>Microsoft sync services](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/syncdisabled) |
| Microsoft Edge\Additional | Enable Application<br>Bound Encryption | Enabled | [Enable Application<br>Bound Encryption](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/applicationboundencryptionenabled) |
| Microsoft Edge\Additional | Limit cookies from<br>specific websites to<br>the current session | Enabled | [Limit cookies from<br>specific websites to<br>the current session](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/cookiessessiononlyforurls) |
| Microsoft Edge\Additional | Set the system<br>default printer as<br>the default printer | Enabled | [Set the system<br>default printer as<br>the default printer](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/printpreviewusesystemdefaultprinter) |
| Microsoft Edge\Additional | Switch intranet sites<br>to a work profile | Enabled | [Switch intranet sites<br>to a work profile](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/switchintranetsitestoworkprofile) |
| Microsoft Edge\Content settings | Allow insecure content<br>on specified sites | [*.contoso.com] | [Allow insecure content<br>on specified sites](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/insecurecontentallowedforurls) |
| Microsoft Edge\Content settings | Block insecure content<br>on specified sites | ["*"] | [Block insecure content<br>on specified sites](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/insecurecontentblockedforurls) |
| Microsoft Edge\Content settings | Control use of the<br>Web Bluetooth API | Enabled, Do not allow any site to request access to Bluetooth devices via the Web Bluetooth API | [Control use of the<br>Web Bluetooth API](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/defaultwebbluetoothguardsetting) |
| Microsoft Edge\Content settings | Control where security<br>restrictions on insecure<br>origins apply | *.company.com | [Control where security<br>restrictions on insecure<br>origins apply](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/overridesecurityrestrictionsoninsecureorigin) |
| Microsoft Edge\Content settings | Grant access to specific<br>sites to connect to<br>specific USB devices | Enabled [*.contoso.com] | [Grant access to specific<br>sites to connect to<br>specific USB devices](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/webusballowdevicesforurls) |
| Microsoft Edge\Extensions | Control which extensions<br>cannot be installed | ["*"] | [Control which extensions<br>cannot be installed](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/extensioninstallblocklist) |
| Microsoft Edge\Microsoft Edge | Allow download<br>restrictions | Block dangerous downloads (1) | [Allow download<br>restrictions](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/downloadrestrictions) |
| Microsoft Edge\Microsoft Edge | Allow media autoplay<br>for websites | Disabled | [Allow media autoplay<br>for websites](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/autoplayallowed) |
| Microsoft Edge\Microsoft Edge | Allow remote<br>debugging | Disabled | [Allow remote<br>debugging](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/remotedebuggingallowed) |
| Microsoft Edge\Microsoft Edge | Allow specific extensions<br>to be installed | [] | [Allow specific extensions<br>to be installed](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/extensioninstallallowlist) |
| Microsoft Edge\Microsoft Edge | Allow user-level native<br>messaging hosts (installed<br>without admin permissions) | Enabled | [Allow user-level native<br>messaging hosts (installed<br>without admin permissions)](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/nativemessaginguserlevelhosts) |
| Microsoft Edge\Microsoft Edge | Block insecure content<br>on specified sites | ["*"] | [Block insecure content<br>on specified sites](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/insecurecontentblockedforurls) |
| Microsoft Edge\Microsoft Edge | Blocks external extensions<br>from being installed | Enabled | [Blocks external extensions<br>from being installed](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/blockexternalextensions) |
| Microsoft Edge\Microsoft Edge | Clear browsing data<br>when Microsoft Edge closes | Enabled | [Clear browsing data<br>when Microsoft Edge closes](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/clearbrowsingdataonexit) |
| Microsoft Edge\Microsoft Edge | Configure allowed<br>extension types | [] | [Configure allowed<br>extension types](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/extensionallowedtypes) |
| Microsoft Edge\Microsoft Edge | Configure auto discard<br>sleeping tabs | Enabled | [Configure auto discard<br>sleeping tabs](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/autodiscardsleepingtabsenabled) |
| Microsoft Edge\Microsoft Edge | Configure extension and<br>user script install sources | [] | [Configure extension and<br>user script install sources](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/extensioninstallsources) |
| Microsoft Edge\Microsoft Edge | Configure native<br>messaging block list | Enabled, ["*"] | [Configure native<br>messaging block list](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/nativemessagingblocklist) |
| Microsoft Edge\Microsoft Edge | Configure plugins<br>policy | Click to play (3) | [Configure plugins<br>policy](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/defaultpluginssetting) |
| Microsoft Edge\Microsoft Edge | Configure sleeping<br>tabs | Enabled | [Configure sleeping<br>tabs](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/sleepingtabsenabled) |
| Microsoft Edge\Microsoft Edge | Configure when efficiency<br>mode should become active | Enabled,  become active (Device) | [Configure when efficiency<br>mode should become active](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/efficiencymode) |
| Microsoft Edge\Microsoft Edge | Control Manifest v2<br>extension availability | Disabled | [Control Manifest v2<br>extension availability](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/extensionmanifestv2availability) |
| Microsoft Edge\Microsoft Edge | Control where<br>developer tools<br>can be used | Enabled | [Control where<br>developer tools<br>can be used](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/developertoolsavailability) |
| Microsoft Edge\Microsoft Edge | Control which extensions<br>are installed silently | [] | [Control which extensions<br>are installed silently](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/extensioninstallforcelist) |
| Microsoft Edge\Microsoft Edge | Control which extensions<br>cannot be installed | ["*"] | [Control which extensions<br>cannot be installed](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/extensioninstallblocklist) |
| Microsoft Edge\Microsoft Edge | Default JavaScript<br>setting | Enabled, Allow sites to run JavaScript (1) | [Default JavaScript<br>setting](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/defaultjavascriptsetting) |
| Microsoft Edge\Microsoft Edge | Default images<br>setting | Enabled, Allow sites to show images (1) | [Default images<br>setting](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/defaultimagessetting) |
| Microsoft Edge\Microsoft Edge | Delay before running<br>idle actions | 30 | [Delay before running<br>idle actions](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/idletimeout) |
| Microsoft Edge\Microsoft Edge | Enable insecure<br>download warnings | Enabled | [Enable insecure<br>download warnings](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/showdownloadsinsecurewarningsenabled) |
| Microsoft Edge\Microsoft Edge | Enable startup<br>boost | Disabled | [Enable startup<br>boost](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/startupboostenabled) |
| Microsoft Edge\Microsoft Edge | Let screen reader users<br>get image descriptions<br>from Microsoft | Enabled | [Let screen reader users<br>get image descriptions<br>from Microsoft](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/accessibilityimagelabelsenabled) |
| Microsoft Edge\Microsoft Edge | Notify a user that a<br>browser restart is recommended<br>or required for pending updates | Recommended - Show a recurring prompt to the user indicating that a restart is recommended | [Notify a user that a<br>browser restart is recommended<br>or required for pending updates](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/relaunchnotification) |
| Microsoft Edge\Microsoft Edge | Set download<br>directory | ${user_home}/Downloads/EdgeControlled | [Set download<br>directory](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/downloaddirectory) |
| Microsoft Edge\Microsoft Edge | Set the background tab<br>inactivity timeout for<br>sleeping tabs | 6Hours (21600) = 6 hours of inactivity | [Set the background tab<br>inactivity timeout for<br>sleeping tabs](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/sleepingtabstimeout) |
| Microsoft Edge\Microsoft Edge | Show Downloads button<br>on the toolbar | Enabled | [Show Downloads button<br>on the toolbar](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/showdownloadstoolbarbutton) |
| Microsoft Edge\Network settings | Control whether TLS 1.3<br>Early Data is enabled<br>in Microsoft Edge | Enabled | [Control whether TLS 1.3<br>Early Data is enabled<br>in Microsoft Edge](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/tls13earlydataenabled) |
| Microsoft Edge\Network settings | Enable the network<br>service sandbox | Enabled | [Enable the network<br>service sandbox](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/networkservicesandboxenabled) |
| Microsoft Edge\Network settings | Manage exposure of<br>local IP addressess<br>by WebRTC | Enabled [*.contoso.com] | [Manage exposure of<br>local IP addressess<br>by WebRTC](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/webrtclocalipsallowedurls) |
| Microsoft Edge\Network settings | WebRTC IP Handling<br>Policy for URL Patterns | default_public_and_private_interfaces | [WebRTC IP Handling<br>Policy for URL Patterns](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/webrtciphandlingurl) |
| Microsoft Edge\Proxy settings | Configure proxy<br>settings | {"mode": "system"} | [Configure proxy<br>settings](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/proxysettings) |
| Microsoft Edge\SmartScreen settings | Configure Microsoft<br>Defender SmartScreen to<br>block potentially unwanted apps | Enabled | [Configure Microsoft<br>Defender SmartScreen to<br>block potentially unwanted apps](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/smartscreenpuadetectionenabled) |
| Microsoft Edge\Startup, home page and new tab page | Configure InPrivate<br>mode availability | InPrivate mode available (0) | [Configure InPrivate<br>mode availability](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/inprivatemodeavailability) |

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
|-----------|----------|-------|----------------|
| Microsoft Edge\Additional | Allow clipboard use<br>on specific sites | Enabled, *.company.com | [Allow clipboard use<br>on specific sites](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/clipboardallowedforurls) |
| Microsoft Edge\Additional | Allow download<br>restrictions | Block all downloads (3) | [Allow download<br>restrictions](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/downloadrestrictions) |
| Microsoft Edge\Additional | Application Guard<br>Traffic Identification | Enabled | [Application Guard<br>Traffic Identification](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/applicationguardtrafficidentificationenabled) |
| Microsoft Edge\Additional | Block clipboard use<br>on specific sites | Enabled, * | [Block clipboard use<br>on specific sites](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/clipboardblockedforurlss) |
| Microsoft Edge\Additional | Clear browsing data<br>when Microsoft Edge closes | Enabled | [Clear browsing data<br>when Microsoft Edge closes](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/clearbrowsingdataonexit) |
| Microsoft Edge\Additional | Control printing | Disabled | [Control printing](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/printingenabled) |
| Microsoft Edge\Additional | Control where<br>developer tools<br>can be used | Disallowed (2) | [Control where<br>developer tools<br>can be used](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/developertoolsavailability) |
| Microsoft Edge\Additional | Enable site isolation<br>for every site | Enabled | [Enable site isolation<br>for every site](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/siteperprocess) |
| Microsoft Edge\Additional | Force Microsoft Defender<br>SmartScreen checks on<br>downloads from trusted sources | Enabled | [Force Microsoft Defender<br>SmartScreen checks on<br>downloads from trusted sources](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/smartscreenpromptoverrideenabled) |
| Microsoft Edge\Additional | Prevents files from<br>being uploaded while in<br>Application Guard | Enabled | [Prevents files from<br>being uploaded while in<br>Application Guard](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/applicationguarduploadblockingenabled) |
| Microsoft Edge\Additional | Send required and<br>optional diagnostic data<br>about browser usage | Off (0) | [Send required and<br>optional diagnostic data<br>about browser usage](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/diagnosticdata) |
| Microsoft Edge\Browsing Data Lifetime | Browsing Data<br>Lifetime Settings | [{"data_types": ["browsing_history", "download_history", "cookies_and_other_site_data", "cached_images_and_files"], "time_to_live_in_hours": 24}] | [Browsing Data<br>Lifetime Settings](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/browsingdatalifetime) |
| Microsoft Edge\Content settings | Block access to<br>a list of URLs | ["*"] | [Block access to<br>a list of URLs](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/urlblocklist) |
| Microsoft Edge\Content settings | Define a list of<br>allowed URLs | ["*.company.com","*.microsoft.com","*.office.com"] | [Define a list of<br>allowed URLs](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/urlallowlist) |
| Microsoft Edge\Content settings | Minimum TLS<br>version enabled | TLS 1.2 | [Minimum TLS<br>version enabled](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/sslversionmin) |
| Microsoft Edge\Force Ephemeral Profiles | Enable use of<br>ephemeral profiles | Enabled | [Enable use of<br>ephemeral profiles](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/forceephemeralprofiles) |
| Microsoft Edge\Microsoft Edge | Allow user<br>feedback | Disabled | [Allow user<br>feedback](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/userfeedbackallowed) |
| Microsoft Edge\Microsoft Edge | Enable site isolation<br>for specific origins | Disabled | [Enable site isolation<br>for specific origins](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/isolateorigins) |
| Microsoft Edge\Microsoft Edge | URL reporting in Edge<br>diagnostic data enabled | Disabled | [URL reporting in Edge<br>diagnostic data enabled](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/urldiagnosticdataenabled) |
| Microsoft Edge\Network isolation | Allow QUIC<br>protocol | Disabled (enhanced security) | [Allow QUIC<br>protocol](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/quicallowed) |
| Microsoft Edge\Network isolation | Maximum number of<br>concurrent connections<br>to the proxy server | Enabled, 6 (limit connections) | [Maximum number of<br>concurrent connections<br>to the proxy server](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/maxconnectionsperproxy) |
| Microsoft Edge\Network settings | Enable network<br>prediction | Never predict (2) | [Enable network<br>prediction](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/networkpredictionoptions) |
| Microsoft Edge\Network settings | Restrict the range of<br>local UDP ports<br>used by WebRTC | "10000-10100" (restricted range) | [Restrict the range of<br>local UDP ports<br>used by WebRTC](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/webrtcudpportrange) |
| Microsoft Edge\Proxy settings | Configure proxy<br>bypass list | [] (no bypassing) | [Configure proxy<br>bypass list](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/proxybypasslist) |
| Microsoft Edge\Proxy settings | Configure proxy<br>pac URL | "https://proxy.company.com/proxy.pac" | [Configure proxy<br>pac URL](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/proxypacurl) |
| Microsoft Edge\Startup, home page and new tab page | Configure InPrivate<br>mode availability | InPrivate mode forced (1) | [Configure InPrivate<br>mode availability](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/inprivatemodeavailability) |
| Microsoft Edge\User Data Snapshot Retention | Limits the number of<br>user data snapshots retained<br>for use in case of<br>emergency rollbac | 1 | [Limits the number of<br>user data snapshots retained<br>for use in case of<br>emergency rollbac](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/userdatasnapshotretentionlimit) |

12. Select **Next**.  
13. For **Assignments**, assign to **SEB-Level2-Devices** group.  
14. Select **Next** to review the settings. Then choose **Save**.   

### Validation

After deploying all Windows security levels, validate that the policies have applied correctly and that each configuration behaves as expected on a test device.

- **Policy verification:**  
  In the Intune admin center, go to **Devices** > **Windows** > **Manage devices** > **Configuration**, and locate the policies for each level.  
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
For additional confirmation, monitor **edge://policy** and the **Device configuration report** in the Intune admin center to ensure the expected number of policies are active per level.

::: zone-end

::: zone pivot="macos"

## Settings Catalog for macOS

Settings Catalog for macOS provides foundational browser security for enrolled Mac devices.

> **Microsoft Documentation:**
> - [Settings Catalog for macOS](../configuration/settings-catalog.md)
> - [Microsoft Edge Browser Policies](/deployedge/microsoft-edge-policies)

> [!IMPORTANT]
> **macOS Platform Limitations:**
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
   - **Name:** Level 1 – Enterprise basic security – macOS Settings Catalog  
   - **Description:** Foundational browser configuration for Microsoft Edge on macOS with core security and privacy controls.  
6. Select **Next**.  
7. On the **Configuration settings** tab, select **+ Add settings**.  
8. In the **Settings picker**, locate each setting using one of the following options:  
   - **Search for a setting:** Use the **search box** to find the setting name listed in the table. When multiple results appear, choose the entry that matches the **Category**.  
   - **Browse by category:** Expand **Microsoft Edge** and select the **Category** listed for that setting.  
9. Configure each setting using the **Value** specified in the table.  

| Category | Setting | Value | Documentation |
|--------------------|---------|-------|----------------|
| Microsoft Edge | Configure Microsoft Defender SmartScreen | Enabled | [Configure Microsoft Defender SmartScreen](/deployedge/microsoft-edge-browser-policies/smartscreenenabled) |
| Microsoft Edge | Configure Microsoft Defender SmartScreen to block potentially unwanted apps | Enabled | [Configure Microsoft Defender SmartScreen to block potentially unwanted apps](/deployedge/microsoft-edge-browser-policies/smartscreenpuadetectionenabled) |
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
| Microsoft Edge Update | Specifies how Microsoft Edge Update handles available updates from Microsoft Edge | automatic-silent-only (automatic-silent-only) = Updates are applied only when they're found by the periodic update check | [UpdatePolicyOverride](/deployedge/microsoft-edge-update-policies#updatedefault) |
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
|--------------------|---------|-------|----------------|
| Microsoft Edge | Enhance the security state in Microsoft Edge | Strict | [Enhance the security state in Microsoft Edge](/deployedge/microsoft-edge-browser-policies/enhancesecuritymode) |
| Microsoft Edge | Configure InPrivate mode availability | Disabled (1) = InPrivate mode disabled | [Configure InPrivate mode availability](/deployedge/microsoft-edge-browser-policies/inprivatemodeavailability) |
| Microsoft Edge | Control which extensions cannot be installed | ["*"] | [Control which extensions cannot be installed](/deployedge/microsoft-edge-browser-policies/extensioninstallblocklist) |
| Microsoft Edge | Control use of the WebUSB API | BlockWebUsb (2) = Do not allow any site to request access to USB devices via the WebUSB API | [Control use of the WebUSB API](/deployedge/microsoft-edge-browser-policies/defaultwebusbguardsetting) |
| Microsoft Edge | Control use of the WebHID API | BlockWebHid (2) = Do not allow any site to request access to HID devices via the WebHID API | [Control use of the WebHID API](/deployedge/microsoft-edge-browser-policies/defaultwebhidguardsetting) |
| Microsoft Edge | Control where developer tools can be used | DeveloperToolsDisallowed (2) = Don't allow using the developer tools | [Control where developer tools can be used](/deployedge/microsoft-edge-browser-policies/developertoolsavailability) |
| Microsoft Edge | Control the availability of developer mode on extensions page | Disallow (1) = Do not allow the usage of developer mode on extensions page | [Control the availability of developer mode on extensions page](/deployedge/microsoft-edge-browser-policies/extensiondevelopermodesettings) |
| Microsoft Edge | Enable Microsoft Defender SmartScreen DNS requests | Enabled | [Enable Microsoft Defender SmartScreen DNS requests](/deployedge/microsoft-edge-browser-policies/smartscreendnsrequestsenabled) |
| Microsoft Edge | Shopping in Microsoft Edge Enabled | Disabled | [Shopping in Microsoft Edge Enabled](/deployedge/microsoft-edge-browser-policies/edgeshoppingassistantenabled) |
| Microsoft Edge | Edge Wallet E-Tree Enabled | Disabled | [Edge Wallet E-Tree Enabled](/deployedge/microsoft-edge-browser-policies/edgewalletetreeenabled) |
| Microsoft Edge | Enable Microsoft Bing trending suggestions in the address bar | Disabled | [Enable Microsoft Bing trending suggestions in the address bar](/deployedge/microsoft-edge-browser-policies/addressbartrendingsuggestenabled) |

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
|--------------------|---------|-------|----------------|
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
| Microsoft Edge | Manage exposure of local IP addressess by WebRTC | [] | [Manage exposure of local IP addressess by WebRTC](/deployedge/microsoft-edge-browser-policies/webrtclocalipsallowedurls) |
| Microsoft Edge | Control which extensions are installed silently | [] | [Control which extensions are installed silently](/deployedge/microsoft-edge-browser-policies/extensioninstallforcelist) |
| Microsoft Edge | Configure allowed extension types | extension (extension) = Extension | [Configure allowed extension types](/deployedge/microsoft-edge-browser-policies/extensionallowedtypes) |
| Microsoft Edge | Configure tracking prevention exceptions for specific sites | *.company.com | [Configure tracking prevention exceptions for specific sites](/deployedge/microsoft-edge-browser-policies/allowtrackingforurls) |
| Microsoft Edge | Allow media autoplay for websites | Disabled | [Allow media autoplay for websites](/deployedge/microsoft-edge-browser-policies/autoplayallowed) |
| Microsoft Edge | Allow or block video capture | Disabled | [Allow or block video capture](/deployedge/microsoft-edge-browser-policies/videocaptureallowed) |
| Microsoft Edge | Allow or block audio capture | Disabled | [Allow or block audio capture](/deployedge/microsoft-edge-browser-policies/audiocaptureallowed) |
| Microsoft Edge | Default notification setting | BlockNotifications (2) = Don't allow any site to show desktop notifications | [Default notification setting](/deployedge/microsoft-edge-browser-policies/defaultnotificationssetting) |
| Microsoft Edge | Default geolocation setting | BlockGeolocation (2) = Don't allow any site to track users' physical location | [Default geolocation setting](/deployedge/microsoft-edge-browser-policies/defaultgeolocationsetting) |
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

