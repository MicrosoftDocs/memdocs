---
title: "Unique Identifier Value for a Resource"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 1fe1e9f1-daed-4df8-bf32-df7258d9a3fe
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# About the Unique Identifier Value for a Resource
In System Center Configuration Manager, the Configuration Manager unique identifier property for a new resource class is optional. If you report inventory data for the resource, you must include this property. The Configuration Manager unique identifier value must be unique — it relates your resource discovery data to your inventory data (SMS_G_xxx). Typically, hardware resources use a GUID to uniquely identify individual resources.  

 The format of the Configuration Manager unique identifier value is as follows.  

```  
<ID Type>:<ID Value>  
```  

 For example, Configuration Manager uses a GUID to identify Configuration Manager clients.  

```  
GUID:4976DCD4-CAAE-11D2-8E00-00104BCC3648  
```  

 You can use any \<ID Type> and \<ID Value> values to identify a new resource. However, when discovering data for an existing resource type, you should follow the convention that is used by that resource type.  

## See Also  
 [System Center Configuration Manager Software Development Kit](../../../../develop/core/misc/system-center-configuration-manager-sdk.md)   
 [Configuration Manager Discovery](../../../../develop/core/servers/configure/discovery.md)   
 [Extending Discovery and Inventory](../../../../develop/core/servers/configure/extending-resource-discovery.md)   
 [How to Get the Unique Identifier Value for a Client](../../../../develop/core/servers/configure/how-to-get-the-unique-identifier-value-for-a-client.md)   
 [Configuration Manager Resource Management Server WMI Classes](../../../../develop/reference/core/clients/manage/configuration-manager-resource-management-server-wmi-classes.md)
