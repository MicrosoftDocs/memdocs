---
title: "Introduction to application management"
titleSuffix: "Configuration Manager"
description: "Discover the basic information you’ll need to manage and deploy System Center Configuration Manager applications."
ms.custom: na
ms.date: 12/23/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-app
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 08f711ba-83bf-4b5f-9520-a0778c6ae7eb
caps.latest.revision: 18
author: mattbriggs
ms.author: mabrigg
manager: angrobe
experimental: true
experiment_id: "rob-table-161101"

---
# Introduction to application management in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

In this topic, you'll learn the basics you need to know before you start working with System Center Configuration Manager applications.  

> [!TIP]  
>  If you are already familiar with how to manage applications in Configuration Manager, you can skip this topic and move on to creating a sample application. See [Create and deploy an application with System Center Configuration Manager](../../apps/get-started/create-and-deploy-an-application.md).  

## What is an application?  
 Although *application* is a widely used term in computing, in Configuration Manager, it means something different. Think of an application like a box. This box contains one or more sets of installation files for a software package (known as a **deployment type**), plus instructions on how to deploy the software.  

 When the application is deployed to devices, **requirements** decide which deployment type is installed on the device.  

 You can do many more things with an application. You'll learn about these things as you read this guide. The following table introduces some concepts you'll need to know before you start to dig deeper:  

|Concept|Description|    
|-|-|  
|**Requirements**|In previous versions of Configuration Manager, you would often create a collection containing the devices you wanted to deploy an application to. Although you can still create a collection, with requirements you can specify more detailed criteria for an application deployment.<br /><br /> For example, you can specify that an application can only install on devices that run Windows 10. Then, you can deploy the application to your devices, but it will only install on devices that run Windows 10.<br /><br /> Configuration Manager evaluates requirements to determine whether an application and any of its deployment types will be installed. Then it determines the correct deployment type by which to install an application. Every seven days, by default, the requirement rules are reevaluated to ensure compliance according to the client setting **Schedule re-evaluation for deployments**.<br /><br /> For details, see [Create and deploy an application](../../apps/get-started/create-and-deploy-an-application.md).|  
|**Global conditions**|While requirements are used with a specific deployment type in a single application, you can also create global conditions. These are a library of predefined requirements that you can use with any application and deployment type.<br /><br /> Configuration Manager contains a set of built-in global conditions, and you can also create your own.<br /><br /> For details, see [Create global conditions](../../apps/deploy-use/create-global-conditions.md).|  
|**Simulated deployment**|Evaluates the requirements, detection method, and dependencies for an application. It reports the results without actually installing the application.<br /><br /> For details, see [Simulate application deployments](../../apps/deploy-use/simulate-application-deployments.md).|  
|**Deployment action**|Specifies whether you want to install, or uninstall (when supported), the application you are deploying.<br /><br /> For details, see [Deploy applications](../../apps/deploy-use/deploy-applications.md).|  
|**Deployment purpose**|Specifies whether the deployment app will  be **Required**, or **Available**.<br /><br /> **Required** means that the application is deployed automatically according to the schedule that has been set up. However, a user can track the application deployment status if it is not hidden, and can install the application before the deadline by using the Software Center.<br /><br /> **Available** means that if the application is deployed to a user, the user sees the published application in Software Center, and can request it on demand.<br /><br /> For details, see [Deploy applications](../../apps/deploy-use/deploy-applications.md).|  
|**Revisions**|When you make revisions to an application or to a deployment type that is contained in an application, Configuration Manager creates a new version of the application. You can display the history of each application revision, view its properties, restore a previous version of an application, or delete an old version.<br /><br /> For details, see [Update and retire applications](../../apps/deploy-use/update-and-retire-applications.md).|  
|**Detection method**|Detection methods are used to discover whether a deployed application is already installed. If the detection method indicates the application is installed, Configuration Manager does not attempt to install it again.<br /><br /> For details, see [Create applications](../../apps/deploy-use/create-applications.md).|  
|**Dependencies**|Dependencies define one or more deployment types from another application that must be installed before a deployment type is installed. You can set up the dependent deployment types to be installed automatically before a deployment type is installed.<br /><br /> For details, see [Create applications](../../apps/deploy-use/create-applications.md).|  
|**Supersedence**|Configuration Manager lets you upgrade or replace existing applications by using a supersedence relationship. When you supersede an application, you can specify a new deployment type to replace the deployment type of the superseded application. You can also decide whether to upgrade or uninstall the superseded application before the superseding application is installed.<br /><br /> For details, see [Create applications](../../apps/deploy-use/create-applications.md).|  
|**User-centric management**|Configuration Manager applications support user-centric management, letting you associate specific users with specific devices. Instead of having to remember the name of a user’s device, you can deploy apps to the user and to the device. This functionality can help you make sure that the most important apps are always available on each device that a specific user accesses. If a user acquires a new computer, you can automatically install the user’s apps on the device before they sign in.<br /><br /> For details, see [Link users and devices with user device affinity](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).|  

