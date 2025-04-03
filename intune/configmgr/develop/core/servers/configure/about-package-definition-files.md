---
description: Learn how to use Configuration Manager to help automate package creation using package definition files.
title: About Package Definition Files
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: concept-article
ms.assetid: fbd5743c-ff78-4890-9e32-5a133c02878c
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# About Package Definition Files
Package definition files are predefined scripts that you can use to help automate package creation with Configuration Manager. These are files that contain the package and program information that is needed to distribute a package to clients, with the exception of the source file location.  

 Package definition files often come with an application's source files or are available from the application's developer. Configuration Manager also has a selection of package definition files that are automatically imported and available in the Create Package from Definition Wizard. 

 For more information about the format of these files, see the Package Definition File Format section later in this topic.  

## Package Definition File Format  
 Each package definition file is an ASCII text file following a standard .ini file format and containing the following sections:  

### [PDF]  
 This section identifies the file as a package definition file and contains the following information:  

 **Version**  
 Specifies the version of the package definition file format that is used by the file, corresponding to the version of System Management Server (SMS) or Configuration Manager for which they were written. This entry is required.  

### [Package Definition]  
 This section of the package definition file specifies the overall properties of the package and provides the following information:  

 Name  
 The name of the package, up to 50 characters. This entry is required.  

 Version  
 The version of the package, up to 32 characters. This entry is optional.  

 Icon  
 Specifies the file that contains the icon to use for this package. If it is used, this icon replaces the default package icon in the Configuration Manager console. This entry is optional.  

 Publisher  
 The publisher of the package, up to 32 characters. This entry is required.  

 Language  
 The language version of the package, up to 32 characters. This entry is required.  

 Comment  
 An optional comment about the package, up to 127 characters.  

 ContainsNoFiles  
 This entry indicates whether or not a source is associated with the package.  

 Programs  
 Specifies the programs that are defined for this package. Each program name corresponds to a [Program] section in this package definition file. This entry is required.  

 For example:  

 `Programs=Typical, Custom, Uninstall`  

 MIFFileName  
 The name of the Management Information Format (MIF) file that contains the package status, up to 50 characters.  

 MIFName  
 The name of the package (for MIF matching), up to 50 characters.  

 MIFVersion  
 The version number of the package (for MIF matching), up to 32 characters.  

 MIFPublisher  
 The software publisher of the package (for MIF matching), up to 32 characters.  

