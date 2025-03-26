---
title: International support
titleSuffix: Configuration Manager
description: Configure Configuration Manager to comply with specific international requirements.
ms.date: 10/06/2016
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: article
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# International support in Configuration Manager

*Applies to: Configuration Manager (current branch)*

The following sections provide technical details to help you make Configuration Manager compliant with specific international requirements.  

## GB18030 Requirements  
 Configuration Manager meets the standards that are defined in GB18030 so that you can use Configuration Manager in China. A Configuration Manager deployment must have the following configurations to meet the GB18030 requirements:  

-   Each site server computer and SQL Server computer that you use with Configuration Manager must use a Chinese operating system.  

-   Each site database and each instance of SQL Server in the hierarchy must use the same collation, and must be one of the following:  

    -   Chinese_Simplified_Pinyin_100_CI_AI  

    -   Chinese_Simplified_Stroke_Order_100_CI_AI  

    > [!NOTE]  
    >  These database collations are an exception to the requirements that are noted in [Support for SQL Server versions for Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  

-   You must place a file with the name **GB18030.SMS** in the root folder of the system volume of each site server computer in the hierarchy. This file does not contain any data and can be an empty text file that is named to meet this requirement.  
