---
title: Migration security and privacy
titleSuffix: Configuration Manager
description: Get security best practices and privacy information for migration to your Configuration Manager current branch environment.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Security and privacy for migration to Configuration Manager current branch

*Applies to: Configuration Manager (current branch)*

This topic contains security best practices and privacy information for migration to your Configuration Manager current branch environment.  

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
 Migration discovers information from the site databases that you identify in a source infrastructure and stores this data to the database in the destination hierarchy. The information that Configuration Manager can discover from a source site or hierarchy depends upon the features that were enabled in the source environment, as well as the management operations that were performed in that source environment.  

For more information about security and privacy information, see [Security and privacy for Configuration Manager](../../security/index.yml). 

You can migrate some or all of the supported data from a source site to a destination hierarchy.  

Migration is not enabled by default and requires several configuration steps. Migration information is not sent to Microsoft.  

Before you migrate data from a source hierarchy, consider your privacy requirements.