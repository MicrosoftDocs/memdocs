---
title: Example validation state transitions
titleSuffix: Configuration Manager
description: See examples of validation state transitions for Asset Intelligence in Configuration Manager.
ms.date: 02/22/2017
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: article
author: sheetg09
ms.author: sheetg
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Example validation state transitions for Asset Intelligence

*Applies to: Configuration Manager (current branch)*

Asset Intelligence validation states in Configuration Manager aren't static and can change from administrative actions that you take to affect the data that are stored in the Asset Intelligence catalog. This topic provides examples for possible validation state transitions.

##  <a name="BKMK_UncategorizedIsCategorized"></a> Uncategorized catalog item is categorized by the administrative user  

|**State transition**|**State transition description**|  
|--------------------------|--------------------------------------|  
|**Uncategorized**|An inventoried software title that hasn't been previously categorized by System Center Online or that the administrative user has entered into the Asset Intelligence catalog.|  
|**Uncategorized** to **UserDefined**|The uncategorized item is categorized by the administrative user.|  

##  <a name="BKMK_CategorizedIsReCategorized"></a> Categorized catalog item is recategorized by the administrative user  

|**State transition**|**State transition description**|  
|--------------------------|--------------------------------------|  
|**Validated**|Catalog item has been defined by System Center Online researchers and is present in the Asset Intelligence catalog.|  
|**Validated** to **User Defined**|The validated catalog item is re-categorized by the administrative user.|  

> [!NOTE]  
>  Because categorization information obtained from System Center Online is stored in the database and cannot be deleted, the administrative user can revert back to the System Center Online categorization later.  

##  <a name="BKMK_UserDefinedIsRecategorized"></a> User-defined catalog item is recategorized by System Center Online  

|**State transition**|**State transition description**|  
|--------------------------|--------------------------------------|  
|**Uncategorized**|An inventoried software title is entered into the Asset Intelligence catalog that hasn't been previously categorized by System Center Online or the administrative user.|  
|**User Defined**|The uncategorized item is categorized by the administrative user.|  
|**User Defined** to **Updateable**|A user-defined catalog item has been categorized differently by System Center Online during subsequent manual bulk updates of the Asset Intelligence catalog.<br /><br /> The administrative user can use the **Software Details Conflict Resolution** dialog box to decide whether to use the new categorization information or the previous user-defined value.|  
|**Updateable** to **Validated**|The administrative user uses the **Software Details Conflict Resolution** dialog box to use the new categorization information received from System Center Online during the previous catalog update.|  
|or||  
|**Updateable** to **User Defined**|The administrative user uses the **Software Details Conflict Resolution** dialog box to use the previous user-defined value.|  

> [!NOTE]  
>  Because categorization information obtained from System Center Online is stored in the database and cannot be deleted, the administrative user can revert back to the System Center Online categorization later.  

##  <a name="BKMK_UncategorizedIsSubmitted"></a> Uncategorized catalog item is submitted to System Center Online for categorization  

|**State transition**|**State transition description**|  
|--------------------------|--------------------------------------|  
|**Uncategorized**|An inventoried software title is entered into the Asset Intelligence database that hasn't been previously categorized by System Center Online or the administrative user.|  
|**Uncategorized** to **Pending**|The uncategorized item is submitted to System Center Online for categorization by the administrative user.|  
|**Pending** to **Validated**|The item is categorized by System Center Online. The administrative user imports the item into the Asset Intelligence catalog by using a bulk catalog update or Asset Intelligence catalog synchronization. Both are available by using the Asset Intelligence synchronization point site system role.|  

##  <a name="BKMK_UserDefinedIsSubmitted"></a> User-defined catalog item is submitted to System Center Online for categorization  

|**State transition**|**State transition description**|  
|--------------------------|--------------------------------------|  
|**Uncategorized**|An inventoried software title is entered into the Asset Intelligence database that hasn't been previously categorized by an administrative user or System Center Online.|  
|**User Defined**|You categorized the uncategorized item.|  
|**User Defined** to **Pending**|You submit the user-defined item to System Center Online for categorization.|  
|**Pending** to **Updateable**|A user-defined catalog item has been categorized differently by System Center Online during subsequent catalog synchronization. You can use the **Resolve Conflict** action to decide whether to use the new categorization information or the previous user-defined value. For more information about resolving conflicts, see [Resolve software details conflicts](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails).|  
|**Updateable** to **Validated**|You use the **Resolve Conflict** action and select the new categorization information received from System Center Online during the previous catalog update. For more information about resolving conflicts, see [Resolve software details conflicts](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails).|  
|or||  
|**Updateable** to **User Defined**|You use the **Resolve Conflict** action and select to use the previous user-defined value. For more information about resolving conflicts, see [Resolve software details conflicts](../../../../core/clients/manage/asset-intelligence/operations-for-asset-intelligence.md#BKMK_ResolveSoftwareDetails).|  

> [!NOTE]  
>  Because categorization information obtained from System Center Online is stored in the database and cannot be deleted, you can revert back to the System Center Online categorization later.  
