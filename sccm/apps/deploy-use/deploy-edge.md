---
title: Deploy and update Microsoft Edge, version 77 and later
titleSuffix: Configuration Manager
description: How to deploy and update Microsoft Edge, version 77 and later with Configuration Manager
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 73b420be-5d6a-483a-be66-c4d274437508
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
---

# Microsoft Edge Management

*Applies to: Configuration Manager (Current Branch)*

The all-new Microsoft Edge is ready for business. Starting in Configuration Manager version 1910, you can now deploy [Microsoft Edge, version 77 and later](https://docs.microsoft.com/deployedge/) to your users.

## <a name="bkmk_Microsoft_Edge"></a> Deploy Microsoft Edge, version 77 and later
<!--4561024-->
Admins can pick the Beta or Dev channel, along with a version of the Microsoft Edge client to deploy. Each release incorporates learnings and improvements from our customers and community.

### Prerequisites for deploying

For clients targeted with a Microsoft Edge, version 77 and later deployment:

- PowerShell [Execution Policy](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_execution_policies) can't be set to Restricted.
  - PowerShell is executed to perform the installation.
  
The device running the Configuration Manager console needs access to the following endpoints:

|Location|Use|
|---|---|
|`https://edgeupdates.azurewebsites.net/api/products?view=enterprise`|Information about releases of Microsoft Edge version 77 and later|
|`http://dl.delivery.mp.microsoft.com`|Content for Microsoft Edge releases, version 77 and later|




### Create a deployment

Create a Microsoft Edge, version 77 and later application using the built-in application experience, which makes Microsoft Edge easier to manage:

1. In the console, under **Software Library**, there's a new node called **Microsoft Edge Management**.
1. Select **Create Microsoft Edge Application** from either the ribbon, or by right-clicking on the **Microsoft Edge Management** node.

   ![Microsoft Edge Management node right-click action](./media/4561024-create-microsoft-edge-application.png)

1. On the **Application Settings** page of the wizard, specify a name, description, and location for the content for the app.
1. On the **Microsoft Edge Settings** page, you select a channel and version to deploy. The Learn More link takes you to the [Microsoft Edge Insiders page](https://www.microsoftedgeinsider.com/).

   ![Microsoft Edge Settings page in the deployment wizard](./media/4561024-edge-settings-wizard.png)

1. On the **Deployment** page, decide if you want to deploy the application. If you select **Yes**, you can specify your deployment settings for the application. For more information about deployment settings, see [Deploy applications](/configmgr/apps/deploy-use/deploy-applications#bkmk_deploy-general).
1. In **Software Center** on the client device, the user can see and install the application.

   ![Microsoft Edge Settings page in the deployment wizard](./media/4561024-software-center-install-edge.png)

### Log files for deployment

|Location|Log|Use|
|---|---|---|
| Site server|SMSProv.log|Shows details if the creation of the app or deployment fails.|
| [Varies](/sccm/core/plan-design/hierarchy/log-files)|PatchDownloader.log| Shows details if the content download fails|
| Client|  AppEnforce.log|Shows installation information|

## Update Microsoft Edge, version 77 and later
<!--4831871-->

Starting in Configuration Manager version 1910, you may notice that there is a node called **All Microsoft Edge updates** under **Microsoft Edge Management**. While you won't see updates in this node quite yet, we wanted you to know that Configuration Manager is ready for them.

   ![All Microsoft Edge updates node](./media/4831871-all-microsoft-edge-updates.png)

## Next steps

[Monitor applications](/configmgr/apps/deploy-use/monitor-applications-from-the-console)