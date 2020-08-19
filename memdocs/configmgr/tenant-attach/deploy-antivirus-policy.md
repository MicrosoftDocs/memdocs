---
title: Tenant attach - Deploy endpoint security Antivirus policy from the Microsoft Endpoint Manager admin center  (preview)
titleSuffix: Configuration Manager
description: " Create and deploy Microsoft Defender antivirus policies from the Microsoft Endpoint Manager console and for Configuration Manager collections."
ms.date: 08/24/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 07379821-02b3-4c61-af03-329c782e10d6
manager: dougeby
author: mestew
ms.author: mstewart
---

# <a name="bkmk_atp"></a> Tenant attach: Create and deploy endpoint security Antivirus policy from the admin center (preview)
<!--5691658-->
*Applies to: Configuration Manager (current branch)*

> [!Important]
> - This information relates to a preview feature which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here. 

Microsoft Endpoint Manager is an integrated solution for managing all of your devices. Microsoft brings together Configuration Manager and Intune into a single console called **Microsoft Endpoint Manager admin center**. Create Microsoft Defender antivirus policies in the Microsoft Endpoint Manager console and deploy them to Configuration Manager collections.


## Prerequisites

- Access to the [Microsoft Endpoint Manager admin center](https://endpoint.microsoft.com/).
- An E5 license for [Microsoft Defender ATP](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-atp/minimum-requirements#licensing-requirements).
- An environment that's [tenant attached with uploaded devices](device-sync-actions.md).
- A minimum of Configuration Manager version 2006 and the corresponding version of the console installed.
   - Upgrade the target devices to the latest version of the Configuration Manager client.
- At least one Configuration Manager collection that's [available for assigning Endpoint security policies](atp-onbaord.md#bkmk_collections)

## Supported Antivirus profile for tenant attached devices

[!INCLUDE [Profiles for Configuration Manager tenant attached devices](../../intune/protect/includes/configmgr-antivirus-profiles.md)]

## Assign antivirus policies to a collection

1. In a browser, go to [https://aka.ms/MDAVTenantAttachPreview](https://aka.ms/MDAVTenantAttachPreview).
1. Select **Endpoint security** then **Antivirus**.
1. Select **Create Policy**.
1. For the **Platform**, select **Windows 10 and Windows Server (ConfigMgr)**.
1. For the **Profile**, select **Micrososft Defender Antivirus (Preview)** then **Create**.
1. Assign a **Name** and optionally a **Description** on the **Basics** page.
1. On the **Configuration settings** page, configure the settings you want to manage with this profile. When your done configuring settings, select **Next**. For more information about available policies, see [Antivirus policy settings for tenant attached devices](../../intune/protect/antivirus-microsoft-defender-settings-windows-tenant-attach.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json).
1. Assign the policy to a Configuration Manager collection on the **Assignments** page.

## Next steps

[Antivirus policy settings for tenant attached devices](../../intune/protect/antivirus-microsoft-defender-settings-windows-tenant-attach.md?toc=/mem/configmgr/tenant-attach/toc.json&bc=/mem/configmgr/tenant-attach/breadcrumb/toc.json)