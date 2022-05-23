---
title: Packages and programs
titleSuffix: Configuration Manager
description: Support deployments that use legacy packages and programs with Configuration Manager.
ms.date: 04/08/2022
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.localizationpriority: medium
---

# Packages and programs in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Configuration Manager continues to support packages and programs that were used in Configuration Manager 2007. A deployment that uses packages and programs might be more suitable than an application when you deploy any of the following tools or scripts:  

- Administrative tools that don't install an application on a computer
- "One-off" scripts that don't need to be continually monitored  
- Scripts that run on a recurring schedule and can't use global evaluation

> [!TIP]  
> Consider using the [Scripts](create-deploy-scripts.md) feature in the Configuration Manager console. Scripts may be a better solution for some of the preceding scenarios instead of using packages and programs.

When you migrate packages from an earlier version of Configuration Manager, you can deploy them in your Configuration Manager hierarchy. After migration is complete, the packages appear in the **Packages** node in the **Software Library** workspace.

You can modify and deploy these packages in the same way you did by using software distribution. The **Import Package from Definition Wizard** remains in Configuration Manager to import legacy packages. Advertisements are converted to deployments when you migrate from Configuration Manager 2007 to a Configuration Manager hierarchy.  

> [!NOTE]  
> Use Package Conversion Manager to convert packages and programs into Configuration Manager applications. Package Conversion Manager is integrated with Configuration Manager. For more information, see [Package Conversion Manager](../pcm/package-conversion-manager.md).  

Packages can use some new features of Configuration Manager, including distribution point groups and monitoring. You can't deploy Microsoft Application Virtualization (App-V) applications with packages and programs in Configuration Manager. To distribute virtual applications, create them as Configuration Manager applications. For more information, see [Deploy App-V virtual applications](../get-started/deploying-app-v-virtual-applications.md).  


## Create a package and program

### Use the Create Package and Program wizard

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Application Management**, and select the **Packages** node.  

2. In the **Home** tab of the ribbon, in the **Create** group, choose **Create Package**.  

3. On the **Package** page of the **Create Package and Program Wizard**, specify the following information:  

    - **Name**: Specify a name for the package with a maximum of 50 characters.  

    - **Description**: Specify a description for this package with a maximum of 128 characters.  

    - **Manufacturer** (optional): Specify a manufacturer name to help you identify the package in the Configuration Manager console. This name can be a maximum of 32 characters.

    - **Language** (optional): Specify the language version of the package with a maximum of 32 characters.  

    - **Version** (optional): Specify a version number for the package with a maximum of 32 characters.

    - **This package contains source files**: This setting indicates whether the package requires source files to be present on client devices. By default, the wizard doesn't enable this option, and Configuration Manager doesn't use distribution points for the package. When you select this option, specify the package content to distribute to distribution points.  

    - **Source folder**: If the package contains source files, choose **Browse** to open the **Set Source Folder** dialog box, and then specify the location of the source files for the package.  

        > [!NOTE]  
        > The computer account of the site server must have read access permissions to the source folder that you specify.
        >
        > Windows limits the source path to 256 characters or less. This limit applies to package source as well as applications. For more information, see [Naming Files, Paths, and Namespaces](/windows/win32/fileio/naming-a-file).

    - If you want to pre-cache content on a client, specify the **Architecture** and **Language** of the package. For more information, see [Configure pre-cache content](../../osd/deploy-use/configure-precache-content.md).<!--4224642-->  

4. On the **Program Type** page of the **Create Package and Program Wizard**, select the **Standard** program type for computers. Or you can skip this step and create a program later.

    > [!TIP]
    > To create a new program for an existing package, first select the package. Then, in the **Home** tab, in the **Package** group, choose **Create Program** to open the **Create Program Wizard**.
    >
    > The **Program for device** type is a legacy option that only applies to mobile devices, which aren't currently managed by Configuration Manager.

#### Custom icons for packages

<!--12486335-->

