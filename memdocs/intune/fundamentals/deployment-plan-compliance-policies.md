---
# required metadata

title: Configure compliance policies
titleSuffix: Microsoft Intune
description: Description for configuring compliance policies
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/8/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite:
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection: 
  - M365-identity-device-management 
  - highpri
---
<!-- >
# Configure compliance policies

## Recommended compliance policies - basic

## Recommended compliance policies - advanced?

### tunnel?

### certificates?

### Defender for Endpoint

### Conditional access ?
-->

# Step 3 – Plan for compliance policies

*This article stub remains a work in progress*

Previously, you’ve set up your Intune subscription and created app protection policies. Next, plan for and configure device compliance settings and policies to help protect organizational data by requiring devices to meet requirements that you set. You'll deploy these policies directly to devices, or to users so that any device they use must also meet your requirements. The following are a few examples of common requirements:

- Minimum operating system versions for different platforms
- Password or PIN requirements like complexity and length
- Devices being at or below a *threat level* as determined by mobile threat defense software you use, like Microsoft Defender for Endpoint, or one of Intune’s other supported partners.

Your compliance policies can also take certain *actions* when a device fails to meet your requirements, including:

- Remotely lock a noncompliant device.
- Send email or notifications to a device or user, so the device user can bring it into compliance.
- Identify a device that might be ready for retirement when it remains out of compliance for some time.

If you use Conditional Access, your Conditional Access policies can use the results of your device compliance policies to determine which devices can access your organizational resources. This access control is separate from the *actions for noncompliance* that you include in your device compliance policies.

The following sections describe considerations for device compliance management, with later sections discussing more advanced configurations and integrations that provide more capabilities. There is no single group of settings of setting configurations that fit all customers. Instead, we believe all environments should start by configuring the tenant-wide device compliance settings that define how the Intune compliance service interacts with devices. Then, with a core foundation for device compliance established, add the additional layers you need to meet your organizational needs and expectations. Some of these additional layers include:  

- Deploying platform-specific device configuration policies to enforce your device compliance goals.
- Use of status results from a Mobile Threat Defense partner, like Microsoft Defender for Endpoint or one of many other third-party partners.
- Integrating a third-party compliance partner when not using Intune as your Mobile Device Management authority.
- Configuring Azure Active Directory (Azure AD) Conditional Access policies to gate which devices have access to resources based on the devcies compliance status.
- Defining custom compliance settings (for Windows and Linux) to use settings that aren't yet natively available through the Intune compliance policy UI.

<!-- ## Prerequisites

The prerequisites for device compliance will depend on the product, features, and capabilities you use.

- Intune subscription – *Required*. With an Intune subscription, you also have Azure AD *(v/level*), which is a basic requirement to use Intune.
- Azure AD – *Required*. Included with the Intune subscription, a basic Azure AD *(v/level*)> is sufficient for Compliance policy settings and Device compliance policies. However, Azure AD Premium is required to use Conditional Access.
- Azure AD Premium – Optional. Azure AD Premium *(v/level*) or greater is required to use Conditional Access.
- Third party compliance partner – Optional.
- ???
- ??? 
-->

## Device compliance foundation

✔️ **Configure tenant-wide Compliance policy settings**

We believe all organizations should understand the use of the tenant-wide compliance settings. These settings apply to all applicable devices, establish how compliance evaluations function in your tenant, and are distinct from other configurations, like the settings you configure and deploy to discrete groups and device platforms.

The tenant-wide settings are comprised of following three *Compliance policy settings*:

1. Set **Mark devices with no compliance policy assigned as** to be **noncompliant**. This configuration is required if you plan to use compliance policies to help protect your organizations resources from unauthorized access. This configuration supports integrating compliance policies with Conditional Access so you can gate which users and devices can access company resources.

2. Applicable only to iOS/iPad devices, consider setting **Enhanced jailbreak detection** to **Enabled**. This configuration changes how the device compliance policy setting *block jailbroken devices* functions by adding extra criteria for when to run detection. When enabled, this option can effect a devices battery life because devices run additional jailbreak detections when:  

   - The Company Portal app opens.
   - The device physically moves a significant distance, which is approximately 500 meters or more. Intune can’t guarantee that each significant location change results in a jailbreak detection check, as the check depends on a device's network connection at the time.

   On iOS 13 and higher, users must select *Always Allow* whenever the device prompts them to continue allowing Company Portal to use their location in the background. If enabled, this will allow more frequent jailbreak detection checks.

