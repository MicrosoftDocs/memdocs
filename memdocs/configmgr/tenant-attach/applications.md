---
title: Tenant attach - Applications (preview) in the admin center
titleSuffix: Configuration Manager
description: "Install applications for uploaded Configuration Manager devices from the admin center."
ms.date: 08/10/2020
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 963dda08-87b8-4e80-90a7-25625efe8861
manager: dougeby
author: mestew
ms.author: mstewart
---

# <a name="bkmk_apps"></a> Tenant attach: Install an application from the admin center (preview)
<!--cm 6024389, in 7220536 pubpreview Aug 10, 2020-->
*Applies to: Configuration Manager (current branch)*

> [!Important]
> - This information relates to a preview feature which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

Microsoft Endpoint Manager is an integrated solution for managing all of your devices. Microsoft brings together Configuration Manager and Intune into a single console called **Microsoft Endpoint Manager admin center**. From the Microsoft Endpoint Management admin center, you can initiate an application install in real time for a tenant attached device.

   :::image type="content" source="media/6024389-tenant-attach-application-list.png" alt-text="Applications in Microsoft Endpoint Manager admin center" lightbox="media/6024389-tenant-attach-application-list.png":::

## Prerequisites

- All of the prerequisites for [Tenant attach: ConfigMgr client details](client-details.md#prerequisites).
- [Update Rollup for Microsoft Endpoint Configuration Manager version 2002](https://support.microsoft.com/help/4560496/) and the corresponding version of the console installed
- Enable the optional feature **Approve application requests for users per device**. For more information, see [Enable optional features from updates](../core/servers/manage/install-in-console-updates.md#bkmk_options).
- At least one application deployed to a device collection with the **An administrator must approve a request for this application on the device** option set on the deployment. For more information, see [Approve applications](../apps/deploy-use/app-approval.md#bkmk_opt).

Additionally, you'll need the following for installing [user targeted applications](#bkmk_user):

- Configuration Manager version 2006 and the corresponding version of the console installed
- At least one application deployed to the user currently logged on to the device with the **An administrator must approve a request for this application on the device** option set on the deployment. For more information, see [Approve applications](../apps/deploy-use/app-approval.md#bkmk_opt).
   - User targeted applications or applications without the approval option set don't appear in the application list.

## Permissions

The user account needs the following permissions:

- The **Read** permission for the device's **Collection** in Configuration Manager.
- The **Read** permission for **Application** in Configuration Manager.
- The **Approve** permission for **Application** in Configuration Manager.
- The **Admin User** role for the Configuration Manager Microservice application in Azure AD.
  - Add the role in Azure AD from **Enterprise applications** > **Configuration Manager Microservice** > **Users and groups** > **Add user**. Groups are supported if you have Azure AD premium.
    - The [Application Administrator role in Azure AD](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles) has sufficient permissions to add a user to the application's **Admin User** role.

## Deploy an application to a device


1. In a browser, navigate to [https://endpoint.microsoft.com](https://endpoint.microsoft.com).
1. Select **Devices** then **All Devices**.
1. Select a device that is synced from Configuration Manager via [tenant attach](device-sync-actions.md).
1. Select **Applications**.
1. Select the application and click **Install**.

   :::image type="content" source="media/6024389-tenant-attach-application-install.png" alt-text="Application installation from Microsoft Endpoint Manager admin center" lightbox="media/6024389-tenant-attach-application-install.png":::

## Application status
The following status 

## <a name="bkmk_user"></a> Deploy an application to a user
<!--7518897-->
Starting in Configuration Manager version 2006, user available applications appear in the **Applications** node for a ConfigMgr device. The application list in the admin center includes applications deployed to the user currently logged on to the device.

   - Multi-user session scenarios aren't supported.
   - Azure AD joined devices aren't currently supported, only AD joined devices.





## Next steps

[Troubleshoot applications](troubleshoot-applications.md)