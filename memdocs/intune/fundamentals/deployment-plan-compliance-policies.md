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

Previously, you’ve set up your Intune subscription and created app protection policies. Next, plan for and configure device compliance settings and policies to help protect organizational data by requiring devices to meet requirements that you set. If you’re not yet familiar with compliance policies, see [Compliance overview](../protect/device-compliance-get-started.md).

You deploy compliance policies to groups of devices or users. When deployed to users, any device the user signs into must then meet the policies requirements. Some common examples of compliance requirements include:

- Requiring a minimum operating system version
- Use of a password or PIN that meets certain complexity and length requirements
- A device being at or below a *threat level* as determined by mobile threat defense software you use. Mobile threat defense software includes Microsoft Defender for Endpoint or one of Intune’s other supported partners.

When devices fail to meet the requirements of a compliance policy, that policy can apply one or more *actions for noncompliance*. Some actions include:

- Remotely locking the noncompliant device.
- Send email or notifications to the device or user about the compliance issue, so a device user can bring it back into compliance.
- Identify a device that might be ready for retirement should it remain out of compliance for an extended time.
When you're planning for and deploying your compliance policies, it can help to approach compliance policies through our recommendations through different levels. We recommend starting with the minimal compliance settings, which are common to most or all platforms, and then expanding by adding more advanced configurations and integrations that provide more capabilities.

Because different device platforms support different compliance capabilities or use different names for similar settings, listing each option is beyond this deployment plan. Instead, we’ll provide categories and examples of settings in those categories for each of the following levels:

