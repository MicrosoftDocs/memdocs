---
title: Enhanced HTTP
titleSuffix: Configuration Manager
description: Use modern authentication to secure client communication without the need for PKI certificates.
ms.date: 03/28/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 4deac022-e397-4f1f-bc0a-cea6c6c6368d
author: aczechowski
ms.author: aaroncz
manager: dougeby


---

# Enhanced HTTP

*Applies to: Configuration Manager (current branch)*

<!--1356889,1358460-->

> [!Tip]  
> This feature was first introduced in version 1806 as a [pre-release feature](../../servers/manage/pre-release-features.md). Beginning with version 1810, this feature is no longer a pre-release feature.  

Microsoft recommends using HTTPS communication for all Configuration Manager communication paths, but it's challenging for some customers due to the overhead of managing PKI certificates.

Configuration Manager version 1806 includes improvements to how clients communicate with site systems. There are two primary goals for these improvements:  

- You can secure sensitive client communication without the need for PKI server authentication certificates.  

- Clients can securely access content from distribution points without the need for a network access account, client PKI certificate, and Windows authentication.  

All other client communication is over HTTP. Enhanced HTTP isn't the same as enabling HTTPS for client communication or a site system.<!-- SCCMDocs issue #1212 -->

> [!Note]  
> PKI certificates are still a valid option for customers with the following requirements:  
>
> - All client communication is over HTTPS  
> - Advanced control of the signing infrastructure
>
> Also, If you're already using PKI, the PKI cert bound in IIS will be used even if enhanced HTTP is turned on.



## <a name="bkmk_scenario"></a> Scenarios

The following scenarios benefit from these improvements:  

### <a name="bkmk_scenario1"></a> Scenario 1: Client to management point

<!--1356889-->
[Azure Active Directory (Azure AD)-joined devices](/azure/active-directory/devices/concept-azure-ad-join) can communicate with a management point configured for HTTP. The site server generates a certificate for the management point allowing it to communicate via a secure channel.

> [!Note]  
> This behavior is changed from Configuration Manager current branch version 1802, which requires an HTTPS-enabled management point for Azure AD-joined clients communicating through a cloud management gateway. For more information, see [Enable management point for HTTPS](../../clients/manage/cmg/certificates-for-cloud-management-gateway.md#bkmk_mphttps).  

### <a name="bkmk_scenario2"></a> Scenario 2: Client to distribution point

<!--1358228-->
A workgroup or Azure AD-joined client can authenticate and download content over a secure channel from a distribution point configured for HTTP. These types of devices can also authenticate and download content from a distribution point configured for HTTPS without requiring a PKI certificate on the client. It's challenging to add a client authentication certificate to a workgroup or Azure AD-joined client.

This behavior includes OS deployment scenarios with a task sequence running from boot media, PXE, or Software Center. For more information, see [Network access account](accounts.md#network-access-account).<!--1358278-->

### <a name="bkmk_scenario3"></a> Scenario 3: Azure AD device identity

<!--1358460-->
An Azure AD-joined or [hybrid Azure AD device](/azure/active-directory/devices/concept-azure-ad-join-hybrid) without an Azure AD user signed in can securely communicate with its assigned site. The cloud-based device identity is now sufficient to authenticate with the CMG and management point for device-centric scenarios. (A user token is still required for user-centric scenarios.)  


## Features

The following Configuration Manager features support or require enhanced HTTP:

- [Cloud management gateway](../../clients/manage/cmg/plan-cloud-management-gateway.md)
- [OS deployment without a network access account](../../../osd/plan-design/planning-considerations-for-automating-tasks.md#enhanced-http)
- [Enable co-management for new internet-based Windows 10 devices](../../../comanage/tutorial-co-manage-new-devices.md)
- [App approvals via email](../../../apps/deploy-use/app-approval.md#bkmk_email-approve)
- [Administration service](../../../develop/adminservice/overview.md)
- [View recently connected consoles](../../servers/manage/admin-console.md#bkmk_viewconnected)

> [!Note]  
> The software update point and related scenarios have always supported secure HTTP traffic with clients as well as the cloud management gateway. It uses a mechanism with the management point that's different from certificate- or token-based authentication.<!-- SCCMDocs issue #1148 -->


## Prerequisites  

- A management point configured for HTTP client connections. Set this option on the **General** tab of the management point role properties.  

- A distribution point configured for HTTP client connections. Set this option on the **Communication** tab of the distribution point role properties. Don't enable the option to **Allow clients to connect anonymously**.  

- Onboard the site to Azure AD for cloud management.  

    - If you've already met this prerequisite for your site, you need to update the Azure AD application. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select **Azure Active Directory Tenants**. Select the Azure AD tenant, select the web application in the **Applications** pane, and then select **Update application setting** in the ribbon.  

- *For [Scenario 3](#bkmk_scenario3) only*: A client running Windows 10 version 1803 or later, and joined to Azure AD. The client requires this configuration for Azure AD device authentication.<!-- SCCMDocs issue 1126 -->


## Configure the site

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the  **Sites** node. Select the site and choose **Properties** in the ribbon.  

2. Switch to the **Client Computer Communication** tab.

    > [!Note]
    > Starting in version 1906, this tab is called **Communication Security**.<!-- SCCMDocs#1645 -->  

    Select the option for **HTTPS or HTTP**. Then enable the option to **Use Configuration Manager-generated certificates for HTTP site systems**.

> [!Tip]
> Wait up to 30 minutes for the management point to receive and configure the new certificate from the site.

<!--3798957-->
Starting in version 1902, you can also enable enhanced HTTP for the central administration site. Use this same process, and open the properties of the central administration site. This action only enables enhanced HTTP for the SMS Provider roles at the central administration site. It's not a global setting that applies to all sites in the hierarchy.

You can see these certificates in the Configuration Manager console. Go to the **Administration** workspace, expand **Security**, and select the **Certificates** node. Look for the **SMS Issuing** root certificate, as well as the site server role certificates issued by the SMS Issuing root.

For more information on how the client communicates with the management point and distribution point with this configuration, see [Communications from clients to site systems and services](communications-between-endpoints.md#Planning_Client_to_Site_System).


## See also

- [Plan for security](../security/plan-for-security.md)  

- [Security and privacy for Configuration Manager clients](../../clients/deploy/plan/security-and-privacy-for-clients.md)  

- [Configure security](../security/configure-security.md)  

- [Communication between endpoints](communications-between-endpoints.md)  
