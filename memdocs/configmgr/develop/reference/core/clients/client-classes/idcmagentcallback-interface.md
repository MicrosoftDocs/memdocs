---
description: Learn how to use the IDCMAgentCallback interface to represent the callback for the desired configuration management agent. This interface inherits from IUnknown.
title: IDCMAgentCallback Interface
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 65f4a6ba-e72e-4449-abe2-39a67d3f915e
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# IDCMAgentCallback Interface
The `IDCMAgentCallback` interface, in Configuration Manager, represents the callback for the Desired Configuration Management Agent. This interface inherits from `IUnknown`.  

## In This Section  
 The following table lists the methods in the `IDCMAgentCallback` interface.  

|Term|Definition|  
|----------|----------------|  
|[IDCMAgentCallback::NotifyComplete](../../../../../develop/reference/core/clients/client-classes/idcmagentcallback--notifycomplete-method.md)|Notifies the caller that a Desired Configuration Management agent job has been completed.|  
|[IDCMAgentCallback::NotifyError](../../../../../develop/reference/core/clients/client-classes/idcmagentcallback--notifyerror-method.md)|Notifies the caller that a Desired Configuration Management agent job has failed to be completed.|  
|[IDCMAgentCallback::NotifyProgress](../../../../../develop/reference/core/clients/client-classes/idcmagentcallback--notifyprogress-method.md)|Notifies the caller of progress made on a Desired Configuration Management agent job.|  

## UUID  
 The UUID for `IDCMAgentCallback` is 513FB8A1-67E9-4f18-8E77-0CBD6BE95708.  

## See Also  
 [Compliance Settings (DCM) Client Interfaces](../../../../../develop/reference/core/clients/client-classes/compliance-settings--dcm--client-interfaces.md)
