---
title: Asset Intelligence security & privacy
titleSuffix: Configuration Manager
description: Security guidance and privacy information for Asset Intelligence in Configuration Manager.
ms.date: 05/05/2021
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Security and privacy for Asset Intelligence in Configuration Manager

*Applies to: Configuration Manager (current branch)*

This article contains security guidance and privacy information for Asset Intelligence in Configuration Manager.

## Security guidance

### Secure license files

When you import a Microsoft Volume Licensing file or a General License Statement file, secure the file and communication channel. Configure NTFS permissions to make sure that only authorized users can access the license files. Use Server Message Block (SMB) signing to keep the integrity of the data when it's transferred to the site server during the import process.

### Limit permissions for users who import license files

Use the principle of least permissions to import the license files. Use [role-based administration](../../../understand/fundamentals-of-role-based-administration.md) to grant the **Manage Asset Intelligence** permission to the administrative user who imports license files. The built-in role of **Asset Manager** includes this permission.

## Privacy information

Asset Intelligence extends the inventory capabilities of Configuration Manager to provide a higher level of asset visibility. Asset Intelligence information collection isn't automatically enabled. You can modify the type of information collected by enabling hardware inventory reporting classes. For more information, see [Configure Asset Intelligence](configuring-asset-intelligence.md).

Configuration Manager stores Asset Intelligence information in the site database the same as inventory information. When clients connect to management points by using HTTPS, the data is always encrypted during transfer to the management point. When clients connect by using HTTP, configure the inventory data transfer to be [signed and encrypted](../../../plan-design/security/configure-security.md#signing-and-encryption). Inventory data isn't stored in an encrypted format in the database. Information is kept in the database until the site maintenance task [Delete Aged Inventory History](../../../servers/manage/reference-for-maintenance-tasks.md#delete-aged-inventory-history) deletes it every 90 days by default. You can configure the deletion interval.

Asset Intelligence doesn't send information about users, computers, or license usage to Microsoft. You can choose to send System Center Online requests for categorization. For these requests, you tag one or more uncategorized software titles and send them to Microsoft for research and categorization. After you upload a software title, Microsoft researchers identify and categorize the software. They then make that information available to all customers who use the online service.

When you submit information to System Center Online, understand the following privacy implications:

- Upload applies only to generic software title information that you choose to send to Microsoft. For example, software name and publisher. Inventory information isn't sent to Microsoft.

- Upload never occurs automatically, and the system isn't designed for this task to be automated. Manually select and approve the upload of each software title.

- Before the upload process starts, the Configuration Manager console shows you exactly what data it will upload.

- License information isn't sent to Microsoft. Configuration Manager stores the license information in a separate area of the site database, and it can't be sent to Microsoft.

- Any software title that you upload becomes public. The knowledge of that software and its categorization become part of the online Asset Intelligence catalog. Other customers can then download the catalog updates.

- The source of the software title isn't recorded in the Asset Intelligence catalog, and it isn't made available to other customers. Still verify that you don't include any application titles that contain any private information.

- You can't recall uploaded data.
