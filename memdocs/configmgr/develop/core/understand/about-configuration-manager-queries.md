---
title: "Configuration Manager Queries"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: e20ee196-8b6b-49c1-98e8-613438ea8279
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# About Configuration Manager Queries
You can create and run the queries that are accessible in the Configuration Manager console under **Queries**. The queries can be used to locate objects in a Configuration Manager site that match your query criteria. These objects include items such as specific types of computers or user groups. Queries can return most types of Configuration Manager objects, including sites, collections, packages, and saved queries themselves. However, queries are most useful for extracting information that is related to resource discovery, inventory data, and status messages.  

> [!NOTE]
> For more information, see [Introduction to queries](../../../core/servers/manage/introduction-to-queries.md).  

## SMS_Query  
 Configuration Manager queries are defined by `SMS_Query` object instances. The query is a WQL query and is defined in the `Expression` property. For more information about WQL, see [Configuration Manager Extended WMI Query Language](../../../develop/core/understand/extended-wmi-query-language.md).  

 Each query has a unique identifier assigned to it by the SMS Provider and can be used to get a specific query.  

 For information about running a query, see [How to Run a Configuration Manager Query](../../../develop/core/understand/how-to-run-a-query.md).  

 You can also create queries by creating instances of `SMS_Query`. When you create a query, it is displayed in the Configuration Manager console under **Queries**. If you want to, you can limit the results returned to those resources that belong to a specific collection. For more information about creating queries, see [How to Create a Configuration Manager Query](../../../develop/core/understand/how-to-create-a-configuration-manager-query.md).  

## See Also  
 [Configuration Manager Extended WMI Query Language](../../../develop/core/understand/extended-wmi-query-language.md)   
 [Configuration Manager Result Sets](../../../develop/core/understand/result-sets.md)   
 [Configuration Manager Special Queries](../../../develop/core/understand/special-queries.md)   
 [How to Create a Configuration Manager Query](../../../develop/core/understand/how-to-create-a-configuration-manager-query.md)   
 [How to Run a Configuration Manager Query](../../../develop/core/understand/how-to-run-a-query.md)   
 [SMS_Query](../../../develop/reference/core/clients/manage/sms_query-server-wmi-class.md)
