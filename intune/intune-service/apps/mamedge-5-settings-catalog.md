---
title: Step 5. Create Settings Catalog policies for Microsoft Edge for Business
description: Step 5. Create Settings Catalog policies for Microsoft Edge for Business on Windows and macOS.
ms.date: 01/16/2025
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

Settings Catalog for Windows provides comprehensive browser configuration with progressive security levels aligned with NIST, DISA STIG, and CISA frameworks. Following this guide doen’t make your organization compliant with these standards; they were used as input to build the security framework.

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

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Devices** > **Windows** > **Manage devices** > **Configuration** > **Create** > **New Policy**.  
3. Select **Windows 10 and later** for platform and **Settings catalog** for profile type.  
4. Select **Create**.  
5. On the **Basics** tab:  
   - **Name:** Level 1 - Enterprise basic security - Windows Settings Catalog  
   - **Description:** Basic browser security configuration for Microsoft Edge on Windows devices.  
6. Select **Next**.  
7. On **Configuration settings**, select **+ Add settings**.
8. From the **Settings picker**, search for **Microsoft Edge** and select it.
9. Select the following settings:

| Configuration Area | Category | Setting |
|--------------------|-----------|----------|
| Core Security (SmartScreen & HTTPS) | Microsoft Edge | Configure Microsoft Defender SmartScreen to<br>protect users from malicious sites: Enabled |
|  | Microsoft Edge | Configure Microsoft Defender SmartScreen<br>to block potentially unwanted apps: Enabled |
|  | Microsoft Edge | Configure Automatic HTTPS to ensure<br>secure connections: Enabled |
| Privacy & Tracking Prevention | Microsoft Edge | Block tracking of users' web-browsing<br>activity: Strict (3) |
|  | Microsoft Edge | Enable network prediction to improve<br>performance: Don't predict (2) |
|  | Microsoft Edge | Enable search suggestions for the address<br>bar: Disabled |
|  | Microsoft Edge | Send required and optional diagnostic data<br>about browser usage: Off (0) |
|  | Microsoft Edge | Configure Do Not Track setting to signal<br>user preference: Enabled |
| Content Settings & Security | Microsoft Edge | Default pop-up window setting (Device):<br>Don't allow any site to show popups (2) |
|  | Microsoft Edge | Default geolocation setting (Device):<br>Don't allow any site to track location (2) |
|  | Microsoft Edge | Default sensors setting (Device):<br>Don't allow sites to access sensors (2) |
|  | Microsoft Edge | Default notification setting (Device):<br>Don't allow any site to show notifications (2) |
|  | Microsoft Edge | Default media stream setting (Device):<br>Don't allow access to camera/mic (2) |
|  | Microsoft Edge | Block third party cookies to improve<br>privacy: Enabled |
| Password & Autofill Security | Microsoft Edge | Enable saving passwords to the password<br>manager: Disabled |
|  | Microsoft Edge | Enable AutoFill for addresses and contact<br>information: Disabled |
|  | Microsoft Edge | Enable AutoFill for payment instruments<br>and cards: Disabled |
|  | Microsoft Edge | Biometric authentication for local data<br>storage reauth: Disabled |
| Import & Export Controls | Microsoft Edge | Allow importing of autofill form data:<br>Disabled |
|  | Microsoft Edge | Allow importing of saved passwords:<br>Disabled |
|  | Microsoft Edge | Allow importing of browsing history:<br>Disabled |
|  | Microsoft Edge | Allow importing of payment information:<br>Disabled |
| Browser Experience & Customization | Microsoft Edge | Configure the home page URL:<br>https://portal.office.com |
|  | Microsoft Edge | Show Home button on toolbar for user<br>convenience: Enabled |
|  | Microsoft Edge | Hide the First-run experience and splash<br>screen for users: Enabled |
|  | Microsoft Edge | Suppress unsupported OS warning to avoid<br>disruption: Enabled |
|  | Microsoft Edge | Enable browser sign-in and force users to<br>sign in: Force (2) |
| Shopping & Consumer Features | Microsoft Edge | Shopping in Microsoft Edge feature:<br>Disabled |
|  | Microsoft Edge | Allow users to be prompted for Microsoft<br>Wallet password: Disabled |
|  | Microsoft Edge | Show feature and merchandise<br>recommendations in Edge: Disabled |
| Sidebar & UI Features | Microsoft Edge | Allow feature suggestions in sidebar:<br>Disabled |
|  | Microsoft Edge | Enable Microsoft Search integration in<br>sidebar: Disabled |
|  | Microsoft Edge | Allow side panel sites list customization:<br>Disabled |
| AI & Copilot Features | Microsoft Edge | Configure Copilot integration:<br>Enabled, but available to users |
|  | Microsoft Edge | Control the mode of the Copilot AI<br>features: AI-powered features available |
| Network & DNS | Microsoft Edge | Control the mode of DNS-over-HTTPS:<br>Enabled, fallback to insecure DNS allowed |
|  | Microsoft Edge | DNS interception checks for validation:<br>Enabled |
|  | Microsoft Edge | Allow QUIC protocol for connectivity:<br>Disabled |
| Search Engine Configuration | Microsoft Edge | Enable the default search provider:<br>Enabled |
|  | Microsoft Edge | Default search provider name:<br>Microsoft Bing |
|  | Microsoft Edge | Default search provider search URL:<br>https://www.bing.com/search?q={searchTerms} |
|  | Microsoft Edge | Default search provider keyword:<br>bing |
| Privacy Sandbox & Data Collection | Microsoft Edge | Privacy Sandbox Ad measurement feature:<br>Disabled |
|  | Microsoft Edge | Privacy Sandbox Topics feature:<br>Disabled |
|  | Microsoft Edge | Privacy Sandbox Fledge feature:<br>Disabled |
|  | Microsoft Edge | Personalize detected languages for<br>website translation: Disabled |
| Experimentation & Telemetry | Microsoft Edge | Experimentation and Configuration Service<br>Control: Retrieve configurations (1) |
| Update Management | Microsoft Edge Update | Control updater's communication with the<br>Experimentation and Configuration Service:<br>Disabled (0) |

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

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Devices** > **Windows** > **Manage devices** > **Configuration** > **Create** > **New Policy**.  
3. Select **Windows 10 and later** for platform and **Settings catalog** for profile type.  
4. Select **Create**.  
5. On the **Basics** tab:  
   - **Name:** Level 2 - Enterprise enhanced security - Windows Settings Catalog  
   - **Description:** Enhanced browser security including Application Bound Encryption and extension controls.
