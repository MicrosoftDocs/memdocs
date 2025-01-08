---
# required metadata

title: Configure Defender for Endpoint Web protection on Android devices in Microsoft Intune
description: Use Intune policy to manage Microsoft Defender for Endpoint web protection settings on Android devices managed by Microsoft Intune.
keywords:
author: brenduns 
ms.author: brenduns
manager: dougeby
ms.date: 08/22/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.reviewer: aanavath

# optional metadata
#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
- sub-secure-endpoints
---

# Configure Microsoft Defender for Endpoint web protection on Android devices managed by Intune

When you integrate [Microsoft Defender for Endpoint](../protect/advanced-threat-protection-configure.md) with Microsoft Intune, you can use device configuration profiles to modify some Defender for Endpoint settings on Android devices.

By default, Microsoft Defender for Endpoint for Android includes and enables the Microsoft Defender for Endpoint [Web protection](/windows/security/threat-protection/microsoft-defender-atp/web-protection-overview) feature that can help to secure devices against web threats and protect users from phishing attacks.

While enabled by default, there are valid reasons to disable it on some Android devices. For example, you might decide to use only the Defender for Endpoint app scan feature or to prevent web protection from using your VPN while it scans for harmful URLs.

With Intune device configuration policy, you can turn off all or part of the web protection feature. The method you use and the capabilities you can disable depend on how the Android device is enrolled with Intune:

- **Android device administrator**. Use a configuration profile to set custom OMA-URI settings on the device that disable the entire web protection feature or that disable only the use of VPNs. For general information about custom settings for Android devices, see [Use custom settings for Android devices in Microsoft Intune](../configuration/custom-settings-android.md).

- **Android Enterprise personally owned work profile**. Use an app configuration profile and the configuration designer to disable web protection. This method and enrollment type support disabling all web protection capabilities but don't support disabling only the use of VPNs. For general information about app configuration policies, see [Use the configuration designer](../apps/app-configuration-policies-use-android.md#use-the-configuration-designer).

