---
title: "Deployment Type Extension Versioning"
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
ms.assetid: 33b69e99-dc7c-45dc-8291-362af08956b6searchScope: - ConfigMgr SDK
caps.latest.revision: 12
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# Deployment Type Extension Versioning
Configuration Manager supports in-place versioning for minor upgrades and out-of-place versioning for major upgrades.  

## Versioning  

### Minor Revisions  
 Configuration Manager supports in-place versioning for minor upgrades that are backwards compatible. For in-place versioning, simply increment the version number.  

### Major Revisions  
 Configuration Manager supports out-of-place versioning for major upgrades that are not backwards compatible. For out-of-place versioning, it is necessary to create a new extension and technology id.  

## See Also  
 [Configuration Manager Application Management Extension](../../develop/apps/application-management-extension.md)   
 [Configuration Manager Reference](../../develop/reference/configuration-manager-reference.md)
