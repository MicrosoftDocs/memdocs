---
# required metadata
title: What is Windows 365 Enterprise? 
titleSuffix:
description: What is Windows 365 Enterprise?
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 05/09/2023
ms.topic: overview
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: naramkri
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started; intro-overview
ms.collection:
- M365-identity-device-management
- tier2
- essentials-overview
---

# What is Windows 365 Enterprise?

Windows 365 Enterprise is a cloud-based service that automatically creates a new type of Windows virtual machine (Cloud PCs) for your end users. It provides the productivity, security, and collaboration benefits of Microsoft 365. Windows 365 Enterprise uses:

- [Microsoft Intune](/mem/) to manage the Cloud PCs.
- Microsoft Entra ID for identity and access control.
- Azure Virtual Desktop for remote connectivity.

Each Cloud PC is assigned to an individual user and is their dedicated Windows device. Assigning a Cloud PC to a user is just like assigning an Exchange Online mailbox to a user. When a [Windows 365 license](https://www.microsoft.com/windows-365/enterprise/compare-plans-pricing) is assigned to a user:

- Provisioning of a new Cloud PC automatically starts.
- The Cloud PC is enrolled into Microsoft Intune.

With the Windows 365 service, you can:

- Automatically provision on-demand Windows Enterprise Cloud PCs for your users. [Provisioning](provisioning.md) is the automatic creation of Cloud PCs for your end users. After you set up Cloud PC support in Microsoft Intune, a Cloud PC is automatically provisioned whenever you assign a user with a Cloud PC license to an appropriate Microsoft Entra user group. To set up Cloud PC support, you’ll:
  - [Optional] Create [Azure network connections](azure-network-connections.md), which are links between the Cloud PCs and your on-premises resources.
  - Choose a built-in, optimized Windows [image](device-images.md) (or create your own) to use as the basis for each Cloud PC.
- Manage your Cloud PCs like your organization’s other devices in [Microsoft Intune](https://go.microsoft.com/fwlink/?linkid=2109431). Based on your configuration, Cloud PCs are either:
  - Joined to your enterprise Active Directory domain and synced to Microsoft Entra ID.
  - Directly joined to Microsoft Entra ID.
  
  Regardless of the join type, your Cloud PCs are fully managed by Microsoft Intune. Windows 365 is fully integrated into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). Cloud PCs are seamlessly managed in Microsoft Intune like any other supported device, including configuration, apps, and updates.
- [Configure provisioning policies](create-provisioning-policy.md) to create custom Cloud PC configurations.
- Use device groups, policies, and security baselines to customize your Cloud PC configurations to support different user needs.
- Pre-install [apps](app-overview.md) in your custom Cloud PC image and push more apps to them through Microsoft Intune.

### Other versions of Windows 365

There are other versions available for Windows 365. For more information, see [What is Windows 365?](../overview.md).

[!INCLUDE [What is a Cloud PC?](../includes/what-is-cloud-pc.md)]

## Billing

Cloud PCs are billed in a per-user per-month cost model. This model means your organization doesn’t have to manage the variability of compute and storage costs of a traditional hosted desktop model.

By default, Cloud PCs are joined to your enterprise Active Directory domain, synced to Microsoft Entra ID, and fully managed by Microsoft Intune.

## Microsoft 365 Lighthouse

Managed Server Providers (MSPs) can manage Cloud PCs in Microsoft 365 Lighthouse for their customer tenants. For more information, see [Windows 365 (Cloud PCs) page overview](/microsoft-365/lighthouse/m365-lighthouse-win365-page-overview).

<!-- ########################## -->
## Next steps

[Plan your Cloud PC deployment](planning-guide.md).

If you're looking for Windows 365 Business documentation, see [Get started with Windows 365 Business and Cloud PCs](/microsoft-365/admin/setup/get-started-windows-365-business).
