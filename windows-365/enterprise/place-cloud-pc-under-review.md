---
# required metadata
title: Place a Cloud PC under review
titleSuffix:
description: Learn how placing a Windows 365 Cloud PC can help you support digital forensics.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 09/27/2022
ms.topic: overview
ms.service: windows-365
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: anbiswas    
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Place a Windows 365 Enterprise Cloud PC under review

As part of a digital forensics request, you may be asked to provide a snapshot of a Cloud PC to internal or external investigators. Placing a Cloud PC under review saves a snapshot of the Cloud PC to your Azure Storage account. From there, you can provide the snapshot to the investigator.

## Requirements

To place a Cloud PC under review, you must meet the following requirements:

- A Windows 365 Enterprise license.
- An Azure Storage account in the same tenant, set up as per the requirements below.

## Set up your Azure storage account

To place a Cloud PC under review, you must first have an Azure storage account in the same tenant as the Cloud PC. For more information to help you decide which type of account fits your needs, see [Storage account overview](/azure/storage/common/storage-account-overview). We recommend that you create and maintain a dedicated storage account with dedicated access controls for auditing Cloud PCs.
As part of the process to place Cloud PCs under review, Windows 365 may be granted a contributor role for your Azure storage account.

1. [Create a Storage Account](/azure/storage/common/storage-account-create) in the same subscription as your Azure Network Connection. To create the account, you can use PowerShell, Azure CLI, Azure Resource Manager Template, or Azure portal.
2. For best performance, configure the storage account with the following settings;
    - **No region limit**
    - **Premium Page Blob performance**
    - **TLS 1.2 encryption**
    - **Allow connectivity through a public endpoint**
3. [Assign an Azure role for access to blob data](/azure/storage/blobs/assign-azure-role-data-access). The minimum permission required for the Windows 365 service to place a Cloud PC under review is Storage Account Contributor.

## Place a Cloud PC under review

After setting up an Azure storage account with permissions as explained above, you can place a Cloud PC under review using the following steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and select  **Devices** > **All Devices** > choose a device.
    ![Screenshot of choose a device](./media/place-cloud-pc-under-review/choose-device.png)
    
2. Select the ellipses (**…**) > **Place cloud PC under review**.
    ![Screenshot of place a Cloud PC under review](./media/place-cloud-pc-under-review/place-cloud-pc-under-review.png)
    
3. Select the Azure subscription and the Azure storage account to which the Windows 365 service was given **Storage Account Contributor** permissions.
    ![Screenshot of choose a subscription and storage](./media/place-cloud-pc-under-review/subscription-storage.png)
    
4. Select **Place under review**. Based on the size of the Cloud PC, it could take a few minutes for the snapshot to be saved to the storage account.

## Remove a Cloud PC from review

Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and select  **Devices** > **All Devices** > choose a device > **…** > **Remove from review**.

## Bulk actions

You can also use Intune’s bulk device actions to place multiple Cloud PCs under review at the same time. For more information, see [Use bulk device actions]( /mem/intune/remote-actions/bulk-device-actions).

## Next steps
[Learn more about digital forensics and Cloud PCs](digital-forensics.md).
