---
title: Toolkit reference - Microsoft Deployment Toolkit (MDT) Scripts
titleSuffix: Microsoft Deployment Toolkit
description: Reference details for Microsoft Deployment Toolkit (MDT) Scripts
ms.date: 09/09/2016
ms.subservice: mdt
ms.service: configuration-manager
ms.topic: reference
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: frankroj,mstewart,aaroncz
---

# Scripts

The scripts used in LTI and ZTI deployments reference properties that determine the process steps and configuration settings used during the deployment process. Use this reference section to help it determine the correct scripts to include in actions and the valid arguments to provide when running each script. The following information is provided for each script:

- **Name**.Specifies the name of the script.

- **Description**.Provides a description of the purpose of the script and any pertinent information regarding script customization.

- **Input**. Indicates the files used for input to the script.

- **Output**.Indicates the files created or modified by the script.

- **References**.Indicates other scripts or configuration files that are referenced by the script.

- **Location**.Indicates the folder where the script can be found. In the information for the location, the following variables are used:

  - **program_files**. This variable points to the location of the Program Files folder on the computer where MDT is installed.

  - **distribution**. This variable points to the location of the Distribution folder for the deployment share.

  - **platform**. This variable is a placeholder for the operating system platform (x86 or x64).

- **Use**.Provides the commands and options that you can specify.

- **Arguments and description**. Indicate the valid arguments to be specified for the script and a brief description of what each argument means.

- **Properties**.The properties referenced by the script.

## BDD_Autorun.wsf

