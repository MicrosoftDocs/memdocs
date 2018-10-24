---
title: Enhanced HTTP
titleSuffix: Configuration Manager
description: Use modern authentication to secure client communication without the need for PKI certificates.
ms.date: 10/24/2018
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

> [!Note]  
> In this version of Configuration Manager, Enhanced HTTP is a pre-release feature. To enable it, see [Pre-release features](/sccm/core/servers/manage/pre-release-features).  

Microsoft recommends using HTTPS communication for all Configuration Manager communication paths, but it's challenging for some customers due to the overhead of managing PKI certificates. The introduction of Azure Active Directory (Azure AD) integration reduces some but not all of the certificate requirements. 

Configuration Manager version 1806 includes improvements to how clients communicate with site systems. There are two primary goals for these improvements:  

- You can secure client communication without the need for PKI server authentication certificates.  

- Clients can securely access content from distribution points without the need for a network access account.  

> [!Note]  
> PKI certificates are still a valid option for customers that want to use it.  


## <a name="bkmk_scenario"></a> Scenarios

The following scenarios benefit from these improvements:  


### <a name="bkmk_scenario1"></a> Scenario 1: Client to management point
<!--1356889-->

[Azure AD-joined devices](https://docs.microsoft.com/azure/active-directory/device-management-introduction#azure-ad-joined-devices) can communicate through a cloud management gateway (CMG) with a management point configured for HTTP. The site server generates a certificate for the management point allowing it to communicate via a secure channel.   

> [!Note]  
> This behavior is changed from Configuration Manager current branch version 1802, which requires an HTTPS-enabled management point for this scenario. For more information, see [Enable management point for HTTPS](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_mphttps).  


### <a name="bkmk_scenario2"></a> Scenario 2: Client to distribution point
<!--1358228-->

A workgroup or Azure AD-joined client can download content over a secure channel from a distribution point configured for HTTP.   


### <a name="bkmk_scenario3"></a> Scenario 3 Azure AD device identity 
<!--1358460-->

An Azure AD-joined or [hybrid Azure AD device](https://docs.microsoft.com/azure/active-directory/device-management-introduction#hybrid-azure-ad-joined-devices) without an Azure AD user signed in can securely communicate with its assigned site. The cloud-based device identity is now sufficient to authenticate with the CMG and management point.  


## Prerequisites  

- A management point configured for HTTP client connections. Set this option on the **General** tab of the site system role properties.  

- A distribution point configured for HTTP client connections. Set this option on the **General** tab of the site system role properties. Don't enable the option to **Allow clients to connect anonymously**.  

- A cloud management gateway.  

- Onboard the site to Azure AD for cloud management.  

    - If you've already met this prerequisite for your site, you need to update the Azure AD application. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select **Azure Active Directory Tenants**. Select the Azure AD tenant, select the web application in the **Applications** pane, and then click **Update application setting** in the ribbon.  

- *[Scenario 3](#bkmk_scenario3) only*: A client running Windows 10 version 1803 and joined to Azure AD. 



## Configure the site

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and selectthe  **Sites** node. Select the site and choose **Properties** in the ribbon.  

2. Switch to the **Client Computer Communication** tab. Select the option for **HTTPS or HTTP** and then enable the option to **Use Configuration Manager-generated certificates for HTTP site systems**.  

> [!Tip]
> Wait up to 30 minutes for the management point to receive and configure the new certificate from the site.

You can see these certificates in the Configuration Manager console. Go to the **Administration** workspace, expand **Security**, and select the **Certificates** node. Look for the **SMS Issuing** root certificate, as well as the site server role certificates issued by the SMS Issuing root.



## Known issues

- The user can't view in Software Center any applications targeted to them as available.  

- OS deployment scenarios still require the network access account.  

- Rapidly and repeatedly enabling and disabling the option to **Use Configuration Manager-generated certificates for HTTP site systems** may cause the certificate to not properly bind to the site system roles. No certificates issued by the "SMS Issuing" certificate are bound to a website in Windows Server Internet Information Services (IIS). To work around this issue, delete all certificates issued by "SMS Issuing" from the **SMS** certificate store in Windows, and then restart the smsexec service.

- Don't configure the site for **HTTPS only** and **Use Configuration Manager-generated certificates for HTTP site systems**.

- When enabling enhanced HTTP, existing clients automatically re-register with the site. This behavior typically occurs during the next policy polling cycle. After you enable enhanced HTTP but before clients re-register, [client notification](/sccm/core/clients/manage/collections/manage-collections#client-notification) actions don't work. The site can't verify the client message signature. This interruption shouldn't be longer than the policy cycle, which is one hour by default. <!--SCCMDocs-pr issue #2823-->


## Technical details

### Client to management point communication

There are two stages when a client communicates with a management point: authentication (transport) and authorization (message). This process varies depending upon the following factors: 
- Site configuration: HTTP, HTTPS, or enhanced HTTP
- Management point configuration: HTTPS only, or allows HTTP or HTTPS
- Device identity
- User identity

Use the following table to understand how this process works:


| MP type  | Client authentication  | Client authorization<br>Device identity  | Client authorization<br>User identity  |
|----------|---------|---------|---------|
| HTTP     | No<br>With Enhanced HTTP, the site verifies the *user* and/or *device* Azure AD token. | Location request: No<br>Client package: No<br>Registration: Yes, using one of the following methods:<br> - Anonymous (manual approval)<br> - Active Directory domain<br> - Azure AD *device* token (Enhanced HTTP) | Yes for user scenarios, using one of the following methods:<br> - Active Directory domain<br> - Azure AD *user* token (Enhanced HTTP) |
| HTTPS    | Yes, using one of the following methods:<br> - PKI certificate<br> - Active Directory domain<br> - Azure AD *user* and/or *device* token (version 1706) | Location request: No<br>Client package: No<br>Registration: Yes, using one of the following methods:<br> - Anonymous (manual approval)<br> - Active Directory domain<br> - PKI certificate<br> - Azure AD *device* token (version 1706) | Yes for user scenarios, using one of the following methods:<br> - Active Directory domain<br> - Azure AD *user* token (version 1706) |

> [!Tip]  
> For more information on the configuration of the management point for different device identity types and with the cloud management gateway, see [Enable management point for HTTPS](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#bkmk_mphttps).  


### Client to distribution point communication

When a client communicates with a distribution point, it only needs to authenticate before downloading the content. Use the following table to understand how this process works:


| DP type  | Client authentication  |
|----------|---------|
|HTTP (anonymous) | No |
|HTTP      | - Windows authentication (network access account)<br> - Content access token (Enhanced HTTP) |
|HTTPS     | - PKI certificate<br> - Windows authentication (network access account)<br> - Content access token (Enhanced HTTP) |



## See also
- [Plan for security](/sccm/core/plan-design/security/plan-for-security)  

- [Security and privacy for Configuration Manager clients](/sccm/core/clients/deploy/plan/security-and-privacy-for-clients)  

- [Configure security](/sccm/core/plan-design/security/configure-security)  

- [Communication between endpoints](/sccm/core/plan-design/hierarchy/communications-between-endpoints)  

