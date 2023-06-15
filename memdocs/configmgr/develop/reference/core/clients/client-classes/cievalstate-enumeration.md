---
title: CIEvalState Enumeration
titleSuffix: Configuration Manager
description: In Configuration Manager, the CIEvalState enumeration is used by the ICIINFO Interface.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 952016eb-b0b5-47a6-acef-01d65acc9f65
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# CIEvalState Enumeration
In Configuration Manager, the `CIEvalState` enumeration defines configuration item evaluation states. This enumeration is used by the [ICIINFO Interface](../../../../../develop/reference/core/clients/client-classes/iciinfo-interface.md).  

## Syntax  

```  
typedef enum tagCIEvalState  
{  
  ciIdle = 0,  
  ciEvaluating   
} CIEvalState;  
```  

## Elements  
 ciIdle  
 Configuration item is idle.  

 ciEvaluating  
 Configuration item is being evaluated.  

## See Also  
 [ICIINFO Interface](../../../../../develop/reference/core/clients/client-classes/iciinfo-interface.md)
