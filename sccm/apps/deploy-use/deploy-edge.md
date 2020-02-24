---
title: Deploy and update Microsoft Edge, version 77 and later
titleSuffix: Configuration Manager
description: How to deploy and update Microsoft Edge, version 77 and later with Configuration Manager
ms.date: 02/24/2020
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 73b420be-5d6a-483a-be66-c4d274437508
author: mestew
ms.author: mstewart
manager: dougeby


---

# Microsoft Edge Management

*Applies to: Configuration Manager (Current Branch)*

The all-new Microsoft Edge is ready for business. Starting in Configuration Manager version 1910, you can now deploy [Microsoft Edge, version 77 and later](https://docs.microsoft.com/deployedge/) to your users. A PowerShell script is used to install the Edge build selected. The script also turns off automatic updates for Edge so they can be managed with Configuration Manager.

## <a name="bkmk_Microsoft_Edge"></a> Deploy Microsoft Edge
<!--4561024-->
Admins can pick the Beta, Dev, or Stable channel, along with a version of the Microsoft Edge client to deploy. Each release incorporates learnings and improvements from our customers and community.

### Prerequisites for deploying

For clients targeted with a Microsoft Edge deployment:

- PowerShell [Execution Policy](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_execution_policies) can't be set to Restricted.
  - PowerShell is executed to perform the installation.

The device running the Configuration Manager console needs access to the following endpoints:

|Location|Use|
|---|---|
|`https://edgeupdates.microsoft.com/api/products?view=enterprise`|Information about releases of Microsoft Edge|
|`http://dl.delivery.mp.microsoft.com`|Content for Microsoft Edge releases|

### Verify Microsoft Edge update policies

In version 1910, when Microsoft Edge is deployed, the installation script turns off automatic updates for Microsoft Edge so they can be managed with Configuration Manager. You can change this behavior using Group Policy. For more information, see [Plan your deployment of Microsoft Edge](https://docs.microsoft.com/deployedge/deploy-edge-plan-deployment#define-and-configure-policies) and [Microsoft Edge update policies](https://docs.microsoft.com/DeployEdge/microsoft-edge-update-policies).


### Create a deployment

Create a Microsoft Edge application using the built-in application experience, which makes Microsoft Edge easier to manage:

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

## Update Microsoft Edge
<!--4831871-->

Starting in Configuration Manager version 1910, you'll see a node called **All Microsoft Edge updates** under **Microsoft Edge Management**. This node helps you manage updates for all Microsoft Edge channels.<!--initial edge updates released Jan 15,2020-->

1. To get updates for Microsoft Edge, ensure you have the **Updates** classification and the **Microsoft Edge** product [selected for synchronization](/configmgr/sum/get-started/configure-classifications-and-products).

   [![Select Microsoft Edge as product in software update point properties](./media/4831871-microsoft-edge-product-sup.png)](./media/4831871-microsoft-edge-product-sup.png#lightbox)

1. In the **Software Library** workspace, expand **Microsoft Edge Management** and click on the **All Microsoft Edge Updates** node.

1. If needed, click **Synchronize Software Updates** in the ribbon to start a synchronization. For more information, see [Synchronize software updates](/configmgr/sum/get-started/synchronize-software-updates).

   ![All Microsoft Edge updates node](./media/4831871-all-microsoft-edge-updates.png)

1. Manage and deploy Microsoft Edge updates like any other update, such as adding them to your [automatic deployment rule](/configmgr/sum/deploy-use/automatically-deploy-software-updates). Some of the common updates tasks you can do from the **All Microsoft Edge Updates** node include:

   - [Create a phased deployment](/configmgr/osd/deploy-use/create-phased-deployment-for-task-sequence)
   - [Manually deploy software updates](/configmgr/sum/deploy-use/manually-deploy-software-updates)
   - [Download software updates](/configmgr/sum/deploy-use/download-software-updates)

## Next steps

[Monitor applications](/configmgr/apps/deploy-use/monitor-applications-from-the-console)

[Monitor software updates](/configmgr/sum/deploy-use/monitor-software-updates)

[Manage and monitor phased deployments](/configmgr/osd/deploy-use/manage-monitor-phased-deployments)
