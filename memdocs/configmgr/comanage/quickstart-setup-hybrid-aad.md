---
title: Set up hybrid Microsoft Entra ID
titleSuffix: Configuration Manager
description: If your environment currently has domain-joined Windows devices, set up hybrid Microsoft Entra ID before you enable co-management
ms.date: 11/08/2021
ms.subservice: co-management
ms.service: configuration-manager
ms.topic: install-set-up-deploy
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Set up hybrid Microsoft Entra ID for co-management

If you have Windows 10 or later devices joined to on-premises Active Directory, before you enable co-management in Configuration Manager, first join these devices to Microsoft Entra ID. This process is called Microsoft Entra hybrid join.

In the following video, senior program manager Sandeep Deo and product marketing manager Adam Harbour discuss and demo configuring devices in Microsoft Entra ID:

> [!VIDEO https://aka.ms/docs/player?id=a40c36a8-8e70-4a5e-9df1-3af055e8d6c3]

The Microsoft Entra hybrid join process automatically registers your on-premises domain-joined devices with Microsoft Entra ID. For more information on this process, see the following articles:

- [What is a device identity in Microsoft Entra ID?](/azure/active-directory/devices/overview)
- [How to plan your Microsoft Entra hybrid join](/azure/active-directory/devices/hybrid-azuread-join-plan)

Microsoft Entra hybrid join is one of the key foundations for co-management. This process can be challenging for some customers, for example:

- Your organization uses a third-party identity solution
- The complexities of setting up Active Directory Federation Services (ADFS)

Resolving these challenges can take some guidance. This article helps to mitigate any delays.

> [!TIP]
> As we talk with our customers that are using Microsoft Intune to deploy, manage, and secure their client devices, we often get questions regarding co-managing devices and Microsoft Entra hybrid joined devices. Many customers confuse these two topics. Co-management is a management option, while Microsoft Entra ID is an identity option. For more information, see [Understanding hybrid Microsoft Entra ID and co-management scenarios](https://techcommunity.microsoft.com/t5/microsoft-endpoint-manager-blog/understanding-hybrid-azure-ad-join-and-co-management/ba-p/2221201). This blog post aims to clarify Microsoft Entra hybrid join and co-management, how they work together, but aren't the same thing.

## How to do it

Devices are similar to users when creating an identity that you want to protect. To protect a device's identity at any time and in any location, you need to bring the identity of that device into Microsoft Entra ID.

Based on the type of domain you're using, there are two primary ways to do that. Configure Microsoft Entra hybrid join for one of the following domain types:

- [Federated domains](/azure/active-directory/devices/hybrid-azuread-join-federated-domains)
- [Managed domains](/azure/active-directory/devices/hybrid-azuread-join-managed-domains)

The two preceding methods provide the best experience. For more detailed information including the fully manual process, see the following articles:

- [How to plan your Microsoft Entra hybrid join implementation](/azure/active-directory/devices/hybrid-azuread-join-plan)
- [ADFS pass-through authentication for hybrid Microsoft Entra ID](/windows-server/identity/ad-fs/ad-fs-overview), which includes Microsoft Entra discovery

For troubleshooting guidance, see the [Microsoft Entra hybrid join troubleshooting guide](/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current).

## Case study

A large European software company with over 100,000 users in its network took a granular and phased approach towards enabling Microsoft Entra hybrid join.

During the planning phase, since Microsoft Entra hybrid join is a key element supporting co-management, the Configuration Manager administrators worked with the identity team. This software company had many ADFS rules, and some of them were complex. To address this challenge, the identity team reviewed the existing ADFS rules before they enabled Microsoft Entra hybrid join. The IT team also chose to upgrade Microsoft Entra Connect to the latest version. Microsoft Entra Connect now provides an automated process flow for enabling Microsoft Entra hybrid join.

After successful deployment and testing in their pre-production environment, this customer enabled Microsoft Entra hybrid join for the whole production estate. Within a week, they had every Windows 10 device co-managed.

## Contact FastTrack

If you need assistance setting up Microsoft Entra ID at any point in the process, go to [Microsoft FastTrack](https://microsoft.com/fasttrack/), sign in, and request assistance.

For more information, see [Get help from FastTrack](quickstart-fasttrack.md).