Starting in version 2203, add custom icons for packages. These icons appear in Software Center when you deploy the package and program. Instead of a default icon, a custom icon can improve the user experience to better identify the software.

On the **General** tab of package properties, in the section for the icon, select **Browse**. Select an icon from the default shell library, or browse to another file in a local or network path.

- It supports the following file types:
  - Programs (`.exe`)
  - Libraries (`.dll`)
  - Icons (`.ico`)
  - Images (`.png`, `.jpeg`, `.jpg`)
- The file doesn't need to be on clients that you target with the deployment. Configuration Manager includes the image with the deployment policy.
- The maximum file size for an image is 256 KB.
- Icons can have pixel dimensions of up to 512 x 512.

When clients receive the deployment policy, they'll display the icon in Software Center.

> [!NOTE]
> To take full advantage of new Configuration Manager features, after you update the site, also update clients to the latest version. While new functionality appears in the Configuration Manager console when you update the site and console, the complete scenario isn't functional until the client version is also the latest.

### Create a program

1. On the **Program Type** page of the **Create Package and Program Wizard**, choose **Standard Program**, and then choose **Next**.

2. On the **Standard Program** page, specify the following information:  

    - **Name:** Specify a name for the program with a maximum of 50 characters.  

        > [!NOTE]  
        > The program name must be unique within a package. After you create a program, you can't modify its name.  

    - **Command Line**: Enter the command line to use to start this program, or choose **Browse** to browse to the file location.  

        If you don't specify an extension for a file name, Configuration Manager attempts to use .com, .exe, and .bat as possible extensions.  

        When the client runs the program, Configuration Manager searches for the file in the following locations:

        - Within the package
        - The local Windows folder
        - The local *%path%*

        If it can't find the file, the program fails.  

    - **Startup folder** (optional): Specify the folder from which the program runs, up to 127 characters. This folder can be an absolute path on the client. It can also be a path that's relative to the distribution point folder that contains the package.

    - **Run**: Specify the mode in which the program runs on client computers. Select one of the following options:  

        - **Normal**: The program runs in the normal mode based on system and program defaults. This mode is the default.  

        - **Minimized**: The program runs minimized on client devices. Users might see installation activity in the notification area or on the taskbar.  

        - **Maximized**: The program runs maximized on client devices. Users see all installation activity.  

        - **Hidden**: The program runs hidden on client devices. Users don't see any installation activity.  

    - **Program can run**: Specify whether the program runs only when a user is signed in, only when no user is signed in, or regardless of whether a user is signed in to the client computer.  

    - **Run mode**: Specify whether the program runs with administrative permissions or with the permissions of the user who's currently signed in.  

    - **Allow users to view and interact with the program installation**: Use this setting, if available, to specify whether to allow users to interact with the program installation. This option is only available if the following conditions are met:

        - **Program can run** setting is **Only when a user is logged on** or **Whether or not a user is logged on**
        - **Run mode** setting is to **Run with administrative rights**  

    - **Drive mode**: Specify information about how this program runs on the network. Choose one of the following options:  

        - **Runs with UNC name**: Specify that the program runs with a Universal Naming Convention (UNC) name. This setting is the default.  

        - **Requires drive letter**: Specify that the program requires a drive letter to fully qualify its location. For this setting, Configuration Manager can use any available drive letter on the client.  This setting requires the deployment to use the Deployment option **Run program from distribution point** and the package's Data Access option enabled to **Copy the content in this package to a package share on distribution points**.

        - **Requires specific drive letter**: Specify that the program requires a specific drive letter that you specify to fully qualify its location. For example, **Z:**. If the client is already using the specified drive letter, the program doesn't run.  This setting requires the deployment to use the Deployment option **Run program from distribution point** and the package's Data Access option enabled to **Copy the content in this package to a package share on distribution points**.

    - **Reconnect to distribution point at log on**: Indicate whether the client reconnects to the distribution point when the user signs in. By default, the wizard doesn't enable this option.

