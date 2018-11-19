---
title: Manage collections
titleSuffix: Configuration Manager
description: Do common collections management tasks in Configuration Manager.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: e102fd1a-76df-4d8e-b1b0-10ee18318f67
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# How to manage collections in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Use the overview information in this article to help you perform management tasks for collections in Configuration Manager.  

> [!NOTE]  
>  For information about how to create Configuration Manager collections, see [How to create collections](/sccm/core/clients/manage/collections/create-collections).  



## <a name="bkmk_device"></a> How to manage device collections  

 In the **Assets and Compliance** workspace, select **Device Collections**, select the collection to manage, and then select a management task.  


#### Show Members
 Displays all of the resources that are members of the selected collection in a temporary node under the **Devices** node.


#### Add Selected Items
 Provides the following options: 

 - **Add Selected Items to Existing Device Collection**: Opens the **Select Collection** dialog box. Select the collection to which you want to add the members of the selected collection. The selected collection is included in this collection by using an **Include Collections** membership rule.  

 - **Add Selected Items to New Device Collection**: Opens the **Create Device Collection Wizard** where you can create a new collection. The selected collection is included in this collection by using an **Include Collections** membership rule.  


 For more information, see [How to create collections](/sccm/core/clients/manage/collections/create-collections).


#### Install Client
 Opens the **Install Client Wizard**. This wizard uses client push installation to install a Configuration Manager client on all computers in the selected collection. For more information, see [Client push installation](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_ClientPush).


#### Run Script
 Opens the **Run Script** wizard to run a PowerShell script on all of the clients in the collection. For more information, see [Create and run PowerShell scripts](/sccm/apps/deploy-use/create-deploy-scripts).


#### Manage Affinity Requests
 Opens the **Manage User Device Affinity Requests** dialog box. Approve or reject pending requests to establish user device affinities for devices in the selected collection. For more information, see [Link users and devices with user device affinity](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity)


#### Clear Required PXE Deployments
 Clears any required PXE boot deployments from all members of the selected collection. For more information, see [Use PXE to deploy Windows over the network](/sccm/osd/deploy-use/use-pxe-to-deploy-windows-over-the-network).


#### Update Membership
 Evaluates the membership for the selected collection. For collections with many members, this update might take some time to finish. Use the **Refresh** action to update the display with the new collections members after the update is completed.


#### Add Resources
 Opens the **Add Resources to Collection** dialog box. Search for new resources to add to the selected collection. The icon for the selected collection displays an hourglass symbol while the update is in progress.


#### Client Notification
 For more information, see [Client notifications](/sccm/core/clients/manage/client-notification).


#### Endpoint Protection
 For more information, see [Client notifications](/sccm/core/clients/manage/client-notification).


#### Export
 Opens the **Export Collection Wizard** that helps you export this collection to a Managed Object Format (MOF) file. This file can then be archived or imported at another Configuration Manager site. When you export a collection, referenced collections aren't exported. A referenced collection is referenced by the selected collection through the use of an **Include** or **Exclude** rule.


#### Copy
 Creates a copy of the selected collection. The new collection uses the selected collection as a limiting collection.


#### Refresh
 Refresh the view.


#### Delete
 Deletes the selected collection. You can also delete all of the resources in the collection from the site database. 

 You can't delete the collections that are built into Configuration Manager. For a list of the built-in collections, see [Introduction to collections](/sccm/core/clients/manage/collections/introduction-to-collections#built-in-collections).


#### Simulate Deployment
 Opens the **Simulate Application Deployment Wizard**. This wizard lets you test the results of an application deployment without installing or uninstalling the application. For more information, see [How to simulate application deployments](/sccm/apps/deploy-use/simulate-application-deployments).


