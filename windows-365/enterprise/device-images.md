---
# required metadata
title: Device images in Windows 365
titleSuffix:
description: Learn about device images in Windows 365.
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 08/02/2021
ms.topic: overview
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

# Device images overview

Windows 365 uses both default and custom operating system images to automatically create the virtual Cloud PCs that you provide to your end users. The default images are available from the gallery in Microsoft Endpoint Manager as a part of creating your provisioning policy. You can also [upload custom images](add-device-images.md) that you create.

## Image requirements

Both marketplace and custom images must meet the following requirements:

- Windows 10 Enterprise version 1909 or later.
- Hyper-V Gen 1 images.
- Generalized VM image.
- Single Session VM images (multi-session isn’t supported).
- Default 64 GB OS disk size. The OS disk size will be automatically adjusted to the size specified in SKU description of the Windows 365 license.

A custom image must also meet the following extra requirements:

- Exist in an Azure subscription that has an on-premises network connection already setup.
- Is stored as a managed image in Azure.

Storing a managed image on Azure incurs storage costs. However customers can delete the managed image from Azure once they've successfully uploaded it as Device Images to Microsoft Endpoint Manager.

## Gallery images

Windows 365 provides a built-in gallery of Windows Enterprise images accessible through the provisioning policy creation flow. They are replicated to all Azure regions to give you a quick provisioning experience. These images are updated monthly with the latest security updates so that end users have a secure and seamless experience.

There are two sets of images available to choose from across the different versions of Windows 10 Enterprise:

- **Images with pre-installed Microsoft 365 Apps**: Microsoft 365 Apps and Teams optimizations are already installed. The following settings are pre-applied:
  - IsAVDEnvironment reg key (Teams).
  - C++ Runtime (Teams).
  - WebRTC Redirector (Teams).
  - Microsoft Teams (Teams).
  - Edge settings like Sleeping Tabs, Startup boost, and First Time optimizations based on Azure AD and synchronization.
  - Microsoft Outlook first-time configuration settings (auto log on based on Azure AD profile, support for other profiles).
- **Images with OS optimizations**: These are Windows Enterprise images optimized for improved performance on virtualized environments and on lower end hardware configurations. The following settings are pre-applied:
  - Services optimized for virtualization.
  - UWP packages removed.
  - Task scheduler actions disabled.

### Recommended image by license

You can choose any image for any Windows 365 license. However, for optimal performance, the following recommendations apply:

| Windows 365 license | Recommended gallery image |
| --- | --- |
| 2vCPU/4GB/64GB and above | Windows 10 Enterprise + Microsoft 365 Apps |
| 1vCPU/2GB/64GB | Windows 10 Enterprise + OS Optimizations |

## Custom images

If none of the default gallery images meet your requirements, you can upload up to 20 of your own custom device images.

For more information on creating such a custom image, see [Create a managed image of a generalized VM in Azure](/azure/virtual-machines/windows/capture-image-resource). For best performance, you should also make sure to optimize your image for a virtual desktop role. For more information on this optimization, see [Optimizing Windows 10, version 2004 for a Virtual Desktop Infrastructure (VDI) role](/windows-server/remote/remote-desktop-services/rds-vdi-recommendations-2004).

A custom image can be created using [any of the images above as a starting point](https://azuremarketplace.microsoft.com/marketplace/apps/microsoftwindowsdesktop.windows-ent-cpc). For example, you can start with an image above and then install more applications and make more configuration changes.

For more information about adding a device image to Windows 365, see [Add and delete custom device images](add-device-images.md).

When you upload a custom device image, Windows 365:

1. Copies the image to a temporary subscription.
2. Runs the following validation checks on the image:
    1. Verifies all the Windows 365 image requirements are met.
    2. Deploys a virtual machine and makes sure that the images can be booted and provisioned as a Cloud PC.
3. Replicates the image across all Azure regions where you have an on-premises network connection.

<!-- ########################## -->
## Next steps

[Learn about device configuration](device-configuration.md).
