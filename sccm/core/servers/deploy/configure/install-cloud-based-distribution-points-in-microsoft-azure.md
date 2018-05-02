---
title: "Install cloud-based distribution points"
titleSuffix: "Configuration Manager"
description: "Learn what you need to do to start using cloud-based distribution points in Microsoft Azure."
ms.date: 2/8/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: bb83ac87-9914-4a35-b633-ad070031aa6e
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Install cloud-based distribution points in Microsoft Azure for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

You can install System Center Configuration Manager cloud-based distribution points in Microsoft Azure. If you're unfamiliar with cloud-based distribution points, see [Use a cloud-based distribution point](../../../../core/plan-design/hierarchy/use-a-cloud-based-distribution-point.md) before continuing.

 Before you begin the installation, make sure that you have the required certificate files:  

-   A Microsoft Azure management certificate that is exported to a .cer file and to a .pfx file.  

-   A Configuration Manager cloud-based distribution point service certificate that is exported to a .pfx file.  

    > [!TIP]
    >   For more information about these certificates, see the section for cloud-based distribution points in the [PKI certificate requirements for System Center Configuration Manager](../../../../core/plan-design/network/pki-certificate-requirements.md) topic. For an example deployment of the cloud-based distribution point service certificate, see the "Deploying the Service Certificate for Cloud-Based Distribution Points" section in [Step-by-step example deployment of the PKI certificates for System Center Configuration Manager: Windows Server 2008 Certification Authority](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  


 After you install the cloud-based distribution point, Azure automatically generates a GUID for the service, and appends this to the DNS suffix of **cloudapp.net**. Using this GUID, you must configure DNS with a DNS alias (CNAME record). This lets you map the service name that you define in the Configuration Manager cloud-based distribution point service certificate to the automatically generated GUID.  

 If you use a proxy web server, you might have to configure proxy settings to enable communication with the cloud service that hosts the distribution point.  

##  <a name="BKMK_ConfigWindowsAzureandInstallDP"></a> Set up Azure and install cloud-based distribution points  
 Use the following procedures to set up Azure to support distribution points, and then install the cloud-based distribution point in Configuration Manager.  

### To set up a cloud service in Azure for a distribution point  

1.  Open a web browser to the Azure portal, at https://manage.windowsazure.com, and access your account.  

2.  Click **Hosted Services, Storage Accounts & CDN**, and then select **Management Certificates**.  

3.  Right-click your subscription, and then select **Add Certificate**.  

4.  For **Certificate file**, specify the .cer file that contains the exported Azure management certificate to use for this cloud service, and then click **OK**.  

The management certificate is loaded in Azure, and you can now install a cloud-based distribution point.  

### To install a cloud-based distribution point for Configuration Manager  

1.  Complete the steps in the preceding procedure to set up a cloud service in Azure with a management certificate.  

2.  In the **Administration** workspace of the Configuration Manager console, expand **Cloud Services**, and select **Cloud Distribution Points**. On the **Home** tab, click **Create Cloud Distribution Point**.  

3.  On the **General** page of the Create Cloud Distribution Point Wizard, set up the following:  

    -   Specify the **Subscription ID** for your Azure account.  

        > [!TIP]  
        >  You can find your Azure subscription ID in the Azure portal.  

    -   Specify the **Management certificate**. Click **Browse** to specify the .pfx file that contains the exported Azure management certificate, and then enter the password for the certificate. Optionally, you can specify a version 1 .publishsettings file from Azure SDK 1.7.  

4.  Click **Next**. Configuration Manager connects to Azure to validate the management certificate.  

5.  On the **Settings** page, complete the following, and then click **Next**:  

    -   For **Region**, select the Azure region where you want to create the cloud service that hosts this distribution point.  

    -   For **Certificate file**, specify the .pfx file that contains the exported certificate for the Configuration Manager cloud-based distribution point service. Then enter the password.  

        > [!NOTE]  
        >  The **Service FQDN** box is automatically populated from the certificate subject name. In most cases, you do not have to edit it. The exception is if you are using a wildcard certificate in a testing environment. For example, in this case you might not specify the host name, so that multiple computers that have the same DNS suffix can use the certificate. In this scenario, the certificate subject contains a value similar to **CN=\*.contoso.com**, and Configuration Manager displays a message that you must specify the correct FQDN. Click **OK** to close the message, and then enter a specific name before the DNS suffix to provide a complete FQDN. For example, you might add **clouddp1** to specify the complete service FQDN of **clouddp1.contoso.com**. The Service FQDN must be unique in your domain and not match any domain-joined device.  
        >   
        >  Wildcard certificates are supported for testing environments only.  

6.  On the **Alerts** page, set up storage quotas, transfer quotas, and at what percentage of these quotas you want Configuration Manager to generate alerts. Then click **Next**.  

7.  Complete the wizard.  

The wizard creates a new hosted service for the cloud-based distribution point. After you close the wizard, you can monitor the installation progress of the cloud-based distribution point in the Configuration Manager console. You can also monitor the **CloudMgr.log** file on the primary site server. You can monitor the provisioning of the cloud service in the Azure portal.  

> [!NOTE]  
>  It can take up to 30 minutes to provision a new distribution point in Azure. The following message is repeated in the **CloudMgr.log** file until the storage account is provisioned: **Waiting for check if container exists. Will check again in 10 seconds**. Then, the service is created and configured.  

 You can identify that the cloud-based distribution point installation is completed by using the following methods:  

-   In the Azure portal, the **Deployment** for the cloud-based distribution point displays a status of **Ready**.  

-   In the Configuration Manager console, in the **Administration** workspace, **Hierarchy Configuration**, **Cloud** node, the cloud-based distribution point displays a status of **Ready**.  

-   Configuration Manager displays a status message ID **9409** for the SMS_CLOUD_SERVICES_MANAGER component.  

##  <a name="BKMK_ConfigDNSforCloudDPs"></a> Set up name resolution for cloud-based distribution points  
 Before clients can access the cloud-based distribution point, they must be able to resolve the name of the cloud-based distribution point to an IP address that Azure manages. Clients do this in two stages:  

1.  They map the service name that you provided with the certificate of the Configuration Manager cloud-based distribution point service to your Azure service FQDN. This FQDN contains a GUID and the DNS suffix of **cloudapp.net**. The GUID is automatically generated after you install the cloud-based distribution point. You can see the full FQDN in the Azure portal, by referencing the **SITE URL** in the dashboard of the cloud service. An example site URL is **http://d1594d4527614a09b934d470.cloudapp.net**.  

2.  They resolve the Azure service FQDN to the IP address that Azure allocates. This IP address can also be identified in the dashboard for the cloud service in the Azure portal, and is named **PUBLIC VIRTUAL IP ADDRESS (VIP)**.  

To map the service name that you provided with the Configuration Manager cloud-based distribution point service certificate (for example, **clouddp1.contoso.com**) to your Azure service FQDN (for example, **d1594d4527614a09b934d470.cloudapp.net**), DNS servers on the Internet must have a DNS alias (CNAME record). Clients can then resolve the Azure service FQDN to the IP address by using DNS servers on the Internet.  

##  <a name="BKMK_ConfigProxyforCloud"></a> Set up proxy settings for primary sites that manage cloud services  
 When you use cloud services with Configuration Manager, the primary site that manages the cloud-based distribution point must be able to connect to the Azure portal. The site connects using the **System** account of the primary site computer. This connection is made by using the default web browser on the primary site server computer.  

 On the primary site server that manages the cloud-based distribution point, you might have to set up proxy settings to enable the primary site to access the Internet and Azure.  

 Use the following procedure to set up proxy settings for the primary site server in the Configuration Manager console.  

> [!TIP]  
>  You can also set up the proxy server when you install new site system roles on the primary site server by using the **Add Site System Roles Wizard**.  

#### To set up proxy settings for the primary site server  

1.  In the Configuration Manager console, click **Administration**.  

2.  In the **Administration** workspace, expand **Site Configuration**, and click **Servers and Site System Roles**. Then select the primary site server that manages the cloud-based distribution point.  

3.  In the details pane, right-click **Site system**, and then click **Properties**.  

4.  In **Site System Properties**, select the **Proxy** tab, and then set up the proxy settings for this primary site server.  

5.  Click **OK** to save the settings.  
