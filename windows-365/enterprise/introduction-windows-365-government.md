---
# required metadata
title: What is Windows 365 Government?
titleSuffix:
description: Learn about Windows 365 Government.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 10/3/2022
ms.topic: overview
ms.service: cloudpc
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# What is Windows 365 Government?

Windows 365 Government is a cloud-based service that automatically creates virtual machines (Cloud PCs) for US government users. This service spans across a regulated US Government Community Cloud (GCC) and a public facing cloud. It meets federal, state, and local US government needs to securely stream Windows apps, data, content, and settings on Cloud PCs from regulated clouds to any device at any time.

Windows 365 Government customers are government agencies or public entities that qualify to use services hosted in GCC and GCC High. The services in the GCC and GCC High clouds must meet specific requirements and pass rigorous audit reviews before customers are allowed to use them.

For GCC, users who access Windows 365 Government Cloud PCs have an identity in the Azure AD public tenant.  For GCC High, users who access Windows 365 Government Cloud PCs have an identity in the Azure AD Government tenant.  The underlying resources are isolated from the general public through a series of physical and logical controls. For more information, see [Azure Government](https://learn.microsoft.com/azure/azure-government/documentation-government-plan-identity).

Windows 365 Government supports this scenario in a secure, scalable, and transparent manner. It provides flexibility to administrators to manage users in the public cloud, resources in the government cloud, and the dynamic relationship between the two.

Windows 365 Government is available GCC and GCC High customers in the US, as well as contractors (in US entities) holding or processing data on behalf of US government agencies.

For more information about Cloud PCs and Windows 365, see [What is Windows 365?](..\overview.md) For more information about purchasing, see [How to buy Windows 365 Government](https://aka.ms/win365).

## Features not yet supported Windows 365 Government

The following features are not yet supported for Windows 365 GCC and/or GCCH.

| Feature | GCC | GCCH |
|:----|:----|:----|
|Windows 11 support|![X](./media/manage-rdp-device-restrictions/xmark.png)|![X](./media/manage-rdp-device-restrictions/xmark.png)|
|Provision Cloud PCs with Secure Boot and vTPM|![X](./media/manage-rdp-device-restrictions/xmark.png)|![X](./media/manage-rdp-device-restrictions/xmark.png)|
|Configure installed language and region for provisioning Cloud PCs|![X](./media/manage-rdp-device-restrictions/xmark.png)|![X](./media/manage-rdp-device-restrictions/xmark.png)|
|Digital forensics and placing a Cloud PC under review|![X](./media/manage-rdp-device-restrictions/xmark.png)|![X](./media/manage-rdp-device-restrictions/xmark.png)|
|Unified dashboard|![X](./media/manage-rdp-device-restrictions/xmark.png)|![X](./media/manage-rdp-device-restrictions/xmark.png)|
|Virtualization-based workloads|![X](./media/manage-rdp-device-restrictions/xmark.png)|![X](./media/manage-rdp-device-restrictions/xmark.png)|
|Endpoint analytics support|![Check](./media/manage-rdp-device-restrictions/checkmark.png)|![X](./media/manage-rdp-device-restrictions/xmark.png)|
|Windows 365 Security baseline|![X](./media/manage-rdp-device-restrictions/xmark.png)|![X](./media/manage-rdp-device-restrictions/xmark.png)|
|RDP Shortpath for public networks|![X](./media/manage-rdp-device-restrictions/xmark.png)|![X](./media/manage-rdp-device-restrictions/xmark.png)|
|Windows 365 System based alerting on Microsoft Endpoint Manager for Cloud PCs|![X](./media/manage-rdp-device-restrictions/xmark.png)|![X](./media/manage-rdp-device-restrictions/xmark.png)|
|User initiated feedback in End User Portal and Windows 365 Web Client|![X](./media/manage-rdp-device-restrictions/xmark.png)|![X](./media/manage-rdp-device-restrictions/xmark.png)|

## Next steps

To learn more about Windows 365, see [What is Windows 365?](..\overview.md)
