---
title: "Manage collections"
titleSuffix: "Configuration Manager"
description: "Do common collections management tasks in System Center Configuration Manager."
ms.date: 4/25/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e102fd1a-76df-4d8e-b1b0-10ee18318f67
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# How to manage collections in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Use the overview information in this topic to help you perform management tasks for collections in System Center Configuration Manager.  

> [!NOTE]  
>  For information about how to create Configuration Manager collections, see [How to create collections in System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md).  

## How to manage device collections  
 In the **Assets and Compliance** workspace, select **Device Collections**, select the collection to manage, and then select a management task.  

 Use the following table for more information about the management tasks that might require some information before you select them.  

|Management task|Details|More information|  
|---------------------|-------------|----------------------|  
|**Show Members**|Displays all of the resources that are members of the selected collection in a temporary node under the **Devices** node.|No additional information.|  
|**Add Selected Items**|Provides the following options to perform one of the following actions:<br /><br /> - <br />                    **Add Selected Items to Existing Device Collection** - Opens the **Select Collection** dialog box where you can select the collection to which you want to add the members of the selected collection. The selected collection is included in this collection by using an **Include Collections** membership rule.<br /><br /> - **Add Selected Items to New Device Collection** - Opens the **Create Device Collection Wizard** where you can create a new collection. The selected collection is included in this collection by using an **Include Collections** membership rule.|[How to create collections in System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md)|  
|**Install Client**|Opens the **Install Client Wizard** which uses client push installation to install a Configuration Manager client on all computers in the selected collection.|[How to deploy clients to Windows computers](../../../../core/clients/deploy/deploy-clients-to-windows-computers.md)|  
|**Manage Affinity Requests**|Opens the **Manage User Device Affinity Requests** dialog box where you can approve or reject pending requests to establish user device affinities for devices in the selected collection.|[Link users and devices with user device affinity in System Center Configuration Manager](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)|  
|**Clear Required PXE Deployments**|Clears any required PXE boot deployments from all members of the selected collection.|[Introduction to operating system deployment](../../../../osd/understand/introduction-to-operating-system-deployment.md)|  
|**Update Membership**|Evaluates the membership for the selected collection. For collections with many members, this update might take some time to finish. Use the **Refresh** action to update the display with the new collections members after the update is completed.|No additional information.|  
|**Add Resources**|Opens the **Add Resources to Collection** dialog box where you can search for new resources to add to the selected collection.<br /><br /> The icon for the selected collection will display an hourglass symbol while the update is in progress.|No additional information.|  
|**Client Notification**|Instructs all clients in the selected device collection to download computer or user policy.|No additional information.|  
|**Endpoint Protection**|Performs a full or quick antimalware scan or downloads the latest antimalware definitions to computers in the selected collection.|[Endpoint Protection in System Center Configuration Manager](../../../../protect/deploy-use/endpoint-protection.md)|  
|**Export**|Opens the **Export Collection Wizard** that helps you export this collection to a Managed Object Format (MOF) file that can then be archived or used at another Configuration Manager site.<br /><br /> When you export a collection, collections that are referenced by the selected collection through the use of an **Include** or **Exclude** rule are not exported.|No additional information.|  
|**Copy**|Creates a copy of the selected collection. The new collection uses the selected collection as a limiting collection.|No additional information.|  
|**Delete**|Deletes the selected collection. You can also delete all of the resources in the collection from the site database.<br /><br /> You cannot delete the collections that are built into Configuration Manager.|For a list of the built-in collections, see [Introduction to collections in System Center Configuration Manager](../../../../core/clients/manage/collections/introduction-to-collections.md).|  
|**Simulate Deployment**|Opens the **Simulate Application Deployment Wizard** which lets you test the results of an application deployment without installing or uninstalling the application.|[How to simulate application deployments with System Center Configuration Manager](../../../../apps/deploy-use/simulate-application-deployments.md)|  
|**Deploy**|Displays the following options:<br /><br /> - <br />                    **Application** - Opens the **Deploy Software Wizard** where you can select and configure an application deployment to the selected collection.<br /><br /> - <br />                    **Program** - Opens the **Deploy Software Wizard** where you can select and configure a package and program deployment to the selected collection.<br /><br /> - **Configuration Baseline** - Opens the **Deploy Configuration Baselines** dialog box where you can configure the deployment of one or more configuration baselines to the selected collection.<br /><br /> - <br />                    **Task Sequence** - Opens the **Deploy Software Wizard** where you can select and configure a task sequence deployment to the selected collection.<br /><br /> - <br />                    **Software Updates** - Opens the **Deploy Software Updates Wizard** where you can configure the deployment of software updates to resources in the selected collection.|[How to deploy applications with System Center Configuration Manager](../../../../apps/deploy-use/deploy-applications.md)<br /><br /> [Packages and programs in System Center Configuration Manager](../../../../apps/deploy-use/packages-and-programs.md)<br /><br /> [How to deploy configuration baselines in System Center Configuration Manager](../../../../compliance/deploy-use/deploy-configuration-baselines.md)<br /><br /> [Manage task sequences to automate tasks in System Center Configuration Manager](../../../../osd/deploy-use/manage-task-sequences-to-automate-tasks.md)<br /><br /> [Manage software updates in System Center Configuration Manager](/sccm/sum/understand/software-updates-introduction)|  

