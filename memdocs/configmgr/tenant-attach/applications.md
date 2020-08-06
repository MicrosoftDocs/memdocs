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
You can now initiate an application install in real time for a tenant attached device from the Microsoft Endpoint Management admin center.

> [!Important]
> - This information relates to a preview feature which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.


## Prerequisites

- All of the prerequisites for [Tenant attach: ConfigMgr client details](client-details.md#prerequisites).
- [Update Rollup for Microsoft Endpoint Configuration Manager version 2002](https://support.microsoft.com/help/4560496/) and the corresponding version of the console installed
- Enable the optional feature **Approve application requests for users per device**. For more information, see [Enable optional features from updates](../core/servers/manage/install-in-console-updates.md#bkmk_options).
- At least one application deployed to a device collection with the **An administrator must approve a request for this application on the device** option set on the deployment. For more information, see [Approve applications](../apps/deploy-use/app-approval.md#bkmk_opt).


Additionally, you'll need the following for user targeted applications:

- Configuration Manager version 2006 and the corresponding version of the console installed
- At least one application deployed to a device collection with the **An administrator must approve a request for this application on the device** option set on the deployment. For more information, see [Approve applications](../apps/deploy-use/app-approval.md#bkmk_opt).
   - User targeted applications or applications without the approval option set don't appear in the application list.

## Permissions

The user account needs the following permissions:

- The **Read** permission for the device's **Collection** in Configuration Manager.
- The **Read** permission for **Application** in Configuration Manager.
- The **Approve** permission for **Application** in Configuration Manager.
- The **Admin User** role for the Configuration Manager Microservice application in Azure AD.
  - Add the role in Azure AD from **Enterprise applications** > **Configuration Manager Microservice** > **Users and groups** > **Add user**. Groups are supported if you have Azure AD premium.
   
## Deploy an application from the admin center

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace and select the **Devices** node.
1. Right-click on a device that's been uploaded to Microsoft Endpoint Manager.
1. In the right-click menu, select **Start** > **Admin Center Preview** to open the preview in your browser.
1. Go to **Applications** in the admin center preview.
1. Select the application and click **Install**.


## Next steps

[Troubleshoot applications](troubleshoot-applications.md)