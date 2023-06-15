---
description: "Learn how to set an event property in Configuration Manager using ICcmEvent::SetProperty method class."
title: "ICCMEvent::SetProperty Method"
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 44f3a746-4a3c-489d-bbfb-78cf0ed31fed
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# ICCMEvent::SetProperty Method
In Configuration Manager, the `ICcmEvent::SetProperty` method sets an event property.  

## Syntax  

```  
[C++]  
HRESULT ICcmEvent::SetProperty  
(  
      BSTR sPropName,   
   VARIANT* vPropValue  
);  
```  

#### Parameters  
 `sPropName`  
 Data type: `BSTR`  

 Qualifiers: [in]  

 Name of the property to set. This must correspond to a property name in the Windows Management Instrumentation (WMI) event class.  

 `vPropValue`  
 Data type: `VARIANT`  

 Qualifiers: [in]  

 Pointer to the new value for the property.  

## Return Values  
 An `HRESULT` code. Possible values include, but are not limited to, the following:  

 S_OK  
 The method succeeded.  

## Remarks  
 Your application must set the [EventType property](../../../../../develop/reference/core/servers/manage/iccmevent--eventtype-property.md) before calling this method.  

## Requirements  
 Smscore.dll.  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [SMSEvent Class (client)](../../../../../develop/reference/core/servers/manage/smsevent-class.md)
