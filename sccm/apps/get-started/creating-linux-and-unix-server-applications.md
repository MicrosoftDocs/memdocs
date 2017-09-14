---
title: "Create Linux and UNIX server applications | Microsoft Docs"
description: "See which considerations you must take into account when you create and deploy applications for Linux and Unix devices."
ms.custom: na
ms.date: 04/13/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 79cd131a-1a24-4751-87c8-7f275e45d847
caps.latest.revision: 7
author: mattbriggsms.author: mabriggmanager: angrobe

---
# Create Linux and UNIX server applications with System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
Take the following considerations into account when you create and deploy applications for computers that run Linux and UNIX.  

## General considerations  
 The Configuration Manager client for Linux and UNIX supports **software deployments that use packages and programs**. You cannot deploy Configuration Manager applications to computers that run Linux and UNIX.  

 The capabilities of Linux and UNIX software deployment includes:  

-   Software installation for Linux and UNIX servers, including the following:  

    -   New software deployment  

    -   Software updates for programs that are already on a computer  

    -   Operating system patches  

-   Native Linux and UNIX commands, and scripts that are located on Linux and UNIX servers  

-   Deployments that are limited to the operating systems that you specify when you select the program option **Only on specified client platforms**

-   Maintenance windows to control when software installs

-   Deployment status messages to monitor deployments  

-   The option for the client to throttle network usage when it's downloading software from a distribution point  

### Differences between deploying to Linux and UNIX computers and deploying to Windows devices
The main differences between deploying packages and programs to Linux and UNIX computers and deploying packages and programs to Windows devices are as follows:  

|Configuration|Details|  
|-------------------|-------------|  
|Use only configurations that are intended for computers, and don't use configurations that are intended for users.|The Configuration Manager client for Linux and UNIX does not support configurations that are intended for users.|  
|Configure programs to download software from the distribution point and run the programs from the local client cache.|The Configuration Manager client for Linux and UNIX does not support running software from the distribution point. Instead, you must configure the software to download to the client and then get installed.<br /><br /> By default, after the client for Linux and UNIX installs software, that software is deleted from the client’s cache. However, packages that are configured with **Persist content in the client cache** are not deleted from the client and remain in the client’s cache after the software installs.<br /><br /> The client for Linux and UNIX does not support configurations for the client cache, and the maximum size of the client cache is limited only by the free disk space on the client computer.|  
|Configure the Network Access Account for distribution point access|Linux and UNIX computers are designed to be workgroup computers. To access packages from the distribution point in the Configuration Manager site server domain, you must configure the Network Access Account for the site. You must specify this account as a software distribution component property and configure the account before you deploy software.<br /><br /> You can configure multiple Network Access Accounts at each site. The client for Linux and UNIX can use each of the accounts you configure as a Network Access Account.<br /><br /> For more information, see [Site components for System Center Configuration Manager](../../core/servers/deploy/configure/site-components.md).|  

 You can deploy packages and programs to collections that contain only Linux or UNIX clients, or you can deploy them to collections that contain a mix of client types, such as the **All Systems Collection**. However, non-Linux and non-UNIX clients won't install the software or report failure.  

 When the Configuration Manager client for Linux and UNIX receives and runs a deployment, it generates status messages. You can view these status messages in the Configuration Manager console, or by using reports to monitor the deployment status.  

 For information about how to use packages and programs, see [Packages and programs](../../apps/deploy-use/packages-and-programs.md).  

##  Configure packages, programs, and deployments for Linux and UNIX servers  
 You can create and deploy packages and programs by using the available default options in the Configuration Manager console. The client does not require any unique configurations.  

 Use the information in the following sections to configure packages and programs as well as deployments.  

### Packages and programs  
 To create a package and program for a Linux or UNIX server, use the **Create Package and Program Wizard** from the Configuration Manager console. The client for Linux and UNIX supports most package and program settings. However, several settings are not supported. When you create or configure a package and program, consider the following:  

-   Include the file types that are supported by the destination computers.  

-   Define the command lines that are appropriate for use on the destination computer.  

-   Keep in mind that settings that interact with users are not supported.  