#### Deploy
 Displays the following options:  

 - **Application**: Opens the **Deploy Software Wizard**. Select and configure an application deployment to the selected collection. For more information, see [How to deploy applications](/sccm/apps/deploy-use/deploy-applications).  

 - **Program**: Opens the **Deploy Software Wizard**. Select and configure a package and program deployment to the selected collection. For more information, see [Packages and programs](/sccm/apps/deploy-use/packages-and-programs).  

 - **Configuration Baseline**: Opens the **Deploy Configuration Baselines** dialog box. Configure the deployment of one or more configuration baselines to the selected collection. For more information, see [How to deploy configuration baselines](/sccm/compliance/deploy-use/deploy-configuration-baselines).  

 - **Task Sequence**: Opens the **Deploy Software Wizard**. Select and configure a task sequence deployment to the selected collection. For more information, see [Manage task sequences to automate tasks](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_DeployTS).  

 - **Software Updates**: Opens the **Deploy Software Updates Wizard**. Configure the deployment of software updates to resources in the selected collection. For more information, see [Manage software updates](/sccm/sum/understand/software-updates-introduction).  


#### Clear Server Group Deployment Locks
 Manually release all server group deployment locks for the collection. For more information, see [Service a server group](/sccm/sum/deploy-use/service-a-server-group).


#### Move
 Move the selected collection to another folder in the **Device Collections** node. 


#### Properties
 For more information, see [Collection properties](#BKMK_CollProp).  



## <a name="bkmk_user"></a> How to manage user collections  

 In the **Assets and Compliance** workspace, select **User Collections**, select the collection to manage, and then select a management task.  

 > [!Note]  
 > The following actions are available on user collections, but the behaviors are the same as with device collections. Other than they apply to user collections and the users within. For more information, see the corresponding action under [How to manage device collections](#bkmk_device).  

 - **Show Members**  
 - **Add Selected Items**  
     - **Add Selected Items to Existing User Collection**  
     - **Add Selected Items to New User Collection**  
 - **Manage Affinity Requests**  
 - **Update Membership**  
 - **Add Resources**  
 - **Export**  
 - **Copy**  
 - **Refresh**  
 - **Delete**  
 - **Simulate Deployment**  
 - **Deploy**  
     - **Application**  
     - **Program**  
     - **Configuration Baseline**   
 - **Move**  
 - **Properties**



##  <a name="BKMK_CollProp"></a> Collection properties  

 When you open the **Properties** dialog box for a collection, view and configure the following options:  

#### General
 View and configure general information about the selected collection including the collection name and the limiting collection.

#### Membership Rules
 Configure the membership rules that define the membership of this collection. For more information, see [How to create collections](/sccm/core/clients/manage/collections/create-collections).  

#### Power Management
 Configure power management plans that you've assigned to computers in the selected collection. For more information, see [Introduction to power management](/sccm/core/clients/manage/power/introduction-to-power-management).  

#### Deployments
 Displays any software that you've deployed to members of the selected collection.  

#### Maintenance Windows
 View and configure maintenance windows that are applied to members of the selected collection. For more information, see [How to use maintenance windows](/sccm/core/clients/manage/collections/use-maintenance-windows).

#### Collection Variables
 Configure variables that apply to this collection and can be used by task sequences. For more information, see [How to set task sequence variables](/sccm/osd/understand/using-task-sequence-variables#bkmk_set).  

#### Distribution Point Groups
 Associate one or more distribution point groups to members of the selected collection. For more information, see [Manage content and content infrastructure](/sccm/core/servers/deploy/configure/manage-content-and-content-infrastructure).

#### Security
 Displays the administrative users who have permissions for the selected collection from associated roles and security scopes. For more information, see [Fundamentals of role-based administration](/sccm/core/understand/fundamentals-of-role-based-administration).  

#### Alerts 
 Configure when alerts are generated for client status and Endpoint Protection. For more information, see [How to configure client status](/sccm/core/clients/deploy/configure-client-status) and [How to monitor Endpoint Protection](/sccm/protect/deploy-use/monitor-endpoint-protection).  
