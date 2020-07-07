---
title: Tenant attach - ConfigMgr client details in the admin center
titleSuffix: Configuration Manager
description: "View client details for Configuration Manager devices from the admin center."
ms.date: 04/10/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 7a597d9e-a878-48d0-a7ce-56a1dbfd0e5c
manager: dougeby
author: mestew
ms.author: mstewart
---


# <a name="bkmk_mem"></a> Tenant attach: ConfigMgr client details in the admin center (preview)
<!--6374854, 6521921-->

You can now see ConfigMgr client details including collections, boundary group membership, and real-time client information for a specific device in the Microsoft Endpoint Manager admin center.

> [!Important]
> This information relates to a preview feature which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.
> - The boundary groups tab functions only for stand alone sites. The tab will be empty in the admin center for anything other than a standalone primary site.

## Prerequisites

- An environment that's [tenant attached with uploaded devices](device-sync-actions.md).
- One of the following browsers:
  - Microsoft Edge, version 77 and later
  - Google Chrome
- The user account has been discovered with both [Azure Active Directory (Azure AD) user discovery](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc) and [Active Directory user discovery](/../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).
  - Meaning the user account needs to be a synced user object in Azure.

## Permissions

The user account needs the following permissions:

- The **Read** permission for the device's **Collection** in Configuration Manager.
- The **Admin User** role for the Configuration Manager Microservice application in Azure AD.
  - Add the role in Azure AD from **Enterprise applications** > **Configuration Manager Microservice** > **Users and groups** > **Add user**. Groups are supported if you have Azure AD premium.

## View ConfigMgr client details

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace and select the **Devices** node.
1. Right-click on a device that's been uploaded to Microsoft Endpoint Manager.
1. In the right-click menu, select **Start** > **Admin Center Preview** to open the preview in your browser.
     - This launch is a preview experience.

   [![Launch the Admin Center Preview](media/6374854-start-admin-center.png)](media/6374854-start-admin-center.png#lightbox)

> [!NOTE]
> Note the following behaviors for some of the client details:
>
> - The primary site updates the following fields once an hour: **Last policy request**, **Last active time**, and **Last management point**.
>
> - To populate the **Logged on user** field, at least one user needs to sign in to the device after you install the Configuration Manager client.

## Next steps

[Troubleshoot client details](troubleshoot-client-details.md)

