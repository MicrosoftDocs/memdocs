---
author: banreet
ms.author: banreetkaur
ms.subservice: client-mgt
ms.service: configuration-manager
ms.topic: include
ms.date: 01/27/2022
ms.localizationpriority: medium
---

The following table lists the log files that contain information related to the cloud management gateway.

|Log name|Description|Computer with log file|
|--------------|-----------------|----------------------------|  
|CloudMgr.log|Records details about deploying the cloud management gateway service, ongoing service status, and use data associated with the service. To configure the logging level, edit the **Logging level** value in the following registry key: `HKLM\SOFTWARE\ Microsoft\SMS\COMPONENTS\ SMS_CLOUD_ SERVICES_MANAGER`|The *installdir* folder on the primary site server or CAS.|
|CMGSetup.log <sup>[Note 1](#bkmk_note1)</sup>|Records details about the second phase of the cloud management gateway deployment (local deployment in Azure). To configure the logging level, use the setting **Trace level** (**Information** (Default), **Verbose**, **Error**) on the **Azure portal\Cloud services configuration** tab.|The **%approot%\logs** on your Azure server, or the SMS/Logs folder on the site system server|
|CMGService.log <sup>[Note 1](#bkmk_note1)</sup>|Records details about the cloud management gateway service core component in Azure. To configure the logging level, use the setting **Trace level** (**Information** (Default), **Verbose**, **Error**) on the **Azure portal\Cloud services configuration** tab.|The **%approot%\logs** on your Azure server, or the SMS/Logs folder on the site system server|
|SMS_Cloud_ProxyConnector.log|Records details about setting up connections between the cloud management gateway service and the cloud management gateway connection point.|Site system server|
|CMGContentService.log <sup>[Note 1](#bkmk_note1)</sup>|<!--SCCMDocs-pr issue #2822-->When you enable a CMG to also serve content from Azure storage, this log records the details of that service.|The **%approot%\logs** on your Azure server, or the SMS/Logs folder on the site system server|

- For troubleshooting deployments, use **CloudMgr.log** and **CMGSetup.log**
- For troubleshooting service health, use **CMGService.log** and **SMS_Cloud_ProxyConnector.log**.
- For troubleshooting client traffic, use **CMGService.log** and **SMS_Cloud_ProxyConnector.log**.

#### <a name="bkmk_note1"></a> Note 1: Logs synchronized from Azure

These are local Configuration Manager log files that cloud service manager syncs from Azure storage every five minutes. The cloud management gateway pushes logs to Azure storage every five minutes. So the maximum delay is 10 minutes. Verbose switches affect both local and remote logs. The actual file names include the service name and role instance identifier. For example, CMG-*ServiceName*-*RoleInstanceID*-CMGSetup.log. These log files are synced, so you don't need to RDP to the cloud management gateway to obtain them, and that option isn't supported.
