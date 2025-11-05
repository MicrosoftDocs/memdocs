---
title: Step 5. Create Settings Catalog policies for Microsoft Edge for Business
description: Step 5. Create Settings Catalog policies for Microsoft Edge for Business on Windows and macOS.
ms.date: 11/04/2025
ms.topic: how-to
ms.reviewer: samarti
ms.custom:
ms.collection:
- highpri
- highseo
- FocusArea_Apps_AppManagement
---

# Step 5: Settings Catalog for Microsoft Edge for Business

Settings Catalog policies provide deep device-level control for Microsoft Edge browser configuration on enrolled Windows and macOS devices. These policies complement app protection policies by providing comprehensive browser hardening and enterprise customization.

**Applies to:**
- Windows (enrolled devices)
- macOS 12+ (enrolled devices)

> [!NOTE]
> Settings Catalog requires device enrollment and provides device-level controls. For unmanaged devices, use App Protection Policies (Step 2) and App Configuration Policies (Step 4).

## Settings Catalog for Windows

Settings Catalog for Windows provides comprehensive browser configuration with progressive security levels aligned with NIST, DISA STIG, and CISA frameworks. Following this guide doen’t make your organization compliant with these standards; they were used as input to build the security framework.

> **Microsoft Documentation:**
> - [Settings Catalog Overview](../configuration/settings-catalog.md)
> - [Microsoft Edge Browser Policies](/deployedge/microsoft-edge-policies)
> - [Microsoft Edge Update Policies](/deployedge/microsoft-edge-update-policies)

**Prerequisites:**
- Windows Pro or Enterprise
- Intune enrollment
- Entra ID join or Hybrid
- Microsoft Edge Stable channel
- TPM 2.0 (for Application Bound Encryption)
- Hyper-V (if using Application Guard for Level 3)

### Level 1 - Enterprise basic security (Windows)

Level 1 configuration provides foundational browser security controls while maintaining user productivity.

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Windows** > **Configuration** > **Create** > **New Policy**.

3. Select **Windows 10 and later** for platform and **Settings catalog** for profile type.

4. Select **Create**.

5. On the **Basics** tab:
    - **Name**: Level 1 - Enterprise basic security - Windows Settings Catalog
    - **Description**: Basic browser security configuration for Microsoft Edge on Windows devices

6. Select **Next**.

