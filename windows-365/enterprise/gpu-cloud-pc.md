---
# required metadata
title: GPU Cloud PCs in Windows 365
titleSuffix:
description: Learn about GPU-enabled Cloud PCs in Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 07/31/2024
ms.topic: overview
ms.service: windows-365
ms.subservice: windows-365-enterprise
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

# GPU Cloud PCs in Windows 365

Windows 365 offers GPU-enabled Cloud PCs that are suitable for graphics intense workloads that need to be performance optimized. These offerings can help with graphic design, image and video rendering, 3D modeling, and data processing and visualization applications that require a GPU to perform.

Three GPU offerings are available for Window 365 Enterprise (including FedRamp) and Windows 365 Frontline Cloud PCs:

| GPU offering | Minimum specs | Powered by | Intended for |
| --- | --- |
| Windows 365 Enterprise GPU Standard | 4 vCPU, 16-GB RAM, 8-GB vRAM, 512 GB (with 176-GB temporary storage) | NVIDIA and AMD | Applications that benefit from basic graphic acceleration on one 3840x2160 display or up to two 1920x1080p displays. |
| Windows 365 Enterprise GPU Super | 8 vCPU, 56-GB RAM, 12-GB vRAM, 1 TB (with 352-GB temporary storage) | NVIDIA | Applications with greater specification requirements and high-end graphics workloads on up to four 3840x2160 displays. |
| Windows 365 Enterprise GPU Max | 16 vCPU, 110-GB RAM, 16-GB vRAM, 1 TB (with 352-GB temporary storage) | NVIDIA | Graphics intensive workloads that demand high performance and have strict latency requirements. |

For more information on these offerings, see [Cloud PC size recommendations](cloud-pc-size-recommendations.md).

For purchasing the GPU offerings, contact your account team. GPU offerings aren't available from the web direct channel.

## Registry keys and drivers on GPU Cloud PCs

Registry keys are automatically set during the provisioning process.

Supported drivers are automatically installed as part of the provisioning process. You don't need to manually install drivers. However, drivers aren't automatically updated, so must manually update drivers as needed.

## Allowlist

You must allow the following URLs on each Windows 365 GPU Cloud PC:
 
| URL | Hardware |
| --- | --- |
| download.microsoft.com | Nvidia, AMD |
| go.microsoft.com | Nvidia, AMD |
| raw.githubusercontent.com/Azure/azhpc-extensions/master/NvidiaGPU/resources.json<br>(Nvidia driver resource file) | Nvidia |
| raw.githubusercontent.com/Azure/azhpc-extensions/master/AmdGPU/resources.json (AMD driver resource file) | AMD |

## Supported regions

The GPU offerings are available in all [Windows 365 supported regions](requirements.md?tabs=enterprise%2Cent#supported-azure-regions-for-cloud-pc-provisioning) except for the following:

- Central US
- Norway East
- West Europe

The West US 2 region is supported but is a restricted region.

## Recommendations when using GPU Cloud PCs

For optimal performance of GPU-enabled Cloud PCs, consider these recommendations:

- Make sure that your network is configured to turn on UDP by default. For more information about UDP, see [RDP Shortpath](/azure/virtual-desktop/rdp-shortpath?tabs=public-networks#network-configuration).
- Make sure that you're running your GPU Cloud PC in full screen mode. Minimized windows require extra processing and coordination with the local device that can impede the session performance.
- Use the Windows app for optimal connection experience.
- Use Windows 11 Cloud PCs.
- GPU-enabled Cloud PCs come pre-provisioned with the correct driver needed for the best experience. For information about installing drivers, see [Install NVIDIA GPU drivers on N-series VMs running Windows](/azure/virtual-machines/windows/n-series-driver-setup) and [Install AMD GPU drivers on N-series VMs running Windows](/azure/virtual-machines/windows/n-series-amd-driver-setup) (for the Standard SKU only in limited regions). The use of any external drivers, including drivers from NVIDIA and AMD websites, isn't supported.
- Don’t use the Multimedia Redirection extension for the browser or for Teams. By default, this extension is uninstalled for GPU-enabled Cloud PCs during provisioning.

<!-- ########################## -->
## Next steps

For more information on Cloud PC offerings, see [Cloud PC size recommendations](cloud-pc-size-recommendations.md).