6. Select **Next**.  
7. On **Configuration settings**, select **+ Add settings**.
8. From the **Settings picker**, search for **Microsoft Edge** and select it.
9. Select the following settings:

| Configuration Area | Category | Setting |
|--------------------|-----------|----------|
| Core Security (SmartScreen & HTTPS) | Microsoft Edge | Configure Microsoft Defender SmartScreen to<br>protect users from malicious sites: Enabled |
|  | Microsoft Edge | Configure Microsoft Defender SmartScreen<br>to block potentially unwanted apps: Enabled |
|  | Microsoft Edge | Configure Automatic HTTPS to ensure<br>secure connections: Enabled |
| Privacy & Tracking Prevention | Microsoft Edge | Block tracking of users' web-browsing<br>activity: Strict (3) |
|  | Microsoft Edge | Enable network prediction to improve<br>performance: Don't predict (2) |
|  | Microsoft Edge | Enable search suggestions for the address<br>bar: Disabled |
|  | Microsoft Edge | Send required and optional diagnostic data<br>about browser usage: Off (0) |
|  | Microsoft Edge | Configure Do Not Track setting to signal<br>user preference: Enabled |
| Content Settings & Security | Microsoft Edge | Default pop-up window setting (Device):<br>Don't allow any site to show popups (2) |
|  | Microsoft Edge | Default geolocation setting (Device):<br>Don't allow any site to track location (2) |
|  | Microsoft Edge | Default sensors setting (Device):<br>Don't allow sites to access sensors (2) |
|  | Microsoft Edge | Default notification setting (Device):<br>Don't allow any site to show notifications (2) |
|  | Microsoft Edge | Default media stream setting (Device):<br>Don't allow access to camera/mic (2) |
|  | Microsoft Edge | Block third party cookies to improve<br>privacy: Enabled |
| Password & Autofill Security | Microsoft Edge | Enable saving passwords to the password<br>manager: Disabled |
|  | Microsoft Edge | Enable AutoFill for addresses and contact<br>information: Disabled |
|  | Microsoft Edge | Enable AutoFill for payment instruments<br>and cards: Disabled |
|  | Microsoft Edge | Biometric authentication for local data<br>storage reauth: Disabled |
| Import & Export Controls | Microsoft Edge | Allow importing of autofill form data:<br>Disabled |
|  | Microsoft Edge | Allow importing of saved passwords:<br>Disabled |
|  | Microsoft Edge | Allow importing of browsing history:<br>Disabled |
|  | Microsoft Edge | Allow importing of payment information:<br>Disabled |
| Browser Experience & Customization | Microsoft Edge | Configure the home page URL:<br>https://portal.office.com |
|  | Microsoft Edge | Show Home button on toolbar for user<br>convenience: Enabled |
|  | Microsoft Edge | Hide the First-run experience and splash<br>screen for users: Enabled |
|  | Microsoft Edge | Suppress unsupported OS warning to avoid<br>disruption: Enabled |
|  | Microsoft Edge | Enable browser sign-in and force users to<br>sign in: Force (2) |
| Shopping & Consumer Features | Microsoft Edge | Shopping in Microsoft Edge feature:<br>Disabled |
|  | Microsoft Edge | Allow users to be prompted for Microsoft<br>Wallet password: Disabled |
|  | Microsoft Edge | Show feature and merchandise<br>recommendations in Edge: Disabled |
| Sidebar & UI Features | Microsoft Edge | Allow feature suggestions in sidebar:<br>Disabled |
|  | Microsoft Edge | Enable Microsoft Search integration in<br>sidebar: Disabled |
|  | Microsoft Edge | Allow side panel sites list customization:<br>Disabled |
| AI & Copilot Features | Microsoft Edge | Configure Copilot integration:<br>Enabled, but available to users |
|  | Microsoft Edge | Control the mode of the Copilot AI<br>features: AI-powered features available |
| Network & DNS | Microsoft Edge | Control the mode of DNS-over-HTTPS:<br>Enabled, fallback to insecure DNS allowed |
|  | Microsoft Edge | DNS interception checks for validation:<br>Enabled |
|  | Microsoft Edge | Allow QUIC protocol for connectivity:<br>Disabled |
| Search Engine Configuration | Microsoft Edge | Enable the default search provider:<br>Enabled |
|  | Microsoft Edge | Default search provider name:<br>Microsoft Bing |
|  | Microsoft Edge | Default search provider search URL:<br>https://www.bing.com/search?q={searchTerms} |
|  | Microsoft Edge | Default search provider keyword:<br>bing |
| Privacy Sandbox & Data Collection | Microsoft Edge | Privacy Sandbox Ad measurement feature:<br>Disabled |
|  | Microsoft Edge | Privacy Sandbox Topics feature:<br>Disabled |
|  | Microsoft Edge | Privacy Sandbox Fledge feature:<br>Disabled |
|  | Microsoft Edge | Personalize detected languages for<br>website translation: Disabled |
| Experimentation & Telemetry | Microsoft Edge | Experimentation and Configuration Service<br>Control: Retrieve configurations (1) |
| Update Management | Microsoft Edge Update | Control updater's communication with the<br>Experimentation and Configuration Service:<br>Disabled (0) |
| Enhanced SmartScreen & Security | Microsoft Edge | Prevent bypassing Microsoft Defender<br>SmartScreen prompts for sites: Enabled |
|  | Microsoft Edge | Prevent bypassing of Microsoft Defender<br>SmartScreen warnings about downloads: Enabled |
|  | Microsoft Edge | Enable Application Bound Encryption to<br>protect sensitive data: Enabled |
|  | Microsoft Edge | Enhance the security state in Microsoft<br>Edge: Strict |
| Extension Management & Developer Tools | Microsoft Edge | Control which extensions cannot be<br>installed: ["*"] |
|  | Microsoft Edge | Control where developer tools can be<br>used: Disallowed (2) |
|  | Microsoft Edge | Block external extensions from being<br>installed: Enabled |
| API & Hardware Access Controls | Microsoft Edge | Control use of the WebUSB API:<br>Do not allow any site to request access to<br>USB devices (2) |
|  | Microsoft Edge | Control use of the WebHID API:<br>Do not allow any site to request access to<br>HID devices (2) |
|  | Microsoft Edge | Control use of the Web Bluetooth API:<br>Do not allow any site to request access to<br>Bluetooth devices (2) |
|  | Microsoft Edge | Control use of the Serial API:<br>Do not allow any site to request access to<br>serial ports (2) |
| Privacy & Data Controls | Microsoft Edge | Continue running background apps after<br>Microsoft Edge closes: Disabled |
|  | Microsoft Edge | Disable synchronization of data using<br>Microsoft sync services: Enabled |
|  | Microsoft Edge | Clear browsing data when Microsoft Edge<br>closes: Enabled |
|  | Microsoft Edge | Configure InPrivate mode availability:<br>Disabled (1) |
|  | Microsoft Edge | Enable Guest mode in browser:<br>Disabled |
| Content & Script Security | Microsoft Edge | Block insecure content on specified sites:<br>["*"] |
|  | Microsoft Edge | Enable site isolation for every site:<br>Enabled |
|  | Microsoft Edge | Allow user feedback:<br>Disabled |
|  | Microsoft Edge | Enable the Click-to-Call feature in<br>Microsoft Edge: Disabled |
| Download & File Security | Microsoft Edge | Set download directory:<br>1 (prompt for location) |
|  | Microsoft Edge | Allow download restrictions:<br>Block dangerous downloads (1) |
| Browser Features & UI | Microsoft Edge | Allow users to access the games menu in<br>Microsoft Edge: Disabled |
|  | Microsoft Edge | Enable split screen in Microsoft Edge:<br>Disabled |
|  | Microsoft Edge | Show Collections menu entry:<br>Disabled |
|  | Microsoft Edge | Show microsoft.com homepage as desktop<br>Start page instead of New Tab page:<br>Disabled |
| AI & Copilot Enhanced Controls | Microsoft Edge | Configure Copilot page context:<br>Copilot can't use page content for<br>prompts (1) |
|  | Microsoft Edge | Show Compose (writing assistance) on<br>websites: Disabled |
|  | Microsoft Edge | Show a prompt to organize tabs:<br>Disabled |
| Certificate & Security | Microsoft Edge | Minimum SSL version enabled:<br>TLS 1.2 |
|  | Microsoft Edge | Require online OCSP/CRL checks for local<br>trust anchors: Enabled |
|  | Microsoft Edge | Allow certificates from root stores:<br>Disabled |
| Search & Address Bar | Microsoft Edge | Enable Microsoft Bing trending suggestions<br>in the address bar: Disabled |
|  | Microsoft Edge | Enable related matches in Find on Page:<br>Disabled |
| Performance & Resource Management | Microsoft Edge | Configure when efficiency mode should<br>become active: Enabled, Efficiency mode is<br>always active |
|  | Microsoft Edge | Configure sleeping tabs:<br>Enabled |
| Startup & Behavior | Microsoft Edge | Action to take on startup:<br>Open specific pages (4) |
|  | Microsoft Edge | URLs to open on startup:<br>["https://portal.office.com"] |
| Update Management | Microsoft Edge Update | Update policy override default:<br>Automatic silent updates only (3) |

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

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Devices** > **Windows** > **Manage devices** > **Configuration** > **Create** > **New Policy**.  
3. Select **Windows 10 and later** for platform and **Settings catalog** for profile type.  
4. Select **Create**.  
5. On the **Basics** tab:  
   - **Name:** Level 3 - Enterprise high security - Windows Settings Catalog  
   - **Description:** High security including URL allowlisting, Application Guard, and zero-trust controls.  
