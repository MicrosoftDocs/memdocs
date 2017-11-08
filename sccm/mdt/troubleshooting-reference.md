---

title: "Troubleshoot MDT"
titleSuffix: "Microsoft Deployment Toolkit"
description: "Troubleshooting reference for the Microsoft Deployment Toolkit"
ms.date:  09/09/2016
ms.prod: configuration-manager
ms.technology:
  - mdt
ms.topic: article
ms.assetid:  91a7a69a-deac-4b0f-aac9-b7bd187c53fb

author: angrobe  
ms.author: angrobe  
manager: angrobe

---


## Introduction to Troubleshooting Reference  
 The deployment of operating systems and applications as well as the migration of user state can be a challenging endeavor, even when you are equipped with appropriate tools and guidance. This reference, which is part of Microsoft® Deployment Toolkit (MDT) 2013, provides information on current known issues, possible workarounds for those issues, and troubleshooting guidance.  

> [!NOTE]
>  In this document, *Windows* applies to the Windows 8.1, Windows 8, Windows 7, Windows Server 2012 R2, Windows Server 2012, and Windows Server 2008 R2 operating systems unless otherwise noted. MDT does not support ARM processor–based versions of Windows. Similarly, *MDT* refers to MDT 2013 unless otherwise stated.  

> [!NOTE]
>  The Microsoft Diagnostics and Recovery Toolset (DaRT) contains powerful tools for recovering and troubleshooting client computers that do not start or have become unstable. You can use DaRT to determine the cause of a crash, restore lost files, and so on. You can also use DaRT as a troubleshooting tool when developing and deploying a Windows operating system. For example, if a built image fails to start correctly, you can start the client computer containing the image by using ERD Commander—a diagnostic environment. Then, you can explore the client computer’s hard disk, view the event log, remove updates, change operating system settings, and so on. DaRT is part of the Microsoft Desktop Optimization Pack for Software Assurance. To learn more about DaRT, see [http://www.microsoft.com/windows/enterprise/products-and-technologies/mdop/dart.aspx](http://www.microsoft.com/windows/enterprise/products-and-technologies/mdop/dart.aspx).  

## Understanding Logs  
 Before effective troubleshooting of MDT can begin, you must have a clear understanding of the many .log files used during an operating system deployment. When you know which log files to research for what failure condition and at what time, issues that were once mysterious and difficult to understand may become clear and understandable.  

 The MDT log file format is designed to be read by Trace32, which is part of the System Center Configuration Manager 2007 Toolkit V2, available for download from the [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=9257). The logs can also be read by the Configuration Manager Trace Log Tool (CMTrace) that is available with System Center 2012 Configuration Manager and later versions. Use these tools whenever possible to read the log files, because it makes finding errors much easier.  

 The rest of this section details the log files created during deployment as well as during Windows Setup. This section also provides examples of when to use the files for troubleshooting.  

### MDT Logs  
 Each MDT script automatically creates log files when running. The names of these log files match the name of the script—for example, ZTIGather.wsf creates a log file named *ZTIGather.log*. Each script also updates a common master log file (BDD.log) that aggregates the contents of the log files that MDT scripts create. MDT log files reside in C:\MININT\SMSOSD\OSDLOGS during the deployment process. Depending on the type of deployment being conducted, the log files are moved at the completion of the deployment to either %WINDIR%\SMSOSD or %WINDIR%\TEMP\SMSOSD. For Lite Touch Installation (LTI) deployments, the logs start in C:\MININT\SMSOSD\OSDLogs. They end up in %WINDIR%\TEMP\DeploymentLogs when the task sequence processing is complete.  

 MDT creates the following log files:  

-   **BDD.log**. This is the aggregated MDT log file that is copied to a network location at the end of the deployment if you specify the **SLShare** property in the Customsettings.ini file.  

-   **LiteTouch.log**. This file is created during LTI deployments. It resides in %WINDIR%\TEMP\DeploymentLogs unless you specify the **/debug:true** option.  

-   ***Scriptname*.log**. This file is created by each MDT script. *Scriptname* represents the name of the script in question.  

-   **SMSTS.log**. This file is created by the Task Sequencer and describes all Task Sequencer transactions. Depending on the deployment scenario, it may reside in %TEMP%, %WINDIR%\System32\ccm\logs, or C:\\_SMSTaskSequence, or C:\SMSTSLog.  

-   **Wizard.log**. The deployment wizards create and update this file.  

-   **WPEinit.log**. This file is created during the Windows PE initialization process and is useful for troubleshooting errors encountered while starting Windows PE.  

-   **DeploymentWorkbench_*id*.log**. This log file is created in the %temp% folder when you specify **a /debug** when starting the Deployment Workbench.  

### Configuration Manager Operating System Deployment Logs  
 For information about which operating system deployment log files created by Microsoft System Center 2012 R2 Configuration Manager, see [Technical Reference for Log Files in Configuration Manager](http://technet.microsoft.com/library/hh427342.aspx).  

 When running the Windows User State Migration Tool (USMT), MDT automatically adds the logging options to save the USMT log files to the MDT log file locations. The log files and when they are created are as follows:  

-   **USMTEstimate.log**. Created when estimating the USMT requirements  

-   **USMTCapture.log**. Created by the USMT when capturing data  

-   **USMTRestore.log**. Created by the USMT when restoring data  

 The ZeroTouchInstallation.vbs script automatically scans the USMT progress log files for errors and warnings. The script generates event ID 41010 to Microsoft System Center Operations Manager with the following summary (where *usmt_type* is **ESTIMATE**, **SCANSTATE**, or **LOADSTATE**; *error_count* is the total number of errors found; and *warning_count* is the total number of warnings found):  

```  
ZTI USMT <usmt_type> reported <error_count> errors and <warning_count> warnings  
```  

 If the error count is greater than 0, this event is an Error type. If the warning count is greater than 0 with no errors, then the event is a Warning type. Otherwise, the event is an Informational type.  

## Identifying Error Codes  
 REF _Ref308172724 \h Table 1 lists the error codes that the MDT scripts create and provides a description of each error code. These error codes are recorded in the BDD.log file.  

### Table  SEQ Table \\* ARABIC 1. Error Codes and Their Description  

|||  
|-|-|  
|**Error code**|**Description**|  
|5201|A connection to the deployment share could not be made. The deployment will not proceed.|  
|5203|A connection to the deployment share could not be made. The deployment will not proceed.|  
|5205|A connection to the deployment share could not be made. The deployment will not proceed.|  
|5206|The Deployment Wizard was canceled or did not complete successfully. The deployment will not proceed.|  
|5207|A connection to the deployment share could not be made. The deployment will not proceed.|  
|5208|**DeploymentType** is not set. Must set some value for **SkipWizard**.|  
|5208|Unable to find the SMS Task Sequencer. The deployment will not proceed.|  
|5400|Create object: **Set *class_instance* = New *class_name***|  
|5490|Create MSXML2.DOMDocument.|  
|5495|Create MSXML2.DOMDocument.ParseErr.ErrCode.|  
|5496|LoadControlFile.FindFile: *ConfigFile*|  
|5601|Verify OS guid: %OSGUID% exists.|  
|5602|Open XML with OSGUID: %OSGUID%.|  
|5610|Verify file.|  
|5630|Verify file: *ImagePath*.|  
|5640|Verify file: *ImagePath*.|  
|5641|FindFile: ImageX.exe.|  
|5643|Find BootSect.exe.|  
|5650|Verify directory: *SourcePath*.|  
|5651|Verify directory: *SourcePath*\Platform.|  
|5652|FindFile: bootsect.exe.|  
|6001|Verify drive.|  
|6002|Verify drive.|  
|6010|Test for TSGUID.|  
|6020|Robocopy returned value: *Value*.|  
|6021|Robocopy returned value: *Value*.|  
|6101|Check for file: *DeployCab*.|  
|6102|Expand Sysprep files from DEPLOY.CAB.|  
|6111|Run Sysprep.exe.|  
|6121|Run Sysprep.|  
|6191|Test for **CloneTag** in registry to verify Sysprep completed.|  
|6192|Test for **SystemSetupInProgress** in registry to verify Sysprep completed.|  
|6401|Authorized DHCP server.|  
|6501|Computer backup not possible, no network path (**BackupShare**, **BackupDir**) specified.|  
|6502|ERROR - Unable to locate IMAGEX, unable to perform backup.|  
|6601|GetObject(... root/wmi:BCDStore).|  
|6602|BCD.OpenStore (*BCDStore*).|  
|6701|Configured protectors.|  
|6702|Moved boot files.|  
|6703|Create BDE partition.|  
|6704|Defragment drive.|  
|6705|Shrink drive.|  
|6706|Testing for more than 1 partition.|  
|6707|Create boot files.|  
|6708|Encrypt the disk.|  
|6709|Connect to MicrosoftVolumeEncryption WMI provider.|  
|6710|Encrypting the disk.|  
|6711|**ProtectKeyWithTPM**.|  
|6712|**ProtectKeyWithTPMAndPIN**.|  
|6713|**ProtectKeyWithTPMAndStartupKey**.|  
|6714|Save external key to file.|  
|6715|Protect with external key.|  
|6716|Save external key to file.|  
|6717|Protect key with numerical password.|  
|6718|**GetKeyProtectorNumberialP@ssword.**|  
|6718|Save password to file.|  
|6719|Open *PasswordFile*.|  
|6720|Encrypt the drive.|  
|6721|Open *DiskPartFile*.|  
|6722|Create partition.|  
|6723|Get existing BDE drive.|  
|6724|Open *DiskPartFile*.|  
|6727|Attempt to open *DiskPartFile*.|  
|6729|Create text file *DiskPartFile*.|  
|6730|Execute **cmd /c DISKPART.EXE /s *DiskPartFile* >> *LogPath*\ZTIMarkActive_diskpart.log 2>&1**|  
|6731|Find bcdboot.exe.|  
|6732|Connect to Microsoft TPM provider.|  
|6733|Get a TPM instance in the provider class.|  
|6734|Get TPM instance.|  
|6735|Check to see if TPM is enabled.|  
|6736|Check to see if TPM is activated.|  
|6737|Check to see if TPM is owned.|  
|6738|Check to see if TPM ownership is allowed.|  
|6739|Check to see if TPM is enabled.|  
|6740|Check to see if TPM is activated.|  
|6741|Check to see if TPM is owned and ownership is allowed.|  
|6741|TPM Owner Password set|  
|6742|TPM Owner P@ssword set to **AdminP@ssword**.|  
|6743|Set TPM Owner P@ssword to value.|  
|6744|Check to see if TPM is enabled.|  
|6745|Check TPM owner.|  
|6746|Check for endorsement key pair.|  
|6747|Check to see if TPM is activated.|  
|6748|Check to see if TPM ownership is allowed.|  
|6749|Convert owner p@ssword to owner authorization.|  
|6750|Create endorsement key pair.|  
|6751|Change owner authorization.|  
|6752|Run **Cmd**.|  
|6753|Validate TPM.|  
|6754|Get BDE instance.|  
|6755|Protect key with TPM.|  
|6756|Check for removable media to configure. **ProtectKeyWithTpmAndStartupKey**.|  
|6757|Protect key with TPM and startup key.|  
|6758|Look for BDE pin.|  
|6759|Protect key with TPM and Pin.|  
|6760|Find removable media for **BDEKeyLocation**.|  
|6761|Protect with external key.|  
|6762|Recovery P@ssword being saved to *PasswordFile*.|  
|6764|Configure BitLocker policy.|  
|7000|Unable to locate ZTIConfigure.xml; aborting.|  
|7001|Looking for unattend AnswerFile.|  
|7100|ERROR - This script should only run in the full OS.|  
|7101|ERROR - Not enough values supplied for generating DCPromo answer file.|  
|7102|ERROR - Mandatory properties for creating a new replica DC were not specified.|  
|7103|ERROR - Mandatory properties for creating a new child domain were not specified.|  
|7104|ERROR - Mandatory properties for creating a new forest were not specified.|  
|7105|ERROR - Mandatory properties for creating a new forest were not specified.|  
|7200|Unable to configure DHCP server because the service is not installed.|  
|7201|Unable to read the scope details; `GetScopeDetails()` failed.|  
|7202|Not enough values specified for scope creation.|  
|7203|Not enough values provided to set the IP range for this scope.|  
|7204|No value specified for scope exclusion range.|  
|7300|Unable to issue DNS commands.|  
|7700|Not a New Computer scenario; exiting disk partition.|  
|7701|Disk is not large enough for System and BDE partitions, Required = 1.5 GB.|  
|7702|Disk is not large enough for System and WinRE partitions, Required = 10 GB.|  
|7703|DeployRoot is on disk # *DiskIndex*. Running an OEM Scenario: Skip.|  
|7704|Running an OEM Scenario: Skip.|  
|7704|Extended and logical partitions are not allowed with BitLocker.|  
|7712|Verify Drive/*Volume Drive* is present. Format.|  
|7900|Findfile: Microsoft.BDD.PnpEnum.exe.|  
|7901|**AllDrivers.Exists("*GUID*").**|  
|7904|**AllDrivers.Exists("*GUID*").**|  
|9200|Findfile(PkgMgr.exe).|  
|9601|ERROR - ZTITatoo state restore task should be running in the full OS; aborting.|  
|9701|Nonzero return code from USMT estimate, rc = *Error*.|  
|9702|User state capture not possible; insufficient local space and no network path (UDShare, UDDir) specified.|  
|9703|Nonzero return code from USMT capture, rc = *Error*.|  
|9704|No valid command line option was specified.|  
|9801|ERROR - Attempting to deploy a client operating system to a machine running a server operating system.|  
|9802|ERROR - Attempting to deploy a server operating system to a machine running a client operating system.|  
|9803|ERROR - Machine is not authorized for upgrading (OSInstall=*OSInstall*); aborting.|  
|9804|ERROR - *Memory* MB of memory is insufficient. At least *Memory* MB of memory is required.|  
|9805|ERROR - Processor speed of *ProcessorSpeed* MHz is insufficient.  At least a *ProcessorSpeed* MHz processor is required.|  
|9806|ERROR - insufficient space is available on *Drive*. An additional *Size* MB is required.|  
|9807|ERROR - insufficient space is available on *Drive*. An additional *Size* MB is required.|  
|9901|The ZTIWindowsUpdate script should not run in Windows PE.|  
|9902|ZTIWindowsUpdate has run and failed too many times. Count = *Count*.|  
|9903|Unexpected issue installing the updated Windows Update Agent, rc = *Error*.|  
|9904|Failed to create object: **Microsoft.Update.Session**.|  
|9905|Failed to create object: **Microsoft.Update.UpdateColl**.|  
|9906|Critical file *File* was not found; aborting.|  
|10000|Create object: **Set oLTICleanup = New LTICleanup**.|  
|10201|Unable to Join Domain *Domain*. Stop installation.|  
|10203|FindFile(LTISuspend.wsf).|  
|10204|Run Program *LTISuspend*.|  
|41024|Run ImageX.|  
|52012|All the wizard parameters are not set.|  

 REF _Ref308173499 \h Listing 1 provides an excerpt from a log file that illustrates how to find the error code. In this excerpt, the error code reported is 5001.  

 **Listing  SEQ Equation \\\* ARABIC 1. Excerpt from an SMSTS.log File That Contains Error Code 5001**  

```  
.  
.  
.  
The operating system installation failed. Please contact your system administrator for assistance.  

The action "Zero Touch Installation - Validation" failed with exit code 5001  
.  
.  
.  

```  

### Converting Error Codes  
 Many error codes presented in the log files seem cryptic and difficult to correlate to an actual error condition. However, the following process demonstrates how to convert an error code and obtain meaningful information that may assist in problem resolution.  

 **Problem**: An image capture fails with error code 0x80070040.  

 **Possible Solution 1**: The error code presented is in hexadecimal format that you need to convert to decimal format. To do this, you need a scientific calculator, and the calculator included with Windows operating systems is well suited to this task.  

 **To convert an error code**  

1.  Click **Start**, and then point to **All Programs**. Point to **Accessories**, and then click **Calculator**.  

2.  From the **View** menu, click **Scientific**.  

3.  Select **Hex**, and then enter the last four digits of the code—in this case, **0040**, as shown in  REF _Ref308173547 \h Figure 1.  

     ![TroubleshootingReference1](../Image/TroubleshootingReference1.jpg "TroubleshootingReference1")  
Figure  SEQ Figure \\* ARABIC 1. Error conversion  

     **Figure  SEQ Figure \\\* ARABIC 1. Error conversion**  

     Notice that leading zeros are not displayed while the calculator is in Hexadecimal mode.  

4.  Select **Dec**.  

     The hexadecimal value *40* is converted to a decimal value of *64*.  

5.  Open a Command Prompt window, type **NET HELPMSG 64**, and then press ENTER.  

     The **NET HELPMSG** command translates the numerical error code into meaningful text. In the case of the error code provided here, it translates to “The specified network name is no longer available.”  

 This information indicates that a networking problem may exist on the target computer or between the target computer and the server on which the deployment share resides. These problems might include network drivers not being installed properly or a mismatch in speed and duplex settings.  

 **Possible Solution 2:** Use the Microsoft Exchange Server Error Code Look-up utility. This command-line utility is valuable in assisting with error code translation. It is available for download from the [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=985).  

### Review of Sample Logs  
 MDT creates log files that you can use to troubleshoot problems in the MDT deployment process. The following sections provide examples of how to use the MDT log files to troubleshoot the deployment process:  

-   Problems that relate to failures accessing the MDT database (MDT DB), as described in [Failure to Access the Database](#FailuretoAccesstheDatabase)  

####  <a name="FailuretoAccesstheDatabase"></a> Failure to Access the Database  
 **Problem:** An error occurs while running a deployment that used a CustomSettings.ini file containing numerous sections and specifying, with the **Priority** property, the priority of each section to be processed. BDD.log contains the following error messages:  

-   ```  
    ERROR - Opening Record Set (Error Number = -2147217911) (Error Description: The SELECT permission was denied on the object 'ComputerAdministrators', database 'AdminDB', schema 'dbo'.)  
    ```  

-   ```  
    ADO error: The SELECT permission was denied on the object 'ComputerAdministrators', database 'AdminDB', schema 'dbo'. (Error #-2147217911; Source: Microsoft OLE DB Provider for SQL Server; SQL State: 42000; NativeError: 229  
    ```  

-   ```  
    ERROR - Unhandled error returned by ZTIGather: Object required (424)  
    ```  

> [!NOTE]
>  For clarity, the log file contents above have been represented as they appear while being viewed using the Trace32 program.  

 **Possible Solution:** The issue, as pointed out on the first line of the log file sample, is that permission to access the database was denied. Therefore, the script cannot establish a secure connection to the database, possibly because a user ID and password were not available. As a result, database access was attempted using the computer account. The easiest way to work around this issue is to grant everyone Read access to the database.  

## Troubleshooting  
 Prior to embarking on in\-depth troubleshooting processes, review the following items and ensure that any associated requirements have been met:  

-   Installation issues can result if all software and hardware prerequisites have not been met.  

### Application Installation  
 Review the problems and solutions for application installation issues:  

-   Installation source files that are blocked for security reasons as described in [Blocked Executables](#BlockedExecutables)  

-   Loss of network connectivity as described in [Lost Network Connections](#LostNetworkConnections)  

-   Installation error 30029 while installing the 2007 Microsoft Office system or related files as described in [The 2007 Microsoft Office System](#MicrosoftOfficeSystem)  

####  <a name="BlockedExecutables"></a> Blocked Executables  
 **Problem:** If installation source files are downloaded from the Internet, it is likely that they will be marked with one or more NTFS file system data streams. For more information about NTFS data streams, see [File Streams](http://msdn2.microsoft.com/library/aa364404\(VS.85\).aspx). The existence of NTFS file system data streams might cause an **Open File – Security Warning** prompt to be displayed. The installation will not proceed until you click **Run** at the prompt.  

 As  REF \_Ref308173670 \\h Figure 2 shows, you can view NTFS file system data streams using the **More** command and the [Streams utility](http://technet.microsoft.com/sysinternals/bb897440.aspx).  

 ![TroubleshootingReference2](../Image/TroubleshootingReference2.jpg "TroubleshootingReference2")  
Figure  SEQ Figure \\\* ARABIC 2. NTFS data streams  

 **Figure 2. NTFS data streams**  

 **Possible Solution 1:** Right\-click the installation source file, and then click **Properties**. Click **Unblock**, and then click **OK** to remove the NTFS file system data streams from the file. Repeat this process for each installation source file that is blocked by the existence of one or more NTFS file system data streams.  

 **Possible Solution 2:** Use the Streams utility, as  REF \_Ref308173670 \\h Figure 2 shows, to remove the NTFS file system data streams from the installation source file. The Streams utility can remove NTFS file system data streams from one or more files or folders at once.  

####  <a name="LostNetworkConnections"></a> Lost Network Connections  
 **Problem:** An installation may fail if it installs device drivers or alters device and network configurations. These changes may result in a lapse in network connectivity that causes the installation to fail.  

 **Possible Solution:** Implement the ZTICacheUtil.vbs script to enable download and execution for the installation. This script is designed to tweak the advertisement to enable download and execute. The download uses Background Intelligent Transfer Service \(BITS\) if the Configuration Manager distribution point is Web\-based Distributed Authoring and Versioning and BITS enabled. At the same time, it modifies Configuration Manager to run the ZTICache.vbs script first, which makes sure the program does not delete itself during the deployment process.  

####  <a name="MicrosoftOfficeSystem"></a> The 2007 Microsoft Office System  
 **Problem:** While deploying the 2007 Office system and including a Windows Installer patch \(MSP\) file, the installation may fail with error code 30029.  

 Further investigation in the ZTIApplications.log shows the following messages:  

-   ```  
    About to run command: \\Server\Deployment$\Tools\X86\bddrun.exe \\Server\Share\Microsoft\Office\2007\Professional\setup.exe /adminfile \\Server\Share\Microsoft\Office\2007\Professional\file.msp  
    ```  

-   ```  
    ZTI Heartbeat: command has been running for 12 minutes (process ID 1600) Return code from command = 30029  
    ```  

-   ```  
    Application Microsoft Office 2007 Professional returned an unexpected return code: 30029  
    ```  

 **Possible Solution 1:** Relocate the MSP file to the Updates directory, and then run setup.exe without specifying the **\/adminfile** option. For more information about deploying updates during the installation, see [Deploying the 2007 Office system](http://technet.microsoft.com/library/cc303395\(v=Office.12\).aspx).  

 **Possible Solution 2:** Verify that the MSP file does not have the **Suppress modal** check box selected. For more information about configuring this setting, see [Overview of 2007 Office System Deployment](http://technet.microsoft.com/library/bb490141.aspx).  

### AutoLogon  
 Review the problems and solutions for automatic logon issues:  

-   Interruption of the LTI and Zero Touch Installation \(ZTI\) deployment processes because of logon security banners as described in [Logon Security Banners](#LogonSecutiryBanners)  

-   Interruption of the LTI and ZTI deployment processes because of prompts for user credentials as described in [Prompted for User Credentials](#PromtedforUserCredentials)  

####  <a name="LogonSecutiryBanners"></a> Logon Security Banners  
 **Problem:** MDT task sequences are processed during an interactive user session, which requires that the target computer be allowed to log on automatically using a specified administrative account. If a Group Policy object \(GPO\) is in place that enforces a logon security banner, this automatic logon will not be allowed to proceed, because the security banner halts the logon process while it waits for a user to accept the stated policy.  

 **Possible Solution:** Be sure that the GPO is applied to specific organizational units \(OUs\) and not included in the default domain GPO. When you add computers to the domain, specify that they be added to an OU that is not affected by a GPO that enforces a logon security banner. In the Task Sequence Editor, include as one of the last task sequence steps a script that relocates the computer account to the desired OU.  

> [!NOTE]
>  If you are reusing existing Active Directory® Domain Services \(AD DS\) accounts, ensure that prior to deploying to the target computer you have relocated the target computer’s account to an OU that is not affected by the GPO that enforces the security logon banner.  

####  <a name="PromtedforUserCredentials"></a> Prompted for User Credentials  
 **Problem:** You created an image of a computer that was joined to the domain. While deploying the new image to a target computer, the deployment process halts, because auto\-logon does not occur and the user is prompted to enter appropriate credentials. The deployment process resumes when the credentials are provided and the user is logged on.  

 **Possible Solution:** When capturing images, the source computer should not be joined to a domain. If the computer was joined to a domain, join the computer to a workgroup, re\-capture the image, and attempt the deployment to a target computer to determine whether the issue is resolved.  

### BIOS  
 **Problem:** While deploying to a target computer that is equipped with Intel vPro technology, the deployment may end with a stop error. Even though all updated drivers have been included as out\-of\-box drivers in the Deployment Workbench, the target computer does not start.  

 Possible Solution: Review the settings in the target computer’s basic input\/output system \(BIOS\) to determine whether the default Serial Advanced Technology Attachment mode is configured as Advanced Host Controller Interface \(AHCI\). Unfortunately, certain Windows operating systems do not support AHCI by default.  

### Database Problems  
 Review database\-related problems and solutions:  

-   Errors generated as a result of improperly configured firewalls on database server as described in [Blocked SQL Server Browser Requests](#BlockedSQLServerBrowserRequests)  

-   Errors generated as a result of broken connections with the database server as described in [Named Pipe Connections](#NamedPipeConnections)  

####  <a name="BlockedSQLServerBrowserRequests"></a> Blocked SQL Server Browser Requests  
 **Problem:** During the MDT deployment process, information can be retrieved from Microsoft SQL Server® databases. However, errors might be generated that relate to an improperly configured firewall on the database server.  

 **Possible Solution:** The Windows Firewall in Windows Server helps prevent unauthorized access to computer resources. However, if the firewall is configured incorrectly, attempts to connect to a SQL Server instance may be blocked. To access an instance of SQL Server that is behind the firewall, configure the firewall on the computer that is running SQL Server. For more information on configuring firewall ports for SQL Server, see the Microsoft Support article [How do I open the firewall port for SQL Server on Windows Server 2008?](http://support.microsoft.com/kb/968872)  

####  <a name="NamedPipeConnections"></a> Named Pipe Connections  
 **Problem:** During the MDT deployment process, information can be retrieved from SQL Server databases. However, errors might be generated that relate to broken SQL Server connections. These can be caused by not enabling named pipe connections in Microsoft SQL Server.  

 **Possible Solution:** To resolve these problems, enable named pipes in SQL Server. Also, specify the **SQLShare** property, which it is required when making a connection to an external database using named pipes. When connecting using named pipes, use integrated security to make the connection to the database. In the case of LTI deployments, the user account that you specify makes the connection to the database. For ZTI deployments that use Configuration Manager, the network access account connects to the database. Because Windows PE has no security context by default, you must make a network connection to the database server to establish a security context for the user who will be making the connection.  

 The network share that the **SQLShare** property specifies provides a means to connect to the server to gain a proper security context. You must have Read access to the share. When the connection is made, you can then establish the named pipe connection to the database. The **SQLShare** property is not needed and should not be used when making a TCP\/IP connection to the database.  

 Enable named pipe connections by performing the following tasks based on the version of SQL Server you are using:  

-   Enable named pipe connections for SQL Server 2008 R2 as described in [Enable Named Pipe Connections in SQL Server 2008 R2](#EnableNamedPipeConnectionsinSQLServer).  

-   Enable named pipe connections for SQL Server 2005 as described in [Enable Named Pipe Connections in SQL Server 2005](#EnableNamedPipeConnectionsinSQL).  

#####  <a name="EnableNamedPipeConnectionsinSQLServer"></a> Enable Named Pipe Connections in SQL Server 2008 R2  
 To enable named pipe connections in SQL Server 2008 R2, perform the following steps:  

1.  On the computer running SQL Server 2008 R2 that hosts the database to be queried, click **Start**, and then point to **All Programs**. Point to **Microsoft SQL Server 2008 R2**, and then click **SQL Server Management Studio**.  

2.  In the **Microsoft SQL Server Management Studio** console, in the **Object Explorer,** right\-click ***sql\_server\_name***, and then click **Properties** \(where *sql\_server\_name* is the name of the computer running SQL Server to be configured\).  

3.  The Server Properties \- ***sql\_server\_name*** dialog box is displayed.  

4.  In the **Server Properties** \- ***sql\_server\_name*** dialog box, in **Select a page**, click **Connections**.  

5.  On the **Connections** page, ensure the **Allow remote connections to this server** check box is selected and then click **OK**.  

6.  Close the Microsoft SQL Server Management Studio console.  

7.  On the computer running SQL Server 2008 R2 that hosts the database to be queried, click **Start**, and then point to **All Programs**. Point to **Microsoft SQL Server 2008 R2**, point to **Configuration Tools**, and then click **SQL Server Configuration Manager**.  

8.  In the **Sql Server Configuration Manager** console, go to SQL Server Configuration Manager \(Local\) \/ SQL Server Network Configuration \/ Protocols for *sql\_instance* \(where *sql\_instance* in the name of the SQL Server instance to be configured\).  

9. In the details pane, right\-click **Named Pipes**, and then click **Enable**.  

     The Warning dialog box appears indicating that the changes will be saved but will not take effect until the service is stopped and restarted.  

10. In the **Warning** dialog box, click **OK**.  

11. In the **Sql Server Configuration Manager** console, go to SQL Server Configuration Manager \(Local\) \/ SQL Server Services.  

12. In the details pane, right\-click **SQL Server*\(sql\_instance\)***, and then click **Restart** \(where *sql\_instance* in the name of the SQL Server instance that you configured in step 2\).  

     The SQL Server Configuration Manager progress bar is displayed that shows the status of restarting the services. After the service restarts, the progress bar closes.  

13. Close the SQL Server Configuration Manager console.  

 For additional information, [How to enable remote connections in SQL Server 2008](http://blogs.msdn.com/b/walzenbach/archive/2010/04/14/how-to-enable-remote-connections-in-sql-server-2008.aspx).  

#####  <a name="EnableNamedPipeConnectionsinSQL"></a> Enable Named Pipe Connections in SQL Server 2005  
 To enable named pipe connections in SQL Server 2005, perform the following steps:  

1.  On the computer running SQL Server 2005 that hosts the database to be queried, click **Start**, and then point to **All Programs**. Point to **Microsoft SQL Server 2005**, point to **Configuration Tools**, and then click **SQL Server Surface Area Configuration**.  

2.  In the **SQL Server 2005 Surface Area Configuration** dialog box, click **Surface Area Configuration for Services and Connections**.  

3.  In the **Surface Area Configuration for Services and Connections – *server\_name*** dialog box \(where *server\_name* is the name of the computer running SQL Server 2005\), in **Select a component and then configure its services and connections**, go to MSSQLSERVER\\Database Engine, and then click **Remote Connections**.  

4.  Click **Local and remote connections**, click **Using both TCP\/IP and named pipes**, and then click **Apply**.  

5.  In the **Surface Area Configuration for Services and Connections – *server\_name*** dialog box \(where *server\_name* is the name of the computer running SQL Server 2005\), in **Select a component and then configure its services and connections**, go to MSSQLSERVER\\Database Engine, and then click **Service**.  

6.  Click **Stop**.  

     The MSSQLSERVER service stops.  

7.  Click **Start**.  

     The MSSQLSERVER service starts.  

8.  Click **OK**.  

9. Close SQL Server 2005 Surface Area Configuration.  

 For additional information, see the Microsoft Support article [How to configure SQL Server 2005 to allow remote connections](http://support.microsoft.com/kb/914277)  

### Deployment Scripts  
 Review MDT\-related problems and solutions:  

-   Prompted for user credentials and may receive error 0x80070035 as described in [Credentials_script](#Credentials_script)  

-   Error message “Wuredist.cab not found” appears as described in [ZTIWindowsUpdate](#ZTIWindowsUpdate)  

####  <a name="Credentials_script"></a> Credentials\_script  
 **Problem:** During the last start\-up of a newly deployed computer, the user is prompted to provide user credentials and may receive error 0x80070035, which indicates that the network path was not found.  

 **Possible Solution:** Be sure that the WIM file does not include a MININT or \_SMSTaskSequence folder. To delete these folders, first use the ImageX utility to mount the WIM file, and then delete the folders.  

> [!NOTE]
>  If an Access Denied error occurs when you attempt to delete the folders from the WIM file, open a Command Prompt window, switch to the root of the image contained in the WIM file, and then run **RD MININT** and **RD \_SMSTaskSequence**.  

####  <a name="ZTIWindowsUpdate"></a> ZTIWindowsUpdate  
 **Problem:** If you use the ZTIWindowsUpdate.wsf script to apply software updates during deployment, note that this script may communicate directly with the Microsoft Update website to download and install the required Windows Update Agent binaries, scan for applicable software updates, download the binaries for the applicable software updates, and then install the downloaded binaries. This process requires that your networking infrastructure be configured to allow the target computer to gain access to the Microsoft Update website.  

 If the deployment share does not contain the Windows Update Agent installation files and the target computer does not have appropriate Internet access, error “wuredist.cab not found” is reported in the ZTIWindowsUpdate.log and BDD.log files.  

 **Possible Solution:** Follow the steps outlined in the section, "ZTIWindowsUpdate.wsf", in the MDT document *Toolkit Reference*.  

### Deployment Shares  
 Review deployment share–related problems and solutions:  

-   Updating WIM files fails when updating a deployment share as described in [Failure to Update WIM Files](#FailuretoUpdateWIMFiles).  

####  <a name="FailuretoUpdateWIMFiles"></a> Failure to Update WIM Files  
 In a “simple” environment:  

-   MDT typically picks up WIMGAPI.DLL from C:\\Windows\\system32 \(always in the path\). The version of this WIMGAPI.DLL must match the version \(build\) of the operating system.  

-   On a 64\-bit operating system, MDT always uses the x64 WIMGAPI.DLL file; only that file should be in the system PATH. On a 32\-bit operating system, MDT always uses the x86 WIMGAPI.DLL file; only that file should be in the system PATH. \(Other products, such as Configuration Manager, use the 32\-bit version of WIMGAPI.DLL, even on a 64\-bit operating system, but they manage and install that version.\)  

 **Problem:** When attempting to update a deployment share, the user will be informed that the mounting of one or more .wim files did not succeed.  

 **Possible Solution:** Open a Command Prompt window and run **where WIMGAPI.DLL**. For the first entry in the list \(the first location found by searching the path\), ensure that the **Version** property matches the build of the Windows Assessment and Deployment Kit \(Windows ADK\) that is installed. Also ensure that the property matches the operating system build number.  

### The Windows Deployment Wizard  
 Review Windows Deployment Wizard–related problems and solutions:  

-   Windows Deployment Wizard pages are displayed even when LTI is configured to skip the wizard pages as described in [Wizard Pages Are Not Skipped](#WizardPagesareNotSkipped).  

####  <a name="WizardPagesareNotSkipped"></a> Wizard Pages Are Not Skipped  
 **Problem:** A wizard page is displayed even though the MDT DB or CustomSettings.ini file specify that the wizard should be skipped.  

 **Possible Solution:** To properly skip a wizard page, include all properties that would be specified on that wizard page where appropriate in the MDT DB or CustomSettings.ini file along with appropriate values. If a property is configured improperly for a skipped wizard page, that page will be shown. For more information about which properties are required to ensure that a wizard page is skipped, see the section, "Providing Properties for Skipped Deployment Wizard Pages", in the MDT document *Toolkit Reference*.  

### Disks and Partitioning  
 Review disk partitioning problems and solutions:  

-   BitLocker® Drive Encryption issues as described in [BitLocker Drive Encryption](#BitLockerDriveEncryption)  

-   Disk partitioning errors as described in Disk Partitioning Errors  

-   Failures during Refresh Computer deployment scenarios caused by logical or dynamic disks as described in [Support for Logical and Dynamic Disks](#SupportforLoogicalandDynamicDisks)  

####  <a name="BitLockerDriveEncryption"></a> BitLocker Drive Encryption  
 Deploying BitLocker requires a specific configuration for proper deployment. The following potential problems may be related to the configuration of the target computer:  

-   In ZTI and UDI deployments, the ZTIBde.wsf Script Fails with the Error “Unable to open registry key ‘HKEY\_CURRENT\_USER\\Control Panel\\International\\LocaleName’ for reading”, as described in [ZTIBde.wsf Script Fails with the Error “Unable to open registry key ‘HKEY_CURRENT_USER\Control Panel\International\LocaleName’ for reading”](#ZTIBde.wsf).  

-   USB devices, CD drives, DVD drives, or other removable media devices on the target computer that appear as multiple drive letters, as described in [Devices Appear as Multiple Drive Letters](#DevicesAppearasMultipleDriveLetters)  

-   Shrinking drive C on the target computer to provide sufficient unallocated disk space as described in [Problems with Shrinking Disks](#ProblemswithShrinkingDisks)  

#####  <a name="ZTIBde.wsf"></a> ZTIBde.wsf Script Fails with the Error “Unable to open registry key ‘HKEY\_CURRENT\_USER\\Control Panel\\International\\LocaleName’ for reading”  
 **Problem:** While trying to deploy BitLocker on the target computer in ZTI or UDI, the ZTIBde.wsf script fails with the error “Unable to open registry key ‘HKEY\_CURRENT\_USER\\Control Panel\\International\\LocaleName’ for reading.”  

 **Possible Solution:** Specify the locale in the **UILanguage** property. In ZTI and UDI, the ZTIBde.wsf script runs in the system control, so a full user profile is not loaded. When the ZTIBde.wsf script tries to read the locale information it is not in the registry, because the registry \(user profile\) is not fully loaded. As a workaround, specify the locale in the **UILanguage** property.  

#####  <a name="DevicesAppearasMultipleDriveLetters"></a> Devices Appear as Multiple Drive Letters  
 **Problem:** Some devices can appear as multiple logical drive letters, depending on how they are partitioned. In some cases, they can emulate a 1.44\-megabyte \(MB\) floppy disk drive and a memory storage drive. Therefore, Windows may assign the same device drive letters A and B for floppy disk emulation and F for the memory storage drive. By default, MDT scripts use the lowest drive letter \(in this example, A\).  

 **Possible Solution:** Override the default setting on the **Specify the BitLocker recovery details** page in the Windows Deployment Wizard. The Windows Deployment Wizard summary page displays a warning to inform the user which drive letter was selected to store BitLocker recovery information. In addition, the BDD.log and ZTIBDE.log files record the removable media devices detected and which device was selected to store the BitLocker recovery information.  

#####  <a name="ProblemswithShrinkingDisks"></a> Problems with Shrinking Disks  
 **Problem:** Not enough unallocated disk space exists on the target computer to enable BitLocker. To deploy BitLocker on a target computer, at least 2 gigabytes \(GB\) of unallocated disk space is required to create the system volume. The *system volume* is the volume that contains the hardware\-specific files needed to load Windows after the BIOS has booted the computer.  

 **Possible Solution 1:** On existing computers, use the Diskpart tool to shrink drive C so that the system volume can be created. In some instances, though, the Diskpart tool may not be able to shrink drive C sufficiently to provide 2 GB of unallocated disk space, possibly because of fragmented disk space within drive C.  

 One possible solution to this problem is to defragment drive C. To do so, perform the following steps:  

1.  Run the Diskpart **shrink querymax** command to identify the maximum amount of disk space that can be unallocated.  

2.  If the value returned in step 1 is less than 2 GB, clean drive C of any unnecessary files, and then defragment it.  

3.  Run the Diskpart **shrink querymax** command again to verify that more than 2 GB of disk space can be unallocated.  

4.  If the value returned in step 3 is still less than 2 GB, perform one of the following tasks:  

    -   Defragment drive C multiple times to ensure that it is fully optimized.  

    -   Back up the data on drive C, delete the existing partition, create a new partition, and then restore the data to the new partition.  

 **Possible Solution 2:** The ZTIBDE.wsf script runs the Disk Preparation Tool \(bdehdcfg.exe\) and configures the system volume partition size to 2 GB by default. You can customize the ZTIBDE.wsf script to change the default, if necessary. However, modifying the MDT scripts is not recommended.  

####  <a name="SupportforLoogicalandDynamicDisks"></a> Support for Logical and Dynamic Disks  
 **Problem:** When performing a Refresh Computer deployment scenario, the deployment process may fail when deploying to a target computer that is using logical drives or dynamic disks.  

 **Possible Solution:** MDT does not support deploying operating systems to logical drives or dynamic disks.  

### Domain Join  
 **Problem:** During deployment, you use the Windows Deployment Wizard to provide all the necessary information for the target computer, including credentials, domain join information, and static IP configuration. When Setup finishes, you can see that the system has not joined the domain and is still in a workgroup.  

 **Possible Solution:** An LTI deployment of MDT configures the static IP information after the operating system is up and running. If the target computer is located on a network segment that does not have Dynamic Host Configuration Protocol \(DHCP\), an automated domain join specified in Unattend.xml will fail when no DHCP is present.  

 Configure Unattend.xml to join a workgroup. Then, use the built\-in **Recover from Domain** task sequence step to add a step in the task sequence to join the domain after the static IP has been applied.  

### Driver Installation  
 To ensure the best possible user experience, installation of hardware devices and software drivers should run as seamlessly as possible, with little or no user intervention. Microsoft provides tools and guidelines to help create installation packages that meet this goal. For general information about driver installation, see [Device and Driver Installation](http://www.microsoft.com/whdc/driver/install/default.mspx).  

 Review device driver installation–related problems and solutions:  

-   Problems that occur when using $OEM$ mass storage drivers with MDT as described in Combine $OEM$ Mass Storage Drivers with MDT Mass Storage Logic  

-   Troubleshooting device driver installation issues using the SetupAPI.log as described in [Troubleshoot Device Installation with SetupAPI.log](#TroubleshootDeviceInstallationwithSetupAPI.log)  

####  <a name="TroubleshootDeviceInstallationwithSetupAPI.log"></a> Troubleshoot Device Installation with SetupAPI.log  
 The white paper [Troubleshooting Device Installation with the SetupAPI Log File](http://msdn.microsoft.com/windows/hardware/gg463393.aspx) provides information about debugging Windows device installation. Specifically, the paper provides guidelines for driver developers and testers to interpret the SetupAPI log file.  

 One of the most useful log files for debugging purposes is the SetupAPI.log file. This plain\-text file maintains the information that SetupAPI records about device installation, service pack installation, and update installation. Specifically, the file maintains a record of device and driver changes as well as major system changes beginning from the most recent Windows installation. This paper focuses on using the SetupAPI log file to troubleshoot device installation; it does not describe the log file sections that are associated with service pack and update installations.  

### New Computer Deployments  
 Review the problems and solutions for New Computer deployment scenarios:  

-   Problems starting the deployment process using Pre\-Boot Execution Environment \(PXE\) boot as described in [PXE Boot](#PXEBoot)  

####  <a name="PXEBoot"></a> PXE Boot  
 In brief, the PXE protocol operates as follows: The client computer initiates the protocol by broadcasting a DHCP Discover packet containing an extension that identifies the request as coming from a client computer that implements the PXE protocol. Assuming that a boot server implementing this extended protocol is available, the boot server sends an offer containing the IP address of the server that will service the client. The client uses Trivial File Transfer Protocol to download the executable file from the boot server. Finally, the client computer runs the downloaded bootstrap program.  

 The initial phase of this protocol piggybacks on a subset of the DHCP messages to enable the client to discover a boot server \(that is, a server that delivers executable files for new computer setup\). The client computer may use the opportunity to obtain an IP address \(which is the expected behavior\) but is not required to do so.  

 The second phase of this protocol takes place between the client computer and a boot server and uses the DHCP message format as a convenient format for communication. This second phase is otherwise unrelated to the standard DHCP services. The next few pages outline the step\-by\-step process during PXE client computer initialization.  

 For more information on troubleshooting PXE boot\-related issues in Windows Deployment Services running in Legacy or Mixed mode, see the Microsoft Support article [Description of PXE Interaction Among PXE Client, DHCP, and RIS Server](http://support.microsoft.com/kb/244036).  

 Review the following solutions for PXE boot issues:  

-   Disable Windows PE logging to SetupAPI.log as described in [Disable Windows PE Logging in Windows Deployment Services](#DisableWindowsPELogginginWindowsDeploymentServices).  

-   Ensure that DHCP is configured properly as described in [Ensure the Proper DHCP Configuration](#EnsuretheProperDHCPConfiguration).  

-   Improve the response times for assigning IP addresses to PXE client computers as described in [Improve PXE IP Address Assignment Response Time](#ImprovePXEIPAddressAssignmentResponseTime).  

#####  <a name="DisableWindowsPELogginginWindowsDeploymentServices"></a> Disable Windows PE Logging in Windows Deployment Services  
 The first procedure recommended is to make sure that logging to setupapi.log has been disabled.  

#####  <a name="EnsuretheProperDHCPConfiguration"></a> Ensure the Proper DHCP Configuration  
 Depending on the router models in use, the specific router configuration of DHCP broadcast forwarding may be supported to either a subnet \(or router interface\) or a specific host. If the DHCP servers and the computer running Windows Deployment Services are separate computers, ensure that the routers that forward DHCP broadcasts are designed so that both the DHCP and Windows Deployment Services servers receive the client broadcasts; otherwise, the client computer does not receive a reply to its remote boot request.  

 Is there a router between the client computer and the remote installation server that is not allowing the DHCP\-based requests or responses through? When the Windows Deployment Services client computer and the Windows Deployment Services server are on separate subnets, configure the router between the two systems to forward DHCP packets to the Windows Deployment Services server. This arrangement is necessary, because Windows Deployment Services client computers discover a Windows Deployment Services server by using a DHCP broadcast message. Without DHCP forwarding set up on a router, the client computers’ DHCP broadcasts do not reach the Windows Deployment Services server. This DHCP forwarding process is sometimes referred to as *DHCP Proxy* or *IP Helper Address* in router configuration manuals. Refer to the router instructions for more information about setting up DHCP forwarding on a specific router.  

#####  <a name="ImprovePXEIPAddressAssignmentResponseTime"></a> Improve PXE IP Address Assignment Response Time  
 Check the following elements if it is taking a long time \(15–20 seconds\) for the PXE client computer to retrieve an IP address:  

-   Are the network adapter on the target computer and the switch or router set to the same speed \(automatic, duplex, full, and so on\)  

-   Is the IP address for the Windows Deployment Services server in the IP Helper file on the router through which the connection is made? If the list of IP addresses in the IP Helper file is long, can you move the address for the Windows Deployment Services server near the top  

### Restarting the Deployment Process  
 **Problem:** While testing and troubleshooting a new or modified task sequence, you may need to restart the target computer so that the deployment process can start over from the beginning. Unexpected results may occur, because MDT keeps track of its progress by writing data to the hard disk; any restart of the target computer has MDT resume where it left off at the previous restart.  

 **Possible Solution:** To allow the deployment process to restart from the beginning, delete the C:\\MININT and C:\\\_SMSTaskSequence folders prior to restarting the target computer.  

### Sysprep  
 Review Sysprep\-related problems and solutions:  

-   The target computer is not appearing in the correct AD DS OU as described in [The Computer Account Is in the Wrong OU](#ComputerAccountisintheWrongOU).  

####  <a name="ComputerAccountisintheWrongOU"></a> The Computer Account Is in the Wrong OU  
 **Problem:** The target computer is properly joined to the domain, but the computer account is in the wrong OU.  

 **Possible Solution 1:** If an account pre\-exists for the target computer, the account will remain in its original OU. To move the account to the specified OU, add a task sequence step that uses an automation tool, such as a Microsoft Visual Basic® Scripting Edition, to move the account.  

 **Possible Solution 2:** Verify that the specified OU is in the correct format and that it exists. The correct OU format should be `OU=Reception,OU=NYC,DC=Woodgrovebank,DC=com`.  

### Configuration Manager  
 **Problem:** The error message shown in  REF \_Ref308174600 \\h Figure 3 is displayed when you attempt to create a Configuration Manager PXE service point using the **Create self\-signed PXE certificate** option.  

 ![TroubleshootingReference3](../Image/TroubleshootingReference3.jpg "TroubleshootingReference3")  
Figure  SEQ Figure \\\* ARABIC 3. PXE service point error  

 **Figure  SEQ Figure \\\* ARABIC 3. PXE service point error**  

 **Possible Solution:** If a PXE service point previously existed on the server you are configuring, the PXE service point may not have deleted the self\-created certificates when you uninstalled it. Delete the PXE certificate folder from C:\\Documents and Settings\\*user\_name*\\Application Data\\Microsoft\\Crypto\\RSA, where *user\_name* is the name of the user performing the current configuration or who performed the previous configuration. The New Site Role Wizard in the Configuration Manager console should successfully finish when you have deleted the folder.  

### Task Sequences  
 Review task sequence–related problems and solutions:  

-   Task sequence does not finish successfully or has unpredictable behavior as described in [The Task Sequence Does Not Finish Successfully](#TaskSequenceDoesNotFinishSuccessfully).  

-   Original equipment manufacturer \(OEM\) task sequences in LTI are listed on boot images with the opposite processor architecture as described in [The OEM Task Sequence Incorrectly Appears for a Boot Image Created for a Different Processor Architecture](#OEMTaskSequenceIncorrectlyAppearsforBootImage).  

-   The Windows Deployment Wizard displays the error message “Bad Task Sequence Item \(Invalid OS GUID\)” as described in [Bad Task Sequence Item (Invalid OS GUID) Message in the Windows Deployment Wizard](#BadTaskSequenceItem).  

-   While configuring a network connection name, the message “Please enter a valid name for the network adapter” is displayed as described in [Apply Network Settings](#ApplyNetworkSettings).  

-   Problems that may occur as a result of improper configuration of continue on error configuration settings for task sequence steps as described in [Use Continue on Error](#UseContinueonError).  

####  <a name="TaskSequenceDoesNotFinishSuccessfully"></a> The Task Sequence Does Not Finish Successfully  
 **Problem:** Task sequence may not finish successfully or has unpredictable behavior.  

 **Possible Solution:** The **Install Operating System** task sequence step \(for LTI\) or the **Apply Operating System Image** task sequence step \(for UDI and ZTI\) may have been modified after the creation of the task sequence step can lead to unpredictable results. For example, if a task sequence was created to deploy a 32\-bit Windows 8.1 image, and then later the **Install Operating System** task sequence step or the **Apply Operating System Image** task sequence step was changed to reference a 64\-bit Windows 8.1 image, the task sequence may not run successfully.  

 It is recommended that a new task sequence is created to deploy a different operating system image.  

####  <a name="OEMTaskSequenceIncorrectlyAppearsforBootImage"></a> The OEM Task Sequence Incorrectly Appears for a Boot Image Created for a Different Processor Architecture  
 **Problem:** A task sequence based on a LTI OEM task sequence template is showing up for a boot image with a different processor architecture. For example, an OEM task sequence that deploys a 64\-bit operation system is showing on a 32\-bit boot image.  

 **Possible Solution:** This is expected behavior as OEM task sequences in LTI are not considered to be “platform\-specific” will always be listed, regardless of the processor architecture of the boot image.  

####  <a name="BadTaskSequenceItem"></a> Bad Task Sequence Item \(Invalid OS GUID\) Message in the Windows Deployment Wizard  
 **Problem:** When running the Windows Deployment Wizard, the wizard displays the error message “Bad Task Sequence Item \(Invalid OS GUID\).” The operating system is listed in the OperatingSystem.xml file; however, the operating system is not displayed in the Deployment Workbench.  

 **Possible Solution:** The original operating system source has two or more WIM files associated. A SKU that is associated with a task sequence is deleted; however, other SKUs for the operating system source still exist. When the task sequence that references the deleted SKU is selected on the **Select a task sequence to execute on this computer** wizard page in the Windows Deployment Wizard, the error message “Bad Task Sequence Item \(Invalid OS GUID\)" is displayed after you click **Next** on the wizard page.  

 To resolve this problem, perform one of the following tasks:  

-   Remove all SKUs from the operating system source. The Windows Deployment Wizard behaves normally, and the error message is not displayed.  

-   Change the task sequence to use a different operating system image.  

####  <a name="ApplyNetworkSettings"></a> Apply Network Settings  
 **Problem:** When configuring the network connection name in the Deployment Workbench, a validation error prompts you with the message, “Please enter a valid name for the network adapter.”  

 **Possible Solution:** Remove any spaces and invalid characters from the specified connection name.  

####  <a name="UseContinueonError"></a> Use Continue on Error  
 If a MDT task sequence is configured not to continue on error and that task sequence returns an error, all remaining task sequences in that task sequence group are skipped. However, the remaining task sequence groups are processed. Consider the following:  

 Two task sequence groups have been created, and either group contains more than one task sequence step:  

-   Group A  

    -   Step A  

    -   Step B  

-   Group B  

    -   Step A  

    -   Step B  

 If Group A\\Step A is configured not to continue on error, then Group A\\Step B will not be processed. However, all task sequence steps in Group B will be processed.  

### The User State Migration Tool  
 Review USMT\-related problems and solutions:  

-   Shortcuts that point to documents stored in network shared folders may not be restored properly as described in [Missing Desktop Shortcuts](#MissingDesktopShortcuts).  

####  <a name="MissingDesktopShortcuts"></a> Missing Desktop Shortcuts  
 **Problem:** While using USMT to migrate user data, shortcuts that point to network documents may not be restored. The shortcuts are captured during Scanstate; however, they are never restored to the target computer during Loadstate.  

 **Possible Solution:** Edit the MigUser.xml file and comment out the following line:  

 Original:  

```  
<include> filter='MigXmlHelper.IgnoreIrrelevantLinks()'>  
```  

 Modified:  

```  
<include> <!-- filter='MigXmlHelper.IgnoreIrrelevantLinks()'> -->  
```  

### Windows Imaging Format Files  
 Review WIM\-related problems and solutions:  

-   LTI and ZTI deployments fail with WIM file errors in the BDD.log file as described in [Corrupt WIM File](#CorruptWIMFile).  

####  <a name="CorruptWIMFile"></a> Corrupt WIM File  
 **Problem:** When deploying an image, the deployment fails with the following entries in the BDD.log file:  

-   ```  
    The image \\Server\Deployment$\Operating Systems\Windows\version1.wim was not applied successfully by ImageX, rc = 2  
    ```  

-   ```  
    LTIApply COMPLETED.  Return Value = 2  
    ```  

-   ```  
    ZTI ERROR - Non-zero return code by LTIApply, rc = 2  
    ```  

 Investigate the issue by mounting the WIM file using ImageX results in the error, “The data is invalid.” Further investigation shows that the date stamp of the .wim file is many years before the current date. It is possible that another process, such as a virus scanner, was holding the .wim file open after it was previously closed at the conclusion of a Read or Write process.  

 **Possible Solution:** Restore the .wim file from backup media.  

### Windows PE  
 Review Windows PE–related problems and solutions:  

-   The LTI or ZTI deployment process is not initiated because of insufficient RAM or wireless network adapters as described in [Deployment Process Not Initiated—Limited RAM or Wireless Network Adapter](#LimitedRamorWirelessNetworkAdapter).  

-   The LTI or ZTI deployment process is not initiated because of missing Windows PE components as described in [Deployment Process Not Initiated—Missing Components](#MissingComponents).  

-   The LTI or ZTI deployment process is not initiated because of missing or incorrect device drivers as described in [Deployment Process Not Initiated—Missing or Incorrect Drivers](#MissingorIncorrectDrivers).  

####  <a name="LimitedRamorWirelessNetworkAdapter"></a> Deployment Process Not Initiated—Limited RAM or Wireless Network Adapter  
 **Problem:** When deploying an image to certain target computers, Windows PE starts, runs **wpeinit**, opens a Command Prompt window but does not actually start the deployment process. Troubleshooting the problem by mapping a network drive from the target computer indicates that the network adapter drivers are not loaded.  

 **Possible Solution 1:**The Deployment Wizard is not starting, because there is insufficient RAM. Verify that the target computer has at least 512 MB of RAM and that no shared video memory consumes more than 64 MB of the 512 MB.  

 The versions of Windows PE that MDT supports are unable to run on a target computer that has less than 512 MB of RAM.  

 **Possible Solution 2:** Do not include the wireless drivers in the Windows PE image.  

####  <a name="MissingComponents"></a> Deployment Process Not Initiated—Missing Components  
 **Problem:** When troubleshooting a failed deployment, a review of the BDD.log file lists the following entry:  

```  
ERROR - Unable to create ADODB.Connection object, impossible to query SQL Server: ActiveX component can't create object (429).  
```  

 **Possible Solution:** This error may indicate that the Windows PE image was not created using MDT. If you are using Configuration Manager, do not use one of the existing Windows PE images that Configuration Manager created; instead, create an image using the Import Microsoft Deployment Task Sequence Wizard.  

> [!NOTE]
>  The Windows PE images that Configuration Manager creates contain components that support scripting, XML, and Windows Management Instrumentation (WMI), but they do not contain components that support Microsoft ActiveX® Data Objects (ADO).  

####  <a name="MissingorIncorrectDrivers"></a> Deployment Process Not Initiated—Missing or Incorrect Drivers  
 **Problem:** When deploying to certain target computers, Windows PE starts, runs **wpeinit**, opens a Command Prompt window, but does not actually start the deployment process. Troubleshooting by mapping a network drive from the target computer indicates that the network adapter drivers are not loaded. A review of the SetupAPI.log file located in *X*:\Windows\System32\Inf indicates that Windows PE generates errors when it is configuring the network adapter, one of which is, “This driver is not meant for this platform.” The drivers in the **Out-of-Box Drivers** list have been injected into the image.  

 **Possible Solution:** It is possible that Windows PE is having a driver conflict with another driver. When configuring the settings for the Windows PE image in the Deployment Workbench, create a Windows PE drivers group that contains only network adapter and storage drivers, and then configure the deployment share to use only the Windows PE driver group.  

## Deployment Process Flow Charts  
 This section provides two sets of MDT flow charts: one for LTI deployments and one for ZTI deployments with Configuration Manager. Each flow chart illustrates the tasks run during that deployment type.  

 Familiarize yourself with the deployment process flow charts by:  

-   Reviewing the LTI deployment process flowcharts as described in [LTI Deployment Process Flowcharts](#LTIDeploymentProcessFlowcharts)  

-   Reviewing the ZTI deployment process flowcharts as described in [ZTI Deployment Process Flowcharts](#ZTIDevelopmentProcessFlowcharts)  

###  <a name="LTIDeploymentProcessFlowcharts"></a> LTI Deployment Process Flowcharts  
 Flow charts are provided for the following phases:  

-   Validation ( REF _Ref308175154 \h Figure 4)  

-   State Capture ( REF _Ref308175160 \h Figure 5 and  REF _Ref308175167 \h Figure 6)  

-   Preinstall ( REF _Ref308175174 \h Figure 7,  REF _Ref308175180 \h Figure 8, and  REF _Ref308175186 \h Figure 9)  

-   Install ( REF _Ref308175193 \h Figure 10)  

-   Postinstall ( REF _Ref308175199 \h Figure 11 and  REF _Ref308175204 \h Figure 12)  

-   State Restore ( REF _Ref308175212 \h Figure 13,  REF _Ref308175218 \h Figure 14,  REF _Ref308175225 \h Figure 15, and  REF _Ref308175233 \h Figure 16)  

 ![TroubleshootingReference4](../Image/TroubleshootingReference4.jpg "TroubleshootingReference4")  
Figure  SEQ Figure \\* ARABIC 4. Flow chart for the Validation Phase  

 **Figure  SEQ Figure \\\* ARABIC 4. Flow chart for the Validation Phase**  

 ![TroubleshootingReference5](../Image/TroubleshootingReference5.jpg "TroubleshootingReference5")  
Figure  SEQ Figure \\* ARABIC 5. Flow chart for the State Capture Phase (1 of 2)  

 **Figure  SEQ Figure \\\* ARABIC 5. Flow chart for the State Capture Phase (1 of 2)**  

 ![TroubleshootingReference6](../Image/TroubleshootingReference6.jpg "TroubleshootingReference6")  
Figure  SEQ Figure \\* ARABIC 6. Flow chart for the State Capture Phase (2 of 2)  

 **Figure  SEQ Figure \\\* ARABIC 6. Flow chart for the State Capture Phase (2 of 2)**  

 ![TroubleshootingReference7](../Image/TroubleshootingReference7.jpg "TroubleshootingReference7")  
Figure  SEQ Figure \\* ARABIC 7. Flow chart for the Preinstall Phase (1 of 3)  

 **Figure  SEQ Figure \\\* ARABIC 7. Flow chart for the Preinstall Phase (1 of 3)**  

 ![TroubleshootingReference8](../Image/TroubleshootingReference8.jpg "TroubleshootingReference8")  
Figure  SEQ Figure \\* ARABIC 8. Flow chart for the Preinstall Phase (2 of 3)  

 **Figure  SEQ Figure \\\* ARABIC 8. Flow chart for the Preinstall Phase (2 of 3)**  

 ![TroubleshootingReference9](../Image/TroubleshootingReference9.jpg "TroubleshootingReference9")  
Figure  SEQ Figure \\* ARABIC 9. Flow chart for the Preinstall Phase (3 of 3)  

 **Figure  SEQ Figure \\\* ARABIC 9. Flow chart for the Preinstall Phase (3 of 3)**  

 ![TroubleshootingReference10](../Image/TroubleshootingReference10.jpg "TroubleshootingReference10")  
Figure  SEQ Figure \\* ARABIC 10. Flow chart for the Install Phase  

 **Figure  SEQ Figure \\\* ARABIC 10. Flow chart for the Install Phase**  

 ![TroubleshootingReference11](../Image/TroubleshootingReference11.jpg "TroubleshootingReference11")  
Figure  SEQ Figure \\* ARABIC 11. Flow chart for the Postinstall Phase (1 of 2)  

 **Figure  SEQ Figure \\\* ARABIC 11. Flow chart for the Postinstall Phase (1 of 2)**  

 ![TroubleshootingReference12](../Image/TroubleshootingReference12.jpg "TroubleshootingReference12")  
Figure  SEQ Figure \\* ARABIC 12 Flow chart for the Postinstall Phase (2 of 2)  

 **Figure  SEQ Figure \\\* ARABIC 12 Flow chart for the Postinstall Phase (2 of 2)**  

 ![TroubleshootingReference13](../Image/TroubleshootingReference13.jpg "TroubleshootingReference13")  
Figure  SEQ Figure \\* ARABIC 13. Flow chart for the State Restore Phase (1 of 4)  

 **Figure  SEQ Figure \\\* ARABIC 13. Flow chart for the State Restore Phase (1 of 4)**  

 ![TroubleshootingReference14](../Image/TroubleshootingReference14.jpg "TroubleshootingReference14")  
Figure  SEQ Figure \\* ARABIC 14. Flow chart for the State Restore Phase (2 of 4)  

 **Figure  SEQ Figure \\\* ARABIC 14. Flow chart for the State Restore Phase (2 of 4)**  

 ![TroubleshootingReference15](../Image/TroubleshootingReference15.jpg "TroubleshootingReference15")  
Figure  SEQ Figure \\* ARABIC 15. Flow chart for the State Restore Phase (3 of 4)  

 **Figure  SEQ Figure \\\* ARABIC 15. Flow chart for the State Restore Phase (3 of 4)**  

 ![TroubleshootingReference16](../Image/TroubleshootingReference16.jpg "TroubleshootingReference16")  
Figure  SEQ Figure \\* ARABIC 16. Flow chart for the State Restore Phase (4 of 4)  

 **Figure  SEQ Figure \\\* ARABIC 16. Flow chart for the State Restore Phase (4 of 4)**  

###  <a name="ZTIDevelopmentProcessFlowcharts"></a> ZTI Deployment Process Flowcharts  
 Flow charts are provided for the following phases of ZTI deployment with Configuration Manager:  

-   Initialization ( REF _Ref308175339 \h Figure 17)  

-   Validation ( REF _Ref308175345 \h Figure 18)  

-   State Capture ( REF _Ref308175351 \h Figure 19)  

-   Preinstall ( REF _Ref308175357 \h Figure 20)  

-   Install ( REF _Ref308175363 \h Figure 21)  

-   Postinstall ( REF _Ref308175382 \h Figure 22)  

-   State Restore ( REF _Ref308175388 \h Figure 23 and  REF _Ref308175394 \h Figure 24)  

-   Capture ( REF _Ref308175401 \h Figure 25)  

 ![TroubleshootingReference17](../Image/TroubleshootingReference17.jpg "TroubleshootingReference17")  
Figure  SEQ Figure \\* ARABIC 17. Flow chart for the Initialization Phase  

 **Figure  SEQ Figure \\\* ARABIC 17. Flow chart for the Initialization Phase**  

 ![TroubleshootingReference18](../Image/TroubleshootingReference18.jpg "TroubleshootingReference18")  
Figure  SEQ Figure \\* ARABIC 18. Flow chart for the Validation Phase  

 **Figure  SEQ Figure \\\* ARABIC 18. Flow chart for the Validation Phase**  

 ![TroubleshootingReference19](../Image/TroubleshootingReference19.jpg "TroubleshootingReference19")  
Figure  SEQ Figure \\* ARABIC 19. Flow chart for the State Capture Phase  

 **Figure  SEQ Figure \\\* ARABIC 19. Flow chart for the State Capture Phase**  

 ![TroubleshootingReference20](../Image/TroubleshootingReference20.jpg "TroubleshootingReference20")  
Figure  SEQ Figure \\* ARABIC 20. Flow chart for the Preinstall Phase  

 **Figure  SEQ Figure \\\* ARABIC 20. Flow chart for the Preinstall Phase**  

 ![TroubleshootingReference21](../Image/TroubleshootingReference21.jpg "TroubleshootingReference21")  
Figure  SEQ Figure \\* ARABIC 21. Flow chart for the Install Phase  

 **Figure  SEQ Figure \\\* ARABIC 21. Flow chart for the Install Phase**  

 ![TroubleshootingReference22](../Image/TroubleshootingReference22.jpg "TroubleshootingReference22")  
Figure  SEQ Figure \\* ARABIC 22. Flow chart for the Postinstall Phase  

 **Figure  SEQ Figure \\\* ARABIC 22. Flow chart for the Postinstall Phase**  

 ![TroubleshootingReference23](../Image/TroubleshootingReference23.jpg "TroubleshootingReference23")  
Figure  SEQ Figure \\* ARABIC 23. Flow chart for the State Restore Phase (1 of 2)  

 **Figure  SEQ Figure \\\* ARABIC 23. Flow chart for the State Restore Phase (1 of 2)**  

 ![TroubleshootingReference24](../Image/TroubleshootingReference24.jpg "TroubleshootingReference24")  
Figure  SEQ Figure \\* ARABIC 24. Flow chart for the State Restore Phase (2 of 2)  

 **Figure  SEQ Figure \\\* ARABIC 24. Flow chart for the State Restore Phase (2 of 2)**  

 ![TroubleshootingReference25](../Image/TroubleshootingReference25.jpg "TroubleshootingReference25")  
Figure  SEQ Figure \\* ARABIC 25. Flow chart for the Capture Phase  

 **Figure  SEQ Figure \\\* ARABIC 25. Flow chart for the Capture Phase**  

## Finding Additional Help  
 Find additional help in resolving MDT deployment problems by:  

-   Contacting Microsoft Support as described in [Microsoft Support](#MicrosoftSupport)  

-   Obtaining additional support through blogs and other Internet resources as described in [Internet Support](#InternetSupport)  

###  <a name="MicrosoftSupport"></a> Microsoft Support  
 Microsoft provides Premier and Professional level support for Microsoft Deployment Toolkit.  

 Professional level support: [http://support.microsoft.com/](http://support.microsoft.com/)  

 Premier level support: [https://premier.microsoft.com/](https://premier.microsoft.com/)  

> [!NOTE]
>  When contacting support, be clear that the issue is with MDT and the specific version.  

###  <a name="InternetSupport"></a> Internet Support  
 Many online sources provide additional troubleshooting assistance for MDT beyond what is covered in this reference. These online sources include:  

-   Microsoft-hosted blogs  

    -   [MDT Team blog](http://blogs.technet.com/b/msdeployment/)  

    -   [Configuration Manager Team blog](http://blogs.technet.com/b/configmgrteam/)  

    -   [Michael Niehaus’ blog](http://blogs.technet.com/b/mniehaus/) (Michael Niehaus writes on Windows and Microsoft Office deployment.)  

-   Microsoft-hosted newsgroups and forums:  

     The following newsgroups and forums are available with support from Microsoft employees, industry peers, and Microsoft Valued Professionals:  

    -   [Configuration Manager - Operating System Deployment](http://social.technet.microsoft.com/Forums/home?forum=configmanagerosd)  

    -   [Windows 8 Installation, Setup, and Deployment](http://social.technet.microsoft.com/Forums/windows/home?forum=w8itproinstall)  

-   Deployment-related information sources from outside Microsoft:  

    -   [DeployVista.com](http://www.deployvista.com/)  

    -   [myITforum.com](http://www.myitforum.com/)
