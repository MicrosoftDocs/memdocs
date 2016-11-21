---
title: "Management tasks for System Center Configuration Manager applications | Microsoft Docs"
description: "Manage System Center Configuration Manager applications and deployment types."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c4041e21-21ff-4d95-ab05-14007e0047cf
caps.latest.revision: 8
author: robstackmsftms.author: robstack
manager: angrobe

---
# Management tasks for System Center Configuration Manager applications*Applies to: System Center Configuration Manager (Current Branch)*
Use the information in this topic to help you manage System Center Configuration Manager applications and deployment types.  

For help creating applications and deployment types, see [Create applications](../../apps/deploy-use/create-applications.md).  

> [!IMPORTANT]  
>  Depending on the type of application or deployment type, some of the management options might not be available.  

##  Manage applications  
 In the **Software Library** workspace, expand **Application Management** > **Applications**, select the application to manage, and then select a management task.  

|Task|Details|  
|----------|-------------|  
|**Manage Access Accounts**|Opens the **Manage Access Accounts** dialog box where you can specify the level of access that is allowed for the content that is associated with the selected application.|  
|**Create Prestage Content File**|Opens the **Create Prestaged Content File Wizard** that helps you to manage the distribution of content to remote distribution points. When the scheduling and throttling does not provide a valid solution for the remote distribution point, you can prestage the content on the distribution point<br /><br /> See [Manage content and content infrastructure](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|**Revision History**|Opens the **Application Revision History** dialog box that allows you to view the properties of revisions that were made to this application, delete old application revisions and restore old versions of this application.<br /><br /> See [How to revise and supersede applications](../../apps/deploy-use/revise-and-supersede-applications.md).|  
|**Create Deployment Type**|Opens the **Create Deployment Type Wizard** that allows you to add a new deployment type to the selected application.<br /><br /> See [Create applications](../../apps/deploy-use/create-applications.md).|  
|**Update Statistics**|Updates the information that is displayed in the **Deployments** node of the **Monitoring** workspace about the deployments of this application.<br /><br /> See [Monitor applications from the System Center Configuration Manager console](../../apps/deploy-use/monitor-applications-from-the-console.md).|  
|**Reinstate**|This option reinstates an application that was retired by using the **Retire** management task.|  
|**Retire**|When you retire an application, it is no longer available for deployment but the application and any deployments of the application are not deleted. Existing copies of this application that were installed on client computers will not be removed. Any revisions to the application will be deleted from Configuration Manager after 60 days. However, any installed copies of the application are not removed.<br /><br /> To delete an application, you must first retire the application, delete any deployments, remove references to it by other deployments, and then delete all of its revisions.<br /><br /> See [Revise and supersede applications](../../apps/deploy-use/revise-and-supersede-applications.md).|  
|**Export**|Opens the **Export Application Wizard** that allows you to export the selected applications to a .zip file that you can then archive or install on another site. If you choose to export application content, a folder will be created and will contain the content.<br /><br /> You can also export application dependencies, supersedence relationships and conditions and content for the application and its dependencies.<br /><br /> The Windows PowerShell cmdlet, **Export-CMApplication**, performs the same function. For more information, see [http://go.microsoft.com/fwlink/p/?LinkID=258880](http://go.microsoft.com/fwlink/p/?LinkID=258880) in the Microsoft System Center 2012 Configuration Manager SP1 Cmdlet Reference documentation.|  
|**Delete**|Deletes the currently selected application.<br /><br /> You cannot delete an application if other applications are dependent on it, if it has an active deployment, or if it has dependent task sequences.|  
|**Simulate Deployment**|Opens the **Simulate Application Deployment Wizard** where you can test the results of an application deployment to computers without installing or uninstalling the application.<br /><br /> See [Simulate application deployments](../../apps/deploy-use/simulate-application-deployments.md).|  
|**Deploy**|Opens the **Deploy Software Wizard** where you can deploy the selected application to collections of computers in your hierarchy.<br /><br /> See [Deploy applications](../../apps/deploy-use/deploy-applications.md).|  
|**Distribute Content**|Opens the **Distribute Content Wizard** where you can copy the content for the selected application to distribution points in your hierarchy.<br /><br /> See [Manage content and content infrastructure](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|**View Relationships**|Displays a graphical diagram showing the relationships of the selected applications to other applications. Choose from one of the following:<br><br> - **Dependency** – Displays the applications that are dependent on, and the applications that the selected application depends on.<br>-                    **Supersedence** – Displays the applications that are superseded, and applications that the selected item is superseded by.<br>- **Global Conditions** – Displays the global conditions that are referenced by this application.<br /><br /> See [Revise and supersede applications](../../apps/deploy-use/revise-and-supersede-applications.md) and [Create global conditions](../../apps/deploy-use/create-global-conditions.md).|  

##  Manage deployment types  
 In the **Software Library** workspace, expand **Application Management**, select **Applications**, select the application that contains the deployment type that you want to manage, in the details pane, click the **Deployment Types** tab, select the deployment type that you want to manage and then select a management task.  

|Task|Details|  
|----------|-------------|  
|**Increase Priority**|Increases the priority of the selected deployment type. Deployment types are evaluated in order. When a deployment type meets the specified requirements, it will be run and then no further deployment types on the priority list will be evaluated.|  
|**Decrease Priority**|Decreases the priority of the selected deployment type.|  
|**Delete**|Deletes the selected deployment type.<br><br>You cannot delete a deployment type if it is referenced by a deployment type in another application.<br>To delete a deployment type, you must remove any dependencies to the deployment type that are contained in other deployment types.<br>Additionally, you must also remove previous revisions of any application that contains a deployment type that references the deployment type that you want to delete.|  
|**Update Content**|Refreshes the content for the selected deployment type.<br /><br /> When you start this wizard for a deployment type that contains a virtual application, the **Update Content Wizard** is started. This wizard allows you to modify publishing options and requirement rules for the selected virtual application. For more information, see [Create applications](../../apps/deploy-use/create-applications.md).<br /><br /> When you refresh the content of a deployment type, a new revision of the application is created. This might cause client devices to be updated with the new application.|  
