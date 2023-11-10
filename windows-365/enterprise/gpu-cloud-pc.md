---
# required metadata
title: Windows 365 size recommendations
titleSuffix:
description: Learn about the different Cloud PC sizes that are available with different SKUs in Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 03/24/2023
ms.topic: overview
ms.service: windows-365
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
ms.collection:
- M365-identity-device-management
- tier2
---

# GPU Cloud PCs in Windows 365

Graphic Processing Unit (GPU)-enabled Cloud PCs are suitable for graphics intense workloads that need to be performance optimized. Such workloads include graphic design, image and video rendering, 3D modeling, gaming, data processing and visualization applications that require a GPU to perform. GPU-enabled Cloud PCs require fewer vCPUs for optimized performance because they can offload rendering to the GPU.

Three GPU offerings are available for Window 365 Enterpise Cloud PCs:

- Windows 365 Enterprise GPU 4 vCPU, 16 GB RAM, 4 GB vRAM, 512 GB
- Windows 365 Enterprise GPU 8 vCPU, 56 GB RAM, 12 GB vRAM, 1 TB  
- Windows 365 Enterprise GPU 16 vCPU, 110 GB RAM, 16 GB vRAM, 1 TB

For more details on these offerings, see [Cloud PC size recommendations](cloud-pc-size-recommendations.md).

Windows 365 GPU configurations are powered by NVIDIA and AMD.

These GPU offerings define the minimum specs provided for vCPU, RAM, and vRAM. It's possible that customers might get more vCPU, RAM, and/or vRAM depending on capacity in the customer's deployment region. Customers will never get less vCPU, RAM, and/or vRAM than their license specifies.  

For more information about how to choose your GPU configuration, see [Announcing Windows 365 GPU-enabled Cloud PCs now in Public Preview](https://aka.ms/w365/gpu/blog).

## Registry keys

Registry keys and supported drivers are automatically installed on GPU-enabled Cloud PCs as part of the provisioning process. You don't need to manually install registry keys. 

## In public preview

The GPU offerings are in [public preview](../public-preview.md). During this time, GPU offerings are available:

- Through a limited application process using [this form](https://aka.ms/win365gpu).
- For Windows 365 Enterprise only.
- In the following regions:
  - East US
  - East US 2
  - West Europe
  - Central India
  - West US 3
  - South Central US
  - Australia East
  - Southeast Asia
  - North Europe
  - Germany West Central

## Features not supported by GPU offerings

- Step-up SKUs
- Resize
- Nested virtualization

<!-- ########################## -->
## Next steps

For more information on Cloud PC offerings, see [Cloud PC size recommendations](cloud-pc-size-recommendations.md).