6. Select **Next**.  
7. On **Configuration settings**, select **+ Add settings**.
8. From the **Settings picker**, search for **Microsoft Edge** and select it.
9. Select the following settings:

| Configuration Area | Category | Setting |
|--------------------|-----------|----------|
| Core Security (SmartScreen & HTTPS) | Microsoft Edge | Configure Microsoft Defender SmartScreen to<br>protect users from malicious sites: Enabled |
|  | Microsoft Edge | Configure Microsoft Defender SmartScreen<br>to block potentially unwanted apps: Enabled |
|  | Microsoft Edge | Configure Automatic HTTPS to ensure<br>secure connections: Enabled |
| Privacy & Tracking Prevention | Microsoft Edge | Block tracking of users' web-browsing<br>activity: Strict (3) |
|  | Microsoft Edge | Enable network prediction to improve<br>performance: Don't predict (2) |
|  | Microsoft Edge | Enable search suggestions for the address<br>bar: Disabled |
|  | Microsoft Edge | Send required and optional diagnostic data<br>about browser usage: Off (0) |
|  | Microsoft Edge | Configure Do Not Track setting to signal<br>user preference: Enabled |
| Content Settings & Security | Microsoft Edge | Default pop-up window setting (Device):<br>Don't allow any site to show popups (2) |
|  | Microsoft Edge | Block third party cookies to improve<br>privacy: Enabled |
| Password & Autofill Security | Microsoft Edge | Enable saving passwords to the password<br>manager: Disabled |
|  | Microsoft Edge | Enable AutoFill for addresses and contact<br>information: Disabled |
|  | Microsoft Edge | Enable AutoFill for payment instruments<br>and cards: Disabled |
|  | Microsoft Edge | Biometric authentication for local data<br>storage reauth: Disabled |
| Import & Export Controls | Microsoft Edge | Allow importing of autofill form data:<br>Disabled |
|  | Microsoft Edge | Allow importing of saved passwords:<br>Disabled |
|  | Microsoft Edge | Allow importing of browsing history:<br>Disabled |
|  | Microsoft Edge | Allow importing of payment information:<br>Disabled |
| Browser Experience & Customization | Microsoft Edge | Configure the home page URL:<br>https://portal.office.com |
|  | Microsoft Edge | Show Home button on toolbar for user<br>convenience: Enabled |
|  | Microsoft Edge | Hide the First-run experience and splash<br>screen for users: Enabled |
|  | Microsoft Edge | Suppress unsupported OS warning to avoid<br>disruption: Enabled |
|  | Microsoft Edge | Enable browser sign-in and force users to<br>sign in: Force (2) |
| Shopping & Consumer Features | Microsoft Edge | Shopping in Microsoft Edge feature:<br>Disabled |
|  | Microsoft Edge | Allow users to be prompted for Microsoft<br>Wallet password: Disabled |
|  | Microsoft Edge | Show feature and merchandise<br>recommendations in Edge: Disabled |
| Sidebar & UI Features | Microsoft Edge | Allow feature suggestions in sidebar:<br>Disabled |
|  | Microsoft Edge | Allow side panel sites list customization:<br>Disabled |
| URL Filtering & Access Control | Microsoft Edge | Define a list of allowed URLs:<br>["*.company.com","*.microsoft.com","*.office.com","login.microsoftonline.com"] |
|  | Microsoft Edge | Block access to a list of URLs:<br>["*"] |
|  | Microsoft Edge | Allows you to set a list of URL patterns<br>that specify sites which are not allowed to<br>load images: ["*"] |
| Application Guard (Windows Defender Application Guard) | Microsoft Edge | Configure Microsoft Defender Application<br>Guard: Enabled |
|  | Microsoft Edge | Prevents files from being uploaded to<br>Microsoft Defender Application Guard:<br>Enabled |
|  | Microsoft Edge | Traffic Identification:<br>Enabled |
| Enhanced SmartScreen & Security | Microsoft Edge | Prevent bypassing Microsoft Defender<br>SmartScreen prompts for sites: Enabled |
|  | Microsoft Edge | Prevent bypassing of Microsoft Defender<br>SmartScreen warnings about downloads: Enabled |
|  | Microsoft Edge | Enable Application Bound Encryption to<br>protect sensitive data: Enabled |
|  | Microsoft Edge | Enhance the security state in Microsoft<br>Edge: Strict |
| Extension Management & Developer Tools | Microsoft Edge | Control which extensions cannot be<br>installed: ["*"] |
|  | Microsoft Edge | Control where developer tools can be<br>used: Disallowed (2) |
|  | Microsoft Edge | Block external extensions from being<br>installed: Enabled |
| API & Hardware Access Controls | Microsoft Edge | Control use of the WebUSB API:<br>Do not allow any site to request access to<br>USB devices (2) |
|  | Microsoft Edge | Control use of the WebHID API:<br>Do not allow any site to request access to<br>HID devices (2) |
|  | Microsoft Edge | Control use of the Web Bluetooth API:<br>Do not allow any site to request access to<br>Bluetooth devices (2) |
|  | Microsoft Edge | Control use of the Serial API:<br>Do not allow any site to request access to<br>serial ports (2) |
| Privacy & Data Controls | Microsoft Edge | Continue running background apps after<br>Microsoft Edge closes: Disabled |
|  | Microsoft Edge | Clear browsing data when Microsoft Edge<br>closes: Enabled |
| InPrivate & Guest Mode | Microsoft Edge | Configure InPrivate mode availability:<br>InPrivate mode forced (2) |
|  | Microsoft Edge | Enable Guest mode in browser:<br>Disabled |
| Content & Script Security | Microsoft Edge | Block insecure content on specified sites:<br>["*"] |
|  | Microsoft Edge | Enable site isolation for every site:<br>Enabled |
|  | Microsoft Edge | Allow user feedback:<br>Disabled |
|  | Microsoft Edge | Enable the Click-to-Call feature in<br>Microsoft Edge: Disabled |
| Download & File Security | Microsoft Edge | Set download directory:<br>1 (prompt for location) |
|  | Microsoft Edge | Allow download restrictions:<br>Block all downloads (3) |
|  | Microsoft Edge | Prompt for download location:<br>Enabled |
| Printing | Microsoft Edge | Enable printing:<br>Disabled |
|  | Microsoft Edge | Print Headers and Footers:<br>Disabled |
|  | Microsoft Edge | Enable print preview:<br>Disabled |
| GDPR Data Retention & Privacy | Microsoft Edge | Browsing Data Lifetime Settings:<br>[{"data_types": ["browsing_history","download_history","cookies_and_other_site_data","cached_images_and_files"],"time_to_live_in_hours": 24}] |
|  | Microsoft Edge | Enable use of ephemeral profiles:<br>Enabled |
|  | Microsoft Edge | Clear cached images and files on exit:<br>Enabled |
| Screen Capture & Recording | Microsoft Edge | Allow screen capture:<br>Disabled |
|  | Microsoft Edge | Allow screenshots of Windows Defender<br>Application Guard: Disabled |
| Password & Credential Management | Microsoft Edge | Password manager enabled:<br>Disabled |
|  | Microsoft Edge | Allow password reveal button:<br>Disabled |
|  | Microsoft Edge | Enable Password Monitor:<br>Disabled |
| AI & Copilot Maximum Restrictions | Microsoft Edge | Configure Copilot:<br>Disabled |
|  | Microsoft Edge | Show Compose on websites:<br>Disabled |
|  | Microsoft Edge | Allow Image Creator in Microsoft Edge:<br>Disabled |
| Sync & Data Sharing | Microsoft Edge | Disable synchronization of data:<br>Enabled |
|  | Microsoft Edge | Sync Types Disabled:<br>["favorites","settings","passwords","addresses","collections","tabs","extensions","history"] |
| Browser Features Lockdown | Microsoft Edge | Show Collections menu entry:<br>Disabled |
|  | Microsoft Edge | Allow users to access the games menu:<br>Disabled |
|  | Microsoft Edge | Enable split screen:<br>Disabled |
|  | Microsoft Edge | Enable Drop feature in Microsoft Edge:<br>Disabled |
|  | Microsoft Edge | Enable Microsoft Wallet payment feature:<br>Disabled |
| Sidebar & App Restrictions | Microsoft Edge | Allow sidebar in Microsoft Edge:<br>Disabled |
|  | Microsoft Edge | Enable Microsoft Search in sidebar:<br>Disabled |
|  | Microsoft Edge | Show Microsoft Rewards app in Microsoft<br>Edge sidebar: Disabled |
| Media & Device Access | Microsoft Edge | Default media stream setting:<br>Don't allow any site to request access (2) |
|  | Microsoft Edge | Default geolocation setting:<br>Don't allow any site to track location (2) |
|  | Microsoft Edge | Default sensors setting:<br>Don't allow any site to access sensors (2) |
|  | Microsoft Edge | Default notification setting:<br>Don't allow notifications (2) |
| Certificate & SSL Enforcement | Microsoft Edge | Minimum SSL version enabled:<br>TLS 1.3 |
|  | Microsoft Edge | Require online OCSP/CRL checks:<br>Enabled |
|  | Microsoft Edge | Allow proceeding from the SSL warning<br>page: Disabled |
| Certificate & Security | Microsoft Edge | Allow certificates from root stores:<br>Disabled |
| Search Engine Configuration | Microsoft Edge | Enable the default search provider:<br>Enabled |
|  | Microsoft Edge | Default search provider name:<br>Microsoft Bing |
|  | Microsoft Edge | Default search provider search URL:<br>https://www.bing.com/search?q={searchTerms} |
|  | Microsoft Edge | Default search provider keyword:<br>bing |
| Search & Address Bar | Microsoft Edge | Enable Microsoft Bing trending suggestions<br>in the address bar: Disabled |
|  | Microsoft Edge | Enable related matches in Find on Page:<br>Disabled |
| Performance & Resource Management | Microsoft Edge | Configure when efficiency mode should<br>become active: Enabled, Efficiency mode is<br>always active |
|  | Microsoft Edge | Configure sleeping tabs:<br>Enabled |
| Startup & Behavior | Microsoft Edge | Action to take on startup:<br>Open specific pages (4) |
|  | Microsoft Edge | URLs to open on startup:<br>["https://portal.office.com"] |
| Version Control & Update Management | Microsoft Edge Update | Target Version Override:<br>[Specific version - e.g., "120.0.6099"] |
|  | Microsoft Edge Update | Update policy override default:<br>Manual updates only (0) |
|  | Microsoft Edge Update | Rollback to Target version:<br>Always rollback to target version (1) |
|  | Microsoft Edge Update | Remove Desktop Shortcuts upon update<br>default: Force delete system-level and<br>user-level Desktop Shortcuts (2) |
| Update Management | Microsoft Edge Update | Control updater's communication with the<br>Experimentation and Configuration Service:<br>Disabled (0) |

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

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Devices** > **macOS** > **Manage devices** > **Configuration** > **Create** > **New Policy**.  
3. Select **macOS** for platform and **Settings catalog** for profile type.  
4. Select **Create**.
5. On the **Basics** tab:  
   - **Name:** Level 1 - Enterprise basic security - macOS Settings Catalog  
   - **Description:** Basic browser security for Microsoft Edge on macOS.  
