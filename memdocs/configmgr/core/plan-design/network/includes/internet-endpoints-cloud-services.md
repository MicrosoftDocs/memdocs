---
author: banreet
ms.author: banreetkaur
ms.subservice: client-mgt
ms.service: configuration-manager
ms.topic: include
ms.date: 03/15/2022
ms.localizationpriority: medium
---

This section covers the following features:

- Cloud management gateway (CMG)
- Microsoft Entra integration
- Microsoft Entra ID-based discovery
- Cloud distribution point (CDP)

  > [!NOTE]
  > The cloud-based distribution point (CDP) is deprecated. Starting in version 2107, you can't create new CDP instances. To provide content to internet-based devices, enable the CMG to distribute content.<!-- 10247883 -->

The following sections list the endpoints by role. Some endpoints refer to a service by `<prefix>`, which is the prefix name of the CMG. For example, if your CMG is `GraniteFalls.WestUS.CloudApp.Azure.Com`, then the actual storage endpoint is `GraniteFalls.blob.core.windows.net`.<!-- SCCMDocs#2288 -->

> [!TIP]
> To clarify some terminology:
>
> - CMG _service name_: The common name (CN) of the CMG server authentication certificate. Clients and the CMG connection point site system role communicate with this service name. For example, `GraniteFalls.contoso.com` or `GraniteFalls.WestUS.CloudApp.Azure.Com`.
>
> - CMG _deployment name_: The first part of the service name plus the Azure location for the cloud service deployment. The cloud service manager component of the service connection point uses this name when it deploys the CMG in Azure. The deployment name is always in an Azure domain. The Azure location depends upon the deployment method, for example:
>
>   - Virtual machine scale set: `GraniteFalls.WestUS.CloudApp.Azure.Com`
>   - Classic deployment: `GraniteFalls.CloudApp.Net`
>
> This article uses examples with a virtual machine scale set as the recommended deployment method in version 2107 and later. If you use a classic deployment, note the difference as you read this article and configure internet access.

### Service connection point for cloud services

For Configuration Manager to deploy the CMG service in Azure, the service connection point needs access to:

- Specific Azure endpoints, which are different per environment depending upon the configuration. Configuration Manager stores these endpoints in the site database. Query the **AzureEnvironments** table in SQL Server for the list of Azure endpoints.

- Azure services:
  - `management.azure.com` (Azure public cloud)
  - `management.usgovcloudapi.net` (Azure US Government cloud)

- For Microsoft Entra user discovery: Microsoft Graph endpoint `https://graph.microsoft.com/`

### CMG connection point for cloud services

The CMG connection point needs access to the following endpoints:

| Type               | Azure public cloud                     | Azure US Government cloud               |
|--------------------|----------------------------------------|-----------------------------------------|
| _Service_ name     | `<prefix>.<region>.cloudapp.azure.com` | `<prefix>.<region>.usgovcloudapi.net`            |
| Storage endpoint 1 | `<prefix>.blob.core.windows.net`       | `<prefix>.blob.core.usgovcloudapi.net`  |
| Storage endpoint 2 | `<prefix>.table.core.windows.net`      | `<prefix>.table.core.usgovcloudapi.net` |
| Key vault          | `<prefix>.vault.azure.net`             | `<prefix>.vault.usgovcloudapi.net`      |

The CMG connection point site system supports using a web proxy. For more information on configuring this role for a proxy, see [Proxy server support](../proxy-server-support.md#configure-the-proxy-for-a-site-system-server).

The CMG connection point only needs to connect to the CMG service endpoints. It doesn't need access to other Azure endpoints.

### Configuration Manager client for cloud services

Any Configuration Manager client that needs to communicate with a CMG needs access to the following endpoints:

| Type               | Azure public cloud                     | Azure US Government cloud               |
|--------------------|----------------------------------------|-----------------------------------------|
| _Deployment_ name  | `<prefix>.<region>.cloudapp.azure.com` | `<prefix>.usgovcloudapp.net`            |
| Storage endpoint   | `<prefix>.blob.core.windows.net`       | `<prefix>.blob.core.usgovcloudapi.net`  |
| Microsoft Entra endpoint  | `login.microsoftonline.com`            | `login.microsoftonline.us`              |

### Configuration Manager console for cloud services

Any device with the Configuration Manager console needs access to the following endpoints:

| Type | Azure public cloud | Azure US Government cloud |
|--|--|--|
| Microsoft Entra endpoints | `login.microsoftonline.com`<br>`aadcdn.msauth.net`<br>`aadcdn.msftauth.net` | `login.microsoftonline.us` |
