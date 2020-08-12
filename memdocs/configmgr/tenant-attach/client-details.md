---
title: Tenant attach - ConfigMgr client details (preview) in the admin center
titleSuffix: Configuration Manager
description: "View client details for Configuration Manager devices from the admin center."
ms.date: 07/08/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 7a597d9e-a878-48d0-a7ce-56a1dbfd0e5c
manager: dougeby
author: mestew
ms.author: mstewart
---


# <a name="bkmk_mem"></a> Tenant attach: ConfigMgr client details in the admin center (preview)
<!--6024387, 6374854, 6521921, intune 7552762 pubpreview July 7, 2020-->
*Applies to: Configuration Manager (current branch)*

Microsoft Endpoint Manager is an integrated solution for managing all of your devices. Microsoft brings together Configuration Manager and Intune into a single console called **Microsoft Endpoint Manager admin center**. You can see ConfigMgr client details including collections, boundary group membership, and real-time client information for a specific device in the admin center.

> [!Important]
> - This information relates to a preview feature which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.
> - The boundary groups tab functions only for stand alone sites. The tab will be empty in the admin center for anything other than a standalone primary site.

## Prerequisites

- An environment that's [tenant attached with uploaded devices](device-sync-actions.md).
- One of the following browsers:
  - Microsoft Edge, version 77 and later
  - Google Chrome
- The user account has been discovered with both [Azure Active Directory (Azure AD) user discovery](https://docs.microsoft.com/mem/configmgr/core/servers/deploy/configure/about-discovery-methods#azureaddisc) and [Active Directory user discovery](https://docs.microsoft.com/mem/configmgr/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutUser).
  - Meaning the user account needs to be a synced user object in Azure.

## Permissions

The user account needs the following permissions:

- The **Read** permission for the device's **Collection** in Configuration Manager.
- The **Admin User** role for the Configuration Manager Microservice application in Azure AD.
  - Add the role in Azure AD from **Enterprise applications** > **Configuration Manager Microservice** > **Users and groups** > **Add user**. Groups are supported if you have Azure AD premium.
   > [!TIP]
   > The [Application Administrator role in Azure AD](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles) has sufficient permissions to add a user to the application's **Admin User** role.

## View ConfigMgr client details

1. In a browser, navigate to [https://endpoint.microsoft.com](https://endpoint.microsoft.com).
1. Select **Devices** then **All Devices**.
1. Select a device that is synced from Configuration Manager via [tenant attach](device-sync-actions.md).
1. Select the **Client details (preview)**.
   - The primary site updates the following fields once an hour:
      - **Last policy request**
      - **Last active time**
      - **Last management point**.

   :::image type="content" source="media/6024387-device-details.png" alt-text="Client details in Microsoft Endpoint Manager admin center" lightbox="media/6024387-device-details.png":::

1. Select the **Collections (preview)** to list the client's collections.

   :::image type="content" source="media/6024387-device-collections.png" alt-text="Client collections in Microsoft Endpoint Manager admin center" lightbox="media/6024387-device-collections.png":::

## Next steps

[Troubleshoot client details](troubleshoot-client-details.md)
