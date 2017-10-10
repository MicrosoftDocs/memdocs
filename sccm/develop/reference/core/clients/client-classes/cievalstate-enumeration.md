---
title: "CIEvalState Enumeration"
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
ms.assetid: 952016eb-b0b5-47a6-acef-01d65acc9f65searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# CIEvalState Enumeration
In System Center Configuration Manager, the `CIEvalState` enumeration defines configuration item evaluation states. This enumeration is used by the [ICIINFO Interface](../../../../../develop/reference/core/clients/client-classes/iciinfo-interface.md).  

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
