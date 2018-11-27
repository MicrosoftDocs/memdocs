---
title: Install cloud distribution points
titleSuffix: Configuration Manager
description: Use these steps to set up a cloud distribution point in Configuration Manager.
ms.date: 11/27/2018
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

This article details the steps to install a Configuration Manager cloud distribution point in Microsoft Azure. It includes the following sections:
- [Before you begin](#bkmk_before) 
- [Set up](#bkmk_setup)
- [Configure DNS](#bkmk_dns)
- [Set up site server proxy](#bkmk_proxy)
- [Distribute content and configure clients](#bkmk_client)
- [Manage and monitor](#bkmk_monitor)
- [Modify](#bkmk_modify)
- [Advanced troubleshooting](#bkmk_tshoot) 



## <a name="bkmk_before"></a> Before you begin

Start by reading the article [Use a cloud distribution point](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point). That article helps you plan and design your cloud distribution points. 

Use the following checklist to make sure you have the necessary information and prerequisites to create a cloud distribution point:  

- The site server can connect to Azure. If your network uses a proxy, [configure the site system role](#bkmk_proxy).  

- The **Azure environment** to use. For example, the Azure Public Cloud or the Azure US Government Cloud.  

- Starting in version 1806 and *recommended*, use the **Azure Resource Manager deployment**. It has the following requirements:<!--1322209-->  

    - Integration with [Azure Active Directory](/sccm/core/servers/deploy/configure/azure-services-wizard) for **Cloud Management**. Azure AD user discovery isn't required.  

    - The Azure **Subscription ID**.  

    - The Azure **Resource Group**.  

    - A **subscription admin account** needs to sign in during the wizard.  

- If you plan to use the Azure **classic service deployment**, you need the following requirements:  
    > [!Important]  
    > Starting in version 1810, classic service deployments in Azure are deprecated in Configuration Manager. Start using Azure Resource Manager deployments for the cloud management gateway. For more information, see [Plan for CMG](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager).  

    - The Azure **Subscription ID**.  

    - An Azure **management certificate**, exported as both .CER and .PFX files. An Azure subscription administrator needs to add the .CER management certificate to the subscription in the [Azure portal](https://portal.azure.com).  

- A **server authentication certificate**, exported as a .PFX file.  

- A globally unique **service name** for the cloud distribution point.  

    > [!TIP]  
    > Before requesting the server authentication certificate that uses this service name, confirm that the desired Azure domain name is unique. For example, *WallaceFalls.CloudApp.Net*. Sign in to the [Microsoft Azure portal](https://portal.azure.com). Select **Create a resource**, choose the **Compute** category, then select **Cloud Service**. In the **DNS name** field, type the desired prefix, for example *WallaceFalls*. The interface reflects whether the domain name is available or already in use by another service. Don't create the service in the portal, just use this process to check the name availability.  
 
- The Azure **region** for this deployment.  



##  <a name="bkmk_setup"></a> Set up   

Perform this procedure on the site to host this cloud distribution point as determined by your [design](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#bkmk_topology).  

1.  In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select **Cloud Distribution Points**. In the ribbon, select **Create Cloud Distribution Point**.  

2.  On the **General** page of the Create Cloud Distribution Point Wizard, configure the following settings:  

    1. First specify the **Azure environment**.  

    2. Starting in version 1806 and *recommended*, select **Azure Resource Manager deployment** as the deployment method. Select **Sign in** to authenticate with an Azure subscription admin account. The wizard auto-populates the remaining fields from the information stored during the Azure AD integration prerequisite. If you own multiple subscriptions, select the **Subscription ID** of the desired subscription to use.  

    > [!Note]  
    > Starting in version 1810, classic service deployments in Azure are deprecated in Configuration Manager. 
    > 
    > If you need to use a classic service deployment, select that option on this page. First enter your Azure **Subscription ID**. Then select **Browse** and select the .PFX file for the Azure management certificate.  

3.  Select **Next**. Wait as the site tests the connection to Azure.  

4.  On the **Settings** page, specify the following settings, and then select **Next**:  

    - **Region**: Select the Azure region where you want to create the cloud distribution point.  

    - **Resource Group** (Azure Resource Manager deployment method only)  

        - **Use existing**: Select an existing resource group from the drop-down list.  

        - **Create new**: Enter the new resource group name to create in your Azure subscription.  

    - **Primary site**: Select the primary site to distribute content to this distribution point.

    - **Certificate file**: Select **Browse** and select the .PFX file for this cloud distribution point's server authentication certificate. The common name from this certificate populates the required **Service FQDN** and **Service name** fields.  

        > [!NOTE]  
        > The cloud distribution point server authentication certificate supports wildcards. If you use a wildcard certificate, replace the asterisk (*) in the **Service FQDN** field with the desired hostname for the service.  

5. On the **Alerts** page, set up storage quotas, transfer quotas, and at what percentage of these quotas you want Configuration Manager to generate alerts. Then select **Next**.  

6. Complete the wizard.  


### Monitor installation  

The site starts to create a new hosted service for the cloud distribution point. After you close the wizard, monitor the installation progress of the cloud distribution point in the Configuration Manager console. Also monitor the **CloudMgr.log** file on the primary site server. If necessary, monitor the provisioning of the cloud service in the Azure portal.  

> [!NOTE]  
>  It can take up to 30 minutes to provision a new distribution point in Azure. The **CloudMgr.log** file repeats the following message until the storage account is provisioned:  
> `Waiting for check if container exists. Will check again in 10 seconds`  
> After it provisions the storage account, the service is created and configured.  


### Verify installation

Verify that the cloud distribution point installation is complete by using the following methods:  

- In the Configuration Manager console, go to the **Administration** workspace. Expand **Cloud Services**, and select the **Cloud Distribution Points** node. Find the new cloud distribution point in the list. The Status column should be **Ready**.  

- In the Configuration Manager console, go to the **Monitoring** workspace. Expand **System Status**, and select the **Component Status** node. Show all messages from the **SMS_CLOUD_SERVICES_MANAGER** component, and look for status message ID **9409**.  

- If necessary, go to the Azure portal. The **Deployment** for the cloud distribution point displays a status of **Ready**.  



##  <a name="bkmk_dns"></a> Configure DNS  

Before clients can use the cloud distribution point, they must be able to resolve the name of the cloud distribution point to an IP address that Azure manages. The management point gives them the **Service FQDN** of the cloud distribution point. The cloud distribution point exists in Azure as the **Service name**. See these values on the **Settings** tab of the cloud distribution point properties. 

> [!Note]  
> The **Cloud Distribution Points** node in the console includes a column named **Service Name**, but actually shows the **Service FQDN** value. To see both values, open **Properties** for the cloud distribution point and switch to the **Settings** tab.  

<!-- Remove based on feedback from RoYork
If you issue the server authentication certificate from your PKI, you may directly specify the Azure **Service name**. For example, `WallaceFalls.cloudapp.net`. When you specify this certificate in the Create Cloud Distribution Point Wizard, both the **Service FQDN** and **Service name** properties are the same. In this scenario, you don't need to configure DNS. The name that clients receive from the management point is the same name as the service in Azure.  
-->

The server authentication certificate common name should include your domain name. This name is required when you purchase a certificate from a public provider. It's recommended when issuing this certificate from your PKI. For example, `WallaceFalls.contoso.com`. When you specify this certificate in the Create Cloud Distribution Point Wizard, the common name populates the **Service FQDN** property (`WallaceFalls.contoso.com`). The **Service name** takes the same hostname (`WallaceFalls`) and appends it to the Azure domain name, `cloudapp.net`. In this scenario, clients need to resolve your domain's **Service FQDN** (`WallaceFalls.contoso.com`) to the Azure **Service name** (`WallaceFalls.cloudapp.net`). Create a CNAME alias to map these names.


### Create CNAME alias

Create a canonical name record (CNAME) in your organization's public, internet-facing DNS. This record creates an alias for the cloud distribution point's **Service FQDN** property that clients receive, to the Azure **Service name**. For example, create a new CNAME record for `WallaceFalls.contoso.com` to `WallaceFalls.cloudapp.net`.  


### Client name resolution process

The following process shows how a client resolves the name of the cloud distribution point:  

1. The client gets the **Service FQDN** of the cloud distribution point in the list of content sources. For example, `WallaceFalls.contoso.com`.  

2. It queries DNS, which resolves the Service FQDN using the CNAME alias to the Azure **Service name**. For example, `WallaceFalls.cloudapp.net`.  

3. It queries DNS again, which resolves the Azure service name to the Azure public IP address.   

4. The client uses this IP address to start communication with the cloud distribution point.   

5. The cloud distribution point presents the server authentication certificate to the client. The client uses the trust chain of the certificate to validate.  



## <a name="bkmk_proxy"></a> Set up site server proxy  

The primary site server that manages the cloud distribution point needs to communicate with Azure. If your organization uses a proxy server to control internet access, configure the primary site server to use this proxy.   

For more information, see [Proxy server support](/sccm/core/plan-design/network/proxy-server-support).  



## <a name="bkmk_client"></a> Distribute content and configure clients

Distribute content to the cloud distribution point the same as any other on-premises distribution point. The management point doesn't include the cloud distribution point in the list of content locations unless it has the content that clients request. For more information, see [Distribute and manage content](/sccm/core/servers/deploy/configure/deploy-and-manage-content). 

Manage a cloud distribution point the same as any other on-premises distribution point. These actions include assigning it to a distribution point group, and managing content packages. For more information, see [Install and configure distribution points](/sccm/core/servers/deploy/configure/install-and-configure-distribution-points).

Default client settings automatically enable clients to use cloud distribution points. Control access to all cloud distribution points in your hierarchy with the following client setting:  

   - In the **Cloud Settings** group, modify the setting **Allow access to cloud distribution points**.  

       - By default, this setting is set to **Yes**.  

       - Modify and deploy this setting for both users and devices.  



## <a name="bkmk_monitor"></a> Manage and monitor  

Monitor content that you distribute to a cloud distribution point the same as with any other on-premises distribution points. For more information, see [Monitor content](/sccm/core/servers/deploy/configure/monitor-content-you-have-distributed). 

### <a name="bkmk_alerts"></a> Alerts  

Configuration Manager periodically checks the Azure service. If the service isn't active, or if there are subscription or certificate issues, Configuration Manager raises an alert. 

Configure thresholds for the amount of data that you want to store on the cloud distribution point, and for the amount of data that clients download from the distribution point. Use alerts for these thresholds to help you decide when to stop or delete the cloud service, adjust the content that you store on the cloud distribution point, or modify which clients can use the service. 

- **Storage alert threshold**: The storage alert threshold sets an upper limit in GB on the amount of data or content that you want store on the cloud distribution point. By default, this threshold is 2,000 GB. Configuration Manager generates warning and critical alerts when the remaining free space reaches the levels that you specify. By default, these alerts occur at 50% and 90% of the threshold.  

- **Monthly transfer alert threshold**: The monthly transfer alert threshold helps you to monitor the amount of content that transfers from the distribution point to clients for a 30-day period. By default, this threshold is 10,000 GB. The site raises warning and critical alerts when transfers reach values that you define. By default, these alerts occur at 50% and 90% of the threshold.  

    > [!IMPORTANT]  
    >  Configuration Manager monitors the transfer of data, but does not stop the transfer of data beyond the specified transfer alert threshold.  

Specify thresholds for each cloud distribution point during installation, or use the **Alerts** tab of the cloud distribution point properties.  

> [!NOTE]  
>  Alerts for a cloud distribution point depend on usage statistics from Azure, which can take up to 24 hours to become available. For more information about Storage Analytics for Azure, see [Storage Analytics](https://docs.microsoft.com/rest/api/storageservices/storage-analytics).  

In an hourly cycle, the primary site that monitors the cloud distribution point downloads transaction data from Azure. It stores this transaction data in the `CloudDP-<ServiceName>.log` file on the site server. Configuration Manager then evaluates this information against the storage and transfer quotas for each cloud distribution point. When the transfer of data reaches or exceeds the specified volume for either warnings or critical alerts, Configuration Manager generates the appropriate alert.  

> [!WARNING]  
>  Because the site downloads information about data transfers from Azure every hour, the usage might exceed a warning or critical threshold before Configuration Manager can access the data and raise an alert.  



## <a name="bkmk_modify"></a> Modify

View high-level information about the distribution point in the **Cloud Distribution Points** node under **Cloud Services** in the **Administration** workspace of the Configuration Manager console. Select a distribution point and select **Properties** to see more details.  

When you edit the properties of a cloud distribution point, the following tabs include settings to edit:  

#### Settings  

- **Description**  

- **Certificate file**: Before the server authentication certificate expires, issue a new certificate with the same common name. Then add the new certificate here for the service to start using. If the certificate expires, clients won't trust and use the service.  

#### Alerts
Adjust the data thresholds for storage and monthly transfer alerts.  

#### Content
Manage content the same as for an on-premises distribution point.  


### Redeploy the service

More significant changes, such as the following configurations, require redeploying the service:
- Classic deployment method to Azure Resource Manager
- Subscription
- Service name
- Private to public PKI
- Azure region

Starting in version 1806, if you have an existing cloud distribution point on the classic deployment method, in order to use the Azure Resource Manager deployment method you need to deploy a new cloud distribution point. There are two options:

- If you want to reuse the same service name:  

    1. First delete the classic cloud distribution point. If there isn't another cloud distribution point, then clients may not be able to get content.  

    2. Create a new cloud distribution point using a Resource Manager deployment. Reuse the same server authentication certificate.  

    3. Distribute the necessary software package content to the new cloud distribution point.  

- If you want to use a new service name:  

    1. Create a new cloud distribution point using a Resource Manager deployment. Use a new server authentication certificate.  

    2. Distribute the necessary software package content to the new cloud distribution point.  

    3. Delete the classic cloud distribution point.

> [!Tip]  
> To determine the current deployment model of a cloud distribution point:<!--SCCMDocs issue #611-->  
> 1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Cloud Distribution Points** node.  
> 2. Add the **Deployment Model** attribute as a column to the list view. For a Resource Manager deployment, this attribute is **Azure Resource Manager**.  


### Stop or start the cloud service on demand

Stop a cloud distribution point at any time in the Configuration Manager console. This action immediately prevents clients from downloading additional content from the service. Restart the cloud service from the Configuration Manager console to restore access for clients. For example, stop a cloud service when it reaches a data threshold.  

When you stop a cloud distribution point, the cloud service doesn't delete the content from the storage account. It also doesn't prevent the site server from transferring additional content to the cloud distribution point. The management point still returns the cloud distribution point to clients as a valid content source. 

Use the following procedure to stop a cloud distribution point:  

1. In the Configuration Manager console, go to the **Administration** workspace. Expand **Cloud Services**, and select the **Cloud Distribution Points** node.  

2. Select the cloud distribution point. To stop the cloud service that runs in Azure, select **Stop service** in the ribbon.  

3. Select **Start service** to restart the cloud distribution point.  


### Delete a cloud distribution point

To uninstall a cloud distribution point, select the distribution point in the Configuration Manager console, and then select **Delete**.  

When you delete a cloud distribution point from a hierarchy, Configuration Manager removes the content from the cloud service in Azure. 

Manually removing any components in Azure causes the system to be inconsistent. This state leaves orphaned information, and unexpected behaviors may occur.



## <a name="bkmk_tshoot"></a> Advanced troubleshooting

If you need to collect diagnostic logging from the Azure VMs to help troubleshoot problems with your cloud distribution point, use the following PowerShell sample to enable the service diagnostic extension for the subscription:<!--514275-->  

``` PowerShell
# Change these variables for your Azure environment. The current values are provided as examples. You can find the values for these from the Azure portal.
$storage_name="4780E38368358502‬‭23C071" # The name of the storage account that goes with the CloudDP
$key="3jSyvMssuTyAyj5jWHKtf2bV5JF^aDN%z%2g*RImGK8R4vcu3PE07!P7CKTbZhT1Sxd3l^t69R8Cpsdl1xhlhZtl" # The storage access key from the Storage Account view
$service_name="4780E38368358502‬‭23C071" # The name of the cloud service for the CloudDP, which for a Cloud DP is the same as the storage name
$azureSubscriptionName="8ba1cb83-84a2-457e-bd37-f78d2dd371ee" # The subscription name the tenant is using 
$subscriptionId="8ba1cb83-84a2-457e-bd37-f78d2dd371ee" # The subscription ID the tenant is using 

# This variable is the path to the config file on the local computer.
$public_config="F:\PowerShellDiagFile\diagnostics.wadcfgx"

# These variables are for the Azure management certificate. Install it in the Current User certificate store on the system running this script. 
$thumbprint="dac9024f54d8f6df94935fb1732638ca6ad77c13" # The thumbprint of the Azure management certificate 
$mycert = Get-Item cert:\\CurrentUser\My\$thumbprint

Set-AzureSubscription -SubscriptionName $azureSubscriptionName -SubscriptionId $subscriptionId -Certificate $mycert

Select-AzureSubscription $azureSubscriptionName

Set-AzureServiceDiagnosticsExtension -StorageAccountName $storage_name -StorageAccountKey $key -DiagnosticsConfigurationPath $public_config –ServiceName $service_name -Slot 'Production' -Verbose
```


The following sample is an example **diagnostics.wadcfgx** file as referenced in the **public_config** variable in the above PowerShell script. For more information, see [Azure Diagnostics extension configuration schema](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics-schema).  

``` XML
<?xml version="1.0" encoding="utf-8"?>
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <WadCfg>
    <DiagnosticMonitorConfiguration overallQuotaInMB="4096">
      <Directories scheduledTransferPeriod="PT1M">
        <IISLogs containerName ="wad-iis-logfiles" />
        <FailedRequestLogs containerName ="wad-failedrequestlogs" />
      </Directories>
      <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Application!*" />
      </WindowsEventLog>
      <Logs scheduledTransferPeriod="PT1M" scheduledTransferLogLevelFilter="Information" />
      <CrashDumps dumpType="Full">
        <CrashDumpConfiguration processName="WaAppAgent.exe" />
        <CrashDumpConfiguration processName="WaIISHost.exe" />
        <CrashDumpConfiguration processName="WindowsAzureGuestAgent.exe" />
        <CrashDumpConfiguration processName="WaWorkerHost.exe" />
        <CrashDumpConfiguration processName="DiagnosticsAgent.exe" />
        <CrashDumpConfiguration processName="w3wp.exe" />
      </CrashDumps>
      <PerformanceCounters scheduledTransferPeriod="PT1M">
        <PerformanceCounterConfiguration counterSpecifier="\Memory\Available MBytes" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\ISAPI Extension Requests/sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Web Service(_Total)\Bytes Total/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Requests/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET Applications(__Total__)\Errors Total/Sec" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Queued" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\ASP.NET\Requests Rejected" sampleRate="PT3M" />
        <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT3M" />
      </PerformanceCounters>
    </DiagnosticMonitorConfiguration>
  </WadCfg>
</PublicConfig>
```

