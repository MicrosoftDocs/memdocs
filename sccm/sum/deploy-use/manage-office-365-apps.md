---

title: Manage Office 365 apps |  Configuration Manager
description: "Use the Office 365 Client Management dashboard in Configuration Manager to review Office 365 client information and deploy Office 365 apps."
keywords:
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 11/08/2016
ms.topic: article
ms.prod: configuration-manager
ms.service:
ms.technology:
 - configmgr-sum
ms.assetid: 6c28f80e-b5c1-4bf6-9a5b-b882c388681a

---

# Manage Office 365 apps
Beginning in Configuration Manager version 1610, the Office 365 Client Management dashboard provides information about Office 365 clients and deployments, let's you deploy Office 365 apps to clients, and create automatic deployment rules for Office 365 apps.

## Office 365 Client Management dashboard  
Starting in Configuration Manager version 1610, the Office 365 Client Management dashboard is available in the Configuration Manager console. To view the dashboard, go to **Software Library** > **Overview** > **Office 365 Client Management**.

<!--- >[!NOTE]
>In the **What's New** workspace in the Configuration Manager console, the new dashboard is incorrectly named **Office 365 Servicing dashboard**. --->

The dashboard displays charts for the following:

- Number of Office 365 clients
- Office 365 client versions
- Office 365 client languages
- Office 365 client channels     
For more information, see [Overview of update channels for Office 365 ProPlus](https://technet.microsoft.com/library/mt455210.aspx).
- Automatic deployment rules with Office 365 apps (have Office 365 Client selected in the set of available products).

You can take the following actions on the dashboard:
- At the top of the dashboard, use the **Collection** drop-down setting to filter the dashboard data by members of a specific collection.
- On the upper-right side of the dashboard, click **Office 365 Installer** to start the Office 365 Client Installation Wizard to deploy Office 365 apps to clients. For details, see [Deploy Office 365 apps to clients](#deploy-office-365-apps-to-clients).
- On the middle-right side of the dashboard, click **Create an ADR** to open the Automatic Deployment Rule Wizard to create a new automatic deployment rule (ADR). To create an ADR for Office 365 apps, select **Office 365 Client** when you choose the product. For more information, see [Automatically deploy software updates](/sccm/sum/deploy-use/automatically-deploy-software-updates).
- On the lower-right side of the dashboard, click **Create Client Agent Settings** to open Client Agent settings. For more information, see [About client settings](/sccm/core/clients/deploy/about-client-settings).

## Deploy Office 365 apps to clients
Starting in Configuration Manager version 1610, from the Office 365 Client Management dashboard, you can start the Office 365 Installer that lets you configure Office 365 installation settings, download files from Office Content Delivery Networks (CDNs), and deploy the files as an application in Configuration Manager.

<!--- ### Limitations of Office 365 deployment
- You might have issues when you try to import existing client settings (XML) in the Office 365 App Install wizard. You can manually configure the client settings without an issue. --->

#### To deploy Office 365 apps to clients
1. In the Configuration Manager console, navigate to **Software Library** > **Overview** > **Office 365 Client Management**.
2. Click **Office 365 Installer** in the upper-right pane. The Office 365 Client Installation Wizard opens.
3. On the **Application Settings** page, provide a name and description for the app, enter the download location for the files, and then click **Next**. Note that the location must be specified in the form &#92;&#92;*server*&#92;*share*.
4. On the **Import Client Settings** page, choose whether to import the Office 365 client settings from an existing XML configuration file or to manually specify the settings, and then click **Next**.
When you have an existing configuration file, enter the location for the file and skip to step 7. Note that the location must be specified in the form &#92;&#92;*server*&#92;*share*&#92;*filename*.XML.
5. On the **Client Products** page, select the Office 365 suite that you use, select the applications that you want to include, select any additional Office products that should be included, and then click **Next**.
6. On the **Client Settings** page, choose the settings to include, and then click **Next**.
7. On the **Deployment** page, choose whether to deploy the application, and then click **Next**.
If you choose not to deploy the package in the wizard, skip to step 9.
8. Configure the remainder of the wizard pages as you would for a typical application deployment. For more information, see [Create and deploy an application](/sccm/apps/get-started/create-and-deploy-an-application).
9. Complete the wizard.
10. You can deploy or edit the application just as you would with any other application in Configuration Manager from **Software Library** > **Overview** > **Application Management** > **Applications**.

>[!NOTE]
>After you deploy Office 365 apps, you can create automatic deployment rules to maintain the apps. To create an ADR for Office 365 apps, click **Create an ADR**, and select **Office 365 Client** when you choose the product. For more information, see [Automatically deploy software updates](/sccm/sum/deploy-use/automatically-deploy-software-updates).
