---
title: "Packages and programs"
description: "Support deployments that use packages and programs or applications with System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: caad0507-9913-415a-b13d-d36f8f0a1b80
caps.latest.revision: 8
caps.handback.revision: 0
author: mattbriggsms.author: mabrigg
manager: angrobe

---
# Packages and programs in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
System Center Configuration Manager continues to support packages and programs that were used in Configuration Manager 2007. A deployment that uses packages and programs might be more suitable than a deployment that uses an application when you deploy any of the following:  

- Applications to Linux and UNIX servers
- Scripts that do not install an application on a computer, such as a script to defragment the computer disk drive
- “One-off” scripts that do not need to be continually monitored  
- Scripts that run on a recurring schedule and cannot use global evaluation

When you migrate packages from an earlier version of Configuration Manager, you can deploy them in your Configuration Manager hierarchy. After migration is complete, the packages appear in the **Packages** node in the **Software Library** workspace.

You can modify and deploy these packages in the same way you did by using software distribution. The **Import Package from Definition Wizard** remains in Configuration Manager to import legacy packages. Advertisements are converted to deployments when they are migrated from Configuration Manager 2007 to a Configuration Manager hierarchy.  

> [!NOTE]  
>  You can use Microsoft System Center Configuration Manager Package Conversion Manager to convert packages and programs into Configuration Manager applications.  
>   
>  For more information, see [Configuration Manager Package Conversion Manager](https://technet.microsoft.com/library/hh531519.aspx).  

Packages can use some new features of Configuration Manager, including distribution point groups and monitoring. Microsoft Application Virtualization (App-V) applications cannot be distributed by using packages and programs in Configuration Manager. To distribute virtual applications, you must create them as Configuration Manager applications.  

##  Create a package and program  
 Use one of these procedures to help you create or import packages and programs.  

### Create a package and program using the Create Package and Program wizard  

1.  In the Configuration Manager console, choose **Software Library** > **Application Management** > **Packages**.  

3.  In the **Home** tab, in the **Create** group, choose **Create Package**.  

4.  On the **Package** page of the **Create Package and Program Wizard**, specify the following information:  

    -   **Name**: Specify a name for the package with a maximum of 50 characters.  

    -   **Description**: Specify a description for this package with a maximum of 128 characters.  

    -   **Manufacturer** (optional): Specify a manufacturer name to help you identify the package in the Configuration Manager console. This name can be a maximum of 32 characters.

    -   **Language** (optional): Specify the language version of the package with a maximum of 32 characters.  

    -   **Version** (optional):  Specify a version number for the package with a maximum of 32 characters.

    -   **This package contains source files**: This setting indicates whether the package requires source files to be present on client devices. By default, this check box is cleared, and Configuration Manager does not use distribution points for the package. When this check box is selected, distribution points are used.  

    -   **Source folder**: If the package contains source files, choose **Browse** to open the **Set Source Folder** dialog box, and then specify the location of the source files for the package.  

        > [!NOTE]  
        >  The computer account of the site server must have read access permissions to the source folder that you specify.  

5.  On the **Program Type** page of the **Create Package and Program Wizard**, select the type of program to create, and then choose **Next**. You can create a program for a computer or device, or you can skip this step and create a program later.  

    > [!TIP]  
    >  To create a new program for an existing package, first select the package. Then, in the **Home** tab, in the **Package** group, choose **Create Program** to open the **Create Program Wizard**.  

6.  Use one of the following procedures to create a standard program or a device program.  

    #### Create a standard program  

  1.  On the **Program Type** page of the **Create Package and Program Wizard**, choose **Standard Program**, and then choose **Next**.     

    2.  On the **Standard Program** page, specify the following information:  

        -   **Name:** Specify a name for the program with a maximum of 50 characters.  

            > [!NOTE]  
            >  The program name must be unique within a package. After you create a program, you cannot modify its name.  

        -   **Command Line**: Enter the command line to use to start this program, or choose **Browse** to browse to the file location.  

            If a file name does not have an extension that's specified, Configuration Manager attempts to use .com, .exe, and .bat as possible extensions.  

             When the program is run on a client, Configuration Manager first searches for the command-line file name within the package,  searches next in the local Windows folder, and then searches in local *%path%*. If the file cannot be found, the program fails.  

        -   **Startup folder** (optional): Specify the folder from which the program runs, up to 127 characters. This folder can be an absolute path on the client or a path that's relative to the distribution point folder that contains the package.

        -   **Run**: Specify the mode in which the program runs on client computers. Select one of the following:  

            -   **Normal**: The program runs in the normal mode based on system and program defaults. This is the default mode.  

            -   **Minimized**: The program runs minimized on client devices. Users might see installation activity in the notification area or on the taskbar.  

            -   **Maximized**: The program runs maximized on client devices. Users see all installation activity.  

            -   **Hidden**: The program runs hidden on client devices. Users don't see any installation activity.  

        -   **Program can run**: Specify whether the program runs only when a user is signed in, only when no user is signed in, or regardless of whether  a user is signed in to the client computer.  

        -   **Run mode**: Specify whether the program runs with administrative permissions or with the permissions of the user who's currently signed in.  

        -   **Allow users to view and interact with the program installation**: Use this setting, if available, to specify whether to allow users to interact with the program installation. This check box is available only when **Only when no user is logged on** or **Whether or not a user is logged on** is selected for **Program can run** and when **Run with administrative rights** is selected for **Run mode**.  

        -   **Drive mode**: Specify information about how this program runs on the network. Choose one of the following:  

            -   **Runs with UNC name**: Specify that the program runs with a Universal Naming Convention (UNC) name. This is the default setting.  

            -   **Requires drive letter**: Specify that the program requires a drive letter to fully qualify its location. For this setting, Configuration Manager can use any available drive letter on the client.  

            -   **Requires specific drive letter** : Specify that the program requires a specific drive letter that you specify to fully qualify its location (for example, **Z:**). If the specified drive letter is already used on a client, the program does not run.  

        -   **Reconnect to distribution point at log on**: Use this check box to indicate whether the client computer reconnects to the distribution point when the user signs in. By default, this check box is cleared.  

  3.  On the **Requirements** page of the **Create Package and Program Wizard,** specify the following information:  

        -   **Run another program first**: Use this setting to identify a package and program that runs before this package and program runs.  

        -   **Platform requirements**: Select **This program can run on any platform** or  **This program can run only on specified platforms**, and then choose the operating systems that clients must be running to be able to install the package and program.  

        -   **Estimated disk space**: Specify the amount of disk space that the software program requires to run on the computer. This can be specified as **Unknown** (the default setting) or as a whole number greater than or equal to zero. If a value is specified, units for the value must also be specified.  

        -   **Maximum allowed run time (minutes)**: Specify the maximum time that the program is expected to run on the client computer. This can be specified as **Unknown** (the default setting) or as a whole number greater than zero.  

             By default, this value is set to 120 minutes.  

            > [!IMPORTANT]  
            >  If you are using maintenance windows for the collection on which this program is run, a conflict could occur if the **Maximum allowed run time** is longer than the scheduled maintenance window. However, if the maximum run time is set to **Unknown**, the program starts to run during the maintenance window and continues to run as needed after the maintenance window is closed. If the user sets the maximum run time to a specific period that exceeds the length of any available maintenance window, then the program doesn't run.  

             If the value is set to **Unknown**, Configuration Manager sets the maximum allowed run time as 12 hours (720 minutes).  

            > [!NOTE]  
            >  If the maximum run time (whether set by the user or as the default value) is exceeded, Configuration Manager stops the program if **run with administrative rights** is selected and **Allow users to view and interact with the program installation** is not selected.  

  4.  Choose **Next**.  

    #### Create a device program  

  1.  On the **Program Type** page of the **Create Package and Program Wizard**, select **Program for device**, and then choose **Next**.  

  2.  On the **Program for Device** page, specify the following:  

        -   **Name**: Specify a name for the program with a maximum of 50 characters.  

            > [!NOTE]  
            >  The program name must be unique within a package. After you create a program, you cannot modify its name.  

        -   **Comment** (optional): Specify a comment for this device program with a maximum of 127 characters.  

        -   **Download folder**: Specify the name of the folder on the Windows CE device in which the package source files will be stored. The default value is **\Temp\\**.  

        -   **Command Line**: Enter the command line to use to start this program, or choose **Browse** to browse to the file location.  

        -   **Run command line in download folder**: Select this option to run the program from the previously specified download folder.  

        -   **Run command line from this folder**: Select this option to specify a different folder from which to run the program.  

    3.  On the **Requirements** page, specify the following:  

        -   **Estimated disk space**: Specify the amount of disk space that's required for the software. This is displayed to users of mobile devices before they install the program.  

        -   **Download program**: Specify information regarding when this program can be downloaded to mobile devices. You can specify **As soon as possible**, **Only over a fast network**, or **Only when the device is docked**.  

        -   **Additional requirements**: Specify any additional requirements for this program. These are displayed to users before they install the software. For example, you could notify users that they need to close all other applications before running the program.  

  4.  Choose **Next**.  

  7.  On the **Summary** page, review the actions that will be taken, and then complete the wizard.  

 Verify that the new package and program are displayed in the **Packages** node of the **Software Library** workspace.  

## Create a package and program from a package definition file  

1.  In the Configuration Manager console, choose **Software Library** > **Application Management** > **Packages**.  

3.  On the **Home** tab, in the **Create** group, choose **Create Package from Definition**.  

4.  On the **Package Definition** page of the **Create Package from Definition Wizard**, choose an existing package definition file, or choose **Browse** to open a new package definition file. After you have specified a new package definition file, select it from the **Package definition** list, and then choose **Next**.  

5.  On the **Source Files** page, specify information about any required source files for the package and program, and then choose **Next**.  

6.  If the package requires source files, on the **Source Folder** page, specify the location from which the source files are to be obtained, and then choose **Next**.  

7.  On the **Summary** page, review the actions that will be taken, and then complete the wizard. The new package and program are displayed in the **Packages** node of the **Software Library** workspace.  

 For more information about package definition files, see [About the package definition file format](/sccm/apps/deploy-use/packages-and-programs#about-the-package-definition-file-format) in this topic.  

##  Deploy packages and programs  

1.  In the Configuration Manager console, choose **Software Library** > **Application Management** > **Packages**.  

2.  Select the package that you want to deploy, and then in the **Home** tab in the **Deployment** group, choose **Deploy**.  

3.  On the **General** page of the **Deploy Software Wizard**, specify the name of the package and program that you want to deploy, the collection to which you want to deploy the package and program, and optional comments for the deployment.  

     Select **Use default distribution point groups associated to this collection** if you want to store the package content on the collections default distribution point group. If you did not associate the selected collection with a distribution point group, this option is unavailable.  

4.  On the **Content** page, choose **Add**, and then select the distribution points or distribution point groups to which you want to deploy the content that is associated with this package and program.  

5.  On the **Deployment Settings** page, choose a purpose for this deployment, and specify options for wake-up packets and metered connections:  

    -   **Purpose**: Choose from:  

        -   **Available**: If the application is deployed to a user, the user sees the published package and program in the Application Catalog and can request it on demand. If the package and program is deployed to a device, the user sees it in Software Center and can install it on demand.  

        -   **Required**: The package and program is deployed automatically, according to the configured schedule. However, a user can track the package and program deployment status and install it before the deadline by using Software Center.  

    -   **Send wake-up packets**: If the deployment purpose is set to **Required** and this option is selected, a wake-up packet is sent to computers before the deployment is installed to wake the computer from sleep at the installation deadline time. Before you can use this option, computers must be configured for Wake On LAN.  

    -  **Allow clients on a metered Internet connection to download content after the installation deadline, which might incur additional costs**: Select this if it's required.  

    > [!NOTE]  
    >  The **Pre-deploy software to the user's primary device** option is not available when you deploy a package and program.  

6.  On the **Scheduling** page, configure when this package and program will be deployed or made available to client devices.  

     The options on this page vary depending on whether the deployment action is set to **Available** or **Required**.  

7.  If the deployment purpose is set to **Required**, configure the rerun behavior for the program from the **Rerun behavior** drop-down menu. Choose from the following options:  

    |Rerun behavior|More information|  
    |--------------------|----------------------|  
    |Never rerun deployed program|The program won't be rerun on the client, even if the program originally failed or if the program files are changed.|  
    |Always rerun program|The program is always rerun on the client when the deployment is scheduled, even if the program has already successfully run. This can be useful when you use recurring deployments in which the program is updated, for example with antivirus software.|  
    |Rerun if failed previous attempt|The program is rerun when the deployment is scheduled only if it failed on the previous run attempt.|  
    |Rerun if succeeded on previous attempt|The program is rerun only if it previously ran successfully on the client. This is useful when you use recurring advertisements in which the program is routinely updated, and in which each update requires the previous update to be successfully installed.|  

8. On the **User Experience** page, specify the following information:  

    -   **Allow users to run the program independently of assignments**: If enabled, users can install this software from Software Center regardless of any scheduled installation time.  

    -   **Software installation**: Allows the software to be installed outside of any configured maintenance windows.  

    -   **System restart (if required to complete the installation)**: If the software installation requires a device restart to finish, allow this to happen outside of any configured maintenance windows.  

    -   **Embedded devices**: When you deploy packages and programs to Windows Embedded devices that are write-filter-enabled, you can specify that packages and programs be installed on the temporary overlay and commit changes later. Alternately, you commit the changes on the installation deadline or during a maintenance window. When you commit changes on the installation deadline or during a maintenance window, a restart is required and the changes persist on the device.  

        > [!NOTE]  
        >  When you deploy a package or program to a Windows Embedded device, make sure that the device is a member of a collection that has a configured maintenance window. For more information about how maintenance windows are used when you deploy packages and programs to Windows Embedded devices, see [Creating Windows Embedded applications](../../apps/get-started/creating-windows-embedded-applications.md).  

9. On the **Distribution Points** page, specify the following information:  

    -   **Deployment options**: Specify the actions that a client should take to run program content. You can specify behavior when the client is in a fast network boundary, or a slow or unreliable network boundary.  

    -   **Allow clients to share content with other clients on the same subnet**: Select this option to reduce load on the network by allowing clients to download content from other clients on the network that already downloaded and cached the content. This option utilizes Windows BranchCache and can be used on computers that run Windows Vista SP2 and later.  

    -   **Allow clients to use a fallback source location for content**:  

        -  **Versions earlier than 1610**: You can select the **Allow fallback source location for content check box** to enable clients outside these boundary groups to fall back and use the distribution point as a source location for content when no other distribution points are available.

        - **Version 1610 and later**: You can no longer configure **Allow fallback source location for content**.  Instead, you configure relationships between boundary groups that determine when a client can begin to search additional boundary groups for a valid content source location.

10. On the **Summary** page, review the actions that will be taken, and then complete the wizard.  

     You can view the deployment in the **Deployments** node of the **Monitoring** workspace and in the details pane of the package deployment tab when you select the deployment. For more information, see [Monitor packages and programs](/sccm/apps/deploy-use/packages-and-programs#monitor-packages-and-programs) in this topic.  

> [!IMPORTANT]  
>  If you configured the option **Run program from distribution point** on the **Distribution Points** page of the **Deploy Software Wizard**, do not clear the option **Copy the content in this package to a package share on distribution points** because this makes the package unavailable to run from distribution points.  

##  Monitor packages and programs  
 To monitor package and program deployments, use the same procedures that you use to monitor applications as detailed in [Monitor applications](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

 Packages and programs also includes a number of built-in reports, which enable you to monitor information about the deployment status of packages and programs. These reports have the report category of **Software Distribution – Packages and Programs** and **Software Distribution – Package and Program Deployment Status**.  

 For more information about how to configure reporting in Configuration Manager, see [Reporting in System Center Configuration Manager](../../core/servers/manage/reporting.md).  

##  Manage packages and programs  
 In the **Software Library** workspace, expand **Application Management**, choose **Packages**, choose the package that you want to manage, and then choose a management task from the following table:  

|Task|More information|  
|----------|----------------------|  
|**Create Prestage Content File**|Opens the **Create Prestaged Content File Wizard**, which enables you to create a file that contains the package content that can be manually imported to another site. This is useful in situations where you have low network bandwidth between the site server and the distribution point.|  
|**Create Program**|Opens the **Create Program Wizard**, which enables you to create a new program for this package.|  
|**Export**|Opens the **Export Package Wizard**, which enables you to export the selected package and its content to a file.<br /><br /> For information about how to import packages and programs, see [Create packages and programs](/sccm/apps/deploy-use/packages-and-programs#create-packages-and-programs) in this topic.|  
|**Deploy**|Opens the **Deploy Software Wizard**, which enables you to deploy the selected package and program to a collection. For more information, see [Deploy packages and programs](/sccm/apps/deploy-use/packages-and-programs#deploy-packages-and-programs) in this topic.|  
|**Distribute Content**|Opens the **Distribute Content Wizard**, which enables you to send the content that is associated with the package and program to selected distribution points or distribution point groups.|  
|**Update Distribution Points**|Updates distribution points with the latest content for the selected package and program.|  

##  About the package definition file format  
 Package definition files are scripts that you can use to help automate package and program creation with Configuration Manager. They provide all of the information that Configuration Manager needs to create a package and program, except for the location of package source files. Each package definition file is an ASCII or UTF-8 text file that uses the .ini file format and that contains the following sections:  

###  [PDF]  
 This section identifies the file as a package definition file. It contains the following information:  

-   **Version**: Specify the version of the package definition file format that is used by the file. This corresponds to the version of System Management Server (SMS) or Configuration Manager for which it was written. This entry is required.  

###  [Package Definition]  
 Specify the properties of the package and program. It provides the following information:  

-   **Name**: The name of the package, up to 50 characters.  

-   **Version** (optional): The version of the package, up to 32 characters.  

-   **Icon** (optional): The file that contains the icon to use for this package. If specified, this icon replaces the default package icon in the Configuration Manager console.

-   **Publisher**: The publisher of the package, up to 32 characters.

-   **Language**: The language version of the package, up to 32 characters.

-   **Comment** (optional): A comment about the package, up to 127 characters.

-   **ContainsNoFiles**: This entry indicates whether or not a source is associated with the package.  

-   **Programs**: The programs that are defined for this package. Each program name corresponds to a **[Program]** section in this package definition file.  

     Example:  

     `Programs=Typical, Custom, Uninstall`  

-   **MIFFileName**: The name of the Management Information Format (MIF) file that contains the package status, up to 50 characters.  

-   **MIFName**: The name of the package (for MIF matching), up to 50 characters.  

-   **MIFVersion**: The version number of the package (for MIF matching), up to 32 characters.  

-   **MIFPublisher**: The software publisher of the package (for MIF matching), up to 32 characters.  

###  [Program]  
 For each program that's specified in the **Programs** entry in the **[Package Definition]** section, the package definition file must include a [Program] section that defines that program. Each Program section provides the following information:  

-   **Name**: The name of the program, up to 50 characters. This entry must be unique within a package. This name is used when defining advertisements. On client computers, the name of the program is shown in **Run Advertised Programs** in Control Panel.  

-   **Icon** (optional): Specify the file that contains the icon to use for this program. If specified, this icon replaces the default program icon in the Configuration Manager console and is displayed on client computers when the program is advertised.

-   **Comment** (optional): A comment about the program, up to 127 characters.

-   **CommandLine**: Specify the command line for the program, up to 127 characters. The command is relative to the package source folder.

-   **StartIn**: Specify the working folder for the program, up to 127 characters. This entry can be an absolute path on the client computer or a path that's relative to the package source folder.

-   **Run**: Specify the program mode in which the program runs. You can specify **Minimized**, **Maximized**, or **Hidden**. If this entry is not included, the program runs in normal mode.  

-   **AfterRunning**: Specify any special action that occurs after the program is successfully completed. Options available are **SMSRestart**, **ProgramRestart**, or **SMSLogoff**. If this entry is not included, the program doesn't run a special action.  

-   **EstimatedDiskSpace**: Specify the amount of disk space that the software program requires to run on the computer. This can be specified as **Unknown** (the default setting) or as a whole number greater than or equal to zero. If a value is specified, the units for the value must also be specified.  

     Example:  

     `EstimatedDiskSpace=38MB`  

-   **EstimatedRunTime**: Specify the estimated duration (in minutes) that the program is expected to run on the client computer. This can be specified as **Unknown** (the default setting) or as a whole number greater than zero.  

     Example:  

     `EstimatedRunTime=25`  

-   **SupportedClients**: Specify the processors and operating systems on which this program runs. The specified platforms must be separated by commas. If this entry is not included, supported platform checking is disabled for this program.  

-   **SupportedClientMinVersionX**, **SupportedClientMaxVersionX**: Specify the beginning-to-ending range for version numbers for the operating systems that are specified in the **SupportedClients** entry.  

     Example:  

    ```  
    SupportedClients=Win NT (I386),Win NT (IA64),Win NT (x64)  
    Win NT (I386) MinVersion1=5.00.2195.4  
    Win NT (I386) MaxVersion1=5.00.2195.4  
    Win NT (I386) MinVersion2=5.10.2600.2  
    Win NT (I386) MaxVersion2=5.10.2600.2  
    Win NT (I386) MinVersion3=5.20.0000.0  
    Win NT (I386) MaxVersion3=5.20.9999.9999  
    Win NT (I386) MinVersion4=5.20.3790.0  
    Win NT (I386) MaxVersion4=5.20.3790.2  
    Win NT (I386) MinVersion5=6.00.0000.0  
    Win NT (I386) MaxVersion5=6.00.9999.9999  
    Win NT (IA64) MinVersion1=5.20.0000.0  
    Win NT (IA64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion1=5.20.0000.0  
    Win NT (x64) MaxVersion1=5.20.9999.9999  
    Win NT (x64) MinVersion2=5.20.3790.0  
    Win NT (x64) MaxVersion2=5.20.9999.9999  
    Win NT (x64) MinVersion3=5.20.3790.0  
    Win NT (x64) MaxVersion3=5.20.3790.2  
    Win NT (x64) MinVersion4=6.00.0000.0  
    Win NT (x64) MaxVersion4=6.00.9999.9999   
    ```  

-   **AdditionalProgramRequirements** (optional): Provide any other information or requirements for client computers, up to 127 characters.

-   **CanRunWhen**: Specify the user status that the program requires to run on the client computer. Available values are **UserLoggedOn**, **NoUserLoggedOn**, or **AnyUserStatus**. The default value is **UserLoggedOn**.  

-   **UserInputRequired**: Specify whether the program requires interaction with the user. Available values are **True** or **False**. The default value is **True**. This entry is set to **False** if **CanRunWhen** is not set to **UserLoggedOn**.  

-   **AdminRightsRequired**: Specify whether the program requires administrative credentials on the computer to run. Available values are **True** or **False**. The default value is **False**. This entry is set to **True** if **CanRunWhen** is not set to **UserLoggedOn**.  

-   **UseInstallAccount**: Specify whether the program uses the Client Software Installation Account when it runs on client computers. By default, this value is **False**. This value is also **False** if **CanRunWhen** is set to **UserLoggedOn**.  

-   **DriveLetterConnection**: Specify whether the program requires a drive letter connection to the package files that are located on the distribution point. You can specify **True** or **False**. The default value is **False**, which enables the program to use a Universal Naming Convention (UNC) connection. When this value is set to **True**, the next available drive letter is used (starting with Z: and proceeding backward).  

-   **SpecifyDrive** (optional): Specify a drive letter that the program requires to connect to the package files on the distribution point. This specification forces the use of the specified drive letter for client connections to distribution points.

-   **ReconnectDriveAtLogon**: Specify whether the computer reconnects to the distribution point when the user signs in. Available values are **True** or **False**. The default value is **False**.  

-   **DependentProgram**: Specify a program in this package that must run before the current program. This entry uses the format **DependentProgram**=<**ProgramName>**, where **<ProgramName\>** is the **Name** entry for that program in the package definition file. If there are no dependent programs, leave this entry empty.  

     Example:  

     DependentProgram=Admin  
    DependentProgram=  

-   **Assignment**: Specify how the program is assigned to users. This value can be: **FirstUser** (only the first user who signs in to the client runs the program) or **EveryUser** (every user who signs in runs the program). When **CanRunWhen** is not set to **UserLoggedOn**, this entry is set to **FirstUser**.  

-   **Disabled**: Specify whether this program can be advertised to clients. Available values are **True** or **False**. The default value is **False**.  
