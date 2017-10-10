---
title: "SMS_ResourceMap Class"
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
ms.assetid: 8040e549-3866-4ee9-a412-e5cd1e6ffa64searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_ResourceMap Server WMI Class
The `SMS_ResourceMap` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in System Center Configuration Manager, that maps a resource type to its resource class name and display name.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_ResourceMap : SMS_BaseClass  
{  
     String DisplayName;  
     String ResourceClassName;  
     UInt32 ResourceType;  
};  
```  

## Methods  
 The following table lists the methods in `SMS_ResourceMap`.  

|Method|Description|  
|------------|-----------------|  
|[GetClassesWithData Method in Class SMS_ResourceMap](../../../../../develop/reference/core/clients/manage/getclasseswithdata-method-in-class-sms_resourcemap.md)|Gets the names of the classes that have inventory data for a resource.|  
|[Refresh Method in Class SMS_ResourceMap](../../../../../develop/reference/core/clients/manage/refresh-method-in-class-sms_resourcemap.md)|Updates the resource and inventory class definitions.|  

## Properties  
 `DisplayName`  
 Data type: **String**  

 Access type: Read/Write  

 Qualifiers: None  

 Name displayed in the System Center Configuration Manager console to represent the resource class name. For a list of the default resource display names, see the `ResourceType` property.  

 `ResourceClassName`  
 Data type: **String**  

 Access type: Read/Write  

 Qualifiers: None  

 Class name of the resource. For a list of the default resource class names, see the `ResourceType` property.  

 `ResourceType`  
 Data type: **UInt32**  

 Access type: Read/Write  

 Qualifiers: [key]  

 Type of resources on the site. Possible values are:  

|Resource type|Display name|Class|  
|-------------------|------------------|-----------|  
|3|User Group|`SMS_R_UserGroup`|  
|4|User|`SMS_R_User`|  
|5|System|`SMS_R_System`|  
|See the following Note|IP Network|`SMS_R_IPNetwork`|  

> [!NOTE]
>  The IP network resource type might not have a resource type value of 6. Its value depends on when Network Discovery was initiated relative to the discovery of new architectures by the Discovery Data Manager. The resource type value is 6 if the Data Discovery Manager discovered a new architecture before network discovery was initiated.  

## Remarks  
 Class qualifiers for this class include:  

-   Read (read-only)  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Resource Management Server WMI Classes](../../../../../develop/reference/core/clients/manage/configuration-manager-resource-management-server-wmi-classes.md)
