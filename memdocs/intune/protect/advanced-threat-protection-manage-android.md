---
# required metadata

title: Manage Microsoft Defender ATP web protection for Android devices in Microsoft Intune - Azure | Microsoft Docs
description: Configure Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) web protection for Android in Intune.
keywords:
author: brenduns 
ms.author: brenduns
manager: dougeby
ms.date: 12/07/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.reviewer: aanavath

# optional metadata
#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Configure Microsoft Defender for Endpoint on Android devices you manage with Intune

When you integrate Microsoft Intune and Microsoft Defender for Endpoint (Defender for Endpoint), you can use device configuration profiles to modify some settings of Defender for Endpoint on Android devices.

Before proceeding, you must successfully [Configure Defender for Endpoint in Intune](../protect/advanced-threat-protection-configure.md) and onboard Android devices to Defender for Endpoint.

## Configure web protection on devices that run Android

By default, Defender for Endpoint on Android includes and enables the web protection feature. [Web protection](/windows/security/threat-protection/microsoft-defender-atp/web-protection-overview) helps to secure devices against web threats and protect users from phishing attacks.

While enabled by default, there are valid reasons to disable this protection on some Android devices. For example, you might choose to use only the Defender for Endpoint app scan feature, or to prevent web protection from using your VPN while it scans for harmful URLs.

Intune supports turning off all or part of the web protection feature. The method you use and the capabilities you can disable depend on how the Android device is enrolled with Intune:

- **Android device administrator**: Use a configuration profile to set custom OMA-URI settings on the device to disable the entire web protection feature or to disable only the use of VPNs. For general information about custom settings for Android devices, see [Custom settings](../configuration/custom-settings-android.md).

- **Android Enterprise Personally-Owned Work Profile**: Use an app configuration profile and the *configuration designer* to disable web protection. This method and enrollment type support disabling all web protection capabilities but doesn't support disabling only the use of VPNs. For general information about app configuration policies, see [Use the configuration designer](../apps/app-configuration-policies-use-android.md#use-the-configuration-designer).