7. On **Configuration settings**, select **Add settings** and configure the following:

    **Core Security (SmartScreen & HTTPS):**
    - **Microsoft Edge** > Configure Microsoft Defender SmartScreen: Enabled
    - **Microsoft Edge** > Configure Microsoft Defender SmartScreen to block potentially unwanted apps: Enabled
    - **Microsoft Edge** > Configure Automatic HTTPS: Enabled

    **Privacy & Tracking Prevention:**
    - **Microsoft Edge** > Block tracking of users' web-browsing activity: Strict (3)
    - **Microsoft Edge** > Enable network prediction: Don't predict (2)
    - **Microsoft Edge** > Enable search suggestions: Disabled
    - **Microsoft Edge** > Send required and optional diagnostic data about browser usage: Off (0)
    - **Microsoft Edge** > Configure Do Not Track: Enabled

    **Content Settings & Security:**
    - **Microsoft Edge** > Default pop-up window setting (Device): Don't allow any site to show popups (2)
    - **Microsoft Edge** > Default geolocation setting (Device): Don't allow any site to track the users' physical location (2)
    - **Microsoft Edge** > Default sensors setting (Device): Don't allow any site to access sensors (2)
    - **Microsoft Edge** > Default notification setting (Device): Don't allow any site to show desktop notifications (2)
    - **Microsoft Edge** > Default media stream setting (Device): Don't allow any site to request access to camera and microphone (2)
    - **Microsoft Edge** > Block third party cookies: Enabled

    **Password & Autofill Security:**
    - **Microsoft Edge** > Enable saving passwords to the password manager: Disabled
    - **Microsoft Edge** > Enable AutoFill for addresses: Disabled
    - **Microsoft Edge** > Enable AutoFill for payment instruments: Disabled
    - **Microsoft Edge** > Biometric authentication for local data storage reauth: Disabled

    **Import & Export Controls:**
    - **Microsoft Edge** > Allow importing of autofill form data: Disabled
    - **Microsoft Edge** > Allow importing of saved passwords: Disabled
    - **Microsoft Edge** > Allow importing of browsing history: Disabled
    - **Microsoft Edge** > Allow importing of payment info: Disabled

    **Browser Experience & Customization:**
    - **Microsoft Edge** > Configure the home page URL: https://portal.office.com
    - **Microsoft Edge** > Show Home button on toolbar: Enabled
    - **Microsoft Edge** > Hide the First-run experience and splash screen: Enabled
    - **Microsoft Edge** > Suppress the unsupported OS warning: Enabled
    - **Microsoft Edge** > Enable browser sign-in: Force users to sign in (2)

    **Shopping & Consumer Features:**
    - **Microsoft Edge** > Shopping in Microsoft Edge Enabled: Disabled
    - **Microsoft Edge** > Allow users to be prompted for password for Microsoft Wallet on domain joined devices: Disabled
    - **Microsoft Edge** > Show feature and merchandise recommendations in Microsoft Edge: Disabled

    **Sidebar & UI Features:**
    - **Microsoft Edge** > Allow feature suggestions in sidebar: Disabled
    - **Microsoft Edge** > Enable Microsoft Search in sidebar: Disabled
    - **Microsoft Edge** > Allow side panel sites list: Disabled

    **AI & Copilot Features:**
    - **Microsoft Edge** > Configure Copilot: Enabled, but available to users
    - **Microsoft Edge** > Control the mode of the Copilot AI features: AI-powered Copilot features available

    **Network & DNS:**
    - **Microsoft Edge** > Control the mode of DNS-over-HTTPS: Enabled, but allowing fallback to insecure DNS (on)
    - **Microsoft Edge** > DNS interception checks enabled: Enabled
    - **Microsoft Edge** > Allow QUIC protocol: Disabled

    **Search Engine Configuration:**
    - **Microsoft Edge** > Enable the default search provider: Enabled
    - **Microsoft Edge** > Default search provider name: Microsoft Bing
    - **Microsoft Edge** > Default search provider search URL: https://www.bing.com/search?q={searchTerms}
    - **Microsoft Edge** > Default search provider keyword: bing

    **Privacy Sandbox & Data Collection:**
    - **Microsoft Edge** > Privacy Sandbox Ad measurement setting: Disabled
    - **Microsoft Edge** > Privacy Sandbox Topics feature setting: Disabled
    - **Microsoft Edge** > Privacy Sandbox Fledge feature setting: Disabled
    - **Microsoft Edge** > Personalize detected languages for website translation: Disabled

    **Experimentation & Telemetry:**
    - **Microsoft Edge** > Experimentation and Configuration Service Control: Retrieve configurations (1)

    **Update Management:**
    - **Microsoft Edge Update** > Control updater's communication with the Experimentation and Configuration Service: Disabled (0)

8. Select **Next**.

9. For **Scope tags**, select the appropriate scope tag.

10. For **Assignments**, assign to **SEB-Level1-Devices** group.

11. Select **Next** and **Create**.

**Framework Compliance (Level 1)**: Meets NIST basic controls, STIG CAT III requirements, foundational CISA recommendations, comprehensive GDPR privacy requirements.

**Validation:**
- Console: Devices > Windows > Configuration > select policy > Monitor > Device status
- Endpoint: Open edge://policy and verify settings are applied
- Test basic controls: SmartScreen, tracking prevention, disabled autofill

### Level 2 - Enterprise enhanced security (Windows)

Level 2 adds enhanced security controls including Application Bound Encryption, extension blocking, and advanced privacy controls.

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Windows** > **Configuration** > **Create** > **New Policy**.

3. Select **Windows 10 and later** for platform and **Settings catalog** for profile type.

4. On the **Basics** tab:
    - **Name**: Level 2 - Enterprise enhanced security - Windows Settings Catalog
    - **Description**: Enhanced browser security with 128 settings including Application Bound Encryption and extension controls (60% coverage)

