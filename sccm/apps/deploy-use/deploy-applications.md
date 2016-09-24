---
title: "Deploy applications | System Center Configuration Manager"
ms.custom: na
ms.date: 03/11/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2629c376-ec43-4f0e-a78b-4223cc9302bf
caps.latest.revision: 10
caps.handback.revision: 0
author: robstackmsft

---
# Deploy applications with System Center Configuration Manager
 
  
 Before you can deploy a System Center Configuration Manager application, you must create at least one deployment type for the application. For more information about creating applications and deployment types, see [How to create applications with System Center Configuration Manager](../../apps/deploy-use/create-applications.md).  
  
> [!IMPORTANT]  
>  You can deploy (install/uninstall) required applications, but not packages or software updates. Mobile devices also do not support simulated deployments.  
>   
>  Additionally, mobile devices do not support user experience and scheduling settings in the Deploy Software Wizard.  
  
 You can also simulate an application deployment. This type of deployment tests the applicability of an application deployment to computers without installing or uninstalling the application. A simulated deployment evaluates the detection method, requirements and dependencies for a deployment type, and reports the results in the **Deployments** node of the **Monitoring** workspace. For more information, see [How to simulate application deployments with System Center Configuration Manager](../../apps/deploy-use/simulate-application-deployments.md).  
  
## Deploy an application  
  
1.  In the Configuration Manager console, click **Software Library** > **Application Management** > **Applications**.  
  
3.  In the **Applications** list, select the application that you want to deploy. Then, on the **Home** tab, in the **Deployment** group, click **Deploy**.  
  
4.  On the **General** page of the Deploy Software Wizard, specify the following information:  
  
    -   **Software** – This displays the application to deploy. You can click **Browse** to select a different application.  
  
    -   **Collection** – Click **Browse** to select the collection to deploy the application to.  
  
    -   **Use default distribution point groups associated to this collection** – Select this option if you want to store the application content on the collection's default distribution point group. If you have not associated the selected collection with a distribution point group, this option is not available.  
  
    -   **Automatically distribute content for dependencies** – If this is enabled and any of the deployment types in the application contain dependencies, then the dependent application content will be also sent to distribution points.  
  
        > [!IMPORTANT]  
        >  If you update the dependent application after the primary application has been deployed, any new content for the dependency will not be automatically distributed.  
  
    -   **Comments (optional)** – Optionally, enter a description of this deployment.  
  
5.  On the **Content** page, click **Add** to add the content that is associated with this deployment to distribution points or distribution point groups. If you have selected Use default distribution points associated to this collection on the **General** page, then this option will be automatically populated and can only be modified by a member of the **Application Administrator** security role.  
  
6.  Click **Next**.  
  
7.  On the **Deployment Settings** page of the Deploy Software Wizard, specify the following information:  
  
    -   **Action** – From the drop-down list, choose whether this deployment is intended to **Install** or **Uninstall** the application.  
  
        > [!NOTE]  
        >  If an application is deployed twice to a device, once with an action of **Install** and once with an action of **Uninstall**, the application deployment with an action of **Install** will take priority.  
        >   
        >  You cannot change the action of a deployment after it has been created.  
  
    -   **Purpose** – From the drop-down list, choose one of the following options:  
  
        -   **Available** - If the application is deployed to a user, the user sees the published application in Software Center and can install it on demand.  
  
        -   **Required** - The application is deployed automatically according to the configured schedule. However, a user can track the application deployment status if it is not hidden, and can install the application before the deadline from Software Center.  
  
            > [!NOTE]  
            >  When the deployment action is set to **Uninstall**, the deployment purpose is automatically set to **Required** and cannot be changed.  
  
    -   Deploy automatically according to schedule whether or not a user is logged on – If the deployment is to a user, select this option to deploy the application to the user’s primary devices. This setting does not require the user to log on before the deployment runs. Do not select this option if the user must provide input to complete the installation. This option is only available when the deployment has a purpose of **Required**.  
  
    -   **Send wake-up packets** – If the deployment purpose is set to **Required** and this option is selected, a wake-up packet is sent to computers before the deployment is installed to wake the computer from sleep at the installation deadline time. Before you can use this option, computers and networks must be configured for Wake On LAN.  
  
    -   **Allow clients on a metered Internet connection to download content after the installation deadline, which might incur additional costs** – This option is only available for deployments with a purpose of **Required**.  
  
    -   **Require administrator approval if users request this application** – If this option is selected, the administrator must approve any user requests for the application before it can be installed. This option is unavailable when the deployment purpose is **Required** or when the application is deployed to a device collection.  
  
        > [!NOTE]  
        >  Application approval requests are displayed in the **Approval Requests** node, under **Application Management** in the **Software Library** workspace. If an approval request is not approved within 45 days, it will be removed. Additionally, reinstalling the Configuration Manager client might cancel any pending approval requests.  
  
    -   **Automatically upgrade any superseded version of this application** – If this option is selected, any superseded versions of the application will be upgraded with the superseding application.  
  
