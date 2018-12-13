---
title: "See a View by Using SQL Server"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 8a8df275-7e63-4159-9f9a-5f21621be0f1
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to See a Configuration Manager View by Using SQL Server
The following examples demonstrate various Microsoft System Center Configuration Manager SQL view queries.  

## Examples  

#### To determine the display name of a resource type from the resource type number  

-   In SQL Server, query the Configuration Manager database with the following SQL statement:  

```  
select DisplayName from v_ResourceMap where ResourceType=5  
```  

#### To determine discovery properties for a particular resource type  

-   In SQL Server, query the Configuration Manager database with the following SQL statement:  

```  
select * from v_ResourceAttributeMap where ResourceType=5  
```  

#### To list the inventory groups for a particular resource type  

-   In SQL Server, query the Configuration Manager database with the following SQL statement:  

```  
select InvClassName from v_GroupMap where ResourceType = 5  
```  

## See Also  
 [Configuration Manager Schema](../../../develop/core/understand/configuration-manager-schema.md)   
 [Configuration Manager Programming Fundamentals](../../../develop/core/understand/configuration-manager-programming-fundamentals.md)
