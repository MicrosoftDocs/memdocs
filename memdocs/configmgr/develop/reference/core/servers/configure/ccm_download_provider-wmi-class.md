---
title: CCM_Download_Provider Class
titleSuffix: Configuration Manager
description: In Configuration Manager, the CCM_Download_Provider class defines and registers a non-Microsoft download plug-in provider.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 888329e2-1af1-4233-8ea2-90a841356c38
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# CCM_Download_Provider WMI Class
The **CCM_Download_Provider** class, in Configuration Manager, defines and registers a non-Microsoft download plug-in provider.  

## Syntax  

```  
class CCM_Download_Provider: CCM_Policy  
{  
    string  LogicalName;  
    string  CLSID;   
    uint32  Priority;   
    String  GlobalSettings;   
    string  Reserved;   
};  

```  

#### Parameters  
 `LogicalName`  
 Data type: String  

 Qualifiers: [in, RealKey, NotNull: ToInstance ToSubClass]  

 The name of the non-Microsoft provider. This field must match the value specified to the SMS provider.  

 `CLSID`  
 Data type: String  

 Qualifiers: [in, NotNull: ToInstance, ToSubClass]  

 The COM class ID corresponding to the interface implementation.  

 `Priority`  
 Data type: String  

 Qualifiers: [in, NotNull: ToInstance ToSubClass]  

 Priority in the face of multiple alternate provider choices. For future use. Must be nonzero.  

 `GlobalSettings`  
 Data type: String  

 Qualifiers: [in]  

 Provider specific data. Use this for any client-wide configuration for the provider.  

 `Reserved`  
 Data type: String  

 Qualifiers: [in]  

 Reserved for future use.  

## Return Values  
 None.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  
