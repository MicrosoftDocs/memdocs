---
# required metadata
title: Set up nested virtualization on your Windows 365 Cloud PC.
titleSuffix:
description: Learn how to set up nested virtualization on your Windows 365 Cloud PC.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 04/05/2022
ms.topic: how-to
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

# Set up nested virtualization on your Cloud PC (preview)

Nested virtualization is a feature that lets customers use systems like the following on their Windows 365 Enterprise Cloud PCs:

- Windows Subsystem for Linux (WSL)
- Windows Subsystem for Android
- Sandbox
- Hyper-V  

## Requirements

To use nested virtualization, the Cloud PC must meet these requirements:

- 8vCPU/32 (Cloud PCs resized from 1vCPU/2GB and 2vCPU/4GB to 8vCPU/32GB aren't supported)
- Be in one of these regions (other regions aren't currently supported):
  - US East
  - US East 2
  - US West 3
  - US South central
  - Australia East
  - Europe North
  - Europe West
  - UK South
  - Canada Central
  - India Central
  - Japan East
  - France Central

## Set up nested virtualization

1. If the Cloud PC was provisioned before April 5, 2022, you must [reprovision](reprovision-cloud-pc.md) the Cloud PC.
2. To set up a specific nested virtualizaiton system, see the following articles:
    - [Set up a WSL development environment](/windows/wsl/setup/environment).
    - [Windows Subsystem for Android™️](/windows/android/wsa/).
    - [Install Hyper-V on Windows 10](/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v).


<!-- ########################## -->
## Next steps

For more information about nested virtualization, see [Run Hyper-V in a Virtual Machine with Nested Virtualization](/virtualization/hyper-v-on-windows/user-guide/nested-virtualization).