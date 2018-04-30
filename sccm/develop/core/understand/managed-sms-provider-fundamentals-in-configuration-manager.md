---
title: "Managed SMS Provider Fundamentals"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 18924a3e-0cc3-4aa8-98bc-b6beca182d4e
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Managed SMS Provider Fundamentals in Configuration Manager
The managed SMS Provider library is a .NET Framework library that wraps the System.Management classes and provides a System Center Configuration Manager-centric object model. It also provides a wrapper for accessing the Configuration Manager site control file.  

 The library can be used outside of any code relating to the Configuration Manager console .NET Framework library, but is built on the same underlying architecture.  

 For information about using managed code with the System Center Configuration Manager client, see [About Configuration Manager WMI Programming](../../../develop/core/clients/programming/about-configuration-manager-wmi-programming.md).  

## Configuration Manager Classes and Interfaces  
 The primary classes and interfaces for use with the managed SMS Provider are the following:  

### WqlConnectionManager  
 The class `WqlConnectionManager` provides access to the Configuration Manager Windows Management Instrumentation (WMI) provider.  

 It is an implementation of the abstract base class [ConnectionManagerBase](https://msdn.microsoft.com/library/microsoft.configurationmanagement.managementprovider.connectionmanagerbase.aspx) that defines connections throughout the managed System Center Configuration Manager libraries.  

 It is used to connect to the SMS Provider and query, or create, System Center Configuration Manager object instances. The following tasks demonstrate the basic usage of WqlConnectionManager.  

 [How to Connect to a Configuration Manager Provider using Managed Code](../../../develop/core/understand/how-to-connect-to-an-sms-provider-by-using-managed-code.md).  

 [How to Read a Configuration Manager Object Using Managed Code](../../../develop/core/understand/how-to-read-a-configuration-manager-object-by-using-managed-code.md).  

 [How to Perform an Asynchronous Configuration Manager Query Using  Managed Code](../../../develop/core/understand/how-to-perform-an-asynchronous-query-by-using-managed-code.md)  

### IResultObject  
 [IResultObject](https://msdn.microsoft.com/library/microsoft.configurationmanagement.managementprovider.iresultobject.aspx) is an interface that all result sets and objects expose. Through it, you can read, modify, delete, call methods on, and otherwise manipulate Configuration Manager objects. You typically get an `IResultObject` whenever you create an object or as a result of a query.  

 The following tasks demonstrate the basic use of `IResultObject`:  

 [How to Modify a Configuration Manager Object Using Managed Code](../../../develop/core/understand/how-to-modify-a-configuration-manager-object-by-using-managed-code.md)  

 [How to Delete a Configuration Manager Object Using Managed Code](../../../develop/core/understand/how-to-delete-a-configuration-manager-object-by-using-managed-code.md)  

 [How to Call a Configuration Manager Object Method Using Managed Code](../../../develop/core/understand/how-to-call-a-configuration-manager-object-class-method-by-using-managed-code.md)  

### QueryProcessor  
 QueryProcesor provides support for both synchronous and asynchronous queries against the SMS Provider. In asynchronous queries, [SmsBackgroundWorker](https://msdn.microsoft.com/library/microsoft.configurationmanagement.managementprovider.smsbackgroundworker.aspx) is used to provide thread support query results. The following tasks demonstrate queries:  

 [How to Perform an Asynchronous Configuration Manager Query Using Managed Code](../../../develop/core/understand/how-to-perform-an-asynchronous-query-by-using-managed-code.md).  

 [How to Perform a Synchronous Configuration Manager Query Using  Managed Code](../../../develop/core/understand/how-to-perform-a-synchronous-configuration-manager-query-by-using-managed-code.md).  

### IQueryPropertyItem  
 [IQueryPropertyItem](https://msdn.microsoft.com/library/microsoft.configurationmanagement.managementprovider.iquerypropertyitem.aspx) is a single property of the result object, supports data binding and get/set properties.  

 The following tasks demonstrate the use of `IQueryPropertyItem`:  

 [How to Modify a Configuration Manager Object Using Managed Code](../../../develop/core/understand/how-to-modify-a-configuration-manager-object-by-using-managed-code.md).  

## Assemblies  
 The assemblies that are required for using managed SMS Provider are:  

 microsoft.configurationmanagement.managementprovider  

 adminui.wqlqueryengine  

 The WMI implementation of the managed Configuration Manager libraries is provided by adminui.wqlqueryengine.  

## See Also  
 [Configuration Manager Provider](../../../develop/core/understand/sms-provider-in-configuration-manager.md)   
 [Configuration Manager Objects](../../../develop/core/understand/configuration-manager-objects-overview.md)
