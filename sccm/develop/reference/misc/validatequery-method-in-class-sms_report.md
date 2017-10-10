---
title: "ValidateQuery Method"
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
ms.assetid: d4da35eb-a222-43fe-b8bd-992fd32f9b95searchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# ValidateQuery Method in Class SMS_Report
The `ValidateQuery` Windows Management Instrumentation (WMI) class method, in Configuration Manager, verifies that a report query is a valid SQL statement and performs the same level of validation that occurs when the report is saved.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
Boolean ValidateQuery(  
     String SQLQuery,  
     String Parameters[],  
     String SQLErrorMessage  
);  
```  

#### Parameters  
 `SQLQuery`  
 Data type: `String`  

 Qualifiers: [in]  

 Query statement to validate.  

 `Parameters`  
 Data type: `String` Array  

 Qualifiers: [in]  

 Query parameters.  

 `SQLErrorMessage`  
 Data type: `String`  

 Qualifiers: [out]  

 SQL error message.  

## Return Values  
 A `Boolean` data type that is `true` if the query is valid.  

## Remarks  
 This method validates the SQL query that produces the result set of the [SMS_Report Server WMI Class](../../../develop/reference/misc/sms_report-server-wmi-class.md) object. Your application calls this method before running the query.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Report Server WMI Class](../../../develop/reference/misc/sms_report-server-wmi-class.md)
