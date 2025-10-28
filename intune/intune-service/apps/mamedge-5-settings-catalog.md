---
title: Step 5. Create Settings Catalog policies for Microsoft Edge for Business
description: Step 5. Create Settings Catalog policies for Microsoft Edge for Business on Windows and macOS.
ms.date: 10/28/2025
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

Settings Catalog for Windows provides comprehensive browser configuration with progressive security levels aligned with NIST, DISA STIG, and CISA frameworks.

> **Microsoft Documentation:**
> - [Settings Catalog Overview](../configuration/settings-catalog.md)
> - [Microsoft Edge Browser Policies](/deployedge/microsoft-edge-policies)
> - [Microsoft Edge Update Policies](/deployedge/microsoft-edge-update-policies)

**Prerequisites:**
- Windows 10/11 Pro or Enterprise
- Intune enrollment (Entra ID join or Hybrid)
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

    **Core Security:**
    - **Microsoft Edge** > **SmartScreen settings** > Configure Microsoft Defender SmartScreen: Enabled
    - **Microsoft Edge** > Configure Automatic HTTPS: Enabled
    - **Microsoft Edge** > **Content settings** > Default pop-up window setting: Don't allow any site to show popups (2)
    - **Microsoft Edge** > **Content settings** > Block third party cookies: Enabled

    **Privacy & Tracking:**
    - **Microsoft Edge** > Block tracking of users' web-browsing activity: Strict (3)
    - **Microsoft Edge** > Enable network prediction: Don't predict (2)
    - **Microsoft Edge** > Enable search suggestions: Disabled
    - **Microsoft Edge** > Send required and optional diagnostic data: Off (0)

    **Password & Autofill:**
    - **Microsoft Edge** > Enable saving passwords to the password manager: Disabled
    - **Microsoft Edge** > Enable AutoFill for addresses: Disabled
    - **Microsoft Edge** > Enable AutoFill for payment instruments: Disabled

    **Import Controls:**
    - **Microsoft Edge** > Allow importing of autofill form data: Disabled
    - **Microsoft Edge** > Allow importing of saved passwords: Disabled
    - **Microsoft Edge** > Allow importing of browsing history: Disabled

    **Browser Customization:**
    - **Microsoft Edge** > Configure the home page URL: https://portal.office.com
    - **Microsoft Edge** > Show Home button on toolbar: Enabled
    - **Microsoft Edge** > Hide the First-run experience: Enabled

8. Select **Next**.

9. For **Scope tags**, select the appropriate scope tag.

10. For **Assignments**, assign to **SEB-Level1-Devices** group.

11. Select **Next** and **Create**.

**Validation:**
- Console: Devices > Windows > Configuration > select policy > Monitor > Device status
- Endpoint: Open edge://policy and verify settings are applied

### Level 2 - Enterprise enhanced security (Windows)

Level 2 adds enhanced security controls including Application Bound Encryption and extension blocking.

1. Follow steps 1-6 from Level 1.

2. On the **Basics** tab:
    - **Name**: Level 2 - Enterprise enhanced security - Windows Settings Catalog
    - **Description**: Enhanced browser security with Application Bound Encryption and extension controls

3. On **Configuration settings**, configure all Level 1 settings PLUS:

    **Enhanced Security:**
    - **Microsoft Edge** > Configure Microsoft Defender SmartScreen to block potentially unwanted apps: Enabled
    - **Microsoft Edge** > Enable Application Bound Encryption: Enabled
    - **Microsoft Edge** > **Extensions** > Control which extensions can't be installed: ["*"]
    - **Microsoft Edge** > Configure InPrivate mode availability: Disabled (1)

    **Advanced Privacy:**
    - **Microsoft Edge** > Continue running background apps after Microsoft Edge closes: Disabled
    - **Microsoft Edge** > Disable synchronization of data: Enabled
    - **Microsoft Edge** > Clear browsing data when Microsoft Edge closes: Enabled

    **Content Security:**
    - **Microsoft Edge** > Block insecure content on specified sites: ["*"]
    - **Microsoft Edge** > Control use of the WebUSB API: Do not allow (2)
    - **Microsoft Edge** > Control use of the WebHID API: Do not allow (2)

    **Developer Tools:**
    - **Microsoft Edge** > Control where developer tools can be used: Disallowed (2)

4. For **Assignments**, assign to **SEB-Level2-Devices** group.

5. Select **Next** and **Create**.

**Validation:**
- Verify ABE is active: edge://policy
- Test extension blocking: attempt to install extension

### Level 3 - Enterprise high security (Windows)

Level 3 provides maximum security with URL allowlisting and Application Guard isolation.

1. Follow steps 1-6 from Level 1.

2. On the **Basics** tab:
    - **Name**: Level 3 - Enterprise high security - Windows Settings Catalog
    - **Description**: High security with URL allowlisting and Application Guard

3. On **Configuration settings**, configure all Level 1 and Level 2 settings PLUS:

    **URL Filtering:**
    - **Microsoft Edge** > **Content settings** > Define a list of allowed URLs: ["*.company.com","*.microsoft.com","*.office.com"]
    - **Microsoft Edge** > **Content settings** > Block access to a list of URLs: ["*"]

    **Application Guard:**
    - **Microsoft Edge** > Application Guard Traffic Identification: Enabled
    - **Microsoft Edge** > Prevents files from being uploaded while in Application Guard: Enabled

    **Maximum Security:**
    - **Microsoft Edge** > Allow download restrictions: Block all downloads (3)
    - **Microsoft Edge** > Enable site isolation for every site: Enabled
    - **Microsoft Edge** > Configure InPrivate mode availability: InPrivate mode forced (1)

    **Data Protection:**
    - **Microsoft Edge** > Allow clipboard use on specific sites: *.company.com
    - **Microsoft Edge** > Block clipboard use on specific sites: *
    - **Microsoft Edge** > Control printing: Disabled

    **GDPR Data Retention:**
    - **Microsoft Edge** > Browsing Data Lifetime Settings: [{"data_types": ["browsing_history", "download_history", "cookies_and_other_site_data"], "time_to_live_in_hours": 24}]
    - **Microsoft Edge** > Enable use of ephemeral profiles: Enabled

4. For **Assignments**, assign to **SEB-Level3-Devices** group.

5. Select **Next** and **Create**.

**Validation:**
- Test URL filtering: Navigate to nonallowlisted site (should be blocked)
- Verify Application Guard: Check for container when accessing external sites

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
    - **Microsoft Edge** > Configure Automatic HTTPS: Enabled
    - **Microsoft Edge** > Default pop-up window setting: Do not allow popups (2)

    **Network Security:**
    - **Microsoft Edge** > Control the mode of DNS-over-HTTPS: Enable without fallback
    - **Microsoft Edge** > DNS interception checks enabled: Enabled
    - **Microsoft Edge** > Allow QUIC protocol: Disabled

    **Privacy:**
    - **Microsoft Edge** > Block tracking of users' web-browsing activity: Strict (3)
    - **Microsoft Edge** > Enable network prediction: Don't predict (2)
    - **Microsoft Edge** > Enable search suggestions: Disabled

    **Password Management:**
    - **Microsoft Edge** > Enable saving passwords to the password manager: Disabled
    - **Microsoft Edge** > Enable AutoFill for addresses: Disabled
    - **Microsoft Edge** > Enable AutoFill for credit cards: Disabled

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
