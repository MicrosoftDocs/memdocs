---
# required metadata

title: Create device profiles in Microsoft Intune
description: Add or configure a device configuration profile in Microsoft Intune. Select the platform type, configure the settings, add a scope tag.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 09/20/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:
ms.assetid: d98aceff-eb35-4e3e-8e40-5f300e7335cc

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: heenamac
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
  - M365-identity-device-management
  - highpri
---

# Create a device profile in Microsoft Intune

[!INCLUDE [windows-phone-81-windows-10-mobile-support](../includes/windows-phone-81-windows-10-mobile-support.md)]

Device profiles allow you to add and configure settings, and then push these settings to devices in your organization. You have some options when creating policies:

- **Administrative templates**: On Windows 10/11 devices, these templates are ADMX settings that you configure. If you're familiar with ADMX policies or group policy objects (GPO), then using administrative templates is a natural step to Microsoft Intune and Endpoint Manager.

  For more information, see [Administrative Templates](administrative-templates-windows.md)

- **Baselines**: On Windows 10/11 devices, these baselines include preconfigured security settings. If you want to create security policy using recommendations by Microsoft security teams, then security baselines are for you.

  For more information, see [Security baselines](../protect/security-baselines.md).

- **Settings catalog**: On Windows 10/11 devices, use the settings catalog to see all the available settings, and in one location. For example, you can see all the settings that apply to BitLocker, and create a policy that just focuses on BitLocker. On macOS devices, use the settings catalog to configure Microsoft Edge version 77 and settings. 

  For more information, see [Settings catalog](settings-catalog.md).

  On macOS, continue using the [preference file](/deployedge/configure-microsoft-edge-on-mac) to:
  
  - Configure earlier versions of Microsoft Edge
  - Configure Edge browser settings that aren't in settings catalog

- **Templates**: On Android, iOS/iPadOS, macOS, and Windows devices, the templates include a logical grouping of settings that configure a feature or concept, such as VPN, email, kiosk devices, and more. If you're familiar with creating device configuration policies in Microsoft Intune, then you're already using these templates.

  For more information, including the available templates, see [Apply features and settings on your devices using device profiles](device-profiles.md).

This article:

- Lists the steps to create a profile.
- Shows you how to add a scope tag to "filter" your policies.
- Describes applicability rules on Windows client devices, and shows you how to create a rule.
- Lists the check-in refresh cycle times when devices receive profiles and any profile updates.

## Create the profile

Profiles are created in the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431). In this admin center, select **Devices**. You have the following options:

:::image type="content" source="./media/device-profile-create/devices-overview.png" alt-text="In Endpoint Manager and Microsoft Intune, select Devices to see what you can configure and manage.":::

- **Overview**: Lists the status of your profiles, and provides more details on the profiles you assigned to users and devices.
- **Monitor**: Check the status of your profiles for success or failure, and also view logs on your profiles.
- **By platform**: Create and view policies and profiles by your platform. This view may also show features specific to the platform. For example, select **Windows**. You'll see Windows-specific features, such as **Windows Update Rings** and **PowerShell scripts**.
- **Policy**: Create device profiles, upload custom [PowerShell scripts](../apps/intune-management-extension.md) to run on devices, and add data plans to devices using [eSIM](esim-device-configuration.md).

When you create a profile (**Configuration profiles** > **Create profile**), choose your platform:

- **Android device administrator**
- **Android Enterprise**
- **iOS/iPadOS**
- **macOS**
- **Windows 10 and later**
- **Windows 8.1 and later**

Then, choose the profile. Depending on the platform you choose, the settings you can configure are different. The following articles describe the different profiles:

