---
# required metadata

title: Delivery Optimization settings for Windows devices in Microsoft Intune
description: Configure how Windows devices you manage with Intune use Delivery Optimization. In Intune, create a device configuration profile to install updates from the internet. Also see how to replace existing update rings with a Delivery Optimization profile.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/05/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
ms.reviewer: kerimh
---

# Delivery Optimization settings in Microsoft Intune

Applies to:

- Windows 10
- Windows 11

With Intune, use Delivery Optimization settings for your Windows devices to reduce bandwidth consumption when those devices download applications and updates. Configure Delivery Optimization as part of your device configuration profiles.  

This article describes how to configure Delivery Optimization settings as part of a device configuration profile. After you create a profile, you then assign or deploy that profile to your Windows devices.

To view a list of the Delivery Optimization settings that Intune supports, see [Delivery Optimization settings for Intune](delivery-optimization-settings.md).  

To learn about Delivery Optimization on Windows 10 and Window 11, see [Delivery Optimization updates](/windows/deployment/update/waas-delivery-optimization) in the Windows documentation.  

## Create the profile

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Configuration profiles** > **Create profile**.

3. Enter the following properties:

   - **Platform**: Select **Windows 10 and later**.
   - **Profile**: Select **Templates** > **Delivery Optimization**.

4. Select **Create**.

5. In **Basics**, enter the following properties:

   - **Name**: Enter a descriptive name for the new profile.
   - **Description**: Enter a description for the profile. This setting is optional, but recommended.

6. Select **Next**.

7. On the **Configuration settings** page, define how you want updates and apps to download. For information about available settings, see [Delivery Optimization settings for Intune](delivery-optimization-settings.md).

   When you're done configuring settings, select **Next**.

8. On the **Scope (Tags)** page, select **Select scope tags** to open the *Select tags* pane to assign scope tags to the profile.
  
   Select **Next** to continue.

9. On the **Assignments** page, select the groups that will receive this profile. For more information on assigning profiles, see [Assign user and device profiles](../configuration/device-profile-assign.md).

   Select **Next**.

10. On the **Applicability Rules** page, use the **Rule**, **Property**, and **Value** options to define how this profile applies within assigned groups.

11. On the **Review + create** page, when you're done, choose **Create**. The profile is created and is shown in the list.

The next time each device checks in, the policy is applied.

## Remove Delivery Optimization from Windows Update Rings

Delivery Optimization was previously configured as part of Software Update Rings. Beginning in February of 2019, Delivery Optimization settings are configured as part of a Deliver Optimization device configuration profile, which includes additional settings that affect more than Software Update delivery to devices. If you haven't already, remove the Delivery Optimization setting from your Update Rings by setting it to *Not configured*, and then use a Delivery Optimization profile to manage the larger range of available options.

1. Create a Delivery Optimization device configuration profile:

    1. In the Microsoft Endpoint Manager admin center, select **Devices** > **Configuration profiles** > **Create profile**.
    2. Enter the following properties:

        - **Platform**: Select **Windows 10 and later**.
        - **Profile**: Select **Templates** > **Delivery Optimization**.

    3. Select **Create**.
    4. In **Basics**, enter the following properties:

        - **Name**: Enter a descriptive name for the new profile.
        - **Description**: Enter a description for the profile. This setting is optional, but recommended.

    5. Select **Next**.
    6. In **Configuration settings** > **Download mode**, choose the same mode that's used by the existing software update ring *unless* you want to change the settings you apply to your devices. Your options:

        - **Not configured​**
        - **HTTP only, no peering​**
        - **HTTP blended with peering behind the same NAT**
        - **HTTP blended with peering across a private group​**
        - **HTTP blended with Internet peering​**
        - **Simple download mode with no peering​**
        - **Bypass mode**

    7. Configure [any additional settings](delivery-optimization-settings.md) you want to manage, and continue creating the profile.

        In **Assignments**, assign this new profile to the same devices and users as the existing software update ring. For more information, see [assign the profile](device-profile-assign.md).

2. Unconfigure the existing software ring:

    1. In the Microsoft Endpoint Manager admin center, go to **Devices** > **Update rings for Windows 10 and later**.
    2. In the list, select your update ring.
    3. In the settings, set **Delivery Optimization download mode** to **Not configured**.
    4. **OK** > **Save** your changes.

## Next steps

After you [assign the profile](device-profile-assign.md), [monitor its status](device-profile-monitor.md).

View the [Delivery Optimization settings](delivery-optimization-settings.md) for Intune.
