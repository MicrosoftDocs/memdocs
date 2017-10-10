---
title: "Azure services wizard"
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
    [Enable clients to authenticate by using Azure Active Directory](/sccm/core/clients/deploy/deploy-clients-cmg-azure) (Azure AD). You can also [configure Azure AD User Discovery](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc).
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


## <a name="webapp"></a> Create the Azure web app for use with Configuration Manager

The Azure services web app connects your Configuration Manager site to Azure AD and is a prerequisite for using Azure services with your infrastructure. To do this:

1.	In the **Administration** workspace of the Configuration Manager console, expand **Cloud Services**, and then click **Azure Services**.
2.	On the **Home** tab, in the **Azure Services** group, click **Configure Azure Services**.
3.	On the **Azure Services** page of the Azure Services Wizard, select **Cloud Management** to allow clients to authenticate with the hierarchy using Azure AD.
4.	On the **General** page of the wizard, specify a name, and a description for your Azure service.
5.	On the **App** page of the wizard, select your Azure environment from the list, then click **Browse** to select the *Web app* and *Native Client app*  that will be used to configure the Azure service.     
    **Web app:**   Browse opens the Server App window.    
	  In the **Server App** window, select the server app you want to use, and then click **OK**. Server apps are the Azure web apps that contain the configurations for your Azure account, including your Tenant ID, Client ID, and a secret key for clients.
    If you do not have an available app, use one of the following:
		- **Create**: To create a new server app, click **Create**. Next provide a friendly name for the app, the homepage URL, App ID URI, and the Secret key validity period. By default, the secret key validity period is one year.

         To continue, someone must now sign-in to Azure to complete the web app creation in Azure. The account that you use to sign-in to Azure does not need to be the same account that runs the Azure Services Wizard. After sign-in to Azure, Configuration Manager creates the web app in Azure for you, including the Client ID and secret key for use with the web app. Later, you can view these from the Azure portal.

         When you use Create to configure a web app, Configuration Manager can create the web app for you in Azure AD.
		- **Import**: To use a web app that already exists in your Azure subscription, click **Import**. Provide a friendly name for the app and the tenant, and then specify the Tenant ID, Client ID, and the secret key for the Azure web app that you want Configuration Manager to use. After you Verify the information, click **OK** to continue.

          This option is not available for all services you might configure.

   **Native Client app:**  Browse opens the Client App window.  
     In the **Client App** window, select the client app you want to use, and then click **OK**.

     If you do not have an available client app, use one of the following:
     - **Create**: To create a new Client app, click **Create**. Next provide a friendly name for the app and the Reply URL.

          To continue, someone must now sign-in to Azure to complete the client app creation in Azure. The account that you use to sign-in to Azure does not need to be the same account that runs the Azure Services Wizard. After sign-in to Azure, Configuration Manager creates the native client app in Azure for you, including the Client ID for use with the web app. Later, you can view these from the Azure portal.
          When you use Create to configure the app, Configuration Manager can creates the native client app for you in Azure AD.
     - **Import**: To use a client app that already exists in your Azure subscription, click **Import**. Provide a friendly name for the app and the Client ID. Then, click **OK** to continue.
           This option is not available for all services you might configure.

  <!--  MOVE THIS AND STEP 6 TO configure Azure AD User Discover  content
       [!TIP]  
     When you use Import, the account you use to run the wizard must have the *Read directory data* application permission in the Azure portal. This is required to set the correct permissions for the App. When you use Create, Configuration Manager creates the app with the correct permissions. However, you still must give consent to the application in the Azure portal.   -->


6.	On the **Discovery** page of the wizard, click **Enable Azure Active Directory User Discovery**, and then click **Settings**.
In the **Azure AD User Discovery Settings** dialog box, configure a schedule for when discovery occurs. You can also enable delta discovery which checks for only new, or changed accounts in Azure AD. Learn more about [Azure AD User Discovery](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc).

 7.	Complete the wizard.

At this point, you have connected your Configuration Manager site to Azure AD.

## View the configuration of an Azure service
You can view the properties of an Azure service you have configured for use.

In the console, go to **Administration** > **Overview** > **Cloud Services** > **Azure Services**. Next, choose the service you want to view or edit, and then click **Properties**.
