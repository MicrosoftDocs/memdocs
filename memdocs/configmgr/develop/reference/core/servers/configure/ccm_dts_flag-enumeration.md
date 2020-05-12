---
title: "CCM_DTS_FLAG Enumeration"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 90f20778-f069-4af1-bcfd-c27230818a77
author: aczechowski
ms.author: aaroncz
manager: dougeby


---
# CCM_DTS_FLAG Enumeration
The **CCM_DTS_FLAG** enumeration indicates special options on download jobs.  

## Syntax  

```  
typedef enum  
{  
    CCM_DTS_FLAG_SINGLEFILE             = 0x00000001,   
    CCM_DTS_FLAG_DIRECTORY              = 0x00000002,   
    CCM_DTS_FLAG_NOTIFYPROGRESS         = 0x00000004,   
    CCM_DTS_FLAG_INSECURETRANSPORT      = 0x00000008,   
    CCM_DTS_FLAG_TOPLEVELFILESONLY      = 0x00000010,   
    CCM_DTS_FLAG_SENDAUTHHEADERS        = 0x00000020,   
    CCM_DTS_FLAG_SENDAUTHHEADERS_MIXED  = 0x00000040,   
    CCM_DTS_FLAG_USEINPUTMANIFEST       = 0x00000080,   
    CCM_DTS_FLAG_SKIPHOSTCHANGEHANDLING = 0x00000100   
}  
CCM_DTS_FLAG;  

```  

## Members  

|||  
|-|-|  
|CCM_DTS_FLAG_SINGLEFILE|Reserved.|  
|CCM_DTS_FLAG_DIRECTORY|Indicates that `szRemotePath` is a directory and that all of its contents should be downloaded. This should always be specified in the case of alternate providers.|  
|CCM_DTS_FLAG_NOTIFYPROGRESS|This indicates that progress notifications are required. Even if this flag is not specified, success and error notifications are still required.|  
|CCM_DTS_FLAG_INSECURETRANSPORT|Reserved.|  
|CCM_DTS_FLAG_TOPLEVELFILESONLY|Reserved.|  
|CCM_DTS_FLAG_SENDAUTHHEADERS|Reserved.|  
|CCM_DTS_FLAG_SENDAUTHHEADERS_MIXED|Reserved.|  
|CCM_DTS_FLAG_USEINPUTMANIFEST|Reserved.|  
|CCM_DTS_FLAG_SKIPHOSTCHANGEHANDLING|Reserved.|  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  
