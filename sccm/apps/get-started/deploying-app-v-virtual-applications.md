---
title: "Deploy App-V virtual applications"
titleSuffix: "Configuration Manager"
description: "See which considerations you must take into account when you create and deploy virtual applications."
ms.custom: na
ms.date: 02/16/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ddcad9f2-a542-4079-83ca-007d7cb44995
caps.latest.revision: 11
caps.handback.revision: 0
author: mattbriggsms.author: mabriggmanager: angrobe

---
# Deploy App-V virtual applications with System Center Configuration Manager*Applies to: System Center Configuration Manager (current branch)*
When you use Configuration Manager to manage virtual applications, you gain the following benefits:  

-   A single management infrastructure  

-   Scalability, deployment, and content distribution features, like collections and user device affinity  

-   Advanced application management features  

-   Operating system deployment, software and hardware inventory, software metering, and asset intelligence to support virtual applications  

For more information about how to create and sequence applications with Microsoft Application Virtualization (App-V), see [Application Virtualization](https://technet.microsoft.com/library/cc843848.aspx) in the TechNet Library.  

In addition to the other System Center Configuration Manager requirements and procedures for creating an application, you must take the following considerations into account when you create and deploy virtual applications:

-   To deploy virtual applications to computers, you must have the Configuration Manager client and App-V Client installed on your computers. Client devices can include desktop and portable computers, and Virtual Desktop Infrastructure (VDI) clients. The Configuration Manager and App-V Client software work together to deliver, locate, and launch virtual application packages. The Configuration Manager client manages the delivery of virtual application packages to the App-V Client. The App-V Client runs the virtual application on the client.  

-   To deploy a virtual application, you must first create the virtual application by using the App-V Application Virtualization Sequencer. The sequencer monitors the installation and setup process for an application and records the information that is needed for the application to run in a virtual environment. You can also use the sequencer to set which files and configurations apply to all users, and which configurations users can customize.  

-   When you sequence an application, you must save the package to a location that Configuration Manager can access. You can then create an application deployment that contains this virtual application.  

-   Configuration Manager does not support the use of the shared read-only cache feature of App-V.  

-   Configuration Manager supports the Shared Content Store feature in App-V 5.  

-   When you create a deployment type for a virtual application, Configuration Manager creates the deployment type by using the contents of the application manifest file. This is an XML file that has information about the virtual application. Additionally, Configuration Manager creates requirements for the deployment type based on the contents of the App-V .osd file that has information about the supported operating systems for the virtual application.  

-   To deploy virtual applications in Configuration Manager, client computers must have at minimum the App-V 4.6 SP1 or a later version of the client installed.  

-   Before you can successfully deploy virtual applications, you must update the App-V Client with the hotfix described in the Knowledge Base article [2645225](https://support.microsoft.com/kb/2645225).  

-   When you use connection groups in App-V 5.0, your deployed virtual applications can share the same file system and registry on client computers. Unlike standard virtual applications, these applications can share data with one another. Additionally, connection groups preserve user settings for the applications that they contain. App-V virtual environments in Configuration Manager are used to set up connection groups on client computers. Virtual environments are created or changed on client computers when the application is installed or when clients next evaluate their installed applications. You can prioritize these applications so that when multiple applications try to change a file system or registry value, the application that has the highest priority takes precedence. For more information, see [Create App-V virtual environments](../../apps/deploy-use/create-app-v-virtual-environments.md).  

##  Supported App-V versions  
 Configuration Manager supports the following versions of App-V:  

-   **App-V 4.6**: To use virtual applications in Configuration Manager, client computers must have the App-V 4.6 SP1, App-V 4.6 SP2, or App-V 4.6 SP3 client installed.  

     Before you can successfully deploy virtual applications, you must also update the App-V 4.6 SP1 client with the hotfix that is described in the Knowledge Base article [2645225](http://go.microsoft.com/fwlink/p/?LinkId=237322).  

-   **App-V 5, App-V 5.0 SP1, App-V 5.0 SP2, App-V 5.0 SP3, and App-V 5.1**: For App-V 5.0 SP2, you must install [Hotfix Package 5](https://support.microsoft.com/en-us/kb/2963211) or use App-V 5.0 SP3.  
-   **App-V 5.2**: This is built into Windows 10 Enterprise (Anniversary Update and later).

For more information about App-V in Windows 10, see the following topics:

- [What's new in App-V](https://technet.microsoft.com/itpro/windows/manage/appv-about-appv)
- [Getting Started with App-V for Windows 10](https://technet.microsoft.com/itpro/windows/manage/appv-getting-started)
- [Upgrading to App-V for Windows 10 from an existing installation](https://technet.microsoft.com/itpro/windows/manage/appv-upgrading-to-app-v-for-windows-10-from-an-existing-installation)

##  Steps to manage App-V virtual applications  
 To manage App-V virtual applications, follow these steps:  

1.   **Sequence**: Sequencing is the process of converting an application into a virtual application by using the App-V sequencer.

2.   **Create**: Use the Create Deployment Type Wizard to import the sequenced application into a Configuration Manager deployment type that you can then add to an application. You can also create virtual environments that allow multiple virtual applications to share settings.

3.   **Distribute**: Distribution is the process of making App-V applications available on Configuration Manager distribution points.

4.   **Deploy**: Deployment is the process of making the application available on client computers. This is called streaming in an App-V full infrastructure.  

##  Configuration Manager virtual application delivery methods  
Configuration Manager supports two methods for delivery of virtual applications to clients: streaming delivery and local delivery (download and execute).

When you're deciding which delivery method to use, compare the reduced disk space requirement for streaming delivery against the guaranteed availability of App-V applications in local delivery. The increased client disk space that is required for local delivery might be preferable to streaming delivery so that users always have the application available from any location.  

###  Streaming delivery
When you use Configuration Manager to manage the App-V Client, it supports the streaming of virtual applications through HTTP or HTTPS from a distribution point. Streaming through HTTP or HTTPS is enabled by default and is set up in the dialog box for distribution point properties. When you deploy a virtual application to client computers and a user runs the virtual application, the Configuration Manager client contacts a management point to determine which distribution point to use. Then, the application is streamed from the distribution point.  

Use the information in this table to help you decide if streaming delivery is the best delivery method for you:

|Advantages|Disadvantages|  
|----------------|-------------------|  
|This method uses standard network protocols to stream package content from distribution points.<br /><br /> Program shortcuts for virtual applications invoke a connection to the distribution point, so the virtual application delivery is on demand.<br /><br /> This method works well for clients with high-bandwidth connections to the distribution points.<br /><br /> Updated virtual applications distributed throughout the enterprise are available as clients receive policy that informs them that the current version is superseded and they download only the changes from the previous version.<br /><br /> Access permissions are defined at the distribution point to prevent users from accessing unauthorized applications or packages.|Virtual applications are not streamed until the user runs the application for the first time. In this scenario, a user might receive program shortcuts for virtual applications and then disconnect from the network before running the virtual applications for the first time. If the user tries to run the virtual application while the client is offline, the user sees an error and can't run the virtualized application because a Configuration Manager distribution point is not available to stream the application. The application will be unavailable until the user reconnects to the network and runs the application.<br /><br /> To avoid this, you can use the local delivery method for virtual application delivery to clients, or you can enable the Internet-based client management for streaming delivery.|  

###  Local delivery (download and execute)  
When you use the local delivery method, the Configuration Manager client first downloads the entire virtual application package into the Configuration Manager client cache. The Configuration Manager then instructs the App-V Client to stream the application from the Configuration Manager cache into the App-V cache. If you deploy a virtual application to client computers and its content is not in the App-V cache, the App-V Client streams the application content from the Configuration Manager client cache into the App-V cache, and then runs the application. After the application runs successfully, you can set the Configuration Manager client to delete any older versions of the package at the next deletion cycle, or to persist them in Configuration Manager client cache.  

Use the information in this table to help you decide if local delivery is the best delivery method for you:   

|Advantages|Disadvantages|  
|----------------|-------------------|  
|The standard distribution point functionality is used to download the package by using Background Intelligent Transfer Service (BITS).<br /><br /> Virtual application package contents are delivered locally to the client. This means that users can run them when their computer is not connected to the network.<br /><br /> This method is suitable for slow or unreliable network connections and for computers that only occasionally connect to the network.<br /><br /> Configuration Manager uses Remote Differential Compression (RDC) to send to clients only the bytes within the files that have changed when virtual application package content is updated. The Configuration Manager client uses RDC to build a new version of a virtual application package based on the current version of the package and any changes sent to the client.<br /><br /> This method provides application resiliency for mobile users or disconnected users. Admins can choose to persist the package in the Configuration Manager cache after delivery if the virtual application was deployed with an install action. The package in the Configuration Manager client cache serves as a local, reliable streaming source for the App-V Client to pull the package into its cache.|Disk space that equals up to twice the size of the virtual application package is required on the client when the virtual application is persisted in the Configuration Manager cache.|  

###  Deployment from an image

You can also preinstall virtual applications on a computer and then create an image of that computer for deployment to other computers. But if the virtual application package was created at a different site, the binary delta replication will not be used to download updates to the application. This option can be useful in a virtual desktop infrastructure when you want applications to be available immediately instead of downloading the applications after the user logs on.    

##  Migrating from an App-V infrastructure to a Configuration Manager and App-V infrastructure  
Use the following table to help you plan a migration from an existing App-V infrastructure to virtual application management with Configuration Manager.  

|Step|More information|  
|----------|----------------------|  
|Examine your current virtual applications to choose the applications that you want to migrate to your Configuration Manager infrastructure.|No additional information.|  
|Evaluate the users and devices to which the virtual applications will be deployed.|Create Configuration Manager collections to group together the users and devices to which you want to deploy the virtual applications. See [Introduction to collections](/sccm/core/clients/manage/collections/introduction-to-collections).|  
|Migrate App-V 5 connection groups to Configuration Manager virtual environments.|See the [Migrate App-V 5 connection groups to Configuration Manager virtual environments](/sccm/apps/get-started/deploying-app-v-virtual-applications#migrate-app-v-5-connection-groups-to-configuration-manager-virtual-environments) section in this topic.|  
|Investigate to find out if any of your virtual applications exist as full applications in your Configuration Manager infrastructure.|For easier management, you can add the virtual application as a new deployment type to the existing full application. See [Create applications](../../apps/deploy-use/create-applications.md).|  
|Create applications to replace your existing App-V packages.|See [Introduction to application management](/sccm/apps/understand/introduction-to-application-management) and [Create applications](../../apps/deploy-use/create-applications.md).|  
|Configuration Manager begins to manage virtual applications on a client after the first deployment of a virtual application. After this, Configuration Manager must manage all App-V applications on the computer.|No additional information.|  
|Distribute the content to the appropriate distribution points to enable local delivery of applications.|See [Manage content and content infrastructure](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).|  
|Deploy the application to Configuration Manager clients.<br /><br /> If the App-V application was created with an earlier version of the sequencer that does not create a manifest XML file, you can open it and save it in a newer version of the sequencer to create the file. This file is required to deploy virtual applications with Configuration Manager.<br /><br /> App-V supports the virtual application packages that are created with the SoftGrid 4.1 SP1 or 4.2 versions of the sequencer.<br /><br /> If the applications were previously installed locally, you must uninstall them before you deploy a virtual version of the application.|See [Deploy applications](../../apps/deploy-use/deploy-applications.md).|  
|System Center Configuration Manager no longer supports using packages and programs that contain virtual applications. When you migrate from Configuration Manager 2007 to System Center Configuration Manager, Configuration Manager converts these packages into applications.<br /><br /> Configuration Manager 2007 advertisements are converted into the following deployment types:<br /><br /> - Migrating App-V packages with no advertisement:  One deployment type that uses the default deployment type settings.<br /><br /> - Migrating App-V packages with one advertisement: One deployment type that uses the same settings as the <br />                Configuration Manager 2007 advertisement.<br /><br /> - Migrating App-V packages with multiple advertisements: A deployment type, for each <br />                Configuration Manager 2007 advertisement, that uses the settings for that advertisement.|See [Planning for the migration of Configuration Manager objects to System Center Configuration Manager](../../core/migration/planning-for-the-migration-of-objects.md).|  

##  Migrating App-V 5 connection groups to Configuration Manager virtual environments  
App-V virtual environments in Configuration Manager allow virtual applications that you have deployed to share the same file system and registry on client computers. This means that unlike standard virtual applications, these applications can share data with each other. Virtual environments are created or changed on client computers when the application is installed or when clients next evaluate their installed applications. Virtual environments are similar to connection groups in standalone App-V 5.  

When you migrate connection groups from standalone App-V 5 to Configuration Manager virtual environments, you must ensure that Configuration Manager correctly manages the connection groups that already exist on client computers, and that the user's environment within those connection groups is preserved.  

To convert App-V 5 connection groups to Configuration Manager virtual environments:  

1.  Create Configuration Manager applications for all applications that existed in App-V.  

2.  Deploy the applications to users or devices with a deployment purpose of **Required**. Deployments to users must be deployed to the same users who used the application in App-V. Deployments to computers must be deployed to the same computers that had the application in App-V.  

3.  After the deployment is finished, create virtual environments that match the connection groups that are published in standalone App-V. The virtual environment must have the same packages (specifically, App-V 5 deployment types) in the same order.  

For information about how to create an App-V virtual environment, see [How to create App-V virtual environments](../../apps/deploy-use/create-app-v-virtual-environments.md).  

Alternatively, you can delete all connection groups from the App-V Client before you begin to deploy applications with Configuration Manager. But any settings that users might have saved in App-V connection groups will be lost.  

##  Dynamic Suite Composition in App-V 4.6  
Dynamic Suite Composition is a feature that lets you define one virtual application package as having a dependency on another virtual application package. When the application is run, the App-V Client hosts the primary package and the dependent package in the same virtual environment for the application.  

For you to use this feature with Configuration Manager, both packages must be deployed and registered with the App-V Client. To ensure that dependent package content is hosted locally on the client computer, set up the application deployment for local delivery (download and execute).  

For more information about App-V Dynamic Suite Composition, see your App-V documentation.  

##  Converting App-V 4.6 applications to App-V 5 applications  
The application package format has changed between App-V 4.6 and App-V 5. Applications that have been sequenced by using App-V 4.6 are no longer supported. But App-V 5 has a package converter tool that you can use to convert applications. For more information, see your [App-V 5 documentation](http://technet.microsoft.com/library/jj713472.aspx).  

Use the following steps to convert App-V 4.6 applications to App-V 5 applications:  

1.  Convert or resequence the App-V 4.6 packages into the App-V 5 format.  

2.  Deploy the App-V 5 client to computers in your hierarchy.  

3.  Create new applications that contain deployment types for your App-V 5 applications, and create supersedence rules to supersede the App-V 4.6 applications.  

4.  Create virtual environments as required.  

5.  Deploy the new App-V 5 applications to computers.  

##  User and deployment configuration files  
User and deployment configuration files have settings that control how an application behaves. You can use these files to change application settings without resequencing the application.  

A typical App-V 5 application might contain the following files:  

-   An application package (.appv) file  

-   A user configuration file  

-   A deployment configuration file  

The user configuration file has settings that apply only to the logged-on user. You can, for example, edit the configuration files to change the information about the application shortcut that will be deployed to users. You can also create a Configuration Manager application with multiple deployment types. Each deployment type can contain a different user configuration file and use requirement rules to ensure that these are installed for the relevant users.  

The deployment configuration file has settings that apply to the computer, like registry settings. The file can also have user settings, which are applied to all users.  

If you want to deploy App-V 5 virtual applications with Configuration Manager, all three files must be present in the same folder when you create the App-V 5 deployment type. If there are multiple files in the folder, Configuration Manager will use the most recent.  

For more information, see your [App-V 5 documentation](http://technet.microsoft.com/library/jj713466.aspx).  

##  App-V local interaction  
In some application deployment scenarios, applications are installed locally on client computers, and other applications are deployed as virtual applications to the same client computer. By default, the applications that were locally installed cannot see or communicate directly with virtualized applications. This is the intended behavior of the application isolation that App-V provides. Local interaction is a feature of the App-V Client that you can enable for each application to allow locally installed applications that run on a client computer to see and communicate with virtualized applications. Configuration Manager and App-V fully support local interaction.  

For more information about the App-V local interaction feature, see your App-V documentation.  

##  App-V 5 Shared Content Store  
Configuration Manager supports the App-V 5 Shared Content Store feature. For more information, see [Planning for the App-V 5.0 Shared Content Store (SCS)](http://technet.microsoft.com/library/jj713431.aspx).  

##  Monitoring virtual applications  

### Virtual application reports  
You can use the following reports to monitor App-V in your Configuration Manager environment:  

|Report name|Description|  
|-----------------|-----------------|  
|App-V Virtual Environment Results|Shows information about a selected virtual environment that is in a specified state for a selected collection (App-V 5 only).|  
|App-V Virtual Environment Results For Asset|Shows information about a selected virtual environment for a specified asset and any deployment types for the selected virtual environment (App-V 5 only).|  
|App-V Virtual Environment Status|Shows compliance information for a selected virtual environment for a selected collection. The **Retained** column in this report shows the assets in which a virtual environment that was previously set up is no longer applicable, but it is retained to persist user settings in applications that run in the virtual environment (App-V 5 only).|  
|Computers with a specific virtual application|Shows a summary of computers that have the specified App-V shortcut that the Application Virtualization Management Sequencer created (App-V 4.6 only).|  
|Computers with a specific virtual application package|Shows a list of computers that have the specified App-V application package installed (App-V 4.6 only).|  
|Count all instances of virtual application packages|Shows a count of all detected App-V application packages (App-V 4.6 only).|  
|Count all instances of virtual applications|Shows a count of all detected App-V applications (App-V 4.6 only).|  

### Log files  
Configuration Manager records information about virtual application deployments in log files. For information about the log files that virtual applications and Configuration Manager application management use, see [Log files in System Center Configuration Manager](../../core/plan-design/hierarchy/log-files.md).  

For Windows Vista, Windows 7, and Windows 8, you can find logs for the App-V client in C:\ProgramData\Microsoft\Application Virtualization Client.  
