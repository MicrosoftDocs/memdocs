---
title: "SMS Provider Field Length Restrictions"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: dea156b8-e508-4234-a350-fbd10dec8ea7
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS Provider Field Length Restrictions
The SMS Provider places restrictions on the width of character fields for schema classes. If you write a program that writes to these classes, you should take these field widths into account. Where they are used in the user interface, the SMS online Help provides the maximum character widths. You can also determine the width by dividing the corresponding schema class table column width by two to give the field width in characters.  

 You can determine the schema class table column width from the corresponding SQL Server views. For information about mapping schema classes to SQL Server views, see SMS Schema View Mapping. The steps for obtaining the table column width from the SQL Server view in SQL Server are:  

- Open the SQL Server view's properties to see which table and table columns it uses.  

- Open the corresponding table in the database Tables view to discover the column width.  

  Classes that are commonly affected by this restriction are:  

- SMS_Package  

- SMS_Advertisement  

- SMS_Program  

- SMS_DistributionPoint  

- SMS_PDF_Package  

- SMS_PDF_Program  

- SMS_Query  

- SMS_Report  

- SMS_ReportDashboard  

- SMS_ReportViewSchema  

- SMS_CollectionRuleQuery  

- SMS_Collection  

- SMS_UserInstancePermissions  

- SMS_UserClassPermissions  

- SMS_UserInstancePermissionNames  

- SMS_UserClassPermissionNames