6. Select **Next**.  
7. On **Configuration settings**, select **+ Add settings**.
8. From the **Settings picker**, search for **Microsoft Edge** and select it.
9. Select the following settings:

| Configuration Area | Category | Setting |
|--------------------|-----------|----------|
| Core Security | Microsoft Edge | Configure Microsoft Defender SmartScreen:<br>Enabled |
|  | Microsoft Edge | Configure Microsoft Defender SmartScreen<br>to block potentially unwanted apps:<br>Enabled |
|  | Microsoft Edge | Configure Automatic HTTPS:<br>Enabled |
|  | Microsoft Edge | Default pop-up window setting:<br>Do not allow popups (2) |
|  | Microsoft Edge | Block third party cookies:<br>Enabled |
| Network Security | Microsoft Edge | Control the mode of DNS-over-HTTPS:<br>Enable without fallback |
|  | Microsoft Edge | DNS interception checks enabled:<br>Enabled |
|  | Microsoft Edge | Allow QUIC protocol:<br>Disabled |
| Privacy & Tracking | Microsoft Edge | Block tracking of users' web-browsing<br>activity: Strict (3) |
|  | Microsoft Edge | Enable network prediction:<br>Don't predict (2) |
|  | Microsoft Edge | Enable search suggestions:<br>Disabled |
|  | Microsoft Edge | Send required and optional diagnostic data:<br>Off (0) |
|  | Microsoft Edge | Configure Do Not Track:<br>Enabled |
| Content Settings | Microsoft Edge | Default geolocation setting:<br>Don't allow any site to track location (2) |
|  | Microsoft Edge | Default sensors setting:<br>Don't allow any site to access sensors (2) |
|  | Microsoft Edge | Default notification setting:<br>Don't allow notifications (2) |
|  | Microsoft Edge | Default media stream setting:<br>Don't allow any site to request access (2) |
| Password Management | Microsoft Edge | Enable saving passwords to the password<br>manager: Disabled |
|  | Microsoft Edge | Enable AutoFill for addresses:<br>Disabled |
|  | Microsoft Edge | Enable AutoFill for credit cards:<br>Disabled |
|  | Microsoft Edge | Biometric authentication for local data<br>storage reauth: Disabled |
| Import Controls | Microsoft Edge | Allow importing of autofill form data:<br>Disabled |
|  | Microsoft Edge | Allow importing of saved passwords:<br>Disabled |
|  | Microsoft Edge | Allow importing of browsing history:<br>Disabled |
|  | Microsoft Edge | Allow importing of payment info:<br>Disabled |
| Browser Experience | Microsoft Edge | Configure the home page URL:<br>https://portal.office.com |
|  | Microsoft Edge | Show Home button on toolbar:<br>Enabled |
|  | Microsoft Edge | Hide the First-run experience:<br>Enabled |
|  | Microsoft Edge | Enable browser sign-in:<br>Force users to sign in (2) |
| Search Engine | Microsoft Edge | Enable the default search provider:<br>Enabled |
|  | Microsoft Edge | Default search provider name:<br>Microsoft Bing |
|  | Microsoft Edge | Default search provider search URL:<br>https://www.bing.com/search?q={searchTerms} |

