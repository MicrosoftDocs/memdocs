---
title: "About Configuration Baselines and Items"
titleSuffix: "Configuration Manager"
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
ms.assetid: 56bdef4b-bcf8-46f5-bf92-d86e0dfce08dsearchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# About Configuration Baselines and Configuration Items
In System Center Configuration Manager, baselines are used to define the configuration of a product or system that is established at a specific point in time. Configuration baselines in System Center Configuration Manager contain a defined set of desired configurations that are evaluated for compliance as a group.  

## Configuration Baselines  
 Configuration baselines contain one or more configuration items with associated rules, and they are assigned to computers through collections, together with a compliance evaluation schedule.  

> [!NOTE]
>  Although you can assign configuration baselines to a collection that contains users, the configuration baselines are evaluated only by computers in the collection.  

 You can create your own configuration baselines with the Configuration Manager console, and you can import configuration baselines from the following sources:  

-   A Best Practices configuration baseline from Microsoft or other vendors  

-   Custom authored configuration baselines from within your own organization, but external to Configuration Manager  

-   Another Configuration Manager site  

 When configuration baselines are imported, unless they were originally created in the same Configuration Manager site, you cannot directly modify them in the Configuration Manager console. If you need to refine the configuration items to meet your business requirements, the recommended path is as follows:  

1.  Create child configuration items with your custom values.  

2.  Duplicate the configuration baseline.  

3.  Edit the duplicated baseline, and replace the configuration items with your edited child configuration items.  

### Configuration Baseline Rules  
 Configuration baselines rules are used to specify how the configuration items that are included in the configuration baseline are to be assessed for compliance on client computers. There are fixed types of configuration baseline rules that cannot be changed in Configuration Manager. Configuration items can be added to the following configuration baseline rules:  

-   **One of the following operating system configuration items must be present and properly configured.**  

-   **These applications and general configuration items are required and must be properly configured.**  

-   **If these optional application configuration items are detected, they must be properly configured.**  

-   **These software updates must be present.**  

-   **These application configuration items must not be present.**  

-   **These configuration baselines must also be validated.**  

### Configuration Baseline Assignment  
 Before client computers can assess their compliance with configuration baselines in Configuration Manager, the configuration baseline must be assigned to them through collections of computers.  

 The assignment consists of the following properties:  

-   The configuration baseline itself  

-   Which collection to target for compliance evaluation, and whether it includes any defined sub-collections  

-   The compliance evaluation schedule, which is initially configured with the default compliance evaluation schedule but can be changed for each assignment  

 Configuration baseline assignments are optional properties for a configuration baseline. A single configuration baseline can be assigned to multiple collections by defining multiple configuration baseline assignments.  

### Dependent Configuration Baseline  
 One of the configuration baseline rules is to include another configuration baseline. This nesting capability provides a layered method of defining a base configuration baseline for a wide range of computers and then refining this base configuration with additional configuration baselines that have more specific configurations for computers with similar roles.  

 Dependent baselines are also used when you want to combine your own business requirements with those of an imported configuration baseline (such as Best Practices configuration baselines from Microsoft) that cannot be directly edited. When the Best Practices configuration baseline is upgraded with a new version, you can import the later version without having to create a new configuration baseline.  

 Dependent configuration baselines are displayed in the Configuration Manager console as a property of a configuration baseline.  

### Duplicate Configuration Baseline  
 A duplicate configuration baseline in Configuration Manager is an exact copy of an existing configuration baseline that does not retain any relationship to the original. Creating a duplicate configuration baseline might be appropriate if you wanted to create a number of similar but unrelated configuration baselines and you had one configuration baseline that you use as a template. Another scenario is if you needed to redefine the rules or configuration items in an imported configuration baseline.  

 You cannot duplicate an imported configuration baseline if it contains configuration data that the Configuration Manager cannot interpret.  

