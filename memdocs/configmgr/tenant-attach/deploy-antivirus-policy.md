---
title: Tenant attach - Onboard Configuration Manager clients to Microsoft Defender ATP (preview) from the Microsoft Endpoint Manager admin center
titleSuffix: Configuration Manager
description: "Install applications for uploaded Configuration Manager devices from the admin center."
ms.date: 08/11/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 963dda08-87b8-4e80-90a7-25625efe8861
manager: dougeby
author: mestew
ms.author: mstewart
---

# <a name="bkmk_atp"></a> Tenant attach: Onboard Configuration Manager clients to Microsoft Defender ATP (preview) from the Microsoft Endpoint Manager admin center
<!--5691658-->
*Applies to: Configuration Manager (current branch)*

> [!Important]
> - This information relates to a preview feature which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here. 

Microsoft Endpoint Manager is an integrated solution for managing all of your devices. Microsoft brings together Configuration Manager and Intune into a single console called **Microsoft Endpoint Manager admin center**.


## Prerequisites

- Access to the [Microsoft Endpoint Manager admin center](https://endpoint.microsoft.com/).
- An E5 license for [Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/minimum-requirements#licensing-requirements).
- An environment that's [tenant attached with uploaded devices](device-sync-actions.md).
- A minimum of Configuration Manager version 2006 and the corresponding version of the console installed.
   - Upgrade the target devices to the latest version of the Configuration Manager client.
- At least one Configuration Manager collection that's [available for assigning Endpoint security policies](atp-onbaord.md#bkmk_collections)


