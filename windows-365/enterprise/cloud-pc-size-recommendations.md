---
# required metadata
title: Windows 365 size recommendations
titleSuffix:
description: Learn about the different Cloud PC sizes that are available with different SKUs in Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 07/25/2024
ms.topic: overview
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: chbrinkh
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Cloud PC size recommendations

Windows 365 offers fixed-price licensing (through Microsoft 365) for different Cloud PC sizes. You should assess your business requirements to determine which sizes make sense for your users.  

If extra resources are needed for the Cloud PC, an admin or end user can easily upgrade the size of their Cloud PC. For more information, see [Resize a Cloud PC](resize-cloud-pc.md).  

For information about end-user hardware requirements, see [End-user hardware requirements](..\end-user-hardware-requirements.md).

This table shows examples of the different sizes available for a Cloud PC:

| Cloud PC CPUs, RAM, and storage | Example scenarios | Recommended apps |
| --- | --- | --- |
| 2vCPU/4GB/256GB<br>2vCPU/4GB/128GB<br>2vCPU/4GB/64GB  | Frontline workers, call centers, education/training/CRM access, mergers and acquisition, short-term and seasonal, customer services.  | Microsoft 365 Apps, Microsoft Teams (Audio only),  OneDrive, Adobe Reader, Microsoft Edge, line-of-business apps, Defender support. |
| 2vCPU/8GB/256GB<br>2vCPU/8GB/128GB | Bring-your-own-PC, work from home, market researchers, government, consultants. | Microsoft 365 Apps, Microsoft Teams, Outlook, Excel, Access, PowerPoint, OneDrive, Adobe Reader, Microsoft Edge, line-of-business apps, Defender support. |
| 4vCPU/16GB/512GB<br>4vCPU/16GB/256GB<br>4vCPU/16GB/128GB | Finance, government, consultants, healthcare services, bring-your-own-PC, work from home. | Microsoft 365 Apps, Microsoft Teams, Outlook, Excel, Access, PowerPoint, Power BI, Dynamics 365, OneDrive, Adobe Reader, Microsoft Edge, line-of-business app, Defender support. |
| 8vCPU/32GB/512GB<br>8vCPU/32GB/256GB<br>8vCPU/32GB/128GB | Software developers, engineers, content creators, design and engineering workstations. | Microsoft 365 Apps, Microsoft Teams, Outlook, Access, OneDrive, Adobe Reader, Microsoft Edge, Power BI, Visual Studio Code, virtualization-based workloads: Hyper-V, Windows Subsystem for Linux (WSL), line-of-business apps, and Defender support. |
| GPU Standard 4vCPU/16GB/4GBvRAM/512GB<br>GPU Super 8CPU/56GB/12GBvRAM/1TB<br>GPU Max 16vCPU/110GB/16GBvRAM/1TB<br>For details, see [GPU Cloud PCs](gpu-cloud-pc.md).| Graphic design, image and video rendering, 3D modeling, gaming, data processing, and visualization |Microsoft 365 Apps, Microsoft Teams, Outlook, Excel, Access, Adobe, Figma, Autodesk, Revit, Illustrator, Blender, Unity, ArcGIS, Microsoft Edge, Power BI, Visual Studio Code, line-of-business apps, Defender support. |
| 16vCPU/64GB/512GB<br>16vCPU/64GB/1TB | Software development, engineering, data analysis and visualization, financial services and wealth management. | Microsoft 365 Apps, Microsoft Teams, Outlook, Excel, Access, Adobe Reader, Microsoft Edge, Power BI, Tableau, Visual Studio Code, Blackrock Aladdin, Bloomberg, Eclipse, line-of-business apps, Defender support. |

The recommended gallery image is available in the Provisioning Policy marketplace. For more information, see [Device images overview](device-images.md).

## Test performance  

To ensure experience expectations are met, you should test your deployment with simulation tools. You can track the user experience and resource consumption with services like Endpoint Analytics.

<!-- ########################## -->
## Next steps

For more information, see [Device images overview](device-images.md).