3. Configure **Compliance status validity period (days)** to have Intune mark devices as noncompliant when they’ve failed to report a compliance status for longer than the configured time. By being marked noncompliant, devices that might otherwise have access to your organizations resources can be blocked or identified for retirement, making int easier to round up and then remove aged or risky devices from management altogether.

To learn more about Compliance Policy Settings at the tenant level, and how to configure them, see [Compliance policy settings](../protect/device-compliance-get-started.md#compliance-policy-settings)

## Core device compliance policy

✔️ **Identify your organizations desired compliance configurations for device platform**  
✔️ **Deploy device configuration policies for each platform type**

Use device compliance policies to identify when devices that will access your apps and data are in a state that meets your organization’s requirements. These policies support a range of settings that are specific to each platform. Some compliance settings evaluate and report back a status for that device. Other settings can function more like device configuration settings byh enforcing a requirement, such as those for password complexity or PIN requirements.

Before creating a series of policies:

- Identify some minimum compliance expectations for your organization. With expectations for device compliance in mind, you can then configure an deploy device configuration policies to support your goals. Requirements and criteria for settings will vary from organization to organization, and in some cases between different groups of users or devices within an organization. Following are some common settings to consider as a start, regardless of the platform type like Windows, iOS/iPadOS, or Android:

  - Password complexity
  - *Example 2*
  - *Example 3*

- Consider how different compliance policies can interact with each other, and how compliance settings interact with device configuration settings. It's possible to deploy different configurations for a setting to a device from separate policy sources. When devices receive different configurations for a setting, results might be unexpected. However, with a bit of planning, you can minimize overlap, and aim to reduce the overall number of policies you use to effectively meet your device compliance goals. See [If multiple policies are assigned to the same user or device, how do I know which settings gets applied?](../configuration/device-profile-troubleshoot.md#if-multiple-policies-are-assigned-to-the-same-user-or-device-how-do-i-know-which-settings-gets-applied).

The following list of articles is a good place to start to get an understanding of the settings Intune policies natively support:

- [Android device administrator](../protect/compliance-policy-create-android.md)
- [Android Enterprise](../protect/compliance-policy-create-android-for-work.md)
- [Android Open-Source Project (AOSP)](../protect/compliance-policy-create-android-aosp.md) 
- [iOS](../protect/compliance-policy-create-ios.md)
- [macOS](../protect/compliance-policy-create-mac-os.md)
- [Windows 10/11](../protect/compliance-policy-create-windows.md)

> [!TIP]  
> In addition to the build-in policy options, Intune supports custom compliance settings for Windows and Linux. This lets you define settings for compliance that are not part of Intune’s built-in policy UI. Custom compliance is treated as an advanced compliance configuration. Linux is supported only through custom compliance settings.

When ready to create policies, see [Create a policy](../protect/create-compliance-policy.md). Your policies can also include [Actions for noncompliance](../protect/actions-for-noncompliance.md) that can help users bring their devices into compliance or lock a device that might be at risk. Actions your Intune compliance policies can initiate include:

- Marking a device as noncompliant.
- Sending email to end users so they can remediate the compliance issue
- Remotely locking noncompliance devices
- Add the device to a list of devices for retirement.
- After your policies roll out to devices, you can then [Monitor device compliance](../protect/compliance-policy-monitor.md) success.

## Advanced compliance policy configurations

✔️ **Add data from Mobile Threat Defense partners to your device compliance policies**  
✔️ **Integrate a third-party compliance partner with Intune**  
✔️ **Define custom compliance settings for Windows and Linux**  
✔️ **Use compliance data with Conditional Access to gate access to your organization’s resources**

With robust device compliance policies in place, you can then implement more advanced compliance options, including:

- Integrate device compliance status with Conditional Access to help gate which devices are allowed to access email, other cloud services, or on-premises resources.
- Expand your device compliance policies by defining [Custom compliance settings](../protect/compliance-use-custom-settings.md) that aren't available natively through the Intune compliance policy UI.
- Include compliance data from third-party compliance partners, when Intune isn’t your Mobile Device Management authority. With such a configuration, compliance data from those devices can be used with your conditional access policies](../protect/device-compliance-get-started#integrate-with-conditional-access.md).
- Use data [Mobile Threat Defense partners](../protect/mobile-threat-defense.md) as part of your device compliance policies, and in your Conditional Access policies.
