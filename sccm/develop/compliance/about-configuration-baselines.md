---
title: "About Configuration Baselines"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: 23847c17-73c3-44b8-a163-e1f62576d4bbsearchScope: - ConfigMgr SDK
caps.latest.revision: 5
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# About Configuration Baselines
In System Center Configuration Manager, baselines are used to define the configuration of a product or a system that is established at a specific point in time, capturing both structure and details. Configuration baselines in System Center Configuration Manager contain a defined set of desired configurations that are evaluated for compliance as a group.  

 Configuration baselines contain one or more configuration items with associated rules, and they are assigned to computers through collections, together with a compliance evaluation schedule.  

> [!NOTE]
>  Although you can assign configuration baselines to a collection that contains users, the configuration baselines will be evaluated only by computers in the collection, and not by users in the collection.  

 You can create your own configuration baselines with the Configuration Manager console, and you can import configuration baselines from the following sources:  

-   A Best Practices configuration baseline from Microsoft or other vendors  

-   Custom authored configuration baselines from within your own organization, but external to Configuration Manager  

-   Another Configuration Manager site  

 When configuration baselines are imported, unless they were originally created in the same Configuration Manager site, you will not be able to directly modify them in the Configuration Manager console. If you need to refine the configuration items to meet your business requirements, the recommended path is:  

1.  Create child configuration items with your custom values.  

2.  Duplicate the configuration baseline.  

3.  Edit the duplicated baseline, and replace the configuration items with your edited child configuration items.  

## Configuration Baseline Rules  
 Configuration baselines rules are used to specify how the configuration items that are included in the configuration baseline are to be assessed for compliance on client computers. There are fixed types of configuration baseline rules that cannot be changed in Configuration Manager. Configuration items can be added to the following configuration baseline rules:  

-   **One of the following operating system configuration items must be present and properly configured.**  

-   **These applications and general configuration items are required and must be properly configured.**  

-   **If these optional application configuration items are detected, they must be properly configured.**  

-   **These software updates must be present.**  

-   **These application configuration items must not be present.**  

-   **These configuration baselines must also be validated.**  

### RequiredItems  

-   These applications and general configuration items are required and must be properly configured.  

### ProhibitedItems  

-   These application configuration items must not be present.  

### OptionalItems  

-   If these optional application configuration items are detected, they must be properly configured.  

### OperatingSystems  

-   One of the following operating system configuration items must be present and properly configured.  

### SoftwareUpdates  

-   These software updates must be present.  

### Baselines  

-   These configuration baselines must also be validated.  

### OtherConfigurationItems  

-   References to content defined as raw Service Modeling Language (SML).  

## See Also  
 [Authoring Desired Configuration Management Configuration Baselines and Configuration Items](../../develop/compliance/authoring-compliance-settings-configuration-baselines-and-configuration-items.md)
