---
title: Association Classes
titleSuffix: Configuration Manager
description: An association allows you to logically relate the instances of two classes. An association consists of two key properties which are paths or pointers.
ms.date: 09/20/2016
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 268bb9d1-3058-4c09-8e38-148a51d879f7
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Configuration Manager Association Classes
In Configuration Manager, an association allows you to logically relate the instances of two classes. Typically, an association consists of two key properties (which are paths, or pointers, that uniquely identify the location of the other class instances), but an association can also contain additional properties. The provider uses the key properties to retrieve the requested data.  

 Although association classes provide a convenient means to collect related information, they are inherently slow. If performance is an issue, you should consider collecting the related information yourself.  

> [!NOTE]
>  Association classes are read-only except for the `SMS_CollectToSubCollect_a` class. Association class names are suffixed with _a.  

 The following table shows the association classes.  

|Association class|Description|  
|-----------------------|-----------------|  
|`SMS_AdvertToSourceSite_a`|Relates an advertisement with the site that created the advertisement.|  
|`SMS_BaseAssociation`|An abstract class that is the base class for all Configuration Manager association classes. It has no properties.|  
|`SMS_CollectionMember_a`|Relates a collection with its member resources.|  
|`SMS_CollectionToPkgAdvert_a`|Relates an advertisement with its target collection.|  
|`SMS_CollectToSubCollect_a`|Relates a collection with its parent collection.|  
|`SMS_ObjectToClassPermissions_a`|Relates a secured object with various users that have class permissions on the object.|  
|`SMS_ObjectToInstancePermissions_a`|Relates a secured object with users that have permissions for an instance of a secured object.|  
|`SMS_PackageToAdvert_a`|Relates an advertisement to the package it advertises.|  
|`SMS_PackageToSourceSite_a`|Relates a package to the site that created the package.|  
|`SMS_PDFPkgToPDFProgram_a`|Relates a package definition file package to package definition file programs that are part of the package.|  
|`SMS_PkgToPkgAccess_a`|Relates a package with the user accounts that are used to access a package on its distribution points.|  
|`SMS_PkgToPkgProgram_a`|Relates a package with the programs that form the package.|  
|`SMS_PkgToPkgServer_a`|Relates a package with its distribution points.|  
|`SMS_SCFToSCI_a`|Relates a site control file with the site control items that make up the current site control file.|  
|`SMS_SCFToSite_a`|Relates a site control file with the site to which it belongs.|  
|`SMS_SiteToROOTColl_a`|Relates a site with the root of the collections that belong to it.|  
|`SMS_SiteToSiteID_a`|Relates a site with its identifying information.|  
|`SMS_SiteToSubSite_a`|Defines the hierarchy of sites by relating a site with its subsites.|  

## See Also  
 [Configuration Manager Bit Field Properties](../../../develop/core/understand/configuration-manager-bit-field-properties.md)   
 [Configuration Manager Date and Time Formats](../../../develop/core/understand/date-and-time-formats.md)   
 [Configuration Manager Embedded Objects](../../../develop/core/understand/embedded-objects.md)   
 [Configuration Manager Extended WMI Query Language](../../../develop/core/understand/extended-wmi-query-language.md)   
 [Objects overview](configuration-manager-objects-overview.md)
 [Configuration Manager Lazy Properties](../../../develop/core/understand/configuration-manager-lazy-properties.md)   
 [About errors](about-configuration-manager-errors.md)
 [Configuration Manager Object Security](../../../develop/core/understand/configuration-manager-object-security.md)   
 [Configuration Manager Special Queries](../../../develop/core/understand/special-queries.md)
