---
# required metadata

title: Windows Delivery Optimization settings in Microsoft Intune
description: Configure device configuration policy to manage Delivery Optimization settings on Windows devices you manage with Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/07/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
ms.reviewer: davguy
---

# Delivery Optimization settings in Microsoft Intune

With Intune, you can use Delivery Optimization settings for your Windows devices to reduce bandwidth consumption when those devices download applications and updates. This article describes how to configure Delivery Optimization settings as part of an Intune device configuration profile. After you create a profile, you then assign or deploy that profile to your Windows devices.

- View the list of the [Delivery Optimization settings](delivery-optimization-settings.md) that Intune supports.
- Learn about [Delivery Optimization updates](/windows/deployment/update/waas-delivery-optimization) in the Windows documentation.

This feature applies to:

- Windows 10
- Windows 11

## Create the profile

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Manage devices** > **Configuration** > **Create** > **New Policy**.

3. Enter the following properties:

   - **Platform**: Select **Windows 10 and later**.
   - **Profile type**: Select **Templates** > **Delivery optimization**.

4. Select **Create**.

5. In **Basics**, enter the following properties:

   - **Name**: Enter a descriptive name for the new profile.
   - **Description**: Enter a description for the profile. This setting is optional, but recommended.

6. Select **Next**.

7. On the **Configuration settings** page, define how you want updates and apps to download. For information about available settings, see [Delivery Optimization settings for Intune](delivery-optimization-settings.md).

   When you're done configuring settings, select **Next**.

8. On the **Scope (Tags)** page, select **Select scope tags** to open the *Select tags* pane to assign scope tags to the profile.
  
   Select **Next** to continue.

9. On the **Assignments** page, select the groups that receive this profile. For more information on assigning profiles, see [Assign user and device profiles](../configuration/device-profile-assign.md).

   Select **Next**.

10. On the **Applicability Rules** page, use the **Rule**, **Property**, and **Value** options to define how this profile applies within assigned groups.

11. On the **Review + create** page, when you're done, choose **Create**. The profile is created and is shown in the list.

The next time each device checks in, the policy is applied.

## Next steps

After you [assign the profile](device-profile-assign.md), [monitor its status](device-profile-monitor.md).

View the [Delivery Optimization settings](delivery-optimization-settings.md) for Intune.