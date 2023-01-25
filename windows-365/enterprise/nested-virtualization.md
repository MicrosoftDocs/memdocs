---
# required metadata
title: Set up virtualization-based workloads on your Windows 365 Cloud PC.
titleSuffix:
description: Learn how to set up nested virtualization on your Windows 365 Cloud PC.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 07/07/2022
ms.topic: how-to
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
ms.collection: M365-identity-device-management
---

# Set up virtualization-based workloads support

Virtualization-based workloads let customers use the following systems on their Windows 365 Enterprise Cloud PCs:

- Windows Subsystem for Linux (WSL)
- Windows Subsystem for Android
- Sandbox
- Hyper-V  

## Requirements

To use virtualization-based workloads, the Cloud PC must meet these requirements:

- 4vCPU Cloud PC (Downsizing to 2vCPU Cloud PCs will disable nested virtualization)
- Be in one of the [supported regions](requirements.md?tabs=enterprise%2Cent#supported-azure-regions-for-cloud-pc-provisioning).

## Set up virtualization-based workloads

To set up a specific virtualization-based workloads system, see the following articles:
    - [Set up a WSL development environment](/windows/wsl/setup/environment).
    - [Windows Subsystem for Android™️](/windows/android/wsa/).
    - [Install Hyper-V on Windows 10](/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v).


<!-- ########################## -->
## Next steps

For more information about virtualization-based workloads, see [Run Hyper-V in a Virtual Machine with Nested Virtualization](/virtualization/hyper-v-on-windows/user-guide/nested-virtualization).
