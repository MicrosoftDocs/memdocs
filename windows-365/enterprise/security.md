---
# required metadata
title: Overview of security concepts in Windows 365
titleSuffix:
description: Learn about security concepts in Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 07/20/2022
ms.topic: overview
ms.service: cloudpc
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: chrimo
ms.suite: ems
search.appverid: 
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# Windows 365 security

<< introduction >>

## Secure Cloud PC access

The first security boundary to protect is access to the Cloud PC through the Windows 365 service.

## Secure Cloud PC devices

After securing access to Cloud PCs, the next security boundary is the Cloud PC, aka Windows device, itself.

### Security features enabled by default

All new Cloud PCs have the following security components enabled by default:

- **vTPM**: Short for virtual Trusted Platform Module, a vTPM provides Cloud PCs their own dedicate TPM instance that acts as a secure vault for keys and measurements. For more information, see [vTPM](/azure/virtual-machines/trusted-launch#vtpm).
- **Secure Boot**: Secure Boot is a feature that will prevent the Windows operating system from booting if untrusted rootkits or boot kits are installed on the machine. For more information, see [secure boot](/azure/virtual-machines/trusted-launch#secure-boot).

With both security components enabled, Windows 365 supports enabling the following Windows security features:

- Hypervisor Code Integrity (HVCI)
- [Microsoft Defender Credential Guard](/windows/security/identity-protection/credential-guard/credential-guard-manage)

### Security features requiring specific Cloud PC SKUs or configuration

The following security components are enabled by default on specific Cloud PC SKUs or configurations:

- **Virtualization-based workloads**
    - **Description**: Virtualization-based workloads typically require the Windows device to enable the Hyper-V feature and run the workloads in an isolated space, to protect the Windows OS from any security threats.
    - **Security features supported**:
        - [Microsoft Defender Application Guard](/windows/security/threat-protection/microsoft-defender-application-guard/md-app-guard-overview)
        - [Windows Sandbox](/windows/security/threat-protection/windows-sandbox/windows-sandbox-overview)
    - **Required configuration**: Cloud PC must have 8 vCPU and 32 GB RAM. See [set up virtualization-based workloads support](nested-virtualization) for more information.

## Secure Cloud PC data
