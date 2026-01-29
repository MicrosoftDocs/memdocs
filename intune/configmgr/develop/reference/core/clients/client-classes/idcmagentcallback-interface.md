---
description: Learn how to use the IDCMAgentCallback interface to represent the callback for the desired configuration management agent. This interface inherits from IUnknown.
title: IDCMAgentCallback Interface
ms.date: 09/20/2016
ms.subservice: sdk
ms.topic: reference
ms.collection: tier3
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
