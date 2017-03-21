---
title: "Capabilities in Technical Preview 1703 Configuration Manager"
description: "Learn about features available in the Technical Preview for System Center Configuration Manager, version 1703."
ms.custom: na
ms.date: 03/24/2017
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2e801f8c-d331-41ee-8f27-908448fc0951
caps.latest.revision: 5
author: Brenduns
ms.author: brenduns
manager: angrobe
---
# Capabilities in Technical Preview 1703 for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*

This article introduces the features that are available in the Technical Preview for System Center Configuration Manager, version 1703. You can install this version to update and add new capabilities to your Configuration Manager technical preview site. Before installing this version of the technical preview, review the introductory topic, [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md), to become familiar with general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback about the features in a technical preview.    


**The following are new features you can try out with this version.**  

## Deploy volume-purchased iOS apps to device collections


You can now deploy licensed apps to devices as well as users. Depending on the apps ability to support device licensing, an appropriate license will be claimed when you deploy it, as follows:

|||||
|-|-|-|-|
|Configuration Manager version|App supports device licensing?|Deployment collection type|Claimed license|
|Earlier than 1702|Yes|User|User license|
|Earlier than 1702|No|User|User license|
|Earlier than 1702|Yes|Device|User license|
|Earlier than 1702|No|Device|User license|
|1702 and later|Yes|User|User license|
|1702 and later|No|User|User license|
|1702 and later|Yes|Device|Device license|
|1702 and later|No|Device|User license|

For more information about volume-purchased iOS apps, see [Manage volume-purchased iOS apps](/sccm/mdm/deploy-use/manage-volume-purchased-ios-apps).



## Configure Azure Services wizard
Technical preview 1703 introduces the **Configure Azure Services** wizard. This wizard provides a common configuration experience that replaces the individual workflows to set up the cloud services you use with Configuration Manager. This is done by using an **Azure web app** to provide the subscription and configuration details that you otherwise enter each time you set up a new Configuration Manager component or service with Azure.

With technical preview 1703, only Windows Store for Business (WSfB) is configured by using this wizard.  Other cloud services are configured by using their separate workflows.

-	Use the information in this preview topic to replace the configuration steps found in the [Set up Windows Store for Business synchronization](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#set-up-windows-store-for-business-synchronization) section of the Current Branch topic [Manage apps from the Windows Store for Business with System Center Configuration Manager](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business).

-	For more information about web apps, see [Authentication and authorization in Azure App Service](https://docs.microsoft.com/azure/app-service/app-service-authentication-overview), and [Web Apps overview](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview).

### Prerequisites and planning
When you set up a connection between Configuration Manager and the Windows Store for Business, you must provide a folder where app content synchronized from the store will be kept. To ensure that this folder is secure and that its content can be deployed to devices, make sure the following permissions are in place:
-	The computer on which you install the service connection point site system role (the top-level site in the hierarchy) must have read and write permissions to the folder you specified when using the **Computer$** account.  

-	The app author must have read permissions to the folder you specified.  

-	The **Computer$** account of each computer that hosts an instance of the SMS Provider must be able to use the folder you specified.

In Azure Active Directory, register Configuration Manager as a web application or Web API management tool. This creates the client ID that you will need later.

### Use the wizard to configure the WSfB cloud service

1. In the console, go to **Administration** > **Overview** > **Cloud Services Management** > **Azure** > **Azure Services**, and then choose **Configure Azure Services** to start the **Azure Services Wizard**.

2. On the **Azure Services** page, select the service you want to configure, and then click **Next**. With this preview, only WSfB can be configured.

3. On the **General** page, provide a friendly name for the **Azure service name** and an optional description, and then click **Next**.

4. On the **App** page, specify your Azure environment, and then click **Browse** to open the Server App window.

5. In the **Server App** window, select the server app you want to use, and then click **OK**.
Server apps are the Azure web apps that contain the configurations for your Azure account, including your Tenant ID, Client ID, and a secret key for clients. If you do not have an available server app, use one of the following:
  -	**Create**: To create a new server app, click **Create**. Provide a friendly name for the app and the tenant. Then, after you sign-in to Azure, Configuration Manager creates the web app in Azure for you, including the Client ID and secret key for use with the web app. Later, you can view these from the Azure portal.
  -	**Import**: To use a web app that already exists in your Azure subscription, click **Import**. Provide a friendly name for the app and the tenant, and then specify the Tenant ID, Client ID, and the secret key for the Azure web app that you want Configuration Manager to use. After you **Verify** the information, click **OK** to continue.  </br></br>

6. Review the **Information** page and complete any additional steps and configurations as directed. These configurations are necessary to use the service with Configuration Manager.
For example, to configure WSfB:

  1. In Azure you must register Configuration Manager as a web application or Web API and record the client ID. You also specify a client key for use by the management tool (which is Configuration Manager).

  2.	In the WSfB console you must configure Configuration Manager as the store management tool, enable support for offline licensed apps, and then purchase at least one app.   </br>

  Click **Next** when you are ready to continue.

7. On the **App Configurations** page, complete the app catalog and language configurations for this service, and then click **Next**.
8. After the wizard completes, the Configuration Manager console shows that you have configured **Windows Store for Business** as a **Cloud Service Type**.

You can now use the remainder of the [Current Branch content](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business) for managing apps from the WSfB to synchronize, create and deploy, and monitor Windows Store for Business Apps.

### Modify a cloud service configuration
You can view and edit the properties of a cloud service to modify the configuration.

In the console go to **Administration** > **Overview** > **Cloud Services Management** > **Azure** > **Azure Services**, and then choose **Configure Azure Services**, select a Cloud Service and then choose **Properties**.