## Configuration Items  
 Configuration items define a discrete unit of configuration to assess for compliance. They can contain one or more elements and their validation criteria, and they typically define a unit of configuration that you want to monitor at the level of independent change.  

 Configuration items are the building blocks for configuration baselines, and consequently the same configuration item can be used in multiple configuration baselines.  

 System Center Configuration Manager supports the following configuration item types:  

 **Operating system configuration item**  
 A configuration item to determine compliance for settings relating to the operating system version and configuration.  

 **Application configuration item**  
 A configuration item to determine compliance for an application. This can include whether the application is installed as well as details about its configuration.  

 **General configuration item**  
 A configuration item to determine compliance for general settings and objects, where their existence does not depend on the operating system, an application, or a software update.  

 **Software updates configuration item**  
 A configuration item to determine compliance of software updates using the software updates feature in Configuration Manager.  

 You cannot import, create, or configure software updates configuration items in the **Desired Configuration Management** node. Instead, these are made available to configuration baselines through the software updates feature when software updates are downloaded. This means that software updates configuration items can be selected to be included in configuration baselines, although they are not displayed under the **Configuration Items** node.  

 The other configuration items can be imported, created, and configured with the Configuration Manager console. These configuration items display a number of properties, which include the following:  

-   General  

-   Objects  

-   Settings  

-   Windows version  

-   Applicability  

-   Detection method  

 The properties that are available to each configuration item depend on the configuration item type. For example, you can configure an operating system configuration item to check for the exact version of the operating system. This property is not applicable to the other configuration items, so you do not see the Windows Version property that is available for other configuration items. The following table lists the configurable properties of a configuration item in Configuration Manager, and it shows whether the configurable property is available for each configuration item type.  

||||  
|-|-|-|  
|Key:|√ = Available property|Ø = Property not available|  

|Configuration Item Type|General|Windows Version|Objects|Settings|Detection Method|Applicability|Security|  
|-----------------------------|-------------|---------------------|-------------|--------------|----------------------|-------------------|--------------|  
|General|√|Ø|√|√|Ø|√|√|  
|Application|√|Ø|√|√|√|√|√|  
|Operating System|√|√|√|√|Ø|Ø|√|  
|Software Updates|√|Ø|Ø|Ø|Ø|Ø|√|  

 With the exception of software updates configuration items, you can view and edit the properties of each configuration item in the **Configuration Items** node under **Desired Configuration Management** in the Configuration Manager console. Use the **Software Updates** node to view and edit software updates configuration items.  

 In addition to the configurable properties of a configuration item in the **Desired Configuration Management** node, you also see displayed audit information in the **General** properties, which shows when the configuration item was created, when it was last edited, and by whom. Additionally, a **Relationships** property tab shows how the configuration item relates to other configuration items and configuration baselines.  

### Child Configuration Item  
 A child configuration item is a copy of a configuration item that continues to inherit the properties of the original configuration item. You cannot modify the child configuration item's inherited objects and settings with their validation criteria, but you can add additional validation criteria to the inherited objects and settings, and you can also add new objects and settings to the child configuration item. The usual purpose for creating and editing a child configuration item is that it refines the original configuration item to meet your business requirements.  

 Because of the dependency relationship of properties that are inherited from the parent to the child configuration item, modifying the original configuration item affects the child configuration item.  

 Child configuration items are appropriate when you have imported configuration data from a Best Practices configuration baseline and you want to be able to update the configuration data when new versions are released that will continue to pass their properties onto the child configuration item.  

 Another scenario for using child configuration item is when you need to retain inheritance for precise administration. For example, you can use a child configuration item if you have a configuration item that defines a corporate security policy that all computers must comply with, but your finance department computers are subject to additional security requirements. In this situation, you might create a child configuration item from the corporate security policy configuration item. The child configuration item inherits all the properties from the corporate security policy, but it is edited to contain the additional security requirements. If the corporate security policy changed, the original configuration item could be modified without having to also modify the configuration item for the computers in the finance department. Similarly, if the requirements for the finance department computers changed, only the child configuration item would need to be modified and not the original configuration item that defines the corporate security policy.  

### Duplicate Configuration Item  
 A duplicate configuration item is an exact copy of another configuration item that does not retain any relationship to the original configuration item. You can therefore use a duplicate configuration item as a template to modify just a few properties and independently retain both configuration items, or you can use it when you have imported a read-only configuration item (for example, from a Best Practices configuration baseline) and want to use the configuration item with modification and not retain any inheritance from the original configuration item.  

 Additionally, if you want to use an imported configuration item but delete from it objects or settings (or their related validation criteria), your only editing choice is to create a duplicate configuration item and edit that duplicate configuration item accordingly.  

## See Also  
 [Configuration Manager Compliance Settings (DCM)](../../develop/compliance/compliance-settings-dcm.md)
