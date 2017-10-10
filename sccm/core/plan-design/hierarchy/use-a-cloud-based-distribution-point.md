---
title: "Cloud-based distribution point"
description: "Learn about configurations and limitations for using a cloud-based distribution point with System Center Configuration Manager."
ms.custom: na
ms.date: 3/27/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3cd9c725-6b42-427d-9191-86e67f84e48c
caps.latest.revision: 9
author: Brenduns
ms.author: brenduns
manager: angrobe

---
# Use a cloud-based distribution point with System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

A cloud-based distribution point is a System Center Configuration Manager distribution point that is hosted in Microsoft Azure. The following information is intended to help you learn about configurations and limitations for using a cloud-based distribution point.

After you have installed a primary site and are ready to install a cloud-based distribution point, see [Install cloud-based distribution points in Azure](../../../core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure.md).


## Plan to use a cloud-based distribution point
When you use a cloud-based distribution, you:  

-   **Configure client settings** to enable users and devices to access the content.  

-   **Specify a primary site to manage the transfer of content** to the distribution point.  

-   **Specify thresholds** for the amount of content that you want to store on the distribution point and the amount of content that you want to enable clients to transfer from the distribution point.  


Based on the thresholds that you configure, Configuration Manager can raise alerts that warn you when the combined amount of content that you have stored on the distribution point is near the specified storage amount, or when transfers of data by clients are close to the thresholds that you defined.  

Cloud-based distribution points support several features that are also offered by on-premises distribution points:  

-   You manage cloud-based distribution points individually or as members of distribution point groups.  

-   You can use a cloud-based distribution point as a fallback content location.  

-   You receive support for both intranet and Internet-based clients.  


Cloud-based distribution points provide the following additional benefits:  

-   Content that is sent to a cloud-based distribution point is encrypted by Configuration Manager before Configuration Manager sends it to Azure.  

-   In Azure, you can manually scale the cloud service to meet changing demands for content requests by clients, without the requirement to install and provision additional distribution points.  

-   The cloud-based distribution point supports the download of content by clients that are configured for Windows BranchCache.  


A cloud-based distribution point has the following limitations:  

-  Prior to using version 1610 with the Hotfix KB4010155, you cannot use a cloud-based distribution point to host software update packages. This issue is fixed beginning with version 1702, and later.  

-   You cannot use a cloud-based distribution point for PXE or multicast-enabled deployments.  

-   Clients are not offered a cloud-based distribution point as a content location for a task sequence that is deployed by using the deployment option **Download content locally when needed by running task sequence**. However, task sequences that are deployed by using the deployment option of **Download all content locally before starting task sequence** can use a cloud-based distribution point as a valid content location.  

-   A cloud-based distribution point does not support packages that run from the distribution point. All content must be downloaded by the client and then run locally.  

-   A cloud-based distribution point does not support streaming applications by using Application Virtualization or similar programs.  

-   A cloud-based distribution point does not support prestaged content. The distribution manager of the primary site that manages the distribution point transfers all content to the distribution point.  

-   A cloud-based distribution point cannot be configured as a pull-distribution point.  

##  <a name="BKMK_PrereqsCloudDP"></a> Prerequisites for cloud-based distribution points  
 A cloud-based distribution point requires the following prerequisites for its use:  