10. Select **Next**.  
11. For **Scope tags**, select the appropriate scope tag.  
12. For **Assignments**, assign to **SEB-Level1-Devices** group.  
13. Select **Next** to review the settings. Then choose **Create**.  

### Level 2 - Enterprise enhanced security for macOS

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Devices** > **macOS** > **Manage devices** > **Configuration** > **Create** > **New Policy**.  
3. Select **macOS** for platform and **Settings catalog** for profile type.  
4. Select **Create**.
5. On the **Basics** tab:  
   - **Name:** Level 2 - Enterprise enhanced security - macOS Settings Catalog  
   - **Description:** Enhanced security with extension blocking and privacy controls.  
6. Select **Next**.  
7. On **Configuration settings**, select **+ Add settings**.
8. From the **Settings picker**, search for **Microsoft Edge** and select it.
9. Select the following settings:

| Configuration Area | Category | Setting |
|--------------------|-----------|----------|
| Core Security | Microsoft Edge | Configure Microsoft Defender SmartScreen:<br>Enabled |
|  | Microsoft Edge | Configure Microsoft Defender SmartScreen<br>to block potentially unwanted apps:<br>Enabled |
|  | Microsoft Edge | Configure Automatic HTTPS:<br>Enabled |
|  | Microsoft Edge | Default pop-up window setting:<br>Do not allow popups (2) |
|  | Microsoft Edge | Block third party cookies:<br>Enabled |
| Enhanced Security | Microsoft Edge | Prevent bypassing Microsoft Defender<br>SmartScreen prompts for sites:<br>Enabled |
|  | Microsoft Edge | Prevent bypassing of Microsoft Defender<br>SmartScreen warnings about downloads:<br>Enabled |
|  | Microsoft Edge | Enhance the security state in Microsoft Edge:<br>Strict |
|  | Microsoft Edge | Configure InPrivate mode availability:<br>Disabled (1) |
|  | Microsoft Edge | Enable Guest mode in browser:<br>Disabled |
| Network Security | Microsoft Edge | Control the mode of DNS-over-HTTPS:<br>Enable without fallback |
|  | Microsoft Edge | DNS interception checks enabled:<br>Enabled |
|  | Microsoft Edge | Allow QUIC protocol:<br>Disabled |
| Privacy & Tracking | Microsoft Edge | Block tracking of users' web-browsing<br>activity:<br>Strict (3) |
|  | Microsoft Edge | Enable network prediction:<br>Don't predict (2) |
|  | Microsoft Edge | Enable search suggestions:<br>Disabled |
|  | Microsoft Edge | Send required and optional diagnostic data:<br>Off (0) |
|  | Microsoft Edge | Configure Do Not Track:<br>Enabled |
| Privacy & Data Controls | Microsoft Edge | Continue running background apps after<br>Microsoft Edge closes:<br>Disabled |
|  | Microsoft Edge | Disable synchronization of data:<br>Enabled |
|  | Microsoft Edge | Clear browsing data when Microsoft Edge closes:<br>Enabled |
|  | Microsoft Edge | Enable Microsoft Bing trending suggestions:<br>Disabled |
|  | Microsoft Edge | Allow user feedback:<br>Disabled |
| Content Settings | Microsoft Edge | Default geolocation setting:<br>Don't allow any site to track location (2) |
|  | Microsoft Edge | Default sensors setting:<br>Don't allow any site to access sensors (2) |
|  | Microsoft Edge | Default notification setting:<br>Don't allow notifications (2) |
|  | Microsoft Edge | Default media stream setting:<br>Don't allow any site to request access (2) |
| Content Security | Microsoft Edge | Block insecure content on specified sites:<br>["*"] |
|  | Microsoft Edge | Enable site isolation for every site:<br>Enabled |
| Password Management | Microsoft Edge | Enable saving passwords to the password<br>manager:<br>Disabled |
|  | Microsoft Edge | Enable AutoFill for addresses:<br>Disabled |
|  | Microsoft Edge | Enable AutoFill for credit cards:<br>Disabled |
|  | Microsoft Edge | Biometric authentication for local data<br>storage reauth:<br>Disabled |
| Import Controls | Microsoft Edge | Allow importing of autofill form data:<br>Disabled |
|  | Microsoft Edge | Allow importing of saved passwords:<br>Disabled |
|  | Microsoft Edge | Allow importing of browsing history:<br>Disabled |
|  | Microsoft Edge | Allow importing of payment info:<br>Disabled |
| Download Security | Microsoft Edge | Set download directory:<br>Prompt for location (1) |
|  | Microsoft Edge | Allow download restrictions:<br>Block dangerous downloads (1) |
| Browser Features | Microsoft Edge | Allow users to access the games menu:<br>Disabled |
|  | Microsoft Edge | Show Collections menu entry:<br>Disabled |
| Browser Experience | Microsoft Edge | Configure the home page URL:<br>https://portal.office.com |
|  | Microsoft Edge | Show Home button on toolbar:<br>Enabled |
|  | Microsoft Edge | Hide the First-run experience:<br>Enabled |
|  | Microsoft Edge | Enable browser sign-in:<br>Force users to sign in (2) |
| Search Engine | Microsoft Edge | Enable the default search provider:<br>Enabled |
|  | Microsoft Edge | Default search provider name:<br>Microsoft Bing |
|  | Microsoft Edge | Default search provider search URL:<br>https://www.bing.com/search?q={searchTerms} |
| AI & Copilot Controls | Microsoft Edge | Configure Copilot page context:<br>Copilot can't use page content (1) |
|  | Microsoft Edge | Show Compose on websites:<br>Disabled |
| Extension & Developer Controls | Microsoft Edge | Control which extensions can't be installed:<br>["*"] |
|  | Microsoft Edge | Control where developer tools can be used:<br>Disallowed (2) |
|  | Microsoft Edge | Block external extensions from being installed:<br>Enabled |
| API & Hardware Access | Microsoft Edge | Control use of the WebUSB API:<br>Do not allow (2) |
|  | Microsoft Edge | Control use of the WebHID API:<br>Do not allow (2) |
|  | Microsoft Edge | Control use of the Web Bluetooth API:<br>Do not allow (2) |
|  | Microsoft Edge | Control use of the Serial API:<br>Do not allow (2) |
| Certificate Security | Microsoft Edge | Minimum SSL version enabled:<br>TLS 1.2 |
|  | Microsoft Edge | Require online OCSP/CRL checks for local<br>trust anchors:<br>Enabled |

