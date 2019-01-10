---
title: Set up hybrid Azure AD
titleSuffix: Configuration Manager
description: If your environment currently has domain-joined Windows 10 devices, set up hybrid Azure AD before you enable co-management
ms.date: 01/14/2019
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: 27dd26d1-e99c-4431-b2f8-60406394b6db
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Set up hybrid Azure AD for co-management

If you have Windows 10 devices joined to on-premises Active Directory, before you enable co-management in Configuration Manager, first join these devices to Azure Active Directory (Azure AD). This process is called hybrid Azure AD join. 

The hybrid Azure AD-join process automatically registers your on-premises domain-joined devices with Azure AD. For more information on this process, see the following articles:
- [Introduction to device management in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/device-management-introduction) 
- [How to plan your Hybrid Azure AD join](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-plan)

Hybrid Azure AD join is one of the key foundations for co-management. This process can be challenging for some customers, for example:
- Your organization uses a third-party identity solution 
- The complexities of setting up Active Directory Federation Services (ADFS)

Resolving these challenges can take some guidance. This article helps to mitigate any delays.


## How to do it

Devices are similar to users when creating an identity that you want to protect. To protect a device's identity at any time and in any location, you need to bring the identity of that device into Azure AD.

Based on the type of domain you're using, there are two primary ways to do that. Configure hybrid Azure AD join for one of the following domain types:  
- [Federated domains](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-federated-domains)  
- [Managed domains](https://docs.microsoft.com/azure/active-directory/devices/hybrid-azuread-join-managed-domains)  

The two preceding methods provide the best experience. For more detailed information including the fully manual process, see the following articles:
- [Manually configure hybrid Azure AD joined devices](https://docs.microsoft.com/azure/active-directory/device-management-hybrid-azuread-joined-devices-setup)  
- [ADFS pass-through authentication for hybrid Azure AD](https://docs.microsoft.com/windows-server/identity/ad-fs/ad-fs-overview), which includes Azure AD discovery  

For troubleshooting guidance, see the [Windows 10 hybrid Azure AD join troubleshooting guide](https://docs.microsoft.com/azure/active-directory/devices/troubleshoot-hybrid-join-windows-current).



## Case study

A large European software company with over 100,000 users in its network took a granular and phased approach towards enabling hybrid Azure AD join.

During the planning phase, since hybrid Azure AD join is a key element supporting co-management, the Configuration Manager administrators worked with the identity team. This software company had many ADFS rules, and some of them were complex. To address this challenge, the identity team reviewed the existing ADFS rules before they enabled hybrid Azure AD join. The IT team also chose to upgrade Azure AD Connect to the latest version. Azure AD Connect now provides an automated process flow for enabling hybrid Azure AD join.

After successful deployment and testing in their pre-production environment, this customer enabled hybrid Azure AD join for the whole production estate. Within a week, they had every Windows 10 device co-managed.



## Contact FastTrack

If you need assistance setting up Azure AD at any point in the process, go to [Microsoft FastTrack](https://Microsoft.com/FastTrack/), sign in, and request assistance. 

For more information, see [Get help from FastTrack](/sccm/comanage/quickstart-fasttrack). 

