---
title: Package definition files
titleSuffix: Configuration Manager
description: Learn about using package definition files to create packages and programs in Configuration Manager
ms.date: 07/26/2019
ms.subservice: app-mgt
ms.service: configuration-manager
ms.topic: how-to
author: baladelli
manager: apoorvseth
ms.author: baladell
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Package definition files

*Applies to: Configuration Manager (current branch)*

Package definition files are scripts to help you automate the creation of [Packages and programs](packages-and-programs.md) in Configuration Manager. They provide all of the information that Configuration Manager needs to create a package and program, except for the location of package source files.

## About the package definition file format

Each package definition file is an ASCII or UTF-8 text file that uses the .ini file format. It contains the following sections:  

### [PDF]

This section identifies the file as a package definition file. It contains the following information:  

- **Version**: Specify the version of the package definition file format that the file uses. This version corresponds to the version of Configuration Manager for which it was written. This entry is required.  

### [Package Definition]

Specify the properties of the package and program. It provides the following information:  

- **Name**: The name of the package, up to 50 characters.  

- **Version** (optional): The version of the package, up to 32 characters.  

- **Icon** (optional): The file that contains the icon to use for this package. If specified, this icon replaces the default package icon in the Configuration Manager console.

- **Publisher**: The publisher of the package, up to 32 characters.

- **Language**: The language version of the package, up to 32 characters.

- **Comment** (optional): A comment about the package, up to 127 characters.

- **ContainsNoFiles**: This entry indicates if the package has any source files.  

- **Programs**: The programs that you define for this package. Each program name corresponds to a **[Program]** section in this package definition file.  

    Example:  

    `Programs=Typical, Custom, Uninstall`  

- **MIFFileName**: The name of the Management Information Format (MIF) file that contains the package status, up to 50 characters.  

- **MIFName**: The name of the package for MIF matching, up to 50 characters.  

- **MIFVersion**: The version number of the package for MIF matching, up to 32 characters.  

- **MIFPublisher**: The software publisher of the package for MIF matching, up to 32 characters.  

### [Program]

Include a [Program] section for each program that you specify in the **Programs** entry in the **[Package Definition]** section. This section defines each program. Each program section provides the following information:  

- **Name**: The name of the program, up to 50 characters. This entry must be unique within a package.  

- **Icon** (optional): Specify the file that contains the icon to use for this program. This icon replaces the default program icon in the Configuration Manager console. The client also displays this icon when you deploy the program to a collection.

- **Comment** (optional): A comment about the program, up to 127 characters.

- **CommandLine**: Specify the command line for the program, up to 127 characters. The command is relative to the package source folder.

- **StartIn**: Specify the working folder for the program, up to 127 characters. This entry can be an absolute path on the client computer or a path that's relative to the package source folder.

- **Run**: Specify the program mode in which the program runs. You can specify **Minimized**, **Maximized**, or **Hidden**. If you don't include this entry, the program runs in normal mode.  

- **AfterRunning**: Specify any special action that occurs after the program successfully completes. Options available are **SMSRestart**, **ProgramRestart**, or **SMSLogoff**. If you don't include this entry, the program doesn't run a special action.  

- **EstimatedDiskSpace**: Specify the amount of disk space that the software program requires to run on the computer. The default value is **Unknown**. You can set the value as a whole number greater than or equal to zero. If you specify a value, also include the units for the value.  

    Example:  

    `EstimatedDiskSpace=38MB`  

- **EstimatedRunTime**: Specify the estimated duration in minutes that you expect the program to run on the client computer. The default value is **120**. You can set the value as a whole number greater than zero, or **Unknown**.  

    Example:  

    `EstimatedRunTime=25`  

- **SupportedClients**: Specify the processors and operating systems on which this program runs. Separate the platforms by commas. If you don't include this entry, the client doesn't check supported platforms for this program.  

- **SupportedClientMinVersionX**, **SupportedClientMaxVersionX**: Specify the beginning-to-ending range for version numbers for the operating systems that are specified in the **SupportedClients** entry.  

    Example:  

    ```INI
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

- **AdditionalProgramRequirements** (optional): Provide any other information or requirements for client computers, up to 127 characters.

- **CanRunWhen**: Specify the user status that the program requires to run on the client computer. Available values are **UserLoggedOn**, **NoUserLoggedOn**, or **AnyUserStatus**. The default value is **UserLoggedOn**.  

- **UserInputRequired**: Specify whether the program requires interaction with the user. Available values are **True** or **False**. The default value is **True**. This entry is set to **False** if **CanRunWhen** isn't set to **UserLoggedOn**.  

- **AdminRightsRequired**: Specify whether the program requires administrative credentials on the computer to run. Available values are **True** or **False**. The default value is **False**. This entry is set to **True** if **CanRunWhen** isn't set to **UserLoggedOn**.  

- **UseInstallAccount**: Specify whether the program uses the client software installation account when it runs on client computers. By default, this value is **False**. This value is also **False** if **CanRunWhen** is set to **UserLoggedOn**.  

- **DriveLetterConnection**: Specify whether the program requires a drive letter connection to the package files on the distribution point. You can specify **True** or **False**. The default value is **False**, which enables the program to use a Universal Naming Convention (UNC) connection. When this value is set to **True**, the client uses the next available drive letter, starting with Z: and proceeding backwards.  

- **SpecifyDrive** (optional): Specify a drive letter that the program requires to connect to the package files on the distribution point. This setting forces the use of the specified drive letter for client connections to distribution points.

- **ReconnectDriveAtLogon**: Specify whether the computer reconnects to the distribution point when the user signs in. Available values are **True** or **False**. The default value is **False**.  

- **DependentProgram**: Specify a program in this package that must run before the current program. This entry uses the format `DependentProgram=<ProgramName>`, where `<ProgramName>` is the **Name** entry for that program in the package definition file. If there are no dependent programs, leave this entry empty.  

    Examples:  

    `DependentProgram=Admin`  
    `DependentProgram=`  

- **Assignment**: Specify how the program is assigned to users. This value can be:

    - **FirstUser**: Only the first user who signs in to the client runs the program
    - **EveryUser**: Every user who signs in runs the program

    When **CanRunWhen** isn't set to **UserLoggedOn**, this entry is set to **FirstUser**.  

- **Disabled**: Specify whether you can deploy this program to clients. Available values are **True** or **False**. The default value is **False**.  


## Use a package definition file  

1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Application Management**, and select the **Packages** node.  

2. On the **Home** tab of the ribbon, in the **Create** group, choose **Create Package from Definition**.  

3. On the **Package Definition** page of the **Create Package from Definition Wizard**, choose an existing package definition file. To open a new package definition file, choose **Browse**. After you specify a new package definition file, select it from the **Package definition** list.

4. On the **Source Files** page, specify information about any required source files for the package and program.  

5. If the package requires source files, on the **Source Folder** page, specify the location from where the site can get the source files.  

6. Complete the wizard.  


## See also

[Packages and programs](packages-and-programs.md)
