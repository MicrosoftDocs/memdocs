---
title: "CCM_CTM_JobStateEx4 Class"
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
ms.assetid: 22bbbfab-5613-4b83-9527-ef956aa485bcsearchScope: - ConfigMgr SDK
caps.latest.revision: 11
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
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

 Provider specific data for the current provider.  

 `CurrentProviderSettingsFromRequest`  
 Data type: String  

 Qualifiers: [in]  

 CurrentProviderSettingsFromRequest …  

## Return Values  
 None.  

## Remarks  
 There will be an instance of this class for each job started by the Content Transfer Manager.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Configuration Manager Alternate Content Provider](../../../../../develop/reference/core/servers/configure/alternate-content-provider-classes.md)