This script displays a dialog box that indicates the user inserted deployment media created by the MDT process (such as a bootable DVD or a removable hard disk). The message is displayed for 15 seconds. If no action is taken, the script starts LiteTouch.vbs.

 For more information about LiteTouch.vbs, see [LiteTouch.vbs](#litetouchvbs).

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information required by the scripts to complete the deployment process|
|**Output**|None|
|**References**|**LiteTouch.vbs**. Initiates LTI|
|**Location**|*distribution*\Scripts|
|**Use**|None|

### Arguments

|**Value**|**Description**|
|-|-|
|None|None|

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|None|||

## BDD_Welcome_ENU.xml

This XML file contains the script code and HTML layout for the **Welcome to Windows Deployment** page that is displayed at the start of the Deployment Wizard. This XML file is read by Wizard.hta, which runs the wizard pages embedded in this XML file.

|**Value**|**Description**|
|-|-|
|**Input**|None|
|**Output**|None|
|**References**|- **NICSettings_Definition_ENU.xml**. Allows the user to provide configuration settings for network adapters<br><br> - **Wizard.hta**. Displays the Deployment Wizard pages<br><br> - **WPEUtil.exe**. Initializes Windows PE and network connections; initiates LTI|
|**Location**|*distribution*\Tools\\*platform*|
|**Use**|`mshta.exeWizard.hta BDD_Welcome_ENU.xml`|

### Arguments

|**Value**|**Description**|
|-|-|
|None|None|

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**KeyboardLocalePE**|-||
|**WelcomeWizardCommand**||-|
|**WizardComplete**||-|

## Credentials_ENU.xml

This XML file contains the script code and HTML layout for the **Specify credentials for connecting to network shares** wizard page in the Deployment Wizard. This XML file is read by Wizard.hta, which runs the wizard pages embedded in this XML file.

> [!NOTE]
>
> This wizard page is only displayed if there is a failure while validating the predefined user credentials.

|**Value**|**Description**|
|-|-|
|**Input**|None|
|**Output**|None|
|**References**|**Credentials_scripts.vbs**. Contains user credential support functions|
|**Location**|*distribution*\Scripts|
|**Use**|`mshta.exe Wizard.hta /NotWizard /definition:Credentials_ENU.xml [/ValidateAgainstDomain:domain &#124; /ValidateAgainstUNCPath:uncpath]  </DoNotSave> </LeaveShareOpen>`|

### Arguments

|**Value**|**Description**|
|-|-|
|None|None|

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|None|||

## Credentials_scripts.vbs

This script parses the arguments that were provided when loading the Credentials_ENU.xml file into the Deployment Wizard. It also performs user credential validation. This script is read by the Credentials_ENU.xml file.

 For more information about Credentials_ENU.xml, see the corresponding topic in [Credentials_ENU.xml](#credentials_enuxml).

|**Value**|**Description**|
|-|-|
|**Input**|None|
|**Output**|Event messages are written to these log files:<br><br> - **Credentials_scripts.log**. Log file that contains events generated by this script<br><br> - **BDD.log**. Log file that contains events generated by all MDT scripts|
|**References**|None|
|**Location**|*distribution*\Scripts|
|**Use**|`<script language="VBScript" src="Credentials_scripts.vbs"/>`|

### Arguments

|**Value**|**Description**|
|-|-|
|None|None|

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**UserCredentials**||-|
|**UserDomain**|-||

## DeployWiz_Definition_ENU.xml

This XML file contains the script code and HTML layout for each wizard page in the Deployment Wizard. This file is read by Wizard.hta, which runs the wizard pages embedded in this XML file. This .xml file contains the following wizard pages:

- **Welcome**

- **Specify credentials for connecting to network shares**

- **Task Sequence**

- **Computer Details**

- **User Data**

- **Move Data and Settings**

- **User Data (Restore)**

- **Computer Backup**

- **Product Key**

- **Language Packs**

- **Locale and Time**

- **Roles and Features**

- **Applications**

- **Administrator Password**

- **Local Administrators**

- **Capture Image**

- **BitLocker**

- **Ready to Begin**

|**Value**|**Description**|
|-|-|
|**Input**|None|
|**Output**|None|
|**References**|- **DeployWiz_Initialization.vbs**. Includes support functions and subroutines used by the script<br><br> - **DeployWiz_Validation.vbs**. Includes support functions and subroutines used by the script<br><br> - **ZTIBackup.wsf**. Creates a backup of the target computer<br><br> - **ZTIPatches.wsf**. Installs updates (language packs, security updates, and so on)<br><br> - **ZTIUserState.wsf**. Initializes user state migration to capture and restore user state on the target computer|
|**Location**|*distribution*\Scripts|
|**Use**|None|

### Arguments

|**Value**|**Description**|
|-|-|
|None|None|

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**DeploymentMethod**|-||
|**DeploymentType**|-||
|**DoCapture**|-||
|**ImageBuild**|-||
|**ImageFlags**|-||
|**IsBDE**|-||
|**IsServerOS**|-||
|**JoinDomain**|-||
|**OSDComputerName**|-||
|**OSVersion**|-||
|**SkipAdminAccounts**|-||
|**SkipAdminPassword**|-||
|**SkipApplications**|-||
|**SkipBitLocker**|-||
|**SkipCapture**|-||
|**SkipComputerBackup**|-||
|**SkipComputerName**|-||
|**SkipDomainMembership**|-||
|**SkipLocaleSelection**|-||
|**SkipPackageDisplay**|-||
|**SkipProductKey**|-||
|**SkipRoles**|-||
|**SkipSummary**|-||
|**SkipTaskSequence**|-||
|**SkipTimeZone**|-||
|**SkipUserData**|-||
|**TaskSequenceTemplate**|-||
|**UserDomain**|-||
|**UserID**|-||
|**UserPassword**|-||
|**USMTOfflineMigration**|-||

## DeployWiz_Initialization.vbs

This script initializes the pages in the **Deployment Wizard** (stored in [DeployWiz_Definition_ENU.xml](#deploywiz_definition_enuxml)). It also contains functions and subroutines that the Deployment Wizard calls during an LTI deployment.

|**Value**|**Description**|
|-|-|
|**Input**|- **DomainOUList.xm**l. Contains a list of domain OUs<br><br> - **ListOfLanguages.xml**<br><br> - **LocationServer.xml**. Contains a list of available deployment shares<br><br> - **Environment variables**. Contains the list of property values, custom properties, database connections, deployment rules, and other information that the scripts require to complete the deployment process; the environment variables are populated by ZTIGather.wsf|
|**Output**|Event message are written to these log files:<br><br> - **DeployWiz_Initialization.log**. Log file that contains events generated by this script<br><br> - **BDD.log**. Log file that contains events generated by all MDT scripts|
|**References**|**ZTIApplications.wsf**. Initiates application installation|
|**Location**|*distribution*\Scripts|
|**Use**|`<script language="VBScript" src="DeployWiz_Initialization.vbs"/>`|

### Arguments

|**Value**|**Description**|
|-|-|
|None|None|

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**Architecture**|-||
|**Applications**|-||
|**BackupDir**|-||
|**BackupFile**|-||
|**BackupShare**|-||
|**BDEInstall**|-||
|**BDEKeyLocation**|-||
|**BDERecoveryKey**|-||
|**BDEWaitForEncryption**|-||
|**CapableArchitecture**|-||
|**ComputerBackupLocation**|-||
|**CustomWizardSelectionProfile**|-||
|**DeploymentType**|-||
|**DeployRoot**|-||
|**DomainAdmin**|-||
|**DomainAdminDomain**|-||
|**DomainAdminPassword**|-||
|**DomainOUs**|-||
|**ImageBuild**|-||
|**ImageFlags**|-||
|**ImageLanguage**|-||
|**ImageLanguage001**|-||
|**ImageProcessor**|-||
|**IsServerOS**|-||
|**KeyboardLocale**|-||
|**KeyboardLocale_Edit**|-||
|**LanguagePacks**|-||
|**LanguagePacks001**|-||
|**LocalDeployRoot**|-||
|**MandatoryApplications**|-||
|**OSDComputerName**|-||
|**OSCurrentBuild**|-||
|**OSDBitLockerCreateRecoveryPassword**|-||
|**OSDBitLockerMode**|-||
|**OSDBitLockerStartupKeyDrive**|-||
|**OSDBitLockerWaitForEncryption**|-||
|**OSSKU**|-||
|**OSVersion**|-||
|**OverrideProductKey**|-||
|**ProductKey**|-||
|**SkipCapture**|-||
|**SkipDomainMembership**|-||
|**TaskSequenceID**|-||
|**TimeZoneName**|-||
|**TSGUID**|-||
|**UDDir**|-||
|**UDShare**|-||
|**UILanguage**|-||
|**UserDataLocation**|-||
|**UserDomain**|-||
|**UserID**|-||
|**UserLocale**|-||
|**UserPassword**|-||
|**WizardSelectionProfile**|-||

## DeployWiz_Validation.vbs

This script initializes and validates the information typed in the pages of the Deployment Wizard (stored in [DeployWiz_Definition_ENU.xml](#deploywiz_definition_enuxml)). This script contains functions and subroutines that the Deployment Wizard calls during an LTI deployment.

|**Value**|**Description**|
|-|-|
|**Input**|- **OperatingSystems.xml**. Contains the list of operating systems available for deployment<br><br> - **Environment variables**. Contains the list of property values, custom properties, database connections, deployment rules, and other information required by the scripts to complete the deployment process; the environment variables are populated by ZTIGather.wsf|
|**Output**|None|
|**References**|- **Credentials_ENU.xml**. Prompts the user for credentials that will be used when connecting to network resources<br><br> - **ZTIGather.wsf**. Gathers properties and processing rules|
|**Location**|*distribution*\Scripts|
|**Use**|`<script language="VBScript" src="DeployWiz_Validation.vbs"/>`|

### Arguments

|**Value**|**Description**|
|-|-|
|None|None|

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**Architecture**|-||
|**DeploymentType**|-|-|
|**DeployTemplate**||-|
|**ImageBuild**|-||
|**ImageProcessor**|-|-|
|**OSVersion**|-||
|**TaskSequenceID**||-|
|**TSGUID**|-||
|**UserCredentials**|-||
|**UserDomain**||-|
|**UserID**||-|
|**UserPassword**||-|

## LiteTouch.vbs

This script is called by the Deployment Wizard to initiate LTI. The script:

- Removes the C:\MININT folder (if it exists)

- Checks that the target computer meets the requirements for running the Deployment Wizard by calling [ZTIPrereq.vbs](#ztiprereqvbs)

- Starts the Deployment Wizard by running [LiteTouch.wsf](#litetouchwsf)

|**Value**|**Description**|
|-|-|
|**Input**|None|
|**Output**|None|
|**References**|- **BDDRun.exe**<br><br> - **ZTIPrereq.vbs**. Used to determine whether the target computer meets the prerequisites for deploying a new operating system<br><br> - **LiteTouch.wsf**. The script responsible for controlling the LTI deployment process|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript LiteTouch.vbs </debug:value>`|

### Arguments

|     **Value**      |                                                                                                                                                     **Description**                                                                                                                                                     |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/debug:*value*** | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> - **TRUE**, event messages are sent to the console and the .log files<br><br> - **FALSE**, event messages are sent only to the .log files (this is the behavior when the argument is not provided) |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|None|||

## LiteTouch.wsf

This script is called by [LiteTouch.vbs](#litetouchvbs) and is responsible for controlling the LTI deployment process. This includes:

- Running the Deployment Wizard

- Running the LTI deployment process by using the appropriate task sequence file

|**Value**|**Description**|
|-|-|
|**Input**|- ***task_sequence_file*.xml**. Contains the tasks and sequence of tasks for the LTI deployment process<br><br> - **Environment variables**. Contains the list of property values, custom properties, database connections, deployment rules, and other information required by the scripts to complete the deployment process; the environment variables are populated by ZTIGather.wsf|
|**Output**|-                          **LiteTouch.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|-                          **BDD_Welcome_ENU.xml**. Displays the Deployment Wizard **Welcome** page for LTI deployment<br><br> -                          **DeployWiz_Definition_ENU.xml**. Displays the Deployment Wizard pages for LTI deployment<br><br> -                          **Diskpart.exe**. Utility that allows the automated management of disks, partitions, and volumes<br><br> -                          **LTICleanup.wsf**. Performs cleanup tasks after deployment finishes<br><br> -                          **LTICopyScripts.wsf**. Copies the deployment scripts to a local hard drive on the target computer<br><br> -                          **MSHTA.exe**. HTML application host<br><br> -                          **RecEnv.exe**. If this utility exists, the user is prompted to determine whether to launch Windows Recovery Environment.<br><br> -                          **Regsvr32.exe**. Registers files (.dll, .exe, .ocx, and so on) with the operating system<br><br> -                          **Summary_Definition_ENU.xml**. Displays the summary results for the LTI deployment<br><br> -                          **TsmBootStrap.exe**. Task sequence Bootstrap utility<br><br> -                          **Wizard.hta**. Displays the Deployment Wizard pages<br><br> -                          **WPEUtil.exe**. Initializes Windows PE and network connections; initiates LTI<br><br> -                          **ZTIGather.wsf**. Gathers properties and processing rules<br><br> -                          **ZTIPrereq.vbs**. Checks that the target computer meets the requirements for running the Deployment Wizard<br><br> -                          **ZTINICConfig.wsf**. Configures activated network adapters<br><br> -                          **ZTIUtility.vbs**. Includes support functions and subroutines the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`BDDRun.exe "wscript.exe <ScriptDirectory>\LiteTouch.wsf </debug:value>"`|

### Arguments

|     **Value**      |                                                                                                                                                                                  **Description**                                                                                                                                                                                  |
|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/debug:*value*** | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (this is the behavior when the argument is not provided) |
|     **/Start**     |                                                                                                                                                  Creates a shortcut in the new operating system that runs once the shell starts                                                                                                                                                   |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**_DoNotCleanLiteTouch**|-||
|**_SMSTSPackageName**||-|
|**AdminPassword**|-||
|**Architecture**|-|-|
|**BootPE**|-|-|
|**ComputerBackupLocation**||-|
|**ComputerName**|-||
|**DeployDrive**|-|-|
|**DeploymentMethod**|-|-|
|**DeploymentType**|-|-|
|**DeployRoot**|-|-|
|**DestinationLogicalDrive**||-|
|**DomainAdmin**||-|
|**DomainAdminDomain**||-|
|**DomainAdminPassword**||-|
|**FinishAction**|-||
|**HostName**|-||
|**IsServerCoreOS**|-||
|**JoinDomain**|-||
|**JoinWorkgroup**|-|-|
|**KeyboardLocalePE**|-||
|**LTISuspend**|-||
|**OSDAdapterCount**|-||
|**OSDComputerName**|-|-|
|**Phase**|-|-|
|**ResourceDrive**|-|-|
|**ResourceRoot**|-|-|
|**RetVal**||-|
|**SkipBDDWelcome**|-||
|**SkipFinalSummary**|-|-|
|**SkipWizard**|-||
|**SMSTSLocalDataDrive**||-|
|**TaskSequenceID**|-||
|**TimeZoneName**||-|
|**UserDataLocation**|-|-|
|**UserDomain**|-||
|**UserID**|-||
|**UserPassword**|-||
|**WelcomeWizardCommand**|-||
|**WizardComplete**|-||

## LTIApply.wsf

This script is responsible for installing a Windows PE image to the target computer. The Windows PE image is used to collect information about the target computer and to run the deployment tasks on the target computer.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information the scripts require to complete the deployment process|
|**Output**|-                          **LTIApply.log**. Log file that contains events that this script generates<br><br> -                          **LTIApply_wdsmcast.log**. Log file that contains events that the Wdsmcast utility generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|-                          **CMD.exe**. Allows the running of command-line tools<br><br> -                          **Bootsect.exe**. Applies a boot sector to the hard disk<br><br> -                          **ImageX.exe**. A utility used to create and manage WIM files<br><br> -                          **ZTIBCDUtility.vbs**. Includes utility functions used when performing Boot Manager tasks<br><br> -                          **ZTIConfigFile.vbs**. Includes routines for processing XML files<br><br> -                          **ZTIDiskUtility.vbs**. Includes support functions and subroutines the script uses<br><br> -                          **ZTIUtility.vbs**. Includes support functions and subroutines the script uses<br><br> -                          **Wdsmcast.exe**. A utility that target computers use to join a multicast transmission|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript LTIApply.wsf </pe> </post> </debug:value>`|

### Arguments

|     **Value**      |                                                                                                                                                                                  **Description**                                                                                                                                                                                  |
|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      **/pe**       |                                                                                                                                                    Uses the process for installing the Windows PE image on the target computer                                                                                                                                                    |
|     **/post**      |                                                                                                                                                          Cleans up unnecessary files after the installation of an image                                                                                                                                                           |
| **/debug:*value*** | Outputs the event messages to the console and to the .log files; if the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (this is the behavior when the argument is not provided) |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**Architecture**|-||
|**BootPE**||-|
|**DeployRoot**|-||
|**DestinationLogicalDrive**|-|-|
|**OSGUID**|-||
|**OSCurrentVersion**|-||
|**OSVersion**|-||
|**ImageBuild**|-||
|**ImageFlags**|-||
|**ImageProcessor**|-||
|**ISBDE**|-||
|**SourcePath**||-|
|**TaskSequenceID**|-||
|**UserDomain**|-||
|**UserID**|-||
|**UserPassword**|-||
|**WDSServer**|-||

## LTICleanup.wsf

This script removes any files or configuration settings (such as scripts, folders, registry entries, or automatic logon configuration settings) from the target computer after the deployment process finishes.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the list of property values, custom properties, database connections, deployment rules, and other information that the scripts require to complete the deployment process. The environment variables are populated by ZTIGather.wsf.|
|**Output**|-                          **LTICleanup.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|-                          **Bootsect.exe**. Applies a boot sector to the hard disk<br><br> -                          **Net.exe**. Performs network management tasks<br><br> -                          **RegSvr32.exe**. Registers files (.dll, .exe, .ocx, and so on) with the operating system<br><br> -                          **ZTIBCDUtility.vbs**. Includes utility functions used when performing Boot Manager tasks<br><br> -                          **ZTIUtility.vbs**. Includes support functions and subroutines the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript LTICleanup.wsf </debug:value>`|

### Arguments

|     **Value**      |                                                                                                                                                                                  **Description**                                                                                                                                                                                  |
|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/debug:*value*** | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (this is the behavior when the argument is not provided) |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**_DoNotCleanLiteTouch**|-||
|**DeployRoot**|-||
|**DestinationLogicalDrive**|-||
|**OSVersion**|-||

## LTICopyScripts.wsf

This script copies the deployment scripts for the LTI and ZTI deployment processes to a local hard drive on the target computer.

|**Value**|**Description**|
|-|-|
|**Input**|-                          **Summary_Definition_ENU.xml**. Displays the summary results for the LTI deployment<br><br> -                          **Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **LTICopyScripts.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|**ZTIUtility.vbs**. Includes support functions and subroutines the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript LTICopyScripts.wsf </debug:value>`|

### Arguments

|     **Value**      |                                                                                                                                                                                  **Description**                                                                                                                                                                                  |
|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/debug:*value*** | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (this is the behavior when the argument is not provided) |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|None|||

## LTIGetFolder.wsf

This script displays a dialog box that allows the user to browses to a folder. The selected folder path is stored in the FOLDERPATH environment variable.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the list of property values, custom properties, database connections, deployment rules, and other information that the scripts require to complete the deployment process. The environment variables are populated by ZTIGather.wsf.|
|**Output**|None|
|**References**|-                          **ZTIUtility.vbs**. Includes support functions and subroutines that the script uses<br><br> -                          **WizUtility.vbs**. Includes support functions and subroutines that the UI uses (such as wizard pages)|
|**Location**|-                          *distribution*\Scripts<br><br> -                          *program_files*\Microsoft Deployment Toolkit\Scripts|
|**Use**|`cscript LTIGetFolder.wsf </debug:value>`|

### Arguments

|**Value**|**Description**|
|-|-|
|**/debug:value**|Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (this is the behavior when the argument is not provided)|

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**DefaultFolderPath**|-||
|**FolderPath**||-|

## LTIOEM.wsf

This script is used by an OEM during an LTI OEM scenario to copy the contents of a media deployment share to the target computer's hard disk to prepare it for duplication.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the list of property values, custom properties, database connections, deployment rules, and other information that the scripts require to complete the deployment process. The environment variables are populated by ZTIGather.wsf.|
|**Output**|-                          **LTIOEM.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|-                          **RoboCopy.exe**. File and folder copy tool<br><br> -                          **ZTIUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript LTIOEM.wsf </BITLOCKER &#124; /BDE> </debug:value>`|

### Arguments

|     **Value**      |                                                                                                                                                                                  **Description**                                                                                                                                                                                  |
|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/debug:*value*** | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (this is the behavior when the argument is not provided) |
|   **/BITLOCKER**   |                                                                                                                                                                                 Enables BitLocker                                                                                                                                                                                 |
|      **/BDE**      |                                                                                                                                                                                 Enables BitLocker                                                                                                                                                                                 |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**_DoNotCleanLiteTouch**||-|
|**DeployDrive**|-||
|**DeployRoot**|-||
|**TSGUID**|-||

## LTISuspend.wsf

This script suspends a task sequence to allow manual tasks to be performed. When this script runs, it creates a **Resume Task Sequence** shortcut on the user's desktop that allows the user to restart the task sequence after all manual tasks are completed.

> [!NOTE]
>
> This script is only supported while in the full operating system.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the list of property values, custom properties, database connections, deployment rules, and other information the scripts require to complete the deployment process. The environment variables are populated by ZTIGather.wsf.|
|**Output**|-                          **LTISuspend.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|-                          **LiteTouch.wsf**. Controls the LTI deployment process<br><br> -                          **LTICopyScripts.wsf**. Copies the deployment scripts to a local hard drive on the target computer<br><br> -                          **ZTIUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript LTISuspend.wsf </debug:value>`|

### Arguments

|     **Value**      |                                                                                                                                                                                  **Description**                                                                                                                                                                                  |
|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/debug:*value*** | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (this is the behavior when the argument is not provided) |
|    **/Resume**     |                                                                                                                                                                                         -                                                                                                                                                                                         |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**LTISuspend**||-|
|**SMSTSRebootRequested**||-|

## LTISysprep.wsf

This script prepares the target computer for running Sysprep, runs Sysprep on the target computer, and then verifies that Sysprep ran successfully.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the list of property values, custom properties, database connections, deployment rules, and other information that the scripts require to complete the deployment process. The environment variables are populated by ZTIGather.wsf.|
|**Output**|-                          **LTISysprep.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|-                          **Expand.exe**. Expands compressed files<br><br> -                          **Sysprep.exe**. Prepares computers for duplication<br><br> -                          **ZTIConfigFile.vbs**. Contains routines for processing XML files<br><br> -                          **ZTIUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript LTISysprep.wsf </debug:value>`|

### Arguments

|     **Value**      |                                                                                                                                                                                  **Description**                                                                                                                                                                                   |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/debug:*value*** | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (This is the behavior when the argument is not provided.) |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**Architecture**|-||
|**DeployRoot**|-||
|**DestinationLogicalDrive**|-||
|**DoCapture**|-||
|**OSCurrentBuild**|-||
|**OSDAnswerFilePath**|-||
|**OSGUID**|-||
|**SourcePath**|-|-|
|**TaskSequenceID**|-||

## NICSettings_Definition_ENU.xml

This XML file contains the script code and HTML layout for the **Configure Static IP Network Settings** wizard page in the Deployment Wizard. During an LTI deployment, Wizard.hta reads this file and runs the embedded wizard page that prompts for the required network addressing configuration. If no static IP addressing configuration is supplied, the deployment scripts will default to using DHCP to obtain the required network configuration.

|**Value**|**Description**|
|-|-|
|**Input**|None|
|**Output**|None|
|**References**|**ZTINICUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|None|

### Arguments

|**Value**|**Description**|
|-|-|
|None|None|

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**OSDAdapterxDNSServerList**||-|
|**OSDAdapterxDNSSuffix**||-|
|**OSDAdapterxGateways**||-|
|**OSDAdapterxIPAddressList**||-|
|**OSDAdapterxMacAddress**||-|
|**OSDAdapterxSubnetMask**||-|
|**OSDAdapterxWINSServerList**||-|
|**OSDAdapterCount**||-|

> [!NOTE]
>
> The*x*in the property names listed above is a placeholder for a zero-based array that contains network adapter information.

## Summary_Definition_ENU.xml

This XML file contains the script code and HTML layout for the **Deployment Summary** wizard page in the Deployment Wizard. During an LTI deployment, Wizard.hta reads this file and runs the embedded wizard page that displays the summary results for the LTI deployment. This XML file contains the following wizard pages:

- **Success**. Notification regarding the successful completion of the deployment tasks

- **Failure**. Notification regarding the failure to successfully complete the deployment tasks

|**Value**|**Description**|
|-|-|
|**Input**|None|
|**Output**|None|
|**References**|**Summary_Scripts.vbs**. Includes support functions and subroutines that the wizard pages embedded in this XML file use|
|**Location**|*distribution*\Scripts|
|**Use**|None|

### Arguments

|**Value**|**Description**|
|-|-|
|None|None|

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**SkipFinalSummary**|-||
|**RetVal**|-||

## Summary_scripts.vbs

This script is called by the **Summary** wizard page of the Deployment Wizard. It contains functions and subroutines used for initialization and validation.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|Event message are written to these log files:<br><br> -                          **Summary_scripts.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|None|
|**Location**|*distribution*\Scripts|
|**Use**|`<script language="VBScript" src="Summary_Scripts.vbs"/>`|

### Arguments

|**Value**|**Description**|
|-|-|
|None|None|

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**DeploymentType**|-||
|**RetVal**|-||

## Wizard.hta

This Hypertext Application displays the Deployment Wizard pages.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the list of property values, custom properties, database connections, deployment rules, and other information that the scripts require to complete the deployment process. The environment variables are populated by ZTIGather.wsf.|
|**Output**|-                          **Wizard.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|-                          **LTIGetFolder.wsf**. Script file that initiates a **BrowseForFolder** dialog box<br><br> -                          **ZTIConfigFile.vbs**. Includes routines for processing XML files<br><br> -                          **ZTIUtility.vbs**. Includes support functions and subroutines that the script uses<br><br> -                          **WizUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|-                          *distribution*\Scripts<br><br> -                          *program_files*\Microsoft Deployment Toolkit\Scripts|
|**Use**|`mshta.exe Wizard.hta </definition:filename> </NotWizard> </debug:value>`|

### Arguments

|         **Value**          |                                                                                                                                                                                  **Description**                                                                                                                                                                                   |
|----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     **/debug:*value***     | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (This is the behavior when the argument is not provided.) |
|       **/NotWizard**       |                                                                                                                                                                         Used to bypass wizard page prompts                                                                                                                                                                         |
| **/Definition:*filename*** |                                                                                                                                                            Specifies the XML file that is to be loaded into the wizard                                                                                                                                                             |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**Definition**|-||
|**DefaultFolderPath**||-|
|**FolderPath**|-||
|**WizardComplete**||-|

## WizUtility.vbs

This script contains functions and subroutines that the various Deployment Wizard scripts reference.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **WizUtility.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|**LTIGetFolder.wsf**. Script file that initiates a **BrowseForFolder**dialog box|
|**Location**|-                          *distribution*\Scripts<br><br> -                          *program_files*\Microsoft Deployment Toolkit\Scripts|
|**Use**|`<script language="VBScript" src="WizUtility.vbs"/>`|

### Arguments

|**Value**|**Description**|
|-|-|
|None|None|

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**DefaultFolderPath**||-|
|**DefaultDestinationDisk**|-||
|**DefaultDestinationIsDirty**|-||
|**DefaultDestinationPartition**|-||
|**DeploymentType**|-||
|**DestinationDisk**|-||
|**FolderPath**|-||
|**OSVersion**|-||
|**UserDomain**|-||
|**UserCredentials**||-|

## ZTIApplications.wsf

This script initiates an installation of applications that have been configured in the Applications node in Deployment Workbench. This script will not attempt to install any application that:

- Does not support the target computer's platform type

- Does not support the target computer's processor type

- Has an uninstall entry in the registry under **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall**

> [!NOTE]
>
> If the listed application has any dependent applications defined, this script attempts to install those dependent applications before installing the listed application.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **ZTIApplications.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|-                          **ZTIConfigFile.vbs**. Includes routines for processing XML files<br><br> -                          **ZTIUtility.vbs**. Includes support functions and subroutines that the script uses<br><br> -                          **BDDRun.exe**. Runs a command that requires user interaction|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript ZTIApplications.wsf </debug:value>`|

### Arguments

|     **Value**      |                                                                                                                                                                                  **Description**                                                                                                                                                                                  |
|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/debug:*value*** | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (this is the behavior when the argument is not provided) |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**ApplicationGUID**|-||
|**ApplicationSuccessCodes**|-||
|**DependentApplications**|-||
|**DeploymentMethod**|-||
|**InstalledApplications**|-|-|
|**ResourceDrive**|-||
|**ResourceRoot**|-|-|
|**SMSTSRebootRequested**||-|
|**SMSTSRetryRequested**||-|

## ZTIAppXmlGen.wsf

This script generates an XML file—ZTIAppXmlGen.xml—to use when automatically capturing user data (documents) associated with installed applications. It does so through the **HKEY_CLASSES_ROOT\Software\Classes** registry key and captures any applications that:

- Are not associated with one of these file extensions: .mp3, .mov, .wma, .wmv, .chm, .evt, .evtx, .exe, .com, or .fon

- Are not associated with Microsoft Office, such as the 2007 Office system or Microsoft Office 2003.

- Have a valid open handler listed at **HKEY_CLASSES_ROOT\application\shell\open\command**

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **ZTIAppXmlGen.xml**.Contains a list of applications installed on the target computer<br><br> -                          **ZTIAppXmlGen.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|**ZTIUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript ZTIAppXmlGen.wsf </debug:value>`|

### Arguments

|     **Value**      |                                                                                                                                                                                  **Description**                                                                                                                                                                                   |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/debug:*value*** | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (This is the behavior when the argument is not provided.) |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**DeploymentMethod**|-||
|**DeploymentType**|-||
|**ImageBuild**|-||
|**OSCurrentVersion**|-||
|**USMTMigFiles**|-|-|

## ZTIAuthorizeDHCP.wsf

This script uses the Netsh tool to configure the target computer so that it is an authorized DHCP server in AD DS.

 For more information about authorizing DHCP servers, see [Netsh commands for DHCP](/previous-versions/windows/it-pro/windows-server-2003/cc787375(v=ws.10)).

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **ZTIAuthorizeDHCP.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|-                          **Netsh.exe**. A utility used to automate the configuration of networking components<br><br> -                          **ZTIUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript ZTIAuthorizeDHCP.wsf </debug:value>`|

### Arguments

|     **Value**      |                                                                                                                                                                                  **Description**                                                                                                                                                                                   |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/debug:*value*** | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (This is the behavior when the argument is not provided.) |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**IPAddress**|-||

## ZTIBackup.wsf

This script performs a backup of the target computer using the ImageX utility. The backup is stored in the location specified in the [BackupDir](properties.md#backupdir) and [BackupShare](properties.md#backupshare) properties.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **ZTIBackup.log**. Log file that contains events that this script generates<br><br> -                          **ZTIBackup_imagex.log**. Log file that contains events that ImageX generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|-                          **ImageX.exe**. A utility used to create and manage WIM files<br><br> -                          **ZTIBCDUtility.vbs**. Includes utility functions used when performing Boot Manager tasks<br><br> -                          **ZTIDiskUtility.vbs**. Includes support functions and subroutines that the script uses<br><br> -                          **ZTIUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript ZTIBackup.wsf </debug:value>`|

### Arguments

|     **Value**      |                                                                                                                                                                                  **Description**                                                                                                                                                                                  |
|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/debug:*value*** | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (this is the behavior when the argument is not provided) |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**BackupDir**|-||
|**BackupDisk**|-||
|**BackupDrive**|-||
|**BackupFile**|-||
|**BackupPartition**|-||
|**BackupScriptComplete**||-|
|**BackupShare**|-||
|**ComputerBackupLocation**|-||
|**DeploymentMethod**|-||
|**DeploymentType**|-||
|**DestinationLogicalDrive**|-|-|
|**DoCapture**|-||
|**ImageBuild**|-||
|**ImageFlags**|-||
|**OSDStateStorePath**|-||
|**Phase**|-||
|**TaskSequenceID**|-||
|**USMTLocal**|-||

## ZTIBCDUtility.vbs

This script contains utility functions that some MDT scripts use when performing Boot Manager tasks.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|None|
|**References**|**BCDEdit.exe**. A tool for editing the Windows boot configuration|
|**Location**|-                          *distribution*\Scripts<br><br> -                          *program_files*\Microsoft Deployment Toolkit\Scripts|
|**Use**|`<script language="VBScript" src="ZTIBCDUtility.vbs"/>`|

### Arguments

|**Value**|**Description**|
|-|-|
|None|None|

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|None|||

## ZTIBde.wsf

This script installs and configures BitLocker on the target computer. BitLocker configuration is limited to New Computer scenarios that have hard disks configured with a single partition.

> [!NOTE]
>
> For ZTI and UDI deployments, the **UILanguage** property must be set in CustomSettings.ini or in the MDT DB, because ZTIBde.wsf tries to read the locale from the **UILanguage** property.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **ZTIBde.log**. Log file that contains events that this script generates<br><br> -                          **ZTIBdeFix_diskpart.log**. Log file that contains events that the Diskpart tool generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|-                          **CMD.exe**. Allows running of command-line tools<br><br> -                          **Defrag.exe**. Defragments the hard disk<br><br> -                          **Diskpart.exe**. Utility that allows for the automated management of disks, partitions, and volumes<br><br> -                          **ServerManagerCmd.exe**<br><br> -                          **ZTIDiskUtility.vbs**. Includes support functions and subroutines that the script uses<br><br> -                          **ZTIOSRole.wsf**. Installs server roles<br><br> -                          **ZTIUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript ZTIBde.wsf </debug:value>`|

### Arguments

|     **Value**      |                                                                                                                                                                                  **Description**                                                                                                                                                                                  |
|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/debug:*value*** | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (this is the behavior when the argument is not provided) |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**AdminPassword**|-||
|**BDEDriveLetter**|-|-|
|**BDEDriveSize**|-||
|**BDEInstall**|-||
|**BDEInstallSuppress**|-||
|BDEKeyLocation|-||
|**BDEPin**|-||
|**BDERecoveryKey**|-||
|**BDESecondPass**|-|-|
|**BdeWaitForEncryption**|-||
|**BitlockerInstalled**|-|-|
|**DeploymentMethod**|-||
|**ISBDE**|-||
|**OSDBitLockerCreateRecoveryPassword**|-||
|**OSDBitLockerMode**|-||
|**OSDBitLockerStartupKey**|-||
|**OSDBitLockerStartupKeyDrive**|-||
|**OSDBitLockerTargetDrive**|-||
|**OSDBitLockerWaitForEncryption**|-||
|**OSCurrentBuild**|-||
|**OSCurrentVersion**|-||
|**OSFeatures**|-|-|
|**OSRoles**|-|-|
|**OSRoleServices**|-|-|
|**OSVersion**|-||
|**SMSTSRebootRequested**|-|-|
|**SMSTSRetryRequested**||-|
|**TPMOwnerPassword**|-||

## ZTIBIOSCheck.wsf

This script checks the BIOS on the target computer, and then looks at a list of BIOSes that are incompatible with Windows. The list of incompatible BIOSes is stored in the [ZTIBIOSCheck.xml](support-files.md#ztibioscheckxml) file.

 If the BIOS on the target computer is listed in the [ZTIBIOSCheck.xml](support-files.md#ztibioscheckxml) file, then the script returns a status that indicates the BIOS is incompatible with Windows and the deployment process should be terminated. For information on populating the list of incompatible BIOSes, see [ZTIBIOSCheck.xml](support-files.md#ztibioscheckxml).

|**Value**|**Description**|
|-|-|
|**Input**|-                          **ZTIBIOSCheck.xml**. Contains a list of BIOSes that are known to be incompatible with Windows<br><br> -                          **Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **ZTIBIOSCheck.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|**ZTIUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript ZTIBIOSCheck.wsf </debug:value>`|

### Arguments

|     **Value**      |                                                                                                                                                                                  **Description**                                                                                                                                                                                  |
|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/debug:*value*** | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (this is the behavior when the argument is not provided) |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|None|||

## ZTICoalesce.wsf

Configuration Manager requires packages to be numbered sequentially starting with **PACKAGES001**, with no gaps in the number sequence. Otherwise, installation will fail.

 This script allows you to define and name variables using identifying information about the program to run—for example, **ComputerPackages100**, **ComputerPackages110**, or **CollectionPackages150**. Then, when this script is run, Configuration Manager finds all variables that match a pattern (for example, all variable names that contain the string **Packages**) and builds a sequential list, without gaps, using the base name **PACKAGES**.

 For example, if the following variables were defined (using computer variables, collection variables, or in CustomSettings.ini or the MDT DB, for example):

- **ComputerPackages100=XXX00001:Program**

- **ComputerPackages110=XXX00002:Program**

- **CollectionPackages150=XXX00003:Program**

- **Packages001=XXX00004:Program**

  After the script runs, the list would be:

- **PACKAGES001=XXX00004:Program**

- **PACKAGES002=XXX00001:Program**

- **PACKAGES003=XXX00002:Program**

- **PACKAGES004=XXX00003:Program**

  Configuration Manager would then be able to run all four programs.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **ZTICoalesce.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|**ZTIUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript ZTICoalesce.wsf </debug:value>`|

### Arguments

|          **Value**          |                                                                                                                                                                                  **Description**                                                                                                                                                                                   |
|-----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     **/debug:*value***      | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (This is the behavior when the argument is not provided.) |
| **/CoalesceDigits:*value*** |                  Specifies the number of digits that need to be provided when creating the numbering sequence. For example, a value of:<br><br> -                              **2** would create PACKAGE03<br><br> -                              **3** would create PACKAGE003<br><br> The default value if this argument is not provided is **3**.                   |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**CoalescePattern**|-||
|**CoalesceTarget**|-||

## ZTIConfigFile.vbs

This script contains common routines for processing MDT XML files.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **ZTIConfigFile.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|Net.exe|
|**Location**|*distribution*\Scripts|
|**Use**|`<script language="VBScript" src="ZTIConfigFile.vbs"/>`|

### Arguments

|**Value**|**Description**|
|-|-|
|None|None|

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**IsSafeForWizardHTML**|-||
|**MandatoryApplications**|-||
|**SkipGroupSubFolders**|-||

## ZTIConfigure.wsf

This script configures the Unattend.xml file with the property values specified earlier in the MDT deployment process. The script configures the appropriate file based on the operating system being deployed.

 This script reads the ZTIConfigure.xml file to determine how to update the Unattend.xml file with the appropriate values specified in the deployment properties. The ZTIConfigure.xml file contains the information to translate properties to settings in the Unattend.xml file.

|**Value**|**Description**|
|-|-|
|**Input**|-                          **ZTIConfigure.xml**. Contains a list of property values (specified earlier in the deployment process) and their corresponding configuration settings<br><br> -                          **Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **ZTIConfigure.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|**ZTIUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript ZTIConfigure.wsf </debug:value>`|

### Arguments

|     **Value**      |                                                                                                                                                                                  **Description**                                                                                                                                                                                   |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/debug:*value*** | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (This is the behavior when the argument is not provided.) |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**ComputerName**|-|-|
|**DeploymentType**|-||
|**DeploymentMethod**|-||
|**DeployRoot**|-||
|**DestinationLogicalDrive**|-||
|DomainAdminDomain|-||
|**ImageBuild**|-||
|**OSDAnswerFilePath**|-||
|**OSDAnswerFilePathSysprep**|-||
|**OSDComputerName**|-||
|**Phase**|-||
|**TaskSequenceID**|-||

## ZTIConfigureADDS.wsf

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **ZTIConfigureADDS.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|-                          **Dcpromo.exe**. Installs and removes AD DS<br><br> -                          **Net.exe**. Performs network management tasks<br><br> -                          **ZTIUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript ZTIConfigureADDS.wsf </debug:value>`|

### Arguments

|     **Value**      |                                                                                                                                                                                  **Description**                                                                                                                                                                                   |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/debug:*value*** | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (This is the behavior when the argument is not provided.) |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**ADDSLogPath**|-||
|**ADDSPassword**|-||
|**ADDSUserDomain**|-||
|**ADDSUserName**|-||
|**AutoConfigDNS**|-||
|**ChildName**|-||
|**ConfirmGC**|-||
|**DatabasePath**|-||
|**DomainLevel**|-||
|**DomainNetBiosName**|-||
|**ForestLevel**|-||
|**NewDomain**|-||
|**NewDomainDNSName**|-||
|**OSVersion**|-||
|**ParentDomainDNSName**|-||
|**ReplicaOrNewDomain**|-|-|
|**ReplicaDomainDNSName**|-||
|**ReplicationSourceDC**|-||
|**SafeModeAdminPassword**|-||
|**SiteName**|-||
|**SysVolPath**|-||

## ZTIConfigureDHCP.wsf

This script configures DHCP on the target computer.

> [!NOTE]
>
> DHCP should already be installed on the target computer before running this script.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **ZTIConfigureDHCP.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|-                          **Netsh.exe**. A utility that permits automating the configuration of networking components<br><br> -                          **ZTIUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript ZTIConfigureDHCP.wsf </debug:value>`|

### Arguments

|     **Value**      |                                                                                                                                                                                  **Description**                                                                                                                                                                                   |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/debug:*value*** | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (This is the behavior when the argument is not provided.) |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**DHCPScopesxDescription**|-||
|**DHCPScopesxEndIP**|-||
|**DHCPScopesxExcludeStartIP**|-||
|**DHCPScopesxExcludeEndIP**|-||
|**DHCPScopesxIP**|-||
|**DHCPScopesxName**|-||
|**DHCPScopesxOptionRouter**|-||
|**DHCPScopesxOptionDNSDomainName**|-||
|**DHCPScopesxOptionDNSServer**|-||
|**DHCPScopesxOptionLease**|-||
|**DHCPScopesxOptionNBTNodeType**|-||
|**DHCPScopesxOptionPXEClient**|-||
|**DHCPScopesxOptionWINSServer**|-||
|**DHCPScopesxStartIP**|-||
|**DHCPScopesxSubnetmask**|-||
|**DHCPServerOptionDNSDomainName**|-||
|DHCPServerOptionDNSServer|-||
|**DHCPServerOptionNBTNodeType**|-||
|**DHCPServerOptionPXEClient**|-||
|**DHCPServerOptionRouter**|-||
|**DHCPServerOptionWINSServer**|-||

> [!NOTE]
>
> The *x*in the properties listed here is a placeholder for a zero-based array that contains DHCP configuration information.

## ZTIConfigureDNS.wsf

This script configures DNS on the target computer. To perform the actual configuration tasks, the script uses the Dnscmd utility.

 For more information about Dnscmd.exe, see [Dnscmd Overview](/previous-versions/windows/it-pro/windows-server-2003/cc778513(v=ws.10)).

> [!NOTE]
>
> DNS should already be installed on the target computer before running this script.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **ZTIConfigureDNS.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|-                          **Dnscmd.exe**. Assists administrators with DNS management<br><br> -                          **ZTIUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript ZTIConfigureDNS.wsf </debug:value>`|

### Arguments

|     **Value**      |                                                                                                                                                                                  **Description**                                                                                                                                                                                   |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/debug:*value*** | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (This is the behavior when the argument is not provided.) |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**DNSServerOptionDisableRecursion**|-||
|**DNSServerOptionBINDSecondaries**|-||
|**DNSServerOptionFailOnLoad**|-||
|**DNSServerOptionEnableRoundRobin**|-||
|**DNSServerOptionEnableNetmaskOrdering**|-||
|**DNSServerOptionEnableSecureCache**|-||
|**DNSServerOptionNameCheckFlag**|-||
|**DNSZonesxName**|-||
|**DNSZonesxType**|-||
|**DNSZonesxMasterIP**|-||
|**DNSZonesxDirectoryPartition**|-||
|**DNSZonesxFileName**|-||
|**DNSZonesxScavenge**|-||
|**DNSZonesxUpdate**|-||

> [!NOTE]
>
> The *x*in the properties listed here is a placeholder for a zero-based array that contains DNS configuration information.

## ZTIConnect.wsf

The MDT deployment process uses this script to authenticate with a server computer (such as a computer running SQL Server or another server that has a shared network folder). When this script is run, it validates that a connection can be created to the network shared folder specified in the **/uncpath** argument.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **ZTIConnect.log**.  Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|**ZTIUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript ZTIConnect.wsf /UNCPath:<uncpath> </debug:value>`|

### Arguments

|      **Value**       |                                                                                                                                                                                  **Description**                                                                                                                                                                                   |
|----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/UNCPath:uncpath** |                                                                                                                                                          Specifies a fully qualified UNC path to a network shared folder                                                                                                                                                           |
|  **/debug:*value***  | Outputs the event messages to the console and to the .log files; if the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (This is the behavior when the argument is not provided.) |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|None|||

## ZTICopyLogs.wsf

Copy the Smsts.log and BDD.log files to a subfolder beneath the share that the **SLShare** property specifies. The subfolder takes the name that **OSDComputerName**, **_SMSTSMachineName**, or **HostName** specifies.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **ZTICopyLogs.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|**ZTIUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript ZTICopyLogs.wsf </debug:value>`|

### Arguments

|      **Value**      |                                                                                                                                                                                  **Description**                                                                                                                                                                                   |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/debug: *value*** | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (This is the behavior when the argument is not provided.) |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|None|||

## ZTIDataAccess.vbs

This script contains common routines for database access.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **ZTIDataAccess.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|None|
|**Location**|*distribution*\Scripts|
|**Use**|`<script language="VBScript" src="ZTIDataAccess.vbs"/>`|

### Arguments

|**Value**|**Description**|
|-|-|
|None|None|

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**_SMSTSReserved1**|-||
|**_SMSTSReserved2**|-||
|**RulesFile**|-||
|**UserDomain**|-|-|
|**UserID**|-|-|
|**UserPassword**|-|-|

## ZTIDisableBDEProtectors.wsf

If BitLocker is enabled, this script suspends the BitLocker protectors configured on the system.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **ZTIDisableBDEProtectors.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|**ZTIUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript ZTIDisableBDEProtectors.wsf </debug:value>`|

### Arguments

|     **Value**      |                                                                                                                                                                                  **Description**                                                                                                                                                                                   |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/debug:*value*** | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (This is the behavior when the argument is not provided.) |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**ImageBuild**|-||
|**ISBDE**||-|
|**OSCurrentBuild**|-||
|**OSCurrentVersion**|-||
|**OSVersion**|-||

## ZTIDiskpart.wsf

This script creates the disk partitions on the target computer by calling the Diskpart utility. The parameters used to configure the disk are specified by the Task Sequencer or in CustomSettings.ini. ZTIDiskpart.wsf is primarily run in New Computer scenarios. The process works like this:

1. The MDT deployment process runs the ZTIDiskpart.wsf script based on the steps and sequence of steps in the Task Sequencer.

2. ZTIDiskpart.wsf starts the Diskpart utility and sends it the required configuration commands.

3. ZTIDiskpart.wsf runs Diskpart.exe and provides a .txt file as a command-line parameter.

4. The disk is initially cleaned by sending Diskpart the **CLEAN** command.

5. If this is the first disk and no disk configuration has been specified by the Task Sequencer or in CustomSettings.ini, a single partition is created to store the operating system. However, if a disk configuration has been specified, the disk will be configured according to the specified configuration.

6. If BitLocker is to be enabled, space is reserved at the end of the first disk.

7. All format commands are queued until after Diskpart has finished. If not explicitly specified by the Task Sequencer or in CustomSettings.ini, ZTIDiskpart.wsf performs a quick format of drive C using the following command: `FORMAT C: /FS:NTFS /V:OSDisk /Q /Y`.

8. ZTIDiskpart.wsf copies the ZTIDiskpart_diskpart.log and BDD.log files from the RAM disk back to the hard drive.

   Customize the disk configuration of the target computer by providing the required information in the Task Sequencer or in CustomSettings.ini.

   For more information about configuring disks, see the MDT document *Using the Microsoft Deployment Toolkit*.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **ZTIDiskpart.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|-                          **Diskpart.exe**. Utility that allows for the automated management of disks, partitions, and volumes<br><br> -                          **Format.com**. Formats the hard disk<br><br> -                          **ZTIDiskUtility.vbs**. Includes support functions and subroutines that the script uses<br><br> -                          **ZTIUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript ZTIDiskpart.wsf </debug:value>`|

### Arguments

|     **Value**      |                                                                                                                                                                                  **Description**                                                                                                                                                                                   |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/debug:*value*** | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (This is the behavior when the argument is not provided.) |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**BDEDriveLetter**|-||
|**BDEDriveSize**|-||
|**BDEInstall**|-||
|**DeployDrive**|-||
|**DeploymentType**|-||
|**DestinationDisk**|-||
|**DestinationLogicalDrive**||-|
|**DoNotCreateExtraPartition**|-||
|**ImageBuild**|-||
|**OSDDiskIndex**|-||
|**OSDDiskpartBiosCompatibilityMode**|-|-|
|**OSDDiskType**|-||
|**OSDPartitions**|-||
|**OSDPartitionStyle**|-||
|**SMSTSLocalDataDrive**||-|
|**VolumeLetterVariable**|-||

## ZTIDiskUtility.vbs

This script contains disk-related functions and subroutines that the various scripts in the MDT deployment process call.

|**Value**|**Description**|
|-|-|
|**Input**|None|
|**Output**|-                          **ZTIDiskUtility.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|-                          **BcdBoot.exe**. Configures the system partition<br><br> -                          **DiskPart.exe**. Utility that allows for the automated management of disks, partitions, and volumes|
|**Location**|*distribution*\Scripts|
|**Use**|`<script language="VBScript" src="ZTIDiskUtility.vbs"/>`|

### Arguments

|**Value**|**Description**|
|-|-|
|None|None|

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**DestinationLogicalDrive**|-||
|**UILanguage**|-|-|

## ZTIDomainJoin.wsf

During the State Restore deployment phase, this script verifies that the computer is joined to a domain and recovers from failed attempts to join a domain.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **ZTIDomainJoin.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|-                          **LTISuspend.wsf**<br><br> -                          **ZTIUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript ZTIDomainJoin.wsf </debug:value>`|

### Arguments

|             **Value**             |                                                                                                                                                                                                                                 **Description**                                                                                                                                                                                                                                  |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|        **/debug: *value***        |                                                Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (This is the behavior when the argument is not provided.)                                                |
| **/DomainErrorRecovery: *value*** | Attempts to join the computer to the domain. If the value specified in value is:<br><br> -                              **AUTO**. Retry the domain join process. Restart and retry. This is the default script behavior.<br><br> -                              **FAIL**. Stops all processing. All task sequence processing stops.<br><br> -                              **MANUAL**. Stop processing; allows the user to manually join the computer to the domain. |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**DomainAdmin**|-||
|**DomainAdminDomain**|-||
|**DomainAdminPassword**|-||
|**DomainErrorRecovery**|-||
|**DomainJoinAttempts**|-|-|
|**JoinDomain**|-||
|**JoinWorkgroup**|-||
|**LTISuspend**||-|
|**MachineObjectOU**|-||
|**SMSTSRebootRequested**||-|
|**SMSTSRetryRequested**||-|

## ZTIDrivers.wsf

This script installs additional device drivers onto the target computer before initiating the configuration of the operating system. This script reads the Drivers.xml file and copies the list of device driver files in the Drivers.xml file (created by and managed in the Drivers node in the Deployment Workbench) to the target computer.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **PnpEnum.xml**. Contains a list of all devices installed on the target computer<br><br> -                          **ZTIDrivers.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|-                          **Attrib.exe**. Sets file and folder attributes<br><br> -                          **CMD.exe. Allows running of command-line tools**<br><br> -                          **Microsoft.BDD.PnpEnum.exe**. Utility that enumerates Plug and Play devices<br><br> -                          **Reg.exe**. The console registry tool for reading and modifying registry data<br><br> -                          **ZTIConfigFile.vbs**. Includes routines for processing XML files<br><br> -                          **ZTIUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript ZTIDrivers.wsf </debug:value>`|

### Arguments

|     **Value**      |                                                                                                                                                                                  **Description**                                                                                                                                                                                   |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/debug:*value*** | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (This is the behavior when the argument is not provided.) |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**Architecture**|-||
|**CustomDriverSelectionProfile**|-||
|**DeploymentMethod**|-||
|**DeploymentType**|-||
|**DestinationLogicalDrive**|-|-|
|**DoCapture**|-||
|**DriverPaths**|-||
|**DriverSelectionProfile**|-||
|**ImageBuild**|-||
|**InstallFromPath**|-||
|**OSDAnswerFilePath**|-||
|**OSDAnswerFilePathSysPrep**|-||
|**OSDPlatformArch**|-||
|**Phase**|-||
|**ResourceRoot**|-||

## ZTIExecuteRunbook.wsf

This script runs Orchestrator runbooks on the target computer. An Orchestrator *runbook* is the sequence of activities that orchestrate actions on computers and networks. You can initiate Orchestrator runbooks in MDT using the [Execute Runbook](task-sequence-steps.md#execute-runbook) task sequence step type, which in turn runs this script.

|**Value**|**Description**|
|-|-|
|**Input**|Environment variables contain the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process.|
|**Output**|- BDD.log contains events that all MDT scripts generate.<br><br> - Return status of the runbook completion.<br><br> - Return parameters from the runbook output.|
|**References**|- ZTIUtility.vbs includes support functions and subroutines that the script uses.|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript ZTIExecuteRunbook.wsf </debug:value>`|

### Arguments

|     **Value**      |                                                                                                                                                                                  **Description**                                                                                                                                                                                   |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/debug:*value*** | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (This is the behavior when the argument is not provided.) |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**OrchestratorServer**|-||
|**RunbookName**|-||
|**RunbookID**|-||
|**RunbookParameterMode**|-||
|**RunbookParametersxParameterID**|-||
|**RunbookParametersxParameterValue**|-||
|***RunbookOutputParameters***<br><br> Note:<br><br> If a runbook returns output parameters, a task sequence variable is created for each parameter and the return value of the parameter is assigned to the task sequence variable.||-|

 This script creates the task sequence variables listed in the following table for internal script use. Do not set these task sequence variables in CustomSettings.ini or in the MDT DB.

|**Name**|**Description**|
|-|-|
|**OrchestratorServer**|Name of the server running Orchestrator specified in **Orchestrator Server** in the [Execute Runbook](task-sequence-steps.md#execute-runbook) task sequence step|
|**RunbookName**|Name of the runbook specified in **Runbook** in the [Execute Runbook](task-sequence-steps.md#execute-runbook) task sequence step|
|**RunbookID**|Identifier assigned to the runbook on the Orchestrator server|
|**RunbookParametersxParameterID**|Identifier assigned to a specific runbook parameter on the Orchestrator server|
|**RunbookParametersxParameterName**|Name assigned to a specific runbook parameter on the Orchestrator server|
|**RunbookParametersxParameterValue**|Value assigned to a specific runbook parameter on the Orchestrator server|

## ZTIGather.wsf

This script gathers the properties and processing rules that control the deployment process. The properties and rules (also known as *local properties*) are explicitly defined in this script and contained in the ZTIGather.xml file, in the CustomSettings.ini file, and in the MDT DB (created in the Database node in the Deployment Workbench).

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **ZTIGather.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|-                          **Wpeutil.exe**. Initializes Windows PE and network connections; initiates LTI<br><br> -                          **ZTIDataAccess.vbs**. Contains routines for database access<br><br> -                          **ZTIUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript ZTIGather.wsf </debug:value> </localonly> </inifile:ini_file_name>`|

### Arguments

|         **Value**          |                                                                                                                                                                                                   **Description**                                                                                                                                                                                                    |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     **/debug:*value***     |                  Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (This is the behavior when the argument is not provided.)                  |
|       **/localonly**       | Returns only information about the target computer and the current operating system installed on the target computer; does not parse the input .ini file (specified in the **/inifile** argument); returns properties and rules specified in the .ini file<br><br> If not specified, the script returns information about the target computer and the currently installed operating system; parses the .ini file |
| **/inifile:ini_file_name** |                                                                                                                 Name and path of the input .ini file that contains the properties and rules used in the deployment processIf not specified, the script uses the default value in CustomSettings.ini                                                                                                                  |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**All**|-|-|

## ZTIGroups.wsf

This script captures and restores the local group membership on the target computer. This script is called with the**/capture** argument to back up the group membership from the target computer before deploying the operating system. The **CaptureGroups** property contains the list of groups that script backs up. The script is called with the**/restore** argument to restore the group membership after the operating system is deployed. When performing a restore operation, it restores the membership of all groups that were backed up when the script was run using the **/capture** argument.

> [!NOTE]
>
> When restoring group membership, the script does not create any destination groups that do not already exist on the target computer. Therefore, be sure to include all required groups in the reference computer when building the image file.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **ZTIGroups.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate
|**References**|**ZTIUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript ZTIGroups.wsf </debug:value> </backup> </restore>`|

### Arguments

|     **Value**      |                                                                                                                                                                                  **Description**                                                                                                                                                                                   |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/debug:*value*** | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (This is the behavior when the argument is not provided.) |
|    **/capture**    |                                                                                                                              Backs up the group membership of the local groups on the target computer as specified in the **CaptureGroups** property                                                                                                                               |
|    **/restore**    |                                                                                                                                           Restores the group membership to the local groups backed up earlier in the deployment process                                                                                                                                            |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**CaptureGroups**|-||
|**Groups**|-|-|
|HostName|-||

## ZTILangPacksOnline.wsf

This script installs language packs for Windows operating systems. The script is expecting the language pack CAB files in a folder structure containing at least one folder.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **ZTILangPacksOnline.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|-                          **CMD.exe**. Allows running of command-line tools<br><br> -                          **Lpksetup.exe**. The Language Pack Setup tool used to add or remove language packs<br><br> -                          **ZTIUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript ZTILangPacksOnline.wsf </debug:value>`|

### Arguments

|     **Value**      |                                                                                                                                                                                  **Description**                                                                                                                                                                                   |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/debug:*value*** | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (This is the behavior when the argument is not provided.) |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**Architecture**|-||
|**OSVersion**|-||

## ZTIModifyVol.wsf

This script modifies a volume to set the GPT ID and attributes for utility volumes, which is necessary for creating Windows RE partitions on computers with UEFI. This script needs to be called when deploying to computers with UEFI for these situations:

- LTI deployments where custom partition (volume) structures are being created, such as creating five partitions instead of the standard four partitions that are typically created for use with UEFI

- All ZTI and UDI deployments

> [!NOTE]
>
> This script is intended to be called only when creating partitions structures for use with UEFI. This script should not be called when creating partition structures to be used in deployments without UEFI.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|BDD.log contains events that all MDT scripts generate.|
|**References**|ZTIUtility.vbs includes support functions and subroutines that the script uses.|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript ZTIModifyVol.wsf /UtilityVol:value </debug:value>`|

### Arguments

|        **Value**        |                                                                                                                                                                                  **Description**                                                                                                                                                                                   |
|-------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/UtilityVol:*value*** |                                                                                                             Provides the drive letter of the volume that needs to be configured for a Windows RE Tools partition for use with computers with UEFI (for example, "E:")                                                                                                              |
|   **/debug:*value***    | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (This is the behavior when the argument is not provided.) |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**UtilityVol**|-||

## ZTIMoveStateStore.wsf

This script moves the captured user state and backup files to C:\Windows\Temp\StateStore.

> [!NOTE]
>
> This script is run only when deploying images using Configuration Manager.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **ZTIMoveStateStore.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|**ZTIUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript ZTIMoveStateStore.wsf </debug:value>`|

### Arguments

|     **Value**      |                                                                                                                                                                                  **Description**                                                                                                                                                                                   |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/debug:*value*** | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (This is the behavior when the argument is not provided.) |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|None|||

## ZTINextPhase.wsf

This script updates the **Phase** property to the next phase in the deployment process. The Task Sequencer uses these phases to determine the sequence in which each task must be completed. The **Phase** property includes the following values:

- **VALIDATION**. Identify that the target computer is capable of running the scripts necessary to complete the deployment process.

- **STATECAPTURE**. Save any user state migration data before deploying the new target operating system.

- **PREINSTALL**. Complete any tasks that need to be done (such as creating new partitions) before the target operating system is deployed.

- **INSTALL**. Install the target operating system on the target computer.

- **POSTINSTALL**. Complete any tasks that need to be done before restoring the user state migration data. These tasks customize the target operating system before starting the target computer the first time after deployment (such as installing updates or adding drivers).

- **STATERESTORE**. Restore the user state migration data saved during the State Capture Phase.

  For more information about the **Phase** property, see [Phase](properties.md#phase).

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **ZTINextPhase.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|**ZTIUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript ZTINextPhase.wsf </debug:value>`|

### Arguments

|     **Value**      |                                                                                                                                                                                  **Description**                                                                                                                                                                                   |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/debug:*value*** | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (This is the behavior when the argument is not provided.) |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**DeploymentMethod**|-||
|**Phase**|-|-|

## ZTINICConfig.wsf

This script configures activated network adapters with values that ZTIGather.wsf captured based on the properties listed in the CustomSettings.ini file or the MDT DB (created in the Database node in the Deployment Workbench).

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **ZTINICConfig.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|-                          **ZTIUtility.vbs**. Includes support functions and subroutines that the script uses<br><br> -                          **ZTINicUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript ZTINicConfig.wsf </debug:value> </ForceCapture> </RestoreWithinWinPE>`|

### Arguments

|      **Value**      |                                                                                                                                                                                  **Description**                                                                                                                                                                                   |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/debug:*value***  | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (This is the behavior when the argument is not provided.) |
|  **/ForceCapture**  |                               If there are any local networking adapters with static IP addresses saved, this script captures those settings and saves them to the local environment—for example, C:\MININT\SMSOSD\OSDLogs\Variables.dat. This script can be useful in capturing static IP settings for a large number of computers for automation.                                |
| /RestoreWithinWinPE |                                                                                                                      When specified, applies any saved static IP network settings to the local computer, when appropriate; used for internal processing only.                                                                                                                      |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**DeployDrive**|-|-|
|**DeploymentMethod**|-||
|**DeploymentType**|-||
|**DeployRoot**|-||
|**OSDAdapterCount**|-|-|
|**OSGuid**|-||
|**OSDMigrateAdapterSettings**|-||
|**Phase**|-||

## ZTINICUtility.vbs

This script contains network adapter-related functions and subroutines that the various scripts in the MDT deployment process call.

|**Value**|**Description**|
|-|-|
|**Input**|None|
|**Output**|None|
|**References**|-                          **CMD.exe**. Allows running of command-line tools<br><br> -                          **Netsh.exe**. A utility used to automate the configuration of networking components|
|**Location**|*distribution*\Scripts|
|**Use**|`<script language="VBScript" src="ZTINicUtility.vbs"/>`|

### Arguments

|**Value**|**Description**|
|-|-|
|None|None|

### Properties

|                **Name**                 | **Read** | **Write** |
|-----------------------------------------|----------|-----------|
| **OSDAdapter*AdapterIndexAdapterName*** |    -     |     -     |

> [!NOTE]
>
> *AdapterIndex*in this property is a placeholder for a zero-based array that contains network adapter information.

## ZTIOSRole.wsf

This script installs server roles for target computers that are running Windows operating systems. The script reads the **OSRoles**, **OSRoleServices**, and **OSFeatures** properties to determine what should be installed.

> [!NOTE]
>
> This script is intended to be called only by the **Install Roles and Features** and**Uninstall Roles and Features** task sequence steps. Calling this script directly is not supported.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **ZTIOSRole.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|-                          **CMD.exe**. Allows running of command-line tools<br><br> -                          **OCSetup.exe**. Adds to or removes Windows optional components<br><br> -                          **ServerManagerCmd.exe**. Installs, configures, and manages Windows Server roles and features<br><br> -                          **Sysocmgr.exe**. Adds or removes Windows components<br><br> -                          **ZTIUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript ZTIOSRole.wsf </debug:value>`|

### Arguments

|     **Value**      |                                                                                                                                                                                  **Description**                                                                                                                                                                                   |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/debug:*value*** | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (This is the behavior when the argument is not provided.) |
|   **/Uninstall**   |                                                                                                        If provided, this argument indicates that the roles and features will be uninstalled. If not provided, the script assumes the roles and features will be installed.                                                                                                         |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**IsServerCoreOS**|-||
|**OSFeatures**|-||
|**OSRoles**|-||
|**OSRoleServices**|-||
|**OSVersion**|-||
|**SMSTSRebootRequested**||-|

## ZTIPatches.wsf

This script installs updates (language packs, security updates, and so on) that are listed in the Packages.xml file. The script self-terminates if the deployment is not in one of the following states:

- **Phase** equals **PREINSTALL**

- **DeploymentMethod** equals **SCCM**

  The script starts Pkgmgr if **DeploymentMethod** equals **SCCM**.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **ZTIPatches.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|-                          **Expand.exe**. Expands compressed files<br><br> -                          **Pkgmgr.exe**. Installs or updates Windows Vista offline<br><br> -                          **ZTIConfigFile.vbs**. Includes routines for processing XML files<br><br> -                          **ZTIUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript ZTIPatches.wsf </debug:value>`|

### Arguments

|     **Value**      |                                                                                                                                                                                  **Description**                                                                                                                                                                                   |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/debug:*value*** | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (This is the behavior when the argument is not provided.) |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**Architecture**|-||
|**CustomPackageSelectionProfile**|-||
|**DeployRoot**|-||
|**DeploymentMethod**|-||
|**DeploymentType**|-||
|**DestinationLogicalDrive**|-||
|**LanguagePacks**|-||
|**OSDAnswerFilePath**|-||
|**OSDPlatformArch**|-||
|**PackageSelectionProfile**|-||
|**Phase**|-||
|**ResourceRoot**|-||

## ZTIPowerShell.wsf

This script runs a Windows PowerShell script using a custom Windows PowerShell host.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **ZTIPowerShell.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate<br><br> -                          **Return code**. The numeric value returned by the Windows PowerShell script after completion, which indicates the completion status of the script.|
|**References**|-                          **Microsoft.BDD.TaskSequencePSHost.exe**. Custom Windows PowerShell host used to run the Windows PowerShell script.|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript ZTIPowerShell.wsf`|

### Arguments

|**Value**|**Description**|
|-|-|
|**None**||

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**None**|||

## ZTIPrereq.vbs

This script verifies that the target computer has the prerequisite software installed and that it is functional. The checks the script performs are:

- Determine whether the Windows Script version is equal to or greater than version 5.6.

- Verify that errors do not occur when object references are instantiated to Wscript.Shell, Wscript.Network, Scripting.FileSystemObject MSXML2.DOMDocument, and the Process environment.

  If any one of the checks fails, an error is raised and the script exits the **ValidatePrereq** procedure.

|**Value**|**Description**|
|-|-|
|**Input**|None|
|**Output**|None|
|**References**|None|
|**Location**|*distribution*\Scripts|
|**Use**|`None`|

### Arguments

|**Value**|**Description**|
|-|-|
|None|None|

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|None|||

## ZTISCCM.wsf

This script initializes ZTI when deploying using Configuration Manager. The script performs the following procedure:

1. If debugging is activated, the script creates the OSD.Debug file.

2. The script configures these properties:

   - **ScriptRoot**is set to the parent folder of the currently running script.

   - **DeployRoot** is set to the parent folder of **ScriptRoot**.

   - **ResourceRoot** is set to **DeployRoot**.

   - **DeploySystemDrive** is set to **C:**.

   - **DeploymentMethod** is set to **SCCM**.

3. When **DeployRoot**contains **:\\***:*

   - The **DeployRoot** folder is copied to **_SMSTSMDataPath**\WDPackage

   - **ScriptRoot** is set to **_SMSTSMDataPath**\WDPackage\Scripts

   - **DeployRoot** is set to the parent folder of **ScriptRoot**

   - **ResourceRoot** is set to **DeployRoot**

4. When **Phase** is **NULL**:

   - If the %SystemDrive% environment variable is **X:**, then **DeploymentType**is set to **NEWCOMPUTER** and **Phase** is set to **PREINSTALL**. Otherwise,**DeploymentType** is set to **REPLACE** and **Phase** is set to **VALIDATION**.

   - If the **OldComputer**.tag file exists in the parent folder of the current running script, **DeploymentType** is set to **REPLACE** and **Phase** is set to **VALIDATION**. Otherwise,**DeploymentType** is set to **REFRESH** and **Phase** is set to **VALIDATION**.

   For more information about these properties, see the [Properties](task-sequence-steps.md) article.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **ZTISCCM.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|**ZTIUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript ZTISCCM.wsf </debug:value>`|

### Arguments

|     **Value**      |                                                                                                                                                                                  **Description**                                                                                                                                                                                   |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/debug:*value*** | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (This is the behavior when the argument is not provided.) |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**_SMSTSMDataPath**|-||
|**Architecture**|-||
|**BDDPackageID**|-|-|
|**DeploymentMethod**|-|-|
|**DeploymentType**|-|-|
|**DeployRoot**|-|-|
|**Phase**|-|-|
|**ResourceRoot**|-|-|
|**ScriptRoot**|-|-|
|**ToolRoot**|-|-|

## ZTISetVariable.wsf

This script sets the specified global task sequence variable that corresponds to the name contained in **VariableName** to the value contained in **VariableValue**.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **ZTISetVariable.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|**ZTIUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript ZTISetVariable.wsf </debug:value>`|

### Arguments

|     **Value**      |                                                                                                                                                                                  **Description**                                                                                                                                                                                   |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/debug:*value*** | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (This is the behavior when the argument is not provided.) |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**VariableName**|-||
|**VariableValue**|-||

## ZTITatoo.wsf

This script tattoos the target computer with identification and version information. The script performs the following procedure:

1. Locate and copy the ZTITatoo.mof file to the %SystemRoot%\System32\Wbem folder. Any preexisting ZTITatoo.mof that exists at the destination will be deleted before starting the copy operation.

2. Mofcomp.exe will be run using the following command:

   ```exe
   %SystemRoot%\System32\Wbem\Mofcomp.exe -autorecover %SystemRoot%\System32\Wbem\ZTITatoo.mof.
   ```

3. For all deployment methods (LTI, ZTI, and UDI), these deployment details are written for all deployment methods to the registry at **HKEY_LOCAL_MACHINE\Software\Microsoft\Deployment 4**:

   - **Deployment Method** is set to the deployment method being used and can be set to **LTI**, **ZTI**, or **UDI**, depending on the deployment method being performed.

   - **Deployment Source** is set to the source for the deployment and can be set to **OEM**, **MEDIA**, or the value in the **DeploymentMethod** property.

   - **Deployment Type** is set to the **DeploymentType** property.

   - **Deployment Timestamp** is set to the current date in WMI date format.

   - **Deployment Toolkit Version** is set to the **Version** property.

4. For LTI deployments, these deployment details are written  to the registry at **HKEY_LOCAL_MACHINE\Software\Microsoft\Deployment 4**:

   - **Task Sequence ID** is set to the **TaskSequenceID**property.

   - **Task Sequence Name** is set to the **TaskSequenceName** property.

   - **Task Sequence Version** is set to the **TaskSequenceVersion** property.

5. For all Configuration Manager deployments (ZTI and UDI for Configuration Manager), these deployment details are written to the registry at **HKEY_LOCAL_MACHINE\Software\Microsoft\Deployment 4**:

   - OSD Package ID is set to the **_SMSTSPackageID** task sequence variable.

   - **OSD Program Name** is always set to "**\\***".

   - **OSD Advertisement ID** is set to the **_SMSTSAdvertID** task sequence variable.

6. For LTI deployments where an image is being captured, these deployment details are written to the registry at **HKEY_LOCAL_MACHINE\Software\Microsoft\Deployment 4**:

   - **Capture Method** is set to the deployment method being used and can be set to **LTI**, **ZTI**, or **UDI**, depending on the deployment method being performed.

   - **Capture Timestamp** is set to the current date in WMI date format.

   - **Capture Toolkit Version** is set to the **Version** property.

   - **Capture Task Sequence ID** is set to the **TaskSequenceID**property.

   - **Capture Task Sequence Name** is set to the **TaskSequenceName** property.

   - **Capture Task Sequence Version** is set to the **TaskSequenceVersion** property.

7. For all Configuration Manager deployments (ZTI and UDI for Configuration Manager) in which an image is being captured, these deployment details are written to the registry at **HKEY_LOCAL_MACHINE\Software\Microsoft\Deployment 4**:

   - **Capture OSD Package ID** is set to the **_SMSTSPackageID** task sequence variable.

   - **Capture OSD Program Name** is always set to "*****".

   - **Capture OSD Advertisement ID** is set to the **_SMSTSAdvertID**task sequence variable.

   > [!NOTE]
   >  This script is not designed to run on Windows PE.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **ZTITatoo.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|-                          **Mofcomp.exe**. Command-line .mof file compiler<br><br> -                          **ZTIUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript ZTITatoo.wsf </debug:value>`|

### Arguments

|     **Value**      |                                                                                                                                                                                  **Description**                                                                                                                                                                                   |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/debug:*value*** | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (This is the behavior when the argument is not provided.) |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**_SMSTSAdvertID**|-||
|**_SMSTSPackageID**|-||
|**_SMSTSSiteCode**|-||
|**DeploymentMethod**|-||
|**DeploymentType**|-||
|**Version**|-||
|**TaskSequenceID**|-||
|**TaskSequenceName**|-||
|**TaskSequenceVersion**|-||

## ZTIUserState.wsf

This script initializes USMT to capture and restore user state on the target computer.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **ZTIUserState.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|-                          **CMD.exe**. Allows running of command-line tools<br><br> -                          **Loadstate.exe**. Deposits user state data on a target computer<br><br> -                          **Msiexec.exe**. Manages the installation of .msi-based applications<br><br> -                          **Scanstate.exe**. Collects user data and settings<br><br> -                          **USMT Application Files**<br><br> -                          **ZTIUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript ZTIUserState.wsf </debug:value>`|

### Arguments

|**Value**|**Description**|
|-|-|
|/debug:value|Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (This is the behavior when the argument is not provided.)|
|**/Capture**|-|
|**/Estimate**|-|
|**/Restore**|-|

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**Architecture**|-||
|**DeploymentMethod**|-||
|**DeploymentType**|-||
|**DestinationLogicalDrive**|-||
|**ImageBuild**|-||
|**ImageSize**|-||
|**ImageSizeMultiplier**|-||
|**InstallFromPath**|-||
|**IsServerOS**|-||
|**LoadStateArgs**|-||
|**OSCurrentVersion**|-||
|**OSDMigrateAdditionalCaptureOptions**|-|-|
|**OSDMigrateAdditionalRestoreOptions**|-|-|
|**OSDPackagePath**|-||
|**OSDStateStorePath**||-|
|**OSVersion**|-||
|**ScanStateArgs**|-||
|**StatePath**|-|-|
|**UDDir**|-||
|**UDProfiles**|-||
|**UDShare**|-||
|**UserDataLocation**|-|-|
|**USMTConfigFile**|-||
|**USMTEstimate**|-|-|
|**USMTLocal**||-|
|**USMTMigFiles**|-||

## ZTIUtility.vbs

This script contains utility functions that most of the MDT scripts use.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|None|
|**References**|-                          **Credentials_ENU.xml**. Prompts the user for credentials that will be used when connecting to network resources<br><br> -                          **IPConfig.exe**. Displays all current TCP/IP network configuration values and refreshes DHCP and DNS settings<br><br> -                          **MSHTA.exe**. HTML application host<br><br> -                          **Regsvr32.exe**. Registers files (.dll, .exe, .ocx, and so on) with the operating system<br><br> -                          **Xcopy.exe**. Copies files and directories, including subdirectories|
|**Location**|-                          *distribution*\Scripts<br><br> -                          *program_files*\Microsoft Deployment Toolkit\Scripts|
|**Use**|`<script language="VBScript" src="ZTIUtility.vbs"/>`|

### Arguments

|**Value**|**Description**|
|-|-|
|None|None|

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**_SMSTSAdvertID**|-||
|**_SMSTSCurrentActionName**|-||
|**_SMSTSCustomProgressDialogMessage**|-||
|**_SMSTSInstructionTableSize**|-||
|**_SMSTSLogPath**|-||
|**_SMSTSMachineName**|-||
|**_SMSTSNextInstructionPointer**|-||
|**_SMSTSOrgName**|-||
|**_SMSTSPackageID**|-||
|**_SMSTSPackageName**|-||
|**_SMSTSPackagePath**|-||
|**_SMSTSReserved1**|-||
|**_SMSTSReserved2**|-||
|**Architecture**|-||
|**AssetTag**|-||
|**ComputerName**|-||
|**Debug**|-|-|
|**DeploymentMethod**|-||
|**DeployRoot**|-||
|**DestinationDisk**|-|-|
|**DestinationLogicalDrive**|-|-|
|**DestinationPartition**|-|-|
|**EventShare**|-||
|**HostName**|-||
|**ImageBuild**|-|-|
|**ImageFlags**||-|
|**ImageIndex**||-|
|**ImageLanguage**||-|
|**ImageProcessor**||-|
|**ImageSize**||-|
|**InstallFromPath**||-|
|**JoinDomain**|-||
|**LogPath**|-|-|
|**MacAddress**|-||
|**OSCurrentVersion**|-||
|**OSDAdvertID**|-||
|**OSDAnswerFilePath**|-|-|
|**OSDAnswerFilePathSysprep**|-|-|
|**OSDComputerName**|-|-|
|**OSDPackageID**|-||
|**OSDPackagePath**|-||
|**OSDTargetSystemDrive**|-||
|**OSGUID**||-|
|**OSSKU**|-||
|**OSVersion**|-||
|**Phase**|-||
|**Processor_Architecture**|-||
|**ResourceRoot**|-||
|**SLShare**|-||
|**SLShareDynamicLogging**|-||
|**TaskSequenceID**|-||
|**TaskSequenceName**||-|
|**TaskSequenceVersion**||-|
|**UDDir**|-||
|**UDShare**|-||
|**UserDomain**|-|-|
|**UserID**|-|-|
|**UserPassword**|-|-|
|**UUID**|-||
|**Version**<br><br> **Note:** This variable is an internal variable that represents the version of MDT.|-|-|
|**WDSServer**|-||

## ZTIValidate.wsf

This script ensures that it is safe for the deployment to continue by validating the condition of the target computer. The script processes are:

- If **DeploymentType** equals REFRESH and the target computer is a server, the script exits.

- If **OSInstall** exists and is not equal to YES, the script exits.

- Verify that the minimum amount of RAM exists on the target computer; if not, the script exits.

- Verify that the processor meets the minimum required speed; if not, the script exits.

- Verify that the hard disk size meets the minimum size requirements; if not, the script exits.

- Verify that the target computer's operating system is installed on drive C; if not, the script exits.

- If **DeploymentType = REFRESH**, verify that drive C is not compressed by running `Compact /u C:\`.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **ZTIValidate.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|-                          **Compact.exe**. Displays or alters the compression of files on NTFS file system partitions<br><br> -                          **ZTIUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript ZTIValidate.wsf </debug:value>`|

### Arguments

|     **Value**      |                                                                                                                                                                                  **Description**                                                                                                                                                                                   |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/debug:*value*** | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (This is the behavior when the argument is not provided.) |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**DeploymentType**|-||
|**DestinationLogicalDrive**|-|-|
|**ImageBuild**|-||
|**ImageMemory**|-||
|**ImageProcessorSpeed**|-||
|**ImageSize**|-||
|**ImageSizeMultiplier**|-||
|**IsServerOS**|-||
|**Memory**|-||
|**OSDPackagePath**|-||
|**OSInstall**|-||
|**ProcessorSpeed**|-||
|**SMSTSLocalDataDrive**||-|
|**VerifyOS**|-||

## ZTIVHDCreate.wsf

This script is used to create a virtual hard disk (.vhd or .avhd) file on the target computer and mount the .vhd file as a disk. Then, other portions of the LTI deployment process deploy the Windows operating system and applications to the newly created virtual hard disk. The script processes are as follows:

- The **Class_Initialize** method is used to initialize the **VHDInputVariable** variable.

- Validate that **VHDCreateSource** is defined and locates the source .vhd file (if specified).

- Generate a random .vhd file name if **VHDCreateFilename** equals RANDOM or "" (null).

- Verify that the folder exists where the .vhd file (specified in **VHDCreateFileName**) is to be created.

- Create the .vhd file using the values in **VHDCreateSizePercent**, **VHDCreateSizeMax**, and **VHDCreateType**.

- Create a differencing disk (if specified) using the value in **VHDCreateDiffVHD**.

- The newly created .vhd file and the optional differencing disk are mounted.

- The disk number of the mounted virtual hard disk is returned.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **ZTIVHDCreate.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|-                          **ZTIDiskUtility.vbs**. Includes support functions and subroutines the script uses<br><br> -                          **ZTIUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript ZTIVHDCreate.wsf </debug:value>`|

### Arguments

|     **Value**      |                                                                                                                                                                                  **Description**                                                                                                                                                                                   |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/debug:*value*** | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (This is the behavior when the argument is not provided.) |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**VHDCreateDiffVHD**|-||
|**VHDCreateFileName**|-||
|**VHDCreateSizeMax**|-||
|**VHDCreateSource**|-||
|**VHDCreateType**|-||
|**VHDDisks**||-|
|**VHDInputVariable**|-||
|**VHDOutputVariable**|-||

## ZTIWindowsUpdate.wsf

This script downloads and installs updates from computers on a corporate network that are running WSUS, Windows Update, or Microsoft Update using the [Windows Update Agent (WUA)](/windows/win32/wua_sdk/portal-client) application programming interface (API). By default, this feature is disabled in each task sequence and must be manually activated to run.

 Most enterprises will already have teams and infrastructures in place to update newly deployed computers over the corporate network. This process involves tracking the latest set of patches, drivers, and updates available for each desktop configuration and determining which updates should be downloaded and installed for each configuration. If the organization already has an established process, this script might not be necessary. This script was designed to fill a need for deployment teams that might not have established processes, yet want to ensure that target computers are updated when deployed.

 This script automatically scans the target computer and downloads a wide range of updates that are found to be applicable. Among these are:

- Windows service packs

- Non-Microsoft drivers that were placed on Windows Update

- The latest hotfix updates

- Microsoft Office updates

- Microsoft Exchange Server and SQL Server updates

- Microsoft Visual Studio&reg; updates

- Some non-Microsoft application updates

> [!TIP]
>
> Many hardware manufacturers have placed their drivers on Windows Update. These drivers no longer need to be maintained in the Out-of-Box Drivers directory. Experiment by removing drivers from the distribution share to see which ones are available on Windows Update. Note that if the drivers are not included with Windows by default, do not remove networking or storage drivers, because the operating system will require user input.

 MDT supports the ability to deploy an updated version of WUA as part of the operating system deployment. This helps ensure that target computers are running the correct version of WUA when they are deployed. It also helps eliminate the need to connect to the Internet and download the latest version of WUA after deployment.

 MDT can also configure WUA to collect updates from computers on the corporate network that are running WSUS instead of connecting to Microsoft Updates over the Internet. MDT can optionally configure WUA to use a specific computer running WSUS using the **WSUSServer** property.

 For additional information and for WUA deployment instructions, see [How to Install the Windows Update Agent on Client Computers](https://techcommunity.microsoft.com/t5/configuration-manager-archive/how-to-install-the-windows-update-agent-on-client-computers/ba-p/273422).

 Obtain the latest version of the WUA stand-alone installer for:

- x86 versions (WindowsUpdateAgent30-x86.exe) at [https://go.microsoft.com/fwlink/?LinkID=100334](https://go.microsoft.com/fwlink/?LinkID=100334)

- x64 version (WindowsUpdateAgent30-x64.exe) at [https://go.microsoft.com/fwlink/?LinkID=100335](https://go.microsoft.com/fwlink/?LinkID=100335)

  Windows 7 and later include the most recent version of WUA, so no upgrade is necessary.

  For more information, see [Updating Windows Update Agent](/windows/win32/wua_sdk/updating-the-windows-update-agent).

  When enabled in the Task Sequencer, this script runs multiple times while in the State Restore Phase of operating system deployment. It is first run after the operating system has started for the first time. Ensure that the latest updates and service packs are installed before the installation of any applications that might depend on specific updates or service packs being installed on the target computer. For example, an application might be dependent on the latest version of the Microsoft .NET Framework being installed.

  This script also runs after the installation of applications, which ensures that the latest application service packs and updates have been applied. For example, use this script to ensure that the latest updates are applied to Microsoft Office 2010 or the 2007 Office system.

  It is possible, during the installation of one or more updates, the target computer will need to be restarted to allow an update installation to finish fully. To ensure that updates are properly installed, if the script detects that the installation of an update requires the target computer to be restarted, the script automatically restarts the target computer and resumes if additional updates have been detected and are pending installation. The script exits if it determines that the target computer is fully up to date. An error will be logged if, while updating the target computer, the script has seven unsuccessful attempts to install the updates and the target computer still requires a restart.

  During run time, the script performs the following tasks:

- Configure the target computer to use a WSUS server, if the **WSUSServer** property was specified.

- Verify that the latest version of the WUA is installed on the target computer.

- Search the target computer for applicable updates that are not already installed and that might be typically hidden.

- Each update has an associated **UpdateID** and **QNumber** property:

  -   The **UpdateID** property is in GUID form, such as *67da2176-5c57-4614-a514-33abbdd51f67*.

  -   The **QNumber** property is a numerical value, such as *987654*.

- The script compares the **UpdateID** and **KBArticle** property values against the list of exclusions specified in the following MDT properties:

  -   **WUMU_ExcludeID**. A list of UpdateIDs to exclude; any update with an **UpdateID** found in this list will not be installed.

  -   **WUMU_ExcludeKB**. A list of **QNumbers** to exclude; any update with a **QNumber** found in this list will not be installed.

  -   In addition, any update that requires user input will be excluded and not installed.

- All updates that require approval of an End User License Agreement (EULA) will automatically be approved by the script. Be sure to manually read and check each EULA before running this script in a production environment.

- The activity for each update is written to the ZTIWindowsUpdate.log file, with the string INSTALL or SKIP if the update has been approved for installation, along with the UpdateID, a short description of the update, and the QNumber.

- Each update to be installed is downloaded and installed in batches.

- The target computer might require more than one restart during the update installation.

> [!NOTE]
>
> Windows Internet Explorer 7 requires user interaction, so it is not installed using this script.

> [!NOTE]
>
> By default, include **QNumber 925471** in the **WUMU_ExcludeKB** list to prevent Windows Vista Ultimate from installing extra language packs.

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **ZTIWindowsUpdate.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|-                          **Expand.exe**. Expands compressed files<br><br> -                          **Net.exe**. Performs network management tasks<br><br> -                          **WindowsUpdateAgent30-x86.exe**. Installs WUA<br><br> -                          **WindowsUpdateAgent30-x64.exe**. Installs WUA<br><br> -                          **ZTIUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript ZTIWindowsUpdate.wsf </debug:value> </UpdateCommand:"<IsInstalled=0&#124;1> <IsHidden=0&#124;1>"> </Query:true&#124;false>`|

### Arguments

|         **Value**          |                                                                                                                                                                                  **Description**                                                                                                                                                                                   |
|----------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     **/debug:*value***     | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (This is the behavior when the argument is not provided.) |
| **/UpdateCommand:*param*** |                                                     -                              **IsInstalled**. Set to **0** to query for updates that are not installed.<br><br> -                              **IsHidden**. Set to **0** to query for updates that are hidden.                                                      |
|     **/Query:*value***     |                                                     -                              **True**. Query only for required updates. Do not download and install any binaries.<br><br> -                              **False**. Query for and install required updates. Download and install binaries.                                                     |

> [!NOTE]
>
> When specified, **UpdateCommand** requires at least one option.

> [!NOTE]
>
> If specifying both options for **UpdateCommand**, they must be separated by *and*.

> [!NOTE]
>
> The default value for **UpdateCommand** is **IsInstalled=0** and **IsHidden=0**.

> [!NOTE]
>
> For more information about **UpdateCommand**, see [IUpdateSearcher::Search Method](https://msdn.microsoft.com/library/aa386526\(VS.85\).aspx).

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**Architecture**|-||
|**DoCapture**|-||
|**InstalledUpdates**||-|
|**MSIT_WU_Count**|-|-|
|**NoAutoUpdate_Previous**|-|-|
|**SMSTSRebootRequested**|-|-|
|**SMSTSRetryRequested**|-|-|
|**WSUSServer**|-||
|**WUMU_ExcludeID**|-||
|**WUMU_ExcludeKB**|-||

## ZTIWipeDisk.wsf

This script formats the target computer's hard disk. The script:

- Exits if **WipeDisk** is not equal to **TRUE**

- Determines the appropriate drive to format

- Formats the drive by calling `cmd /c format <Drive> /fs:ntfs /p:3 /Y` (where `<Drive>` is the drive letter of the hard disk drive to be formatted)

|**Value**|**Description**|
|-|-|
|**Input**|**Environment variables**. Contains the property values, custom property values, database connections, deployment rules, and other information that the scripts require to complete the deployment process|
|**Output**|-                          **ZTIWipeDisk.log**. Log file that contains events that this script generates<br><br> -                          **BDD.log**. Log file that contains events that all MDT scripts generate|
|**References**|-                          **CMD.exe**. Allows running of command-line tools<br><br> -                          **Format.com**. Formats the hard disk<br><br> -                          **ZTIUtility.vbs**. Includes support functions and subroutines that the script uses|
|**Location**|*distribution*\Scripts|
|**Use**|`cscript ZTIWipeDisk.wsf </debug:value>`|

### Arguments

|     **Value**      |                                                                                                                                                                                  **Description**                                                                                                                                                                                   |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **/debug:*value*** | Outputs the event messages to the console and to the .log files. If the value specified in value is:<br><br> -                              **TRUE**, event messages are sent to the console and the .log files<br><br> -                              **FALSE**, event messages are sent only to the .log files (This is the behavior when the argument is not provided.) |

### Properties

|**Name**|**Read**|**Write**|
|-|-|-|
|**WipeDisk**|-||

## Related articles

- [Task Sequence Steps](task-sequence-steps.md).
- [Properties](properties.md).
- [Support Files](support-files.md).
- [Utilities](utilities.md).
- [MDT Windows PowerShell Cmdlets](mdt-windows-powershell-cmdlets.md).
- [Tables and Views in the MDT DB](tables-views-mdt-db.md).
- [Windows 7 Feature Dependency Reference](windows-7-feature-dependency.md).
- [UDI Reference](udi-reference.md).