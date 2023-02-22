---
# required metadata

title: Create a Mobile Threat Defense (MTD) device compliance policy with Microsoft Intune
titleSuffix: Microsoft Intune
description: Create an Intune device compliance policy that uses your MTD partner threat levels to determine if a mobile device can access company resources.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/28/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
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
---

# Create Mobile Threat Defense (MTD) device compliance policy with Intune

Intune with MTD helps you detect threats and assess risk on mobile devices. You can create an Intune device compliance policy rule that assesses risk to determine if the device is compliant or not. You can then use a [Conditional Access policy](create-conditional-access-intune.md) to block access to services based on device compliance.

> [!NOTE]
> This information applies to all Mobile Threat Defense partners.

## Before you begin

As part of the MTD setup, in the MTD partner console, you created a policy that classifies various threats as high, medium, and low. Next you'll set the Mobile Threat Defense level in the Intune device compliance policy.

Prerequisites for device compliance policy with MTD:

- Set up MTD integration with Intune

## To create an MTD device compliance policy

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** > **Device Compliance** > **Create Policy**.

3. Select the **Platform**, and then **Create**.

4. On **Basics**, specify  a device compliance policy **Name**, and **Description** (optional). Select **Next** to continue.

5. On **Compliance settings**, expand and configure **Device Health**. Choose the Mobile Threat Level from the drop-down list for **Require the device to be at or under the Device Threat Level**.

   - **Secured**: This level is the most secure. The device can't have any threats present and still access company resources. If any threats are found, the device is evaluated as noncompliant.

   - **Low**: The device is compliant if only low-level threats are present. Anything higher puts the device in a noncompliant status.

   - **Medium**: The device is compliant if the threats found on the device are low or medium level. If high-level threats are detected, the device is determined as noncompliant.

   - **High**: This threat level is the least secure as it allows all threat levels and uses Mobile Threat Defense for reporting purposes only. Devices are required to have the MTD app activated with this setting.

6. Select **Next** to advance through to **Assignments**. Select the groups that will receive this profile. 

> [!IMPORTANT]
> You will see the option to either select user groups, or device based groups under **Select groups to include**. The **Require the device to be at or under the Device Threat Level** setting is currently only supported with **user groups**. Targeting **device groups is currently not supported** and they should not be selected.

   Select **Next**.

7. On the **Review + create** page, when you're done, choose **Create**. The new profile is displayed in the list when you select the policy type for the profile you created.

> [!IMPORTANT]
> If you create Conditional Access policies for Microsoft 365 or other services, the device compliance evaluation is assessed and noncompliant devices are blocked from accessing corporate resources until the threat is resolved in the device and reported to Intune via the chosen MTD vendor.

## To assign an MTD device compliance policy

To assign, or change the assignment of a device compliance policy to users:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Endpoint security** > **Device compliance**.

3. Select the policy you want to assign to users, and then select **Properties**.

4. Select **Edit** for Assignments, and then use the available options to *Include* and *Exclude* groups to receive this policy. As a reminder, targeting **device groups is currently not supported** and they should not be selected.  

5. Select **Review + save** to complete the assignment. When you save the assignment, the policy deploys to your selected users and their devices are evaluated for compliance.

## Next steps

* [Enable MTD with Intune](mtd-connector-enable.md)