## What application types can you deploy?  
 Configuration Manager lets you deploy the following app types:  

- Windows Installer (*.msi file)
- Windows app package (*.appx, *.appxbundle)
- Windows app package (in the Windows Store)
- Microsoft Application Virtualization 4
- Microsoft Application Virtualization  5
- Windows Mobile Cabinet
- macOS  


Additionally, when you manage devices through Microsoft Intune or Configuration Manager on-premises device management, you can manage these further app types:

- Windows Phone app package (*.xap file)
- App Package for iOS (*.ipa file)
- App Package for Android (*.apk file)
- App Package for Android on Google Play
- Windows Phone app package (in the Windows Phone Store)
- Windows Installer through MDM
- Web Application



## State-based applications  
 Configuration Manager applications use state-based monitoring, by which you can track the last application deployment state for users and devices. The state messages display information about individual devices. For example, if an application is deployed to a collection of users, you can view the compliance state of the deployment and the deployment purpose in the Configuration Manager console. You can monitor the deployment of all software by using the **Monitoring** workspace in the Configuration Manager console. Software deployments include software updates, compliance settings, applications, task sequences, and packages and programs. For more information, see [Monitor applications](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

 Application deployments are regularly re-evaluated by Configuration Manager. For example:  

-   A deployed application is uninstalled by the end-user. At the next evaluation cycle, Configuration Manager detects that the application is not present, and reinstalls it.  

-   An application was not installed on a device because it failed to meet the requirements. Later, a change is made to the device and it now meets the requirements. Configuration Manager detects this change, and the application is installed.  


 You can set the re-evaluation interval for application deployments by using the **Schedule re-evaluation for deployments** client setting. For more information, see [About client settings](../../core/clients/deploy/about-client-settings.md).  

## Get started creating an application  
 If you want to jump right in and start to create an application, you'll find a walkthrough for creating a simple application in the [Create and deploy an application](../../apps/get-started/create-and-deploy-an-application.md) topic.  

 If you are familiar with the basics and looking for more detailed reference information about all the options available to you, start from [Create applications](/sccm/apps/deploy-use/create-applications).  

## Software Center and the Application Catalog  
 In previous versions of Configuration Manager, Software Center was used to install and schedule software installations, configure remote control settings, and set up power management. Users could connect to the Application Catalog to browse for and request software, set some preferences, and remotely wipe their mobile devices.  

 While these settings are still available in System Center Configuration Manager, a new version of Software Center is now available that allows you to browse for applications. You don't have to use the Application Catalog, which requires a Silverlight-enabled web browser. However, the Application Catalog website point and Application Catalog web service point site system roles are still required for user-available apps to appear in Software Center.  

 For more information, see [Plan for and configure application management](../../apps/plan-design/plan-for-and-configure-application-management.md).  

## Configuration Manager packages and programs  
 Configuration Manager continues to support packages and programs that were used in previous versions of the product. A deployment that uses packages and programs might be more suitable than a deployment that uses an application when you deploy any of the following:  

-   Scripts that do not install an application on a computer, such as a script to defragment the computer disk drive.  

-   “One-off” scripts that do not need to be continually monitored.  

-   Scripts that run on a recurring schedule and cannot use global evaluation.

 For more information, see [Packages and programs](../../apps/deploy-use/packages-and-programs.md).  
