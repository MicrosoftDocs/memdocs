---
title: "Schema Overview"
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
ms.assetid: 694d88c3-c257-4ef4-a5e6-f732b49ce2f9searchScope: - ConfigMgr SDK
caps.latest.revision: 5
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# Configuration Manager Schema Overview
Configuration Manager uses Windows Management Instrumentation (WMI) to manage its objects. Any managed object, such as a disk drive or a collection of computers, can be represented by an instance of a Configuration Manager class. Configuration Manager also includes classes that represent Configuration Manager features, such as software distribution. Collectively, these Configuration Manager classes are known as the Configuration Manager schema.  

 Configuration Manager uses a Microsoft SQL Server database to store managed object data. Both SQL Server and the WMI API can be used to view and manipulate Configuration Manager managed data. The SMS Provider acts as an intermediary between Configuration Manager site information and WMI by supplying both class and instance data.  

## Server  
 The Configuration Manager classes that represent the Configuration Manager server schema are generally declared in the SMSProv.mof file. This file contains the base classes, static classes, and methods that the SMS Provider supports. Other class definitions, notably those that support inventory, are determined at run time by the SMS Provider. When requested, these class definitions are supplied to WMI. These are called run-time classes. The SMSProv.mof file is located in the \Bin\\<*Platform*>\ directory under the Configuration Manager install directory.  

 For more information about using these Configuration Manager classes by using WMI or managed code, see [Configuration Manager Objects](../../../develop/core/understand/configuration-manager-objects.md)  

 You can also use SQL Views for fast, read-only access to the Configuration Manager schema data. For more information, see [Configuration Manager Schema SQL Views](../../../develop/core/understand/configuration-manager-schema-sql-views.md)  

## Client  
 A number of Managed Object Format (MOF) files represent the client Configuration Manager schema. The client includes schemas that can be used for items such as inventory, policy, and software distribution management.  

 For more information about using client objects with WMI or managed code, see [Configuration Manager Client WMI Programming](../../../develop/core/clients/programming/client-wmi-programming.md).  

## Classes  
 For more information about the classes that Configuration Manager supports, see [Configuration Manager Reference](../../../develop/reference/configuration-manager-reference.md).  

## See Also  
 [About Configuration Manager Schema](../../../develop/core/understand/about-configuration-manager-schema.md)   
 [Configuration Manager Schema View Mapping](../../../develop/core/understand/configuration-manager-schema-view-mapping.md)   
 [Configuration Manager Schema SQL Views](../../../develop/core/understand/configuration-manager-schema-sql-views.md)   
 [Configuration Manager SQL View Security](../../../develop/core/understand/sql-view-security.md)