- **Android Enterprise Fully Managed profile**. Use an app configuration profile and the [configuration designer](../apps/app-configuration-policies-use-android.md#use-the-configuration-designer) to disable the entire web protection feature or to disable only the use of VPNs.

**The following browsers are supported with Defender loopback VPN:** 
- Chrome- 
- Microsoft Edge
- Opera
- Samsung Internet
- Firefox
- Brave
- Tor
- Browser Leopard
- DuckDuckGo
- Dolphin
 
**The following browsers are supported with accessibility service without Defender loopback VPN:**
- Chrome
- Edge
- Opera
- Samsung Internet

> [!IMPORTANT]
> Work profile scenarios (Android Enterprise personally owned devices using a work profile and Android Enterprise corporate owned work profile) do not support the accessibility service.

To configure web protection on devices, use the following procedures to create and deploy the applicable configuration.

## Disable web protection for Android device administrator

[!INCLUDE [android_device_administrator_support](../includes/android-device-administrator-support.md)]

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Manage devices** > **Configuration** > On the *Policies* tab, select **+ Create**.

3. Enter these settings:

   - **Platform**: Select **Android device administrator**.
   - **Profile**: Select **Custom**.

   Select **Create**.

4. In **Basics**, enter these details:

   - **Name**: Enter a descriptive name for the profile. Name your profiles so you can easily identify them later. For example, **Android custom profile for  Defender for Endpoint web protection**.
   - **Description**: Enter a description for the profile. This setting is optional but recommended.

5. In **Configuration settings**, select **Add**.

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

6. In **Assignments**, specify the groups that receive the profile. For more information on assigning profiles, see [Assign user and device profiles](../configuration/device-profile-assign.md).

7. In **Review + create**, when you're done, select **Create**. The new profile is displayed in the list when you select the policy type for the profile you created.

## Disable web protection for the Android Enterprise personally owned work profile

> [!NOTE]
>
> You can't disable web protection for the Android Enterprise personally owned work profile if you've configured the [Auto Setup of Always-on VPN device configuration policy](/windows/security/threat-protection/microsoft-defender-atp/android-intune#auto-setup-of-always-on-vpn) on the enrolled devices.
  
1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Apps** > **App configuration policies** > **Add**, and then select **Managed devices**.

3. In **Basics**, enter these details:

   - **Name**: Enter a descriptive name for the profile. Name your profiles so you can easily identify them later. For example, **Android app configuration for Microsoft Defender for Endpoint web protection**.
   - **Description**: Enter a description for the profile. This setting is optional but recommended.
   - **Platform**: Select **Android Enterprise**.
   - **Profile Type**: Select **Personally-Owned Work Profile Only**.
   - **Targeted app**: Click **Select app**.

4. In **Associated app**, find and select **Defender for Endpoint**, and then select **OK** > **Next**.

5. In **Settings**, in **Configuration settings format**, select **Use configuration designer**, and then select **Add**. The JSON editor opens.

6. Find and select configuration keys **Anti-Phishing** and **VPN**, and then select **OK** to return to the **Settings** page.

1. For the **Configuration values** of both configuration keys (**Anti-Phishing** and **VPN**), enter **0** to disable web protection and enter **1** to enable web protection. By default, web protection is enabled.

   > [!NOTE]
   > Values for Anti-Phishing and VPN should be same either to be 0 to disable or 1 to enable, otherwise both features will automatically be disabled.
   
   > [!NOTE]
   > The **Web Protection** configuration key is deprecated. If you've used this key in the past, complete the previous steps to re-configure the setting by setting the keys **Anti-Phishing** and **VPN** to enable or disable web protection.
   
   Select **Next** to continue.
   
8. In **Assignments**, specify the groups that receive the profile. For more information on assigning profiles, see [Assign user and device profiles](../configuration/device-profile-assign.md).

9. In **Review + create**, when you're done, select **Create**. The new profile is displayed in the list when you select the policy type for the profile you created.

## Disable web protection for the Android Enterprise Fully Managed profile

1. Complete the same configuration steps [described previously](#disable-web-protection-for-the-android-enterprise-personally-owned-work-profile), and add web protection configuration keys **Anti-phishing** and **VPN**. The only difference is the **Profile Type** value. For this value, select **Fully Managed, Dedicated, and Corporate-Owned Work Profile Only**.

   - To disable web protection, enter **0** for configuration values **Anti-Phishing** and **VPN** and enter **1** for both configuration values (**Anti-Phishing** and **VPN**) to enable web protection. By default, web protection is enabled.
      
   - To disable only the use of VPN by web protection, enter these configuration values:
      - **0** for **VPN**
            
      - **1** for **Anti-Phishing**
            
   > [!NOTE]
   > For 'Android Enterprise corporate owned work profile' enrollment scenario values for VPN and Anti-Phishing should be same either both 0 to disable or 1 to enable, otherwise both features will automatically be disabled, but for 'Android Enterprise corporate owned fully managed - no work profile' enrollment scenario need not to have the same value for VPN and Anti-Phishing, each feature can work individually.
   
   > [!NOTE]
   > You can't disable VPN for the Android Enterprise Fully Managed profile if you've configured the Auto Setup of Always-on VPN device configuration     policy on the enrolled devices.
   
   Select **Next** to continue.
   
2. In **Assignments**, specify the groups that receive the profile. For more information on assigning profiles, see [Assign user and device profiles](../configuration/device-profile-assign.md).

3. In **Review + create**, when you're done, select **Create**. The new profile is displayed in the list when you select the policy type for the profile you
   created.

## Next steps

- [Monitor device compliance status for risk levels](../protect/advanced-threat-protection-monitor.md)
- [Use security tasks with Defender for Endpoints Vulnerability Management to remediate problems on devices](../protect/atp-manage-vulnerabilities.md)

- Learn more from the Microsoft Defender for Endpoint documentation:

  - [Microsoft Defender for Endpoint Conditional Access](/windows/security/threat-protection/microsoft-defender-atp/conditional-access)
    
  - [Microsoft Defender for Endpoint risk dashboard](/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)
    
