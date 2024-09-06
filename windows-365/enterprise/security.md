---
# required metadata
title: Overview of security concepts in Windows 365
titleSuffix:
description: Learn about security concepts in Windows 365.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 08/28/2024
ms.topic: overview
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: chrimo
ms.suite: ems
search.appverid: 
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
- essentials-security
---

# Windows 365 security

Windows 365 provides an end-to-end connection flow for users to do their work effectively and securely. Windows 365 is built with [Zero Trust](/security/zero-trust/zero-trust-overview) in mind, providing the foundation for you to implement controls to better secure your environment across the 6 pillars of Zero Trust. You can implement Zero Trust controls for the following categories:

- Securing the access to the Cloud PC
    - Aligns with securing the **Identity**, where you can place more measures on who can access the Cloud PC and under which conditions.
- Securing the Cloud PC device itself
    - Aligns with securing the **Endpoint**, where you can place more measures on the Cloud PC devices since that is the device being used to access organizational data.
- Securing the Cloud PC data and other data available while using the Cloud PC
    - Aligns with securing the **Data**, where you can place more measures on the data itself or on how the Cloud PC user accesses the data.

Take a look at the following sections to better understand the components and features available to you to secure your Cloud PC environment.

## Secure Cloud PC access

The first consideration for securing your environment is to secure access to the Cloud PC.

As described in [identity and authentication](./identity-authentication.md#authentication), there are two authentication challenges to access the Cloud PC:

- The Windows 365 service.
- The Cloud PC.

The primary control for securing access is by using Microsoft Entra Conditional Access to conditionally grant access to the Windows 365 service. To secure access to the Cloud PC, see [set conditional access policies](./set-conditional-access-policies.md).

## Secure Cloud PC devices

The second consideration for securing your environment is to secure the Cloud PC device itself.

### Security features enabled by default

All new Cloud PCs have the following security components enabled by default:

- **vTPM**: Short for virtual Trusted Platform Module, a vTPM provides Cloud PCs their own dedicated TPM instance that acts as a secure vault for keys and measurements. For more information, see [vTPM](/azure/virtual-machines/trusted-launch#vtpm).
- **Secure Boot**: Secure Boot is a feature that prevents the Windows operating system from booting if untrusted rootkits or boot kits are installed on the machine. For more information, see [secure boot](/azure/virtual-machines/trusted-launch#secure-boot).

With both security components enabled, Windows 365 supports enabling the following Windows security features:

- Hypervisor Code Integrity (HVCI)
- [Microsoft Defender Credential Guard](/windows/security/identity-protection/credential-guard/credential-guard-manage)

### Security features requiring specific Cloud PC SKUs or configuration

The following security components are enabled by default on specific Cloud PC SKUs or configurations:

- **Virtualization-based workloads**
    - **Description**: Virtualization-based workloads typically require the Windows device to enable the Hyper-V feature and run the workloads in an isolated space, to protect the Windows OS from any security threats.
    - **Security features**:
        - [Microsoft Defender Application Guard](/windows/security/threat-protection/microsoft-defender-application-guard/md-app-guard-overview)
        - [Windows Sandbox](/windows/security/threat-protection/windows-sandbox/windows-sandbox-overview)
    - **Required configuration**: Cloud PC must have 4 vCPU and 16-GB RAM or more. For more information, see [set up virtualization-based workloads support](nested-virtualization.md#requirements).

> [!NOTE]
> Given the technological complexity, the security promise of Microsoft Defender Application Guard (MDAG) may not hold true on VMs and in VDI environments. Hence, MDAG is currently not officially supported on VMs and in VDI environments. However, for testing and automation purposes on non-production machines, you may enable MDAG on a VM by enabling Hyper-V nested virtualization on the host.

## Microsoft Purview Customer Lockbox

Microsoft Purview Customer Lockbox can be turned on by an admin. Customer Lockbox ensures that Microsoft can't access a customer's content to do service operations without your explicit approval. You can turn Customer Lockbox on or off in the Microsoft 365 admin center. For more information, see [Microsoft Purview Customer Lockbox](/purview/customer-lockbox-requests).

## Secure Cloud PC data

The third consideration for securing your environment is to secure the Cloud PC data and other data that is made available by using the Cloud PC.

### Security of Cloud PC data

The data of the Cloud PC data itself is secured through encryption. For more details, see [data encryption in Windows 365](./encryption.md).

### Security of data available on the Cloud PC

Securing the data available to users on their Cloud PCs should be no different than securing the data available to users on work-assigned Windows PCs. The Cloud PC should be accessed through Remote Desktop Protocol (RDP).

To manage RDP features available to the user during their Cloud PC connection, see [manage RDP device redirections for Cloud PCs](./manage-rdp-device-redirections.md).

## Client update security

Windows 365 Cloud PCs can be accessed from various operating system platforms and clients available in those platforms.

- **Windows OS platforms**: Windows 365 can be accessed using Remote Desktop client for Windows and the Windows 365 App. Both these apps receive updates using the Windows Update service. For more information, see [Windows Update security](/windows/deployment/update/windows-update-security).
- **Apple devices (macOS and iOS)**: Remote desktop client apps and their updates are distributed by Apple's app store. For more information about MacOS and iOS security measures, see [Apple Platform Security](https://support.apple.com/en-sg/guide/security/welcome/web).
- **Android platforms**: Android platform apps downloaded from Google play stores conform to the Google play store terms and conditions. For more information, see [Google Play Terms of Service](https://play.google.com/about/play-terms/index.html).

## Next steps

For more information about Windows Update security, see [Windows Update security](/windows/deployment/update/windows-update-security).
