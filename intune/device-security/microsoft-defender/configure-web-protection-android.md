---
title: Configure Defender for Endpoint web protection on Android devices in Microsoft Intune
description: Use Intune policy to manage Microsoft Defender for Endpoint web protection settings on Android devices managed by Microsoft Intune.
ms.date: 05/22/2026
ms.topic: how-to
ai-usage: ai-assisted
ms.reviewer: aanavath
ms.collection:
- M365-identity-device-management
- sub-secure-endpoints
---

# Configure Microsoft Defender for Endpoint web protection on Android devices managed by Intune

When you integrate [Microsoft Defender for Endpoint](./configure-integration.md) with Microsoft Intune, you can use device configuration profiles to modify some Defender for Endpoint settings on Android devices.

By default, Microsoft Defender for Endpoint for Android includes and enables the Microsoft Defender for Endpoint [Web protection](/defender-endpoint/web-protection-overview) feature that can help to secure devices against web threats and protect users from phishing attacks.

While enabled by default, there are valid reasons to disable it on some Android devices. For example, you might decide to use only the Defender for Endpoint app scan feature or to prevent web protection from using your VPN while it scans for harmful URLs.

With Intune device configuration policy, you can turn off all or part of the web protection feature. The method you use and the capabilities you can disable depend on how the Android device is enrolled with Intune:

- **Android Enterprise personally owned work profile**. Use an app configuration profile and the configuration designer to disable web protection. This method and enrollment type support disabling all web protection capabilities but don't support disabling only the use of VPNs. For general information about app configuration policies, see [Use the configuration designer](../../app-management/configuration/configure-managed-android.md#use-the-configuration-designer).

