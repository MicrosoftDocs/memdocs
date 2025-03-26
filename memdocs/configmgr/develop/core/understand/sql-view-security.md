---
title: SQL View Security
titleSuffix: Configuration Manager
description: Facilitate instance (or row) level security on core object classes. Using the Configuration Manager schema views, an application or user is operating outside of this security mechanism.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: article
ms.assetid: 4f24562b-a8cd-435f-b5d6-8ef4f8cd7e69
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Configuration Manager SQL View Security
The Configuration Manager object security mechanism, implemented in the SMS Provider, facilitates instance (or row) level security on core object classes. By using the Configuration Manager schema views, an application or user is operating outside of this security mechanism. This doesn't mean that the views can't be secured from unauthorized data access; however, security must be configured separately and is less precise than standard Configuration Manager object security. You can give a user read-only permission to access only the views and deny access to any internal Configuration Manager tables. The main security functionality that is lost in the view approach is the ability to secure specific object instances (such as packages and collections) separately for members of groups.  

## See Also  
 [Configuration Manager Schema View Mapping](../../../develop/core/understand/configuration-manager-schema-view-mapping.md)   
 [Configuration Manager Schema SQL Views](../../../develop/core/understand/configuration-manager-schema-sql-views.md)
