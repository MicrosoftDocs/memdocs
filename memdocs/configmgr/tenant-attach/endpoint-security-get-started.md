---
title: Get started - Create and deploy endpoint security policies from the admin center (preview)
titleSuffix: Configuration Manager
description: Create and deploy endpoint security policies from the Microsoft Intune admin center and for Configuration Manager collections.
ms.date: 03/21/2022
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
manager: apoorvseth
author: Banreet
ms.author: banreetkaur
ms.localizationpriority: high
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# <a name="bkmk_atp"></a> Get started: Create and deploy endpoint security policies from the admin center
<!--5691658-->
*Applies to: Configuration Manager (current branch)*

The Microsoft Intune family of products is an integrated solution for managing all of your devices. Microsoft brings together Configuration Manager and Intune into a single console called **Microsoft Intune admin center**.

<!--Adding Include for Prerequisites-->

[!INCLUDE [Profiles for Configuration Manager tenant attached devices](./includes/configmgr-endpoint-security-prerequisties.md)]

## <a name="bkmk_supportedprofiles"></a>Supported endpoint security profiles for tenant attached devices

[!INCLUDE [Profiles for Configuration Manager tenant attached devices](./includes/configmgr-endpoint-security-profiles.md)]

## <a name="bkmk_collections"></a> Make Configuration Manager collections available to assign Endpoint security policies

When you enable collections of devices to work with endpoint security policies from Intune, you're configuring devices in those collections to onboard with Microsoft Defender for Endpoint.

[!INCLUDE [Enable endpoint security policies for a Configuration Manager collection](../../intune/protect/includes/make-configmgr-collection-available-edr.md)]

## Next steps

- [Create and deploy endpoint security Antivirus policy to tenant attached devices](deploy-antivirus-policy.md)
- [Create and deploy endpoint security Firewall policy to tenant attached devices](deploy-firewall-policy.md)
- [Create and deploy endpoint security Endpoint Detection and Response policy to tenant attached devices](atp-onboard.md)