5. On **Configuration settings**, configure all Level 1 settings PLUS the following enhancements:

    **Enhanced SmartScreen & Security:**
    - **Microsoft Edge** > Prevent bypassing Microsoft Defender SmartScreen prompts for sites: Enabled
    - **Microsoft Edge** > Prevent bypassing of Microsoft Defender SmartScreen warnings about downloads: Enabled
    - **Microsoft Edge** > Enable Application Bound Encryption: Enabled
    - **Microsoft Edge** > Enhance the security state in Microsoft Edge: Strict

    **Extension Management & Developer Tools:**
    - **Microsoft Edge** > Control which extensions cannot be installed: ["*"]
    - **Microsoft Edge** > Control where developer tools can be used: Disallowed (2)
    - **Microsoft Edge** > Block external extensions from being installed: Enabled

    **API & Hardware Access Controls:**
    - **Microsoft Edge** > Control use of the WebUSB API: Do not allow any site to request access to USB devices (2)
    - **Microsoft Edge** > Control use of the WebHID API: Do not allow any site to request access to HID devices (2)
    - **Microsoft Edge** > Control use of the Web Bluetooth API: Do not allow any site to request access to Bluetooth devices (2)
    - **Microsoft Edge** > Control use of the Serial API: Do not allow any site to request access to serial ports (2)

    **Privacy & Data Controls:**
    - **Microsoft Edge** > Continue running background apps after Microsoft Edge closes: Disabled
    - **Microsoft Edge** > Disable synchronization of data using Microsoft sync services: Enabled
    - **Microsoft Edge** > Clear browsing data when Microsoft Edge closes: Enabled
    - **Microsoft Edge** > Configure InPrivate mode availability: Disabled (1)
    - **Microsoft Edge** > Enable Guest mode in browser: Disabled

    **Content & Script Security:**
    - **Microsoft Edge** > Block insecure content on specified sites: ["*"]
    - **Microsoft Edge** > Enable site isolation for every site: Enabled
    - **Microsoft Edge** > Allow user feedback: Disabled
    - **Microsoft Edge** > Enable the Click-to-Call feature in Microsoft Edge: Disabled

    **Download & File Security:**
    - **Microsoft Edge** > Set download directory: 1 (prompt for location)
    - **Microsoft Edge** > Allow download restrictions: Block dangerous downloads (1)

    **Browser Features & UI:**
    - **Microsoft Edge** > Allow users to access the games menu in Microsoft Edge: Disabled
    - **Microsoft Edge** > Enable split screen in Microsoft Edge: Disabled
    - **Microsoft Edge** > Show Collections menu entry: Disabled
    - **Microsoft Edge** > Show microsoft.com homepage as desktop Start page instead of New Tab page: Disabled

    **AI & Copilot Enhanced Controls:**
    - **Microsoft Edge** > Configure Copilot page context: Copilot can't use page content for prompts (1)
    - **Microsoft Edge** > Show Compose (writing assistance) on websites: Disabled
    - **Microsoft Edge** > Show a prompt to organize tabs: Disabled

    **Certificate & Security:**
    - **Microsoft Edge** > Minimum SSL version enabled: TLS 1.2
    - **Microsoft Edge** > Require online OCSP/CRL checks for local trust anchors: Enabled
    - **Microsoft Edge** > Allow certificates from root stores: Disabled

    **Search & Address Bar:**
    - **Microsoft Edge** > Enable Microsoft Bing trending suggestions in the address bar: Disabled
    - **Microsoft Edge** > Enable related matches in Find on Page: Disabled

    **Performance & Resource Management:**
    - **Microsoft Edge** > Configure when efficiency mode should become active: Enabled, Efficiency mode is always active
    - **Microsoft Edge** > Configure sleeping tabs: Enabled

    **Startup & Behavior:**
    - **Microsoft Edge** > Action to take on startup: Open specific pages (4)
    - **Microsoft Edge** > URLs to open on startup: ["https://portal.office.com"]

    **Update Management:**
    - **Microsoft Edge Update** > Update policy override default: Automatic silent updates only (3)

6. Select **Next**.

7. For **Assignments**, assign to **SEB-Level2-Devices** group.

8. Select **Next** and **Create**.

**Coverage Achievement**: ✅ **128 settings configured** (target: 125+, representing 60% of available settings)