### [Program]  
 For each program specified in the **Programs** entry in the **[Package Definition]** section, the package definition file must include a section that defines that program. The file must contain a **[Program]** section for all programs that are contained within that package.  

 Name  
 The name of the program, up to 50 characters. This entry must be unique within a package and is used when defining advertisements. On client computers, the name of the program is shown in **Run Advertised Programs** in Control Panel. This entry is required.  

 Icon  
 Specifies the file that contains the icon to use for this program. If it is used, this icon replaces the default program icon in the Configuration Manager console and is displayed on client computers when the program is advertised. This entry is optional.  

 Comment  
 An optional comment about the program, up to 127 characters.  

 CommandLine  
 Specifies the command line for the program, up to 127 characters. The command is relative to the package source folder, if there is package source. This entry is required.  

 StartIn  
 The working folder for the program, up to 127 characters. This entry can be an absolute path on the client computer or a path relative to the package source folder. This entry is required.  

 Run  
 Specifies the program mode in which the program runs. You can specify **Minimized**, **Maximized**, or **Hidden**. If this entry is not included, the program runs in normal mode.  

 AfterRunning  
 Specifies any special action that occurs after the program is completed successfully. Available options are **SMSRestart**, **ProgramRestart**, or **SMSLogoff**. If this entry is not included, the program does not run a special action.  

 EstimatedDiskSpace  
 Specifies the amount of disk space that the software program requires to run on the computer. This can be specified as **Unknown** (the default setting) or as a whole number that is greater than or equal to zero. If a value is specified, units for the value must also be specified.  

 For example:  

 `EstimatedDiskSpace=38MB`  

 EstimatedRunTime  
 Specifies the estimated time (in minutes) that the program is expected to run on the client computer. This can be specified as **Unknown** (the default setting) or as a whole number greater than zero.  

 For example:  

 `EstimatedRunTime=25`  

 SupportedClients  
 Specifies the processors and operating systems on which this program runs. Each platform must be separated by a comma. If this entry is not included with the package definition file, supported platform checking is disabled for this program.  

 SupportedClientMinVersionX, SupportedClientMaxVersionX  
 Specifies the beginning and ending range for version numbers for the operating systems specified in the **SupportedClients** entry.  

 For example:  

 `SupportedClients=Win NT (I386),Win NT (IA64),Win NT (x64)`  

 `Win NT (I386) MinVersion1=5.00.2195.4`  

 `Win NT (I386) MaxVersion1=5.00.2195.4`  

 `Win NT (I386) MinVersion2=5.10.2600.2`  

 `Win NT (I386) MaxVersion2=5.10.2600.2`  

 `Win NT (I386) MinVersion3=5.20.0000.0`  

 `Win NT (I386) MaxVersion3=5.20.9999.9999`  

 `Win NT (I386) MinVersion4=5.20.3790.0`  

 `Win NT (I386) MaxVersion4=5.20.3790.2`  

 `Win NT (I386) MinVersion5=6.00.0000.0`  

 `Win NT (I386) MaxVersion5=6.00.9999.9999`  

 `Win NT (IA64) MinVersion1=5.20.0000.0`  

 `Win NT (IA64) MaxVersion1=5.20.9999.9999`  

 `Win NT (x64) MinVersion1=5.20.0000.0`  

 `Win NT (x64) MaxVersion1=5.20.9999.9999`  

 `Win NT (x64) MinVersion2=5.20.3790.0`  

 `Win NT (x64) MaxVersion2=5.20.9999.9999`  

 `Win NT (x64) MinVersion3=5.20.3790.0`  

 `Win NT (x64) MaxVersion3=5.20.3790.2`  

 `Win NT (x64) MinVersion4=6.00.0000.0`  

 AdditionalProgramRequirements  
 Optional text that can include any other information or requirements for client computers, up to 127 characters.  

 CanRunWhen  
 Specifies the user status that the program requires to run on the client computer. Available values are **UserLoggedOn**, **NoUserLoggedOn**, or **AnyUserStatus**. The default value is **UserLoggedOn**.  

 UserInputRequired  
 Specifies whether the program requires interaction with the user to complete running. Available values are `True` or `False`. The default value is `True`. This entry is set to `False` if **CanRunWhen** is not set to **UserLoggedOn**.  

 AdminRightsRequired  
 Specifies whether the program requires administrative credentials on the computer to run. Available values are `True` or `False`. The default value is `False`. This entry is set to `True` if **CanRunWhen** is not set to **UserLoggedOn**.  

 DriveLetterConnection  
 Specifies whether the program requires a drive letter connection to the package files on the distribution point. You can specify `True` or `False`. The default value is `False`, which allows the program to use a Universal Naming Convention (UNC) connection. When this value is set to `True`, the next available drive letter is used (starting with Z and proceeding backward).  

 SpecifyDrive  
 Specifies a specific drive letter that the program requires to connect to the package files on the distribution point. Using this entry forces the use of the specified drive letter for client connections to distribution points. This entry is optional.  

 ReconnectDriveAtLogon  
 Specifies whether the computer reconnects to the distribution point when the user logs on. Available values are `True` or `False`. The default value is `False`.  

 DependentProgram  
 Specifies a program (in this package) that must run before the current program. This entry uses the following format:  

 **DependentProgram**=\<**ProgramName>**  

 where **\<ProgramName>** is the Name entry for that program in the package definition file. If there are no dependent programs, leave this entry empty.  

 For example:  

 DependentProgram=Admin  

 DependentProgram=  

 Assignment  
 How the program is assigned to users. This value can be **FirstUser** (only the first user who logs on runs the program) or **EveryUser** (every user who logs on to the client runs the program). When **CanRunWhen** is not set to **UserLoggedOn**, this entry is set to **FirstUser**.  

 Disabled  
 Specifies whether this program can be advertised to clients. Available values are `True` or `False`. The default value is `False`.  

## See Also  
 [Software distribution overview](software-distribution-overview.md)
 [About deployments](about-software-distribution-deployments.md)
