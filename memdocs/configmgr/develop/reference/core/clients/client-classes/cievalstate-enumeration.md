---
title: "CIEvalState Enumeration"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 952016eb-b0b5-47a6-acef-01d65acc9f65
author: aczechowski
ms.author: aaroncz
manager: dougeby


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