-   A subscription to Azure (see [About subscriptions and certificates](#BKMK_CloudDPCerts) in this topic).

-   A self-signed or public key infrastructure (PKI) management certificate for communication from a Configuration Manager primary site server to the cloud service in Azure (See [About subscriptions and certificates](#BKMK_CloudDPCerts) in this topic).

-   A service certificate (PKI) that Configuration Manager clients use to connect to cloud-based distribution points and download content from them by using HTTPS.  

-  A device or user must have **Allow Access to cloud distribution points** set to **Yes** in the client setting of **Cloud Services** before a device or user can access content from a cloud-based distribution point. By default, this value is set to **No**.  

-   A client must be able to resolve the name of the cloud service, which requires a Domain Name System (DNS) alias and a CNAME record in your DNS namespace.  

-   A client must be able to access the Internet to use the cloud-based distribution point.  

##  <a name="BKMK_CloudDPCost"></a> Cost of using cloud-based distribution  
 When you use a cloud-based distribution point, plan for the cost of data storage and the download transfers that Configuration Manager clients perform.  

 Configuration Manager includes options to help control costs and monitor data access:  

-   You can control and monitor the amount of content that you store in a cloud service.  

-   You can configure Configuration Manager to alert you when **thresholds** for client downloads meet or exceed monthly limits.  

-   In addition, you can  use peer caching (Windows BranchCache) to help reduce the number of data transfers from cloud-based distribution points by clients. Configuration Manager clients that are configured for BranchCache can transfer content by using cloud-based distribution points.  


**Options:**  

-   **Client Settings for Cloud**: You control access to all cloud-based distribution points in a hierarchy by using **Client Settings**.  

     In **Client Settings**, the category **Cloud Settings** supports the setting **Allow access to cloud distribution points**. By default, this setting is set to **No**. You can enable this setting for both users and devices.  

-   **Thresholds for data transfers**: You can configure thresholds for the amount of data that you want to store on the distribution point, and for the amount of data that clients download from the distribution point.  

     Thresholds for cloud-based distribution points include the following:  

    -   **Storage alert threshold**: A storage alert threshold sets an upper limit on the amount of data or content that you want store on the cloud-based distribution point. Configuration Manager can generate a warning alert when the remaining free space reaches the level that you specify.  

    -   **Transfer alert threshold**: A transfer alert threshold helps you to monitor the amount of content that transfers from the distribution point to clients for a 30-day period. The transfer alert threshold monitors the transfer of data for the previous 30 days, and can raise a warning alert and a critical alert when transfers reach values that you define.  

        > [!IMPORTANT]  
        >  Configuration Manager monitors the transfer of data, but does not stop the transfer of data beyond the specified transfer alert threshold.  

 You can specify thresholds for each cloud-based distribution point during the installation of the distribution point, or you can edit the properties of each cloud-based distribution point after it is installed.  

-   **Alerts**: You can configure Configuration Manager to raise alerts about data transfers to and from each cloud-based distribution point, based on the data transfer thresholds that you specify. These alerts help you monitor data transfers, and can help you decide when to stop the cloud service, adjust the content that you store on the distribution point, or modify which clients can use cloud-based distribution points.  

     In an hourly cycle, the primary site that monitors the cloud-based distribution point downloads transaction data from Azure and stores it in the CloudDP-&lt;ServiceName\>.log on the site server. Configuration Manager then evaluates this information against the storage and transfer quotas for each cloud-based distribution point. When the transfer of data reaches or exceeds the specified volume for either warnings or critical alerts, Configuration Manager generates the appropriate alert.  

    > [!WARNING]  
    >  Because information about data transfers is downloaded from Azure hourly, that data usage might exceed a warning or critical threshold before Configuration Manager can access the data and raise an alert.  

    > [!NOTE]  
    >  Alerts for a cloud-based distribution point depend on usage statistics from Azure, which can take up to 24 hours to become available. For information about Storage Analytics for Azure, including how frequently Azure updates use statistics, see [Storage Analytics](http://go.microsoft.com/fwlink/p/?LinkID=275111) in the MSDN Library.  


-   **Stop or start the cloud service on demand**: You can use the option to stop a cloud service at any time to prevent clients from using the service continuously. When you stop the cloud service, you immediately prevent clients from downloading additional content from the service. Additionally, you can restart the cloud service to restore access for clients. For example, you might want to stop a cloud service when data thresholds are reached.  

     When you stop a cloud service, the cloud service does not delete the content from the distribution point and does not prevent the site server from transferring additional content to the cloud-based distribution point.  

     To stop a cloud service, in the Configuration Manager console, select the distribution point in the **Cloud Distribution Points** node under **Cloud Services**, in the **Administration** workspace. Next, choose **Stop service** to stop the cloud service that runs in Azure.  

##  <a name="BKMK_CloudDPCerts"></a> About subscriptions and certificates for cloud-based distribution points  
 Cloud-based distribution points require certificates to enable Configuration Manager to manage the cloud service that hosts the distribution point, and for clients to access content from the distribution point. The following information provides an overview about these certificates. For more detailed information, see [PKI certificate requirements for System Center Configuration Manager](../../../core/plan-design/network/pki-certificate-requirements.md).  

 **Certificates**  

-   **Management certificate for site server to distribution point communication**: The management certificate establishes trust between the Azure management API and Configuration Manager. This authentication enables Configuration Manager to call on the Azure API when you perform tasks such as deploying content or starting and stopping the cloud service. By using  Azure, you can create your own management certificates, which can be either self-signed certificates or certificates that are issued by a certification authority (CA):  

    -   Provide the .cer file of the management certificate to Azure when you configure Azure for Configuration Manager. The .cer file contains the public key for the management certificate. You must upload this certificate to Azure before you install a cloud-based distribution point. This certificate enables Configuration Manager to access the Azure API.  

    -   Provide the .pfx file of the management certificate to Configuration Manager when you install the cloud-based distribution point. The .pfx file contains the private key for the management certificate. Configuration Manager stores this certificate in the site database. Because the .pfx file contains the private key, you must provide the password to import this certificate file into the Configuration Manager database.  

    If you create a self-signed certificate, you must first export the certificate as a .cer file and then export it again as a .pfx file.  

    Optionally, you can specify a version one **.publishsettings** file from the Azure SDK 1.7. For information about .publishsettings files, refer to the Azure documentation.  

    For more information, see [How to create a management certificate](http://go.microsoft.com/fwlink/p/?LinkId=220281) and [How to add a management certificate to an Azure subscription](http://go.microsoft.com/fwlink/p/?LinkId=241722) in the Azure platform section of the MSDN Library.  

-   **Service certificate for client communication to the distribution point**: The Configuration Manager cloud-based distribution point service certificate establishes trust between the Configuration Manager clients and the cloud-based distribution point, and secures the data that clients download from it by using Secure Socket Layer (SSL) over HTTPS.  

    > [!IMPORTANT]  
    >  The common name in the certificate subject box of the service certificate must be unique in your domain and not match any domain-joined device.  

   For an example deployment of this certificate, see the section **Deploying the service certificate for cloud-based distribution points** in the topic [Step-by-step example deployment of the PKI certificates for System Center Configuration Manager: Windows Server 2008 Certification Authority](/sccm/core/plan-design/network/example-deployment-of-pki-certificates).  

##  <a name="bkmk_Tasks"></a> Common management tasks for cloud-based distribution points  

-   **Site server to cloud-based distribution point communication**: When you install a cloud-based distribution point, you must assign one primary site to manage the transfer of content to the cloud service. This action is equivalent to installing the distribution point site system role on a specific site.  

-   **Client to cloud-based distribution point communication**: When a device or user of a device is configured with the client setting that enables the use of a cloud-based distribution point, the device can receive the cloud-based distribution point as a valid content location:  

    -   The cloud-based distribution point is considered a remote distribution point when a client evaluates available content locations.  

    -   Clients on the intranet only use cloud-based distribution points as a fallback option if on-premises distribution points are not available.  

    Even though you install cloud-based distribution points in specific regions of Azure, clients that use cloud-based distribution points are not aware of the Azure regions and non-deterministically select a cloud-based-distribution point.

This means that if you install cloud-based distribution points in multiple regions, and a client receives multiple cloud-based distribution points as content locations, the client might not use a cloud-based distribution point from the same Azure region as the client.  

Clients that use cloud-based distribution points use the following sequence for content location requests:  

1.  A client that is configured to use cloud-based distribution points always attempts to obtain content from a preferred distribution point first.  

2.  When a preferred distribution point is not available, the client uses a remote distribution point, if the deployment supports this option and if a remote distribution point is available.  

3.  When a preferred distribution point or remote distribution point is not available, the client can then fall back to obtain the content from a cloud-based distribution point.  



  When a client uses a cloud-based distribution point as a content location, the client authenticates itself to the cloud-based distribution point by using a Configuration Manager access token. If the client trusts the Configuration Manager cloud-based distribution point certificate, the client can then download the requested content.  

-   **Monitor cloud-based distribution points**: You can monitor the content that you deploy to each cloud-based distribution point, and you can monitor the cloud service that hosts the distribution point.  

    -   **Content**: You monitor content that you deploy to a cloud-based distribution point the same way you do when you deploy content to on-premises distribution points.  

    -   **Cloud service**: Configuration Manager periodically checks the Azure service and raises an alert if the service is not active, or if there are subscription or certificate issues. You can also view details about the distribution point in the **Cloud Distribution Points** node under **Cloud Services** in the **Administration** workspace of the Configuration Manager console. From this location, you view high-level information about the distribution point. You can also select a distribution point and then edit its properties.  

    When you edit the properties of a cloud-based distribution point, you can:  

    -   Adjust the data thresholds for storage and alerts.  

    -   Manage content as you would for an on-premises distribution point.  

    Finally, for each cloud-based distribution point, you can view, but not edit, the subscription ID, service name, and other related details that are specified when the cloud-based distribution is installed.  

-   **Backup and recovery for cloud-based distribution points**: When you use a cloud-based distribution point in your hierarchy, use the following information to help you plan for backup or recovery of the distribution point:  

    -   When you use the predefined **Backup Site Server** maintenance task, Configuration Manager automatically includes the configurations for the cloud-based distribution point.  

    -   It is a best practice to back up and save a copy of both the management certificate and service certificate that are in use with a cloud-based distribution point. If you restore the Configuration Manager primary site that manages the cloud-based distribution point to a different computer, you must re-import the certificates before you can continue to use them.  

-   **Uninstall a cloud-based distribution point** : To uninstall a cloud-based distribution point, select the distribution point in the Configuration Manager console, and then select **Delete**.  

    When you delete a cloud-based distribution point from a hierarchy, Configuration Manager removes the content from the cloud service in Azure.  
