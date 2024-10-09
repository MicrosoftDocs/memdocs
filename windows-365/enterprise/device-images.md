---
# required metadata
title: Device images in Windows 365
titleSuffix:
description: Learn about device images in Windows 365.
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 09/09/2024
ms.topic: overview
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: evas
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Device images overview

Windows 365 uses both default and custom operating system images to automatically create the virtual Cloud PCs that you provide to your end users. The default images are available from the gallery in Microsoft Intune as a part of creating your provisioning policy. You can also [upload custom images](add-device-images.md) that you create.

## Image requirements

Both marketplace and custom images must meet the following requirements:

- Supported versions of Windows 10 or Windows 11 Enterprise.
- Generation 2 images.
    > [!Note]
    > We recently made the change to **generation 2** (Gen2) virtual machine images. Newly created custom images must be Gen2. Existing custom images uploaded based on generation 1 will remain active.
- The image must never have been Active Directory, Microsoft Entra ID joined, Intune-enrolled, or enrolled for co-management. For more information, see [Sysprep won't run correctly on a device that has been MDM enrolled](/troubleshoot/mem/intune/device-enrollment/troubleshoot-sysprep-windows-10-device-enrolled-mdm).
- Generalized VM image.
- Single Session VM images (multi-session isn’t supported).
- No recovery partition. For information about how to remove a recovery partition, see the [Windows Server command: delete partition](/windows-server/administration/windows-commands/delete-partition).
- Default 64-GB OS disk size. The OS disk size is automatically adjusted to the size specified in SKU description of the Windows 365 license.

A custom image must also meet the following extra requirements:

- Exist in an Azure subscription.
- Is stored as a [managed image](/azure/virtual-machines/capture-image-resource) in Azure.

Storing a managed image on Azure incurs storage costs. However, customers can delete the managed image from Azure once they've successfully uploaded it as a Custom Image to Microsoft Intune.

## Gallery images

Windows 365 provides a built-in gallery of Windows Enterprise images accessible through the [provisioning policy creation flow](create-provisioning-policy.md). Each image helps admins with preset audit policies already enabled, like account policies, logon/logoff, object access, and policy change.

They're replicated to all Azure regions to give you a quick provisioning experience. These images are updated monthly with:

- Optimizations for improved user experience.
- The latest security updates so that end users have a secure and seamless experience.

There are two sets of images available to choose from across the different versions of Windows Enterprise:

- **Images with pre-installed Microsoft 365 Apps**: Microsoft 365 Apps and Teams optimizations are already installed. The following settings are preapplied:
  - IsWVDEnvironment reg key (Teams).
  - C++ Runtime (Teams).
  - WebRTC Redirector (Teams).
  - Microsoft Teams (Teams).
  - Microsoft Edge settings like sleeping tabs, [forced browser sign-in](/deployedge/microsoft-edge-policies#browsersignin), startup boost, and first time optimizations based on Microsoft Entra ID and synchronization. For more information, see [Configure Microsoft Edge policy settings with Microsoft Intune](/deployedge/configure-edge-with-intune).
  - Microsoft Outlook first-time configuration settings (auto log on based on Microsoft Entra profile, support for other profiles).
- **Images with no preinstalled applications**: A plain image without any preinstalled applications (look for images without the **M365 Apps** in the name).

Both types of images are harmonized in GPOs. Any differences are due to preinstalled apps.

### Gallery image update cycle

All supported Windows 365 gallery images are updated monthly after the security patch release schedule of Windows Servicing & Delivery. This update happens around the middle of each month. Updated Windows 365 images are made available in Intune for provisioning around the end of the third week of the month.

Each updated image includes:

- [Windows 10/11 monthly image updates](https://support.microsoft.com/topic/windows-10-release-on-azure-marketplace-update-history-da826e21-45ae-f6b9-de71-5f0ee2ec1563)
- [Microsoft 365 Apps security updates](/officeupdates/microsoft365-apps-security-updates) and [feature updates](/officeupdates/monthly-enterprise-channel)
  - Windows 365 gallery images include the latest Monthly Enterprise Channel release with the latest security updates.
- [Microsoft Teams updates](https://support.microsoft.com/office/what-s-new-in-microsoft-teams-d7092a6d-c896-424c-b362-a472d5f105de)
- [WebRTC redirector service updates](/azure/virtual-desktop/teams-on-avd#install-the-teams-websocket-service)

Applications that come pre-installed are the latest version that is available at the start of the second Tuesday of that month. Any app updates posted on that day are included in the image update of the subsequent month.

Newly provisioned Cloud PCs are automatically created with the latest images. For existing Cloud PCs, you can receive the updates by reprovisioning.

## Custom images

If none of the default gallery images meet your requirements, you can upload up to 20 of your own custom device images.

For more information on creating such a custom image, see [Create a managed image of a generalized VM in Azure](/azure/virtual-machines/windows/capture-image-resource).

A custom image can be created using [any of the images mentioned previously as a starting point](https://azuremarketplace.microsoft.com/marketplace/apps/microsoftwindowsdesktop.windows-ent-cpc). For example, you can start with one of those images and then install more applications and make more configuration changes.

> [!NOTE]
> For custom images with Teams application, follow the instructions detailed in [Create a Cloud PC custom image that supports Microsoft Teams](create-custom-image-support-teams.md) to configure optimizations that are needed.  

For more information about adding a device image to Windows 365, see [Add and delete custom device images](add-device-images.md).

When you upload a custom device image, Windows 365:

1. Copies the image to a temporary subscription.
2. Runs the following validation checks on the image:
    1. Verifies all the Windows 365 image requirements are met.
    2. Deploys a virtual machine and makes sure that the images can be booted and provisioned as a Cloud PC.
3. If you have a Microsoft Entra hybrid join connection, Windows 365 replicates the image across all Azure regions where you have an Azure network connection.
4. If you have a Microsoft Entra join connection, Windows 365 replicates the image to the provisioned region during provisioning.

<!-- ########################## -->
## Next steps

[Learn about device configuration](device-configuration.md).

[Learn about using apps, like Microsoft Teams, with your Cloud PCs](app-overview.md).

[Learn about restoring a Cloud PC to a previous state](restore-overview.md)
