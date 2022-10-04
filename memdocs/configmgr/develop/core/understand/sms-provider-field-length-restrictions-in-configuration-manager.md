---
title: SMS Provider Field Length Restrictions in Configuration Manager
ms.date: 09/20/2016
description: Places restrictions on the width of character fields for schema classes.
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: e5163571-37f5-4dfd-aac6-5bba3ea4c9ea
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: null
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# SMS Provider Field Length Restrictions in Configuration Manager
The SMS Provider, in Configuration Manager, places restrictions on the width of character fields for schema classes. If you write a program that writes to these classes, you should take these field widths into account. Where they are used in the user interface, the Configuration Manager online Help provides the maximum character widths. You can also determine the width by dividing the corresponding schema class table column width by two to give the field width in characters.  

 You can determine the schema class table column width from the corresponding SQL Server views. For information about mapping schema classes to SQL Server views, see [Configuration Manager Schema View Mapping](../../../develop/core/understand/configuration-manager-schema-view-mapping.md). The steps for obtaining the table column width from the SQL Server view in Microsoft SQL Server are:  

1. Open the properties of the SQL Server view to see which table and table columns it uses.  

2. Open the corresponding table in the database tables view to discover the column width.  

   Classes that are commonly affected by this restriction are:  

-   `SMS_Package`  

-   `SMS_Advertisement`  

-   `SMS_Program`  

-   `SMS_DistributionPoint`  

-   `SMS_PDF_Package`  

-   `SMS_PDF_Program`  

-   `SMS_Query`  

-   `SMS_Report`  

-   `SMS_ReportDashboard`  

-   `SMS_ReportViewSchema`  

-   `SMS_CollectionRuleQuery`  

-   `SMS_Collection`  

-   `SMS_UserInstancePermissions`  

-   `SMS_UserClassPermissions`  

-   `SMS_UserInstancePermissionNames`  

-   `SMS_UserClassPermissionNames`  

## See also

 [SMS Provider fundamentals](sms-provider-fundamentals.md)
