---
title: Introduction to app management
titleSuffix: Configuration Manager
description: Discover the basic information you’ll need to manage and deploy Configuration Manager applications.
ms.date: 07/30/2018
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: 08f711ba-83bf-4b5f-9520-a0778c6ae7eb
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Introduction to application management in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

In this article, you'll learn the basics before you start working with Configuration Manager applications.  

> [!TIP]  
>  If you're already familiar with how to manage applications in Configuration Manager, skip this article. Move on to creating a sample application: [Create and deploy an application](/sccm/apps/get-started/create-and-deploy-an-application).  



## What is an application?  

Although *application* is a widely used term in computing, in Configuration Manager, it means something specific. Think of an application like a box. This box contains one or more sets of installation files for a software package (known as a *deployment type*), plus instructions on how to deploy the software.  

When you deploy the application to devices, **requirements** decide which deployment type Configuration Manager installs on the device.  

You can do many more things with an application. You'll learn about these things as you read this guide. The following sections introduce some concepts you'll need to know before you start to dig deeper:  

#### Deployment type
If the *application* is the box, then the *deployment type* is the set of contents in the box. An application needs at least one deployment type, as it determines how to install the app. Use more than one deployment type to configure different content and installation program for the same application. 

For example, your company has a line-of-business application called Astoria. The application developers provide the following ways of installing the app:
- Windows Installer package for full functionality on Windows 10 devices
- An App-V package for use in the terminal server farm
- An Android app package for mobile users  

You create a single application for Astoria in Configuration Manager. The application defines the high-level metadata about the app that's common across all installation methods and platforms. You then create three deployment types for the available installation methods, and deploy the application to all users. Based on the requirements and other configurations on the deployment types, Configuration Manager determines the right method in each use case. 

