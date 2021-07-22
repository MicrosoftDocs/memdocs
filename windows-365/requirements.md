---
# required metadata
title: Windows 365 requirements - Azure | Microsoft Docs
titleSuffix:
description: Windows 365 requirements
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 07/23/2021
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

# Requirements for Windows 365

To use Cloud PCs, you must meet the following requirements:

## Azure requirements

- An active Azure subscription.
- Sufficient permissions to grant Windows 365 each of the following:
  - A reader role on the subscription.
  - Network contributor permissions on the resource group.
  - A network contributor role on the vNet.

## Azure Active Directory and Intune requirements

- A valid and working Intune and Azure Active Directory tenant.
- No enrollment restrictions in place for Windows.
- Infrastructure configuration: You must configure your infrastructure to automatically hybrid Azure AD join any devices that domain join to the on-premises Active Directory. This [configuration lets them be recognized and managed in the cloud](/azure/active-directory/devices/overview).

## Domain requirements

- If an organizational unit is specified, ensure it exists and is valid.
- An Active Directory user account with sufficient permissions to join the computer into the specified organizational unit within the Active Directory domain. If you do not specify an organizational unit, the user account must have sufficient permissions to join the computer to the Active Directory domain.

## Licensing requirements

- You must have an Intune license so that you can use Intune to manage the devices.
- Users must have licenses for Windows, Intune, Azure AD, and Windows 365 to use their Cloud PC.

## Management requirements

You must use [Microsoft Endpoint Manager admin center](https://admin.microsoft.com/) to manage your Cloud PCs.

## Role and identity requirements

- Admin role: You must be an [Intune Administrator in Azure AD](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#intune-administrator) to provision Cloud PCs.
- User identity: Cloud PC users must be configured with [hybrid identities](/azure/active-directory/hybrid/whatis-hybrid-identity) so that they can authenticate with resources both on-premises and in the cloud.

## Supported Azure regions for Cloud PC provisioning

You can create a virtual network and provision Cloud PCs in the following Azure regions:

- US East
- US East 2
- US West 2
- US South central
- Asia Southeast
- Australia East
- Europe North
- Europe West
- UK South
- Canada Central
- India Central
- Japan East
- France Central

<!-- ########################## -->
## Next steps

[Review network requirements](requirements-network.md)