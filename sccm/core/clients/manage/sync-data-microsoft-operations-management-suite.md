---
title: "Sync data to Microsoft Operations Management Suite "
titleSuffix: "Configuration Manager"
description: "Sync data from System Center Configuration Manager to Microsoft Operations Management Suite."
ms.custom: na
ms.date: 7/31/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 33bcf8b3-a6b6-4fc9-bb59-70a9621b2b0d
caps.latest.revision: 9
author: mattbriggs
ms.author: mabrigg
manager: angrobe
---

#  Sync data from Configuration Manager to the Microsoft Operations Management Suite

*Applies to: System Center Configuration Manager (Current Branch)*

You may use the **Azure Services Wizard** to configure your connection from Configuration Manager to Operations Management Suite (OMS) cloud service. Beginning with version 1706, the wizard replaces previous workflows to configure this connection. For earlier versions, see [Sync data from Configuration Manager to the Microsoft Operations Management Suite (1702 and earlier)](#Sync-data-from-Configuration-Manager-to-the-Microsoft-Operations-Management-Suite-(1702-and-earlier)).

- 	The wizard is used to configure cloud services for Configuration Manager, like OMS, Windows Store for Business (WSfB), and Azure Active Directory (Azure AD).  

-   Configuration Manager connects to OMS for features like [Log Analytics](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite), or [Upgrade Readiness](/sccm/core/clients/manage/upgrade/upgrade-analytics).

## Prerequisites for the OMS Connector
Prerequisites to configure a connection to OMS are unchanged from those [documented for the Current Branch version 1702](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite#prerequisites). That information is repeated here:  

- 	Before you install the OMS connector in Configuration Manager, you must provide Configuration Manager with permissions to OMS. Specifically, you must grant *contributor access* to the Azure *Resource Group* that contains the OMS Log Analytics workspace. The procedures to do so are documented in the Log Analytics content. See [Provide Configuration Manager with permissions to OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms) in the OMS documentation.

- 	The OMS connector must be installed on the computer that hosts a [service connection point](/sccm/core/servers/deploy/configure/about-the-service-connection-point) that is in [online mode](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation).

- 	You must install a Microsoft Monitoring Agent for OMS installed on the service connection point along with the OMS connector. The Agent and the OMS connector must be configured to use the same **OMS Workspace**. To install the agent, see [Download and install the agent](/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent) in the OMS documentation.
- 	After you install the connector and agent, you must configure OMS to use Configuration Manager data. To do so, in the OMS Portal you [Import Configuration Manager collections](/azure/log-analytics/log-analytics-sccm#import-collections).

## Use the Azure Services Wizard to configure the connection to OMS

1.	In the console, go to **Administration** > **Overview** > **Cloud Services** > **Azure Services**, and then choose **Configure Azure Services** from the **Home** tab of the ribbon, to start the **Azure Services Wizard**.

2.	On the **Azure Services** page, select the Operation Management Suite cloud service. Provide a friendly name for the **Azure service name** and an optional description, and then click **Next**.

3.	On the **App** page, specify your Azure environment (the technical preview supports only the Public Cloud). Then, click **Browse** to open the Server App window.

4.	Select a web app:

    - 	**Import**: To use a web app that already exists in your Azure subscription, click **Import**. Provide a friendly name for the app and the tenant, and then specify the Tenant ID, Client ID, and the secret key for the Azure web app that you want Configuration Manager to use. After you **Verify** the information, click **OK** to continue.   

    > [!NOTE] 	
    > When you configure OMS with this preview, OMS only supports the *import* function for a web app. Creating a new web app is not supported. Similarly, you cannot reuse an existing app for OMS.

5.	If you accomplished all the other procedures successfully, then the information on the **OMS Connection Configuration** screen will automatically appear on this page. Information for the connection settings should appear for your **Azure subscription**, **Azure resource group**, and **Operations Management Suite Workspace**.

6.	The wizard connects to the OMS service using the information you've input. Select the device collections that you want to sync with OMS and then click **Add**.

7.	Verify your connection settings on the **Summary** screen, then select **Next**. The **Progress** screen shows the connection status, then should **Complete**.

8.	After the wizard completes, the Configuration Manager console shows that you have configured **Operation Management Suite** as a **Cloud Service Type**.

## Sync data from Configuration Manager to the Microsoft Operations Management Suite (1702 and earlier)


*Applies to: System Center Configuration Manager (1702 and prior versions)*

You can use the Microsoft Operations Management Suite (OMS) Connector to sync data such as your collections from System Center Configuration Manager to OMS Log Analytics  in Microsoft Azure. This makes data from your Configuration Manager deployment visible in OMS.
> [!TIP]
> The OMS Connector is a pre-release feature. To learn more, see [Use pre-release features from updates](/sccm/core/servers/manage/pre-release-features).

Beginning with version 1702, you can use the OMS connector to connect to an OMS workspace that is on Microsoft Azure Government cloud. This requires you to modify a configuration file before you install the OMS connector. See [use the OMS connector with the Azure Government cloud](#fairfaxconfig) in this topic.

### Prerequisites
- Before you install the OMS connector in Configuration Manager, you must provide Configuration Manager with permissions to OMS. Specifically, you must grant *contributor access* to the Azure *Resource Group* that contains the OMS Log Analytics workspace. The procedures to do so are documented in the Log Analytics content. See [Provide Configuration Manager with permissions to OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms) in the OMS documentation.

- The OMS connector must be installed on the computer that hosts a [service connection point](/sccm/core/servers/deploy/configure/about-the-service-connection-point) that is in [online mode](/sccm/core/servers/deploy/configure/about-the-service-connection-point#a-namebkmkmodesa-modes-of-operation).

  If you have connected OMS to a standalone primary site and plan to add a central administration site to your environment, you must delete the current connection, and then reconfigure the connector at the new central administration site.

- You must install a Microsoft Monitoring Agent for OMS installed on the service connection point along with the OMS connector.  The Agent and the OMS connector must be configured to use the same **OMS Workspace**. To install the agent, see [Download and install the agent](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#download-and-install-the-agent) in the OMS documentation.

- After you install the connector and agent, you must configure OMS to use Configuration Manager data.  To do so, in the OMS Portal you [Import Configuration Manager collections](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#import-collections).



### Install the OMS Connector  
1. In the Configuration Manager console, configure your [hierarchy to use pre-release features](/sccm/core/servers/manage/pre-release-features), and then enable the use of the OMS Connector.  
0
2. Next, go to the **Administration** > **Cloud Services** > **OMS Connector**. In the ribbon, click on "Create connection to Operations Management Suite". This opens the **Connection to Operation Management Suite Wizard**. Select **Next**.  


3.	On the **General** page, confirm that you have the following information, then select **Next**.  
  - Registered Configuration Manager as a “Web Application and/or Web API” management tool, and that you have the [client ID from this registration](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications).  
  - Created a client key for the registered management tool in Azure Active Directory.  

  - In the Azure Management Portal, provided the registered web app with permission to access OMS, as described in [Provide Configuration Manager with permissions to OMS](https://docs.microsoft.com/azure/log-analytics/log-analytics-sccm#provide-configuration-manager-with-permissions-to-oms).  

4.	On the **Azure Active Directory** page, configure your connection settings to OMS by providing your **Tenant**, **Client ID**, and **Client secret key**, then select **Next**.  

5.	On the **OMS Connection Configuration** page, provide your connection settings by filling in your **Azure subscription**, **Azure resource group**, and **Operations Management Suite Workspace**.  The workspace must match the workspace that is configured for the Microsoft Management Agent that is installed on the service connection point.  

6.	Verify your connection settings on the **Summary** page, then select **Next**. The **Progress** page will show the connection status, then should **Complete**.

After you have linked Configuration Manager to OMS, you can add or remove collections, and view the properties of the OMS connection.

### Verify the OMS connector properties
1.	In the Configuration Manager console, go to **Administration** > **Cloud Services**, and then select **OMS Connector** to open the **OMS Connection ** page**.
2.	Within this page there are two tabs:
  - **Azure Active Directory:**   
    This tab shows your **Tenant**, **Client ID**, **Client secret key expiration**, and allows you to verify your client secret key has expired.

  - **OMS Connection Properties:**  
    This tab shows your **Azure subscription**, **Azure resource group**, **Operations Management Suite Workspace**, and a list of **Device collections that Operations Management Suite can get data for**. Use the **Add** and **Remove** buttons to modify which collections are allowed.

### <a name="fairfaxconfig"> </a> Use the OMS connector with the Azure Government cloud


1.  On any computer that has the Configuration Manager console installed, edit the following configuration file to point to the government cloud:  ***&lt;CM install path>\AdminConsole\bin\Microsoft.configurationManagmenet.exe.config***

  **Edits:**

    Change the value for the setting name *FairFaxArmResourceID* to be equal to “https://management.usgovcloudapi.net/”

   - **Original:**
      &lt;setting name="FairFaxArmResourceId" serializeAs="String">   
      &lt;value>&lt;/value>   
      &lt;/setting>

   - **Edited:**     
      &lt;setting name="FairFaxArmResourceId" serializeAs="String">
      &lt;value>https://management.usgovcloudapi.net/&lt;/value>  
      &lt;/setting>

  Change the value for the setting name *FairFaxAuthorityResource* to be equal to "https://login.microsoftonline.us/"

  - **Original:**
    &lt;setting name="FairFaxAuthorityResource" serializeAs="String">   
    &lt;value>&lt;/value>

	- **Edited:**
    &lt;setting name="FairFaxAuthorityResource" serializeAs="String">   
    &lt;value>https://login.microsoftonline.us/&lt;/value>

2.	After you save the file with the two changes, restart the Configuration Manager console on the same computer, and then use that console to install the OMS connector. To install the connector, use the information in [Sync data from Configuration Manager to the Microsoft Operations Management Suite](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite), and select the **Operations Management Suite Workspace** that is on the Microsoft Azure Government cloud.

3.	After the OMS connector installs, the connection to the Government cloud is available when you use any console that connects to the site.
