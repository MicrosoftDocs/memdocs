---
# required metadata
title: Windows 365 GPU-enabled Cloud PC performance
titleSuffix:
description: Learn about GPU-enabled Cloud PC performance in Windows 365.
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

# Windows 365 GPU-enabled Cloud PC performance

Windows 365 provides the following Graphics Processing Unit (GPU)-enabled Cloud PC configurations for Windows 365 Enterprise and Windows 365 Frontline:  

- Windows 365 GPU Standard
- Windows 365 GPU Super
- Windows 365 GPU Max

These offerings are supported by NVIDIA and AMD to cater to:

- graphic design
- image and video rendering
- 3D modeling
- data visualization and processing workloads

## Updates

Windows 365 GPU-enabled Cloud PCs are provisioned with state-of-the-art and high-performance hardware. However, infrastructure evolves over time, which might result in updates to the underlying virtual machines and hardware available to customers. These adjustments are necessary to implement improvements, maintain performance, and enhance the end-user experience. The Windows 365 product team regularly conducts rigorous testing, so that each update contributes positively to the performance that you experience with Windows 365 GPU-enabled Cloud PCs. This article explores how we test the performance of the Windows 365 GPU-enabled Cloud PCs, and the relative workload targets of the three offerings.

## Graphics performance testing

To assess the performance of the Windows 365 GPU-enabled Cloud PCs, we conduct various industry standard graphics tests:

- Rendering performance tests to evaluate GPU stability and performance. We use various sample files to measure rendering speed and quality. These tests help us understand how well the GPU handles complex visual tasks.
- Rendering resolution test to evaluate frame rate and latency. We test different resolutions (like 1080p and 4K) to observe how the GPU performs under varying display demands. High resolutions can stress the GPU more.
- CPU tests to understand the impact of CPU performance on graphics tasks. We analyze how well the CPU offloads to the GPU during rendering and other graphics-intensive operations.
- Stress tests to evaluate overall system performance and reliability. The system is subjected to heavy workloads, simulating real-world usage. These tests help identify any bottlenecks or issues.

All GPU-enabled Cloud PC configurations are tested in the same production environment within the same region. Specific third-party agents deployed by customers aren't considered in the routine testing, as they may have their own resource requirements affecting performance.

Conducting your own testing can provide valuable insights that closely resemble your users’ graphics needs. Include the graphics applications that your users use and examine the test results to make informed decisions for your users. For more information, see the [Planning guide for Windows 365](planning-guide.md).

## Graphics workload targets

While the software rendering of non-GPU-enabled Windows 365 Cloud PCs does a great job for most applications, there are some applications that might require the performance of direct calls into APIs that use a GPU. Common examples include products from Adobe, ArcGIS, Autodesk, and Dassault Systèmes, among others. Other products might necessitate the use of a dedicated GPU or are optimized to perform more efficiently with one, according to their published system requirements on their respective websites.

| GPU offering | Intended for | Displays supported | Comparable to | AI development support |
| --- | --- | --- | --- |
| Windows 365 GPU Standard | Graphics applications requiring 8-GB vRAM or less. | One 3840x2160 display or up to two 1920x1080 displays. | Devices with entry level dedicated graphics GPUs. | No. |
| Windows 365 GPU Super | High-end graphics workloads requiring 12-GB vRAM or less. | Up to four 3840x2160 displays. | Desktop devices with dedicated graphics GPUs. | No. |
| Windows 365 GPU Max | Maximum performance requiring up to 24-GB vRAM. | Multiple display support at higher resolutions. | Desktop graphics workstations servicing the most demanding graphics workloads. | Yes, with VSCode AI Toolkit, Phi-3 with ONNX, and more. |

All GPU-enabled Cloud PCs are compatible with and support AI functionalities that are integrated into widely used software applications like Copilot. For AI development or for running AI tasks that require intensive GPU processing, use Windows 365 GPU Max.

Microsoft hosts GPU-enabled Cloud PCs using the most recent iteration of Microsoft Hyper-V. Each Cloud PC is equipped with a storage drive (C:) for your files and programs, in addition to a substantial ephemeral disk (D:). It’s advisable to use the D: drive for caching temporary files, which can enhance the performance of applications requiring "scratch" disks for handling extensive data sets.

Be sure to review your software vendors’ system requirements before deciding which GPU-enabled Cloud PC offering is best for you. If you find that the current GPU-enabled Cloud PC size doesn't meet your needs, you can choose an offering with a higher configuration.

<!-- ########################## -->
## Next steps

For more information on GPU Cloud PC offerings, see [GPU Cloud PCs in Windows 365](gpu-cloud-pc.md).
