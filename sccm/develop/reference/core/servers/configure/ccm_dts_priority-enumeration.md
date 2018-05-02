---
title: "CCM_DTS_PRIORITY Enumeration"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 9d14b0d3-1b61-4b17-9d36-855ddd1a9f82
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# CCM_DTS_PRIORITY Enumeration
The **CCM_DTS_PRIORITY** enumeration indicates the priority of the download.  

## Syntax  

```  
typedef enum  
{  
    CCM_DTS_PRIORITY_FOREGROUND,   
    CCM_DTS_PRIORITY_HIGH,   
    CCM_DTS_PRIORITY_NORMAL,   
    CCM_DTS_PRIORITY_LOW,   
}CCM_DTS_PRIORITY;  

```  

## Members  

|||  
|-|-|  
|CCM_DTS_PRIORITY_FOREGROUND|The highest priority.|  
|CCM_DTS_PRIORITY_HIGH|High priority.|  
|CCM_DTS_PRIORITY_NORMAL|Normal priority.|  
|CCM_DTS_PRIORITY_LOW|Low priority.|  

## Remarks  
 The only strict requirement is that jobs at a lower priority do not block progress of jobs at a higher priority. It is possible in certain NAP-related scenarios that lower priority jobs may be blocked on content needed for remediation that are in higher priority jobs. Providers must respect this.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Configuration Manager Alternate Content Provider](../../../../../develop/reference/core/servers/configure/alternate-content-provider-classes.md)