The following table lists the properties for packages and programs that are not supported:  

|Package and program property|Behavior|More information|  
|----------------------------------|--------------|----------------------|  
|Package share settings:<br /><br /> - All options|An error is generated and the software installation fails|The client does not support this configuration. Instead, the client must download the software by using HTTP or HTTPS, and then run the command line from its local cache.|  
|Package update settings:<br /><br /> - Disconnect users from distribution points|Settings are ignored|The client does not support this configuration.|  
|Operating system deployment settings:<br /><br /> - All options|Settings are ignored|The client does not support this configuration.|  
|Reporting:<br /><br /> - Use package properties for status MIF matching<br /><br /> - Use these fields for status MIF matching|Settings are ignored|The client does not support the use of status MIF files.|  
|**Run**:<br /><br /> - All options|Settings are ignored|The client always runs packages with no user interface.<br /><br /> The client ignores all configuration options for Run.|  
|After running:<br /><br />- Configuration Manager restarts computer<br /><br /> - Program controls restart<br /><br /> - Configuration Manager signs the user out|An error is generated and the software installation fails|The system restart setting and user-specific settings are not supported.<br /><br /> When any setting other than the **No action required** setting is in use, the client generates an error and continues the software installation, with no action taken.|  
|Program can run:<br /><br /> - Only when a user is signed in|An error is generated and the software installation fails|User-specific settings are not supported.<br /><br /> When this option is configured, the client generates an error and fails the installation of the software.<br /><br /> Other options are ignored and the software installation continues.|  
|Run mode:<br /><br /> - Run with user’s rights|Settings are ignored|User-specific settings are not supported.<br /><br /> However, the client supports the configuration running with Administrative rights.<br /><br /> When you specify **Run with administrative rights**, the Configuration Manager client uses its root credentials.<br /><br /> This setting does not generate an error or log entry. Instead, the software installation fails when the client generates an error for the prerequisite configuration of **Program can run** = **Only when a user is signed in**.|  
|Allow users to view and interact with the program installation|Settings are ignored|User-specific settings are not supported.<br /><br /> This configuration is ignored and the software installation continues.|  
|Drive mode:<br /><br /> - All options|Settings are ignored|This setting is not supported because content is always downloaded to the client and run locally.|  
|Run another program first|An error is generated and the software installation fails|Recursive program installation is not supported.<br /><br /> When a program is configured to run another program first, the software installation fails, and the other program installation is not started.|  
|When this program is assigned to a computer:<br /><br /> - Run once for every user who signs in|Settings are ignored|User-specific settings are not supported.<br /><br /> However, the client supports the configuration running once for the computer.<br /><br /> This setting does not generate an error or log entry because an error and log entry are already created for the prerequisite configuration of **Program can run** = **Only when a user is logged on**.|  
|Suppress program notifications|Settings are ignored|The client does not implement a user interface.<br /><br /> When this configuration is selected, it is ignored and the software installation continues.|  
|Disable this program on computers where it is deployed|Settings are ignored|This setting is not supported and does not affect the installation of software.|  
|Allow this program to be installed from the Install Package task sequence without being deployed||The client does not support task sequences.<br /><br /> This setting is not supported and does not affect the installation of software.|  
|Windows Installer:<br /><br /> - All options|Settings are ignored|The client does not support Windows Installer files or settings.|  
|OpsMgr Maintenance Mode:<br /><br /> - All options|Settings are ignored|The client does not support this configuration.|  

### Deploy software to a Linux or UNIX server
 To deploy software to a Linux or UNIX server by using a package and program, you can use the **Deploy Software Wizard** from the Configuration Manager console. Most deployment settings are supported by the client for Linux and UNIX. However several settings are not supported. When you deploy software, consider the following:  

-   You must provision the package on at least one distribution point that is associated with a boundary group that is configured for content location.  

-   The client for Linux and UNIX that receives this deployment must be able to access this distribution point from its network location.  

-   The client for Linux and UNIX downloads the package from the distribution point and runs the program on the local computer.  

