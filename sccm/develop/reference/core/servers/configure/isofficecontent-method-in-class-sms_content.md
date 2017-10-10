---
title: "IsOfficeContent Method"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 037e759f-b8ea-4f6b-b33d-b59056efc02fsearchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# IsOfficeContent Method in Class SMS_Content
The `IsOfficeContent` Windows Management Instrumentation (WMI) class method, in Configuration Manager, specifies whether content is Microsoft Office 365 content.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
Boolean IsOfficeContent (  
    UInt32 ContentId  
);  

```  

#### Parameters  
 `ContentId`  
 Data type: `UInt32`  

 Qualifiers: [in]  

 Content ID.  

## Return Values  
 `True` if content is Microsoft Office 365 content; otherwise, `False`.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Content Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_content-server-wmi-class.md)   
 [Configuration Manager Content Server WMI Classes](../../../../../develop/reference/core/servers/configure/content-server-wmi-classes.md)
