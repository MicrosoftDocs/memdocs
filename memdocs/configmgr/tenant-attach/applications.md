---
title: Tenant attach - Applications (preview) in the admin center
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
   - User targeted applications or applications without the approval option set don't appear in the application list when you're using Configuration Manager version 2002.

Additionally, you'll need the following for installing [user targeted applications](#bkmk_user):<!--7518897-->

- Configuration Manager version 2006 and the corresponding version of the console installed.


## Permissions

The user account needs the following permissions:

- The **Read** permission for the device's **Collection** in Configuration Manager.
- The **Read** permission for **Application** in Configuration Manager.
- The **Approve** permission for **Application** in Configuration Manager.
- The **Admin User** role for the Configuration Manager Microservice application in Azure AD. 
  - Add the role in Azure AD from **Enterprise applications** > **Configuration Manager Microservice** > **Users and groups** > **Add user**. Groups are supported if you have Azure AD premium.
   > [!TIP]
   > The [Application Administrator role in Azure AD](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-assign-admin-roles) has sufficient permissions to add a user to the application's **Admin User** role.

## <a name="bkmk_deploy"></a> Deploy an application to a device

1. In a browser, navigate to [https://endpoint.microsoft.com](https://endpoint.microsoft.com).
1. Select **Devices** then **All Devices**.
1. Select a device that is synced from Configuration Manager via [tenant attach](device-sync-actions.md).
1. Select **Applications**.
1. Select the application and click **Install**.

   :::image type="content" source="media/6024389-tenant-attach-application-install.png" alt-text="Application installation from Microsoft Endpoint Manager admin center" lightbox="media/6024389-tenant-attach-application-install.png":::

You can export all of the data currently in the view into a .csv file. At the top of the page, select the **Export** option to create the file. If the view exceeds 500 rows, only the first 500 are exported.

## Application status

You can filter the application list based on the status.The application status can be one of the following:

- **Available**: The application has never has been installed on the device.
- **Installed**: The application is installed on the device.
- **Installing**: The application is in the process of installing.
- **Install requested**: The installation has been requested, but the client hasn't acknowledged the request yet.
   - If the device is offline, the install request will be acknowledged once it comes back online and receives the policy.  
- **Failed**: The application installation failed.
- **Requirements not met**: The application requirements have not been met.
- **Not installed**: The application isn't currently installed. Typically this status is seen if a different deployment or a user removed the application.
- **Restart pending**: The application is installed but needs a restart to complete (starting in version 2006).

## <a name="bkmk_user"></a> Deploy an application to a user
<!--7518897-->
Starting in Configuration Manager version 2006, user available applications appear in the **Applications** node for a ConfigMgr device. The list of applications available for the device also includes applications deployed to the device's currently logged on user.

Deploying applications to a user has the following limitations:
- Multi-user session scenarios aren't supported.
- Azure AD joined devices aren't currently supported.
   - Devices which are both domain joined and Azure AD joined are supported.

## Next steps

[Troubleshoot applications](troubleshoot-applications.md)