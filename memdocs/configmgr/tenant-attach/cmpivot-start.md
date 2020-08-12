---
title:  Launch tenant attached CMPivot
titleSuffix: Configuration Manager
description: CMPivot overview for Microsoft Endpoint Manager tenant attached devices.
ms.date: 07/31/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: ae6c0c83-2299-4463-958d-5555e3fcbdbe
author: mestew
ms.author: mstewart 
manager: dougeby
---

# <a name="bkmk_cmpivot"></a> Launch CMPivot from the admin center

*Applies to: Configuration Manager (current branch)* 

<!--6024392-->
Starting in Configuration Manager 2006, you can run CMPivot from Microsoft Endpoint Manager admin center. Bring the power of CMPivot to the Microsoft Endpoint Manager admin center. Allow additional personas, like Helpdesk, to be able to initiate real-time queries from the cloud against an individual ConfigMgr managed device and return the results back to the admin center. This gives all the traditional benefits of CMPivot, which allows IT Admins and other designated personas the ability to quickly assess the state of devices in their environment and take action.

## Prerequisites

The following items are required to use CMPivot from the admin center:

- All of the prerequisites for [Tenant attach: ConfigMgr client details](client-details.md)
- Upgrade the target devices to the latest version of the Configuration Manager client.  
- Target clients require a minimum of PowerShell version 4.
- To gather data for the following entities, target clients require PowerShell version 5.0:  
  - Administrators
  - Connection
  - IPConfig
  - SMBConfig

## Permissions

The user account needs the following permissions:

- The **Read** permission for the device's **Collection** in Configuration Manager.
- The **Admin User** role for the Configuration Manager Microservice application in Azure AD.
  - Add the role in Azure AD from **Enterprise applications** > **Configuration Manager Microservice** > **Users and groups** > **Add user**. Groups are supported if you have Azure AD premium.

- Configuration Manager permissions for CMPivot:
  - **Read** permission on the **SMS Scripts** object
  - **Run Scripts** permission on the **Collection**.
    - Alternatively, you can use **Run CMPivot** on **Collection**.
    - **Run Scripts** is a super set of the **Run CMPivot** permission.
  - **Read** permission on **Inventory Reports**
  - The default scope.

## Launch CMPivot

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace and select the **Devices** node.
1. Right-click on a device that's been uploaded to Microsoft Endpoint Manager.
1. In the right-click menu, select **Start** > **Admin Center Preview** to open the preview in your browser.
1. Select **CMPivot**, type your query in the script pane, then select **Run**.

## Next steps

- For query examples, see [CMPivot sample scripts](cmpivot-samples-attached.md).
-  For information about CMPivot entities, operators, and functions, see [CMPivot usage overview](cmpivot-overview-attached.md).
