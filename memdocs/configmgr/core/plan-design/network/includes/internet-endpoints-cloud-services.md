---
author: aczechowski
ms.author: aaroncz
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: include
ms.date: 09/23/2020
---

This section covers the following features:

- Cloud management gateway (CMG)
- Cloud distribution point (CDP)
- Azure Active Directory (Azure AD) integration
- Azure AD-based discovery

The following sections list the endpoints by role. Some endpoints refer to a service by `<name>`, which is the cloud service name of the CMG or CDP. For example, if your CMG is `GraniteFalls.CloudApp.Net`, then the actual storage endpoint is `GraniteFalls.blob.core.windows.net`.<!-- SCCMDocs#2288 -->

> [!TIP]
> To clarify some terminology:
>
> - CMG _service name_: The common name (CN) of the CMG server authentication certificate. Clients and the CMG connection point site system role communicate with this service name. For example, `GraniteFalls.contoso.com` or `GraniteFalls.cloudapp.net`.
>
> - CMG _deployment name_: The first part of the service name plus the Azure location for the cloud service deployment. For example, `GraniteFalls.cloudapp.net`. The cloud service manager component of the service connection point uses this name when it deploys the CMG in Azure. The deployment name is always in an Azure domain.

### Service connection point for cloud services

For Configuration Manager to deploy the CMG or CDP services in Azure, the service connection point needs access to:

- Specific Azure endpoints, which are different per environment depending upon the configuration. Configuration Manager stores these endpoints in the site database. Query the **AzureEnvironments** table in SQL Server for the list of Azure endpoints.

- Azure services:
  - `management.azure.com` (Azure public cloud)
  - `management.usgovcloudapi.net` (Azure US Government cloud)

- For Azure AD user discovery: Microsoft Graph endpoint `https://graph.microsoft.com/`

### CMG connection point

The CMG connection point needs access to the following service endpoints:

- Deployment name (for CMG or CDP):
  - `<name>.cloudapp.net` (Azure public cloud)
  - `<name>.usgovcloudapp.net` (Azure US Government cloud)

- Storage endpoint (for content-enabled CMG or CDP): <!-- does CMGCP need to access this? -->
  - `<name>.blob.core.windows.net` (Azure public cloud)
  - `<name>.blob.core.usgovcloudapi.net` (Azure US Government cloud)

The CMG connection point site system supports using a web proxy. For more information on configuring this role for a proxy, see [Proxy server support](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server).

The CMG connection point only needs to connect to the CMG service endpoints. It doesn't need access to other Azure endpoints.

### Configuration Manager client

- Deployment name (for CMG or CDP):
  - `<name>.cloudapp.net` (Azure public cloud)
  - `<name>.usgovcloudapp.net` (Azure US Government cloud)

- Storage endpoint (for content-enabled CMG or CDP):
  - `<name>.blob.core.windows.net` (Azure public cloud)
  - `<name>.blob.core.usgovcloudapi.net` (Azure US Government cloud)

- For Azure AD token retrieval, the Azure AD endpoint:
  - `login.microsoftonline.com` (Azure public cloud)
  - `login.microsoftonline.us` (Azure US Government cloud)

### Configuration Manager console for cloud services

- For Azure AD token retrieval, the Azure AD endpoint:

  - Azure public cloud
    - `login.microsoftonline.com`
    - `aadcdn.msauth.net`<!-- MEMDocs#351 -->
    - `aadcdn.msftauth.net`

  - Azure US Government cloud
    - `login.microsoftonline.us`
