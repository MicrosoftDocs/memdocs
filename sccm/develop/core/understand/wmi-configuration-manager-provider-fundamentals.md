---
title: "WMI Provider Fundamentals"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 04ca780f-dd83-43de-b967-bb9f8a05eb3a
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# WMI Configuration Manager Provider Fundamentals
Windows Script Host-based applications and scripts work in Windows Management Instrumentation (WMI) through the WMI Object Model, which defines the programming interface to WMI. A number of WMI object types are used when manipulating System Center Configuration Manager objects. For more information about the WMI Object Model, see [Windows Management Instrumentation](http://go.microsoft.com/fwlink/?LinkId=276770).  

 In simple Configuration Manager scripts, you use the following WMI object types:  

-   `SWbemLocator`  

-   `SWbemServices`  

-   `SWbemObjectSet`  

-   `SWbemObject`  

> [!NOTE]
>  Understanding WMI Query Language (WQL) queries is very important for identifying which Configuration Manager objects you want to read. WQL statements allow you to retrieve Configuration Manager objects that are based on SQL-like queries. For example, the following WQL statement is used to identify all Windows Server 2003 systems:  
>   
>  `SELECT * FROM SMS_FullCollectionMembership WHERE CollectionID='SMS000FS'`  

 For more information about using VBScript and WMI, see [How to Use Configuration Manager Objects With WMI](../../../develop/core/understand/how-to-use-configuration-manager-objects-with-wmi.md).  

## SWbemLocator  
 The [SWbemServices](http://go.microsoft.com/fwlink/?LinkId=276771)object is used to create an authenticated connection to the SMS Provider. You use the [ConnectServer](http://go.microsoft.com/fwlink/?LinkId=276772) method to make the connection to the SMS Provider. This method is particularly useful if you need to pass user credentials to a remote Configuration Manager server during connection. You can also use the Windows Script Host [GetObject](http://go.microsoft.com/fwlink/?LinkId=276773) method to create an authenticated connection. The type of object that is returned by `GetObject` depends on the parameters that are passed to it. See [How to Connect to a Configuration Manager Provider Using Managed Code](../../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md) and [How to Connect to a Configuration Manager Provider Using WMI](../../../develop/core/understand/how-to-connect-to-an-sms-provider-in-configuration-manager-by-using-wmi.md) for examples that show how to use either `SWbemLocator` or `GetObject` in your connection script.  

## SWbemServices  
 The [SWbemServices](http://go.microsoft.com/fwlink/?LinkId=276771) object represents an authenticated connection to a SMS Provider, and it is the object that you use to retrieve Configuration Manager objects. You receive an `SWbemServices` object as the return value of the `SWbemLocator` function `ConnectServer` or, alternatively, as the return value when the `GetObject` method is used to connect to the SMS Provider. `SWbemServices` has several methods, but you use only the [Get](http://go.microsoft.com/fwlink/?LinkId=276774), [ExecQuery](http://go.microsoft.com/fwlink/?LinkId=276775), and [InstancesOf](http://go.microsoft.com/fwlink/?LinkId=276776) methods for retrieving objects.  

 `Get` returns a single instance of a Configuration Manager object (`SWbemObject`). `ExecQuery` and `InstancesOf` return Configuration Manager objects in a collection (`SWbemObjectSet`) of Configuration Manager objects.  

## SWbemObjectSet  
 The [SWbemObjectSet](http://go.microsoft.com/fwlink/?LinkId=276777) object represents a collection of Configuration Manager objects. You can use it to enumerate through the collection and read individual instances of the Configuration Manager object (`SWbemObject`) that you are interested in. You typically get a `SWbemObjectSet` object returned to you from the `SWbemServices` retrieval functions.  

## SWbemObject  
 The [SWbemObject](http://go.microsoft.com/fwlink/?LinkId=276778) object allows you to access the properties and other information for a Configuration Manager object.  

## See Also  
 [Configuration Manager Provider](../../../develop/core/understand/sms-provider-in-configuration-manager.md)   
 [Configuration Manager Programming Fundamentals](../../../develop/core/understand/configuration-manager-programming-fundamentals.md)   
 [How to Use Configuration Manager Objects With WMI](../../../develop/core/understand/how-to-use-configuration-manager-objects-with-wmi.md)
