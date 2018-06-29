---
title: Install cloud distribution points
titleSuffix: Configuration Manager
description: Use these steps to set up a cloud distribution point in Configuration Manager.
ms.date: 07/13/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bb83ac87-9914-4a35-b633-ad070031aa6e
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Install a cloud distribution point for Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

This article details the steps to install a Configuration Manager cloud distribution point in Microsoft Azure.  It includes the following sections:
- [Before you begin](#bkmk_before) 
- [Set up](#bkmk_setup)
- [Configure DNS](#bkmk_dns)
- [Set up site server proxy](#bkmk_proxy)
- [Distribute content and configure clients](#bkmk_client)
- [Monitor](#bkmk_monitor)
- [Modify](#bkmk_modify)


## <a name="bkmk_before"></a> Before you begin

Start by reading the article [Use a cloud distribution point](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point). That article helps you plan and design your cloud distribution points. 

Use the following checklist to make sure you have the necessary information and prerequisites to create a cloud distribution point:  

- The **Azure environment** to use. For example, The Azure Public Cloud or the Azure US Government Cloud.  

- If you plan to use the Azure **Classic service deployment**, you need the following requirements:  

    - The Azure **Subscription ID**.  

    - An Azure **Management certificate**, exported as both .CER and .PFX files. An Azure subscription administrator needs to add the .CER management certificate to the subscription in the [Azure portal](https://portal.azure.com).  

- Starting in version 1806, if you plan to use the **Azure Resource Manager deployment**, you need the following requirements:<!--1322209-->  

    - Integration with [Azure Active Directory](/sccm/core/servers/deploy/configure/azure-services-wizard) for **Cloud Management**. Azure AD user discovery isn't required.  

    - The Azure **Subscription ID**.  

    - The Azure **Resource Group**.  

    - A **Subscription admin account** needs to log on during the wizard.  

- A **Certificate file** for server authentication, exported as a .PFX file.  

- A globally unique **Service name** for the cloud distribution point.  

- The Azure **Region** for this deployment.  
 


##  <a name="bkmk_setup"></a> Set up   

Perform this procedure on the top-level site. That site is either a standalone primary site, or the central administration site.  

1.  In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select **Cloud Distribution Points**. In the ribbon, click **Create Cloud Distribution Point**.  

2.  On the **General** page of the Create Cloud Distribution Point Wizard, configure the following settings:  

    a. First specify the **Azure environment**.  

    b. Choose the Azure deployment method, and then configure the associated settings.  

       - **Azure Resource Manager deployment** (starting in version 1806, and recommended): Click **Sign in** to authenticate with an Azure subscription admin account. The wizard auto-populates the remaining fields from the information stored during the Azure AD integration prerequisite. If you own multiple subscriptions, select the **Subscription ID** of the desired subscription to use.  

       - **Classic service deployment** (and in Configuration Manager versions 1802 and earlier): Enter your Azure **Subscription ID**. Then click **Browse** and select the .PFX file for the Azure management certificate.  

3.  Click **Next**. Wait as the site tests the connection to Azure.  

4.  On the **Settings** page, specify the following settings, and then click **Next**:  

    - **Region**: Select the Azure region where you want to create the cloud distribution point.  

    - **Resource Group** (Azure Resource Manager deployment method only)  

        - **Use existing**: Select an existing resource group from the drop-down list.  

        - **Create new**: Enter the new resource group name to create in your Azure subscription.  

    <!--Is **Primary site** a configurable option?-->

    - **Certificate file**: Click **Browse** and select the .PFX file for the cloud distribution point server authentication certificate. The name from this certificate populates the required **Service FQDN** and **Service name** fields.  

        > [!NOTE]  
        > The cloud distribution point server authentication certificate supports wildcards. If you use a wildcard certificate, replace the asterisk (*) in the **Service FQDN** field with the desired hostname for the service.  

5. On the **Alerts** page, set up storage quotas, transfer quotas, and at what percentage of these quotas you want Configuration Manager to generate alerts. Then click **Next**.  

6. Complete the wizard.  


### Monitor installation  

The wizard creates a new hosted service for the cloud distribution point. After you close the wizard, monitor the installation progress of the cloud distribution point in the Configuration Manager console. Also monitor the **CloudMgr.log** file on the primary site server. Monitor the provisioning of the cloud service in the Azure portal.  

> [!NOTE]  
>  It can take up to 30 minutes to provision a new distribution point in Azure. The following message is repeated in the **CloudMgr.log** file until the storage account is provisioned:  
> `Waiting for check if container exists. Will check again in 10 seconds`  
> Then, the service is created and configured.  


### Verify installation

Verify that the cloud distribution point installation is complete by using the following methods:  

- In the Azure portal, the **Deployment** for the cloud distribution point displays a status of **Ready**.  

- In the Configuration Manager console, go to the **Administration** workspace. Expand **Cloud Services**, and select the **Cloud Distribution Points** node. Find the new cloud distribution point in the list. The Status column should be **Ready**.  

- In the Configuration Manager console, go to the **Monitoring** workspace. Expand **System Status**, and select the **Component Status** node. Show all messages from the **SMS_CLOUD_SERVICES_MANAGER** component, and look for status message ID **9409**.  



##  <a name="bkmk_dns"></a> Configure DNS  

Before clients can use the cloud distribution point, they must be able to resolve the name of the cloud distribution point to an IP address that Azure manages. 

### Terminology  

- **Service FQDN**: The name you provided with the server authentication certificate for the cloud distribution point. For example, `WallaceFalls.Contoso.com`.  

- **Azure service FQDN**: The fully qualified domain name (FQDN) of the Azure service. When you create the cloud service for the distribution point, this name is automatically generated by Azure. View the full service FQDN in the [Azure portal](https://portal.azure.com), from the **Cloud services (classic)** blade. Find **Site URL** in the cloud service **Overview**. For example, `http://d1594d4527614a09b934d470.cloudapp.net`.  

- Azure **Public IP address**: The public IP address that Azure gives to the cloud service. Find **Public IP addresses** in the cloud service properties in the Azure portal. For example, `169.254.1.42`.   


### Create CNAME alias

Create a canonical name record (CNAME) in your organization's public DNS. This record creates an alias for the cloud distribution point's certificate **Service FQDN** to the cloud service's **Azure service FQDN**. For example, create a new CNAME record for `WallaceFalls.Contoso.com` to the real Azure service FQDN, `d1594d4527614a09b934d470.cloudapp.net`.  


### Client name resolution process

The following process shows how a client resolves the name of the cloud distribution point:  

1. The client gets the **Service FQDN** of the cloud distribution point in the list of content sources. For example, `WallaceFalls.Contoso.com`.  

2. It queries DNS, which resolves the Service FQDN using the CNAME alias to the **Azure service FQDN**. For example, `d1594d4527614a09b934d470.cloudapp.net`.  

3. It queries DNS again, which resolves the Azure service FQDN to the Azure **Public IP address**. For example, `169.254.1.42`.   

4. The client uses this IP address to start communication with the cloud distribution point.   

5. The cloud distribution point presents the server authentication certificate to the client. The client uses the trust chain of the certificate to validate.  



## <a name="bkmk_proxy"></a> Set up site server proxy  

When you use a cloud distribution point, the primary site server that manages the cloud distribution point needs to communicate with Azure. The site connects using the **System** account of the primary site server. It makes this connection using web browser APIs. If your organization uses a proxy server to control internet access, configure the primary site server to use this proxy.   

1.  In the Configuration Manager console, go to the **Administration** workspace. Expand **Site Configuration**, and select the **Servers and Site System Roles** node. Select the primary site server that manages the cloud distribution point.  

    > [!Tip]  
    > To find the site, open the properties of the cloud distribution point. Switch to the **Settings** tab, and look at the **Primary site** value. Then locate the primary site server for that site.   

2.  In the details pane, right-click the **Site system** role, and select **Properties**.  

3.  In the Site system Properties window, switch to the **Proxy** tab. Configure the proxy settings for this primary site server as needed in your environment.  

4.  Click **OK** to save the settings.  



## <a name="bkmk_client"></a> Distribute content and configure clients

Distribute content to the cloud distribution point the same as any other on-premises distribution point. The management point doesn't include the cloud distribution point in the list of content locations unless it has the content that clients request. 

Manage a cloud distribution point the same as any other on-premises distribution point. This includes assigning to a distribution point group, and managing content packages. For more information, see [Install and configure distribution points](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points).

Default client settings automatically enable clients to use cloud distribution points. Control access to all cloud distribution points in your hierarchy with the following client setting:  

   - In the **Cloud Settings** group, modify the setting **Allow access to cloud distribution points**.  

       - By default, this setting is set to **Yes**.  

       - Modify and deploy this setting for both users and devices.  



## <a name="bkmk_monitor"></a> Monitor  

-   **Monitor cloud distribution points**: You can monitor the content that you deploy to each cloud distribution point, and you can monitor the cloud service that hosts the distribution point.  

    -   **Content**: You monitor content that you deploy to a cloud distribution point the same way you do when you deploy content to on-premises distribution points.  

    -   **Cloud service**: Configuration Manager periodically checks the Azure service and raises an alert if the service is not active, or if there are subscription or certificate issues. You can also view details about the distribution point in the **Cloud Distribution Points** node under **Cloud Services** in the **Administration** workspace of the Configuration Manager console. From this location, you view high-level information about the distribution point. You can also select a distribution point and then edit its properties.  

    When you edit the properties of a cloud distribution point, you can:  

    -   Adjust the data thresholds for storage and alerts.  

    -   Manage content as you would for an on-premises distribution point.  

    Finally, for each cloud distribution point, you can view, but not edit, the subscription ID, service name, and other related details that are specified when the cloud-based distribution is installed.  




-   **Thresholds for data transfers**: You can configure thresholds for the amount of data that you want to store on the distribution point, and for the amount of data that clients download from the distribution point.  

     Thresholds for cloud distribution points include the following:  

    -   **Storage alert threshold**: A storage alert threshold sets an upper limit on the amount of data or content that you want store on the cloud distribution point. Configuration Manager can generate a warning alert when the remaining free space reaches the level that you specify.  

    -   **Transfer alert threshold**: A transfer alert threshold helps you to monitor the amount of content that transfers from the distribution point to clients for a 30-day period. The transfer alert threshold monitors the transfer of data for the previous 30 days, and can raise a warning alert and a critical alert when transfers reach values that you define.  

        > [!IMPORTANT]  
        >  Configuration Manager monitors the transfer of data, but does not stop the transfer of data beyond the specified transfer alert threshold.  

 You can specify thresholds for each cloud distribution point during the installation of the distribution point, or you can edit the properties of each cloud distribution point after it is installed.  

-   **Alerts**: You can configure Configuration Manager to raise alerts about data transfers to and from each cloud distribution point, based on the data transfer thresholds that you specify. These alerts help you monitor data transfers, and can help you decide when to stop the cloud service, adjust the content that you store on the distribution point, or modify which clients can use cloud distribution points.  

     In an hourly cycle, the primary site that monitors the cloud distribution point downloads transaction data from Azure and stores it in the CloudDP-&lt;ServiceName\>.log on the site server. Configuration Manager then evaluates this information against the storage and transfer quotas for each cloud distribution point. When the transfer of data reaches or exceeds the specified volume for either warnings or critical alerts, Configuration Manager generates the appropriate alert.  

    > [!WARNING]  
    >  Because information about data transfers is downloaded from Azure hourly, that data usage might exceed a warning or critical threshold before Configuration Manager can access the data and raise an alert.  

    > [!NOTE]  
    >  Alerts for a cloud distribution point depend on usage statistics from Azure, which can take up to 24 hours to become available. For information about Storage Analytics for Azure, including how frequently Azure updates use statistics, see [Storage Analytics](http://go.microsoft.com/fwlink/p/?LinkID=275111) in the MSDN Library.  


-   **Stop or start the cloud service on demand**: You can use the option to stop a cloud service at any time to prevent clients from using the service continuously. When you stop the cloud service, you immediately prevent clients from downloading additional content from the service. Additionally, you can restart the cloud service to restore access for clients. For example, you might want to stop a cloud service when data thresholds are reached.  

     When you stop a cloud service, the cloud service does not delete the content from the distribution point and does not prevent the site server from transferring additional content to the cloud distribution point.  

     To stop a cloud service, in the Configuration Manager console, select the distribution point in the **Cloud Distribution Points** node under **Cloud Services**, in the **Administration** workspace. Next, choose **Stop service** to stop the cloud service that runs in Azure.  



## <a name="bkmk_modify"></a> Modify

Stop service

Settings - Change **Certificate file**

<!--What happens when the certificate expires-->

Alerts

Scale in Azure portal (add more instances)


-   **Uninstall a cloud distribution point** : To uninstall a cloud distribution point, select the distribution point in the Configuration Manager console, and then select **Delete**.  

    When you delete a cloud distribution point from a hierarchy, Configuration Manager removes the content from the cloud service in Azure.  