3. On the **Requirements** page of the **Create Package and Program Wizard,** specify the following information:  

    - **Run another program first**: Identify a package and program that runs before this package and program runs.  

    - **Platform requirements**: Select **This program can run on any platform** or **This program can run only on specified platforms**. Then choose the OS versions that clients must have to install this package and program.  

    - **Estimated disk space**: Specify the amount of disk space that the program requires to run on the computer. The default setting is **Unknown**. If necessary, specify a whole number greater than or equal to zero. If you set a value, also select units for the value.  

    - **Maximum allowed run time (minutes)**: Specify the maximum time that you expect the program to run on the client computer. The default value is **120** minutes. Only use whole numbers greater than zero.  

        > [!IMPORTANT]  
        > If you use maintenance windows on the same collection to which you deploy this program, a conflict could occur if the **Maximum allowed run time** is longer than the scheduled maintenance window. If you set the maximum run time to **Unknown**, the program starts to run during the maintenance window. It then continues to run as needed after the maintenance window is closed. If you set the maximum run time to a specific period that's greater than the length of any available maintenance window, then the client doesn't run the program.  

        If you set this value to **Unknown**, Configuration Manager sets the maximum allowed run time as 12 hours (720 minutes).  

        > [!NOTE]  
        > If the program exceeds the maximum run time, Configuration Manager stops it if the following conditions are met:
        >
        > - You enable the option to **Run with administrative rights**
        > - You don't enable the option to **Allow users to view and interact with the program installation**  

## Deploy packages and programs  

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Application Management**, and select the **Packages** node.  

2. Select the package that you want to deploy. In the **Home** tab of the ribbon, in the **Deployment** group, choose **Deploy**.  

3. On the **General** page of the **Deploy Software Wizard**, specify the name of the package and program that you want to deploy. Select the collection to which you want to deploy the package and program, and any optional comments.  

    To store the package content on the collection's default distribution point group, select the option to **Use default distribution point groups associated to this collection**. If you didn't associate this collection with a distribution point group, this option is unavailable.  

4. On the **Content** page, choose **Add**. Select the distribution points or distribution point groups to which you want to distribute the content for this package and program.  

5. On the **Deployment Settings** page, configure the following settings:  

    - **Purpose**: Choose one of the following options:

        - **Available**: The user sees the published package and program in Software Center and can install it on demand.  

        - **Required**: The package and program is deployed automatically, according to the configured schedule. In Software Center, you can track its deployment status and install it before the deadline.  

        > [!NOTE]
        > If multiple users are signed into the device, package and task sequence deployments may not appear in Software Center.

    - **Send wake-up packets**: If you set the deployment purpose to **Required** and select this option, the site first sends a wake-up packet to computers at the installation deadline time. Before you can use this option, configure computers for Wake On LAN. For more information, see [How to configure Wake on LAN](../../core/clients/deploy/configure-wake-on-lan.md).  

    - **Allow clients on a metered Internet connection to download content after the installation deadline, which might incur additional costs**  

    > [!NOTE]  
    > When you deploy a package and program, the option to **Pre-deploy software to the user's primary device** isn't available.  

6. On the **Scheduling** page, configure when to deploy this package and program to client devices.  

    The options on this page vary depending on whether you set the deployment action to **Available** or **Required**.  

    For **Required** deployments, configure the rerun behavior for the program from the **Rerun behavior** drop-down menu. Choose from the following options:  

    | Rerun behavior | Description |
    |----------------|-------------|
    | **Never rerun deployed program** | The client won't rerun the program. This behavior happens even if the program originally failed or if the program files are changed. |
    | **Always rerun program** | The client always reruns the program when the deployment is scheduled. This behavior happens even if the program has already successfully run. It's useful with recurring deployments when you update the program. |
    | **Rerun if failed previous attempt** | The client reruns the program when the deployment is scheduled, only if it failed on the previous run attempt. |
    | **Rerun if succeeded on previous attempt** | The client reruns the program only if it previously ran successfully on the client. This behavior is useful with recurring deployments when you routinely update the program, and each update requires the previous update to be successfully installed. |

