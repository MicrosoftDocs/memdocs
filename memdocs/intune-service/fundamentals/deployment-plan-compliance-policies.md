---
# required metadata

title: Configure compliance policies
titleSuffix: Microsoft Intune
description: Description for configuring compliance policies
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 11/22/2023
ms.topic: how-to
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
- tier1
---
<!-- >
# Configure compliance policies

## Recommended compliance policies - basic

## Recommended compliance policies - advanced?

### tunnel?

### certificates?

### Defender for Endpoint

### Conditional Access ?
-->

# Step 3 – Plan for compliance policies

Previously, you set up your Intune subscription and created app protection policies. Next, plan for and configure device compliance settings and policies to help protect organizational data by requiring devices to meet requirements that you set.

:::image type="content" source="./media/deployment-plan-compliance-policies/deployment-plan-compliance-conditional-access.png" alt-text="Diagram that shows getting started with Microsoft Intune with step 3, which is creating compliance and Conditional Access policies.":::

If you’re not yet familiar with compliance policies, see [Compliance overview](../protect/device-compliance-get-started.md).

This article applies to:

- Android Enterprise (Fully Managed, and Personally owned work profiles)
- Android Open-Source Project (AOSP)
- iOS/iPadOS
- Linux
- macOS
- Windows

You deploy compliance policies to groups of devices or users. When deployed to users, any device the user signs into must then meet the policies requirements. Some common examples of compliance requirements include:

- Requiring a minimum operating system version.
- Use of a password or PIN that meets certain complexity and length requirements.
- A device being at or below a *threat level* as determined by mobile threat defense software you use. Mobile threat defense software includes Microsoft Defender for Endpoint or one of Intune’s other supported partners.

When devices fail to meet the requirements of a compliance policy, that policy can apply one or more *actions for noncompliance*. Some actions include:

- Remotely locking the noncompliant device.
- Send email or notifications to the device or user about the compliance issue, so a device user can bring it back into compliance.
- Identify a device that might be ready for retirement should it remain out of compliance for an extended time.
When you're planning for and deploying your compliance policies, it can help to approach compliance policies through our recommendations through different levels. We recommend starting with the minimal compliance settings, which are common to most or all platforms, and then expanding by adding more advanced configurations and integrations that provide more capabilities.

Because different device platforms support different compliance capabilities or use different names for similar settings, listing each option is beyond this deployment plan. Instead, we provide categories and examples of settings in those categories for each of the following levels:

