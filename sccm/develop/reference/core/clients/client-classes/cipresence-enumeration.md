---
title: "CIPresence Enumeration"
titleSuffix: "Configuration Manager"
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
ms.assetid: 0874e405-5ab9-4f43-bb2f-42a95ae7a1c7searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# CIPresence Enumeration
In System Center Configuration Manager, the `CIPresence` enumeration defines configuration item presence types used in the discovery process.  

## Syntax  

```  
typedef enum tagCIPresence  
{  
  ciNotPresent = 0,ciNonCompliant = 0,  
  ciPresent = 1,ciCompliant = 1,  
  ciNotApplicable = 2,  
  ciPresenceUnknown = 3,ciComplianceUnknown = 3,  
  ciEvaluationError = 4,  
  ciNotEvaluated = 5  
} CIPresence;  
```  

## Elements  
 `ciNotPresent, ciNonCompliant`  
 Configuration item not present or not compliant.  

 `ciPresent, ciCompliant`  
 Configuration item present or compliant.  

 `ciNotApplicable`  
 Configuration item not applicable.  

 `ciPresenceUnknown, ciComplianceUnknown`  
 Configuration item presence or compliance unknown.  

 `ciEvaluationError`  
 Configuration item evaluation error.  

 `ciNotEvaluated`  
 Configuration item not evaluated.  

## Remarks  
 This enumeration is used by the [ICIINFO Interface](../../../../../develop/reference/core/clients/client-classes/iciinfo-interface.md).  

## See Also  
 [ICIINFO Interface](../../../../../develop/reference/core/clients/client-classes/iciinfo-interface.md)
