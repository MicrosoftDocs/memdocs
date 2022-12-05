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

Previously, you’ve set up your Intune subscription and created app protection policies. In this step, you’ll configure device compliance settings and policies to help protect organizational data by requiring devices to meet requirements that you set. You deploy these policies directly to devices, or to users so that any device they use must also meet your requirements. Examples of requirements include:  

- Minimum operating system versions for different platforms
- Password or PIN requirements like complexity and length
- Devices being at or below a *threat level* as determined by mobile threat defense software you use, like Microsoft Defender for Endpoint, or one of Intune’s other supported partners.

Your compliance policies can also take some *actions* when a device fails to meet your requirements, including:

- Remotely lock a noncompliant device.
- Send email or notifications to a device or user, so the device user can bring it into compliance.
- Identify a device that might be ready for retirement when it remains out of compliance for some time.

If you use Conditional Access, your Conditional Access policies can use the results of your device compliance policies to determine which devices can access your organizational resources. This access control is separate from the *actions for noncompliance* that you include in your device compliance policies.

The following sections describe considerations for increasing complexity for device compliance management. While there's no single path or groups of settings that fit all customers, we believe everyone should start by establishing the tenant-wide configurations that define how the Intune compliance service interacts with devices. Those settings can then be followed by:

- Adding platform-specific device configuration policies to enforce your device compliance goals.
- Establishing deeper protections by integrating device Mobile Threat Defense partners, like Microsoft Defender for Endpoint.
- Configuring a third-party compliance partner if you use one as your Mobile Device Management authority.
- Deploying Azure Active Directory (Azure AD) Conditional Access policies that use device compliance status to gate which devices have access to resources.
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

Set tenant-wide compliance settings that establish how Intune’s compliance service will interact with devices. These settings are a foundation that’s distinct from settings you configure in platform specific device compliance policies. This foundation is the base on which you can build robust device compliance policies and conditional access integration.

Tenant-wide settings are configured as *Compliance policy settings*:

- Set **Mark devices with no compliance policy assigned as** to be **noncompliant**. This configuration is required if you plan to use compliance policies to help protect your organizations resources from unauthorized access. This configuration supports integrating compliance policies with Conditional Access so you can gate which users and devices can access company resources.

- If you’ll support access from iOS/iPad devices, consider setting **Enhanced jailbreak detection** to **Enabled**. This enhances the device compliance policy setting *block jailbroken devices* by adding extra criteria for when to run detection. With the device compliance setting and this tenant-wide setting enabled, jailbreak detection runs when: 
  - The Company Portal app opens.
  - The device physically moves a significant distance, which is approximately 500 meters or more. Intune can’t guarantee that each significant location change results in a jailbreak detection check, as the check depends on a device's network connection at the time.

  On iOS 13 and higher, users must select *Always Allow* whenever the device prompts them to continue allowing Company Portal to use their location in the background. If enabled, this will allow more frequent jailbreak detection checks.

b. Configure **Compliance status validity period (days)** to have Intune mark devices as noncompliant when they’ve failed to report a compliance status for longer than the configured time. By being marked noncompliant, devices that might otherwise have access to your organizations resources and be blocked or identified for other actions such as retiring to remove them from management altogether.

To learn more about Compliance Policy Settings at the tenant level, and how to configure them, see [Compliance policy settings](../protect/device-compliance-get-started.md#compliance-policy-settings)

## Core device compliance policy

✔️ **Identify your organizations desired compliance configurations for device platform**  
✔️ **Deploy device configuration policies for each platform type**

You want to be sure that the devices that access your apps and data meet your organization’s requirements, like device password complexity or being pin-protected. You also want device operating systems to remain are up to date. To support such goals, you must first identify some minimum compliance expectations, and then deploy device configuration policies to evaluate devices against that criteria. These criteria will vary from organization to organization, but the following are some common settings to consider as a start, regardless of the platform type like Windows, iOS/iPadOS, or Android:

- Password complexity
- *Example 2*
- *Example 3*

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
