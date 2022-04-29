---
title: "Deployment Type Extension Versioning"
description: Configuration Manager supports in-place versioning for minor upgrades and out-of-place versioning for major upgrades.
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 33b69e99-dc7c-45dc-8291-362af08956b6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# Deployment Type Extension Versioning
Configuration Manager supports in-place versioning for minor upgrades and out-of-place versioning for major upgrades.  

## Versioning  

### Minor Revisions  
 Configuration Manager supports in-place versioning for minor upgrades that are backwards compatible. For in-place versioning, simply increment the version number.  

### Major Revisions  
 Configuration Manager supports out-of-place versioning for major upgrades that are not backwards compatible. For out-of-place versioning, it is necessary to create a new extension and technology id.  

## See Also  
 [Configuration Manager Reference](../../develop/reference/configuration-manager-reference.md)
