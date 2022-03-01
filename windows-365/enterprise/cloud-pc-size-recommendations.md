---
# required metadata
title: Windows 365 size recommendations
titleSuffix:
description: Learn about the different Cloud PC sizes that are available with different SKUs in Windows 365.
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

ms.reviewer: chbrinkh
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# Cloud PC size recommendations

Windows 365 offers fixed-price licensing (through Microsoft 365) for different Cloud PC sizes. You should assess your business requirements to determine which sizes make sense for your users.  

If extra resources are needed for the Cloud PC, an admin or end user can easily upgrade the size of their Cloud PC. For more information, see [Resize a Cloud PC](resize-cloud-pc.md).  

For information about end-user hardware requirements, see [End-user hardware requirements](end-user-hardware-requirements.md).

This table shows examples of the different sizes available for a Cloud PC:

| Cloud PC CPUs, RAM, and storage | Example scenarios | Recommended gallery image | Recommended apps |
| --- | --- | --- | --- |
| 1vCPU/2GB/64GB\* | Firstline workers, call centers, education/training/CRM access.  | Windows 10 Enterprise with OS Optimizations  | Office (web-based), Microsoft Edge, OneDrive, lightweight line-of-business app (call center application – web-apps), Defender support. |
| 2vCPU/4GB/256GB<br>2vCPU/4GB/128GB<br>2vCPU/4GB/64GB  | Mergers and acquisition, short-term and seasonal, customer services  | Windows 10/11 Enterprise with Microsoft 365 and Teams | Microsoft 365 Apps, Microsoft Teams (Audio only),  OneDrive, Adobe Reader, Edge, line-of-business apps, Defender support. |
| 2vCPU/8GB/256GB<br>2vCPU/8GB/128GB | Bring-your-own-PC, work from home, market researchers, government, consultants. | Windows 10/11 Enterprise with Microsoft 365 and Teams | Microsoft 365 Apps, Microsoft Teams, Outlook, Excel, Access, PowerPoint, OneDrive, Adobe Reader, Edge, line-of-business apps, Defender support. |
| 4vCPU/16GB/512GB<br>4vCPU/16GB/256GB<br>4vCPU/16GB/128GB | Finance, government, consultants, healthcare services, bring-your-own-PC, work from home. | Windows 10/11 Enterprise with Microsoft 365 and Teams | Microsoft 365 Apps, Microsoft Teams, Outlook, Excel, Access, PowerPoint, Power BI, Dynamics 365, OneDrive, Adobe Reader, Edge, line-of-business app, Defender support. |
| 8vCPU/32GB/512GB<br>8vCPU/32GB/256GB<br>8vCPU/32GB/128GB | Software developers, engineers, content creators, design and engineering workstations. | Windows 10/11 Enterprise with Microsoft 365 and Teams | Microsoft 365 Apps, Microsoft Teams, Outlook, Access, OneDrive, Adobe Reader, Edge, Power BI, Visual Studio Code, line-of-business apps, Defender support. |

\* The 1vCPU option is being retired. Instead, we recommend the 2vCPU as the minimum configuration for new purchases.

The recommended gallery image is available in the Provisioning Policy marketplace. For more information, see [Device images overview](device-images.md).

## Test performance  

To ensure experience expectations are met, you should test your deployment with simulation tools. You can track the user experience and resource consumption with services like Endpoint Analytics.

<!-- ########################## -->
## Next steps

For more information, see [Device images overview](device-images.md).