- **Android Enterprise Fully Managed**: Use an app configuration profile and the [configuration designer](../apps/app-configuration-policies-use-android.md#use-the-configuration-designer) to disable the entire web protection feature or to disable only the use of VPNs.   

To configure web protection on devices, use the following procedures to create and deploy the applicable configuration.

### Disable web protection for Android device administrator

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Configuration profiles** > **Create profile**.

3. Enter the following settings:

   - **Platform**: Select **Android device administrator**
   - **Profile**: Select **Custom**

   Select **Create**.

4. On **Basics**, enter the following details:

   - **Name**: Enter a descriptive name for the profile. Name your profiles so you can easily identify them later. For example, *Android custom profile for  Defender for endpoint web protection*
   - **Description**: Enter a description for the profile. This setting is optional but recommended.

5. On **Configuration settings**, select **Add**.

   Specify settings for the configuration you want to deploy:

   - **Disable web protection**:
     - **Name**: Enter a unique name for this OMA-URI setting so you can easily find it. For example, *Disable Defender for Endpoint web protection*
     - **Description**: (Optional) Enter a description that gives an overview of the setting, and any other important details.
     - **OMA-URI**: Enter **./Vendor/MSFT/DefenderATP/AntiPhishing**
     - **Data type**: Use the drop-down, and select **Integer**
     - **Value**: Enter **0** to disable web protection, including the VPN-based scan.
       > [!NOTE]
       > Enter **1** to enable web protection, which is the default for web protection.

   - **Disable only the use of VPN by web protection**:
     - **Name**: Enter a unique name for this OMA-URI setting so you can easily find it. For example, *Disable Defender for Endpoint web protection VPN*
     - **Description**: (Optional) Enter a description that gives an overview of the setting, and any other important details.
     - **OMA-URI**: Enter **./Vendor/MSFT/DefenderATP/Vpn**
     - **Data type**: Use the drop-down, and select **Integer**
     - **Value**: Enter **0** to disable the VPN-based scan.
       > [!NOTE]
       > Enter **1** to enable web protection, which is the default for web protection.

   Select **Add** to save the OMA-URI settings configuration, and then select **Next** to continue.

6. On **Assignments**, specify the groups that will receive this profile. For more information on assigning profiles, see [Assign user and device profiles](../configuration/device-profile-assign.md).

7. On **Review + create**, when you're done, choose **Create**. The new profile is displayed in the list when you select the policy type for the profile you created.

### Disable web protection for Android Enterprise Personally-Owned Work Profile
   > [!NOTE]
   > You cannot disable web protection for Android Enterprise Personally-Owned Work Profile, if you have configured [**Auto Setup of Always-on VPN, Device
     configuration policy**](https://docs.microsoft.com/en-us/windows/security/threat-protection/microsoft-defender-atp/android-intune#auto-setup-of-always-on-vpn) on the enrolled devices
   
1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Apps** > **App configuration policies** > **Add**, and then select **Managed devices**.

3. On **Basics**, enter the following details:

   - **Name**: Enter a descriptive name for the profile. Name your profiles so you can easily identify them later. For example, *Android app configuration for Defender for Endpoint web protection*.
   - **Description**: Enter a description for the profile. This setting is optional but recommended.
   - **Platform**: Select **Android Enterprise**
   - **Profile Type**: Select **Personally-Owned Work Profile Only**
   - **Targeted app**: Click on **Select app**.

4. On **Associated app**, find and select **Microsoft Defender ATP**, and then select **OK** > **Next**.

5. On **Settings**, use the drop-down for **Configuration settings format**, select **Use configuration designer**, and then click **Add**. The JSON editor opens.

6. Find and select configuration keys **Anti-Phishing, VPN**, and then select **OK** to return to **Settings** page 

7. For **Configuration values** of both the configuration keys (Anti-Phishing, VPN), enter **0** to disable web protection. 

   > [!NOTE]
   > Configuration key **Web Protection** is deprecated. If you have configured with this key in the past, follow the previous steps to re-configure this setting by setting the keys **Anti-Phishing** and **VPN** to enable or disable web protection. 

   > [!NOTE]
   > Enter **1** for both the configuration values (Anti-Phishing, VPN) to enable web protection. This is the default configuration. 
     
   Select **Next** to continue.

8. On **Assignments**, specify the groups that will receive this profile. For more information on assigning profiles, see [Assign user and device profiles](../configuration/device-profile-assign.md).

9. On **Review + create**, when you're done, choose **Create**. The new profile is displayed in the list when you select the policy type for the profile you created.

### Disable web protection for Android Enterprise Fully Managed Profile
1. Follow the same configuration steps as above and add web protection configuration keys **Anti-phishing** and **VPN**. Only difference is the ‘Profile Type’ selection. **Profile Type:** Select **Fully Managed, Dedicated, and Corporate-Owned Work Profile Only** 
      - To **Disable web protection** enter **0** for both Configuration values **Anti-phishing** and **VPN**   
      - To **Disable only the use of VPN by web protection** enter configurtion values
        - **0** for **VPN** 
        - **1** for **Anti-phishing**
      > [!NOTE]
      > You cannot disable **VPN** for **Android Enterprise Fully Managed Profile**, if you have configured [**Auto Setup of Always-on VPN, Device configuration             policy**](https://docs.microsoft.com/en-us/windows/security/threat-protection/microsoft-defender-atp/android-intune#auto-setup-of-always-on-vpn) on the enrolled devices
      
      > [!NOTE]
      > Enter **1** for both the configuration values (Anti-Phishing, VPN) to enable web protection. This is the default configuration. 
 
Select **Next** to continue. 

2. On **Assignments**, specify the groups that will receive this profile. For more information on assigning profiles, see Assign user and device profiles. 

3. On **Review + create**, when you're done, choose **Create**. The new profile is displayed in the list when you select the policy type for the profile you
   created.

## Next steps

- [Monitor compliance for risk levels](../protect/advanced-threat-protection-monitor.md)
- [Use security tasks with ATPs Vulnerability Management to remediate issues on devices](../protect/atp-manage-vulnerabilities.md)

Learn more from the Defender for Endpoint documentation:
- [Defender for Endpoint Conditional Access](/windows/security/threat-protection/microsoft-defender-atp/conditional-access)
- [Defender for Endpoint risk dashboard](/windows/security/threat-protection/microsoft-defender-atp/security-operations-dashboard)
