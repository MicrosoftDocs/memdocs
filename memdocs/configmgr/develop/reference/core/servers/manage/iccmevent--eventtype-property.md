---
title: "ICCMEvent::EventType Property"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 049f86f3-634e-46ca-b162-7fa5b5ac8d14
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# ICCMEvent::EventType Property
`ICcmEvent::EventType` is a read/write property, in Configuration Manager, that indicates the type of Windows Management Instrumentation (WMI) event that is being raised.  

## Syntax  

```  
[C++]  
HRESULT ICcmEvent::EventType([out, retval] BSTR* sEventType);  

HRESULT ICcmEvent::EventType([in] BSTR sEventType);  
```  

#### Parameters  
 `sEventType`  
 Data type: `BSTR`  

 Qualifiers: [in, out, retval]  

 On input, the value to set for the event type. On output, this parameter points to the retrieved event type.  

## Return Values  
 The property returns an `HRESULT` code. Possible values include, but are not limited to, the following:  

 S_OK  
 The method succeeded.  

## Remarks  
 This property must correspond to an `ICcmEvent`-derived class registered in the root\ccm\events namespace.  

## Requirements  
 Smscore.dll.  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [SMSEvent Class (client)](../../../../../develop/reference/core/servers/manage/smsevent-class.md)
