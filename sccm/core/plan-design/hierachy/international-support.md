---
title: "International support in System Center Configuration Manager"
ms.custom: na
ms.date: 2015-12-08
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
author: Brenduns
translation.priority.ht: 
  - cs-cz
  - de-de
  - en-gb
  - es-es
  - fr-fr
  - hu-hu
  - it-it
  - ja-jp
  - ko-kr
  - nl-nl
  - pl-pl
  - pt-br
  - pt-pt
  - ru-ru
  - sv-se
  - tr-tr
  - zh-cn
  - zh-tw
---
# International support in System Center Configuration Manager
The following sections provide technical details to help you configure System Center Configuration Manager to be compliant for specific international requirements.  
  
## GB18030 Requirements  
 Configuration Manager meets the standards that are defined in GB18030 so that you can use Configuration Manager in China. A Configuration Manager deployment must have the following configurations to meet the GB18030 requirements:  
  
-   Each site server computer and SQL Server computer that you use with Configuration Manager must use a Chinese operating system.  
  
-   Each site database and each instance of SQL Server in the hierarchy must use the same collation, and must be one of the following:  
  
    -   Chinese_Simplified_Pinyin_100_CI_AI  
  
    -   Chinese_Simplified_Stroke_Order_100_CI_AI  
  
    > [!NOTE]  
    >  These database collations are an exception to the requirements noted in [Support for SQL Server versions for System Center Configuration Manager](../../../core/plan-design/configs/support-for-sql-server-versions.md).  
  
-   You must place a file with the name **GB18030.SMS** in the root folder of the system volume of each site server computer in the hierarchy. This file does not contain any data and can be an empty text file that is named to meet this requirement.  
  
## See Also  
 [Site and hierarchy infrastructure technical reference for System Center Configuration Manager](../Topic/Site%20and%20hierarchy%20infrastructure%20technical%20reference%20for%20System%20Center%20Configuration%20Manager.md)