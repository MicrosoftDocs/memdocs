---
# required metadata
title: Place a Cloud PC under review
titleSuffix:
description: Learn how placing a Windows 365 Cloud PC can help you support digital forensics.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 10/30/2023
ms.topic: overview
ms.service: windows-365
ms.subservice:
ms.localizationpriority: high
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
As part of the process to place Cloud PCs under review, Windows 365 requires the **Storage Account Contributor** and **Storage Blob Data Contributor** roles for your Azure storage account.

1. [Create a Storage Account](/azure/storage/common/storage-account-create) in the Azure subscription of your choice. To create the account, you can use PowerShell, Azure CLI, Azure Resource Manager Template, or Azure portal.
2. Configure the storage account with the following settings;
    - **Instance details**
        - **Region**: Same region as CloudPC suggested for performance. There is no restriction on which region.
        - **Performance**: **Premium**
        - **Premium account type**: **Page blobs**
    - **Security**
        - Minimum TLS version: **Version 1.2**
    - **Networking**
        - **Network access**: **Enable public access from all networks**

   NOT SUPPORTED: Setting a [Permit scope for copy operations](/azure/storage/common/security-restrict-copy-operations). It must be (null), the default value, to allow copying from any storage account to the destination account.
3. [Assign an Azure role for access to blob data](/azure/storage/blobs/assign-azure-role-data-access). The minimum permissions required for the Windows 365 service to place a Cloud PC under review are Storage Account Contributor and Storage Blob Data Contributor.

## Place a Cloud PC under review

After setting up an Azure storage account with permissions as explained above, you can place a Cloud PC under review using the following steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and select  **Devices** > **All Devices** > choose a device.
    ![Screenshot of choose a device](./media/place-cloud-pc-under-review/choose-device.png)

2. Select the ellipses (**…**) > **Place cloud PC under review**.
    ![Screenshot of place a Cloud PC under review](./media/place-cloud-pc-under-review/place-cloud-pc-under-review.png)

3. Select the Azure subscription and the Azure storage account to which the Windows 365 service was given **Storage Account Contributor** and **Storage Blob Data Contributor** permissions.

   Under **Access during review**, if you choose
   - **Block Access**, the Cloud PC will be immediately powered off so the user cannot access the Cloud PC, and then the snapshot will be created. This is useful in cases where you may want to contain a security threat by shutting the Cloud PC down, and then performing analysis of the snapshot later in an isolated environment.
   - **Allow Access**, the Cloud PC user can continue to use the Cloud PC even as you create a snapshot in the storage account.
   - 
    ![Screenshot of choose a subscription and storage](./media/place-cloud-pc-under-review/subscription-storage.png)

5. Select **Place under review**. Based on the disk size of the Cloud PC and storage account destination region, it can range from minutes to a few hours for each snapshot to be saved to the storage account.

To make the snapshot tamper-evident, you should create a file hash of the snapshot when it has been saved in the storage account. One way of creating the file hash is to use the [Get-FileHash](/powershell/module/microsoft.powershell.utility/get-filehash) cmdlet. For best performance, the Get-FileHash cmdlet should be run against a copy of the downloaded file or be run against the snapshot in the Azure storage account from a resource located in the same Azure region.

## Remove a Cloud PC from review

Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and select  **Devices** > **All Devices** > choose a device > **…** > **Remove from review**.

## Bulk actions

You can also use Intune’s bulk device actions to place multiple Cloud PCs under review at the same time. For more information, see [Use bulk device actions]( /mem/intune/remote-actions/bulk-device-actions).

## Management with API

You can use the Graph API to place or remove a Cloud PC from review. For more information, see [managedDevice: setCloudPcReviewStatus](/graph/api/manageddevice-setcloudpcreviewstatus?view=graph-rest-beta&tabs=http).

## Next steps
[Learn more about digital forensics and Cloud PCs](digital-forensics.md).