- [Administrative templates (Windows)](administrative-templates-windows.md)
- [Custom](custom-settings-configure.md)
- [Delivery Optimization (Windows)](delivery-optimization-windows.md)
- [Derived credential (Android Enterprise, iOS, iPadOS)](../protect/derived-credentials.md)
- [Device features (macOS, iOS, iPadOS)](device-features-configure.md)
- [Device firmware (Windows)](device-firmware-configuration-interface-windows.md)
- [Device restrictions](device-restrictions-configure.md)
- [Domain join (Windows)](domain-join-configure.md)
- [Edition upgrade and mode switch (Windows)](edition-upgrade-configure-windows-10.md)
- [Education (iOS, iPadOS)](../fundamentals/education-settings-configure-ios.md)
- [Email](email-settings-configure.md)
- [Endpoint protection (macOS, Windows)](../protect/endpoint-protection-configure.md)
- [Extensions (macOS)](kernel-extensions-overview-macos.md)
- [Identity protection (Windows)](../protect/identity-protection-configure.md)
- [Kiosk](kiosk-settings.md)
- [Microsoft Defender for Endpoint (Windows)](../protect/advanced-threat-protection.md)
- [Mobility Extensions (MX) profile (Android device administrator)](android-zebra-mx-overview.md)
- [Network boundary (Windows)](network-boundary-windows.md)
- [OEMConfig (Android Enterprise)](android-oem-configuration-overview.md)
- [PKCS certificate](../protect/certificates-pfx-configure.md)
- [PKCS imported certificate](../protect/certificates-imported-pfx-configure.md)
- [Preference file (macOS)](preference-file-settings-macos.md)
- [SCEP certificate](../protect/certificates-scep-configure.md)
- [Secure assessment (Education) (Windows)](education-settings-configure.md)
- [Shared multi-user device (Windows)](shared-user-device-settings.md)
- [Telecom expenses (Android device administrator, iOS, iPadOS)](telecom-expenses-monitor.md)
- [Trusted certificate](../protect/certificates-configure.md)
- [VPN](vpn-settings-configure.md)
- [Wi-Fi](wi-fi-settings-configure.md)
- [Windows health monitoring](windows-health-monitoring.md)
- [Wired networks (macOS)](wired-network-settings-macos.md)

For example, if you select **iOS/iPadOS** for the platform, your options look similar to the following profile:

:::image type="content" source="./media/device-profile-create/create-device-profile.png" alt-text="Create an iOS/iPadOS device configuration policy and profile in Endpoint Manager and Microsoft Intune.":::

If you select **Windows 10 and later** for the platform, your options look similar to the following profile:

:::image type="content" source="./media/device-profile-create/windows-create-device-profile.png" alt-text="Create a Windows device configuration policy and profile in Endpoint Manager and Microsoft Intune.":::

## Scope tags

After you add the settings, you can also add a scope tag to the profile. Scope tags filter profiles to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. And, are used in distributed IT.

For more information about scope tags, and what you can do, see [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md).

## Applicability rules

Applies to:

- Windows 11
- Windows 10

Applicability rules allow administrators to target devices in a group that meet specific criteria. For example, you create a device restrictions profile that applies to the **All Windows 10/11 devices** group. And, you only want the profile assigned to devices running Windows Enterprise.

To do this task, create an **applicability rule**. These rules are great for the following scenarios:

- You use Windows 10 Education (EDU). At Bellows College, you want to target all Windows 10 EDU devices between RS3 and RS4.
- You want to target all users in Human Resources at Contoso, but only want Windows 10 Professional or Enterprise devices.

To approach these scenarios, you:

- Create a devices group that includes all devices at Bellows College. In the profile, add an applicability rule so it applies if the OS minimum version is `16299` and the maximum version is `17134`. Assign this profile to the Bellows College devices group.

  When it's assigned, the profile applies to devices between the minimum and maximum versions you enter. For devices that aren't between the minimum and maximum versions you enter, their status shows as **Not applicable**.

- Create a users group that includes all users in Human Resources (HR) at Contoso. In the profile, add an applicability rule so it applies to devices running Windows 10 Professional or Enterprise. Assign this profile to the HR users group.

  When it's assigned, the profile applies to devices running Windows 10 Professional or Enterprise. For devices that aren't running these editions, their status shows as **Not applicable**.

