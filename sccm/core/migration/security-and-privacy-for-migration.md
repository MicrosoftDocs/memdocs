---
title: "Migration security and privacy"
titleSuffix: "Configuration Manager"
description: "Get security best practices and privacy information for migration to your System Center Configuration Manager environment."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6893fce1-7ad5-4151-9ba9-3096871e8e4a
caps.latest.revision: 5
caps.handback.revision: 0
author: Brendunsms.author: brendunsmanager: angrobe

---
# Security and privacy for migration to System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
This topic contains security best practices and privacy information for migration to your System Center Configuration Manager environment.  

## Security Best Practices for Migration  
 Use the following security best practice for migration.  

|Security best practice|More information|  
|----------------------------|----------------------|  
|Use the computer account for the Source Site SMS Provider Account and the Source Site SQL Server Account rather than a user account.|If you must use a user account for migration, remove the account details when migration is completed.|  
|Use IPsec when you migrate content from a distribution point in a source site to a distribution point in your destination site.|Although the migrated content is hashed to detect tampering, if the data is modified while it is transferred, the migration will fail.|  
|Restrict and monitor the administrative users who can create migration jobs.|The integrity of the database of the destination hierarchy depends upon the integrity of data that the administrative user chooses to import from the source hierarchy. In addition, this administrative user can read all data from the source hierarchy.|  

### Security Issues for Migration  
Migration has the following security issues:  

-   Clients that are blocked from a source site might successfully assign to the destination hierarchy before their client record is migrated.  

     Although Configuration Manager retains the blocked status of clients that you migrate, the client can successfully assign to the destination hierarchy if assignment occurs before the migration of the client record is completed.  

-   Audit messages are not migrated.  

When you migrate data from a source site to a destination site, you lose any auditing information from the source hierarchy.  

## Privacy Information for Migration  
 Migration discovers information from the site databases that you identify in a source infrastructure and stores this data to the database in the destination hierarchy. The information that System Center Configuration Manager can discover from a source site or hierarchy depends upon the features that were enabled in the source environment, as well as the management operations that were performed in that source environment.  

 For more information about security and privacy information, see one of the following topics:  

-   For more information about the privacy information for Configuration Manager 2007, see [Security and Privacy for Configuration Manager 2007](http://go.microsoft.com/fwlink/p/?LinkId=216450) in the Configuration Manager 2007 documentation library.  

-   For more information about the privacy information for System Center 2012 Configuration Manager, see  [Security and Privacy for System Center 2012 Configuration Manager](https://technet.microsoft.com/library/gg682033.aspx) in the System Center 2012 Configuration Manager documentation library.  

-   For more information about the privacy information for System Center Configuration Manager, see [Security and privacy for System Center Configuration Manager](../../core/plan-design/security/security-and-privacy.md).  

You can migrate some or all of the supported data from a source site to a destination hierarchy.  

Migration is not enabled by default and requires several configuration steps. Migration information is not sent to Microsoft.  

Before you migrate data from a source hierarchy, consider your privacy requirements.  
