---
title: ICIINFO Interface
titleSuffix: Configuration Manager
description: ICIINFO can represent a configuration item which has been downloaded and stored by the Desired Configuration Management client or a baseline configuration item in a Desired Configuration Management Agent job in the client data store.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 9c61cbd9-3f54-41da-abf0-05159f43dc86
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# ICIINFO Interface
The `ICIINFO` interface, in Configuration Manager, can represent the properties of a configuration item which has been downloaded and stored by the Desired Configuration Management client or the properties of a baseline configuration item in a Desired Configuration Management Agent job in the client data store. In both cases, the configuration item is either a (top level/root) baseline or a Software Updates configuration item.  

 The interface inherits from `IUnknown`.  

## In This Section  
 The following table lists the methods in the `ICIINFO` interface.  

|Term|Definition|  
|----------|----------------|  
|[ICIINFO::GetCategory](../../../../../develop/reference/core/clients/client-classes/iciinfo--getcategory-method.md)|Gets a localized category name by index and the group name of the category.|  
|[ICIINFO::GetCategoryCount](../../../../../develop/reference/core/clients/client-classes/iciinfo--getcategorycount-method.md)|Gets the count of categories applied to the configuration item.|  
|[ICIINFO::GetCIPresence](../../../../../develop/reference/core/clients/client-classes/iciinfo--getcipresence-method.md)|Gets the current presence for the configuration item.|  
|[ICIINFO::GetContextInfo](../../../../../develop/reference/core/clients/client-classes/iciinfo--getcontextinfo-method.md)|Gets the context information by name from the configuration item.|  
|[ICIINFO::GetDependantPackages](../../../../../develop/reference/core/clients/client-classes/iciinfo--getdependantpackages-method.md)|Gets dependent package information for the configuration item.|  
|[ICIINFO::GetDetailedComplianceInfo](../../../../../develop/reference/core/clients/client-classes/iciinfo--getdetailedcomplianceinfo-method.md)|Gets detailed compliance information from the last compliance evaluation run for the configuration item.|  
|[ICIINFO::GetEvalState](../../../../../develop/reference/core/clients/client-classes/iciinfo--getevalstate-method.md)|Gets the current evaluation state of the configuration item.|  
|[ICIINFO::GetId](../../../../../develop/reference/core/clients/client-classes/iciinfo--getid-method.md)|Gets the ID of the configuration item.|  
|[ICIINFO::GetJobState](../../../../../develop/reference/core/clients/client-classes/iciinfo--getjobstate-method.md)|Gets the current operational job state of the configuration item that is part of a job or task.|  
|[ICIINFO::GetLastEvalTime](../../../../../develop/reference/core/clients/client-classes/iciinfo--getlastevaltime-method.md)|Gets the last evaluation time for the configuration item.|  
|[ICIINFO::GetProperty](../../../../../develop/reference/core/clients/client-classes/iciinfo--getproperty-method.md)|Gets a named property value from the configuration item.|  
|[ICIINFO::GetSdmTypeName](../../../../../develop/reference/core/clients/client-classes/iciinfo--getsdmtypename-method.md)|Gets the fully qualified name of a root configuration item.|  
|[ICIINFO::GetVersion](../../../../../develop/reference/core/clients/client-classes/iciinfo--getversion-method.md)|Gets the version of the configuration item.|  

## Remarks  
 To obtain this interface, the application calls the [IDCMSDK Interface](../../../../../develop/reference/core/clients/client-classes/idcmsdk-interface.md). The application calls the [IDCMAgentCallback Interface](../../../../../develop/reference/core/clients/client-classes/idcmagentcallback-interface.md) interface to respond to agent calls.  

## UUID  
 The UUID for `ICIINFO` is ACF43B8E-23A2-4923-B421-CB918FC5CA1F.  

## See Also  
 [Compliance Settings (DCM) Client Interfaces](../../../../../develop/reference/core/clients/client-classes/compliance-settings--dcm--client-interfaces.md)   
 [IDCMSDK Interface](../../../../../develop/reference/core/clients/client-classes/idcmsdk-interface.md)   
 [IDCMAgentCallback Interface](../../../../../develop/reference/core/clients/client-classes/idcmagentcallback-interface.md)
