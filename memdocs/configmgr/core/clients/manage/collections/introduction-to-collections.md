---
title: Collections introduction
titleSuffix: Configuration Manager
description: Get an introduction to using collections in Configuration Manager.
ms.date: 12/01/2021
ms.subservice: client-mgt
ms.service: configuration-manager
ms.topic: conceptual
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Introduction to collections in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Collections help you organize resources into manageable units. You can create collections to match your client management needs, and to perform operations on multiple resources at one time. 

Most management tasks rely on or require using one or more collections. Although you can use the built-in collection of All Systems, using it for management tasks is not a best practice. Create custom collections to more specifically identify the devices or users for a task.  

 Built-in and custom collections appear in the **User Collections** and **Device Collections** nodes in the **Assets and Compliance** workspace in the Configuration Manager console.  

 Collections that you have recently viewed appear in the **Users** node and in the **Devices** node in the **Assets and Compliance** workspace.  

Here are some examples of collection use:  

|Operation|Example|  
|---------|-------|  
|Grouping resources|You can create collections that  group resources based on your organization's hierarchy.<br /><br /> For example, you could create a collection of all computers in the "London Headquarters" Active Directory Organizational Unit (OU). For more information about how to create this type of collection, see [How to create collections](../../../../core/clients/manage/collections/create-collections.md).<br /><br /> You could  use this collection for operations such as configuring Endpoint Protection settings, configuring device power management settings, or installing the Configuration Manager client.|  
|Application deployment|You can create a collection of all computers that do not have Microsoft Microsoft 365 Apps installed and then deploy it to all computers in that collection.<br /><br /> You can also use application requirements to perform this task. For more information, see [How to create applications with Configuration Manager](../../../../apps/deploy-use/create-applications.md).|  
|[Managing client settings](../../../../core/clients/deploy/about-client-settings.md)|Although the default client settings in Configuration Manager apply to all devices and all users, you can create custom client settings that apply to a collection of devices or a collection of users.<br /><br /> For example, if you want remote control to be available on all but a few devices, configure the default client settings to allow remote control and then configure custom client settings that do not allow remote control, and deploy those to the collection of exceptional clients. |  
|[Power management](../power/introduction-to-power-management.md)|You can configure specific power settings per collection.|  
|[Role-based administration](../../../../core/servers/deploy/configure/configure-role-based-administration.md)|Use collections to control which groups of users have access to various functionality in the Configuration Manager console.|  
|[Maintenance Windows](../../../../core/clients/manage/collections/use-maintenance-windows.md)|With maintenance windows you can define a time period when various Configuration Manager operations can be carried out on members of a device collection. |  


## Collection types in Configuration Manager  
 Configuration Manager has built-in collections for common operations, and you can also create custom collections.   

### Built-in collections  
 By default, Configuration Manager includes the following collections, which cannot be modified.  

|**Collection name**|Description|  
|-------------------------|-----------------|  
|**All User Groups**|Contains the user groups that are discovered by using Active Directory Security Group Discovery.|  
|**All Users**|Contains the users who are discovered by using Active Directory User Discovery.|  
|**All Users and User Groups**|Contains the All Users and the All User Groups collections. This collection contains the largest scope of user and user group resources.|  
|**All Desktop and Server Clients**|Contains the server and desktop devices that have the Configuration Manager client installed. Membership is maintained by Heartbeat Discovery.|  
|**All Mobile Devices**|Contains the mobile devices that are managed by Configuration Manager. Membership is restricted to those mobile devices that are successfully assigned to a site or discovered by the Exchange Server connector.|  
|**All Systems**|Contains the All Desktop and Server Clients, the All Mobile Devices, and the All Unknown Computers collections, and all mobile devices that are enrolled by Microsoft Intune. This collection contains the largest scope of device resources.|  
|**All Unknown Computers**|Contains generic computer records for multiple computer platforms. You can use this collection to deploy an operating system by using a task sequence and PXE boot, bootable media, or prestaged media.| 
|**Co-management Eligible Devices**|  Contains devices that meet the client prerequisites and are eligible for co-management enrollment (added in version 2111). <!--12377291-->|

### Custom collections  
 When you create a custom collection in Configuration Manager, the membership of that collection is determined by one or more collection rules, as described in [How to create collections](../../../../core/clients/manage/collections/create-collections.md). 

