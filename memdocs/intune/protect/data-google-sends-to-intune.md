---
# required metadata

title: Data Google sends to Intune
titleSuffix: Microsoft Intune
description: List of data that Google sends to Intune when Android enterprise device management is enabled with Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 04/08/2022
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid: c379c8db-788a-454e-9098-665ea3bc7b56


# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Data Google sends to Intune

When Android enterprise device management is enabled on a device, Microsoft Intune establishes a connection with Google and user and device information is shared between Intune and Google. Before Microsoft Intune can establish a connection, you must create a Google account.

The following table lists the data that Google sends to Intune when device management is enabled on an Android device:

| Data Google sends to Intune | Details | Used for | Example |
|:---:|:---:|:---:|:---:|
| Enterprise data | Customer's enterprise identifiers in Google. | Links the customer's information between Intune and Google. | **enterpriseId** example: LC04eik8a6.<br>**Name**. The Administrator name as entered when configuring Android enterprise. Example: Joe Smith.<br>**Admin email**. YourAdmin@gmail.com that was used when configuring Android enterprise. |
| Application data | Data for managed Play Store applications. | Targeting the application to users or devices as available or required. | **Application Name** example: Contoso Warehouse Inventory Application.<br>**Unique Identifier to represent application** example: app:com.Contoso.Warehouse.InventoryTracking |
| Service account | Unique internal Google service account for use with specific customer calls. | Used for making calls into Google on the customer behalf (to view apps, devices, and more) | **Name** example: InternalAccount@InternalService.com.<br>**Keys** example: ServiceAccountPassword |

To stop using Android enterprise device management with Microsoft Intune and delete the data, you must both disable the Microsoft Intune Android enterprise device management and also delete your Google account. Refer to Google account how to perform account management.