For more information, see [Create deployment types for the application](/sccm/apps/deploy-use/create-applications#bkmk_create-dt).

#### Requirements
In previous versions of Configuration Manager, you would create a collection of devices to deploy an application to. Although you can still create a collection, use *requirements* to specify more detailed criteria for an application deployment.

For example, specify that an application can only install on devices that run Windows 10. When you deploy the application to all of your devices, it only installs on devices that run Windows 10.

Configuration Manager evaluates requirements to determine whether it installs an application and any of its deployment types. Then it determines the correct deployment type by which to install an application. Every seven days, by default, the Configuration Manager client reevaluates requirement rules to determine compliance according to the client setting **Schedule re-evaluation for deployments**.

For more information, see [Create and deploy an application](/sccm/apps/get-started/create-and-deploy-an-application) and [Deployment type Requirements](/sccm/apps/deploy-use/create-applications#bkmk_dt-require).

#### Global conditions
While you use requirements with a specific deployment type in a single application, you can also create *global conditions*. These conditions are a library of predefined requirements that you can use with any application and deployment type. Configuration Manager includes a set of built-in global conditions, or you can create your own. 

For more information, see [Create global conditions](/sccm/apps/deploy-use/create-global-conditions).

#### Simulated deployment
A *simulated deployment* evaluates the requirements, detection method, and dependencies for an application. A client reports the results without actually installing the application. 

For more information, see [Simulate application deployments](/sccm/apps/deploy-use/simulate-application-deployments).  

#### Deployment action
A *deployment action* specifies whether you want to install or uninstall the application you're deploying. Not all deployment types support the uninstall action. 

For more information, see [Deploy applications](/sccm/apps/deploy-use/deploy-applications).  

#### Deployment purpose
The *deployment purpose* specifies whether the deployment app is **Required** or **Available**:  

- The client automatically installs a *required* deployment according to the schedule that you set. If the application isn't hidden, a user can track its deployment status. They can also use Software Center to install the application before the deadline.  

- If you deploy the application to a user as *available*, they see it in Software Center, and can request it on demand.  

For more information, see [Deploy applications](/sccm/apps/deploy-use/deploy-applications).  

#### Revisions
When you make *revisions* to an application or a deployment type, Configuration Manager creates a new version of the application. Take the following actions in the Configuration Manager console: 
- Display the history of each application revision
- View its properties
- Restore a previous version of an application
- Delete an old version

For more information, see [Update and retire applications](/sccm/apps/deploy-use/update-and-retire-applications).  

#### Detection method
Use *detection methods* to discover whether a device has already installed an application. If the detection method indicates the application is installed, Configuration Manager doesn't attempt to install it again.

For more information, see [Deployment type Detection Method options](/sccm/apps/deploy-use/create-applications##bkmk_dt-detect).

#### Dependencies
*Dependencies* define one or more deployment types from another application that the client must install before it installs this deployment type. 

For more information, see [Deployment type Dependencies](/sccm/apps/deploy-use/create-applications#bkmk_dt-depend).  

#### Supersedence
Configuration Manager lets you upgrade or replace existing applications by using a *supersedence* relationship. When you supersede an application, you specify a new deployment type to replace the deployment type of the superseded application. You can also decide whether to upgrade or uninstall the superseded application before the client installs the superseding application.

For more information, see [Application supersedence](/sccm/apps/deploy-use/revise-and-supersede-applications#application-supersedence).  

#### User-centric management
Configuration Manager applications support *user-centric management*, which lets you associate specific users with specific devices. Instead of having to remember the name of a user's device, deploy apps to the user and to the device. This functionality helps you make sure the most important apps are always available on each of the user's devices. If a user acquires a new computer, Configuration Manager automatically installs their apps on the device before they sign in. 

For more information, see [Link users and devices with user device affinity](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity).  



## What application types can you deploy?  

Configuration Manager lets you deploy the following app types:  

- Windows Installer (msi)  

- Windows app package (appx or appxbundle)  

    > [!Note]  
    > Starting in version 1806, this type includes the new Windows 10 app package (msix) and app bundle (msixbundle) formats.<!--1357427-->  

- Windows app package in the Microsoft Store  

- Microsoft App-V v4 and v5  

- macOS  


Additionally, when you manage devices through Microsoft Intune or Configuration Manager on-premises device management, manage these further app types:  

- Windows Phone app package (xap)  

- Windows Phone app package in the Microsoft Store  

- App package for iOS (ipa)  

- App Package for iOS from App Store  

- App package for Android (apk)  

- App package for Android on Google Play  

- Windows Installer through MDM (msi)  

- Web application



## State-based applications  

Configuration Manager applications use state-based monitoring. You can track the last application deployment state for users and devices. The state messages display information about individual devices. For example, if you deploy an application to a collection of users, you can view the compliance state of the deployment and the deployment purpose in the Configuration Manager console. Monitor the deployment of all software from the **Monitoring** workspace in the Configuration Manager console. For more information, see [Monitor applications](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

The Configuration Manager client regularly reevaluates application deployments. For example:  

- A user uninstalls a deployed application. At the next evaluation cycle, Configuration Manager detects that the app isn't present. The client then automatically reinstalls the app.  

- Configuration Manager didn't install an application on a device because it failed to meet the requirements. Later, a change is made to the device and it now meets the requirements. Configuration Manager detects this change, and the client installs the application.  

You can set the re-evaluation interval for application deployments. Use the **Schedule re-evaluation for deployments** client setting in the **Software Deployment** group. For more information, see [About client settings](/sccm/core/clients/deploy/about-client-settings#software-deployment).  



## Get started creating an application  

If you want to jump right in and create an application, you'll find a walkthrough in the [Create and deploy an application](/sccm/apps/get-started/create-and-deploy-an-application) article.  

If you're familiar with the basics and looking for more detailed reference information about all the available options, start to [Create applications](/sccm/apps/deploy-use/create-applications).  



## Software Center  

Software Center is a Windows application installed with the Configuration Manager client. Use it for the following actions:  
- Browse for and request applications deployed to the device or the user
- Install and schedule software installations
- View installation status for applications, software updates, and operating systems
- Configure remote control settings
- Set up power management

For more information, see the following articles:  
- [Plan for and configure application management](/sccm/apps/plan-design/plan-for-and-configure-application-management)
- [Software Center user guide](/sccm/core/understand/software-center)

> [!Note]  
> The Application Catalog web service point role is no longer required in 1806, but still a supported role. 
> 
> The Application Catalog website role isn't supported in version 1806. For more information, see [Removed and deprecated features](/sccm/core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures).  



## Packages and programs  

Configuration Manager continues to support packages and programs that were used in previous versions of the product. 

For more information, see [Packages and programs](/sccm/apps/deploy-use/packages-and-programs).  



## Next steps

Now that you understand the basic concepts of application management in Configuration Manager, continue to the following articles:
- [Create and deploy an example application](/sccm/apps/get-started/create-and-deploy-an-application)
- [Plan for and configure application management](/sccm/apps/plan-design/plan-for-and-configure-application-management)
- [Create applications](/sccm/apps/deploy-use/create-applications)