- **Level 1** – [**Minimal device compliance**](#level-1---minimal-device-compliance). This category includes configurations that we recommend all tenants have in place.
- **Level 2** – [**Enhanced device compliance settings**](#level-2---enhanced-device-compliance-settings). These include common device configurations such as encryption, or system level file protections.  
- **Level 3** – [**Advanced device compliance configurations**](#level-3---advanced-device-compliance-configurations). High level recommendations include configurations that require deeper integration with other products, such as Microsoft Entra Conditional Access.

Generally, our recommendations place settings that are considered key configurations that are common across platforms at the minimal compliance level, providing a strong return for your investment. Settings listed for at higher levels can involve more complexity, such as settings that require integration of third-party products. Be sure to review all the range recommendations and be ready to adjust your own deployment plan to fit your organization’s needs and expectations.

The following articles can help you understand the settings that Intune policies natively support:

- [Android device administrator](../protect/compliance-policy-create-android.md)
- [Android Enterprise](../protect/compliance-policy-create-android-for-work.md)
- [Android Open-Source Project (AOSP)](../protect/compliance-policy-create-android-aosp.md)
- [iOS](../protect/compliance-policy-create-ios.md)
- [macOS](../protect/compliance-policy-create-mac-os.md)
- [Windows 10/11](../protect/compliance-policy-create-windows.md)

## Level 1 - Minimal device compliance

✔️ **Configure tenant-wide Compliance policy settings**  
✔️ **Set up responses for noncompliance devices (Actions for noncompliance)**  
✔️ **Understand how device compliance and device configuration policies interact**  
✔️ **Use a core set of minimal compliance settings across platforms you support**  

The minimal device compliance settings include the following subjects that all tenants who plan to use compliance policies should understand and be prepared to use:

- *Compliance policy settings* – Tenant-wide settings that affect how the Intune compliance service works with your devices.
- *Actions for noncompliance* – These configurations are common to all device compliance policies.
- *Minimal device compliance policy recommendations* – This category includes the platform specific device compliance settings we believe every tenant should implement to help keep their organizations resources safe.

In addition, we recommend you be familiar with how device compliance policies and device configuration policies are related and interact.

### Compliance policy settings

All organizations should review and set the tenant-wide  *compliance policy settings*. These settings are foundational to supporting platform specific policies. They can also mark devices that haven't evaluated a compliance policy as noncompliant, which can help you protect your organization from new or unknown devices that might fail to meet your security expectations.

- Compliance policy settings are a few configurations you make at the tenant-level that then apply to all devices. They establish how the Intune compliance service functions for your tenant.
- These settings are configured directly in the Microsoft Intune admin center and are distinct from  device compliance policies that you create for specific platforms and deploy to discreet groups of devices or users.

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

Because each non-default action can be added to a policy multiple times, each with a separate configuration, you can customize how the actions apply.

For example, you could configure several related actions to occur in a sequence. First, immediately upon being noncompliant you might have Intune send an email to the device’s user, and perhaps an administrator as well. Then a few days later, a second action could send a different email reminder, with details about a deadline for remediating the device. You might also configure a final action to add a device to a list of devices you might want to retire, with the action set to run only after a device continues to remain noncompliant for an excessive period.

While compliance policy can mark a device as noncompliant, you also need a plan for how to remediate noncompliant devices. This plan could include admins using noncompliant device status to request updates or configurations be made to a device. To provide general guidance to device users, you can configure the *send email to end user* action for noncompliance to include useful tips or contacts for resolving a device compliance issue.

To learn more, see [Actions for noncompliance](../protect/actions-for-noncompliance.md).

### Understand how device compliance and device configuration policies interact

Before diving into compliance policy recommendations by levels, it’s important  to understand the sometimes-close relationship between compliance policies and device configuration policies. With awareness of these interactions, you can better plan for and deploy successful policies for both feature areas.

- Device configuration policies configure devices to use specific configurations. These settings can range across all aspects of the device.
- Device compliance policies focus on a subset of device configurations that are related to security.

Devices that receive compliance policies are  evaluated against the compliance policy configurations with results returned to Intune for possible actions. Some compliance configurations like password requirements result in enforcement on the device, even when device configurations are more lenient.

When a device receives conflicting configurations for a setting either different or similar policy types, conflicts can occur. To help prepare for this scenario, see [Compliance and device configuration policies that conflict](../configuration/device-profile-troubleshoot.md#compliance-and-device-configuration-policies-that-conflict)

Consider synchronizing any planned configurations between device configuration and device compliance teams to help identify configuration overlaps. Ensure the two policy types agree on the same configuration for targeted devices as this can help avoid policy conflicts or leaving a device without the configuration or resource access you expect.

### Minimal compliance settings

After you establish tenant-wide compliance policy settings and establish communications or rules for actions for noncompliant devices, you're likely ready to create and deploy device compliance policies to discrete groups of devices or users.

Review the platform specific policies in the Microsoft Intune admin center to identify which compliance settings are available for each platform and more details about their use. To configure policies, see [Create a compliance policy](../protect/create-compliance-policy.md).

We recommend using the following settings in your minimal device compliance policies:

| Minimal device compliance categories and examples    | Information     |
|------------------------------------------------------|-----------------|
| **Antivirus**, **Antispyware**, and **Antimalware** </br></br> **Windows**: </br> Evaluate devices for solutions that register with Windows Security Center to be on and monitoring for: </br>- Antivirus </br>- Antispyware </br>- Microsoft Defender Antimalware </br></br> **Other platforms**: </br> Compliance policies for platforms other than Windows don't include evaluation for these solutions. | Active solutions for Antivirus, Antispyware, and Antimalware solutions are important.</br></br> Windows compliance policy can assess the state of these solutions when they're active and registered  register with Windows Security Center on a device. </br></br>Non-Windows platforms should still run solutions for antivirus, antispyware, and antimalware, even though Intune compliance policies lack options to evaluate their active presence.  |
| **Operating System versions** </br></br> **All devices**: </br> Evaluate settings and values for operating system versions, including: </br> - Maximum OS </br> - Minimum OS  </br>- Minor and Major build versions  </br>- OS patch levels | Use available settings that define a minimum allowed OS version or build and important patch levels to ensure device operating systems are current and secure. </br></br> Maximum OS settings can help identify new but untested results, and beta or developer OS builds that could introduce unknown risks. </br></br> Linux supports an option to define the Linux distribution type, like Ubuntu. </br></br> Windows supports another setting to set supported build ranges.  |
| **Password configurations** </br></br> **All devices**:</br> - Enforce settings that lock the screen after a period of inactivity, requiring a password or PIN to unlock. </br>  - Require complex passwords that use combinations of letters, numbers, and symbols. </br>- Require a password  or Pin to unlock devices. </br> - Set requirements for a minimum password length. | Use compliance to evaluate devices for password structure and length, and to identify devices that lack passwords or use simple passwords. These settings can help protect access to the device. </br></br> Other options like password reuse or length of time before a password must be changed are explicitly included at the enhanced compliance level.  |

## Level 2 - Enhanced device compliance settings

✔️ **Use enhanced device configuration policies for supported platform types**

### Enhanced compliance settings

Support for enhanced level compliance settings varies greatly by platform as compared to the settings found in the minimal recommendations. Some platforms might not support settings that are supported by related platforms. For example, Android AOSP lacks options that exist for Android Enterprise platforms to configure compliance for system level file and boot protections.

Review the platform specific policies in the Microsoft Intune admin center to identify which compliance settings are available for each platform and more details about their use. To configure policies, see [Create a compliance policy](../protect/create-compliance-policy.md).

We recommend using the following settings in your enhanced device compliance policies:

| Enhanced device compliance categories and examples    | Information     |
|-------------------------------------------------------|-----------------|
| **Applications** </br></br> **Android Enterprise**:</br> - Block apps from unknown sources</br> - Company Portal app runtime integrity </br>  - Manage source locations for apps </br>  - Google Play services  </br> - SafteyNet options for attestation and evaluation  </br></br> **iOS/iPadOS** </br> - Restricted apps</br></br> **macOS**:</br> - Allow apps from specific locations</br> - Block apps from unknown sources</br> - Firewall settings</br></br> **Windows**:</br> - Block apps from unknown sources</br> - Firewall settings  |  Configure  requirements for various applications. </br></br> For Android, manage the use and operation of  applications like Google Play, SafteyNet, and evaluation of the Company Portal app runtime integrity. </br></br> For all platforms, when supported,  manage where apps can be installed from, and which apps shouldn't be allowed on devices that access your organizations resources. </br></br> For macOS and Windows, compliance settings support requiring an active and configured Firewall.  |
| **Encryption**</br></br> **Android Enterprise**:</br> - Require encryption of data storage</br></br> **Android AOSP**:</br> - Require encryption of data storage</br></br> **macOS**:</br> - Require encryption of data storage</br></br> **Linux**: </br> - Require encryption of data storage</br></br> **Windows**:</br> - Require encryption of data storage</br> - BitLocker  | Add compliance settings that require the encryption of data storage. Windows also supports requiring use of BitLocker.  |
| **Password configurations** </br></br> **Android Enterprise**:</br> - Password expiration, and reuse</br></br> **iOS/iPadOS**: </br> - Password expiration, and reuse</br></br> **macOS**: </br> - Password expiration, and reuse</br></br> **Windows**: </br>- Password expiration, and reuse  | Add password compliance settings to ensure passwords are rotated periodically, and that passwords aren't reused frequently.  |
| **System level file and boot protection** </br></br> **Android AOSP**:</br> - Rooted devices </br></br> **Android Enterprise**: </br> - Block USB debugging on device</br> - Rooted devices  </br></br> **iOS/iPadOS** </br> - Jailbroken devices</br></br> **macOS**:</br> - Require system integrity protection </br></br> **Windows**:</br>  - Require code integrity</br> - Require Secure Boot to be enabled on the device</br> - Trusted Platform Module (TPM)  | Configure the platform specific options that evaluate devices for system level or kernel level risks.  |

## Level 3 - Advanced device compliance configurations

✔️ **Add data from Mobile Threat Defense partners to your device compliance policies**  
✔️ **Integrate a third-party compliance partner with Intune**  
✔️ **Define custom compliance settings for Windows and Linux**  
✔️ **Use compliance data with Conditional Access to gate access to your organization’s resources**  
✔️ **Use advanced device configuration policies for supported platform types**

With robust device compliance policies in place, you can then implement more advanced compliance options that go beyond only configuring settings in device compliance policies, including:

- Using data from *Mobile Threat Defense partners* as part of your device compliance policies, and in your Conditional Access policies.  <!-- [Mobile Threat Defense partners](../protect/mobile-threat-defense.md) -->

- Integrating device compliance status with *Conditional Access* to help gate which devices are allowed to access email, other cloud services, or on-premises resources.

- Including compliance data from *third-party compliance partners*. With such a configuration, compliance data from those devices can be used with your [Conditional Access policies](../protect/device-compliance-get-started.md#integrate-with-conditional-access).

- Expanding on built-in device compliance policies by defining custom compliance settings that aren't available natively through the Intune compliance policy UI. <!-- [Custom compliance settings](../protect/compliance-use-custom-settings.md) -->

### Integrate data from a Mobile Threat Defense partner

A Mobile Threat Defense (MTD) solution is software for mobile devices that helps to secure them from various cyber threats. By protecting mobile devices, you help protect your organization and resources. When integrated, MTD solutions provide an additional information source to Intune for your device compliance policies. This information can also be used by Conditional Access rules you can use with Intune.

When integrated, Intune supports use of MTD solutions with enrolled devices, and when supported by the MTD solution, unenrolled devices by using [Microsoft Intune protected apps](../apps/apps-supported-intune-apps.md) and app protection policies.

Be sure to use an MTD partner that is  [supported by Intune](../protect/mobile-threat-defense.md#mobile-threat-defense-partners) and that supports the capabilities your organization needs on the full range of platforms you use.

For example, [Microsoft Defender for Endpoint](../protect/advanced-threat-protection.md) is a Mobile Threat Defense solution you might already use that can be used with the Android, iOS/iPadOS, and Windows platforms. Other solutions, typically support Android and iOS/iPadOS. See [Mobile Threat Defense partners](../protect/mobile-threat-defense.md) to view the list of supported MTD partners.

To learn more about using Mobile Threat Defense software with Intune, start with [Mobile Threat Defense integration with Intune](../protect/mobile-threat-defense.md).

### Use data from third-party compliance partners

Intune supports the use of third-party compliance partners where the partner serves as the mobile device management (MDM) authority for a group of devices. When you use a supported compliance partner, you use that partner to configure device compliance for the devices that solution manages. You also configure that partner solution to pass the compliance results to Intune, which then stores that data in Microsoft Entra ID along with compliance data from Intune. The third-party compliance data is then available for use by Intune when evaluating device compliance policies, and for use by Conditional Access policies.

In some environments, Intune might serve as the only MDM authority you need to use, as by default, Intune is a registered compliance partner for the Android, iOS/iPadOS, and Windows platforms. Other platforms require other compliance partners to serve as a devices MDM authority, like use of Jamf Pro for macOS devices.

If you use a third-party device compliance partner in your environment, ensure they're [supported with Intune](../protect/device-compliance-partners.md#supported-device-compliance-partners). To add support, you configure a [connection for the partner](../protect/device-compliance-partners.md#configure-intune-to-work-with-a-device-compliance-partner) from within the Microsoft Intune admin center, and follow that partners documentation to complete the integration.

For more information on this subject, see [Support third-party device compliance partners in Intune](../protect/device-compliance-partners.md).

### Use custom compliance settings

You can expand on Intune’s built-in device compliance options by configuring custom compliance settings for managed Linux and Windows devices.

Custom settings give you the flexibility to base compliance on the settings that are available on a device without having to wait for Intune to add these settings.

To use custom compliance, you must configure a .JSON file that defines values on the device to use for compliance, and a discovery script that runs on the device to evaluate the settings from the JSON.

To learn more about perquisites, supported platforms, and the JSON and script configurations required for custom compliance, see [Use custom compliance policies and settings for Linux and Windows devices with Microsoft Intune](../ protect/compliance-use-custom-settings.md).

### Integrate compliance with Conditional Access

Conditional Access is a Microsoft Entra capability that works with Intune to help protect devices. For devices that register with Microsoft Entra, Conditional Access policies can use device and compliance details from Intune to enforce access decisions for users and devices.

Combine Conditional Access policy with:

- [Device compliance policies](../protect/create-conditional-access-intune.md) can require a device be marked as compliant before that device can be used to access your organization’s resources. The Conditional Access policies specify apps services you want to protect, conditions under which the apps or services can be accessed, and the users the policy applies to.
- [App protection policies](../protect/app-based-conditional-access-intune.md) can add a security layer that ensures only client apps that support Intune app protection policies can access your online resources, like Exchange or other Microsoft 365 services.

Conditional Access also works with the following to help you keep devices secure:

- Microsoft Defender for Endpoint and third-party MTD apps
- Device compliance partner apps
- Microsoft Tunnel

To learn more, see [Learn about Conditional Access and Intune](../protect/conditional-access.md).

### Advanced compliance settings

Review the platform specific policies in the Microsoft Intune admin center to identify which compliance settings are available for each platform and more details about their use. To configure policies, see [Create a compliance policy](../protect/create-compliance-policy.md).

To configure policies, see [Create a compliance policy](../protect/create-compliance-policy.md).

We recommend using the following settings in your enhanced device compliance policies:

| Advanced device compliance categories and examples    | Information     |
|-------------------------------------------------------|-----------------|
| **Runtime defenses** </br></br> **Android Enterprise**: </br> - Require the device to be at or under the Device Threat Level </br> - Require the device to be at or under the machine risk score </br></br> **iOS/iPadOS**:</br>  - Require the device to be at or under the Device Threat Level </br> - Require the device to be at or under the machine risk score</br></br> **Windows**: </br> - Require the device to be at or under the machine risk score |When you integrate Intune with a Mobile Threat Defense partner, you can use that partners device threat level evaluation as criteria in your compliance policies.  </br></br> When you've integrated Microsoft Defender for Endpoint with Intune, you can use the risk score from Defender as a compliance check.  |

## Follow the minimum recommended baseline policies

1. [Set up Microsoft Intune](deployment-plan-setup.md)
2. [Add, configure, and protect apps](deployment-plan-protect-apps.md)
3. 🡺 **Plan for compliance policies** (*You are here*)
4. [Configure device features](deployment-plan-configuration-profile.md)
5. [Enroll devices](deployment-guide-enroll.md)
