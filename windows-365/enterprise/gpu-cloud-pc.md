---
# required metadata
title: GPU Cloud PCs in Windows 365
titleSuffix:
description: Learn about GPU-enabled Cloud CPs in Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 11/15/2023
ms.topic: overview
ms.service: windows-365
ms.subservice:
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: sefriend
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# GPU Cloud PCs in Windows 365 (preview)

Windows 365 offers GPU-enabled Cloud PCs that are suitable for graphics intense workloads that need to be performance optimized. These offerings can help with graphic design, image and video rendering, 3D modeling, data processing and visualization applications that require a GPU to perform.

Three GPU offerings are available for Window 365 Enterprise Cloud PCs:

| GPU offering | Intended for | 
| --- | --- |
| Windows 365 Enterprise GPU 4 vCPU, 16-GB RAM, 4-GB vRAM, 512 GB | Applications that benefit from basic graphic acceleration on one 3840x2160 display or up to two 1920x1080p displays. |
| Windows 365 Enterprise GPU 8 vCPU, 56-GB RAM, 12-GB vRAM, 1 TB | Applications with greater specification requirements and high-end graphics workloads on up to four 3840x2160 displays. |
| Windows 365 Enterprise GPU 16 vCPU, 110-GB RAM, 16-GB vRAM, 1 TB | Graphics intensive workloads that demand high performance and have strict latency requirements. |

For more information on these offerings, see [Cloud PC size recommendations](cloud-pc-size-recommendations.md).

Other details about GPU-enabled Cloud PCs include:

- Windows 365 GPU configurations are powered by NVIDIA and AMD.
- These GPU offerings define the minimum specs provided for vCPU, RAM, and vRAM. It's possible that customers might get more vCPU, RAM, and/or vRAM depending on capacity in the customer's deployment region. Customers never get less vCPU, RAM, and/or vRAM than their license specifies.
- GPU-enabled Cloud PCs require fewer vCPUs for optimized performance because they can offload rendering to the GPU.

For more information about how to choose your GPU configuration, see [Announcing Windows 365 GPU-enabled Cloud PCs now in Public Preview](https://aka.ms/w365/gpu/blog).

## Registry keys and drivers on GPU Cloud PCs

Registry keys are automatically set during the provisioning process.

Supported drivers are automatically installed as part of the provisioning process. You don't need to manually install drivers.

## In public preview

The GPU offerings are in [public preview](../public-preview.md). During this time, GPU offerings are available:

- Through a limited application process using [this form](https://aka.ms/win365gpu). Select customers will get private access to purchase licenses, after which they can use the normal [provisioning policy process](create-provisioning-policy.md) to create GPU-enabled Cloud PCs. For more information about licensing, see [Windows 365 Licensing](https://www.microsoft.com/licensing/product-licensing/windows-365).
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