## How to manage user collections  
 In the **Assets and Compliance** workspace, select **User Collections**, select the collection to manage, and then select a management task.  

 Use the following table for more information about the management tasks that might require some information before you select them.  

|Management task|Details|More information|  
|---------------------|-------------|----------------------|  
|**Show Members**|Displays all of the resources that are members of the selected collection in a temporary node under the **Users** node.|No additional information.|  
|**Add Selected Items**|This option lets you perform one of the following actions:<br /><br /> - <br />                    **Add Selected Items to Existing User Collection** - Opens the **Select Collection** dialog box where you can select the collection to which you want to add the members of the selected collection. The selected collection is included in this collection by using an **Include Collections** membership rule.<br /><br /> - **Add Selected Items to New User Collection** - Opens the **Create User Collection Wizard** where you can create a new collection. The selected collection is included in this collection by using an **Include Collections** membership rule.|[How to create collections in System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md)|  
|**Manage Affinity Requests**|Opens the **Manage User Device Affinity Requests** dialog box where you can approve or reject pending requests to establish user device affinities for users in the selected collection.|[Link users and devices with user device affinity in System Center Configuration Manager](../../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md)|  
|**Update Membership**|Evaluates the membership for the selected collection. For collections with many members, this update might take some time to finish. Use the **Refresh** action to update the display with the new collections members after the update is completed.<br /><br /> The icon for the selected collection will display an hourglass symbol while the update is in progress.|No additional information.|  
|**Add Resources**|Opens the **Add Resources to Collection** dialog box where you can search for new resources to add to the selected collection.|No additional information.|  
|**Export**|Opens the **Export Collection Wizard** that helps you to export this collection to a Managed Object Format (MOF) file that can then be archived or used at another Configuration Manager site.<br /><br /> When you export a collection, collections that are referenced by the selected collection through the use of an **Include** or **Exclude** rule are not exported.|No additional information.|  
|**Copy**|Creates a copy of the selected collection. The new collection uses the selected collection as a limiting collection.|No additional information.|  
|**Delete**|Deletes the selected collection. You can also delete all of the resources in the collection from the site database.<br /><br /> You cannot delete the collections that are built into Configuration Manager.|For a list of the built-in collections, see [Introduction to collections in System Center Configuration Manager](../../../../core/clients/manage/collections/introduction-to-collections.md).|  
|**Simulate Deployment**|Opens the **Simulate Application Deployment Wizard** which lets you test the results of an application deployment without installing or uninstalling the application.|[How to simulate application deployments with System Center Configuration Manager](../../../../apps/deploy-use/simulate-application-deployments.md)|  
|**Deploy**|Displays the following options:<br /><br /> - **Application** - Opens the **Deploy Software Wizard** where you can select and configure an application deployment to the selected collection.<br /><br /> - <br />                    **Program** - Opens the **Deploy Software Wizard** where you can select and configure a package and program deployment to the selected collection.<br /><br /> - **Configuration Baseline** - Opens the **Deploy Configuration Baselines** dialog box where you can configure the deployment of one or more configuration baselines to the selected collection.|[How to deploy applications with System Center Configuration Manager](../../../../apps/deploy-use/deploy-applications.md)<br /><br /> [Packages and programs in System Center Configuration Manager](../../../../apps/deploy-use/packages-and-programs.md)<br /><br /> [How to deploy configuration baselines in System Center Configuration Manager](../../../../compliance/deploy-use/deploy-configuration-baselines.md)|  

##  <a name="BKMK_CollProp"></a> Collection properties  
 When you open the **Properties** dialog box for a collection, you can view and configure the following properties for a collection.  

|Tab name|More information|  
|--------------|----------------------|  
|**General**|Lets you view and configure general information about the selected collection including the collection name and the limiting collection.|  
|**Membership Rules**|Lets you configure the membership rules that define the membership of this collection. For more information, see [How to create collections in System Center Configuration Manager](../../../../core/clients/manage/collections/create-collections.md).|  
|**Power Management**|Lets you configure power management plans that are assigned to computers in the selected collection. For more information, see [Introduction to power management](../../../../core/clients/manage/power/introduction-to-power-management.md).|  
|**Deployments**|Displays any software that has been deployed to members of the selected collection.|  
|**Maintenance Windows**|Lets you view and configure maintenance windows that are applied to members of the selected collection. For more information, see [How to use maintenance windows in System Center Configuration Manager](../../../../core/clients/manage/collections/use-maintenance-windows.md).|  
|**Collection Variables**|Lets you configure variables that apply to this collection and can be used by task sequences. For more information, see [Task sequence built-in variables](../../../../osd/understand/task-sequence-built-in-variables.md).|  
|**Distribution Point Groups**|Lets you associate one or more distribution point groups to members of the selected collection. For more information, see [Manage content and content infrastructure for System Center Configuration Manager](../../../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|**Security**|Displays the administrative users who have permissions for the selected collection from associated roles and security scopes.|  
|**Monitor**|Lets you configure when alerts are generated for client status and Endpoint Protection. For more information, see [How to configure client status in System Center Configuration Manager](../../../../core/clients/deploy/configure-client-status.md) and [How to monitor Endpoint Protection in System Center Configuration Manager](../../../../protect/deploy-use/monitor-endpoint-protection.md).|  
