---
# required metadata

title: Device compliance policies in Microsoft Intune - Azure | Microsoft Docs
description: Get started with use device compliance policies, overview of status and severity levels, using the InGracePeriod status, working with Conditional Access, and handling devices without an assigned policy.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 02/13/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.reviewer: samyada

# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Set rules on devices to allow access to resources in your organization using Intune

Many mobile device management (MDM) solutions help protect organizational data by requiring users and devices to meet some requirements. In Intune, this feature is called "compliance policies". Compliance policies define the rules and settings that users and devices must meet to be compliant. When combined with Conditional Access, administrators can block users and devices that don't meet the rules.

For example, an Intune administrator can require:

- End users use a password to access organizational data on mobile devices
- The device isn't jail-broken or rooted
- A minimum or maximum operating system version on the device
- The device to be at, or under a threat level

You can also use this feature to monitor the compliance status on devices in your organization.

> [!IMPORTANT]
> Intune follows the device check-in schedule for all compliance evaluations on the device. [Policy and profile refresh cycles](../configuration/device-profile-troubleshoot.md#how-long-does-it-take-for-devices-to-get-a-policy-profile-or-app-after-they-are-assigned) lists the estimated refresh times.

<!---### Actions for noncompliance

You can specify what needs to happen when a device is determined as noncompliant. This can be a sequence of actions during a specific time.
When you specify these actions, Intune will automatically initiate them in the sequence you specify. See the following example of a sequence of
actions for a device that continues to be in the noncompliant status for
a week:

- When the device is first determined to be noncompliant, an email with noncompliant notification is sent to the user.

- 3 days after initial noncompliance state, a follow up reminder is sent to the user.

- 5 days after initial noncompliance state, a final reminder with a notification that access to company resources will be blocked on the device in 2 days if the compliance issues are not remediated is sent to the user.

- 7 days after initial noncompliance state, access to company resources is blocked. This requires that you have Conditional Access policy that specifies that access from noncompliant devices should    be blocked for services such as Exchange and SharePoint.

### Grace Period

This is the time between when a device is first determined as
noncompliant to when access to company resources on that device is blocked. This time allows for time that the user has to resolve
compliance issues on the device. You can also use this time to create your action sequences to send notifications to the user before their access is blocked.

Remember that you need to implement Conditional Access policies in addition to compliance policies in order for access to company resources to be blocked.--->

## Device compliance policies work with Azure AD

Intune uses Azure Active Directory (AD) [Conditional Access](https://docs.microsoft.com/azure/active-directory/conditional-access/overview) (opens another docs web site) to help enforce compliance. When a device enrolls in Intune, the Azure AD registration process starts, and device information is updated in Azure AD. One key piece of information is the device compliance status. This compliance status is used by Conditional Access policies to block or allow access to e-mail and other organization resources.

- [What is device management in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/device-management-introduction) is a great resource on why and how devices are registered in Azure AD.

- [Conditional Access](conditional-access.md) and [common ways to use Conditional Access](conditional-access-intune-common-ways-use.md) describe this feature as it relates to Intune.

## Ways to use device compliance policies

### With Conditional Access

For devices that comply to policy rules, you can give those devices access to email and other organization resources. If the devices don't comply to policy rules, then they don't get access to organization resources. This is Conditional Access.

### Without Conditional Access

You can also use device compliance policies without any Conditional Access. When you use compliance policies independently, the targeted devices are evaluated and reported with their compliance status. For example, you can get a report on how many devices aren't encrypted, or which devices are jail-broken or rooted. When you use compliance policies without Conditional Access, there aren't any access restrictions to organization resources.

## Ways to deploy device compliance policies

You can deploy compliance policy to users in user groups or devices in device groups. When a compliance policy is deployed to a user, all of the user's devices are checked for compliance. On Windows 10 version 1803 and newer devices, it's recommended to deploy to device groups *if* the primary user didn't enroll the device. Using device groups in this scenario helps with compliance reporting.

Intune also includes a set of built-in compliance policy settings. The following built-in policies get evaluated on all devices enrolled in Intune:

- **Mark devices with no compliance policy assigned as**: This property has two values:

  - **Compliant** (*default*): security feature off
  - **Not compliant**: security feature on

  If a device doesn't have a compliance policy assigned, then this device is considered compliant by default. If you use Conditional Access with compliance policies, we recommended you change the default setting to **Not compliant**. If an end user isn't compliant because a policy isn't assigned, then the [Company Portal app](../apps/company-portal-app.md) shows `No compliance policies have been assigned`.

- **Enhanced jailbreak detection**: When enabled, this setting causes jailbroken device status to happen more frequently on iOS/iPadOS devices. This setting only affects devices that are targeted with a compliance policy that blocks jailbroken devices. Enabling this property uses the device's location services and may impact battery usage. The user location data isn't stored by Intune and is only used to trigger jailbreak detection more frequently in the background. 

  Enabling this setting requires devices to:
  - Enable location services at the OS level.
  - Always allow the Company Portal to use location services.

  Evaluation is triggered by opening the Company Portal app or physically moving the device a significant distance of approximately 500 meters or more. On iOS 13 and up, this feature will require users to select Always Allow whenever the device prompts them to continue allowing Company Portal to use their location in the background. If users do not always allow location access and have a policy with this setting configured, their device will be marked noncompliant. Note that Intune cannot guarantee that each significant location change will ensure a jailbreak detection check as this depends on a device's network connection at the time.

- **Compliance status validity period (days)**: Enter the time period that devices report the status for all received compliance policies. Devices that don't return the status within this time period are treated as noncompliant. The default value is 30 days. The minimum value is 1 day.

  This setting shows as the **Is active** default compliance policy (**Devices** > **Monitor** > **Setting compliance**). The background task for this policy runs once a day.

You can use these built-in policies to monitor these settings. Intune also [refreshes or checks for updates](create-compliance-policy.md#refresh-cycle-times) at different intervals, depending on the device platform. [Common questions, issues, and resolutions with device policies and profiles in Microsoft Intune](../configuration/device-profile-troubleshoot.md) is a good resource.

Compliance reports are a great way to check the status of devices. [Monitor compliance policies](compliance-policy-monitor.md) includes some guidance.

## Non-compliance and Conditional Access on the different platforms

The following table describes how noncompliant settings are managed when a compliance policy is used with a Conditional Access policy.

---------------------------

|**Policy setting**| **Platform** |
| --- | ----|
| **PIN or password configuration** | - **Android 4.0 and later**: Quarantined<br>- **Samsung Knox Standard 4.0 and later**: Quarantined<br>- **Android Enterprise**: Quarantined  <br>  <br>- **iOS 8.0 and later**: Remediated<br>- **macOS 10.11 and later**: Remediated  <br>  <br>- **Windows 8.1 and later**: Remediated<br>- **Windows Phone 8.1 and later**: Remediated|
| **Device encryption** | - **Android 4.0 and later**: Quarantined<br>- **Samsung Knox Standard 4.0 and later**: Quarantined<br>- **Android Enterprise**: Quarantined<br><br>- **iOS 8.0 and later**: Remediated (by setting PIN)<br>- **macOS 10.11 and later**: Remediated (by setting PIN)<br><br>- **Windows 8.1 and later**: Not applicable<br>- **Windows Phone 8.1 and later**: Remediated |
| **Jailbroken or rooted device** | - **Android 4.0 and later**: Quarantined (not a setting)<br>- **Samsung Knox Standard 4.0 and later**: Quarantined (not a setting)<br>- **Android Enterprise**: Quarantined (not a setting)<br><br>- **iOS 8.0 and later**: Quarantined (not a setting)<br>- **macOS 10.11 and later**: Not applicable<br><br>- **Windows 8.1 and later**: Not applicable<br>- **Windows Phone 8.1 and later**: Not applicable |
| **Email profile** | - **Android 4.0 and later**: Not applicable<br>- **Samsung Knox Standard 4.0 and later**: Not applicable<br>- **Android Enterprise**: Not applicable<br><br>- **iOS 8.0 and later**: Quarantined<br>- **macOS 10.11 and later**: Quarantined<br><br>- **Windows 8.1 and later**: Not applicable<br>- **Windows Phone 8.1 and later**: Not applicable |
| **Minimum OS version** | - **Android 4.0 and later**: Quarantined<br>- **Samsung Knox Standard 4.0 and later**: Quarantined<br>- **Android Enterprise**: Quarantined<br><br>- **iOS 8.0 and later**: Quarantined<br>- **macOS 10.11 and later**: Quarantined<br><br>- **Windows 8.1 and later**: Quarantined<br>- **Windows Phone 8.1 and later**: Quarantined |
| **Maximum OS version** | - **Android 4.0 and later**: Quarantined<br>- **Samsung Knox Standard 4.0 and later**: Quarantined<br>- **Android Enterprise**: Quarantined<br><br>- **iOS 8.0 and later**: Quarantined<br>- **macOS 10.11 and later**: Quarantined<br><br>- **Windows 8.1 and later**: Quarantined<br>- **Windows Phone 8.1 and later**: Quarantined |
| **Windows health attestation** | - **Android 4.0 and later**: Not applicable<br>- **Samsung Knox Standard 4.0 and later**: Not applicable<br>- **Android Enterprise**: Not applicable<br><br>- **iOS 8.0 and later**: Not applicable<br>- **macOS 10.11 and later**: Not applicable<br><br>- **Windows 10 and Windows 10 Mobile**: Quarantined<br>- **Windows 8.1 and later**: Quarantined<br>- **Windows Phone 8.1 and later**: Not applicable |

---------------------------

**Remediated**: The device operating system enforces compliance. For example, the user is forced to set a PIN.

**Quarantined**: The device operating system doesn't enforce compliance. For example, Android and Android Enterprise devices don't force the user to encrypt the device. When the device isn't compliant, the following actions take place:

- If a Conditional Access policy applies to the user, the device is blocked.
- The Company Portal app notifies the user about any compliance problems.

## Next steps

- [Create a policy](create-compliance-policy.md) and view the prerequisites.
- See the compliance settings for the different device platforms:

  - [Android](compliance-policy-create-android.md)
  - [Android Enterprise](compliance-policy-create-android-for-work.md)
  - [iOS](compliance-policy-create-ios.md)
  - [macOS](compliance-policy-create-mac-os.md)
  - [Windows Holographic for Business](compliance-policy-create-windows.md#windows-holographic-for-business)
  - [Windows Phone 8.1](compliance-policy-create-windows-8-1.md)
  - [Windows 8.1 and later](compliance-policy-create-windows-8-1.md)
  - [Windows 10 and later](compliance-policy-create-windows.md)

- [Reference for policy entities](../developer/reports-ref-policy.md) has information about the Intune Data Warehouse policy entities.
