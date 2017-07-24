---
title: "Azure services wizard | Microsoft Docs"
description: "About the Azure services wizard for System Center Configuration Manager."
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid:  a26a653e-17aa-43eb-ab36-0e36c7d29f49
caps.latest.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe

---
# Configure Azure services for use with Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Beginning with Current Branch version 1706, the **Azure Services Wizard** is used to simplify the process of configuring Azure services you use with Configuration Manager.

This wizard provides a common configuration experience by using an **Azure web app** to provide subscription and configuration details. The web app replaces entering this same information each time you set up a new Configuration Manager component or service with Azure.

The following Azure services are configured using the Configure Azure Services wizard:
-   **Cloud Management**   
    [Enable clients to authenticate by using Azure Active Directory]() (Azure AD). You can also [configure Azure AD User Discovery](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaddisc).
-   **OMS Connector**
    [Connect to Operations Manager Suite](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite)   (OMS) and sync data like collections to OMS Log Analytics.
-   **Upgrade Readiness**
    [Connect to Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics) and view client upgrade-compatibility data.
-   **Windows Store for Business**
    Connect to the on-line store for [Windows Store for Business](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business) and get apps for your organization that you can deploy with Configuration Manager.

When you use the wizard to configure a service, several common actions are available.
These include:
-   Configure the Azure environment:  On the **App** page of the wizard, you select the **Azure environment** that you use. See the content for each service to learn if it supports only the public Azure cloud, or if it can support a private cloud.
-   Create or Import a server app:   On the **App** page of the wizard, you can **Create** and **Import** Azure web apps. The available options depend on the service you are configuring.  In addition, some services might require an additional app. For example, a service might also require a **Native Client app**.


For information about Azure web apps, see [Authentication and authorization in Azure App Service](/azure/app-service/app-service-authentication-overview), and [Web Apps overview](/azure/app-service-web/app-service-web-overview)

## Create a web app for use with Configuration Manager
Before you can complete the configuration of an Azure service in the Wizard, you must have a web app that the wizard can use. The web app, also called a web app, defines the common details about your Azure subscription that the set up for each service requires. By reusing the web app the process to configure additional services is simplified.

You create the web app a single time, and then reuse it with each subsequent service you set up. The web app can be created before you configure a specific service, or during the process of configuring your first service. You can use the Azure Services wizard to create the app. You can also create the web app directly in Azure, and then use that app with Configuration Manager.

When you have an app ready for use, during the configuration of a service that supports import of an app, you **Import** that app to the wizard. If you do not have an app ready for use or the wizard does not support Import for the service you are configuring, you can **Create** the app from within the wizard.

### To create the web app from within the wizard.
1.	On the App page of  the Azure wizard, click **Create**.
2.	Next provide a friendly name for the app, the homepage URL, App ID URI, and the Secret key validity period. By default, the secret key validity period is one year.
3.  To continue, someone must now sign-in to Azure to complete the web app creation in Azure. The account that you use to sign-in to Azure does not need to be the same account that runs the Azure Services Wizard. After sign-in to Azure, Configuration Manager creates the web app in Azure for you. This includes the Client ID and secret key for use with the web app.
4.	Later, you can view the web app information, and Client ID and secret key details from the Azure portal.


## View the configuration of an Azure service
You can view the properties of an Azure service you have configured for use.

In the console, go to **Administration** > **Overview** > **Cloud Services** > **Azure Services**. Next, choose the service you want to view or edit, and then click **Properties**.