7. On the **User Experience** page, specify the following information:  

    - **Allow users to run the program independently of assignments**: Users can install this software from Software Center regardless of any scheduled installation time.  

    - **Software installation**: Allows the software to be installed outside of any configured maintenance windows.  

    - **System restart (if required to complete the installation)**: If the software installation requires a device restart to finish, allow this action to happen outside of any configured maintenance windows.  

    - **Embedded devices**: When you deploy packages and programs to Windows Embedded devices that are write-filter-enabled, you can specify that they install packages and programs on the temporary overlay and commit changes later. Alternately, commit the changes on the installation deadline or during a maintenance window. When you commit changes on the installation deadline or during a maintenance window, a restart is required, and the changes persist on the device.  

        > [!NOTE]  
        > When you deploy a package or program to a Windows Embedded device, make sure that the device is a member of a collection that has a configured maintenance window. For more information about how maintenance windows are used when you deploy packages and programs to Windows Embedded devices, see [Creating Windows Embedded applications](../get-started/creating-windows-embedded-applications.md).  

8. On the **Distribution Points** page, specify the following information:  

    - **Deployment options**: Specify the action that a client when it uses a distribution point in its current boundary group. Also select the action for the client when it uses a distribution point from a neighbor boundary group or the default site boundary group.

        > [!IMPORTANT]  
        > If you configure the deployment option to **Run program from distribution point**, make sure to enable the option to **Copy the content in this package to a package share on distribution points** on the **Data Access** tab of the package properties. Otherwise the package is unavailable to run from distribution points.  

    - **Allow clients to use distribution points from the default site boundary group**: When this content isn't available from any distribution point in the current or neighbor boundary groups, enable this option to let them try distribution points in the site default boundary group.

9. Complete the wizard.  

View the deployment in the **Deployments** node of the **Monitoring** workspace and in the details pane of the package deployment tab when you select the deployment. For more information, see [Monitor packages and programs](#monitor-packages-and-programs).  


## Monitor packages and programs

To monitor package and program deployments, use the same procedures that you use to monitor applications as detailed in [Monitor applications](monitor-applications-from-the-console.md).  

Packages and programs also include a number of built-in reports, which enable you to monitor information about the deployment status of packages and programs. These reports have the report category of **Software Distribution - Packages and Programs** and **Software Distribution - Package and Program Deployment Status**.  

For more information about how to configure reporting in Configuration Manager, see [Introduction to reporting](../../core/servers/manage/introduction-to-reporting.md).  


## Manage packages and programs

In the **Software Library** workspace, expand **Application Management**, and select the **Packages** node. Select the package that you want to manage, and then choose a management task.  

### Create Prestage Content File

Opens the **Create Prestaged Content File Wizard**, to create a file that contains the package content. Use this file to manually import the package to a remote distribution point. This action is useful when you have low network bandwidth between the site server and the distribution point.

### Create Program

Opens the **Create Program Wizard**, to create a new program for this package.

### Export

Opens the **Export Package Wizard**, to export the selected package and its content to a file. Use this file to import the file to another hierarchy.

### Deploy

Opens the **Deploy Software Wizard**, to deploy the selected package and program to a collection. For more information, see [Deploy packages and programs](#deploy-packages-and-programs).

### Distribute content

Opens the **Distribute Content Wizard**, to send the content for a package and program to selected distribution points or distribution point groups.

### Import

Opens the **Import Package Wizard**, to import a previously exported package from a .zip file.

> [!TIP]
> When you import an object in the Configuration Manager console, it imports to the current folder. In earlier versions, Configuration Manager always put imported objects in the root node.<!--6601203-->

### Update distribution points

Updates distribution points with the latest content for the selected package and program.

## Next steps

- [Scripts](create-deploy-scripts.md)

- [Package Conversion Manager](../pcm/package-conversion-manager.md)

- [Package definition files](package-definition-files.md)
