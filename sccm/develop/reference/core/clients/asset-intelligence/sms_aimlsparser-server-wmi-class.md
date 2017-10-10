---
title: "SMS_AIMLSParser Class"
titleSuffix: "Configuration Manager"
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
ms.assetid: e16df2cd-86c2-450c-998f-a2eaa7325ffbsearchScope: - ConfigMgr SDK
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_AIMLSParser Server WMI Class
The `SMS_AIMLSParser` Windows Management Instrumentation (WMI) class in System Center Configuration Manager imports license data.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_AIMLSParser : SMS_BaseClass ();  
```  

## Methods  
 The following table lists the methods in the `SMS_AIMLSParser` class.  

|Method|Description|  
|------------|-----------------|  
|[GetStatus Method in Class SMS_AIMLSParser](../../../../../develop/reference/core/clients/asset-intelligence/getstatus-method-in-class-sms_aimlsparser.md)|Monitors the status of a previous call to the `Import` method. The returned values of the `Status` parameter are:<br /><br /> 0 - Successful completion|  
|[GetSummary Method in Class SMS_AIMLSParser](../../../../../develop/reference/core/clients/asset-intelligence/getsummary-method-in-class-sms_aimlsparser.md)|Retrieves the counts of imported Microsoft license count and non-Microsoft license count.|  
|[Import Method in Class SMS_AIMLSParser](../../../../../develop/reference/core/clients/asset-intelligence/import-method-in-class-sms_aimlsparser.md)|Imports the MLS statement as specified by the `MLSFilepath` parameter (in UNC format) into the System Center Configuration Manager database.|  

## Properties  
 The `SMS_AIMLSParser`  class does not define any properties.  

## Remarks  
 Class qualifiers for this class include:  

-   DisplayName("AI Hinv Classes List")  

-   Dynamic  

-   Provider("ExtnProv")  

-   Secured  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Asset Intelligence](../../../../../develop/core/clients/asset-intelligence/asset-intelligence.md)
