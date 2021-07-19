---
# required metadata
title: Add device images for Windows 365 - Azure | Microsoft Docs
titleSuffix:
description: Learn how to add device images for Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 6/14/2021
ms.topic: how-to
ms.service: cloudpc
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: naramkri
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# Add or delete custom device images

If you want to use a custom device image, you can add it into your Azure subscription and then use it for creating Cloud PCs. You can use standard Azure Marketplace gallery images or [create your own custom images](/azure/virtual-machines/windows/capture-image-resource).

## Add a custom device image

You can upload the custom image to the Windows 365 service by following these steps:

1. Sign in to the [Microsoft Endpoint Manager admin center](https://endpoint.microsoft.com/), select **Devices** > **Windows 365** (under **Provisioning**) > **Device images** > **Add**.
![Screenshot of add device image](./media/add-device-images/add-device-image.png)
2. In the **Add image** page, provide the following information:
    - **Image name**: The name of the image you want to add.
    - **Image version**: A version number of the image with this format: Major(int).Minor(int).Patch(int) format. For example: 0.0.1, 1.5.13.
    - **Operating system**: The operating system of the image.
    - **Source Image**: Choose an image to add. The list will populate with all custom images from your subscription that meet the pre-requisites.

3. Select **Upload** to add the image to your device image list.

## Delete a custom device image

You can delete a custom image from Windows 365 by following these steps:

1. Sign in to the [Microsoft Endpoint Manager admin center](https://endpoint.microsoft.com/), select **Devices** > **Windows 365** (under **Provisioning**) > **Device images**.
2. On the **Device images** page, select the check box next to the image > **Delete**.
3. Select **Yes** on the confirmation pop up to permanently delete the image.

<!-- ########################## -->
## Next steps

[Create a provisioning policy](create-provisioning-policy.md)
