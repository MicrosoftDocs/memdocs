---
title: Configure Azure services
titleSuffix: Configuration Manager
description: Connect your Configuration Manager environment with Azure services for cloud management, Upgrade Readiness, Microsoft Store for Business, and Log Analytics.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: a26a653e-17aa-43eb-ab36-0e36c7d29f49
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Configure Azure services for use with Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Use the **Azure Services Wizard** to simplify the process of configuring the Azure cloud services you use with Configuration Manager. This wizard provides a common configuration experience by using Azure Active Directory (Azure AD) web app registrations. These apps provide subscription and configuration details, and authenticate communications with Azure AD. The app replaces entering this same information each time you set up a new Configuration Manager component or service with Azure.



## Available services

Configure the following Azure services using this wizard:  

-   **Cloud Management**: This service enables the site and clients to authenticate by using Azure AD. This authentication enables other scenarios, such as:  

    - [Install and assign Configuration Manager Windows 10 clients using Azure AD for authentication](/sccm/core/clients/deploy/deploy-clients-cmg-azure)  

    - [Configure Azure AD User Discovery](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  

    - Support certain [cloud management gateway scenarios](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#scenarios)  

-   **Log Analytics Connector**: [Connect to Azure Log Analytics](/sccm/core/clients/manage/sync-data-log-analytics). Sync collection data to Log Analytics.  

    > [!Note]  
    > This article refers to the *Log Analytics Connector*, which was formerly called the *OMS Connector*. There's no functional difference. For more information, see [Azure Management - Monitoring](https://docs.microsoft.com/en-us/azure/monitoring/#operations-management-suite).  

-   **Upgrade Readiness Connector**: Connect to Windows Analytics [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics). View client upgrade compatibility data.  

-   **Microsoft Store for Business**: Connect to the [Microsoft Store for Business](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business). Get store apps for your organization that you can deploy with Configuration Manager.  

### Service details

The following table lists details about each of the services.  

- **Tenants**: The number of service instances you can configure. Each instance must be a distinct Azure tenant.  

- **Clouds**: All services support the global Azure cloud, but not all services support private clouds, such as the Azure US Government cloud.  

- **Web app**: Whether the service uses an Azure AD app of type *Web app / API*, also referred to as a server app in Configuration Manager.  

- **Native app**: Whether the service uses an Azure AD app of type *Native*, also referred to as a client app in Configuration Manager.  

- **Actions**: Whether you can import or create these apps in the Configuration Manager Azure Services Wizard.  


|Service  |Tenants  |Clouds  |Web app  |Native app  |Actions  |
|---------|---------|---------|---------|---------|---------|
|Cloud management with</br>Azure AD User Discovery | Multiple | Public | ![Supported](media/green_check.png) | ![Supported](media/green_check.png) | Import, Create |
|Log Analytics Connector | One | Public, Private | ![Supported](media/green_check.png) | ![Not supported](media/Red_X.png) | Import |
|Upgrade Readiness | One | Public | ![Supported](media/green_check.png) | ![Not supported](media/Red_X.png) | Import |
|Microsoft Store for</br>Business | One | Public | ![Supported](media/green_check.png) | ![Not supported](media/Red_X.png) | Import, Create |


### About Azure AD apps

Different Azure services require distinct configurations, which you make in the Azure portal. Additionally, the apps for each service can require separate permissions to Azure resources.  

You can use a single app for multiple services. There's only one object to manage in Configuration Manager and Azure AD. When the security key on the app expires, you only have to refresh one key.

The most secure configuration is using separate apps for each service. An app for one service might require additional permissions that another service doesn't require. Using one app for different services can provide the app with more permissions than it otherwise requires. 

When you create additional Azure services in the wizard, Configuration Manager is designed to reuse information that is common between services. This behavior helps you from needing to input the same information multiple times. 

For more information about the required app permissions and configurations for each service, see the relevant Configuration Manager article in [Available services](#available-services). 

For more information about Azure apps, start with the following articles:
- [Authentication and authorization in Azure App Service](/azure/app-service/app-service-authentication-overview)
- [Web Apps overview](/azure/app-service-web/app-service-web-overview)
- [Basics of Registering an Application in Azure AD](/azure/active-directory/develop/active-directory-authentication-scenarios#basics-of-registering-an-application-in-azure-ad)  
- [Register your application with your Azure Active Directory tenant](/azure/active-directory/active-directory-app-registration)



## Before you begin

After you decide the service to which you want to connect, refer to the table in [Service details](#service-details). This table provides information you need to complete the Azure Service Wizard. Have a discussion in advance with your Azure AD administrator. Decide if you manually create the apps in advance in the Azure portal, and then import the app details into Configuration Manager. Or use Configuration Manager to directly create the apps in Azure AD. To collect the necessary data from Azure AD, review the information in the other sections of this article.

Some services require the Azure AD apps to have specific permissions. Review the information for each service to determine any required permissions. For example, before you can import a web app, an Azure administrator must first create it in the [Azure portal](https://portal.azure.com). When configuring Upgrade Readiness or the Log Analytics Connector, you need to give your newly registered web app *contributor* permission on the resource group that contains the relevant workspace. This permission allows Configuration Manager to access that workspace. When assigning the permission, search for the name of the app registration in the **Add users** area of the Azure portal. This process is the same as when [providing Configuration Manager with permissions to Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#grant-configuration-manager-with-permissions-to-log-analytics). An Azure administrator must assign these permissions before you import the app into Configuration Manager.



## Start the Azure Services wizard

1.	In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Azure Services** node.  

2.	On the **Home** tab of the ribbon, in the **Azure Services** group, click **Configure Azure Services**.  

3.	On the **Azure Services** page of the Azure Services Wizard:  

    1. Specify a **Name** for the object in Configuration Manager.  

    2. Specify an optional **Description** to help you identify the service.  

    3. Select the Azure service that you want to connect with Configuration Manager.  

4. Click **Next** to continue to the [Azure app properties](#azure-app-properties) page of the Azure Services Wizard.  



## Azure app properties

On the **App** page of the Azure Services Wizard, first select the **Azure environment** from the list. Refer to the table in [Service details](#service-details) for which environment is currently available to the service.

The rest of the App page varies depending upon the specific service. Refer to the table in [Service details](#service-details) for which type of app the service uses, and which action you can use. 
- If the app supports both import and creates actions, click **Browse**. This action opens the [Server app dialog](#server-app-dialog) or the [Client App dialog](#client-app-dialog).
- If the app only supports the import action, click **Import**. This action opens the [Import Apps dialog (server)](#import-apps-dialog-server) or the [Import Apps dialog (client)](#import-apps-dialog-client).

After you specify the apps on this page, click **Next** to continue to the [Configuration or Discovery](#configuration-or-discovery) page of the Azure Services Wizard.

### Web app

This app is the Azure AD type *Web app / API*, also referred to as a server app in Configuration Manager.

#### Server app dialog

When you click **Browse** for the **Web app** on the App page of the Azure Services Wizard, it opens the Server app dialog. It displays a list that shows the following properties of any existing web apps:
- Tenant friendly name
- App friendly name
- Service Type

There are three actions you can take from the Server app dialog:
- To reuse an existing web app, select it from the list. 
- Click **Import** to open the [Import apps dialog](#import-apps-dialog-server).
- Click **Create** to open the [Create Server Application dialog](#create-server-application-dialog).

After you select, import or create a web app, click **OK** to close the Server app dialog. This action returns to the [App page](#azure-app-properties) of the Azure Services Wizard.

#### Import apps dialog (server)

When you click **Import** from the Server app dialog or the App page of the Azure Services Wizard, it opens the Import apps dialog. This page lets you enter information about an Azure AD web app that is already created in the Azure portal. It imports metadata about that web app into Configuration Manager. Specify the following information:
- **Azure AD Tenant Name**
- **Azure AD Tenant ID**
- **Application Name**: A friendly name for the app.
- **Client ID**
- **Secret Key**
- **Secret Key Expiry**: Select a future date from the calendar. 
- **App ID URI**: This value needs to be unique in your Azure AD tenant. It is in the access token used by the Configuration Manager client to request access to the service. By default this value is https://ConfigMgrService.  

After entering the information, click **Verify**. Then click **OK** to close the Import apps dialog. This action returns to either the [App page](#azure-app-properties) of the Azure Services Wizard, or the [Server app dialog](#server-app-dialog).

#### Create Server Application dialog

When you click **Create** from the Server app dialog, it opens the Create Server Application dialog. This page automates the creation of a web app in Azure AD. Specify the following information:
- **Application Name**: A friendly name for the app.
- **HomePage URL**: This value isn't used by Configuration Manager, but required by Azure AD. By default this value is https://ConfigMgrService.  
- **App ID URI**: This value needs to be unique in your Azure AD tenant. It is in the access token used by the Configuration Manager client to request access to the service. By default this value is https://ConfigMgrService.  
- **Secret Key validity period**: click the drop-down list and select either **1 year** or **2 years**. One year is the default value.

Click **Sign in** to authenticate to Azure as an administrative user. These credentials aren't saved by Configuration Manager. This persona doesn't require permissions in Configuration Manager, and doesn't need to be the same account that runs the Azure Services Wizard. After successfully authenticating to Azure, the page shows the **Azure AD Tenant Name** for reference. 

Click **OK** to create the web app in Azure AD and close the Create Server Application dialog. This action returns to the [Server app dialog](#server-app-dialog).


### Native Client app
	
This app is the Azure AD type *Native*, also referred to as a client app in Configuration Manager.

#### Client App dialog

When you click **Browse** for the **Native Client app** on the App page of the Azure Services Wizard, it opens the Client App dialog. It displays a list that shows the following properties of any existing native apps:
- Tenant friendly name
- App friendly name
- Service Type

There are three actions you can take from the Client App dialog:
- To reuse an existing native app, select it from the list. 
- Click **Import** to open the [Import apps dialog](#import-apps-dialog-client).
- Click **Create** to open the [Create Client Application dialog](#create-client-application-dialog).

After you select, import or create a native app, click **OK** to close the Client App dialog. This action returns to the [App page](#azure-app-properties) of the Azure Services Wizard.

#### Import apps dialog (client)

When you click **Import** from the Client App dialog, it opens the Import apps dialog. This page lets you enter information about an Azure AD native app that is already created in the Azure portal. It imports metadata about that native app into Configuration Manager. Specify the following information:
- **Application Name**: A friendly name for the app.
- **Client ID** 

After entering the information, click **Verify**. Then click **OK** to close the Import apps dialog. This action returns to the [Client App dialog](#client-app-dialog).

#### Create Client Application dialog

When you click **Create** from the Client App dialog, it opens the Create Client Application dialog. This page automates the creation of a native app in Azure AD. Specify the following information:
- **Application Name**: A friendly name for the app.
- **Reply URL**: This value isn't used by Configuration Manager, but required by Azure AD. By default this value is https://ConfigMgrService. 

Click **Sign in** to authenticate to Azure as an administrative user. These credentials aren't saved by Configuration Manager. This persona doesn't require permissions in Configuration Manager, and doesn't need to be the same account that runs the Azure Services Wizard. After successfully authenticating to Azure, the page shows the **Azure AD Tenant Name** for reference. 

Click **OK** to create the native app in Azure AD and close the Create Client Application dialog. This action returns to the [Client App dialog](#client-app-dialog).


## Configuration or Discovery

After specifying the web and native apps on the Apps page, the Azure Services Wizard proceeds to either a **Configuration** or **Discovery** page, depending upon the service to which you're connecting. The details of this page vary from service to service. For more information, see one of the following articles:  

-   **Cloud Management** service, **Discovery** page: [Configure Azure AD User Discovery](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)  

-   **Log Analytics Connector** service, **Configuration** page: [Configure the connection to Log Analytics](/sccm/core/clients/manage/sync-data-log-analytics#configure-the-connection-to-log-analytics)  

-   **Upgrade Readiness Connector** service, **Configuration** page: [Use the Azure Wizard to create the connection](/sccm/core/clients/manage/upgrade/upgrade-analytics#use-the-azure-wizard-to-create-the-connection)  

-   **Microsoft Store for Business** service, **Configurations** page: [Configure Microsoft Store for Business synchronization](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business#bkmk_config)  


Finally, complete the Azure Services Wizard through the Summary, Progress, and Completion pages. You've completed the configuration of an Azure service in Configuration Manager. Repeat this process to configure other Azure services.


## View the configuration of an Azure service
View the properties of an Azure service you've configured for use. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select **Azure Services**. Select the service you want to view or edit, and then click **Properties**.

If you select a service and then click **Delete** in the ribbon, this action deletes the connection in Configuration Manager. It doesn't remove the app in Azure AD. Ask your Azure administrator to delete the app when it's no longer needed. Or run the Azure Service Wizard to import the app.<!--483440-->


## Cloud management data flow

The following diagram is a conceptual data flow for the interaction between Configuration Manager, Azure AD, and connected cloud services. This specific example uses the **Cloud Management** service, which includes a Windows 10 client, and both server and client apps. The flows for other services are similar.

![Data flow diagram for Configuration Manager with Azure AD and Cloud Management](media/aad-auth.png)

1.	The Configuration Manager administrator imports or creates the client and server apps in Azure AD.  

2.	Configuration Manager Azure AD user discovery method runs. The site uses the Azure AD server app token to query Microsoft Graph for user objects.  

3.	The site stores data about the user objects. For more information, see [Azure AD User Discovery](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc).  

4.  The Configuration Manager client requests the Azure AD user token. The client makes the claim using the application ID of the Azure AD client app, and the server app as the audience. For more information, see [Claims in Azure AD Security Tokens](/azure/active-directory/develop/active-directory-authentication-scenarios#claims-in-azure-ad-security-tokens).  

5.  The client authenticates with the site by presenting the Azure AD token to the cloud management gateway and/or on-premises HTTPS-enabled management point.  


