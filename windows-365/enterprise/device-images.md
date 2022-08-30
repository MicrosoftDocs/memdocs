---
# required metadata
title: Device images in Windows 365
titleSuffix:
description: Learn about device images in Windows 365.
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 07/12/2022
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

- Windows 10 Enterprise version 20H2 or later.
- Windows 11 Enterprise 21H2.
- Generation 2 images.
    > [!Note]
    > We recently made the change to **generation 2** (Gen2) virtual machine images. Newly created custom images must be Gen2. Existing custom images uploaded based on generation 1 will remain active.
- Generalized VM image.
- Single Session VM images (multi-session isn’t supported).
- No recovery partition. For information about how to remove a recovery partition, see the [Windows Server command: delete partition](/windows-server/administration/windows-commands/delete-partition).
- Default 64-GB OS disk size. The OS disk size will be automatically adjusted to the size specified in SKU description of the Windows 365 license.

A custom image must also meet the following extra requirements:

- Exist in an Azure subscription.
- Is stored as a managed image in Azure.

Storing a managed image on Azure incurs storage costs. However, customers can delete the managed image from Azure once they've successfully uploaded it as a Custom Image to Microsoft Endpoint Manager.

## Gallery images

Windows 365 provides a built-in gallery of Windows Enterprise images accessible through the provisioning policy creation flow. They're replicated to all Azure regions to give you a quick provisioning experience. These images are updated monthly with the latest security updates so that end users have a secure and seamless experience.

There are two sets of images available to choose from across the different versions of Windows Enterprise:

- **Images with pre-installed Microsoft 365 Apps**: Microsoft 365 Apps and Teams optimizations are already installed. The following settings are pre-applied:
  - IsWVDEnvironment reg key (Teams).
  - C++ Runtime (Teams).
  - WebRTC Redirector (Teams).
  - Microsoft Teams (Teams).
  - Microsoft Edge settings like sleeping tabs, startup boost, and first time optimizations based on Azure AD and synchronization.
  - Microsoft Outlook first-time configuration settings (auto log-on based on Azure AD profile, support for other profiles).
- **Images with OS optimizations**: These are Windows Enterprise images optimized for improved performance on virtualized environments and on lower end hardware configurations. The following settings are pre-applied:
  - Services optimized for virtualization.
  - UWP packages removed.
  - Task scheduler actions disabled.

### Gallery image update cycle

All supported Windows 365 gallery images are updated monthly after the security patch release schedule of Windows Servicing & Delivery. This update happens around the middle of each month.

Each updated image includes:

- [Windows 10/11 monthly image updates](https://support.microsoft.com/topic/windows-10-release-on-azure-marketplace-update-history-da826e21-45ae-f6b9-de71-5f0ee2ec1563)
- [Microsoft 365 Apps security updates](/officeupdates/microsoft365-apps-security-updates) and [feature updates](/officeupdates/monthly-enterprise-channel)
- [Microsoft Teams updates](https://support.microsoft.com/office/what-s-new-in-microsoft-teams-d7092a6d-c896-424c-b362-a472d5f105de)
- [WebRTC redirector service updates](/azure/virtual-desktop/teams-on-avd#install-the-teams-websocket-service)

Newly provisioned Cloud PCs are automatically created with the latest images. For existing Cloud PCs, you can receive the updates by reprovisioning.

## Custom images

If none of the default gallery images meet your requirements, you can upload up to 20 of your own custom device images.

For more information on creating such a custom image, see [Create a managed image of a generalized VM in Azure](/azure/virtual-machines/windows/capture-image-resource). For best performance, you should also make sure to optimize your image for a virtual desktop role. For more information on this optimization, see [Optimizing Windows 10, version 2004 for a Virtual Desktop Infrastructure (VDI) role](/windows-server/remote/remote-desktop-services/rds-vdi-recommendations-2004).

A custom image can be created using [any of the images above as a starting point](https://azuremarketplace.microsoft.com/marketplace/apps/microsoftwindowsdesktop.windows-ent-cpc). For example, you can start with an image above and then install more applications and make more configuration changes.

>[Note]
>For custom images with Teams application, you can follow the instructions in [this article](create-custom-image-support-teams.md) to configure optimizations that are needed.  

For more information about adding a device image to Windows 365, see [Add and delete custom device images](add-device-images.md).

When you upload a custom device image, Windows 365:

1. Copies the image to a temporary subscription.
2. Runs the following validation checks on the image:
    1. Verifies all the Windows 365 image requirements are met.
    2. Deploys a virtual machine and makes sure that the images can be booted and provisioned as a Cloud PC.
3. If you have a Hybrid Azure AD Join connection, Windows 365 replicates the image across all Azure regions where you have an Azure network connection.
4. If you have an Azure AD Join connection, Windows 365 replicates the image to the provisioned region during provisioning.

<!-- ########################## -->
## Next steps

[Learn about device configuration](device-configuration.md).

[Learn about using apps, like Microsoft Teams, with your Cloud PCs](app-overview.md).
