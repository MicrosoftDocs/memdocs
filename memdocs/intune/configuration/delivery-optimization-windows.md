---
# required metadata

title: Delivery optimization settings for Windows 10 in Microsoft Intune - Azure | Microsoft Docs
description: Configure how Windows 10 devices you manage with Intune use delivery optimization. In Intune, create a device configuration profile to install updates from the internet. Also see how to replace existing update rings with a delivery optimization profile.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 02/10/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
ms.reviewer: kerimh
---

# Delivery optimization settings in Microsoft Intune

With Intune, use Delivery Optimization settings for your Windows 10 devices to reduce bandwidth consumption when those devices download applications and updates. Configure delivery optimization as part of your device configuration profiles.  

This article describes how to configure delivery optimization settings as part of a device configuration profile. After you create a profile, you then assign or deploy that profile to your Windows 10 devices. 

To view a list of the delivery optimization settings that Intune supports, see [Delivery Optimization settings for Intune](../delivery-optimization-settings.md).  

To learn about Delivery Optimization on Windows 10, see [Delivery Optimization updates](https://docs.microsoft.com/windows/deployment/update/waas-delivery-optimization) in the Windows documentation.  

## Create the profile

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Devices** > **Configuration profiles** > **Create profile**.

3. Enter the following properties:

    - **Name**: Enter a descriptive name for the new profile.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.
    - **Platform**: Select **Windows 10 and later**.
    - **Profile type**: Select **Delivery optimization**.

4. Choose **Settings** > **Configure**, and define how you want updates and apps to download. For information about available settings, see [Delivery optimization settings for Intune](../delivery-optimization-settings.md).

5. When finished, select **OK** > **Create** to save your changes.

The profile is created and is shown in the list. Next, [assign the profile](device-profile-assign.md) and then [monitor its status](device-profile-monitor.md).

<!-- ## Move existing update rings to delivery optimization

**Delivery optimization** settings replace **Software updates – Windows 10 Update Rings**. Your existing update rings can be easily changed to use the **Delivery optimization** settings. To maintain the same settings when you create a delivery optimization profile, use the same *Delivery optimization download mode* and then set the same settings as you already use. However, you can choose to reconfigure delivery optimization settings to take advantage of the full range of addition settings that the Delivery Optimization profile can manage. 
-->

## Remove Delivery Optimization from Windows 10 Update Rings

Delivery Optimization was previously configured as part of Software Update Rings. Beginning in February of 2019, Delivery Optimization settings are configured as part of a Deliver Optimization device configuration profile, which includes additional settings that affect more than Software Update delivery to devices. If you haven’t already, remove the delivery optimization setting from your Update Rings by setting it to *Not configured*, and then use a Delivery Optimization profile to manage the larger range of available options.

1. Create a Delivery Optimization device configuration profile:

    1. In the Microsoft Endpoint Manager admin center, select **Devices** > **Configuration profiles** > **Create profile**.
    2. Enter the following properties:

        - **Name**: Enter a descriptive name for the new profile.
        - **Description**: Enter a description for the profile. This setting is optional, but recommended.
        - **Platform**: Select **Windows 10 and later**.
        - **Profile type**: Select **Delivery optimization**.
        - **Settings**: For **Delivery optimization download mode**, choose the same mode that's used by the existing software update ring unless you want to change the settings you apply to your devices. Your options:
            - **Not configured​**
            - **HTTP only, no peering​**
            - **HTTP blended with peering behind the same NAT**
            - **HTTP blended with peering across a private group​**
            - **HTTP blended with Internet peering​**
            - **Simple download mode with no peering​**
            - **Bypass mode**
    3. Configure any additional settings you might want to manage.

2. Assign this new profile to the same devices and users as the existing software update ring. [Assign the profile](device-profile-assign.md) lists the steps.

3. Unconfigure the existing software ring:
    1. In the Microsoft Endpoint Manager admin center, go to **Software updates** > Windows 10 Update Rings.
    2. In the list, select your update ring.
    3. In the settings, set **Delivery optimization download mode** to **Not configured**.
    4. **OK** > **Save** your changes.

## Next steps

[Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md) its status.  
View the [delivery optimization settings](../delivery-optimization-settings.md) for Intune.
