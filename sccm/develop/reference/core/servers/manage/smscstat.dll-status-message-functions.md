---
title: "Smscstat.dll Status Message Functions"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: 1e9d5ad0-558c-4814-8d0a-90fab3b80a06searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# Smscstat.dll Status Message Functions
In System Center Configuration Manager, the functions that are defined by the Smscstat.dll dynamic-link library, report status messages that can be called by using a C interface.  

## Functions  
 Smscstat.dll exports the following functions.  

|Term|Description|  
|----------|-----------------|  
|[AddAttributeToSMSStatusMessage Function](../../../../../develop/reference/core/servers/manage/addattributetosmsstatusmessage-function.md)|Adds a single optional status message attribute ID/value pair to a status message object.|  
|[CreateSMSStatusMessage Function](../../../../../develop/reference/core/servers/manage/createsmsstatusmessage-function.md)|Creates a status message object.|  
|[ReportSMSStatusMessage Function](../../../../../develop/reference/core/servers/manage/reportsmsstatusmessage-function.md)|Submits a status message object to the Configuration Manager status system.|  

## See Also  
 [Status and State Client APIs](../../../../../develop/reference/core/servers/manage/status-client-apis.md)