- **Android Enterprise fully managed**. Use an app configuration profile and the [configuration designer](../../app-management/configuration/configure-managed-android.md#use-the-configuration-designer) to disable the entire web protection feature or to disable only the use of VPNs.

- **Android device administrator** (deprecated). Use custom OMA-URI settings to disable web protection. For details, see [Disable web protection for Android device administrator](#disable-web-protection-for-android-device-administrator).

Web protection uses a local loopback VPN to intercept and evaluate web traffic. This VPN doesn't route traffic outside the device. The following browsers are known to work with the Defender loopback VPN:

- Chrome
- Microsoft Edge
- Firefox
- Opera
- Samsung Internet
- Brave
- DuckDuckGo

A smaller set of browsers (Chrome, Edge, Opera, Samsung Internet) also support web protection through the Android accessibility service when the loopback VPN isn't in use.

> [!NOTE]
> This list might not be exhaustive. For the latest information about web protection capabilities on Android, see [Configure web protection](/defender-endpoint/android-configure#configure-web-protection) in the Defender for Endpoint documentation.

> [!IMPORTANT]
> Work profile scenarios (Android Enterprise personally owned devices using a work profile and Android Enterprise corporate owned work profile) do not support the accessibility service.

To configure web protection on devices, use the following procedures to create and deploy the applicable configuration.

## Disable web protection for the Android Enterprise personally owned work profile

> [!NOTE]
>
> You can't disable web protection for the Android Enterprise personally owned work profile if you've configured the [Auto Setup of Always-on VPN](./deploy-android.md#set-up-always-on-vpn) device configuration policy on the enrolled devices.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. Select **Apps** > **Managed apps** > **Configuration** > **Create**, and then select **Managed devices**.

1. In **Basics**, enter these details:

   - **Name**: Enter a descriptive name for the profile. Name your profiles so you can easily identify them later. For example, **Android app configuration for Microsoft Defender for Endpoint web protection**.
   - **Description**: Enter a description for the profile. This setting is optional but recommended.
   - **Platform**: Select **Android Enterprise**.
   - **Profile Type**: Select **Personally-Owned Work Profile Only**.
   - **Targeted app**: Select **Select app**.

1. In **Associated app**, find and select **Defender for Endpoint**, and then select **OK** > **Next**.

1. In **Settings**, in **Configuration settings format**, select **Use configuration designer**, and then select **Add**.

1. Find and select configuration keys **Anti-Phishing** and **VPN**, and then select **OK** to return to the **Settings** page.

1. For the **Configuration values** of both configuration keys (**Anti-Phishing** and **VPN**), enter **0** to disable web protection and enter **1** to enable web protection. By default, web protection is enabled.

   > [!NOTE]
   > The values for **Anti-Phishing** and **VPN** must match. Set both to **0** to disable or both to **1** to enable. If the values don't match, both features are automatically disabled.

   Select **Next** to continue.

1. In **Assignments**, specify the groups that receive the profile. For more information on assigning profiles, see [Assign user and device profiles](../../device-configuration/assign-device-profile.md).

1. In **Review + create**, when you're done, select **Create**. The new profile is displayed in the list when you select the policy type for the profile you created.

## Disable web protection for Android Enterprise fully managed

1. Complete the same configuration steps [described previously](#disable-web-protection-for-the-android-enterprise-personally-owned-work-profile) with the following difference: for **Profile Type**, select **Fully Managed, Dedicated, and Corporate-Owned Work Profile Only**.

   - To disable web protection, enter **0** for both **Anti-Phishing** and **VPN**. To enable web protection, enter **1** for both values. By default, web protection is enabled.

   - To disable only the use of VPN by web protection, enter these configuration values:
      - **0** for **VPN**

      - **1** for **Anti-Phishing**

   > [!NOTE]
   > For the **corporate-owned work profile** enrollment scenario, the values for **VPN** and **Anti-Phishing** must match. Set both to **0** to disable or both to **1** to enable. If the values don't match, both features are automatically disabled.
   >
   > For the **corporate-owned fully managed** (no work profile) enrollment scenario, **VPN** and **Anti-Phishing** can be set independently. Each feature works on its own.

   > [!NOTE]
   > You can't disable VPN for Android Enterprise fully managed devices if you've configured the Auto Setup of Always-on VPN device configuration policy on the enrolled devices.

   Select **Next** to continue.

1. In **Assignments**, specify the groups that receive the profile. For more information on assigning profiles, see [Assign user and device profiles](../../device-configuration/assign-device-profile.md).

1. In **Review + create**, when you're done, select **Create**. The new profile is displayed in the list when you select the policy type for the profile you created.

## Disable web protection for Android device administrator

[!INCLUDE [android_device_administrator_support](../../includes/android-device-administrator-support.md)]

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. Select **Devices** > **Manage devices** > **Configuration** > On the *Policies* tab, select **+ Create**.

1. Enter these settings:

   - **Platform**: Select **Android device administrator**.
   - **Profile**: Select **Custom**.

   Select **Create**.

1. In **Basics**, enter these details:

   - **Name**: Enter a descriptive name for the profile. Name your profiles so you can easily identify them later. For example, **Android custom profile for Defender for Endpoint web protection**.
   - **Description**: Enter a description for the profile. This setting is optional but recommended.

1. In **Configuration settings**, select **Add**.

   Specify settings for the configuration you want to deploy:

   - **Disable web protection**:
     - **Name**: Enter a unique name for this OMA-URI setting so you can find it easily. For example, **Disable Defender for Endpoint web protection**.
     - **Description**: (Optional) Enter a description that provides an overview of the setting and any other important details.
     - **OMA-URI**: Enter `./Vendor/MSFT/DefenderATP/AntiPhishing`
     - **Data type**: Select **Integer** in the drop-down list.
     - **Value**: To disable web protection, set *Value* to **0**. To enable web protection, enter **1**, which is the default.

   - **Disable only the use of VPN by web protection**:
     - **Name**: Enter a unique name for this OMA-URI setting so you can find it easily. For example, **Disable Microsoft Defender for Endpoint web protection VPN**.
     - **Description**: (Optional) Enter a description that provides an overview of the setting and any other important details.
     - **OMA-URI**: Enter `./Vendor/MSFT/DefenderATP/Vpn`
     - **Data type**: Select **Integer** in the drop-down list.
     - **Value**: To disable the VPN-based scan, set *Value* to **0**. To enable the VPN-based scan, enter **1**, which is the default.

   Select **Add** to save the OMA-URI settings configuration, and then select **Next** to continue.

1. In **Assignments**, specify the groups that receive the profile. For more information on assigning profiles, see [Assign user and device profiles](../../device-configuration/assign-device-profile.md).

1. In **Review + create**, when you're done, select **Create**. The new profile is displayed in the list when you select the policy type for the profile you created.

## Next steps

- [Monitor device compliance status for risk levels](./monitor.md)
- [Use security tasks with Defender for Endpoints Vulnerability Management to remediate problems on devices](./remediate-vulnerabilities.md)

- Learn more from the Microsoft Defender for Endpoint documentation:

  - [Microsoft Defender for Endpoint Conditional Access](/defender-endpoint/conditional-access)

  - [Microsoft Defender for Endpoint risk dashboard](/defender-endpoint/security-operations-dashboard)