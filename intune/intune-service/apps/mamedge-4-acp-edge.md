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
- Windows
- Android 6.0+
- iOS/iPadOS 15+

> [!NOTE]
> App configuration policies customize browser features and behavior. They complement app protection policies that focus on data protection.

## App configuration policies for Windows

Windows app configuration policies provide browser customization through managed app settings.

> **Microsoft Documentation:**
> - [Microsoft Edge Browser Policies](/deployedge/microsoft-edge-policies)
> - [Windows App Configuration Policies](app-configuration-policies-overview.md)
> - [Managed App Configuration for Windows](app-configuration-policies-managed-app.md)

**Prerequisites:**
- Windows 10/11
- Microsoft Edge installed
- Intune enrollment or MAM managed
- User Entra ID account

### Level 1 - Basic browser configuration (Windows)

1. Navigate to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Apps** > **Configuration** > **Create** > **Managed apps**.

3. On the **Basics** tab:
    - **Name**: Level 1 - Basic browser configuration - Windows ACP
    - **Description**: Basic browser customization for Microsoft Edge on Windows

4. Select **Next**.

5. For **Target policy to**, select **Select apps** > **Microsoft Edge Windows** > **Select**.

6. Select **Next**.

7. For **Settings**, select **Use configuration designer** and add:

    **Core Browser Behavior:**
    - Configure the home page URL: https://portal.office.com
    - Show Home button on toolbar: Enabled
    - Configure the new tab page URL: https://portal.office.com
    - Action to take on startup: Open new tab page

    **Security:**
    - Configure Automatic HTTPS: Enabled
    - Default pop-up window setting: Don't allow popups (2)

    **Privacy:**
    - Enable saving passwords: Disabled
    - Enable AutoFill for addresses: Disabled
    - Enable AutoFill for payment instruments: Disabled
    - Block tracking of users' web-browsing activity: Balanced (2)

    **Search:**
    - Enable search suggestions: Disabled
    - Enable network prediction: Don't predict (2)

    **Import Controls:**
    - Allow importing of autofill form data: Disabled
    - Allow importing of saved passwords: Disabled
    - Allow importing of browsing history: Disabled

    **Downloads:**
    - Set download directory: ${user_home}/Downloads/Edge
    - Ask where to save downloaded files: Enabled
    - Allow download restrictions: Block malicious downloads

    **Features:**
    - Show Hubs Sidebar: Disabled
    - Show Microsoft Rewards experiences: Disabled
    - Shopping in Microsoft Edge: Disabled

8. Select **Next**.

9. For **Assignments**, assign to **SEB-Level1-Users** group.

10. Select **Next** and **Create**.

### Level 2 - Enhanced browser configuration (Windows)

1. Follow steps 1-6 from Level 1.

2. On the **Basics** tab:
    - **Name**: Level 2 - Enhanced browser configuration - Windows ACP
    - **Description**: Enhanced browser configuration with other security controls

3. Configure all Level 1 settings PLUS:

    **Enhanced Security:**
    - SmartScreen for trusted downloads: Enabled
    - Block insecure content on specified sites: ["*"]

    **Extension Management:**
    - Control which extensions can't be installed: ["*"]
    - Configure extension management settings: {"*": {"installation_mode": "blocked"}}

    **Privacy:**
    - Continue running background apps after Microsoft Edge closes: Disabled
    - Disable synchronization of data: Enabled
    - Clear browsing data when Microsoft Edge closes: Enabled

4. For **Assignments**, assign to **SEB-Level2-Users** group.

5. Select **Next** and **Create**.

### Level 3 - High security configuration (Windows)

1. Follow steps 1-6 from Level 1.

2. On the **Basics** tab:
    - **Name**: Level 3 - High security configuration - Windows ACP
    - **Description**: Maximum security browser configuration

3. Configure all Level 1 and Level 2 settings PLUS:

    **URL Filtering:**
    - Define a list of allowed URLs: ["*.company.com","*.microsoft.com","*.office.com"]
    - Block access to a list of URLs: ["*"]

    **Maximum Security:**
    - Allow download restrictions: Block all downloads (3)
    - Control where developer tools can be used: Disallowed (2)
    - Configure InPrivate mode availability: InPrivate forced (1)

4. For **Assignments**, assign to **SEB-Level3-Users** group.

5. Select **Next** and **Create**.

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
