---
# required metadata

title: Create MTD device compliance policy with Microsoft Intune
titleSuffix: Microsoft Intune
description: Create an Intune device compliance policy that uses your MTD partner threat levels to determine if a mobile device can access company resources.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/20/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid: 5d12254f-ffab-4792-b19c-ab37f5e02f35

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Create Mobile Threat Defense (MTD) device compliance policy with Intune

Intune with MTD helps you detect threats and assess risk on mobile devices. You can create an Intune device compliance policy rule that assesses risk to determine if the device is compliant or not. You can then use a [Conditional Access policy](create-conditional-access-intune.md) to block access to services based on device compliance.

> [!NOTE]
> This information applies to all Mobile Threat Defense partners.

## Before you begin

As part of the MTD setup, in the MTD partner console, you created a policy that classifies various threats as high, medium, and low. You now need to set the Mobile Threat Defense level in the Intune device compliance policy.

Prerequisites for device compliance policy with MTD:

- Set up MTD integration with Intune

## To create an MTD device compliance policy

1. Sign in to the [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Device** > **Compliance policies** > **Create policy**.

3. Specify a device compliance policy **Name**, **Description**, select the **Platform**, then select **Configure** under the **Settings** section.

4. On the **compliance policy** pane, choose **Device Health**.

5. On the **Device Health** pane, choose the Mobile Threat Level from the drop-down list for **Require the device to be at or under the Device Threat Level**.

   - **Secured**: This level is the most secure. The device cannot have any threats present and still access company resources. If any threats are found, the device is evaluated as noncompliant.

   - **Low**: The device is compliant if only low-level threats are present. Anything higher puts the device in a noncompliant status.

   - **Medium**: The device is compliant if the threats found on the device are low or medium level. If high-level threats are detected, the device is determined as noncompliant.

   - **High**: This level is the least secure. This allows all threat levels, and uses Mobile Threat Defense for reporting purposes only. Devices are required to have the MTD app activated with this setting.

6. Select **OK** twice, then select **Create** to create the policy.

> [!IMPORTANT]
> If you create Conditional Access policies for Office 365 or other services, the device compliance evaluation is assessed and noncompliant devices are blocked from accessing corporate resources until the threat is resolved in the device.

## To assign an MTD device compliance policy

To assign a device compliance policy to users:

1. Sign in to the [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Device** > **Compliance policies**.

3. Select the policy you want to assign to users, and then select **Assignments**. Use the available options to *Include* and *Exclude* groups to receive this policy.  

4. Select Save to complete the assignment. When you save the assignment, the policy deploys to your selected users and their devices are evaluated for compliance.

## Next steps

[Enable MTD with Intune](mtd-connector-enable.md)
