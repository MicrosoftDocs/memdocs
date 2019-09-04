---
title: Internet access requirements
titleSuffix: Configuration Manager
description: Learn about the internet endpoints to allow for full functionality of Configuration Manager features.
ms.date: 08/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: b34fe701-5d05-42be-b965-e3dccc9363ca
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Internet access requirements

Some Configuration Manager features rely on internet connectivity for full functionality. If your organization restricts network communication with the internet using a firewall or proxy device, make sure to allow these endpoints.

<!-- SCCMDocs-pr #3403 -->

## <a name="bkmk_scp"></a> Service connection point

These configurations apply to the computer that hosts the service connection point and any firewalls between that computer and the internet. They both must allow communications through outgoing port **TCP 443** for HTTPS and outgoing port **TCP 80** for HTTP to the below internet locations.

The service connection point supports using a web proxy (with or without authentication) to use these locations. For more information, see [Proxy server support](/sccm/core/plan-design/network/proxy-server-support).

For more information on the service connection point, see [About the service connection point](/sccm/core/servers/deploy/configure/about-the-service-connection-point).

Other Configuration Manager features may require additional endpoints from the service connection point. For more information, see the other sections in this article.

> [!TIP]  
> The service connection point uses the Microsoft Intune service when it connects to `go.microsoft.com` or `manage.microsoft.com`. There's a known issue in which the Intune connector experiences connectivity issues if the Baltimore CyberTrust Root Certificate isn't installed, is expired, or is corrupted on the service connection point. For more information, see [KB 3187516: Service connection point doesn't download updates](https://support.microsoft.com/help/3187516).  

### <a name="bkmk_scp-updates"/> Updates and servicing

For more information on this function, see [Updates and servicing for Configuration Manager](/sccm/core/servers/manage/updates).

> [!Tip]  
> Enable these endpoints for the [management insight](/sccm/core/servers/manage/management-insights) rule, **Connect the site to the Microsoft cloud for Configuration Manager updates**.

- `*.akamaiedge.net`  

- `*.akamaitechnologies.com`  

- `*.manage.microsoft.com`  

- `go.microsoft.com`  

- `*.blob.core.windows.net`  

- `download.microsoft.com`  

- `download.windowsupdate.com`  

- `sccmconnected-a01.cloudapp.net`  

- `configmgrbits.azureedge.net`  

### Microsoft Intune

For more information on this function, see [Hybrid MDM with Configuration Manager and Microsoft Intune](/sccm/mdm/understand/hybrid-mobile-device-management).

- `*manage.microsoft.com`  

- `https://bspmts.mp.microsoft.com/V`  

- `https://login.microsoftonline.com/{TenantID}`  

### Windows 10 servicing

For more information on this function, see [Manage Windows as a service](/sccm/osd/deploy-use/manage-windows-as-a-service).

- `download.microsoft.com`  

- `https://go.microsoft.com/fwlink/?LinkID=619849`  

- `dl.delivery.mp.microsoft.com`  

### Azure services

For more information on this function, see [Configure Azure services for use with Configuration Manager](/sccm/core/servers/deploy/configure/azure-services-wizard).

- `management.azure.com`  


## Co-management

If you enroll Windows 10 devices to Microsoft Intune for co-management, make sure those devices can access the endpoints required by Intune. For more information, see [Network endpoints for Microsoft Intune](https://docs.microsoft.com/intune/intune-endpoints).


## Microsoft Store for Business

If you integrate Configuration Manager with the [Microsoft Store for Business](/sccm/apps/deploy-use/manage-apps-from-the-windows-store-for-business), make sure the service connection point and targeted devices can access the cloud service. For more information, see [Microsoft Store for Business proxy configuration](https://docs.microsoft.com/microsoft-store/prerequisites-microsoft-store-for-business#proxy-configuration).


## <a name="bkmk_cloud"></a> Cloud services

<!-- SCCMDocs-pr #3402 -->

This section covers the following features:

- Cloud management gateway (CMG)
- Cloud distribution point (CDP)
- Azure Active Directory (Azure AD) integration
- Azure AD-based discovery

For CMG/CDP service deployment, the **service connection point** needs access to:

- Specific Azure endpoints are different per environment depending upon the configuration. Configuration Manager stores these endpoints in the site database. Query the **AzureEnvironments** table in SQL Server for the list of Azure endpoints.  

The **CMG connection point** needs access to the following service endpoints:

- ServiceManagementEndpoint: `https://management.core.windows.net/`  

- StorageEndpoint: `blob.core.windows.net` and `table.core.windows.net`

For Azure AD token retrieval by the **Configuration Manager console** and **client**:

- ActiveDirectoryEndpoint `https://login.microsoftonline.com/`  

For Azure AD user discovery, the **service connection point** needs access to:

- Version 1810 and earlier: Azure AD Graph endpoint `https://graph.windows.net/`  

- Version 1902 and later: Microsoft Graph endpoint `https://graph.microsoft.com/`

The cloud management point (CMG) connection point site system supports using a web proxy. For more information on configuring this role for a proxy, see [Proxy server support](proxy-server-support.md#configure-the-proxy-for-a-site-system-server). The CMG connection point only needs to connect to the CMG service endpoints. It doesn't need access to other Azure endpoints.

For more information on the CMG, see [Plan for CMG](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway).


## <a name="bkmk_sum"></a> Software updates

Allow the active software update point to access the following endpoints so that WSUS and Automatic Updates can communicate with the Microsoft Update cloud service:  

- `http://windowsupdate.microsoft.com`  

- `http://*.windowsupdate.microsoft.com`  

- `https://*.windowsupdate.microsoft.com`  

- `http://*.update.microsoft.com`  

- `https://*.update.microsoft.com`  

- `http://*.windowsupdate.com`  

- `http://download.windowsupdate.com`  

- `https://download.microsoft.com`  

- `http://*.download.windowsupdate.com`  

- `http://test.stats.update.microsoft.com`  

- `http://ntservicepack.microsoft.com`  

For more information on software updates, see [Plan for software updates](/sccm/sum/plan-design/plan-for-software-updates).

### Intranet firewall

You might need to add endpoints to a firewall that's between two site systems in the following cases:

- If child sites have a software update point
- If there's a remote active internet-based software update point at a site

#### Software update point on the child site

- `http://<FQDN for software update point on child site>`  

- `https://<FQDN for software update point on child site>`  

- `http://<FQDN for software update point on parent site>`  

- `https://<FQDN for software update point on parent site>`  


## Manage Office 365

If you use Configuration Manager to deploy and update Office 365, allow the following endpoints:

<!-- SCCMDocs#929 -->

- `officecdn.microsoft.com` to synchronize the software update point for Office 365 client updates

- `config.office.com` to create custom configurations for Office 365 deployments


## Configuration Manager console

Computers with the Configuration Manager console require access to the following internet endpoints for specific features:

### In-console feedback

- `http://petrol.office.microsoft.com`

For more information on this feature, see [Product feedback](/sccm/core/understand/find-help#product-feedback).

### Community workspace, Documentation node

- `https://aka.ms`

- `https://raw.githubusercontent.com`

For more information on this console node, see [Using the Configuration Manager console](/sccm/core/servers/manage/admin-console).

<!-- 
Community Hub
when in current branch, get details from SCCMDocs-pr #3403 
 -->

### Monitoring workspace, Site Hierarchy node

If you use the **Geographical View**, allow access to the following endpoint:

- `http://maps.bing.com`


## Desktop Analytics

For more information on the required endpoints for the Desktop Analytics cloud service, see [Enable data sharing](/sccm/desktop-analytics/enable-data-sharing#endpoints).


## Microsoft public IP addresses

For more information on the Microsoft IP address ranges, see [Microsoft Public IP Space](https://www.microsoft.com/download/details.aspx?id=53602). These addresses update regularly. There's no granularity by service, any IP address in these ranges could be used.


## See also

- [Ports used in Configuration Manager](/sccm/core/plan-design/hierarchy/ports)

- [Proxy server support in Configuration Manager](/sccm/core/plan-design/network/proxy-server-support)