10. Select **Next**.  
11. For **Scope tags**, select the appropriate scope tag.  
12. For **Assignments**, assign to **SEB-Level2-Devices** group.  
13. Select **Next** to review the settings. Then choose **Create**.  

### Level 3 - Enterprise high security for macOS

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Devices** > **macOS** > **Manage devices** > **Configuration** > **Create** > **New Policy**.  
3. Select **macOS** for platform and **Settings catalog** for profile type.  
4. Select **Create**.
5. On the **Basics** tab:  
   - **Name:** Level 3 - Enterprise high security - macOS Settings Catalog  
   - **Description:** High security with URL filtering and maximum restrictions.  
6. Select **Next**.  
7. On **Configuration settings**, select **+ Add settings**.
8. From the **Settings picker**, search for **Microsoft Edge** and select it.
9. Select the following settings:

| Configuration Area | Category | Setting |
|--------------------|-----------|----------|
| Core Security | Microsoft Edge | Configure Microsoft Defender SmartScreen:<br>Enabled |
|  | Microsoft Edge | Configure Microsoft Defender SmartScreen<br>to block potentially unwanted apps:<br>Enabled |
|  | Microsoft Edge | Configure Automatic HTTPS:<br>Enabled |
|  | Microsoft Edge | Default pop-up window setting:<br>Do not allow popups (2) |
|  | Microsoft Edge | Block third party cookies:<br>Enabled |
| Enhanced Security | Microsoft Edge | Prevent bypassing Microsoft Defender<br>SmartScreen prompts for sites:<br>Enabled |
|  | Microsoft Edge | Prevent bypassing of Microsoft Defender<br>SmartScreen warnings about downloads:<br>Enabled |
|  | Microsoft Edge | Enhance the security state in Microsoft Edge:<br>Strict |
| InPrivate & Guest Mode | Microsoft Edge | Configure InPrivate mode availability:<br>InPrivate mode forced (2) |
|  | Microsoft Edge | Enable Guest mode in browser:<br>Disabled |
| Network Security | Microsoft Edge | Control the mode of DNS-over-HTTPS:<br>Enable without fallback |
|  | Microsoft Edge | DNS interception checks enabled:<br>Enabled |
|  | Microsoft Edge | Allow QUIC protocol:<br>Disabled |
| URL Filtering | Microsoft Edge | Define a list of allowed URLs:<br>["*.company.com","*.microsoft.com","*.office.com","login.microsoftonline.com"] |
|  | Microsoft Edge | Block access to a list of URLs:<br>["*"] |
|  | Microsoft Edge | Sites not allowed to load images:<br>["*"] |
| Privacy & Tracking | Microsoft Edge | Block tracking of users' web-browsing<br>activity:<br>Strict (3) |
|  | Microsoft Edge | Enable network prediction:<br>Don't predict (2) |
|  | Microsoft Edge | Enable search suggestions:<br>Disabled |
|  | Microsoft Edge | Send required and optional diagnostic data:<br>Off (0) |
|  | Microsoft Edge | Configure Do Not Track:<br>Enabled |
| Privacy & Data Controls | Microsoft Edge | Continue running background apps after<br>Microsoft Edge closes:<br>Disabled |
|  | Microsoft Edge | Disable synchronization of data:<br>Enabled |
|  | Microsoft Edge | Clear browsing data when Microsoft Edge closes:<br>Enabled |
|  | Microsoft Edge | Enable Microsoft Bing trending suggestions:<br>Disabled |
|  | Microsoft Edge | Allow user feedback:<br>Disabled |
| Content Settings | Microsoft Edge | Default geolocation setting:<br>Don't allow any site to track location (2) |
|  | Microsoft Edge | Default sensors setting:<br>Don't allow any site to access sensors (2) |
|  | Microsoft Edge | Default notification setting:<br>Don't allow notifications (2) |
|  | Microsoft Edge | Default media stream setting:<br>Don't allow any site to request access (2) |
| Content Security | Microsoft Edge | Block insecure content on specified sites:<br>["*"] |
|  | Microsoft Edge | Enable site isolation for every site:<br>Enabled |
| Clipboard Control | Microsoft Edge | Allow clipboard use on specific sites:<br>["*.company.com"] |
|  | Microsoft Edge | Block clipboard use on specific sites:<br>["*"] |
| Password Management | Microsoft Edge | Enable saving passwords to the password<br>manager:<br>Disabled |
|  | Microsoft Edge | Enable AutoFill for addresses:<br>Disabled |
|  | Microsoft Edge | Enable AutoFill for credit cards:<br>Disabled |
|  | Microsoft Edge | Biometric authentication for local data<br>storage reauth:<br>Disabled |
| Password & Credential Lockdown | Microsoft Edge | Allow password reveal button:<br>Disabled |
|  | Microsoft Edge | Enable Password Monitor:<br>Disabled |
| Import Controls | Microsoft Edge | Allow importing of autofill form data:<br>Disabled |
|  | Microsoft Edge | Allow importing of saved passwords:<br>Disabled |
|  | Microsoft Edge | Allow importing of browsing history:<br>Disabled |
|  | Microsoft Edge | Allow importing of payment info:<br>Disabled |
| Download Security | Microsoft Edge | Set download directory:<br>Prompt for location (1) |
|  | Microsoft Edge | Allow download restrictions:<br>Block all downloads (3) |
|  | Microsoft Edge | Prompt for download location:<br>Enabled |
| Maximum Download Security | Microsoft Edge | Allow download restrictions:<br>Block all downloads (3) |
| Printing | Microsoft Edge | Enable printing:<br>Disabled |
|  | Microsoft Edge | Print Headers and Footers:<br>Disabled |
|  | Microsoft Edge | Enable print preview:<br>Disabled |
| Data Protection | Microsoft Edge | Browsing Data Lifetime Settings:<br>[{"data_types": ["browsing_history", "download_history", "cookies_and_other_site_data", "cached_images_and_files"], "time_to_live_in_hours": 24}] |
|  | Microsoft Edge | Clear cached images and files on exit:<br>Enabled |
|  | Microsoft Edge | Clear browsing data when Microsoft Edge closes:<br>Enabled |
| Browser Features | Microsoft Edge | Allow users to access the games menu:<br>Disabled |
|  | Microsoft Edge | Show Collections menu entry:<br>Disabled |
| Browser Features Lockdown | Microsoft Edge | Allow sidebar in Microsoft Edge:<br>Disabled |
|  | Microsoft Edge | Enable Microsoft Search in sidebar:<br>Disabled |
|  | Microsoft Edge | Enable Drop feature:<br>Disabled |
|  | Microsoft Edge | Enable Microsoft Wallet payment feature:<br>Disabled |
| Browser Experience | Microsoft Edge | Configure the home page URL:<br>https://portal.office.com |
|  | Microsoft Edge | Show Home button on toolbar:<br>Enabled |
|  | Microsoft Edge | Hide the First-run experience:<br>Enabled |
|  | Microsoft Edge | Enable browser sign-in:<br>Force users to sign in (2) |
| Search Engine | Microsoft Edge | Enable the default search provider:<br>Enabled |
|  | Microsoft Edge | Default search provider name:<br>Microsoft Bing |
|  | Microsoft Edge | Default search provider search URL:<br>https://www.bing.com/search?q={searchTerms} |
| AI & Copilot Restrictions | Microsoft Edge | Configure Copilot:<br>Disabled |
|  | Microsoft Edge | Show Compose on websites:<br>Disabled |
|  | Microsoft Edge | Allow Image Creator in Microsoft Edge:<br>Disabled |
| Sync Restrictions | Microsoft Edge | Sync Types Disabled:<br>["favorites","settings","passwords","addresses","collections","tabs","extensions","history"] |
| Extension & Developer Controls | Microsoft Edge | Control which extensions can't be installed:<br>["*"] |
|  | Microsoft Edge | Control where developer tools can be used:<br>Disallowed (2) |
|  | Microsoft Edge | Block external extensions from being installed:<br>Enabled |
| API & Hardware Access | Microsoft Edge | Control use of the WebUSB API:<br>Do not allow (2) |
|  | Microsoft Edge | Control use of the WebHID API:<br>Do not allow (2) |
|  | Microsoft Edge | Control use of the Web Bluetooth API:<br>Do not allow (2) |
|  | Microsoft Edge | Control use of the Serial API:<br>Do not allow (2) |
| Certificate Enforcement | Microsoft Edge | Minimum SSL version enabled:<br>TLS 1.3 |
|  | Microsoft Edge | Require online OCSP/CRL checks for local<br>trust anchors:<br>Enabled |
|  | Microsoft Edge | Allow proceeding from the SSL warning page:<br>Disabled |

10. Select **Next**.  
11. For **Scope tags**, select the appropriate scope tag.  
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