- If there are two profiles with the exact same settings, then the profile without an applicability rule is applied. 

  For example, ProfileA targets the Windows 10 devices group, enables BitLocker, and doesn't have an applicability rule. ProfileB targets the same Windows 10 devices group, enables BitLocker, and has an applicability rule to only apply the profile to Windows 10 Enterprise.

  When both profiles are assigned, ProfileA is applied because it doesn't have an applicability rule. 

When you assign the profile to the groups, the applicability rules act as a filter, and only target the devices that meet your criteria.

### Add a rule

1. Select **Applicability Rules**. You can choose the **Rule**, and **Property**:

    :::image type="content" source="./media/device-profile-create/applicability-rules.png" alt-text="Add an applicability rule to a Windows 10 device configuration profile in Endpoint Manager and Microsoft Intune.":::

2. In **Rule**, choose if you want to include or exclude users or groups. Your options:

    - **Assign profile if**: Includes users or groups that meet the criteria you enter.
    - **Don't assign profile if**: Excludes users or groups that meet the criteria you enter.

3. In **Property**, choose your filter. Your options: 

    - **OS edition**: In the list, check the Windows client editions you want to include (or exclude) in your rule.
    - **OS version**: Enter the **min** and **max** Windows client version numbers of you want to include (or exclude) in your rule. Both values are required.

      For example, you can enter `10.0.16299.0` (RS3 or 1709) for minimum version and `10.0.17134.0` (RS4 or 1803) for maximum version. Or, you can be more granular and enter `10.0.16299.001` for minimum version and `10.0.17134.319` for maximum version.

      For more version numbers, see [Windows client release information](/windows/release-health/release-information).

4. Select **Add** to save your changes.

## Refresh cycle times

Intune uses different refresh cycles to check for updates to configuration profiles. If the device recently enrolled, the check-in runs more frequently. [Policy and profile refresh cycles](device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned) lists the estimated refresh times.

At any time, users can open the Company Portal app, and sync the device to immediately check for profile updates.

## Recommendations

When creating profiles, consider the following recommendations:

- Name your policies so you know what they are, and what they do. All [compliance policies](../protect/create-compliance-policy.md) and [configuration profiles](../configuration/device-profile-create.md) have an optional **Description** property. In **Description**, be specific and include information so others know what the policy does.

  Some configuration profile examples include:

  **Profile name**: Admin template - OneDrive configuration profile for all Windows 10 users  
  **Profile description**: OneDrive admin template profile that includes the minimum and base settings for all Windows 10 users. Created by user@contoso.com to prevent users from sharing organizational data to personal OneDrive accounts.

  **Profile name**: VPN profile for all iOS/iPadOS users  
  **Profile description**: VPN profile that includes the minimum and base settings for all iOS/iPadOS users to connect to Contoso VPN. Created by user@contoso.com so users automatically authenticate to VPN, instead of prompting users for their username and password.

- Create your profile by its task, such as configure Microsoft Edge settings, enable Microsoft Defender anti-virus settings, block iOS/iPadOS jailbroken devices, and so on.

- Create profiles that apply to specific groups, such as Marketing, Sales, IT Administrators, or by location or school system.

- Separate user policies from device policies.

  For example, [Administrative Templates in Intune](administrative-templates-windows.md) have thousands of ADMX settings. These templates show if a setting applies to users or devices. When creating admin templates, assign your users settings to a users group, and assign your device settings to a devices group.

  The following image shows an example of a setting that can apply to users, apply to devices, or apply to both:

  :::image type="content" source="./media/device-profile-create/setting-applies-to-user-and-device.png" alt-text="Intune admin template that applies to user and devices in Endpoint Manager and Microsoft Intune.":::

- Every time you create a restrictive policy, communicate this change to your users. For example, if you're changing the passcode requirement from four (4) characters to six (6) characters, let your users know before your assign the policy.

## Next steps

[Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).
