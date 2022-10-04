---
title: IPxeAuthClass Interface
titleSuffix: Configuration Manager
description: The IPxeAuthClass automation interface enables configuration of a PXE service point.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 309571d9-2689-4b49-946d-927e782e96ec
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# IPxeAuthClass Interface
The `IPxeAuthClass` automation interface, in Configuration Manager, enables configuration of a PXE service point by serializing certificate information in the form that is required for the [SubmitRegistrationRecord Method in Class SMS_Site](../../../../../develop/reference/core/servers/configure/submitregistrationrecord-method-in-class-sms_site.md). This interface inherits from `IDispatch`.  

## In This Section  

|Term|Definition|  
|----------|----------------|  
|[IPxeAuthClass::CreateIdentity Method](../../../../../develop/reference/core/clients/client-classes/ipxeauthclass--createidentity-method.md)|Creates a PXE certificate identity used in the client configuration file.|  
|[IPxeAuthClass::ReadIdentity Method](../../../../../develop/reference/core/clients/client-classes/ipxeauthclass--readidentity-method.md)|Reads a PXE certificate identity from the client configuration file.|  

## Remarks  
 The UUID for `IPxeAuthClass` is 2BCF9AFE-C441-4f69-A943-08A4C4EAAE5B.  

## See Also  
 [PxeAuthClass Client COM Automation Class](../../../../../develop/reference/core/clients/client-classes/pxeauthclass-client-com-automation-class.md)   
 [About Operating System Deployment Site Role Configuration](../../../../../develop/osd/about-operating-system-deployment-site-role-configuration.md)
