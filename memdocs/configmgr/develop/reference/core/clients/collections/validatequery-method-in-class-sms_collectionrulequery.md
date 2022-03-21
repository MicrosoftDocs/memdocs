---
title: "ValidateQuery Method"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: f0bb91d3-4f35-4316-ad64-83efe5e94f07
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# ValidateQuery Method in Class SMS_CollectionRuleQuery
The `ValidateQuery` Windows Management Instrumentation (WMI) class method, in Configuration Manager, verifies that the query collection rule is a valid WQL or Extended WQL statement.  

 The following syntax is simplified from Managed Object Format (MOF) code and defines the method.  

## Syntax  

```  
Boolean ValidateQuery(  
     String WQLQuery  
);  
```  

#### Parameters  
 `WQLQuery`  
 Data type: `String`  

 Qualifiers: [in]  

 Query statement to validate.  

## Return Values  
 A `Boolean` data type that is `true` if the query is validated.  

## Remarks  
 Your application calls this method before adding a query rule to a collection. An invalid query rule results in no members being added to the collection for that query. This can be misleading and hard to debug.  

 In addition to being syntactically correct, the query rule must specify resource class names in the FROM clause. For example, the FROM clause must specify [SMS_R_System Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_r_system-server-wmi-class.md), [SMS_R_User Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_r_user-server-wmi-class.md), [SMS_R_UserGroup Server WMI Class](../../../../../develop/reference/core/clients/manage/sms_r_usergroup-server-wmi-class.md), or a user-defined resource class name.  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  