8.  On the **Scheduling** page of the Deploy Software Wizard, configure when this application will be deployed or made available to client devices.  
    The options on this page will differ depending on whether the deployment action is set to **Available** or **Required**.  
  
9. If the application you are deploying supersedes another application, you can configure the installation deadline when users will receive the new application. Do this by using the setting **Installation Deadline** to upgrade users with superseded application.  
  
10. On the **User Experience** page of the Deploy Software Wizard, specify information about how users can interact with the application installation.  
  
     When you deploy applications to Windows Embedded devices that are write-filter enabled, you can specify to install the application on the temporary overlay and commit changes later, or to commit the changes at the installation deadline or during a maintenance window. When you commit changes at the installation deadline or during a maintenance window, a restart is required and the changes persist on the device.  
  
    > [!NOTE]  
    >  When you deploy an application to a Windows Embedded device, make sure that the device is a member of a collection that has a configured maintenance window. For more information about how maintenance windows are used when you deploy applications to Windows Embedded devices, see [Creating Windows Embedded applications with System Center Configuration Manager](../../apps/get-started/creating-windows-embedded-applications.md).  
    >   
    >  The options **Software Installation** and **System restart (if required to complete the installation)** are not used if the deployment purpose is set to **Available**. You can also configure the level of notification a user sees when the application is installed.  
  
11. On the **Alerts** page of the Deploy Software Wizard, configure how Configuration Manager and System Center Operations Manager will generate alerts for this deployment. You can configure thresholds for reporting alerts and turn off reporting for the duration of the deployment.  
  
12. (for iOS apps only) - On the **App Configuration Policies** page, click **New** to associate this deployment with an iOS app configuration policy (if you have created one). For more information about this type of policy, see [Configure iOS apps with app configuration policies in System Center Configuration Manager](../../apps/deploy-use/configure-ios-apps-with-app-configuration-policies.md).  
  
13. On the **Summary** page of the Deploy Software Wizard, review the actions that will be taken by this deployment, and then click **Next** to complete the wizard.  
  
 The new deployment will be displayed in the **Deployments** list in the **Deployments** node of the **Monitoring** workspace. You can edit the properties of this deployment or delete the deployment from the **Deployments** tab of the application detail pane.  
  
## Delete an application deployment  
  
1.  In the Configuration Manager console, click **Software Library**.  
  
2.  In the **Software Library** workspace, expand **Application Management**, and then click **Applications**.  
  
3.  In the **Applications** list, select the application that for which to delete the deployment.  
  
4.  In the **Deployments** tab of the *<application name\>* list, select the application deployment to delete. Then, in the **Deployment** tab, in the **Deployment** group, click **Delete**.  
  
 When you delete an application deployment, any instances of the application that have already been installed are not removed. To remove these applications, you must deploy the application to computers with the action **Uninstall**. If you delete an application deployment, or remove a resource from the collection you are deploying to, the application will no longer be visible in Software Center.  
  