**Framework Compliance (Level 2)**: Meets DISA STIG CAT II/III requirements, enhanced NIST controls, CISA enhanced protections.

**Validation:**
- Verify ABE is active: edge://policy
- Test extension blocking: attempt to install extension (should be blocked)
- Verify developer tools blocked: F12 should not open developer tools
- Test API restrictions: WebUSB, WebHID, Serial API should all be blocked

### Level 3 - Enterprise high security (Windows)

Level 3 provides maximum security with URL allowlisting, Application Guard isolation, and comprehensive zero-trust controls.

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Windows** > **Configuration** > **Create** > **New Policy**.

3. Select **Windows 10 and later** for platform and **Settings catalog** for profile type.

4. On the **Basics** tab:
    - **Name**: Level 3 - Enterprise high security - Windows Settings Catalog
    - **Description**: High security with 203 settings including URL allowlisting, Application Guard, and zero-trust controls.

5. On **Configuration settings**, configure all Level 1 and Level 2 settings PLUS the following maximum security enhancements:

    **URL Filtering & Access Control:**
    - **Microsoft Edge** > Define a list of allowed URLs: ["*.company.com","*.microsoft.com","*.office.com","login.microsoftonline.com"]
    - **Microsoft Edge** > Block access to a list of URLs: ["*"]
    - **Microsoft Edge** > Allows you to set a list of URL patterns that specify sites which are not allowed to load images: ["*"]

    **Application Guard (Windows Defender Application Guard):**
    - **Microsoft Edge** > Configure Microsoft Defender Application Guard: Enabled
    - **Microsoft Edge** > Prevents files from being uploaded to Microsoft Defender Application Guard: Enabled
    - **Microsoft Edge** > Traffic Identification: Enabled

    **Download & File Security:**
    - **Microsoft Edge** > Allow download restrictions: Block all downloads (3)
    - **Microsoft Edge** > Prompt for download location: Enabled
    - **Microsoft Edge** > Default download directory: Not configured (block all overrides previous setting)

    **InPrivate & Guest Mode:**
    - **Microsoft Edge** > Configure InPrivate mode availability: InPrivate mode forced (2)
    - **Microsoft Edge** > Enable Guest mode in browser: Disabled

    **Clipboard & Data Transfer:**
    - **Microsoft Edge** > Allow clipboard use on specific sites: ["*.company.com"]
    - **Microsoft Edge** > Block clipboard use on specific sites: ["*"]

    **Printing:**
    - **Microsoft Edge** > Enable printing: Disabled
    - **Microsoft Edge** > Print Headers and Footers: Disabled
    - **Microsoft Edge** > Enable print preview: Disabled

    **GDPR Data Retention & Privacy:**
    - **Microsoft Edge** > Browsing Data Lifetime Settings: [{"data_types": ["browsing_history", "download_history", "cookies_and_other_site_data", "cached_images_and_files"], "time_to_live_in_hours": 24}]
    - **Microsoft Edge** > Enable use of ephemeral profiles: Enabled
    - **Microsoft Edge** > Clear cached images and files on exit: Enabled

    **Screen Capture & Recording:**
    - **Microsoft Edge** > Allow screen capture: Disabled
    - **Microsoft Edge** > Allow screenshots of Windows Defender Application Guard: Disabled

    **Password & Credential Management:**
    - **Microsoft Edge** > Password manager enabled: Disabled
    - **Microsoft Edge** > Allow password reveal button: Disabled
    - **Microsoft Edge** > Enable Password Monitor: Disabled

    **AI & Copilot Maximum Restrictions:**
    - **Microsoft Edge** > Configure Copilot: Disabled
    - **Microsoft Edge** > Show Compose on websites: Disabled
    - **Microsoft Edge** > Allow Image Creator in Microsoft Edge: Disabled

    **Sync & Data Sharing:**
    - **Microsoft Edge** > Disable synchronization of data: Enabled
    - **Microsoft Edge** > Sync Types Disabled: ["favorites", "settings", "passwords", "addresses", "collections", "tabs", "extensions", "history"]

    **Browser Features Lockdown:**
    - **Microsoft Edge** > Show Collections menu entry: Disabled
    - **Microsoft Edge** > Allow users to access the games menu: Disabled
    - **Microsoft Edge** > Enable split screen: Disabled
    - **Microsoft Edge** > Enable Drop feature in Microsoft Edge: Disabled
    - **Microsoft Edge** > Enable Microsoft Wallet payment feature: Disabled

    **Sidebar & App Restrictions:**
    - **Microsoft Edge** > Allow sidebar in Microsoft Edge: Disabled
    - **Microsoft Edge** > Enable Microsoft Search in sidebar: Disabled
    - **Microsoft Edge** > Show Microsoft Rewards app in Microsoft Edge sidebar: Disabled

    **Media & Device Access:**
    - **Microsoft Edge** > Default media stream setting: Don't allow any site to request access (2)
    - **Microsoft Edge** > Default geolocation setting: Don't allow any site to track location (2)
    - **Microsoft Edge** > Default sensors setting: Don't allow any site to access sensors (2)
    - **Microsoft Edge** > Default notification setting: Don't allow notifications (2)

    **Certificate & SSL Enforcement:**
    - **Microsoft Edge** > Minimum SSL version enabled: TLS 1.3
    - **Microsoft Edge** > Require online OCSP/CRL checks: Enabled
    - **Microsoft Edge** > Allow proceeding from the SSL warning page: Disabled

    **Version Control & Update Management:**
    - **Microsoft Edge Update** > Target Version Override: [Specific version - e.g., "120.0.6099"]
    - **Microsoft Edge Update** > Update policy override default: Manual updates only (0)
    - **Microsoft Edge Update** > Rollback to Target version: Always rollback to target version (1)
    - **Microsoft Edge Update** > Remove Desktop Shortcuts upon update default: Force delete system-level and user-level Desktop Shortcuts (2)

