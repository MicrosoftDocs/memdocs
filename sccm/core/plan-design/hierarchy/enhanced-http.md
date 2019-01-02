---
title: Enhanced HTTP
titleSuffix: Configuration Manager
description: Use modern authentication to secure client communication without the need for PKI certificates.
ms.date: 10/29/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 4deac022-e397-4f1f-bc0a-cea6c6c6368d
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Enhanced HTTP

*Applies to: System Center Configuration Manager (Current Branch)*

<!--1356889,1358460-->

> [!Tip]  
> This feature was first introduced in version 1806 as a [pre-release feature](/sccm/core/servers/manage/pre-release-features). Beginning with version 1810, this feature is no longer a pre-release feature.  


Microsoft recommends using HTTPS communication for all Configuration Manager communication paths, but it's challenging for some customers due to the overhead of managing PKI certificates. The introduction of Azure Active Directory (Azure AD) integration reduces some but not all of the certificate requirements. 

Configuration Manager version 1806 includes improvements to how clients communicate with site systems. There are two primary goals for these improvements:  

- You can secure sensitive client communication without the need for PKI server authentication certificates.  

- Clients can securely access content from distribution points without the need for a network access account, client PKI certificate, and Windows authentication.  

> [!Note]  
> PKI certificates are still a valid option for customers with the following requirements:   
> - All client communication is over HTTPS  
> - Advanced control of the signing infrastructure  


## <a name="bkmk_scenario"></a> Scenarios

The following scenarios benefit from these improvements:  


### <a name="bkmk_scenario1"></a> Scenario 1: Client to management point
<!--1356889-->

[Azure AD-joined devices](https://docs.microsoft.com/azure/active-directory/device-management-introduction#azure-ad-joined-devices) can communicate with a management point configured for HTTP. The site server generates a certificate for the management point allowing it to communicate via a secure channel.   

> [!Note]  
> This behavior is changed from Configuration Manager current branch version 1802, which requires an HTTPS-enabled management point for Azure AD-joined clients communicating through a cloud management gateway. For more information, see [Enable management point for HTTPS](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_mphttps).  


### <a name="bkmk_scenario2"></a> Scenario 2: Client to distribution point
<!--1358228-->

A workgroup or Azure AD-joined client can authenticate and download content over a secure channel from a distribution point configured for HTTP. These types of devices can also authenticate and download content from a distribution point configured for HTTPS without requiring a PKI certificate on the client. It's challenging to add a client authentication certificate to a workgroup or Azure AD-joined client.

This behavior includes OS deployment scenarios with a task sequence running from boot media, PXE, or Software Center. For more information, see [Network access account](/sccm/core/plan-design/hierarchy/accounts#network-access-account).<!--1358278-->


### <a name="bkmk_scenario3"></a> Scenario 3: Azure AD device identity 
<!--1358460-->

An Azure AD-joined or [hybrid Azure AD device](https://docs.microsoft.com/azure/active-directory/device-management-introduction#hybrid-azure-ad-joined-devices) without an Azure AD user signed in can securely communicate with its assigned site. The cloud-based device identity is now sufficient to authenticate with the CMG and management point for device-centric scenarios. (A user token is still required for user-centric scenarios.)  


## Prerequisites  

- A management point configured for HTTP client connections. Set this option on the **General** tab of the site system role properties.  

- A distribution point configured for HTTP client connections. Set this option on the **General** tab of the site system role properties. Don't enable the option to **Allow clients to connect anonymously**.  

- Onboard the site to Azure AD for cloud management.  

    - If you've already met this prerequisite for your site, you need to update the Azure AD application. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select **Azure Active Directory Tenants**. Select the Azure AD tenant, select the web application in the **Applications** pane, and then select **Update application setting** in the ribbon.  

- *[Scenario 3](#bkmk_scenario3) only*: A client running Windows 10 version 1803 or higher and joined to Azure AD. 



## Configure the site

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the  **Sites** node. Select the site and choose **Properties** in the ribbon.  

2. Switch to the **Client Computer Communication** tab. Select the option for **HTTPS or HTTP** and then enable the option to **Use Configuration Manager-generated certificates for HTTP site systems**.  

> [!Tip]
> Wait up to 30 minutes for the management point to receive and configure the new certificate from the site.

You can see these certificates in the Configuration Manager console. Go to the **Administration** workspace, expand **Security**, and select the **Certificates** node. Look for the **SMS Issuing** root certificate, as well as the site server role certificates issued by the SMS Issuing root.

For more information on how the client communicates with the management point and distribution point with this configuration, see [Communications from clients to site systems and services](/sccm/core/plan-design/hierarchy/communications-between-endpoints#Planning_Client_to_Site_System).



## See also
- [Plan for security](/sccm/core/plan-design/security/plan-for-security)  

- [Security and privacy for Configuration Manager clients](/sccm/core/clients/deploy/plan/security-and-privacy-for-clients)  

- [Configure security](/sccm/core/plan-design/security/configure-security)  

- [Communication between endpoints](/sccm/core/plan-design/hierarchy/communications-between-endpoints)  

