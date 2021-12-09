---
title: "SQL View Security"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 4f24562b-a8cd-435f-b5d6-8ef4f8cd7e69
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# Configuration Manager SQL View Security
The Configuration Manager object security mechanism, implemented in the SMS Provider, facilitates instance (or row) level security on core object classes. By using the Configuration Manager schema views, an application or user is operating outside of this security mechanism. This does not mean that the views cannot be secured from unauthorized data access; however, security must be configured separately and is less precise than standard Configuration Manager object security. You can give a user read-only permission to access only the views and deny access to any internal Configuration Manager tables. The main security functionality that is lost in the view approach is the ability to secure specific object instances (such as packages and collections) separately for members of groups.  

## See Also  
 [Configuration Manager Schema View Mapping](../../../develop/core/understand/configuration-manager-schema-view-mapping.md)   
 [Configuration Manager Schema SQL Views](../../../develop/core/understand/configuration-manager-schema-sql-views.md)
