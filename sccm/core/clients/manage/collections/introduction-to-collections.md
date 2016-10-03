---
title: "Collections introduction | System Center Configuration Manager"
description: "Get an introduction to using collections in System Center Configuration Manager."
ms.custom: na
ms.date: 12/08/2015
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d17e1188-d277-438f-9236-db9cd213b421
caps.latest.revision: 8
author: barlanmsftms.author: barlanmanager: angrobe

---
# Introduction to collections in System Center Configuration Manager
Collections in System Center Configuration Manager provide you with the means to organize resources into manageable units, which then enable you to create an organized structure that logically represents the kinds of tasks that you want to perform. Collections are also used to perform Configuration Manager operations on multiple resources at one time. The following table shows some examples for how you might use collections in Configuration Manager:  

|||  
|-|-|  
|Operation|Example|  
|Grouping resources|You can create collections that logically group resources that are based on your organization's hierarchy.<br /><br /> For example, you could create a collection of all computers that reside in the "London Headquarters" Active Directory Organizational Unit (OU). For more information about how to create this type of collection, see [How to create collections in System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md).<br /><br /> You could then use this collection to perform operations such as configuring Endpoint Protection settings, configuring device power management settings, or installing the Configuration Manager client.|  
|Application deployment|You can create a collection of all computers that do not have Microsoft Office 2013 installed and then deploy this software to all computers in that collection.<br /><br /> You can also use application requirements to perform this task. For more information, see [How to create applications with System Center Configuration Manager](../../../../apps/deploy-use/create-applications.md).|  
|Managing client settings|Although the default client settings in Configuration Manager apply to all devices and all users, you can create custom client settings that apply to a collection of devices or a collection of users.<br /><br /> For example, if you want remote control to be available on all but a few devices, configure the default client settings to allow remote control and then configure custom client settings that do not allow remote control. Deploy these custom client settings to a collection that contains the computers that will not use remote control.<br /><br /> For more information about how to use collections for client settings, see [About client settings in System Center Configuration Manager](../../../../core/clients/deploy/about-client-settings.md).|  
|Power management|For each collection that you create, you can configure power settings such as how soon computers in the collection go into sleep mode when they are inactive.<br /><br /> For more information about how to use collections with power management, see [Introduction to power management](../power/introduction-to-power-management.md).|  
|Role-based administration|Collections can be used with role-based administration to control which groups of users have access to various functionality in the Configuration Manager console.<br /><br /> For more information about how configure collections for role-based administration, see [Configure role-based administration for System Center Configuration Manager](../../../../core/servers/deploy/configure/configure-role-based-administration.md).|  
|Maintenance Windows|Maintenance windows provide a means by which administrative users can define a time period when various Configuration Manager operations can be carried out on members of a device collection. You can use maintenance windows to help ensure that client configuration changes occur during periods that do not affect the productivity of the organization.<br /><br /> For more information about maintenance windows, see [How to use maintenance windows in System Center Configuration Manager](../../../../core/clients/manage/collections/use-maintenance-windows.md).|  

 Most management tasks rely on using one or more collections. For example, before you can deploy software updates to devices, you must identify a collection for the deployment of software updates. Although you can use the built-in collection of All Systems, using this collection for management tasks is not a best practice. In all but a testing environment, you will typically benefit from creating your own custom collections to more specifically identify the devices or users to manage.  

 Built-in and custom collections appear in the **User Collections** and **Device Collections** nodes in the **Assets and Compliance** workspace in the Configuration Manager console.  

 Collections that you have recently viewed appear in the **Users** node and in the **Devices** node in the **Assets and Compliance** workspace in the Configuration Manager console.  

## Collection types in Configuration Manager  
 Configuration Manager has some built-in collections that you can use for common operations. In addition, you can create your own collections that group resources specific to your business requirements.  

### Built-in collections  
 By default, Configuration Manager includes the following collections, which cannot be modified.  

|**Collection name**|Description|  
|-------------------------|-----------------|  
|**All User Groups**|Contains the user groups that are discovered by using Active Directory Security Group Discovery.|  
|**All Users**|Contains the users who are discovered by using Active Directory User Discovery.|  
|**All Users and User Groups**|Contains the All Users and the All User Groups collections. This collection cannot be modified and contains the largest scope of user and user group resources.|  
|**All Desktop and Server Clients**|Contains the server and desktop devices that have the Configuration Manager client installed. Membership is maintained by Heartbeat Discovery.|  
|**All Mobile Devices**|Contains the mobile devices that are managed by Configuration Manager. Membership is restricted to those mobile devices that are successfully assigned to a site or discovered by the Exchange Server connector.|  
|**All Systems**|Contains the All Desktop and Server Clients, the All Mobile Devices, the All Unknown Computers collection, and all mobile devices that are enrolled by Microsoft Intune.<br /><br /> This collection cannot be modified and contains the largest scope of device resources.|  
|**All Unknown Computers**|Contains generic computer records for multiple computer platforms. You can use this collection to deploy an operating system by using a task sequence and PXE boot, bootable media, or prestaged media.|  

### Custom collections  
 When you create a custom collection in Configuration Manager, the membership of that collection is determined by one or more collection rules. For information about how to configure collection rules, see [How to create collections in System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md). There are four rules that you can use:  

#### Direct rule  
 Direct rules let you to choose the users or computers that you want to add as members to a collection. This rule gives you direct control over which resources are members of the collection. The membership does not automatically change unless a resource is removed from Configuration Manager. Configuration Manager must discover the resources or you must import the resources before you can add them to a direct rule collection. Direct rule collections have a higher administrative overhead than query rule collections because you must modify this collection type manually.  

#### Query rule  
 Query rules dynamically update the membership of a collection based on a query that Configuration Manager runs on a schedule. For example, you can create a collection of users who are a member of the Human Resources organizational unit in Active Directory Domain Services. Unlike direct rule collections, this collection membership automatically updates when you add or remove new users to the Human Resources organizational unit. Query rules remove the administrative overhead of manually adding devices to the collection by using a direct rule. However, they do reduce the control you have over which computers are added to the collection. Examples of query based rules include:  

-   All users in a specified OU  

-   All computers that run Windows 8  

-   All computers that have more than 20GB of free disk space  

#### Include collections rule  
 The include collections rule lets you include the members of another collection in a Configuration Manager collection. Configuration Manager updates the membership of the current collection on a schedule if the membership of the included collection changes.  

#### Exclude collections rule  
 The exclude collections rule lets you exclude the members of another collection from a Configuration Manager collection. Configuration Manager updates the membership of the current collection on a schedule if the membership of the excluded collection changes.  

> [!NOTE]  
>  If a collection includes both include collection and exclude collection rules and there is a conflict, the exclude rule takes priority over the include rule.  

## Incremental collection updates  
 When you enable incremental updates for a collection, Configuration Manager periodically scans for new or changed resources from the previous collection evaluation and updates a collections membership with these resources, independently of a full collection evaluation. By default, when you enable incremental collection updates, it runs every 5 minutes and helps keep your collection data up-to-date without the overhead of a full collection evaluation.  

> [!NOTE]  
>  When you create a new collection, incremental updates are disabled by default.  
