---
# required metadata

title: Create Mobile Threat Defense compliance policies in Intune
titleSuffix: Microsoft Intune
description: Create an Intune device compliance policy that uses your MTD partner threat levels to determine if a mobile device can access company resources.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/30/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.assetid: 5d12254f-ffab-4792-b19c-ab37f5e02f35

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier3
- M365-identity-device-management
- sub-mtd-apps

---

# Create Mobile Threat Defense device compliance policy with Intune

Intune supports integrating a Mobile Threat Defense (MTD) partner to help you detect threats and assess risk on mobile devices. With MTD integration, your Intune device compliance policies can use rules to assess a devices risk based on the information from that MTD partner to determine if a device is compliant or not. With compliance policy risk assessed, you can then use [Conditional Access policy](create-conditional-access-intune.md) to block access to services from devices that fail to meet the requirements of your device compliance policy.

## Before you begin

Before you create Intune device compliance policies that use MTD partner date, you must complete setup and Integration of that MTD partner with Intune.

View the list of [Mobile Threat Defense partners that Intune supports](../protect/mobile-threat-defense.md#mobile-threat-defense-partners) in the *Mobile Threat Defense integration with Intune* article.

- Each link in the supported partner list opens guidance specific to that partner that can help you understand that partners supported the platforms and capabilities.
- Each partner specific article has a companion article that can help you complete the partner integration with Intune and to configure that partner's Intune connector.
- In addition to configuring integration with Intune, use the partner product and console to create policies to classify the threats that the partner identifies. The policies classify threats as having various threat levels like high, medium, and low.

With integration complete and the partner policy in place, you can then create Intune device compliance policies that successfully use the partner threat-level classifications.

## To create an MTD device compliance policy in Intune

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** > **Device compliance** > **Create policy**.

3. Select the **Platform**:
   - For most platforms, the *Profile type* is automatically set. If not automatically set, select the appropriate Profile type.
   - To continue, select **Create**.

4. On **Basics**, specify a device compliance policy **Name**, and **Description** (optional). Select **Next** to continue.

5. On **Compliance settings**, expand and configure **Device Health**. Choose a threat-level from the drop-down list for **Require the device to be at or under the Device Threat Level**.

   - **Secured**: This level is the most secure. The device can't have any threats present and still access company resources. If any threats are found, the device is evaluated as noncompliant.

   - **Low**: The device is compliant if only low-level threats are present. Anything higher puts the device in a noncompliant status.

   - **Medium**: The device is compliant if the threats found on the device are low or medium level. If high-level threats are detected, the device is determined as noncompliant.

   - **High**: This threat level is the least secure as it allows all threat levels and uses Mobile Threat Defense for reporting purposes only. Devices are required to have the MTD app activated with this setting.

   To continue, select **Next**.

6. On the **Actions for noncompliance** tab, specify a sequence of actions to apply automatically to devices that don't meet this compliance policy.

   You can add multiple actions and configure schedules and other details for some actions. For example, you might change the schedule of the default action *Mark device noncompliant* to occur after one day. You can then add an action to send an email to the user when the device isn't compliant to warn them of that status. You can also add actions that lock or retire devices that remain noncompliant.

   For information about the actions you can configure, see [Add actions for noncompliant devices](actions-for-noncompliance.md), including how to create notification emails to send to your users.

7. On the **Assignments** tab, assign the policy to applicable *user* groups, and then select **Next** to continue.

   > [!IMPORTANT]
   >
   > The **Require the device to be at or under the Device Threat Level** setting supports only **user groups**. Targeting *device groups* with this setting is not supported.

8. On the **Review + create** page, when you're done, choose **Create**. The new profile is displayed in the list when you select the policy type for the profile you created.

## Monitoring risk score sent by Mobile Threat Defense partner

Your Mobile Threat Defense partner can send a risk score for each device for which the MTD app is installed. You can view this under **Reports** > **Device compliance** > **Reports** > **Device Compliance**. Make sure **Device threat level** is selected when opening the **Columns** tab, this may require you to hit **Generate** first.

> [!IMPORTANT]
>
> Conditional Access policies for Microsoft 365 or other services also evaluate device compliance results, which include the threat-level configuration. Any noncompliant device can be blocked from accessing corporate resources until that devices threat-level is remediated to bring the device into compliance with your policies and that status is successfully reported to Intune via the MTD vendor.

## Related content

[Enable a Mobile Threat Defense connector](mtd-connector-enable.md)
