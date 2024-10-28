---
# required metadata
title: Windows 365 requirements
titleSuffix:
description: Windows 365 requirements
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 04/02/2024
ms.topic: how-to
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: chbrinkh
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Requirements for Windows 365

To use Cloud PCs, you must meet the following requirements:

## Azure requirements

### [Windows 365 Enterprise and Frontline](#tab/enterprise)

None, if you plan on provisioning Microsoft Entra joined Cloud PCs on a Microsoft hosted network.

If you choose to provision Cloud PCs on your own network, an active Azure subscription with the following configurations is required:

- Sufficient permissions to grant Windows 365:
  - A reader role on the Azure subscription.
  - Windows365 network interface contributor role on the specified resource group.
  - Windows365 network user role on the virtual network.

### [Windows 365 Government](#tab/government)

All of the Windows 365 Enterprise requirements apply with the following additions.

A subscription in Azure Government is required for Windows 365 Government customers who would like to use any of the following capabilities:

- Hybrid AADJ
- AADJ and with the customer providing their own network
- Custom Images

---

<a name='azure-active-directory-and-intune-requirements'></a>

## Microsoft Entra ID and Intune requirements

- A valid and working Intune and Microsoft Entra tenant.
- Intune default device type enrollment restrictions must be set to Allow Windows (MDM) platform for corporate enrollment. For more information, see [Device Enrollment Restrictions Limitations](mem/intune/enrollment/enrollment-restrictions-set,md#limitations).
- Infrastructure configuration: If you plan on provisioning Microsoft Entra hybrid joined Cloud PCs, you must configure your infrastructure to automatically Microsoft Entra hybrid join any devices that domain join to the on-premises Active Directory. This [configuration lets them be recognized and managed in the cloud](/azure/active-directory/devices/overview).
- Microsoft Entra Domain Services isn't supported because it doesn't support Microsoft Entra hybrid join.

## Domain requirements

None, if you plan on provisioning Microsoft Entra joined Cloud PCs on a Microsoft hosted network.

If you choose to provision Microsoft Entra hybrid joined Cloud PCs, then the following configurations on your domain are required:

- If an organizational unit is specified, ensure it exists and is valid.
- An Active Directory user account with sufficient permissions to join the computer into the specified organizational unit within the Active Directory domain. If you don't specify an organizational unit, the user account must have sufficient permissions to join the computer to the Active Directory domain.
- User accounts that are assigned Cloud PCs must have a synced identity available in both Active Directory and Microsoft Entra ID.

> [!NOTE]
> For the user account used to join the Cloud PCs to the Active Directory Domain Services, make sure to set up appropriate delegation following the instructions in [Increase the computer account limit in the Organizational Unit](/mem/autopilot/windows-autopilot-hybrid#increase-the-computer-account-limit-in-the-organizational-unit).

## Licensing requirements

- You must have an Intune license to use Intune to manage the devices.
- Windows 365 Enterprise: Users must have licenses for Windows E3, Intune, Microsoft Entra ID P1, and Windows 365 to use their Cloud PC.
- Windows 365 Frontline: Users must
  - Have licenses for Windows E3, Intune, Microsoft Entra ID P1.
  - Be added to the Microsoft Entra security group in the provisioning policy to use their Cloud PC.

## Management requirements

- You must use [Microsoft Intune admin center](https://admin.microsoft.com/) to manage your Cloud PCs.
- You must have a Windows 365 Enterprise or Frontline license to manage Cloud PC configurations.

## Role and identity requirements

- Admin role: You must be an [Intune Administrator in Microsoft Entra ID](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#intune-administrator) or [Windows 365 Administrator](/azure/active-directory/roles/permissions-reference) to provision Cloud PCs.
- User identity: Cloud PC users must be configured with [hybrid identities](/azure/active-directory/hybrid/whatis-hybrid-identity) so that they can authenticate with resources both on-premises and in the cloud.

## Supported Azure regions for Cloud PC provisioning

### [Windows 365 Enterprise and Frontline](#tab/ent)

Windows 365 manages the capacity and availability of underlying Azure resources as part of the service. Windows 365 partners closely with Azure to select regions that meet our Windows 365 service requirements for availability and capacity. When selecting a region Microsoft strongly recommends using the **Automatic** option. This automation decreases the chance of provisioning failure, by increasing the possible regions that the CloudPCs will be installed into. On availability, we use features like availability zones in Azure to provide in-region resiliency as built-in value to the service. You can create a virtual network or use the Microsoft hosted network for provisioning Cloud PCs in the following Azure regions:

- Asia
  - East Asia
  - Southeast Asia
- Australia
  - Australia East
- Canada
  - Canada Central
- European Union
  - North Europe
  - West Europe
  - Italy North
  - Poland Central
  - Sweden Central
- France
  - France Central
- Germany
  - Germany West Central
- India
  - Central India
- Japan
  - Japan East
- Norway
  - Norway East
- South Africa
  - South Africa North
- South America
  - Brazil South (Restricted)
- South Korea
  - Korea Central
- Switzerland
  - Switzerland North
- UAE
  - UAE North
- United Kingdom
  - UK South
- US Central
  - Central US
  - South Central US
- US East
  - East US
  - East US 2
- US West
  - West US 2 (Restricted)
  - West US 3

Some features might not be available in some regions.

### [Windows 365 Government](#tab/gov)

- US Government
  - Arizona
  - Virginia

---

<!-- ########################## -->
## Next steps

[Review network requirements](requirements-network.md)
