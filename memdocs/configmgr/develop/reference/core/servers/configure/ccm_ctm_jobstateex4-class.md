---
description: Learn how to represent the state information for a single Content Transfer Manager job using CCM_CTM_JobStateEx4 class.
title: CCM_CTM_JobStateEx4 Class
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 22bbbfab-5613-4b83-9527-ef956aa485bc
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# CCM_CTM_JobStateEx4 Class
The **CCM_CTM_JobStateEx4** class, in Configuration Manager, represents the state information for a single Content Transfer Manager job.  

## Syntax  

```  
class CCM_CTM_JobStateEx4  
{  
    string ProviderSettingsFromRequest;   
    uint32 CurrentProviderPriority;   
    string CurrentProviderLogicalName;   
    string CurrentProviderCLSID;   
    string CurrentProviderGlobalSettings;   
    string CurrentProviderSettingsFromRequest;   
};  

```  

#### Parameters  
 `ProviderSettingsFromRequest`  
 Data type: String  

 Qualifiers: [in]  

 XML describing the allowed alternate providers and provider-specific settings.  

 `CurrentProviderPriority`  
 Data type: UInt32  

 Qualifiers: [in]  

 Priority in the face of multiple alternate provider choices. For future use.  

 `CurrentProviderLogicalName`  
 Data type: String  

 Qualifiers: [in]  

 The name of the current provider. This value must match the value specified to the SMS provider.   

 `CurrentProviderCLSID`  
 Data type: String  

 Qualifiers: [in]  

 The COM class ID corresponding to the current provider.   

 `CurrentProviderGlobalSettings`  
 Data type: String  

 Qualifiers: [in]  

 Provider-specific data for the current provider.  

 `CurrentProviderSettingsFromRequest`  
 Data type: String  

 Qualifiers: [in]  

 Provider-specific settings for the current provider.

## Return Values  
 None.  

## Remarks  
 There will be an instance of this class for each job started by the Content Transfer Manager.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  
