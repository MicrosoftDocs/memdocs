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
> - [Settings Catalog Overview](../configuration/settings-catalog.md)
> - [Microsoft Edge Browser Policies](/deployedge/microsoft-edge-policies)
> - [Microsoft Edge Update Policies](/deployedge/microsoft-edge-update-policies)

**Prerequisites:**

- Windows 11 Pro or Enterprise  
- Intune enrollment  
- Entra ID join or Hybrid  
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
|-----------|----------|-------|----------------|
| Microsoft Edge\SmartScreen settings | Configure Microsoft Defender<br>SmartScreen to protect users<br>from malicious sites | Enabled | [Configure Microsoft Defender<br>SmartScreen to protect users<br>from malicious sites](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/smartscreenenabled) |
| Microsoft Edge\SmartScreen settings | Configure Microsoft Defender<br>SmartScreen to block<br>potentially unwanted apps | Enabled | [Configure Microsoft Defender<br>SmartScreen to block<br>potentially unwanted apps](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/smartscreenpuadetectionenabled) |
| Microsoft Edge\Automatic HTTPS | Enable automatic<br>HTTPS upgrades | Enabled | [Enable automatic<br>HTTPS upgrades](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/httpsonlymode) |
| Microsoft Edge\Content settings | Block tracking of users’<br>web-browsing activity | Strict (3) | [Block tracking of users’<br>web-browsing activity](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/trackingprevention) |
| Microsoft Edge\Network settings | Enable network prediction | Don’t predict (2) | [Enable network prediction](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/networkpredictionoptions) |
| Microsoft Edge\Search experience | Enable search suggestions<br>for the address bar | Disabled | [Enable search suggestions<br>for the address bar](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/searchsuggestenabled) |
| Microsoft Edge\Diagnostics | Send required and optional<br>diagnostic data about browser usage | Off (0) | [Send required and optional<br>diagnostic data about browser usage](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/diagnosticdata) |
| Microsoft Edge\Privacy Sandbox | Configure Do Not Track setting<br>to signal user preference | Enabled | [Configure Do Not Track setting<br>to signal user preference](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/configuredonottrack) |
| Microsoft Edge\Content settings | Default pop-up window setting (Device) | Don’t allow any site to show pop-ups (2) | [Default pop-up window setting (Device)](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/defaultpopupssetting) |
| Microsoft Edge\Content settings | Default geolocation setting (Device) | Don’t allow any site to track location (2) | [Default geolocation setting (Device)](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/defaultgeolocationbehavior) |
| Microsoft Edge\Content settings | Default sensors setting (Device) | Don’t allow sites to access sensors (2) | [Default sensors setting (Device)](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/defaultsensorssetting) |
| Microsoft Edge\Content settings | Default notification setting (Device) | Don’t allow any site to show notifications (2) | [Default notification setting (Device)](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/defaultnotificationssetting) |
| Microsoft Edge\Content settings | Default media stream setting (Device) | Don’t allow access to camera / mic (2) | [Default media stream setting (Device)](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/mediastreamsettings) |
| Microsoft Edge\Content settings | Block third-party cookies to improve privacy | Enabled | [Block third-party cookies to improve privacy](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/thirdpartycookiesblocked) |
| Microsoft Edge\Password Manager and Protection | Enable saving passwords to the password manager | Disabled | [Enable saving passwords to the password manager](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/passwordmanagerenabled) |
| Microsoft Edge\Password Manager and Protection | Enable AutoFill for addresses and contact information | Disabled | [Enable AutoFill for addresses and contact information](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/autofilladdressenabled) |
| Microsoft Edge\Password Manager and Protection | Enable AutoFill for payment instruments and cards | Disabled | [Enable AutoFill for payment instruments and cards](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/autofillcreditcardenabled) |
| Microsoft Edge\Password Manager and Protection | Biometric authentication for local data storage reauth | Disabled | [Biometric authentication for local data storage reauth](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/biometricauthenticationbeforefilling) |
| Microsoft Edge\Import Controls | Allow importing of autofill form data | Disabled | [Allow importing of autofill form data](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/importautofillformdata) |
| Microsoft Edge\Import Controls | Allow importing of saved passwords | Disabled | [Allow importing of saved passwords](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/importsavedpasswords) |
| Microsoft Edge\Import Controls | Allow importing of browsing history | Disabled | [Allow importing of browsing history](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/importhistory) |
| Microsoft Edge\Import Controls | Allow importing of payment information | Disabled | [Allow importing of payment information](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/importpaymentinfo) |
| Microsoft Edge\Startup, home page and new tab page | Configure the home page URL | https://portal.office.com | [Configure the home page URL](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/homepagelocation) |
| Microsoft Edge\Startup, home page and new tab page | Show Home button on toolbar for user convenience | Enabled | [Show Home button on toolbar for user convenience](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/showhomebutton) |
| Microsoft Edge\Startup, home page and new tab page | Hide the First-run experience and splash screen for users | Enabled | [Hide the First-run experience and splash screen for users](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/hidefirstrunexperience) |
| Microsoft Edge\Additional | Suppress unsupported OS warning to avoid disruption | Enabled | [Suppress unsupported OS warning to avoid disruption](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/unsupportedoswarningenabled) |
| Microsoft Edge\Browser Sign-in | Enable browser sign-in and force users to sign in | Force (2) | [Enable browser sign-in and force users to sign in](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/browsersigninenabled) |
| Microsoft Edge\Shopping and Commerce | Shopping in Microsoft Edge feature | Disabled | [Shopping in Microsoft Edge feature](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/edgeshoppingassistantenabled) |
| Microsoft Edge\Wallet and Payments | Allow users to be prompted for Microsoft Wallet password | Disabled | [Allow users to be prompted for Microsoft Wallet password](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/walletserviceenabled) |
| Microsoft Edge\Feature Recommendations | Show feature and merchandise recommendations in Edge | Disabled | [Show feature and merchandise recommendations in Edge](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/showfeatureandmerchandiserecommendationsenabled) |
| Microsoft Edge\Feature Recommendations | Allow feature suggestions in sidebar | Disabled | [Allow feature suggestions in sidebar](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/sidebarfeaturesuggestionsenabled) |
| Microsoft Edge\Sidebar Management | Enable Microsoft Search integration in sidebar | Disabled | [Enable Microsoft Search integration in sidebar](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/sidebarmicrosoftsearchenabled) |
| Microsoft Edge\Sidebar Management | Allow side panel sites list customization | Disabled | [Allow side panel sites list customization](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/sidebarcustomizationsettings) |
| Microsoft Edge\AI Integration | Configure Copilot integration | Enabled, but available to users | [Configure Copilot integration](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/microsoft365copilotchaticonenabled) |
| Microsoft Edge\AI Integration | Control the mode of the Copilot AI features | AI-powered features available | [Control the mode of the Copilot AI features](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/microsoftcopilotsettings) |
| Microsoft Edge\Network Security | Control the mode of DNS-over-HTTPS | Enabled, fallback to insecure DNS allowed | [Control the mode of DNS-over-HTTPS](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/dnsoverhttpsmode) |
| Microsoft Edge\Network Security | DNS interception checks for validation | Enabled | [DNS interception checks for validation](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/dnsinterceptionchecksenabled) |
| Microsoft Edge\Network Security | Allow QUIC protocol for connectivity | Disabled | [Allow QUIC protocol for connectivity](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/quicallowed) |
| Microsoft Edge\Search Provider | Enable the default search provider | Enabled | [Enable the default search provider](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/defaultsearchproviderenabled) |
| Microsoft Edge\Search Provider | Default search provider name | Microsoft Bing | [Default search provider name](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/defaultsearchprovidername) |
| Microsoft Edge\Search Provider | Default search provider search URL | https://www.bing.com/search?q={searchTerms} | [Default search provider search URL](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/defaultsearchprovidersearchurl) |
| Microsoft Edge\Search Provider | Default search provider keyword | bing | [Default search provider keyword](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/defaultsearchproviderkeyword) |
| Microsoft Edge\Privacy Sandbox | Privacy Sandbox Ad measurement feature | Disabled | [Privacy Sandbox Ad measurement feature](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/privacysandboxadmeasurementenabled) |
| Microsoft Edge\Privacy Sandbox | Privacy Sandbox Topics feature | Disabled | [Privacy Sandbox Topics feature](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/privacysandboxtopicsenabled) |
| Microsoft Edge\Privacy Sandbox | Privacy Sandbox Fledge feature | Disabled | [Privacy Sandbox Fledge feature](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/privacysandboxfledgeenabled) |
| Microsoft Edge\Translation | Personalize detected languages for website translation | Disabled | [Personalize detected languages for website translation](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-browser-policies/translateenabled) |
| Microsoft Edge Update\Experimentation and Configuration Service | Experimentation and Configuration Service Control | Retrieve configurations (1) | [Experimentation and Configuration Service Control](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-update-policies#updaterexperimentationandconfigurationservicecontrol) |
| Microsoft Edge Update\Experimentation and Configuration Service | Control updater’s communication with the Experimentation and Configuration Service | Disabled (0) | [Control updater’s communication with the Experimentation and Configuration Service](https://learn.microsoft.com/en-us/deployedge/microsoft-edge-update-policies#updaterexperimentationandconfigurationservicecontrol) |

10. Select **Next**.  
11. For **Scope tags**, select the appropriate scope tag.  
12. For **Assignments**, assign to **SEB-Level1-Devices** group.  
13. Select **Next** to review the settings. Then choose **Create**.  

**Validation:**

- Console: Devices > Windows > Configuration > select policy > Monitor > Device status  
- Endpoint: Open edge://policy and verify settings are applied  
- Test basic controls: SmartScreen, tracking prevention, disabled autofill  

### Level 2 - Enterprise enhanced security for Windows

Level 2 adds enhanced security controls including Application Bound Encryption, extension blocking, and advanced privacy controls.

1. Go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Devices** > **Windows** > **Manage devices** > **Configuration** > **Create** > **New policy**.  
3. For **Platform**, choose **Windows 10 and later**. For **Profile type**, choose **Settings catalog**.  
4. Select **Create**.  
5. On the **Basics** tab, enter:  
   - **Name:** Level 2 – Enterprise enhanced security – Windows Settings Catalog  
   - **Description:** Enhanced browser security including Application Bound Encryption and extension controls.  
6. Select **Next**.  
7. On **Configuration settings**, select **+ Add settings**.  
8. In the **Settings picker**, locate each setting using one of the following options:  
   - **Search for a setting:** Copy the **Setting** from the table and paste it into search. When multiple results appear, choose the entry that matches the **Category**.
   - **Browse by category:** Select the **Category** listed for that setting.  
9. Configure the setting using the **Value** specified.

| Category | Setting | Value |
|--------------------|---------|-------|
|  | Configure Microsoft Defender SmartScreen to protect users from malicious sites | Enabled |
|  | Configure Microsoft Defender SmartScreen to block potentially unwanted apps | Enabled |
|  | Configure Automatic HTTPS to ensure secure connections | Enabled |
|  | Block tracking of users' web-browsing activity | Strict (3) |
|  | Enable network prediction to improve performance | Don't predict (2) |
|  | Enable search suggestions for the address bar | Disabled |
|  | Send required and optional diagnostic data about browser usage | Off (0) |
|  | Configure Do Not Track setting to signal user preference | Enabled |
|  | Default pop-up window setting (Device) | Don't allow any site to show popups (2) |
|  | Default geolocation setting (Device) | Don't allow any site to track location (2) |
|  | Default sensors setting (Device) | Don't allow sites to access sensors (2) |
|  | Default notification setting (Device) | Don't allow any site to show notifications (2) |
|  | Default media stream setting (Device) | Don't allow access to camera/mic (2) |
|  | Block third party cookies to improve privacy | Enabled |
|  | Enable saving passwords to the password manager | Disabled |
|  | Enable AutoFill for addresses and contact information | Disabled |
|  | Enable AutoFill for payment instruments and cards | Disabled |
|  | Biometric authentication for local data storage reauth | Disabled |
|  | Allow importing of autofill form data | Disabled |
|  | Allow importing of saved passwords | Disabled |
|  | Allow importing of browsing history | Disabled |
|  | Allow importing of payment information | Disabled |
|  | Configure the home page URL | https://portal.office.com |
|  | Show Home button on toolbar for user convenience | Enabled |
|  | Hide the First-run experience and splash screen for users | Enabled |
|  | Suppress unsupported OS warning to avoid disruption | Enabled |
|  | Enable browser sign-in and force users to sign in | Force (2) |
|  | Shopping in Microsoft Edge feature | Disabled |
|  | Allow users to be prompted for Microsoft Wallet password | Disabled |
|  | Show feature and merchandise recommendations in Edge | Disabled |
|  | Allow feature suggestions in sidebar | Disabled |
|  | Enable Microsoft Search integration in sidebar | Disabled |
|  | Allow side panel sites list customization | Disabled |
|  | Configure Copilot integration | Enabled, but available to users |
|  | Control the mode of the Copilot AI features | AI-powered features available |
|  | Control the mode of DNS-over-HTTPS | Enabled, fallback to insecure DNS allowed |
|  | DNS interception checks for validation | Enabled |
|  | Allow QUIC protocol for connectivity | Disabled |
|  | Enable the default search provider | Enabled |
|  | Default search provider name | Microsoft Bing |
|  | Default search provider search URL | https://www.bing.com/search?q={searchTerms} |
|  | Default search provider keyword | bing |
|  | Privacy Sandbox Ad measurement feature | Disabled |
|  | Privacy Sandbox Topics feature | Disabled |
|  | Privacy Sandbox Fledge feature | Disabled |
|  | Personalize detected languages for website translation | Disabled |
|  | Experimentation and Configuration Service Control | Retrieve configurations (1) |
|  | Control updater's communication with the Experimentation and Configuration Service | Disabled (0) |
|  | Prevent bypassing Microsoft Defender SmartScreen prompts for sites | Enabled |
|  | Prevent bypassing of Microsoft Defender SmartScreen warnings about downloads | Enabled |
|  | Enable Application Bound Encryption to protect sensitive data | Enabled |
|  | Enhance the security state in Microsoft Edge | Strict |
|  | Control which extensions cannot be installed | ["*"] |
|  | Control where developer tools can be used | Disallowed (2) |
|  | Block external extensions from being installed | Enabled |
|  | Control use of the WebUSB API | Do not allow any site to request access to USB devices (2) |
|  | Control use of the WebHID API | Do not allow any site to request access to HID devices (2) |
|  | Control use of the Web Bluetooth API | Do not allow any site to request access to Bluetooth devices (2) |
|  | Control use of the Serial API | Do not allow any site to request access to serial ports (2) |
|  | Continue running background apps after Microsoft Edge closes | Disabled |
|  | Clear browsing data when Microsoft Edge closes | Enabled |
|  | Configure InPrivate mode availability | Disabled (1) |
|  | Enable Guest mode in browser | Disabled |
|  | Block insecure content on specified sites | ["*"] |
|  | Enable site isolation for every site | Enabled |
|  | Allow user feedback | Disabled |
|  | Enable the Click-to-Call feature in Microsoft Edge | Disabled |
|  | Set download directory | 1 (prompt for location) |
|  | Allow download restrictions | Block dangerous downloads (1) |
|  | Allow users to access the games menu in Microsoft Edge | Disabled |
|  | Enable split screen in Microsoft Edge | Disabled |
|  | Show Collections menu entry | Disabled |
|  | Show microsoft.com homepage as desktop Start page instead of New Tab page | Disabled |
|  | Configure Copilot page context | Copilot can't use page content for prompts (1) |
|  | Show Compose (writing assistance) on websites | Disabled |
|  | Show a prompt to organize tabs | Disabled |
|  | Minimum SSL version enabled | TLS 1.2 |
|  | Require online OCSP/CRL checks for local trust anchors | Enabled |
|  | Allow certificates from root stores | Disabled |
|  | Enable Microsoft Bing trending suggestions in the address bar | Disabled |
|  | Enable related matches in Find on Page | Disabled |
|  | Configure when efficiency mode should become active | Enabled, Efficiency mode is always active |
|  | Configure sleeping tabs | Enabled |
|  | Action to take on startup | Open specific pages (4) |
|  | URLs to open on startup | ["https://portal.office.com"] |
|  | Update policy override default | Automatic silent updates only (3) |

10. Select **Next**.  
11. For **Scope tags**, select the appropriate scope tag.  
12. For **Assignments**, assign to **SEB-Level2-Devices** group.  
13. Select **Next** to review the settings. Then choose **Create**.  

**Validation:**

- Verify ABE is active: edge://policy  
- Test extension blocking: attempt to install extension (should be blocked)  
- Verify developer tools blocked: F12 should not open developer tools  
- Test API restrictions: WebUSB, WebHID, Serial API should all be blocked  

### Level 3 - Enterprise high security for Windows

Level 3 provides maximum security with URL allowlisting, Application Guard isolation, and comprehensive zero-trust controls.

1. Go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Devices** > **Windows** > **Manage devices** > **Configuration** > **Create** > **New policy**.  
3. For **Platform**, choose **Windows 10 and later**. For **Profile type**, choose **Settings catalog**.  
4. Select **Create**.  
5. On the **Basics** tab, enter:  
   - **Name:** Level 3 – Enterprise high security – Windows Settings Catalog  
   - **Description:** High security including URL allowlisting, Application Guard, and zero-trust controls.  
6. Select **Next**.  
7. On **Configuration settings**, select **+ Add settings**.  
8. In the **Settings picker**, locate each setting using one of the following options:  
   - **Search for a setting:** Copy the **Setting** from the table and paste it into search.  
   - **Browse by category:** Select the **Category** listed for that setting.  
   When multiple results appear, choose the entry that matches the **Category**.  
9. Configure the setting using the **Value** specified.

| Category | Setting | Value |
|--------------------|---------|-------|
|  | Configure Microsoft Defender SmartScreen to protect users from malicious sites | Enabled |
|  | Configure Microsoft Defender SmartScreen to block potentially unwanted apps | Enabled |
|  | Configure Automatic HTTPS to ensure secure connections | Enabled |
|  | Block tracking of users' web-browsing activity | Strict (3) |
|  | Enable network prediction to improve performance | Don't predict (2) |
|  | Enable search suggestions for the address bar | Disabled |
|  | Send required and optional diagnostic data about browser usage | Off (0) |
|  | Configure Do Not Track setting to signal user preference | Enabled |
|  | Default pop-up window setting (Device) | Don't allow any site to show popups (2) |
|  | Block third party cookies to improve privacy | Enabled |
|  | Enable saving passwords to the password manager | Disabled |
|  | Enable AutoFill for addresses and contact information | Disabled |
|  | Enable AutoFill for payment instruments and cards | Disabled |
|  | Biometric authentication for local data storage reauth | Disabled |
|  | Allow importing of autofill form data | Disabled |
|  | Allow importing of saved passwords | Disabled |
|  | Allow importing of browsing history | Disabled |
|  | Allow importing of payment information | Disabled |
|  | Configure the home page URL | https://portal.office.com |
|  | Show Home button on toolbar for user convenience | Enabled |
|  | Hide the First-run experience and splash screen for users | Enabled |
|  | Suppress unsupported OS warning to avoid disruption | Enabled |
|  | Enable browser sign-in and force users to sign in | Force (2) |
|  | Shopping in Microsoft Edge feature | Disabled |
|  | Allow users to be prompted for Microsoft Wallet password | Disabled |
|  | Show feature and merchandise recommendations in Edge | Disabled |
|  | Allow feature suggestions in sidebar | Disabled |
|  | Allow side panel sites list customization | Disabled |
|  | Define a list of allowed URLs | ["*.company.com","*.microsoft.com","*.office.com","login.microsoftonline.com"] |
|  | Block access to a list of URLs | ["*"] |
|  | Allows you to set a list of URL patterns that specify sites which are not allowed to load images | ["*"] |
|  | Configure Microsoft Defender Application Guard | Enabled |
|  | Prevents files from being uploaded to Microsoft Defender Application Guard | Enabled |
|  | Traffic Identification | Enabled |
|  | Prevent bypassing Microsoft Defender SmartScreen prompts for sites | Enabled |
|  | Prevent bypassing of Microsoft Defender SmartScreen warnings about downloads | Enabled |
|  | Enable Application Bound Encryption to protect sensitive data | Enabled |
|  | Enhance the security state in Microsoft Edge | Strict |
|  | Control which extensions cannot be installed | ["*"] |
|  | Control where developer tools can be used | Disallowed (2) |
|  | Block external extensions from being installed | Enabled |
|  | Control use of the WebUSB API | Do not allow any site to request access to USB devices (2) |
|  | Control use of the WebHID API | Do not allow any site to request access to HID devices (2) |
|  | Control use of the Web Bluetooth API | Do not allow any site to request access to Bluetooth devices (2) |
|  | Control use of the Serial API | Do not allow any site to request access to serial ports (2) |
|  | Continue running background apps after Microsoft Edge closes | Disabled |
|  | Clear browsing data when Microsoft Edge closes | Enabled |
|  | Configure InPrivate mode availability | InPrivate mode forced (2) |
|  | Enable Guest mode in browser | Disabled |
|  | Block insecure content on specified sites | ["*"] |
|  | Enable site isolation for every site | Enabled |
|  | Allow user feedback | Disabled |
|  | Enable the Click-to-Call feature in Microsoft Edge | Disabled |
|  | Set download directory | 1 (prompt for location) |
|  | Allow download restrictions | Block all downloads (3) |
|  | Prompt for download location | Enabled |
|  | Enable printing | Disabled |
|  | Print Headers and Footers | Disabled |
|  | Enable print preview | Disabled |
|  | Browsing Data Lifetime Settings | [{"data_types": ["browsing_history","download_history","cookies_and_other_site_data","cached_images_and_files"],"time_to_live_in_hours": 24}] |
|  | Enable use of ephemeral profiles | Enabled |
|  | Clear cached images and files on exit | Enabled |
|  | Allow screen capture | Disabled |
|  | Allow screenshots of Windows Defender Application Guard | Disabled |
|  | Password manager enabled | Disabled |
|  | Allow password reveal button | Disabled |
|  | Enable Password Monitor | Disabled |
|  | Configure Copilot | Disabled |
|  | Show Compose on websites | Disabled |
|  | Allow Image Creator in Microsoft Edge | Disabled |
|  | Disable synchronization of data | Enabled |
|  | Sync Types Disabled | ["favorites","settings","passwords","addresses","collections","tabs","extensions","history"] |
|  | Show Collections menu entry | Disabled |
|  | Allow users to access the games menu | Disabled |
|  | Enable split screen | Disabled |
|  | Enable Drop feature in Microsoft Edge | Disabled |
|  | Enable Microsoft Wallet payment feature | Disabled |
|  | Allow sidebar in Microsoft Edge | Disabled |
|  | Enable Microsoft Search in sidebar | Disabled |
|  | Show Microsoft Rewards app in Microsoft Edge sidebar | Disabled |
|  | Default media stream setting | Don't allow any site to request access (2) |
|  | Default geolocation setting | Don't allow any site to track location (2) |
|  | Default sensors setting | Don't allow any site to access sensors (2) |
|  | Default notification setting | Don't allow notifications (2) |
|  | Minimum SSL version enabled | TLS 1.3 |
|  | Require online OCSP/CRL checks | Enabled |
|  | Allow proceeding from the SSL warning page | Disabled |
|  | Allow certificates from root stores | Disabled |
|  | Enable the default search provider | Enabled |
|  | Default search provider name | Microsoft Bing |
|  | Default search provider search URL | https://www.bing.com/search?q={searchTerms} |
|  | Default search provider keyword | bing |
|  | Enable Microsoft Bing trending suggestions in the address bar | Disabled |
|  | Enable related matches in Find on Page | Disabled |
|  | Configure when efficiency mode should become active | Enabled, Efficiency mode is always active |
|  | Configure sleeping tabs | Enabled |
|  | Action to take on startup | Open specific pages (4) |
|  | URLs to open on startup | ["https://portal.office.com"] |
|  | Target Version Override | [Specific version - e.g., "120.0.6099"] |
|  | Update policy override default | Manual updates only (0) |
|  | Rollback to Target version | Always rollback to target version (1) |
|  | Remove Desktop Shortcuts upon update default | Force delete system-level and user-level Desktop Shortcuts (2) |
|  | Control updater's communication with the Experimentation and Configuration Service | Disabled (0) |

10. Select **Next**.  
11. For **Scope tags**, select the appropriate scope tag.  
12. For **Assignments**, assign to **SEB-Level3-Devices** group.  
13. Select **Next** to review the settings. Then choose **Create**.  

**Validation:**

- Test URL filtering: Navigate to non-allowlisted site (should be blocked)  
- Verify Application Guard: Check for container when accessing external sites  
- Test download blocking: All downloads should be blocked  
- Verify clipboard restrictions: Copy/paste should only work on *.company.com sites  
- Test print blocking: Printing should be disabled  
- Verify feature lockdown: Collections, games, sidebar, drop, wallet should all be disabled  

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

### Level 1 - Enterprise basic security for macOS

1. Go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Devices** > **macOS** > **Manage devices** > **Configuration** > **Create** > **New policy**.  
3. For **Platform**, choose **macOS**. For **Profile type**, choose **Settings catalog**.  
4. Select **Create**.  
5. On the **Basics** tab, enter:  
   - **Name:** Level 1 – Enterprise basic security – macOS Settings Catalog  
   - **Description:** Basic browser security for Microsoft Edge on macOS.  
6. Select **Next**.  
7. On **Configuration settings**, select **+ Add settings**.  
8. In the **Settings picker**, locate each setting using one of the following options:  
   - **Search for a setting:** Copy the **Setting** from the table and paste it into search.
   - **Browse by category:** Select the **Category** listed for that setting.
9. Configure the setting using the **Value** specified.

| Category | Setting | Value |
|--------------------|---------|-------|
|  | Configure Microsoft Defender SmartScreen | Enabled |
|  | Configure Microsoft Defender SmartScreen to block potentially unwanted apps | Enabled |
|  | Configure Automatic HTTPS | Enabled |
|  | Default pop-up window setting | Do not allow popups (2) |
|  | Block third party cookies | Enabled |
|  | Control the mode of DNS-over-HTTPS | Enable without fallback |
|  | DNS interception checks enabled | Enabled |
|  | Allow QUIC protocol | Disabled |
|  | Block tracking of users' web-browsing activity | Strict (3) |
|  | Enable network prediction | Don't predict (2) |
|  | Enable search suggestions | Disabled |
|  | Send required and optional diagnostic data | Off (0) |
|  | Configure Do Not Track | Enabled |
|  | Default geolocation setting | Don't allow any site to track location (2) |
|  | Default sensors setting | Don't allow any site to access sensors (2) |
|  | Default notification setting | Don't allow notifications (2) |
|  | Default media stream setting | Don't allow any site to request access (2) |
|  | Enable saving passwords to the password manager | Disabled |
|  | Enable AutoFill for addresses | Disabled |
|  | Enable AutoFill for credit cards | Disabled |
|  | Biometric authentication for local data storage reauth | Disabled |
|  | Allow importing of autofill form data | Disabled |
|  | Allow importing of saved passwords | Disabled |
|  | Allow importing of browsing history | Disabled |
|  | Allow importing of payment info | Disabled |
|  | Configure the home page URL | https://portal.office.com |
|  | Show Home button on toolbar | Enabled |
|  | Hide the First-run experience | Enabled |
|  | Enable browser sign-in | Force users to sign in (2) |
|  | Enable the default search provider | Enabled |
|  | Default search provider name | Microsoft Bing |
|  | Default search provider search URL | https://www.bing.com/search?q={searchTerms} |

10. Select **Next**.  
11. For **Scope tags**, select the appropriate scope tag.  
12. For **Assignments**, assign to **SEB-Level1-Devices** group.  
13. Select **Next** to review the settings. Then choose **Create**.  

### Level 2 - Enterprise enhanced security for macOS

1. Go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Devices** > **macOS** > **Manage devices** > **Configuration** > **Create** > **New policy**.  
3. For **Platform**, choose **macOS**. For **Profile type**, choose **Settings catalog**.  
4. Select **Create**.  
5. On the **Basics** tab, enter:  
   - **Name:** Level 2 – Enterprise enhanced security – macOS Settings Catalog  
   - **Description:** Enhanced security with extension blocking and privacy controls.  
6. Select **Next**.  
7. On **Configuration settings**, select **+ Add settings**.  
8. In the **Settings picker**, locate each setting using one of the following options:  
   - **Search for a setting:** Copy the **Setting** from the table and paste it into search.  
   - **Browse by category:** Select the **Category** listed for that setting.  
   When multiple results appear, choose the entry that matches the **Category**.  
9. Configure the setting using the **Value** specified.

| Category | Setting | Value |
|--------------------|---------|-------|
|  | Configure Microsoft Defender SmartScreen | Enabled |
|  | Configure Microsoft Defender SmartScreen to block potentially unwanted apps | Enabled |
|  | Configure Automatic HTTPS | Enabled |
|  | Default pop-up window setting | Do not allow popups (2) |
|  | Block third party cookies | Enabled |
|  | Prevent bypassing Microsoft Defender SmartScreen prompts for sites | Enabled |
|  | Prevent bypassing of Microsoft Defender SmartScreen warnings about downloads | Enabled |
|  | Enhance the security state in Microsoft Edge | Strict |
|  | Configure InPrivate mode availability | Disabled (1) |
|  | Enable Guest mode in browser | Disabled |
|  | Control the mode of DNS-over-HTTPS | Enable without fallback |
|  | DNS interception checks enabled | Enabled |
|  | Allow QUIC protocol | Disabled |
|  | Block tracking of users' web-browsing activity | Strict (3) |
|  | Enable network prediction | Don't predict (2) |
|  | Enable search suggestions | Disabled |
|  | Send required and optional diagnostic data | Off (0) |
|  | Configure Do Not Track | Enabled |
|  | Continue running background apps after Microsoft Edge closes | Disabled |
|  | Disable synchronization of data | Enabled |
|  | Clear browsing data when Microsoft Edge closes | Enabled |
|  | Enable Microsoft Bing trending suggestions | Disabled |
|  | Allow user feedback | Disabled |
|  | Default geolocation setting | Don't allow any site to track location (2) |
|  | Default sensors setting | Don't allow any site to access sensors (2) |
|  | Default notification setting | Don't allow notifications (2) |
|  | Default media stream setting | Don't allow any site to request access (2) |
|  | Block insecure content on specified sites | ["*"] |
|  | Enable site isolation for every site | Enabled |
|  | Enable saving passwords to the password manager | Disabled |
|  | Enable AutoFill for addresses | Disabled |
|  | Enable AutoFill for credit cards | Disabled |
|  | Biometric authentication for local data storage reauth | Disabled |
|  | Allow importing of autofill form data | Disabled |
|  | Allow importing of saved passwords | Disabled |
|  | Allow importing of browsing history | Disabled |
|  | Allow importing of payment info | Disabled |
|  | Set download directory | Prompt for location (1) |
|  | Allow download restrictions | Block dangerous downloads (1) |
|  | Allow users to access the games menu | Disabled |
|  | Show Collections menu entry | Disabled |
|  | Configure the home page URL | https://portal.office.com |
|  | Show Home button on toolbar | Enabled |
|  | Hide the First-run experience | Enabled |
|  | Enable browser sign-in | Force users to sign in (2) |
|  | Enable the default search provider | Enabled |
|  | Default search provider name | Microsoft Bing |
|  | Default search provider search URL | https://www.bing.com/search?q={searchTerms} |
|  | Configure Copilot page context | Copilot can't use page content (1) |
|  | Show Compose on websites | Disabled |
|  | Control which extensions can't be installed | ["*"] |
|  | Control where developer tools can be used | Disallowed (2) |
|  | Block external extensions from being installed | Enabled |
|  | Control use of the WebUSB API | Do not allow (2) |
|  | Control use of the WebHID API | Do not allow (2) |
|  | Control use of the Web Bluetooth API | Do not allow (2) |
|  | Control use of the Serial API | Do not allow (2) |
|  | Minimum SSL version enabled | TLS 1.2 |
|  | Require online OCSP/CRL checks for local trust anchors | Enabled |

10. Select **Next**.  
11. For **Scope tags**, select the appropriate scope tag.  
12. For **Assignments**, assign to **SEB-Level2-Devices** group.  
13. Select **Next** to review the settings. Then choose **Create**.  

### Level 3 - Enterprise high security for macOS

1. Go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Devices** > **macOS** > **Manage devices** > **Configuration** > **Create** > **New policy**.  
3. For **Platform**, choose **macOS**. For **Profile type**, choose **Settings catalog**.  
4. Select **Create**.  
5. On the **Basics** tab, enter:  
   - **Name:** Level 3 – Enterprise high security – macOS Settings Catalog  
   - **Description:** High-security configuration with URL filtering and maximum restrictions.  
6. Select **Next**.  
7. On **Configuration settings**, select **+ Add settings**.  
8. In the **Settings picker**, locate each setting using one of the following options:  
   - **Search for a setting:** Copy the **Setting** from the table and paste it into search.  
   - **Browse by category:** Select the **Category** listed for that setting.  
   When multiple results appear, choose the entry that matches the **Category**.
9. Configure the setting using the **Value** specified.

| Category | Setting | Value |
|--------------------|---------|-------|
|  | Configure Microsoft Defender SmartScreen | Enabled |
|  | Configure Microsoft Defender SmartScreen to block potentially unwanted apps | Enabled |
|  | Configure Automatic HTTPS | Enabled |
|  | Default pop-up window setting | Do not allow popups (2) |
|  | Block third party cookies | Enabled |
|  | Prevent bypassing Microsoft Defender SmartScreen prompts for sites | Enabled |
|  | Prevent bypassing of Microsoft Defender SmartScreen warnings about downloads | Enabled |
|  | Enhance the security state in Microsoft Edge | Strict |
|  | Configure InPrivate mode availability | InPrivate mode forced (2) |
|  | Enable Guest mode in browser | Disabled |
|  | Control the mode of DNS-over-HTTPS | Enable without fallback |
|  | DNS interception checks enabled | Enabled |
|  | Allow QUIC protocol | Disabled |
|  | Define a list of allowed URLs | ["*.company.com","*.microsoft.com","*.office.com","login.microsoftonline.com"] |
|  | Block access to a list of URLs | ["*"] |
|  | Sites not allowed to load images | ["*"] |
|  | Block tracking of users' web-browsing activity | Strict (3) |
|  | Enable network prediction | Don't predict (2) |
|  | Enable search suggestions | Disabled |
|  | Send required and optional diagnostic data | Off (0) |
|  | Configure Do Not Track | Enabled |
|  | Continue running background apps after Microsoft Edge closes | Disabled |
|  | Disable synchronization of data | Enabled |
|  | Clear browsing data when Microsoft Edge closes | Enabled |
|  | Enable Microsoft Bing trending suggestions | Disabled |
|  | Allow user feedback | Disabled |
|  | Default geolocation setting | Don't allow any site to track location (2) |
|  | Default sensors setting | Don't allow any site to access sensors (2) |
|  | Default notification setting | Don't allow notifications (2) |
|  | Default media stream setting | Don't allow any site to request access (2) |
|  | Block insecure content on specified sites | ["*"] |
|  | Enable site isolation for every site | Enabled |
|  | Allow clipboard use on specific sites | ["*.company.com"] |
|  | Block clipboard use on specific sites | ["*"] |
|  | Enable saving passwords to the password manager | Disabled |
|  | Enable AutoFill for addresses | Disabled |
|  | Enable AutoFill for credit cards | Disabled |
|  | Biometric authentication for local data storage reauth | Disabled |
|  | Allow password reveal button | Disabled |
|  | Enable Password Monitor | Disabled |
|  | Allow importing of autofill form data | Disabled |
|  | Allow importing of saved passwords | Disabled |
|  | Allow importing of browsing history | Disabled |
|  | Allow importing of payment info | Disabled |
|  | Set download directory | Prompt for location (1) |
|  | Allow download restrictions | Block all downloads (3) |
|  | Prompt for download location | Enabled |
|  | Allow download restrictions | Block all downloads (3) |
|  | Enable printing | Disabled |
|  | Print Headers and Footers | Disabled |
|  | Enable print preview | Disabled |
|  | Browsing Data Lifetime Settings | [{"data_types": ["browsing_history", "download_history", "cookies_and_other_site_data", "cached_images_and_files"], "time_to_live_in_hours": 24}] |
|  | Clear cached images and files on exit | Enabled |
|  | Clear browsing data when Microsoft Edge closes | Enabled |
|  | Allow users to access the games menu | Disabled |
|  | Show Collections menu entry | Disabled |
|  | Allow sidebar in Microsoft Edge | Disabled |
|  | Enable Microsoft Search in sidebar | Disabled |
|  | Enable Drop feature | Disabled |
|  | Enable Microsoft Wallet payment feature | Disabled |
|  | Configure the home page URL | https://portal.office.com |
|  | Show Home button on toolbar | Enabled |
|  | Hide the First-run experience | Enabled |
|  | Enable browser sign-in | Force users to sign in (2) |
|  | Enable the default search provider | Enabled |
|  | Default search provider name | Microsoft Bing |
|  | Default search provider search URL | https://www.bing.com/search?q={searchTerms} |
|  | Configure Copilot | Disabled |
|  | Show Compose on websites | Disabled |
|  | Allow Image Creator in Microsoft Edge | Disabled |
|  | Sync Types Disabled | ["favorites","settings","passwords","addresses","collections","tabs","extensions","history"] |
|  | Control which extensions can't be installed | ["*"] |
|  | Control where developer tools can be used | Disallowed (2) |
|  | Block external extensions from being installed | Enabled |
|  | Control use of the WebUSB API | Do not allow (2) |
|  | Control use of the WebHID API | Do not allow (2) |
|  | Control use of the Web Bluetooth API | Do not allow (2) |
|  | Control use of the Serial API | Do not allow (2) |
|  | Minimum SSL version enabled | TLS 1.3 |
|  | Require online OCSP/CRL checks for local trust anchors | Enabled |
|  | Allow proceeding from the SSL warning page | Disabled |

10. Select **Next**.  
11. For **Scope tags**, select the appropriate scope tags and select **Next**.
12. For **Assignments**, assign to **SEB-Level3-Devices** group. 
13. Select **Next** to review the settings. Then choose **Create**.

## Validation

After deploying Settings Catalog policies:

1. **Policy Deployment**: Check Intune console for successful policy deployment  
2. **Endpoint Verification**: On device, navigate to edge://policy and verify settings  
3. **Security Testing**: Test blocked features (downloads, extensions, URLs) per level  
4. **User Experience**: Verify browser functionality meets business requirements  

::: zone-end

## Next steps

Continue to [Step 6](mamedge-6-security-baseline.md) to deploy the Microsoft Edge security baseline.

