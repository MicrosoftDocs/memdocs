---
# required metadata
title: What is Windows 365? - Azure | Microsoft Docs
titleSuffix:
description: What is Windows 365?
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 07/23/2021
ms.topic: overview
ms.service: cloudpc
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: naramkri
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# What is Windows 365?

Windows 365 is a cloud-based service that automatically creates a new type of Windows virtual machine (Cloud PCs) for your end users. It provides the productivity, security, and collaboration benefits of Microsoft 365. Windows 365 uses:

- [Microsoft Endpoint Manager](/mem/) to manage the Cloud PCs.
- Azure Active Directory (Azure AD) for identity and access control.
- Azure Virtual Desktop for remote connectivity.

Each Cloud PC is assigned to an individual user and is their dedicated Windows device. Assigning a Cloud PC to a user is just like assigning an Exchange Online mailbox to a user. When a Windows 365 license is assigned to a user, provisioning of a new Cloud PC automatically starts and the Cloud PC is enrolled into Microsoft Endpoint Management.

With the Windows 365 service, you can:

- Automatically provision on-demand Windows Enterprise Cloud PCs for your users. [Provisioning](provisioning.md) is the automatic creation of Cloud PCs for your end users. After you set up Cloud PC support in Microsoft Endpoint Manager, a Cloud PC is automatically provisioned whenever you assign a user with a Cloud PC license to an appropriate Azure AD user group. To set up Cloud PC support, you’ll:
  - Create [on-premises network connections](on-premises-network-connections.md) which are links between the Cloud PCs and your on-premises resources.
  - Choose a built-in, optimized Windows [image](device-images.md) (or create your own) to use as the basis for each Cloud PC.
- Manage your Cloud PCs like your organization’s other devices in [Microsoft Endpoint Manager](/intune/). By default, Cloud PCs are joined to your enterprise Active Directory domain, synced to Azure Active Directory, and fully managed by Microsoft Endpoint Manager. Windows 365 is fully integrated into the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431). Cloud PCs are seamlessly managed in Microsoft Endpoint Manager like any other supported device, including configuration, apps, and updates.
- [Configure provisioning policies](create-provisioning-policy.md) to create custom Cloud PC configurations.
- Use device groups, policies, and security baselines to customize your Cloud PC configurations to support different user needs.
- Pre-install [apps](app-overview.md) in your custom Cloud PC image and push additional apps to them through Microsoft Endpoint Manager.

## What is a Cloud PC?

A Cloud PC is a highly available, optimized, and scalable virtual machine providing end users with a rich Windows desktop experience. It’s hosted in the Windows 365 service and is accessible from anywhere, on any endpoint.

End users have a 1:1 relationship with their Cloud PC. It’s their own personal PC in the cloud. Users can connect to their Cloud PC by using [windows365.microsoft.com](https://windows365.microsoft.com/). [Browser and app-based access](end-user-access-cloud-pc.md) is available for Windows, Mac, iOS, and Android devices.

### Creating a Cloud PC

Cloud PCs are created ([provisioned](provisioning.md)) automatically by the Windows 365 service when an end user in an appropriate Azure AD user group is assigned a Windows 365 license.

Admins don't manually create Cloud PCs.

## Billing

Cloud PCs are billed in a per-user per-month cost model. This model means your organization doesn’t have to manage the variability of compute and storage costs of a traditional hosted desktop model.

By default, Cloud PCs are joined to your enterprise Active Directory domain, synced to Azure Active Directory, and fully managed by Microsoft Endpoint Manager.

<!-- ########################## -->
## Next steps

[Plan your Cloud PC deployment](planning-guide.md).
