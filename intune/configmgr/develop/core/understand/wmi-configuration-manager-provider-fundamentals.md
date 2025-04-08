---
title: WMI Provider Fundamentals
titleSuffix: Configuration Manager
description: Windows Script Host-based applications and scripts work in Windows Management Instrumentation (WMI) through the WMI Object Model, which defines the programming interface to WMI.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: article
ms.assetid: 04ca780f-dd83-43de-b967-bb9f8a05eb3a
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# WMI Configuration Manager Provider Fundamentals
Windows Script Host-based applications and scripts work in Windows Management Instrumentation (WMI) through the WMI Object Model, which defines the programming interface to WMI. A number of WMI object types are used when manipulating Configuration Manager objects. For more information about the WMI Object Model, see [Windows Management Instrumentation](/windows/win32/wmisdk/wmi-start-page).  

 In simple Configuration Manager scripts, you use the following WMI object types:  

-   `SWbemLocator`  

-   `SWbemServices`  

-   `SWbemObjectSet`  

-   `SWbemObject`  

> [!NOTE]
>  Understanding WMI Query Language (WQL) queries is very important for identifying which Configuration Manager objects you want to read. WQL statements allow you to retrieve Configuration Manager objects that are based on SQL-like queries. For example, the following WQL statement is used to identify all Windows Server 2003 systems:  
>   
>  `SELECT * FROM SMS_FullCollectionMembership WHERE CollectionID='SMS000FS'`  

 For more information about using VBScript and WMI, see [Objects overview](configuration-manager-objects-overview.md).  

## SWbemLocator  
 The [SWbemServices](/windows/win32/wmisdk/swbemservices)object is used to create an authenticated connection to the SMS Provider. You use the [ConnectServer](/windows/win32/wmisdk/swbemlocator-connectserver) method to make the connection to the SMS Provider. This method is particularly useful if you need to pass user credentials to a remote Configuration Manager server during connection. You can also use the Windows Script Host [GetObject](/previous-versions/windows/internet-explorer/ie-developer/windows-scripting/8ywk619w(v=vs.84)) method to create an authenticated connection. The type of object that is returned by `GetObject` depends on the parameters that are passed to it. See [How to Connect to a Configuration Manager Provider Using Managed Code](../../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md) and [How to Connect to a Configuration Manager Provider Using WMI](../../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md) for examples that show how to use either `SWbemLocator` or `GetObject` in your connection script.  

## SWbemServices  
 The [SWbemServices](/windows/win32/wmisdk/swbemservices) object represents an authenticated connection to a SMS Provider, and it is the object that you use to retrieve Configuration Manager objects. You receive an `SWbemServices` object as the return value of the `SWbemLocator` function `ConnectServer` or, alternatively, as the return value when the `GetObject` method is used to connect to the SMS Provider. `SWbemServices` has several methods, but you use only the [Get](/windows/win32/wmisdk/swbemservices-get), [ExecQuery](/windows/win32/wmisdk/swbemservices-execquery), and [InstancesOf](/windows/win32/wmisdk/swbemservices-instancesof) methods for retrieving objects.  

 `Get` returns a single instance of a Configuration Manager object (`SWbemObject`). `ExecQuery` and `InstancesOf` return Configuration Manager objects in a collection (`SWbemObjectSet`) of Configuration Manager objects.  

## SWbemObjectSet  
 The [SWbemObjectSet](/windows/win32/wmisdk/swbemobjectset) object represents a collection of Configuration Manager objects. You can use it to enumerate through the collection and read individual instances of the Configuration Manager object (`SWbemObject`) that you are interested in. You typically get a `SWbemObjectSet` object returned to you from the `SWbemServices` retrieval functions.  

## SWbemObject  
 The [SWbemObject](/windows/win32/wmisdk/swbemobject) object allows you to access the properties and other information for a Configuration Manager object.  

## See also

 [SMS Provider fundamentals](sms-provider-fundamentals.md)
 [Objects overview](configuration-manager-objects-overview.md)
