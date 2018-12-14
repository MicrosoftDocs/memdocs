---
title: "Revise and supersede applications"
titleSuffix: "Configuration Manager"
description: "Learn how to work with System Center Configuration Manager application versions and supersede applications."
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 30170d70-489f-47f7-bebf-9ed0115db26b
author: aczechowski
manager: dougeby
ms.author: aaroncz
---
# Revise and supersede applications in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
In this topic, you'll learn how to work with System Center Configuration Manager application versions and how to supersede applications with a new version.  

##  Application revisions  
 When you make revisions to an application or to a deployment type that is contained in an application, Configuration Manager creates a new revision of the application. You can display the history of each application revision. You can also view its properties, restore a previous revision of an application, or delete an old revision.  

### To display an application revision history  

1.  In the Configuration Manager console, choose **Software Library** > **Application Management** > **Applications**, and then choose the application that you want.  

3.  On the **Home** tab, in the **Application** group, choose **Revision History** to open the **Application Revision History** dialog box.  

### To view an application revision  

1.  In the **Application Revision History** dialog box, select an application revision, and then choose **View**.  

2.  In the **Properties** dialog box, examine the properties of the selected application.  

    > [!NOTE]  
    >  The application properties that are displayed are read-only.  

3.  Close the **Properties** dialog box.  

### To restore an application revision  

1.  In the **Application Revision History** dialog box, select an application revision, and then choose **Restore**.  

2.  In the **Confirm Revision Restore** dialog box, choose **Yes** to restore the selected application revision.  

### To delete an application revision  

1.  In the **Application Revision History** dialog box, select an application revision, and then choose **Delete**.  

2.  In the **Delete Application Revision** dialog box, choose **Yes**.  

> [!IMPORTANT]  
>  You can only delete the current application revision if the application is retired and has no references.  

##  Application supersedence  
 Application management in Configuration Manager lets you upgrade or replace existing applications by using a supersedence relationship. When you supersede an application, you can specify a new deployment type to replace the deployment type of the superseded application and also decide whether to upgrade or uninstall the superseded application before the superseding application is installed.  

> [!IMPORTANT]  
>  When the option to uninstall the superseded deployment type is selected, a deployment type cannot be superseded by a deployment type that was deployed to a different collection type.  For example, a deployment type that was deployed to a device collection cannot be superseded by a deployment type that was deployed to a user collection if the option to uninstall the superseded deployment type is selected.  

### Decide whether to upgrade or replace an application  
 You specify whether to replace or upgrade an app in the **Specify Supersedence Relationship** dialog box of the application properties dialog box. The type of supersedence depends on whether you check the **Uninstall** option in this dialog box:  

-   If you want to update to a newer version of the same application (with the same application ID), **do not** check **Uninstall**.  

-   If you want to change to a different application (with a different application ID), check **Uninstall**. You need to remove the superseded version of the application.  

### Supersede dependent applications  
 In this example, **master application** refers to the app that you are deploying that has the dependencies.  

 You can create a supersedence relationship that updates the dependent application to a new version.  

1. Ensure that the new dependent application and the original dependent application are in the same dependency group of the master application.  

2. Create a supersedence relationship that supersedes the original dependent application with the new dependent application.  

   During new installations of the master application, the new dependent application is installed. Existing installations of the master application are updated with the new dependent application.  

   The end result is that all deployments of the master application use the new dependent application.  

### Further considerations  

-   You can specify multiple supersedence relationships for dependent applications. The highest dependent application in the supersedence chain gets installed.  

-   Dependent applications must be deployed to the device where the master application is installed or the dependent application won't get installed.  

-   For new installations of the master application, when you have multiple dependencies, the dependency order determines which version of the dependent application gets installed.  

### To specify a supersedence relationship  

1.  In the Configuration Manager console, choose **Software Library** > **Application Management** > **Applications**, and then choose the application that supersedes another application.  

3.  On the **Home** tab, in the **Properties** group, choose **Properties** to open the application name **Properties** dialog box.  

4.  On the **Supersedence** tab of the *<Application Name\>* **Properties** dialog box, choose **Add**.  

5.  In the **Specify Supersedence Relationship** dialog box, click **Browse**.  

6.  In the **Choose Application** dialog box, choose the application that you want to supersede, and then choose **OK**.  

7.  In the **Specify Supersedence Relationship** dialog box, select the deployment type that replaces the deployment type of the superseded application.  

    > [!NOTE]  
    >  By default, the new deployment type doesn't uninstall the deployment type of the superseded application. This scenario is commonly used when you want to deploy an upgrade to an existing application. Select **Uninstall** to remove the existing deployment type before the new deployment type is installed. If you decide to upgrade an application, make sure that you test this in a lab environment first.  

8.  Choose **OK** to close the **Specify Supersedence Relationship** dialog box.  

9. Choose **OK** to close the *<Application Name\>* **Properties** dialog box.  

### To display applications that supersede the current application  

1.  In the Configuration Manager console, choose **Software Library**.  

2.  In the **Software Library** workspace, expand **Application Management**, choose **Applications**, and then choose the application that you want.  

3.  On the **Home** tab, in the **Properties** group, choose **Properties** to open the *<Application Name\>* **Properties** dialog box.  

4.  On the **References** tab of the *<Application Name\>* **Properties** dialog box, choose **Applications that supersede this application** from the **Relationship type** drop-down list.  

5.  Review the list of applications that supersede the selected application, and then choose **OK** to close the *<Application Name\>* **Properties** dialog box.  