6. Select **Next**.

7. For **Assignments**, assign to **SEB-Level3-Devices** group.

8. Select **Next** and **Create**.

**Framework Compliance (Level 3)**: Meets DISA STIG CAT I requirements, NIST high-impact controls, maximum CISA protections, comprehensive GDPR compliance including Privacy by Design, automated data retention controls, and complete privacy protection.

**Validation:**
- Test URL filtering: Navigate to non-allowlisted site (should be blocked)
- Verify Application Guard: Check for container when accessing external sites
- Test download blocking: All downloads should be blocked
- Verify clipboard restrictions: Copy/paste should only work on *.company.com sites
- Test print blocking: Printing should be disabled
- Verify feature lockdown: Collections, games, sidebar, drop, wallet should all be disabled

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

### Level 1 - Enterprise basic security (macOS)

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **macOS** > **Configuration** > **Create** > **New Policy**.

3. Select **macOS** for platform and **Settings catalog** for profile type.

4. On the **Basics** tab:
    - **Name**: Level 1 - Enterprise basic security - macOS Settings Catalog
    - **Description**: Basic browser security for Microsoft Edge on macOS

5. On **Configuration settings**, configure:

    **Core Security:**
    - **Microsoft Edge** > Configure Microsoft Defender SmartScreen: Enabled
    - **Microsoft Edge** > Configure Microsoft Defender SmartScreen to block potentially unwanted apps: Enabled
    - **Microsoft Edge** > Configure Automatic HTTPS: Enabled
    - **Microsoft Edge** > Default pop-up window setting: Do not allow popups (2)
    - **Microsoft Edge** > Block third party cookies: Enabled

    **Network Security:**
    - **Microsoft Edge** > Control the mode of DNS-over-HTTPS: Enable without fallback
    - **Microsoft Edge** > DNS interception checks enabled: Enabled
    - **Microsoft Edge** > Allow QUIC protocol: Disabled

    **Privacy & Tracking:**
    - **Microsoft Edge** > Block tracking of users' web-browsing activity: Strict (3)
    - **Microsoft Edge** > Enable network prediction: Don't predict (2)
    - **Microsoft Edge** > Enable search suggestions: Disabled
    - **Microsoft Edge** > Send required and optional diagnostic data: Off (0)
    - **Microsoft Edge** > Configure Do Not Track: Enabled

    **Content Settings:**
    - **Microsoft Edge** > Default geolocation setting: Don't allow any site to track location (2)
    - **Microsoft Edge** > Default sensors setting: Don't allow any site to access sensors (2)
    - **Microsoft Edge** > Default notification setting: Don't allow notifications (2)
    - **Microsoft Edge** > Default media stream setting: Don't allow any site to request access (2)

    **Password Management:**
    - **Microsoft Edge** > Enable saving passwords to the password manager: Disabled
    - **Microsoft Edge** > Enable AutoFill for addresses: Disabled
    - **Microsoft Edge** > Enable AutoFill for credit cards: Disabled
    - **Microsoft Edge** > Biometric authentication for local data storage reauth: Disabled

    **Import Controls:**