-   The client for Linux and UNIX cannot download packages from shared folders. It downloads packages from IIS-enabled distribution points that support HTTP or HTTPS.  

 The following table lists properties for deployments that are not supported:  

|Deployment property|Behavior|More information|  
|-------------------------|--------------|----------------------|  
|Deployment settings – purpose:<br /><br /> - Available<br /><br /> - Required|Settings are ignored|User-specific settings are not supported.<br /><br /> However, the client supports the setting **Required**, which enforces the scheduled installation time, but does not support manual installation prior to that scheduled time.|  
|Send wake-up packets|Settings are ignored|The client does not support this configuration.|  
|Assignment schedule:<br /><br /> - logon<br /><br /> - logoff|An error is generated and the software installation fails|User-specific settings are not supported.<br /><br /> However, the client supports the setting **As soon as possible**.|  
|Notification settings:<br /><br /> - Allow users to run the program independently of assignments|Settings are ignored|The client does not implement a user interface.|  
|When the scheduled assignment time is reached, allow the following activity to be performed outside the maintenance window:<br /><br /> - System restart (if required to complete the installation)|An error is generated|The client does not support a system restart.|  
|Deployment option for fast (LAN) networks:<br /><br /> - Run program from distribution point|An error is generated and the software installation fails|The client cannot run software from the distribution point and instead must download the program before it can run.|  
|Deployment option for a slow or unreliable network boundary, or a fallback source location for content:<br /><br /> - Allow clients to share content with other clients on the same subnet|Settings are ignored|The client does not support sharing content between peers.|  

 For more information about content location, see [Manage content and content infrastructure for System Center Configuration Manager](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

 For more information about how to create a deployment, see [Deploy applications](../../apps/deploy-use/deploy-applications.md).  

##  Manage network bandwidth for software downloads from distribution points  
 The Linux and UNIX client supports network bandwidth controls when it's downloading software from a distribution point.  

 The client uses the Background Intelligent Transfer (BITS) settings that you configure as client settings in Configuration Manager, but does not implement BITS. Instead, to throttle the use of network bandwidth, the client controls the HTTP request chunk size and inter-chunk delay for the software download.  

 To configure a client to use network bandwidth controls, you configure client settings for **Background Intelligent Transfer** and then apply the settings to the client computer. To use bandwidth controls, the client must receive client settings for **Background Intelligent Transfer** with the following settings configured as **Yes**:  

-   **Limit the maximum network bandwidth for BITS background transfers**  

 The client supports the following configurations for Background Intelligent Transfer:  

    -   **Throttling window start time**  

    -   **Throttling window end time**  

    -   **Maximum transfer rate during throttling window (Kbps)**  

    -   **Maximum transfer rate outside the throttling window (Kbps)**  

The following configuration for Background Intelligent Transfer is not supported, and is ignored by the client for Linux and UNIX:  

-   **Allow BITS downloads outside the throttling window**  

 If the download of software to the client from a distribution point is interrupted, the client for Linux and UNIX does not resume the download. Instead, it restarts the download of the entire software package.  

##  Configure operations for software deployments  
 Similarly to the Windows client, the Configuration Manager client for Linux and UNIX discovers new software deployments when it polls and checks for new policy. The frequency at which the client checks for new policy depends on client settings. You can configure maintenance windows to control when software deployments occur.  

 You can configure software deployments to Linux and UNIX servers by using package properties, program properties, and deployment properties.  

 When the client receives policy for a deployment, it submits a status message. It also submits status messages when it starts the installation of software and when the installation finishes or fails.  

 Programs for software deployments run with the root credentials that the Configuration Manager client for Linux and UNIX runs with. The exit code of the programs command is used to determine success or failure. An exit code of 0 (zero) is treated as success. In addition, the **stdout** (standard output stream) and **stderr** (standard error stream) are copied to the log file when the log level is set to INFO or TRACE.  

> [!TIP]  
>  If the software that you want to deploy is located on a Network File System (NFS) share that the Linux or UNIX server can access, you do not need to use a distribution point to download the package. Instead, when you create the package, do not select the check box for **This package contains source files**. Then, when you configure the program, specify the appropriate command line to directly access the package on the NFS mount point.  
