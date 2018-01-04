---
title: "International support"
titleSuffix: "Configuration Manager"
description: "Configure System Center Configuration Manager to comply with specific international requirements."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 46dd9cb2-a812-4b6a-a747-b840f92fef8b
caps.latest.revision: 6
caps.handback.revision: 0
author: aczechowski
ms.author: aaroncz
manager: angrobe

---
# International support in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

The following sections provide technical details to help you make System Center Configuration Manager compliant with specific international requirements.  

## GB18030 Requirements  
 Configuration Manager meets the standards that are defined in GB18030 so that you can use Configuration Manager in China. A Configuration Manager deployment must have the following configurations to meet the GB18030 requirements:  

-   Each site server computer and SQL Server computer that you use with Configuration Manager must use a Chinese operating system.  

-   Each site database and each instance of SQL Server in the hierarchy must use the same collation, and must be one of the following:  

    -   Chinese_Simplified_Pinyin_100_CI_AI  

    -   Chinese_Simplified_Stroke_Order_100_CI_AI  

    > [!NOTE]  
    >  These database collations are an exception to the requirements that are noted in [Support for SQL Server versions for System Center Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  

-   You must place a file with the name **GB18030.SMS** in the root folder of the system volume of each site server computer in the hierarchy. This file does not contain any data and can be an empty text file that is named to meet this requirement.  
