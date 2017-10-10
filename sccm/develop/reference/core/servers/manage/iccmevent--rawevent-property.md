---
title: "ICCMEvent::RawEvent Property"
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
ms.assetid: 4e952869-2e3f-45c8-a259-12898f5373f0searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# ICCMEvent::RawEvent Property
`ICcmEvent::RawEvent` is a read-only property, in Configuration Manager, that indicates information to add to a raw event.  

## Syntax  

```  
[C++]  
HRESULT ICcmEvent::RawEvent([out, retval] IUnknown** ppWmiEvent);  
```  

#### Parameters  
 `ppWmiEvent`  
 Data type: `IUnknown`  

 Qualifiers: [out, retval]  

 Pointer to a pointer to the `IUnknown` interface of the internal Windows Management Instrumentation (WMI) event.  

## Return Values  
 The property returns an `HRESULT` code. Possible values include, but are not limited to, the following:  

 S_OK  
 The method succeeded.  

## Remarks  
 Use of this property permits information that cannot be added through the [SetProperty method](../../../../../develop/reference/core/servers/manage/iccmevent--setproperty-method.md) method to be added to custom events.  

 This property is recommended only for advanced users who need to add information to custom events that cannot be accomplished through the [SetProperty method](../../../../../develop/reference/core/servers/manage/iccmevent--setproperty-method.md) method. It is not supported in VBScript.  

## Requirements  
 Smscore.dll.  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [SMSEvent Class (client)](../../../../../develop/reference/core/servers/manage/smsevent-class.md)