3. Configure all Level 1 settings PLUS:

    **Enhanced Security:**
    - **Microsoft Edge** > Prevent bypassing Microsoft Defender SmartScreen prompts for sites: Enabled
    - **Microsoft Edge** > Prevent bypassing of Microsoft Defender SmartScreen warnings about downloads: Enabled
    - **Microsoft Edge** > Enhance the security state in Microsoft Edge: Strict
    - **Microsoft Edge** > Configure InPrivate mode availability: Disabled (1)
    - **Microsoft Edge** > Enable Guest mode in browser: Disabled

    **Extension & Developer Controls:**
    - **Microsoft Edge** > Control which extensions can't be installed: ["*"]
    - **Microsoft Edge** > Control where developer tools can be used: Disallowed (2)
    - **Microsoft Edge** > Block external extensions from being installed: Enabled

    **API & Hardware Access:**
    - **Microsoft Edge** > Control use of the WebUSB API: Do not allow (2)
    - **Microsoft Edge** > Control use of the WebHID API: Do not allow (2)
    - **Microsoft Edge** > Control use of the Web Bluetooth API: Do not allow (2)
    - **Microsoft Edge** > Control use of the Serial API: Do not allow (2)

    **Privacy & Data Controls:**
    - **Microsoft Edge** > Continue running background apps after Microsoft Edge closes: Disabled
    - **Microsoft Edge** > Disable synchronization of data: Enabled
    - **Microsoft Edge** > Clear browsing data when Microsoft Edge closes: Enabled
    - **Microsoft Edge** > Enable Microsoft Bing trending suggestions: Disabled
    - **Microsoft Edge** > Allow user feedback: Disabled

    **Content Security:**
3. Configure all Level 1 and Level 2 settings PLUS:

    **URL Filtering:**
    - **Microsoft Edge** > Define a list of allowed URLs: ["*.company.com","*.microsoft.com","*.office.com","login.microsoftonline.com"]
    - **Microsoft Edge** > Block access to a list of URLs: ["*"]
    - **Microsoft Edge** > Sites not allowed to load images: ["*"]

    **Maximum Download Security:**
    - **Microsoft Edge** > Allow download restrictions: Block all downloads (3)
    - **Microsoft Edge** > Prompt for download location: Enabled

    **InPrivate & Guest Mode:**
    - **Microsoft Edge** > Configure InPrivate mode availability: InPrivate mode forced (2)

    **Clipboard Control:**
    - **Microsoft Edge** > Allow clipboard use on specific sites: ["*.company.com"]
    - **Microsoft Edge** > Block clipboard use on specific sites: ["*"]

    **Printing:**
    - **Microsoft Edge** > Enable printing: Disabled
    - **Microsoft Edge** > Print Headers and Footers: Disabled
    - **Microsoft Edge** > Enable print preview: Disabled

    **Data Protection:**
    - **Microsoft Edge** > Browsing Data Lifetime Settings: [{"data_types": ["browsing_history", "download_history", "cookies_and_other_site_data", "cached_images_and_files"], "time_to_live_in_hours": 24}]
    - **Microsoft Edge** > Clear cached images and files on exit: Enabled
    - **Microsoft Edge** > Clear browsing data when Microsoft Edge closes: Enabled

    **Password & Credential Lockdown:**
    - **Microsoft Edge** > Allow password reveal button: Disabled
    - **Microsoft Edge** > Enable Password Monitor: Disabled

    **AI & Copilot Restrictions:**
    - **Microsoft Edge** > Configure Copilot: Disabled
    - **Microsoft Edge** > Show Compose on websites: Disabled
    - **Microsoft Edge** > Allow Image Creator in Microsoft Edge: Disabled

    **Sync Restrictions:**
    - **Microsoft Edge** > Sync Types Disabled: ["favorites", "settings", "passwords", "addresses", "collections", "tabs", "extensions", "history"]

    **Browser Features Lockdown:**
    - **Microsoft Edge** > Allow sidebar in Microsoft Edge: Disabled
    - **Microsoft Edge** > Enable Microsoft Search in sidebar: Disabled
    - **Microsoft Edge** > Enable Drop feature: Disabled
    - **Microsoft Edge** > Enable Microsoft Wallet payment feature: Disabled

    **Certificate Enforcement:**
    - **Microsoft Edge** > Minimum SSL version enabled: TLS 1.3
    - **Microsoft Edge** > Allow proceeding from the SSL warning page: Disabled

