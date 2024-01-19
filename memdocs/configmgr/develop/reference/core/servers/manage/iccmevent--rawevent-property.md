---
title: "ICCMEvent::RawEvent Property"
titleSuffix: Configuration Manager
description: "In Configuration Manager, ICcmEvent::RawEvent is a read-only property that indicates information to add to a raw event."
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 4e952869-2e3f-45c8-a259-12898f5373f0
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# ICCMEvent::RawEvent Property
`ICcmEvent::RawEvent` is a read-only property in Configuration Manager that indicates information to add to a raw event.  

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
 The property returns an `HRESULT` code. Possible values include, but aren't limited to, the following one:  

 S_OK  
 The method succeeded.  

## Remarks  
 Use of this property permits information that can't be added through the [SetProperty method](../../../../../develop/reference/core/servers/manage/iccmevent--setproperty-method.md) method to be added to custom events.  

 This property is recommended only for advanced users who need to add information to custom events that can't be accomplished through the [SetProperty method](../../../../../develop/reference/core/servers/manage/iccmevent--setproperty-method.md) method. It isn't supported in VBScript.  

## Requirements  
 Smscore.dll.  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [SMSEvent Class (client)](../../../../../develop/reference/core/servers/manage/smsevent-class.md)