- **Level 1** – [**Minimal device compliance**](#minimal-devcie-compliance). These are configurations that we recommend all tenants have in place.
- **Level 2** – [**Enhanced device compliance settings**](#enhanced-device-compliance-settings). These include common device configurations such as encryption, or system level file protections.  
- **Level 3** – [**Advanced device compliance configurations**](#advanced-device-compliance-configurations). High level recommendations include those that require deeper integration with other products, such as Conditional Access from Azure AD.

Generally, our recommendations place well understood and simple to implement settings at lower levels, providing a strong return for that investment. Settings listed for at higher levels can involve more complexity, such as settings that require integration of third-party products. Be sure to review all the range recommendations and be ready to adjust your own deployment plan to fit your organization’s needs and expectations.

## Minimal device compliance

✔️ Configure tenant-wide Compliance policy settings  
✔️ Set up responses for noncompliance devices (Actions for noncompliance)  
✔️ Establish a core set of compliance settings across platforms you support  
✔️ Understand how device compliance and device configuration policies interact  

The minimal device compliance settings includes the following subjects that all tenants who plan to use compliance policies should understand and be prepared to use:

- *Compliance policy settings* – Tenant-wide settings that affect how the Intune compliance service works with your devices.
- *Actions for noncompliance* – These configurations are common to all device compliance policies.
- *Minimal device compliance policy recommendations* – Thees are the platform specific device compliance settings we believe every tenant should implement to help keep their organizations resources safe.

In addition, we recommend you be familiar with how device compliance policies and device configuration policies are related, and interact.

### Compliance policy settings

All organizations should review and set the tenant-wide  *compliance policy settings*. These settings are foundational to supporting platform specific policies. They can also mark devices that haven't evaluated a compliance policy as noncompliant, which can help you protect your organization from new or unknown devices that might fail to meet your security expectations.

- Compliance policy settings are a few configurations you make at the tenant-level that then apply to all devices. They establish how the Intune compliance service functions for your tenant.
- These settings are configured directly in the Microsoft Endpoint Manager admin center. This is in contrast to device compliance policies that you create for a specific platform, that support different configurations for the same setting through separate policies, and that deploy to discreet groups of devices or users.

To learn more about Compliance Policy Settings at the tenant level, and how to configure them, see [Compliance policy settings](../protect/device-compliance-get-started.md#compliance-policy-settings).

### Actions for noncompliance

Each device compliance policy includes *actions for noncompliance*, which are one or more time-ordered actions that are applied to devices that fail to meet the compliance requirements of the policy. By default, marking a device as noncompliant is an immediate action that’s included in each policy.

For each action you add, you define how long to wait after a device is marked as noncompliant before that action runs.

Available actions you can configure include the following, but not all are available for each device platform:

- **Mark device non-compliant** (default action for all policies)
- **Send push notification to end user**
- **Send email to end user**
- **Remotely lock the noncompliant device**
- **Retire the noncompliant device**

Policy administrators should understand the available options for each action and complete supporting configurations before deploying a policy that requires them. For example, before you can add the  *send email*  action, you must first create one or more email templates with the messages you might want to send. Such an email might include resources to help the user bring their device into compliance. Later, when defining an email action for a policy you can select one of your templates to use with a specific action.

Because each non-default action can be added to a policy multiple times, each with a separate configuration, you can customize how the actions will apply.

For example, you could configure several related actions to occur in a sequence. First, immediately upon being noncompliant you might have Intune send an email to the device’s user, and perhaps an administrator as well. Then a few days later, a second action could send a different email reminder, with details about a deadline for remediating the device. You might also configure a final action to add a device to a list of devices you might want to retire, with the action set to run only after a device continues to remain noncompliant for an excessive period.

While compliance policy can mark a device as noncompliant, you’ll also need a plan for how to remediate noncompliant devices. This could include admins using noncompliant device status to request updates or configurations be made to a device. To provide general guidance to device users, you can configure the *send email to end user* action for noncompliance to include useful tips or contacts for resolving a device compliance issue.

To learn more, see [Actions for noncompliance](../protect/actions-for-noncompliance.md).

### Minimal compliance policy recommendations

After you establish tenant-wide compliance policy settings and establish communications or rules for actions for noncompliant devices, you're likely ready to create and deploy device compliance policies to discrete groups of devices or users.

Before you deploy compliance policies, sync on the expected configurations for settings that overlap between device configuration and device compliance teams. Ensure the two policy types agree on the correct configuration, which can help avoid policy conflicts, over enforcement, or for devices to lack the minimal configurations expected by your organization.

To configure policies, see [Create a compliance policy](../protect/create-compliance-policy.md).

We recommend using the following settings in your minimal device compliance policy:

| Compliance category and examples             | Details                                       |
|---------------------------------------------|------------------------------------------------------------|
| **Operating System versions** </br></br> **All devices**: Evaluate settings and values for operating system versions, including: </br>- Minimum OS  </br>- Maximum OS </br>- OS patch levels </br>- Minor and Major build versions  | Use available settings that define a minimum allowed OS version or build and important patch levels to ensure device operating systems are current and secure. </br></br> Maximum OS settings can help identify new but untested results, and beta or developer OS builds that could introduce unknown risks. </br></br> Windows supports an additional setting to set granular ranges, which is included in the advanced compliance level. |
| **Password configurations** </br></br> **All devices**: Evaluate devices for password structure and length. Common settings  including: </br>- Require a password  or Pin to unlock devices. </br>-Require complex passwords that use combinations of letters, numbers, and symbols. </br>- Set requirements for a minimum password length. </br>- Enforce settings that lock the screen after a period of inactivity, requiring a password or PIN to unlock.| Use compliance to identify devices that lack passwords or use simple passwords  that don’t meet complexity and length requirement that can help protect access to the device.  </br></br> Other options like password reuse or length of time before a password must be changed are explicitly included at the enhanced compliance level.  |
| **Antivirus**, **Antispyware**, and **Antimalware** </br></br> **Windows**: Evaluate devices for solutions that register with Windows Security Center to be on and monitoring for: </br>- Antivirus </br>- Antispyware </br>- Microsoft Defender Antimalware </br></br> **Other platforms**: Compliance policies for platforms other than Windows don't include evaluation for these solutions. | Active solutions for Antivirus, Antispyware, and Antimalware solutions are important.</br></br> Windows compliance policy can assess the state of these solutions when they're active and registered  register with Windows Security Center on a device. </br></br>Non-Windows platforms should still run solutions for antivirus, antispyware, and antimalware, even though Intune compliance policies lack options to evaluate their active presence.  |

### Understand how device compliance and device configuration policies interact

Before diving into compliance policy recommendations by levels, it’s important  to understand the sometimes-close relationship between compliance policies and device configuration policies. With awareness of these interactions, you can better plan for and deploy successful policies for both feature areas.

- Device configuration policies configure devices to use specific configurations. These settings can range across all aspects of the device.
- Device compliance policies focus on a subset of device configurations that are related to security.

Devices that receive compliance policies are  evaluated against the compliance policy configurations with results returned to Intune for possible actions. Some compliance configurations like password requirements result in enforcement on the device, even when device configurations are more lenient.

When a device receives conflicting configurations for a setting either different or similar policy types, conflicts can occur. To help prepare for this scenario, see [If multiple policies are assigned to the same user or device, how do I know which settings gets applied?](../configuration/device-profile-troubleshoot.md#if-multiple-policies-are-assigned-to-the-same-user-or-device-how-do-i-know-which-settings-gets-applied)



## Enhanced device compliance settings

✔️ Deploy device configuration policies for each platform type





> [!NOTE]
> IN PROGRESS > Content after this note is very rough intial draft, and pending further updates - which will align more closely the recent updates above this note] 




Use device compliance policies to identify when devices that will access your apps and data are in a state that meets your organization’s requirements. These policies support a range of settings that are specific to each platform. Some compliance settings evaluate and report back a status for that device. Other settings can function more like device configuration settings by enforcing a requirement, such as those for password complexity or PIN requirements.

Before creating a series of policies:

- Identify some minimum compliance expectations for your organization. With expectations for device compliance in mind, you can then configure and deploy device configuration policies to support your goals. Requirements and criteria for settings will vary from organization to organization, and in some cases between different groups of users or devices within an organization. Following are some common settings to consider as a start, regardless of the platform type like Windows, iOS/iPadOS, or Android:

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

## Advanced device compliance configurations

✔️ **Add data from Mobile Threat Defense partners to your device compliance policies**  
✔️ **Integrate a third-party compliance partner with Intune**  
✔️ **Define custom compliance settings for Windows and Linux**  
✔️ **Use compliance data with Conditional Access to gate access to your organization’s resources**

With robust device compliance policies in place, you can then implement more advanced compliance options, including:

- Integrate device compliance status with Conditional Access to help gate which devices are allowed to access email, other cloud services, or on-premises resources.
- Expand your device compliance policies by defining [Custom compliance settings](../protect/compliance-use-custom-settings.md) that aren't available natively through the Intune compliance policy UI.
- Include compliance data from third-party compliance partners, when Intune isn’t your Mobile Device Management authority. With such a configuration, compliance data from those devices can be used with your conditional access policies](../protect/device-compliance-get-started#integrate-with-conditional-access.md).
- Use data [Mobile Threat Defense partners](../protect/mobile-threat-defense.md) as part of your device compliance policies, and in your Conditional Access policies.