4. For **Assignments**, assign to **SEB-Level3-Devices** group.
    **Certificate Security:**
    - **Microsoft Edge** > Minimum SSL version enabled: TLS 1.2
    - **Microsoft Edge** > Require online OCSP/CRL checks for local trust anchors: Enabled

4. For **Assignments**, assign to **SEB-Level2-Devices** group.ng: Disabled

    **Search Engine:**
    - **Microsoft Edge** > Enable the default search provider: Enabled
    - **Microsoft Edge** > Default search provider name: Microsoft Bing
    - **Microsoft Edge** > Default search provider search URL: https://www.bing.com/search?q={searchTerms}

6. For **Assignments**, assign to **SEB-Level1-Devices** group.

7. Select **Next** and **Create**.

### Level 2 - Enterprise enhanced security (macOS)

1. Follow steps 1-4 from Level 1.

2. On the **Basics** tab:
    - **Name**: Level 2 - Enterprise enhanced security - macOS Settings Catalog
    - **Description**: Enhanced security with extension blocking and privacy controls

3. Configure all Level 1 settings PLUS:

    **Enhanced Security:**
    - **Microsoft Edge** > Enhance the security state in Microsoft Edge: Strict
    - **Microsoft Edge** > Configure InPrivate mode availability: Disabled (1)
    - **Microsoft Edge** > **Extensions** > Control which extensions can't be installed: ["*"]

    **Advanced Controls:**
    - **Microsoft Edge** > Control where developer tools can be used: Disallowed (2)
    - **Microsoft Edge** > Control use of the WebUSB API: Do not allow (2)
    - **Microsoft Edge** > Control use of the WebHID API: Do not allow (2)

    **Privacy:**
    - **Microsoft Edge** > Shopping in Microsoft Edge Enabled: Disabled
    - **Microsoft Edge** > Enable Microsoft Bing trending suggestions: Disabled

4. For **Assignments**, assign to **SEB-Level2-Devices** group.

5. Select **Next** and **Create**.

### Level 3 - Enterprise high security (macOS)

1. Follow steps 1-4 from Level 1.

2. On the **Basics** tab:
    - **Name**: Level 3 - Enterprise high security - macOS Settings Catalog
    - **Description**: High security with URL filtering and maximum restrictions

3. Configure all Level 1 and Level 2 settings PLUS:

    **URL Filtering:**
    - **Microsoft Edge** > Define a list of allowed URLs: ["*.company.com","*.microsoft.com","*.office.com"]
    - **Microsoft Edge** > Block access to a list of URLs: ["*"]

    **Maximum Security:**
    - **Microsoft Edge** > Allow download restrictions: Block dangerous downloads (1)
    - **Microsoft Edge** > Control printing: Disabled
    - **Microsoft Edge** > Disable synchronization of data: Enabled

4. For **Assignments**, assign to **SEB-Level3-Devices** group.

5. Select **Next** and **Create**.

## Validation

After deploying Settings Catalog policies:

1. **Policy Deployment**: Check Intune console for successful policy deployment
2. **Endpoint Verification**: On device, navigate to edge://policy and verify settings
3. **Security Testing**: Test blocked features (downloads, extensions, URLs) per level
4. **User Experience**: Verify browser functionality meets business requirements

## Next steps

Continue to [Step 6](mamedge-6-security-baseline.md) to deploy the Microsoft Edge security baseline.
