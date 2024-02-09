---
title: Toolkit reference - Microsoft Deployment Toolkit (MDT) Properties
titleSuffix: Microsoft Deployment Toolkit
description: Reference details for Microsoft Deployment Toolkit (MDT) Properties
ms.date: 09/09/2016
ms.subservice: mdt
ms.service: configuration-manager
ms.topic: article
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz
---

# Properties
 The scripts used in Lite Touch Installation (LTI) and ZTI reference properties to determine the process steps and configuration settings used during the deployment process. The scripts create some of these properties automatically. Other properties must be configured in the CustomSettings.ini file. Some of these properties are:

- Specific to ZTI only

- Specific to LTI only

- For use in both ZTI and LTI

  Use this reference to help determine the correct properties to configure and the valid values to include for each property.

  For each property the following information is provided:

- **Description**.Provides a description of the purpose of the property and any pertinent information regarding the customization of the property.

  > [!NOTE]
  >  Unless explicitly specified for ZTI or LTI only, a property is valid for both ZTI and LTI.

- **Value and Description**.Indicates the valid values to be specified for the property and a brief description of what each value means. (Values in italics indicate that a value is substituted—for example the value *user1*, *user2* indicates that *user1* and *user2* would be replaced with the actual name of user accounts.)

- **Example**.Provides an example of a property use as it might appear in the .ini files.

  For more information about these and other task sequence properties that might be referenced while performing a ZTI deployment, see [Operating System Deployment Task Sequence Variables](../develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md).

  The deployment scripts generally require values to be specified in upper case so that they are properly read. Therefore, when specifying property values, use uppercase letters.

## Property Definition
 The following sections describe the properties that are available for LTI and ZTI deployments in MDT.

> [!TIP]
>  The properties are sorted in alphabetical order.

###  <a name="\_SMSTSOrgName"></a> \_SMSTSOrgName
 Customizes the Task Sequencer engine's display banner

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*name*|The name that will be used in the Task Sequencer engine's display banner|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] _SMSTSOrgName=Woodgrove Bank`|

###  <a name="ADDSLogPath"></a> ADDSLogPath
 Fully qualified, non-UNC directory on a hard disk on the local computer to host the AD DS log files. If the directory exists it must be empty. If it does not exist, it will be created.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*log_path*|Fully qualified, non-UNC directory on a hard disk on the local computer to host the AD DS log files|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] ADDSLogPath=%DestinationLogicalDrive%\Windows\NTDS`|

###  <a name="ADDSPassword"></a> ADDSPassword
 Account credentials that can be used when promoting the server to a domain controller.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*password*|Account credentials that can be used for the promotion operation|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] ADDSUserName=Administrator ADDSUserDomain=WoodGroveBank ADDSPassword=<complex_password>`|

###  <a name="ADDSUserDomain"></a> ADDSUserDomain
 This is the domain the account specified by **ADDSUserName** should be taken from. If the operation is to create a new forest or to become a member server from a backup domain controller upgrade there is no default. If the operation is to create a new tree, the default is the DNS name of the forest the computer is currently joined to. If the operation is to create a new child domain or a replica then the default is the DNS name of the domain the computer is joined to. If the operation is to demote the computer and the computer is a domain controller in a child domain, the default is the DNS name of the parent domains. If the operation is to demote the computer, and the computer is a domain controller of a tree root domain, the default is the DNS name of the forest.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*domain*|Domain the UserName account should be taken from|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] ADDSUserName=Administrator ADDSUserDomain=WoodGroveBank ADDSPassword=<complex_password>`|

###  <a name="ADDSUserName"></a> ADDSUserName
 Account credentials that will be used when promoting the server to a domain controller.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*user_name*|Account credentials that will be used for the promotion operation|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] ADDSUserName=Administrator ADDSUserDomain=WoodGroveBank ADDSPassword=complex_password`|

###  <a name="Administrators"></a> Administrators
 A list of user accounts and domain groups that will be added to the local Administrator group on the target computer. The **Administrators** property is a list of text values that can be any non-blank value. The **Administrators** property has a numeric suffix (for example, **Administrators001** or **Administrators002**).

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*name*|The name of a user or group that is to be added to the local Administrator group|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] Administrators001=WOODGROVEBANK\NYC Help Desk Staff Administrators002=WOODGROVEBANK\North America East Help Desk Staff PowerUsers001=WOODGROVEBANK\User01 PowerUsers002=WOODGROVEBANK\User02`|

###  <a name="AdminPassword"></a> AdminPassword
 Defines the password that will be assigned to the local Administrator user account on the target computer. If not specified, the pre-deployment password of the Administrator user account will be used.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*admin_password*|The password that is to be assigned to the Administrator user account on the target computer|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] Administrators001=WOODGROVEBANK\NYC Help Desk Staff AdminPassword=<admin_password>`|

###  <a name="Applications"></a> Applications
 A list of application GUIDs that should be installed on the target computer. These applications are specified on the Applications node in Deployment Workbench. These GUIDs are stored in the Applications.xml file. The **Applications** property is a list of text values that can be any non-blank value. The **Applications** property has a numeric suffix (for example, **Applications001** or **Applications002**).

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*application_guid*|The GUID is specified by Deployment Workbench for the application to be deployed to the target computer. The GUID corresponds to the application GUID stored in the Applications.xml file.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] Applications001={1D7DF331-47B7-472C-87B3-442597EC2F7D} Applications002={9d2b8999-5e4d-4f3d-bb05-edaaf4fe5628}`|

###  <a name="ApplicationSuccessCodes"></a> ApplicationSuccessCodes
 A space-delimited list of error codes used by the ZTIApplications script that determine the successful installation of applications.

> [!NOTE]
>  This property is only applicable to the **Install Application** task sequence step type and when **Install multiple applications** is selected.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*error_codes*|The error codes that determine when applications have been successfully installed. Default values are **0** and **3010**.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] ApplicationSuccessCodes=0 3010`|

###  <a name="ApplyGPOPack"></a> ApplyGPOPack
 This property is used to determine whether the **Apply Local GPO Package** task sequence step is performed.

> [!NOTE]
>  The default value for this property always performs the **Apply Local GPO Package** task sequence step. You must explicitly provide a value of "NO" to override this behavior..

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**YES**|The **Apply Local GPO Package** task sequence step is performed. This is the default value.|
|**NO**|The **Apply Local GPO Package** task sequence step is not performed.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] ApplyGPOPack=NO`|

###  <a name="Architecture"></a> Architecture
 The processor architecture of the processor that is currently running, which is not necessarily the processor architecture supported by the target computer. For example, when running a 32-bit–compatible operating system on a 64-bit processor, **Architecture** will indicate that the processor architecture is 32 bit.

 Use the **CapableArchitecture** property to identify the actual processor architecture that the target computer supports.

> [!NOTE]
>  This property is dynamically set by MDT scripts and is not configured in CustomSettings.ini. Treat this property as read only. However, you can use this property within CustomSettings.ini, as shown in the following examples, to aid in defining the configuration of the target computer.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**x86**|Processor architecture is 32 bit.|
|**x64**|Processor architecture is 64 bit.|

|**Example**|
|-|
|None|

###  <a name="AreaCode"></a> AreaCode
 The area code to be configured for the operating system on the target computer. This property allows only numeric characters. This value is inserted into the appropriate configuration settings in Unattend.xml.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*area_code*|The area code where the target computer is to be deployed|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] AreaCode=206 CountryCode=001 Dialing=TONE LongDistanceAccess=9`|

###  <a name="AssetTag"></a> AssetTag
 The asset tag number associated with the target computer. The format for asset tag numbers is undefined. Use this property to create a subsection that contains settings targeted to a specific computer.

> [!NOTE]
>  This property is dynamically set by MDT scripts and cannot have its value set in CustomSettings.ini or the MDT DB. Treat this property as read only. However, you can use this property within CustomSettings.ini or the MDT DB, as shown in the following examples, to aid in defining the configuration of the target computer.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*asset_tag*|The format of the asset tag is undefined and is determined by the asset tag standard of each organization.|

|**Example 1**|
|-|
|`[Settings] Priority=Default  [Default] OSDComputerName=HP-%AssetTag%`|

|**Example 2**|
|-|
|`[Settings] Priority=AssetTag, Default  [Default] OSInstall=YES  [0034034931] OSDComputerName=HPD530-1  [0034003233] OSDNEWMACHINENAME=BVMXP`|

###  <a name="AutoConfigDNS"></a> AutoConfigDNS
 Specifies whether the Active Directory Installation Wizard configures DNS for the new domain if it detects that the DNS dynamic update protocol is not available.

> [!CAUTION]
>  This property value must be specified in uppercase so that the deployment scripts can properly read it.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**YES**|Configures DNS for the new domain if the DNS dynamic update protocol is not available|
|**NO**|Does not configure DNS for the domain|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] AutoConfigDNS=YES`|

###  <a name="BackupDir"></a> BackupDir
 The folder in which backups of the target computer are stored. This folder exists beneath the UNC path specified in the **BackupShare** property. If the folder does not already exist, it will be created automatically.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*Folder*|The name of the folder that exists beneath the shared folder specified in the **BackupShare** property|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DoCapture=YES BackupShare=\\NYC-AM-FIL-01\Backup$ BackupDir=%OSDComputerName% BackupDrive=C:`|

###  <a name="BackupDrive"></a> BackupDrive
 The drive to include in the backup of the target computer. This property defaults to the drive that contains disk 0 partition 1. It can be also set to **ALL**.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*backup_drive*|The drive letter of the drive to back up|
|**ALL**|Back up all drives on the target computer|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DoCapture=YES BackupShare=\\NYC-AM-FIL-01\Backup$ BackupDir=%OSDComputerName% BackupDrive=C:`|

###  <a name="BackupFile"></a> BackupFile
 Specifies the WIM file that will be used by the ZTIBackup.wsf script. For more information about what script uses this property, see [ZTIBackup.wsf](#ZTIBackup.wsf).

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*BackupDir*|The name of the Windows Imaging Format (WIM) file to be used during back up.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DoCapture=YES BackupShare=\\NYC-AM-FIL-01\Backup$ BackupDir=%OSDComputerName% BackupFile=%OSDComputerName%.wim`|

###  <a name="BackupShare"></a> BackupShare
 The shared folder in which backups of the target computer are stored.

 The credentials used to access this shared folder for:

- LTI are the credentials entered in the Deployment Wizard.

- ZTI are the credentials used by the Configuration Manager Advanced Client Network Access account.

  The permissions required on this share are as follows:

- **Domain Computers**. Allow the Create Folders/Append Data permission.

- **Domain Users**. Allow the Create Folders/Append Data permission.

- **Creator Owner**. Allow the Full Control permission.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*UNC_path*|The UNC path of the shared folder<br /><br /> Note:<br /><br /> The UNC path specified in this property must exist before deploying the target operating system.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DoCapture=YES BackupShare=\\NYC-AM-FIL-01\Backup$ BackupDir=%OSDComputerName% BackupDrive=C:`|

###  <a name="BDEAllowAlphaNumericPin"></a> BDEAllowAlphaNumericPin
 This property configures whether BitLocker PINs contain alphanumeric values.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**YES**|Alphanumeric characters are allowed in the PIN.<br /><br /> Note:<br /><br /> In addition to setting this property to **YES**, the **Allow enhanced PINs for startup** group policy setting must be enabled.|
|**NO**|Only numeric characters are allowed in the PIN.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] BDEInstallSuppress=NO BDEAllowAlphaNumericPin=YES BDEDriveLetter=S: BDEDriveSize=2000 BDEInstall=TPMKey BDERecoveryKey=AD BDEKeyLocation=C:`|

###  <a name="BDEDriveLetter"></a> BDEDriveLetter
 The drive letter for the partition that is not encrypted by BitLocker, also known as the *System Volume*. SYSVOL is the directory that contains the hardware-specific files needed to load Windows computers after the BIOS has booted the platform.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*drive_letter*|The letter designation for the logical drive for the System Volume (such as S or T). The default value is **S**.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] BDEInstallSuppress=NO BDEDriveLetter=S: BDEDriveSize=2000 BDEInstall=TPMKey BDERecoveryKey=AD BDEKeyLocation=C:`|

###  <a name="BDEDriveSize"></a> BDEDriveSize
 The size of the BitLocker system partition. The value is specified in megabytes. In the example, the size of the BitLocker partition to create is almost 2 GB (2,000 MB).

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*drive_size*|The size of the partition in megabytes; the default sizes are:<br /><br /> - Windows 7 and Windows Server 2008 R2: 300 MB|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] BDEInstallSuppress=NO BDEDriveLetter=S: BDEDriveSize=2000 BDEInstall=TPMKey BDERecoveryKey=AD BDEKeyLocation=C:`|

###  <a name="BDEInstall"></a> BDEInstall
 The type of BitLocker installation to be performed. Protect the target computer using one of the following methods:

-   A TPM microcontroller

-   A TPM and an external startup key (using a key that is typically stored on a USB flash drive [UFD])

-   A TPM and PIN

-   An external startup key

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TPM**|Protect the computer with TPM only. The TPM is a microcontroller that stores keys, passwords, and digital certificates. The microcontroller is typically an integral part of the computer motherboard.|
|**TPMKey**|Protect the computer with TPM and a startup key. Use this option to create a startup key and to save it on a UFD. The startup key must be present in the port each time the computer starts.|
|**TPMPin**|Protect the computer with TPM and a pin. Use this option in conjunction with the **BDEPin** property.|
|**Key**|Protect the computer with an external key (the recovery key) that can be stored in a folder, in AD DS, or printed.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] BDEInstallSuppress=NO BDEDriveLetter=S: BDEDriveSize=2000 BDEInstall=TPMKey BDERecoveryKey=AD BDEKeyLocation=C:`|

###  <a name="BDEInstallSuppress"></a> BDEInstallSuppress
 Indicates whether the deployment process should skip the BitLocker installation.

> [!CAUTION]
>  This property value must be specified in uppercase so that the deployment scripts can read it properly.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**YES**|Do not attempt to install BitLocker.|
|**NO**|Attempt to install BitLocker.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] BDEInstallSuppress=YES`|

###  <a name="BDEKeyLocation"></a> BDEKeyLocation
 The location for storing the BitLocker recovery key and startup key.

> [!NOTE]
>  If this property is configured using the Deployment Wizard, the property must be the drive letter of a removable disk. If the **SkipBitLocker** property is set to **TRUE** so that the **Specify the BitLocker configuration** wizard page is skipped, this property can be set to a UNC path in CustomSettings.ini or in the MDT database (MDT DB).

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*Location*|Specifies where the recovery key will be stored; must be a UNC path or the drive letter of a removable disk. If not set, the first available removable drive will be used.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] BDEInstallSuppress=NO BDEDriveLetter=S: BDEDriveSize=2000 BDEInstall=TPMKey BDERecoveryKey=AD BDEKeyLocation=C:`|

###  <a name="BDEPin"></a> BDEPin
 The PIN to be assigned to the target computer when configuring BitLocker and the **BDEInstall** or **OSDBitLockerMode** properties are set to **TPMPin**.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*Pin*|The PIN to be used for BitLocker. The PIN can be between 4 and 20 digits long.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] BDEInstallSuppress=NO BDEDriveLetter=S: BDEDriveSize=2000 BDEInstall=TPMPin BDEPin=123456789`|

###  <a name="BDERecoveryKey"></a> BDERecoveryKey
 A Boolean value that indicates whether the process creates a recovery key for BitLocker. The key is used for recovering data encrypted on a BitLocker volume. This key is cryptographically equivalent to a startup key. If available, the recovery key decrypts the volume master key (VMK), which, in turn, decrypts the full volume encryption key (FVEK).

> [!NOTE]
>  The recovery key is stored in the location specified in the **BDEKeyLocation** property.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**AD**|A recovery key is created.|
|Not specified|A recovery key is not created.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] BDEInstallSuppress=NO BDEDriveLetter=S: BDEDriveSize=2000 BDEInstall=TPMKey BDERecoveryKey=AD BDEKeyLocation=C:`|

###  <a name="BDEWaitForEncryption"></a> BDEWaitForEncryption
 Specifies that the deployment process should not proceed until BitLocker has completed the encryption process for all specified drives. Specifying TRUE could dramatically increase the time required to complete the deployment process.

> [!CAUTION]
>  This property value must be specified in uppercase so that the deployment scripts can read it properly.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|Specifies that the deployment process should wait for drive encryption to complete.|
|**FALSE**|Specifies that the deployment process should not wait for drive encryption to complete.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] BDEInstallSuppress=NO BDEDriveLetter=S: BDEDriveSize=2000 OSDBitLockerMode=TPMKey OSDBitLockerStartupKeyDrive=C: OSDBitLockerCreateRecoveryPassword=AD BDEWaitForEncryption=TRUE`|

###  <a name="BitsPerPel"></a> BitsPerPel
 A setting for displaying colors on the target computer. The property can contain numeric digits and corresponds to the color quality setting. In the example, **32** indicates 32 bits per pixel for color quality. This value is inserted into the appropriate configuration settings in Unattend.xml.

> [!NOTE]
>  The default values (in the Unattend.xml template file) are 1,024 pixels horizontal resolution, 768 pixels vertical resolution, 32-bit color depth, and 60 Hertz (Hz) vertical refresh rate.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*bits_per_pixel*|The number of bits per pixel to use for color. The default value is the default for the operating system being deployed.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] BitsPerPel=32 VRefresh=60 XResolution=1024 YResolution=768`|

###  <a name="BuildID"></a> BuildID
 Identifies the operating system task sequence to be deployed to the target computer. You create the task sequence ID on the Task Sequences node in the Deployment Workbench. The **BuildID** property allows alphanumeric characters, hyphens (-), and underscores (\_). The **BuildID** property cannot be blank or contain spaces.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*build_id*|Identifier of the operating system task sequence as defined in the Deployment Workbench for the target operating system being deployed<br /><br /> Note:<br /><br /> Make certain to use the **TaskSequenceID** specified in the Deployment Workbench user interface (UI) and not the GUID of the **TaskSequenceID**.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] BuildID=BareMetal`|

###  <a name="CapableArchitecture"></a> CapableArchitecture
 The processor architecture of the processor supported by the target computer, not the current processor architecture that is running. For example, when running a 32-bit-compatible operating system on a 64-bit processor, **CapableArchitecture** will indicate that the processor architecture is 64 bit.

 Use the **Architecture** property to see the processor architecture that is currently running.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**x86**|Processor architecture is 32 bit.|
|**x64**|Processor architecture is 64 bit.|

|**Example**|
|-|
|None|

###  <a name="CaptureGroups"></a> CaptureGroups
 Controls whether the group membership of local groups on the target computer is captured. This group membership is captured during the State Capture Phase and is restored during the State Restore Phase.

> [!NOTE]
>  This property value must be specified in uppercase so that the deployment scripts can read it properly.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**NO**|Captures no group membership information.|
|**ALL**|Captures the membership of all local groups on the target computer.|
|**YES**|Captures the membership of the Administrator and Power Users built-in groups and the groups listed in the groups' properties. This is the default value if some other value is specified. (**YES** is the typical value.)|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UDShare=\\NYC-AM-FIL-01\MigData$ CaptureGroups=YES Groups1=NYC Application Management Groups2=NYC Help Desk Users`|

###  <a name="ChildName"></a> ChildName
 Specifies whether to append the DNS label at the beginning of the name of an existing directory service domain when installing a child domain.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*name*|The name of the child domain|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] ChildName=childdom.parentdom.WoodGroveBank.com`|

###  <a name="ComputerBackupLocation"></a> ComputerBackupLocation
 The network shared folder where the computer backup is stored. If the target folder does not already exist, it is automatically created.

> [!CAUTION]
>  This property value must be specified in uppercase so that the deployment scripts can read it properly.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*blank*|Same as **AUTO**.|
|*UNC_path*|The UNC path to the network shared folder where the backup is stored.|
|**AUTO**|Creates a backup on a local hard disk if space is available. Otherwise, the backup is saved to a network location specified in the **BackupShare** and **BackupDir** properties.|
|**NETWORK**|Creates a backup on a network location specified in **BackupShare** and **BackupDir**.|
|**NONE**|No backup will be performed.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UDShare=\\NYC-AM-FIL-01\MigData$ ComputerBackupLocation=NETWORK BackupShare=\\NYC-AM-FIL-01\Backup$ BackupDir=%OSDComputerName% UDDir=%OSDComputerName% SLShare=\\NYC-AM-FIL-01\Logs$ UDProfiles=Administrator, User-01, ExtranetUser UserDataLocation=NONE`|

###  <a name="ComputerName"></a> ComputerName
 This property has been deprecated. Use **OSDComputerName** instead.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|None|None|

|**Example**|
|-|
|None|

###  <a name="ConfigFileName"></a> ConfigFileName
 Specifies the name of the configuration file used during OEM deployments.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*file_name*|Specifies the name of the configuration file used during OEM deployments|

|**Example**|
|-|
|None|

###  <a name="ConfigFilePackage"></a> ConfigFilePackage
 Specifies the package ID for the configuration package used during OEM deployments.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*package*|Specifies the package ID for the configuration package used during OEM deployments|

|**Example**|
|-|
|None|

###  <a name="ConfirmGC"></a> ConfirmGC
 Specifies whether the replica is also a global catalog.

> [!CAUTION]
>  This property value must be specified in uppercase so that the deployment scripts can read it properly.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**YES**|Makes the replica a global catalog if the backup was a global catalog.|
|**NO**|Does not make the replica a global catalog.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] ConfirmGC=YES`|

###  <a name="CountryCode"></a> CountryCode
 The country code to be configured for the operating system on the target computer. This property allows only numeric characters. This value is inserted into the appropriate configuration settings in Unattend.xml.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*country_code*|The country code where the target computer is to be deployed|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] AreaCode=206 CountryCode=001 Dialing=TONE LongDistanceAccess=9`|

###  <a name="CriticalReplicationOnly"></a> CriticalReplicationOnly
 Specifies whether the promotion operation performs only critical replication and then continues, skipping the noncritical (and potentially lengthy) portion of replication.

> [!CAUTION]
>  This property value must be specified in uppercase so that the deployment scripts can read it properly.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**YES**|Skips noncritical replication|
|**NO**|Does not skip noncritical replication|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] CriticalReplicationOnly=YES`|

###  <a name="CustomDriverSelectionProfile"></a> CustomDriverSelectionProfile
 Specifies the custom selection profile used during driver installation.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*profile*|Custom selection profile used during driver installation|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] CustomDriverSelectionProfile=CustomDrivers`|

###  <a name="CustomPackageSelectionProfile"></a> CustomPackageSelectionProfile
 Specifies the custom selection profile used during package installation.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*profile*|Custom selection profile used during package installation|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] CustomPackageSelectionProfile=CustomPackages`|

###  <a name="CustomWizardSelectionProfile"></a> CustomWizardSelectionProfile
 Specifies the custom selection profile used by the wizard for filtering the display of various items.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*profile*|Custom selection profile by the wizard for filtering the display of various items|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] CustomWizardSelectionProfile=CustomWizard`|

###  <a name="Database"></a> Database
 The property that specifies the database to be used for querying property values from columns in the table specified in the **Table** property. The database resides on the computer specified in the **SQLServer** property. The instance of Microsoft SQL Server&reg; on the computer is specified in the **Instance** property.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*database*|The name of the database to be used for querying property values|

|**Example**|
|-|
|`[Settings] Priority=Computers, Default  [Default] OSInstall=YES  [Computers] SQLServer=NYC-SQL-01 SQLShare=SQL$ Database=MDTDB Instance=SQLEnterprise2005 Table=Computers Parameters=SerialNumber, AssetTag ParameterCondition=OR`|

###  <a name="DatabasePath"></a> DatabasePath
 Specifies the fully qualified, non\-UNC path to a directory on a fixed disk of the target computer that contains the domain database.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*path*|Specifies the fully qualified, non\-UNC path to a directory on a fixed disk of the local computer that contains the domain database|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DatabasePath=%DestinationLogicalDrive%\Windows\NTSD`|

###  <a name="DBID"></a> DBID
 Specifies the user account used to connect to the computer running SQL Server \(specified by the **SQLServer** property\) using SQL Server authentication. The **DBPwd** property provides the password for the user account in the **DBID** property.

> [!NOTE]
>  SQL Server authentication is not as secure as Integrated Windows authentication. Integrated Windows authentication is the recommended authentication method. Using the **DBID** and **DBPwd** properties stores the credentials in clear text in the CustomSettings.ini file and therefore is not secure. For more information about using Integrated Windows authentication, see the [SQLShare](#SQLShare) property.

> [!NOTE]
>  This property is configurable only by manually editing the CustomSettings.ini and BootStrap.ini files.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*user\_id*|The name of the user account credentials used to access the computer running SQL Server using SQL Server authentication|

|**Example**|
|-|
|`[Settings] Priority=Computers, Default  [Default] OSInstall=YES  [Computers] SQLServer=NYC-SQL-01 DBID=SQL_User-01 DBPwd=<complex_password> NetLib=DBNMPNTW Database=MDTDB Instance=SQLEnterprise2005 Table=Computers Parameters=SerialNumber, AssetTag ParameterCondition=OR`|

###  <a name="DBPwd"></a> DBPwd
 Specifies the password for the user account specified in the **DBID** property. The **DBID** and **DBPwd** properties provide the credentials for performing SQL Server authentication to the computer running SQL Server \(specified by the **SQLServer** property\).

> [!NOTE]
>  SQL Server authentication is not as secure as Integrated Windows authentication. Integrated Windows authentication is the recommended authentication method. Using the **DBID** and **DBPwd** properties stores the credentials in clear text in the CustomSettings.ini file and therefore is not secure. For more information about using Integrated Windows authentication, see the [SQLShare](#SQLShare) property.

> [!NOTE]
>  This property is configurable only by manually editing the CustomSettings.ini and BootStrap.ini files.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*user\_password*|The password for the user account credentials specified in the **DBID** property for using SQL Server authentication|

|**Example**|
|-|
|`[Settings] Priority=Computers, Default  [Default] OSInstall=YES  [Computers] SQLServer=NYC-SQL-01 DBID=SQL_User-01 DBPwd=<complex_password> NetLib=DBNMPNTW Database=MDTDB Instance=SQLEnterprise2005 Table=Computers Parameters=SerialNumber, AssetTag ParameterCondition=OR`|

###  <a name="Debug"></a> Debug
 Controls the verbosity of messages written to the MDT log files. This property can be configured to help assist in troubleshooting deployments by providing extended information about the MDT deployment process.

 You can set this property by starting the LiteTouch.vbs script with the **\/debug:true** command\-line parameter as follows:

```
cscript.exe LiteTouch.vbs /debug:true
```

 After the LiteTouch.vbs script is started, the **Debug** property's value is set to **TRUE**, and all other scripts are automatically read the value of this property and provide verbose information.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or in the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|Debug logging is enabled, which includes the following:<br /><br /> \- Verbose messages are logged.<br /><br /> \- Deprecated messages are logged as errors.|
|**FALSE**|Debug logging is not enabled. This is the default value.|

|**Example**|
|-|
|None|

###  <a name="DefaultGateway"></a> DefaultGateway
 The IP address of the default gateway being used by the target computer. The format of the IP address returned by the property is standard dotted\-decimal notation; for example, 192.168.1.1. Use this property to create a subsection that contains settings targeted to a group of computers based on the IP subnets on which they are located.

> [!NOTE]
>  This property is dynamically set by MDT scripts and cannot have its value set in CustomSettings.ini or the MDT DB. Treat this property as read only. However, you can use this property within CustomSettings.ini or the MDT DB, as shown in the following examples, to aid in defining the configuration of the target computer.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*default\_gateway*|The IP address of the default gateway in standard dotted\-decimal notation|

|**Example**|
|-|
|`[Settings] Priority=DefaultGateway, Default  [Default] OSInstall=YES  [DefaultGateway] 192.168.0.1=HOUSTON 11.1.1.11=REDMOND 172.28.20.1=REDMOND  [REDMOND] Packages001=XXX00004:Program4 Packages002=XXX00005:Program5  [HOUSTON] Packages001=XXX00006:Program6 Packages002=XXX00007:Program7 Packages003=XXX00008:Program8`|

###  <a name="DeployDrive"></a> DeployDrive
 The value used by the scripts to access files and run programs in the deployment share that the Deployment Workbench creates. The property returns the drive letter mapped to the **DeployRoot** property. ZTIApplications.wsf uses the **DeployDrive** property when running any command\-line programs with a .cmd or .bat extension.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*drive\_letter*|The letter designation for the logical drive where the target operating system is to be installed \(such as C or D\)|

|**Example**|
|-|
|None|

###  <a name="DeploymentMethod"></a> DeploymentMethod
 The method being used for the deployment (UNC, media, or Configuration Manager).

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

> [!CAUTION]
>  This property value must be specified in uppercase so that the deployment scripts can read it properly.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**UNC**|The deployment is made to the target computer over the network.|
|**Media**|The deployment is made from local media (such as DVD or hard disk) at the target computer.|
|**SCCM**|ZTI uses this method for Configuration Manager.|

|**Example**|
|-|
|None|

###  <a name="DeploymentType"></a> DeploymentType
 The type of deployment being performed based on the deployment scenario. For ZTI, this property is set dynamically by MDT scripts and is not configured in CustomSettings.ini. For LTI, you can bypass the page in the Deployment Wizard on which the deployment type is selected. In addition, you can specify the deployment type by passing one of the values listed below to the LiteTouch.wsf script as a command-line option.

> [!CAUTION]
>  This property value must be specified in uppercase so that the deployment scripts can read it properly.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**NEWCOMPUTER**|The target computer is a new computer that has never been a member of the network.|
|**REFRESH**|The target computer is an existing computer on the network that needs the desktop environment standard to be redeployed.|
|**REPLACE**|An existing computer on the network is being replaced with a new computer. The user state migration data is transferred from the existing computer to a new computer.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DeploymentType=NEWCOMPUTER`|

###  <a name="DeployRoot"></a> DeployRoot
 Specifies the UNC or local path to the folder that is the root of the folder structure that MDT uses. This folder structure contains configuration files, scripts, and other folders and files that MDT uses. The value of this property is set based on the following MDT deployment technologies:

-   **LTI**. This property is the UNC path to the deployment share that the Deployment Workbench creates. Use this property to select a specific deployment share. The most common use of this property is in the BootStrap.ini file to identify a deployment share before the connection to the deployment share is established. All other deployment share folders are relative to this property (such as device drivers, language packs, or operating systems).

-   **ZTI**. This property is the local path to the folder to which the MDT files package is copied. The **Use Toolkit Package** task sequence step copies the MDT files package to a local folder on the target computer, and then automatically sets this property to the local folder.

    > [!NOTE]
    >  For ZTI, this property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or in the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*path*|The UNC or local path to the .|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DeployRoot=\\NYC-AM-FIL-01\Distribution$ UserDataLocation=NONE`|

###  <a name="DestinationDisk"></a> DestinationDisk
 Disk number that the image will be deployed to.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*disk_number*|The number of the disk to which the image will be deployed|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DestinationDisk=0`|

###  <a name="DestinationLogicalDrive"></a> DestinationLogicalDrive
 The logical drive to which the image will be deployed.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*logical_drive_number*|The logical drive to which the image will be deployed|

|**Example 1**|
|-|
|`[Settings] Priority=Default  [Default] DestinationLogicalDrive=0`|

|**Example 2**|
|-|
|`[Settings] Priority=Default  [Default] DestinationLogicalDrive=0`<br /><br /> `[Settings] Priority=Default  [Default] InstallDNS=YES DomainNetBIOSName=WoodGroveBank NewDomain=Child DomainLevel=3 ForestLevel=3 NewDomainDNSName=newdom.WoodGroveBank.com ParentDomainDNSName=WoodGroveBank.com AutoConfigDNS=YES ConfirmGC=YES CriticalReplicationOnly=NO ADDSUserName=Administrator ADDSUserDomain=WoodGroveBank ADDSPassword=<complex_password> DatabasePath=%DestinationLogicalDrive%\Windows\NTDS ADDSLogPath=%DestinationLogicalDrive%\Windows\NTDS SysVolPath=%DestinationLogicalDrive%\Windows\SYSVOL SafeModeAdminPassword=<complex_password>`|

###  <a name="DestinationPartition"></a> DestinationPartition
 Disk partition to which the image will be deployed.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*partition_number*|The number of the partition to which the image will be deployed|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DestinationPartition=1`|

###  <a name="DHCPScopes"></a> DHCPScopes
 Specifies the number of DHCP scopes to configure.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*scopes*|Specifies the number of DHCP scopes to configure|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DHCPScopes=1`|

###  <a name="DHCPScopesxDescription"></a> DHCPScopesxDescription
 The description of the DHCP scope.

> [!NOTE]
>  The *x* in this properties name is a placeholder for a zero-based array that contains DHCP configurations.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*description*|The description of the DHCP scope|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DHCPScopes0Description=DHCPScope0`|

###  <a name="DHCPScopesxEndIP"></a> DHCPScopesxEndIP
 Specifies the ending IP address for the DHCP scope.

 The *x* in this properties name is a placeholder for a zero-based array that contains DHCP configurations.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*end_IP*|Specifies the ending IP address for the DHCP scope|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DHCPScopes0EndIP=192.168.0.30`|

###  <a name="DHCPScopesxExcludeEndIP"></a> DHCPScopesxExcludeEndIP
 Specifies the ending IP address for the DHCP scope exclusion. IP addresses that are excluded from the scope are not offered by the DHCP server to clients obtaining leases from this scope.

> [!NOTE]
>  The *x* in this properties name is a placeholder for a zero-based array that contains DHCP configurations.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*exclude_end_IP*|Specifies the ending IP address for the DHCP scope exclusion|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DHCPScopes0ExcludeEndIP=192.168.0.15`|

###  <a name="DHCPScopesxExcludeStartIP"></a> DHCPScopesxExcludeStartIP
 Specifies the starting IP address for the DHCP scope exclusion. IP addresses that are excluded from the scope are not offered by the DHCP server to clients obtaining leases from this scope.

> [!NOTE]
>  The *x* in this properties name is a placeholder for a zero-based array that contains DHCP configurations.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*exclude_start_IP*|Specifies the starting IP address for the DHCP scope exclusion|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DHCPScopes0ExcludeStartIP=192.168.0.10`|

###  <a name="DHCPScopesxIP"></a> DHCPScopesxIP
 Specifies the IP subnet of the scope.

 The *x* in this properties name is a placeholder for a zero-based array that contains DHCP configurations.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*IP*|Specifies the IP subnet of the scope|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DHCPScopes0IP=192.168.0.0`|

###  <a name="DHCPScopesxName"></a> DHCPScopesxName
 A user-definable name to be assigned to the scope.

 The *x* in this properties name is a placeholder for a zero-based array that contains DHCP configurations.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*name*|A user-definable name to be assigned to the scope|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DHCPScopes0Name=DHCPScope0`|

###  <a name="DHCPScopesxOptionDNSDomainName"></a> DHCPScopesxOptionDNSDomainName
 Specifies the domain name that the DHCP client should use when resolving unqualified domain names with the DNS.

> [!NOTE]
>  The *x* in this properties name is a placeholder for a zero-based array that contains DHCP configurations.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*DNS_domain_name*|Specifies the domain name that the DHCP client should use when resolving unqualified domain names with the DNS|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DHCPScopes0OptionDNSDomainName=WoodGroveBank.com`|

###  <a name="DHCPScopesxOptionDNSServer"></a> DHCPScopesxOptionDNSServer
 Specifies a list of IP addresses for DNS name servers available to the client. When more than one server is assigned, the client interprets and uses the addresses in the specified order.

> [!NOTE]
>  The *x* in this properties name is a placeholder for a zero-based array that contains DHCP configurations.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*DNS_server*|Specifies a list of IP addresses for DNS name servers available to the client|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DHCPScopes0OptionDNSServer=192.168.0.2`|

###  <a name="DHCPScopesxOptionLease"></a> DHCPScopesxOptionLease
 The duration that the DHCP lease is valid for the client.

> [!NOTE]
>  The *x* in this properties name is a placeholder for a zero-based array that contains DHCP configurations.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*lease*|The duration that the DHCP lease is valid for the client|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DHCPScopes0OptionLease=7`|

###  <a name="DHCPScopesxOptionNBTNodeType"></a> DHCPScopesxOptionNBTNodeType
 Specifies the client node type for NetBT clients.

> [!NOTE]
>  The *x* in this properties name is a placeholder for a zero-based array that contains DHCP configurations.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**1**|Configures the node type as b-node|
|**2**|Configures the node type as p-node|
|**4**|Configures the node type as m-node|
|**8**|Configures the node type as h-node|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DHCPScopes0OptionNBTNodeType=4`|

###  <a name="DHCPScopesxOptionPXEClient"></a> DHCPScopesxOptionPXEClient
 Specifies the IP address used for PXE client bootstrap code.

> [!NOTE]
>  The *x* in this properties name is a placeholder for a zero-based array that contains DHCP configurations.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*PXE_client*|Specifies the IP address used for PXE client bootstrap code|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DHCPScopes0OptionPXEClient=192.168.0.252`|

###  <a name="DHCPScopesxOptionRouter"></a> DHCPScopesxOptionRouter
 Specifies a list of IP addresses for routers on the client subnet. When more than one router is assigned, the client interprets and uses the addresses in the specified order. This option is normally used to assign a default gateway to DHCP clients on a subnet.

> [!NOTE]
>  The *x* in this properties name is a placeholder for a zero-based array that contains DHCP configurations.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*router*|Specifies a list of IP addresses for routers on the client subnet|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DHCPScopes0OptionRouter=192.168.0.253`|

###  <a name="DHCPScopesxOptionWINSServer"></a> DHCPScopesxOptionWINSServer
 Specifies the IP addresses to be used for NBNSes on the network.

> [!NOTE]
>  The *x* in this properties name is a placeholder for a zero-based array that contains DHCP configurations

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*WINS_server*|Specifies the IP addresses to be used for NBNSes on the network|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DHCPScopes0OptionWINSServer=192.168.0.2`|

###  <a name="DHCPScopesxStartIP"></a> DHCPScopesxStartIP
 The starting IP address for the range of IP addresses that are to be included in the scope.

> [!NOTE]
>  The *x* in this properties name is a placeholder for a zero-based array that contains DHCP configurations.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*start_IP*|The starting IP address for the range of IP addresses that are to be excluded from the scope|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DHCPScopes0StartIP=192.168.0.20`|

###  <a name="DHCPScopesxSubnetMask"></a> DHCPScopesxSubnetMask
 Specifies the subnet mask of the client subnet.

> [!NOTE]
>  The *x* in this properties name is a placeholder for a zero-based array that contains DHCP configurations.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*subnet_mask*|Specifies the subnet mask of the client IP subnet|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DHCPScopes0SubnetMask=255.255.255.0`|

###  <a name="DHCPServerOptionDNSDomainName"></a> DHCPServerOptionDNSDomainName
 Specifies the connection-specific DNS domain suffix of client computers.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*DNS_domain_name*|Specifies the connection-specific DNS domain suffix of client computers|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DHCPServerOptionDNSDomainName=Fabrikam.com`|

###  <a name="DHCPServerOptionDNSServer"></a> DHCPServerOptionDNSServer
 Specifies a list of IP addresses to be used as DNS name servers that are available to the client.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*DNS_server*|Specifies a list of IP addresses to be used as DNS name servers that are available to the client|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DHCPServerOptionDNSServer=192.168.0.1,192.168.0.2`|

###  <a name="DHCPServerOptionNBTNodeType"></a> DHCPServerOptionNBTNodeType
 Specifies the client node type for NetBT clients.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**1**|Configures the node type as b-node|
|**2**|Configures the node type as p-node|
|**4**|Configures the node type as m-node|
|**8**|Configures the node type as h-node|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DHCPServerOptionNBTNodeType=4`|

###  <a name="DHCPServerOptionPXEClient"></a> DHCPServerOptionPXEClient
 Specifies the IP address used for PXE client bootstrap code.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*PXE_client*|Specifies the IP address used for PXE client bootstrap code|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DHCPServerOptionPXEClient=192.168.0.252`|

###  <a name="DHCPServerOptionRouter"></a> DHCPServerOptionRouter
 Specifies a list of IP addresses for routers on the client subnet. When more than one router is assigned, the client interprets and uses the addresses in the specified order. This option is normally used to assign a default gateway to DHCP clients on a subnet.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*router*|Specifies a list of IP addresses for routers on the client subnet|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DHCPServerOptionRouter=192.168.0.253`|

###  <a name="DHCPServerOptionWINSServer"></a> DHCPServerOptionWINSServer
 Specifies the IP addresses to be used for NBNSes on the network.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*WINS_server*|Specifies the IP addresses to be used for NBNSes on the network|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DHCPServerOptionWINSServer=192.168.0.2`|

###  <a name="Dialing"></a> Dialing
 The type of dialing supported by the telephony infrastructure where the target computer is located. This value is inserted into the appropriate configuration settings in Unattend.xml.

> [!CAUTION]
>  This property value must be specified in uppercase so that the deployment scripts can read it properly.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**PULSE**|The telephony infrastructure supports pulse dialing.|
|**TONE**|The telephony infrastructure supports touch-tone dialing.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] AreaCode=206 CountryCode=001 Dialing=TONE LongDistanceAccess=9`|

###  <a name="DisableTaskMgr"></a> DisableTaskMgr
 This property controls a user's ability to start Task Manager by pressing CTRL+ALT+DEL. After the user starts Task Manager, they could interrupt the LTI task sequence while running in the new operating system on the target computer. This property is used in conjunction with the **HideShell** property and is only valid when the **HideShell** property is set to **YES**.

> [!NOTE]
>  This property and the **HideShell** property must both be set to **YES** to prevent the user pressing CTRL+ALT+DEL and interrupting the LTI task sequence.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**YES**|Prevent the user from being able to start Task Manager by pressing CTRL+ALT+DEL and subsequently interrupting the LTI task sequence.|
|**NO**|Allow the user to start Task Manager by pressing CTRL+ALT+DEL and subsequently interrupt the LTI task sequence. This is the default value.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DisableTaskMgr=YES HideShell=YES`|

###  <a name="DNSServerOptionBINDSecondaries"></a> DNSServerOptionBINDSecondaries
 Determines whether to use fast transfer format for transfer of a zone to DNS servers running legacy BIND implementations.

 By default, all Windows-based DNS servers use a fast zone transfer format. This format uses compression, and it can include multiple records per TCP message during a connected transfer. This format is also compatible with more recent BIND-based DNS servers that run version 4.9.4 and later.

> [!CAUTION]
>  This property value must be specified in uppercase so that the deployment scripts can read it properly.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|Allows BIND secondaries|
|**FALSE**|Does not allow to BIND secondaries|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DNSServerOptionBINDSecondaries=TRUE`|

###  <a name="DNSServerOptionDisableRecursion"></a> DNSServerOptionDisableRecursion
 Determines whether or not the DNS server uses recursion. By default, the DNS Server service is enabled to use recursion.

> [!CAUTION]
>  This property value must be specified in uppercase so that the deployment scripts can read it properly.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|Disables recursion on the DNS server|
|**FALSE**|Enables recursion on the DNS server|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DNSServerOptionDisableRecursion=TRUE`|

###  <a name="DNSServerOptionEnableNetmaskOrdering"></a> DNSServerOptionEnableNetmaskOrdering
 Determines whether the DNS server reorders address (A) resource records within the same resource record that is set in the server's response to a query based on the IP address of the source of the query.

 By default, the DNS Server service uses local subnet priority to reorder A resource records.

> [!CAUTION]
>  This property value must be specified in uppercase so that the deployment scripts can read it properly.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|Enables netmask ordering|
|**FALSE**|Disables netmask ordering|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DNSServerOptionEnableNetmaskOrdering=TRUE`|

###  <a name="DNSServerOptionEnableRoundRobin"></a> DNSServerOptionEnableRoundRobin
 Determines whether the DNS server uses the round robin mechanism to rotate and reorder a list of resource records if multiple resource records exist of the same type that exist for a query answer.

 By default, the DNS Server service uses round robin.

> [!CAUTION]
>  This property value must be specified in uppercase so that the deployment scripts can read it properly.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|Enables round robin|
|**FALSE**|Disables round robin|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DNSServerOptionEnableRoundRobin=TRUE`|

###  <a name="DNSServerOptionEnableSecureCache"></a> DNSServerOptionEnableSecureCache
 Determines whether the DNS server attempts to clean up responses to avoid cache pollution. This setting is enabled by default. By default, DNS servers use a secure response option that eliminates adding unrelated resource records that are included in a referral answer to their cache. In most cases, any names that are added in referral answers are typically cached, and they help expedite the resolution of subsequent DNS queries.

 With this feature, however, the server can determine that referred names are potentially polluting or insecure and then discard them. The server determines whether to cache the name that is offered in a referral on the basis of whether it is part of the exact, related, DNS domain name tree for which the original queried name was made.

> [!CAUTION]
>  This property value must be specified in uppercase so that the deployment scripts can read it properly.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|Enables cache security|
|**FALSE**|Disables cache security|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DNSServerOptionEnableSecureCache=TRUE`|

###  <a name="DNSServerOptionFailOnLoad"></a> DNSServerOptionFailOnLoad
 Specifies that loading of a zone should fail when bad data is found.

> [!CAUTION]
>  This property value must be specified in uppercase so that the deployment scripts can read it properly.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|Enable fail on load|
|**FALSE**|Disable fail on load|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DNSServerOptionFailOnLoad=TRUE`|

###  <a name="DNSServerOptionNameCheckFlag"></a> DNSServerOptionNameCheckFlag
 Specifies which character standard is used when checking DNS names.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**0**|Uses ANSI characters that comply with Internet Engineering Task Force (IETF) Request for Comments (RFCs). This value corresponds to the **Strict RFC (ANSI)** selection when configuring DNS in the Deployment Workbench.|
|**1**|Uses ANSI characters that do not necessarily comply with IETF RFCs. This value corresponds to the **Non RFC (ANSI)** selection when configuring DNS in the Deployment Workbench.|
|**2**|Uses multibyte UCS Transformation Format 8 (UTF-8) characters. This is the default setting. This value corresponds to the **Multibyte (UTF-8)** selection when configuring DNS in the Deployment Workbench.|
|**3**|Uses all characters. This value corresponds to the **All names** selection when configuring DNS in the Deployment Workbench.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DNSServerOptionNameCheckFlag=2`|

###  <a name="DNSZones"></a> DNSZones
 Specifies the number of DNS zones to configure.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*zones*|Specifies the number of DNS zones to configure|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DNSZones=1 DNSZones0Name=MyNewZone DNSZones0DirectoryPartition=Forest DNSZones0FileName=MyNewZone.dns DNSZones0MasterIP=192.168.0.1,192.168.0.2 DNSZones0Type=Secondary`|

###  <a name="DNSZonesxDirectoryPartition"></a> DNSZonesxDirectoryPartition
 Specifies the directory partition on which to store the zone when configuring secondary or stub zones.

> [!NOTE]
>  The *x* in this properties name is a placeholder for a zero-based array that contains DNS configurations.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**Domain**|Replicates zone data to all DNS server in the AD DS domain|
|**Forest**|Replicates zone data to all DNS server in the AD DS forest|
|**Legacy**|Replicates zone data to all domain controllers in the AD DS domain|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DNSZones0DirectoryPartition=Forest`|

###  <a name="DNSZonesxFileName"></a> DNSZonesxFileName
 Specifies the name of the file that will store the zone information.

> [!NOTE]
>  The *x* in this properties name is a placeholder for a zero-based array that contains DNS configurations.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*file_name*|Specifies the name of the file that will store the zone information|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DNSZones0FileName=MyNewZone.dns`|

###  <a name="DNSZonesxMasterIP"></a> DNSZonesxMasterIP
 A comma delimited list of IP addresses of the main servers to be used by the DNS server when updating the specified secondary zones. This property must be specified when configuring a secondary or stub DNS zone.

> [!NOTE]
>  The *x* in this properties name is a placeholder for a zero-based array that contains DNS configurations.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*IP1,IP2*|A comma-delimited list of IP addresses of the main servers|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DNSZones0MasterIP=192.168.0.1,192.168.0.2`|

###  <a name="DNSZonesxName"></a> DNSZonesxName
 Specifies the name of the zone.

> [!NOTE]
>  The *x* in this properties name is a placeholder for a zero-based array that contains DNS configurations.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*name*|Specifies the name of the zone|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DNSZones0Name=MyNewZone`|

###  <a name="DNSZonesxScavenge"></a> DNSZonesxScavenge
 Configures the Primary DNS server to "scavenge" stale records—that is, to search the database for records that have aged and delete them.

> [!NOTE]
>  The *x* in this properties name is a placeholder for a zero-based array that contains DNS configurations.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|Allow stale DNS records to be scavenged.|
|**FALSE**|Do not allow stale DNS records to be scavenged.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DNSZones0Scavenge=TRUE`|

### DNSZonesxType
 Specifies the type of zone to create.

> [!NOTE]
>  The *x* in this properties name is a placeholder for a zero-based array that contains DNS configurations.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**DSPrimary**|Creates a primary zone and specifying that it should be stored in AD DS on a DNS server configured as a domain controller|
|**DSStub**|Creates a stub zone and specifying that it should be stored in AD DS on a DNS server configured as a domain controller|
|**Primary**|Creates a primary zone|
|**Secondary**|Creates a secondary zone|
|**Stub**|Creates a stub zone|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DNSZones0Type=Secondary`|

###  <a name="DNSZonesxUpdate"></a> DNSZonesxUpdate
 Configures the Primary DNS server to perform dynamic updates.

> [!NOTE]
>  The *x* in this properties name is a placeholder for a zero-based array that contains DNS configurations.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**0**|Does not allow dynamic updates|
|**1**|Allows dynamic updates|
|**2**|Allows secure dynamic updates|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DNSZones0Update=1`|

###  <a name="DoCapture"></a> DoCapture
 Indicator of whether an image of the target computer is to be captured. If it is, Sysprep is run on the target computer to prepare for image creation. After Sysprep has run, a new WIM image is created and stored in the folder within the shared folder designated for target computer backups (**BackupDir** and **BackupShare**, respectively).

> [!CAUTION]
>  This property value must be specified in uppercase so that the deployment scripts can read it properly.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**YES**|Copy the necessary files to run Sysprep on the target computer, run Sysprep on the target computer, and capture a WIM image.|
|**NO**|Do not run Sysprep on the target computer, and do not capture a WIM image.|
|**PREPARE**|Copy the necessary files to run Sysprep on the target computer, but do not run Sysprep or other image-capture processes.|
|**SYSPREP**|Copy the necessary files to run Sysprep on the target computer, run Sysprep on the target computer, but do not capture a WIM image.<br /><br /> Note:<br /><br /> The primary purpose of this value is to allow the creation of a VHD that contains an operating system after Sysprep has been run and no image capture is necessary.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DoCapture=YES DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UDShare=\\NYC-AM-FIL-01\MigData$ UDDir=%OSDComputerName%`|

###  <a name="DomainAdmin"></a> DomainAdmin
 The user account credentials used to join the target computer to the domain specified in **JoinDomain**. Specify as *UserName*.

> [!NOTE]
>  For ZTI, the credentials that Configuration Manager specifies typically are used. If the **DomainAdmin** property is specified, the credentials in the **DomainAdmin** property override the credentials that Configuration Manager specifies.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*domain_admin*|The name of the user account credentials|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DomainAdmin=NYCAdmin DomainAdminDomain=WOODGROVEBANK DomainAdminPassword=<complex_password>`|

###  <a name="DomainAdminDomain"></a> DomainAdminDomain
 The domain in which the user's credentials specified in **DomainAdmin** reside.

> [!NOTE]
>  For ZTI, the credentials that Configuration Manager specifies typically are used. If the **DomainAdmin** property is specified, the credentials in the **DomainAdmin** property override the credentials that Configuration Manager specifies.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*domain_admin_domain*|The name of the domain where the user account credentials reside|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DomainAdmin=NYCAdmin DomainAdminDomain=WOODGROVEBANK DomainAdminPassword=<complex_password>`|

###  <a name="DomainAdminPassword"></a> DomainAdminPassword
 The password used for the domain Administrator account specified in the **DomainAdmin** property to join the computer to the domain.

> [!NOTE]
>  For ZTI, the credentials that Configuration Manager specifies typically are used. If the **DomainAdmin** property is specified, the credentials in the **DomainAdmin** property override the credentials that Configuration Manager specifies.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*domain_admin_password*|The password for the domain Administrator account on the target computer|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DomainAdmin=NYCAdmin DomainAdminDomain=WOODGROVEBANK DomainAdminPassword=<complex_password>`|

###  <a name="DomainLevel"></a> DomainLevel
 This entry specifies the domain functional level. This entry is based on the levels that exist in the forest when a new domain is created in an existing forest.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*Level*|Sets the domain functional level to one of the following:<br /><br /> - 2, Windows Server 2003<br /><br /> - 3, Windows Server 2008<br /><br /> - 4, Windows Server 2008 R2<br /><br /> - 5, Windows Server 2012|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DomainLevel=3`|

###  <a name="DomainNetBiosName"></a> DomainNetBiosName
 Assigns a NetBIOS name to the new domain.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*Name*|Assigns a NetBIOS name to the new domain|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DomainNetBiosName=NewDom`|

###  <a name="DomainOUs"></a> DomainOUs
 A list of AD DS organizational units (OUs) where the target computer account can be created. The **DomainOUs** property lists text values that can be any non-blank value. The **DomainOUs** property has a numeric suffix (for example, **DomainOUs1** or **DomainOUs2**). The values specified by DomainOUs will be displayed in the Deployment Wizard and selectable by the user. The **MachineObjectOU** property will then be set to the OU selected.

 In addition, the same functionality can be provided by configuring the DomainOUList.xml file. The format of the DomainOUList.xml file is as follows:

```xml
<?xml version="1.0" encoding="utf-8"?>
<DomainOUs>
<DomainOU>
  OU=Computers,OU=Tellers,OU=NYC,DC=WOODGROVEBANK,DC=Com
</DomainOU>
<DomainOU>
  OU=Computers,OU=Managers,OU=NYC,DC=WOODGROVEBANK,DC=Com
</DomainOU>
</DomainOUs>
```

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*OU*|The OU in which the target computer account can be created|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSInstall=Y DomainOUs1=OU=Computers, OU=Tellers, OU=NYC, DC=WOODGROVEBANK, DC=Com DomainOUs2=OU=Computers, OU=Managers, OU=NYC, DC=WOODGROVEBANK, DC=Com`|

###  <a name="DoNotCreateExtraPartition"></a> DoNotCreateExtraPartition
 Specifies that deployments of Windows 7 and Windows Server 2008 R2 will not create the 300 MB system partition.

> [!CAUTION]
>  This property value must be specified in uppercase so that the deployment scripts can read it properly.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**YES**|The additional system partition will not be created.|
|**NO**|The additional system partition will be created.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSInstall=Y DoNotCreateExtraPartition=YES`|

> [!NOTE]
>  Do not use this property in conjunction with properties to configure BitLocker settings.

###  <a name="DoNotFormatAndPartition"></a> DoNotFormatAndPartition
 This property is used to configure whether MDT performs any of the partitioning and formatting task sequence steps in task sequences created using the MDT task sequence templates.

> [!CAUTION]
>  This property value must be specified in uppercase so that the deployment scripts can read it properly.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**YES**|The partitioning and formatting task sequence steps in an MDT task sequence will be performed.|
|*Any other value*|The partitioning and formatting task sequence steps in an MDT task sequence will not be performed. This is the default value.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSInstall=YES SkipUserData=YES USMTOfflineMigration=TRUE DoNotFormatAndPartition=YES OSDStateStorePath=\\WDG-MDT-01\StateStore$`|

###  <a name="DriverGroup"></a> DriverGroup
 A list of text values that associates out-of-box drivers created in the Deployment Workbench with each other (typically based on the make and model of a computer). A driver can be associated with one or more driver groups. The **DriverGroup** property allows the drivers within one or more groups to be deployed to a target computer.

 The text values in the list can be any non-blank value. The **DriverGroup** property value has a numeric suffix (for example, **DriverGroup001** or **DriverGroup002**). After it is defined, a driver group is associated with a computer. A computer can be associated with more than one driver group.

 For example, there are two sections for each of the computer manufacturers [Mfgr01] and [Mfgr02]. Two driver groups are defined for the manufacturer Mfgr01: Mfgr01 Video Drivers and Mfgr01 Network Drivers. For the manufacturer Mfgr02, one driver group is defined, Mfgr02 Drivers. One driver group, Shared Drivers, is applied to all computers found in the [Default] section.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*driver_group_name*|The name of the driver group defined in the Deployment Workbench|

|**Example**|
|-|
|`[Settings] Priority=Make, Default  [Default] DriverGroup001=Shared Drivers :: [Mfgr01] DriverGroup001=Mfgr01 Video Drivers DriverGroup002=Mfgr01 Network Drivers  [Mfgr02] DriverGroup001=Mfgr02 Drivers`|

###  <a name="DriverInjectionMode"></a> DriverInjectionMode
 This property is used to control the device drivers that are injected by the [Inject Drivers](#InjectDrivers) task sequence step.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|Auto|Inject only matching drivers from the selection profile or folder.  This is the same behavior as MDT 2008, which injects all drivers that matched one of the plug and play (PnP) identifiers (IDs) on the target computer.|
|All|Inject all drivers in the selection profile or folder.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DriverInjectionMode=ALL DriverSelectionProfile=Nothing DriverPaths001=\\NYC-AM-FIL-01\Drivers$ DriverPaths002=\\NYC-AM-FIL-03\WinDrvs`|

###  <a name="DriverPaths"></a> DriverPaths
 A list of UNC paths to shared folders where additional device drivers are located. These device drivers are installed with the target operating system on the target computer. The MDT scripts copy the contents of these folders to the C:\Drivers folder on the target computer. The **DriverPaths** property is a list of text values that can be any non-blank value. The **DriverPaths** property has a numeric suffix (for example, **DriverPaths001** or **DriverPaths002**).

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*UNC_path*|UNC path to the shared folder in which the additional drivers reside|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DriverPaths001=\\NYC-AM-FIL-01\Drivers$ DriverPaths002=\\NYC-AM-FIL-03\Win8Drvs`|

###  <a name="DriverSelectionProfile"></a> DriverSelectionProfile
 Profile name used during driver installation.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*profile_name*|None|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DriverSelectionProfile=MonitorDrivers`|

###  <a name="EventService"></a> EventService
 The **EventService** property specifies the URL where the MDT monitoring service is running. By default, the service uses TCP port 9800 to communicate. The MDT monitoring service collects deployment information on the deployment process that can be viewed in the Deployment Workbench and using the [Get-MDTMonitorData](#Get-MDTMonitorData) cmdlet.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*url_path*|The URL to the MDT monitoring service.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] EventService=https://WDG-MDT-01:9800 DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$`|

###  <a name="EventShare"></a> EventShare
 The **EventShare** property points to a shared folder in which the MDT scripts record events.

 By default, the shared folder is created in C:\Events.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*UNC_path*|The UNC path to the shared folder in which the MDT scripts record events. The default share name is Events.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] EventShare=\\NYC-AM-FIL-01\Events DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$`|

###  <a name="FinishAction"></a> FinishAction
 Specifies the action to be taken when an LTI task sequence finishes, which is after the **Summary** wizard page in the Deployment Wizard.

> [!TIP]
>  Use this property in conjunction with the **SkipFinalSummary** property to skip the **Summary** wizard page in the Deployment Wizard and automatically perform the action.

> [!CAUTION]
>  This property value must be specified in uppercase so that the deployment scripts can read it properly.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*action*|Where *action* is one of the following:<br /><br /> - **SHUTDOWN**. Shuts down the target computer.<br /><br /> - **REBOOT**. Restarts the target computer.<br /><br /> - **RESTART**. Same as **REBOOT**.<br /><br /> - **LOGOFF**. Log off the current user. If the target computer is currently running Windows PE, then the target computer will be restarted.<br /><br /> - **blank**. Exit the Deployment Wizard without performing any additional actions. This is the default setting.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] FinishAction=REBOOT`|

###  <a name="ForceApplyFallback"></a> ForceApplyFallback
 Controls the method used for installed Windows:

- **setup.exe**. This method is the traditional method, initiated by running setup.exe from the installation media. MDT uses this method by default.

- imagex.exe. This method installs the operating system image using imagex.exe with the **/apply** option. MDT uses this method when the setup.exe method cannot be used (i.e., MDT falls back to using imagex.exe).

  Besides controlling the method used to install these operating systems, this property affects which operating system task sequences are listed in the Deployment Wizard for a specific processor architecture boot image. When the value of this property is set to **NEVER**, only operating system task sequences that match the processor architecture of the boot image are displayed. If the value of this property is set to any other value or is blank, all task sequences that can use the imagex.exe installation method are shown, regardless of the processor architecture.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**NEVER**|MDT always uses the imagex.exe method if necessary. Only task sequences that deploy an operating system that matches the boot image are displayed in the Deployment Wizard.|
|Any other value, including blank| Any task sequence that supports the imagex.exe method is displayed in the Deployment Wizard.|


|**Example**|
 |-|
|`[Settings] Priority=Default  [Default] OSInstall=YES ForceApplyFallback=NEVER`|

###  <a name="ForestLevel"></a> ForestLevel
 This entry specifies the forest functional level when a new domain is created in a new forest.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*level*|Sets the domain functional level to one of the following:<br /><br /> - 2, Windows Server 2003<br /><br /> - 3, Windows Server 2008<br /><br /> - 4, Windows Server 2008 R2<br /><br /> - 5, Windows Server 2012|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] ForestLevel=3`|

###  <a name="FullName"></a> FullName
 The full name of the user of the target computer provided during the installation of the operating system. This value is inserted into the appropriate configuration settings in Unattend.xml.

> [!NOTE]
>  This value is different from the user credentials created after the operating system is deployed. The **FullName** property is provided as information to systems administrators about the user running applications on the target computer.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*full_name*|The full name of the user of the target computer|

|**Example**|
|-|
|`[Settings] Priority=MACAddress, Default Properties=CustomProperty, ApplicationInstall  [Default] CustomProperty=TRUE OrgName=Woodgrove Bank  [00:0F:20:35:DE:AC] OSDNEWMACHINENAME=HPD530-1 ApplicationInstall=Custom FullName=Woodgrove Bank User  [00:03:FF:FE:FF:FF] OSDNEWMACHINENAME=BVMXP  ApplicationInstall=Minimum FullName=Woodgrove Bank Manager`|

###  <a name="GPOPackPath"></a> GPOPackPath
 This property is used to override the default path to the folder in which the GPO packs reside. The path specified in this property is relative to the Templates\GPOPacks folder in a distribution share. MDT automatically scans a specific subfolder of this folder based on the operating system being deployed to the target computer, such as Templates\GPOPacks\\*operating_system* (where *operating_system* is the operating system being deployed). Table 3 list the supported operating systems and the subfolders that correspond to each operating system.

#### Table 3. Windows Operating Systems and Corresponding GPO Pack Subfolder

|**Operating system**|**GPO pack subfolder**|
|-|-|
|Windows 7 with SP1|Win7SP1-MDTGPOPack|
|Windows Server 2008 R2|WS2008R2SP1-MDTGPOPack|

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*path*|The path relative to the *distribution_share*\Templates\GPOPacks folder (where *distribution_share* is the root folder of the distribution share. The default value is the *distribution_share*\Templates\GPOPacks\\*operating_system* folder (where *operating_system* is a subfolder based on the operating system version).<br /><br /> In the example below, setting the GPOPackPath property to a value of "Win7-HighSecurity" configures MDT to use the *distribution_share*\Templates\GPOPacks\Win7-HighSecurity folder as the folder where the GPO packs are stored.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] GPOPackPath=Win7-HighSecurity`|

###  <a name="Groups"></a> Groups
 The list of local groups on the target computer whose membership will be captured. This group membership is captured during the State Capture Phase and is restored during the State Restore Phase. (The default groups are Administrators and Power Users.) The **Groups** property is a list of text values that can be any non-blank value. The **Groups** property has a numeric suffix (for example, **Groups001** or **Groups002**).

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*group_name*|The name of the local group on the target computer for which group membership will be captured|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UDShare=\\NYC-AM-FIL-01\MigData$ CaptureGroups=YES Groups001=NYC Application Management Groups002=NYC Help Desk Users`|

###  <a name="HideShell"></a> HideShell
 This property controls the display of Windows Explorer while the LTI task sequence is running in the new operating system on the target computer. This property can be used in conjunction with the **DisableTaskMgr** property.

> [!NOTE]
>  This property can be used with the **DisableTaskMgr** property to help prevent users from interrupting the LTI task sequence. For more information, see the [DisableTaskMgr](#DisableTaskMgr) property.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**YES**|Windows Explorer is hidden until the task sequence is complete.|
|**NO**|Windows Explorer is visible while the task sequence is running. This is the default value.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DisableTaskMgr=YES HideShell=YES`|

###  <a name="Home_Page"></a> Home_Page
 The URL to be used as the Windows Internet Explorer&reg; home page after the target operating system is deployed.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*URL*|The URL of the web page to be used as the home page for Internet Explorer on the target computer|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] Home_Page=https://portal.woodgrovebank.com`|

###  <a name="HostName"></a> HostName
 The IP host name of the target computer (the name assigned to the target computer).

> [!NOTE]
>  This is the computer name of the target computer, not the NetBIOS computer name of the target computer. The NetBIOS computer name can be shorter than the computer name. Also, this property is dynamically set by MDT scripts and cannot have its value set in CustomSettings.ini or the MDT DB. Treat this property as read only. However, you can use this property within CustomSettings.ini or the MDT DB, as shown in the following examples, to aid in defining the configuration of the target computer.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*host_name*|The IP host name assigned to the target computer|

|**Example**|
|-|
|None|

###  <a name="ImagePackageID"></a> ImagePackageID
 The package ID used for the operating system to install during OEM deployments.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|None|The package ID used for the operating system to install during OEM deployments|

|**Example**|
|-|
|None|

###  <a name="InputLocale"></a> InputLocale
 A list of input locales to be used with the target operating system. More than one input locale can be specified for the target operating system. Each locale must be separated by a semicolon (;). If not specified, the Deployment Wizard uses the input locale configured in the image being deployed.

 Exclude this setting in the Windows User State Migration Tool (USMT) when backing up and restoring user state information. Otherwise, the settings in the user state information will override the values specified in the *InputLocale* property.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*input_locale1; input_locale2*|The locale for the keyboard attached to the target computer|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] UserLocale=en-us InputLocale=0409:00000409;0413:00020409;0413:00000409;0409:00020409`|

###  <a name="InstallPackageID"></a> InstallPackageID
 The package ID used for the operating system to install during OEM deployments.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|None|The package ID used for the operating system to install during OEM deployments|

|**Example**|
|-|
|None|

###  <a name="Instance"></a> Instance
 The instance of SQL Server used for querying property values from columns in the table specified in the **Table** property. The database resides on the computer specified in the **SQLServer** property. The instance of SQL Server on the computer is specified in the **Instance** property.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

| **Value** | **Description** |
|-----------|-----------------|
|           |   *instance*    |

|**Example**|
|-|
|`[Settings] Priority=Computers, Default  [Default] OSInstall=YES  [Computers] SQLServer=NYC-SQL-01 Database=MDTDB Instance=SQLEnterprise2005 Table=Computers Parameters=SerialNumber, AssetTag ParameterCondition=OR`|

###  <a name="IPAddress"></a> IPAddress
 The IP address of the target computer. The format of the IP address returned by the property is standard dotted-decimal notation; for example, 192.168.1.1. Use this property to create a subsection that contains settings targeted to a specific target computer based on the IP address.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*ip\_address*|The IP address of the target computer in standard dotted\-decimal notation|

|**Example**|
|-|
|None|

###  <a name="IsDesktop"></a> IsDesktop
 Indicator of whether the computer is a desktop, because the **Win32\_SystemEnclosure ChassisType** property value is **3**, **4**, **5**, **6**, **7**, **15**, **16**, **35**, or **36**.

> [!NOTE]
>  Only one of the following properties will be true at a time: **IsDesktop**, **IsLaptop**, **IsServer**.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|The target computer is a desktop computer.|
|**FALSE**|The target computer is not a desktop computer.|

|**Example**|
|-|
|None|

###  <a name="IsHypervisorRunning"></a> IsHypervisorRunning
 Specifies whether a hypervisor is present on the target computer. This property is set using information from the **CPUID** interface.

 For further information collected about VMs and information returned from the **CPUID** interface, see the following properties:

-   **IsVM**

-   **SupportsHyperVRole**

-   **SupportsNX**

-   **SupportsVT**

-   **Supports64Bit**

-   **VMPlatform**

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

> [!NOTE]
>  The IsVM property should be used to determine whether the target computer is a virtual or physical machine.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|A hypervisor is detected.|
|**FALSE**|A hypervisor is not detected.|

|**Example**|
|-|
|None|

###  <a name="IsLaptop"></a> IsLaptop
 Indicator of whether the computer is a portable computer, because the **Win32\_SystemEnclosure ChassisType** property value is **8**, **9**, **10**, **11**, **12**, **14**, **18**, **21**, **30**, **31**, or **32**.

> [!NOTE]
>  Only one of the following properties will be true at a time: **IsDesktop**, **IsLaptop**, **IsServer**.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|The target computer is a portable computer.|
|**FALSE**|The target computer is not a portable computer.|

|**Example**|
|-|
|None|

###  <a name="IsServer"></a> IsServer
 Indicator of whether the computer is a server, because the **Win32\_SystemEnclosure ChassisType** property value is **23** or **28**.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|The target computer is a server.|
|**FALSE**|The target computer is not a server.|

|**Example**|
|-|
|None|

###  <a name="IsServerCoreOS"></a> IsServerCoreOS
 Indicator of whether the current operating system running on the target computer is the Server Core installation option of the Windows Server operating system.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|The operating system on the target computer is the Server Core installation option of Windows Server.|
|**FALSE**|The operating system on the target computer is not the Server Core installation option of Windows Server.|

|**Example**|
|-|
|None|

###  <a name="IsServerOS"></a> IsServerOS
 Indicator of whether the current operating system running on the target computer is a server operating system.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|The operating system on the target computer is a server operating system.|
|**FALSE**|The operating system on the target computer is not a server operating system.|

|**Example**|
|-|
|None|

###  <a name="IsUEFI"></a> IsUEFI
 Specifies whether the target computer is currently running with Unified Extensible Firmware Interface \(UEFI\). The UEFI is a specification that defines a software interface between an operating system and platform firmware. UEFI is a more secure replacement for the older BIOS firmware interface present in some personal computers. For more information on UEFI, go to [https:\/\/uefi.org](https://uefi.org).

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|The target computer is currently running with UEFI.|
|**FALSE**|The target computer is not currently running with UEFI.<br /><br /> Note:<br /><br /> It is possible that the target computer may support UEFI, but is running in a compatibility mode that emulates the older BIOS firmware interface. In this situation this value of this property will set to **FALSE** even though the target computer supports UEFI.|

|**Example**|
|-|
|None|

###  <a name="IsVM"></a> IsVM
 Specifies whether the target computer is a VM based on information gathered from the **CPUID** interface. You can determine the specific VM environment using the **VMPlatform** property.

 For further information collected about VMs and information returned from the **CPUID** interface, see the following properties:

-   **IsHypervisorRunning**

-   **SupportsHyperVRole**

-   **SupportsNX**

-   **SupportsVT**

-   **Supports64Bit**

-   **VMPlatform**

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|The target computer is a VM.|
|**FALSE**|The target computer is not a VM.|

|**Example**|
|-|
|None|

###  <a name="JoinDomain"></a> JoinDomain
 The domain that the target computer joins after the target operating system is deployed. This is the domain where the computer account for the target computer is created. The **JoinDomain** property can contain alphanumeric characters, hyphens \(\-\), and underscores \(\_\). The **JoinDomain** property cannot be blank or contain spaces.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*domain\_name*|The name of the domain that the target computer joins|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] JoinDomain=WOODGROVEBANK MachineObjectOU=OU=Reception,OU=NYC,DC=Woodgrovebank,DC=com`|

###  <a name="JoinWorkgroup"></a> JoinWorkgroup
 The workgroup that the target computer joins after the target operating system is deployed. The **JoinWorkgroup** property can contain alphanumeric characters, hyphens \(\-\), and underscores \(\_\). The **JoinWorkgroup** property cannot be blank or contain spaces.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*workgroup\_name*|The name of the workgroup that the target computer joins|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] JoinWorkgroup=WDGV_WORKGROUP`|

###  <a name="KeyboardLocale"></a> KeyboardLocale
 A list of keyboard locales to be used with the target operating system. More than one keyboard locale can be specified for the target operating system. Each locale must be separated by a semicolon \(;\). If not specified, the Deployment Wizard uses the keyboard locale configured in the image being deployed.

 Exclude this setting in USMT when backing up and restoring user state information. Otherwise, the settings in the user state information will override the values specified in the **KeyboardLocale** property.

> [!NOTE]
>  For this property to function properly, it must be configured in both CustomSettings.ini and BootStrap.ini. BootStrap.ini is processed before a deployment share (which contains CustomSettings.ini) has been selected.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*keyboard_locale1; keyboard_locale2*|The locale of the keyboard attached to the target computer.<br /><br /> The value can be specified in the following formats:<br /><br /> - Text (en-us)<br /><br /> - Hexadecimal (0409:00000409)|

|**Example 1**|
|-|
|`[Settings] Priority=Default  [Default] UserLocale=en-us KeyboardLocale=en-us`|

|**Example 2**|
|-|
|`[Settings] Priority=Default  [Default] UserLocale=en-us KeyboardLocale=0409:00000409;1809:00001809;041A:0000041A;083b:0001083b`|

###  <a name="KeyboardLocalePE"></a> KeyboardLocalePE
 The name of the keyboard locale to be used while in Windows PE only.

> [!NOTE]
>  For this property to function properly, it must be configured in both CustomSettings.ini and BootStrap.ini. BootStrap.ini is processed before a deployment share (which contains CustomSettings.ini) has been selected.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*keyboard_locale*|The locale of the keyboard attached to the target computer.<br /><br /> The value can be specified in the following formats:<br /><br /> - Text (en-us)<br /><br /> - Hexadecimal (0409:00000409)|

|**Example 1**|
|-|
|`[Settings] Priority=Default  [Default] KeyboardLocalePE=en-us`|

|**Example 2**|
|-|
|`[Settings] Priority=Default  [Default] KeyboardLocalePE=0409:00000409`|

###  <a name="LanguagePacks"></a> LanguagePacks
 A list of the GUIDs for the language packs to be deployed on the target computer. Deployment Workbench specifies these language packs on the OS Packages node. These GUIDs are stored in the Packages.xml file. The **LanguagePacks** property has a numeric suffix (for example, **LanguagePacks001** or **LanguagePacks002**).

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*language_pack_guid*|The GUID that the Deployment Workbench specifies for the language packs to install on the target computer. The GUID corresponds to the language pack GUID stored in Packages.xml.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] LanguagePacks001={a1923f8d-b07b-44c7-ac1e-353b7cc4c1ad}`|

###  <a name="LoadStateArgs"></a> LoadStateArgs
 The arguments passed to the USMT Loadstate process. The ZTI script inserts the appropriate logging, progress, and state store parameters. If this value is not included in the settings file, the user state restore process is skipped.

 If the Loadstate process finishes successfully, the user state information is deleted. In the event of a Loadstate failure (or non-zero return code), the local state store is moved to %WINDIR%\StateStore to prevent deletion and to ensure that no user state information is lost.

> [!NOTE]
>  Do not add any of the following command-line arguments when configuring this property: **/hardlink**, **/nocompress**, **/decrypt**, **/key**, or **/keyfile**. The MDT scripts will add these command-line arguments if applicable to the current deployment scenario.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|Arguments|The command-line arguments passed to Loadstate.exe.<br /><br /> The default arguments specified by Deployment Workbench are as follows:<br /><br /> - **/v**. Enables verbose output in the Loadstate log. The default is **0**. Specify any number from 0 to 15. The value **5** enables verbose and status output.<br /><br /> - **/c**. When specified, Loadstate will continue to run even if there are nonfatal errors. Without the **/c** option, Loadstate exits on the first error.<br /><br /> - **/lac**. Specifies that if the account being migrated is a local (non-domain) account, and it does not exist on the destination computer, then USMT will create the account but it will be disabled.<br /><br /> For more information about these and other arguments, see the USMT Help files.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSInstall=YES ScanStateArgs=/v:5 /o /c LoadStateArgs=/v:5 /c /lac DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UDShare=\\NYC-AM-FIL-01\MigData$ UDDir=%OSDComputerName%`|

###  <a name="Location"></a> Location
 The geographic location of the target computers. A list of IP addresses that correspond to the default gateways defined for the computers within that location defines the **Location** property. An IP address for a default gateway can be associated with more than one location.

 Typically, the value for the **Location** property is set by performing a database query on the database managed using Deployment Workbench. Deployment Workbench can assist in creating the locations, defining property settings associated with the locations, and then in configuring CustomSettings.ini to perform the database query for the Location property and the property settings associated with the locations.

 For example, a `LocationSettings` section in CustomSettings.ini can query the LocationSettings view in the database for a list of locations that contain the value specified in the **DefaultGateway** property listed in the **Parameters** property. The query returns all settings associated with each default gateway.

 Then the scripts parse each section that corresponds to the locations returned in the query. For example, the value `[Springfield]`and the section `[Springfield-123 Oak Street-4th Floor]` in CustomSettings.ini can represent the corresponding locations. This is an example of how one computer can belong to two locations. The `[Springfield]`section is for all computers in a larger geographic area (an entire city), and the `[Springfield-123 Oak Street-4th Floor]` section is for all computers on the fourth floor at 123 Oak Street, in Springfield.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|          **Value**           |                                    **Description**                                     |
|------------------------------|----------------------------------------------------------------------------------------|
| <em>location1,</em>location2 | The list of locations to be assigned to an individual computer or a group of computers |

|**Example**|
|-|
|`[Settings] Priority=LSettings, Default  [Default] UserDataLocation=AUTO DeployRoot=\\W2K3-SP1\Distribution$ OSInstall=YES ScanStateArgs=/v:15 /o /c LoadStateArgs=/v:7 /c  [LSettings] SQLServer=w2k3-sp1 Instance=MDT2010 Database=MDTDB Netlib=DBNMPNTW SQLShare=SQL$ Table=LocationSettings Parameters=DefaultGateway  [Springfield] UDDir=%OSDComputerName% UDShare=\\Springfield-FIL-01\UserData  [Springfield-123 Oak Street-4th Floor] DeployRoot=\\Springfield-BDD-01\Distribution1$`|

###  <a name="LongDistanceAccess"></a> LongDistanceAccess
 The dialing digits to gain access to an outside line to dial long distance. The property can contain only numeric digits. This value is inserted into the appropriate configuration settings in Unattend.xml.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*language_pack_guid*|The GUID that the Deployment Workbench specifies for the language packs to install on the target computer. The GUID corresponds to the language pack GUID stored in Packages.xml.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] AreaCode=206 CountryCode=001 Dialing=TONE LongDistanceAccess=9`|

###  <a name="MACAddress"></a> MACAddress
 The media access control (MAC) layer address of the primary network adapter of the target computer. The **MACAddress** property is included on the **Priority** line so that property values specific to a target computer can be provided. Create a section for each MAC address for each of the target computers (such as `[00:0F:20:35:DE:AC]`or `[00:03:FF:FE:FF:FF]`) that contain target computer–specific settings.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*mac_address*|The MAC address of the target computer|

|**Example**|
|-|
|`[Settings] Priority=MACAddress, Default  [Default] CaptureGroups=YES Groups1=NYC Application Management Groups2=NYC Help Desk Users  [00:0F:20:35:DE:AC] OSDNEWMACHINENAME=HPD530-1  [00:03:FF:FE:FF:FF] OSDNEWMACHINENAME=BVMXP`|

###  <a name="MachineObjectOU"></a> MachineObjectOU
 The AD DS OU in the target domain where the computer account for the target computer is created.

> [!NOTE]
>  The OU specified in this property must exist before deploying the target operating system.

> [!NOTE]
>  If a computer object already exists in AD DS, specifying **MachineObjectOU** will not cause the computer object to be moved to the specified OU.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*OU\_name*|The name of the OU where the computer account for the target computer will be created|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] JoinDomain=WOODGROVEBANK MachineObjectOU=OU=Reception,OU=NYC,DC=Woodgrovebank,DC=com`|

###  <a name="Make"></a> Make
 The manufacturer of the target computer. The format for **Make** is undefined. Use this property to create a subsection that contains settings targeted to a specific computer manufacturer \(most commonly in conjunction with the **Model** and **Product** properties\).

> [!NOTE]
>  This property is dynamically set by MDT scripts and cannot have its value set in CustomSettings.ini or the MDT DB. Treat this property as read only. However, you can use this property within CustomSettings.ini or the MDT DB, as shown in the following examples, to aid in defining the configuration of the target computer.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*make*|The manufacturer of the target computer|

|**Example**|
|-|
|`[Settings] Priority=Make, Default  [Default]  [Dell Computer Corporation] Subsection=Dell-%Model%  [Dell-Latitude D600] Packages001=XXX00009:Program9 Packages002=XXX0000A:Program10`|

###  <a name="MandatoryApplications"></a> MandatoryApplications
 A list of application GUIDs that will be installed on the target computer. These applications are specified on the Applications node in the Deployment Workbench. The GUIDs are stored in the Applications.xml file. The **MandatoryApplications** property is a list of text values that can be any non\-blank value. The **MandatoryApplications** property has a numeric suffix \(for example, **MandatoryApplications001** or **MandatoryApplications002**\).

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*application\_guid*|The GUID specified by the Deployment Workbench for the application to be deployed to the target computer. The GUID corresponds to the application GUID stored in the Applications.xml file.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] MandatoryApplications001={1D7DF331-47B7-472C-87B3-442597EC2F7D} MandatoryApplications002={9d2b8999-5e4d-4f3d-bb05-edaaf4fe5628} Administrators001=WOODGROVEBANK\NYC Help Desk Staff`|

###  <a name="Memory"></a> Memory
 The amount of memory installed on the target computer in megabytes. For example, the value **2038** indicates 2,038 MB \(or 2 GB\) of memory is installed on the target computer.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*memory*|The amount of memory installed on the target computer in megabytes|

|**Example**|
|-|
|None|

###  <a name="Model"></a> Model
 The model of the target computer. The format for **Model** is undefined. Use this property to create a subsection that contains settings targeted to a specific computer model number for a specific computer manufacturer \(most commonly in conjunction with the **Make** and **Product** properties\).

> [!NOTE]
>  This property is dynamically set by MDT scripts and cannot have its value set in CustomSettings.ini or the MDT DB. Treat this property as read only. However, you can use this property within CustomSettings.ini or the MDT DB, as shown in the following examples, to aid in defining the configuration of the target computer.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*model*|The model of the target computer|

|**Example**|
|-|
|`[Settings] Priority=Make, Default  [Default]  [Dell Computer Corporation] Subsection=Dell-%Model%  [Dell-Latitude D600] Packages001=XXX00009:Program9 Packages002=XXX0000A:Program10`|

###  <a name="NetLib"></a> NetLib
 The protocol to be used to communicate with the computer running SQL Server specified in the **SQLServer** property.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**DBNMPNTW**|Use the named pipes protocol to communicate.|
|**DBMSSOCN**|Use TCP\/IP sockets to communicate.|

|**Example**|
|-|
|`[Settings] Priority=Computers, Default  [Default] ScanStateArgs=/v:5 /o /c LoadStateArgs=/v:5 /c /lac  [Computers] SQLServer=NYC-SQL-01 SQLShare=SQL$ NetLib=DBNMPNTW Database=MDTDB Instance=SQLEnterprise2005 Table=Computers Parameters=SerialNumber, AssetTag ParameterCondition=OR`|

###  <a name="NewDomain"></a> NewDomain
 Indicates the type of a new domain: whether a new domain in a new forest, the root of a new tree in an existing forest, or a child of an existing domain.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|Child|The new domain is a child of an existing domain.|
|Forest|The new domain is the first domain in a new forest of domain trees.|
|Tree|The new domain is the root of a new tree in an existing forest.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] NewDomain=Tree`|

###  <a name="NewDomainDNSName"></a> NewDomainDNSName
 Specifies the required name of a new tree in an existing domain or when Setup installs a new forest of domains.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*name*|Specifies the required name of a new tree in an existing domain or when Setup installs a new forest of domains|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] NewDomainDNSName=newdom.WoodGroveBank.com`|

###  <a name="Order"></a> Order
 The sorting order for the result set on a database query. The result set is based on the configuration settings of the **Database**, **Table**, **SQLServer**, **Parameters**, and **ParameterCondition** properties. More than one property can be provided to sort the results by more than one property.

 For example, if **Order\=Sequence** is specified in the CustomSettings.ini file, then an **ORDER BY** sequence clause is added to the query. **Specifying Order\=Make**, **Model** adds an **ORDER BY Make, Model** clause to the query.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*property1, property2, ...*|Properties to define the sort order for the result set \(where *propertyn* represents the properties in the sort criteria\)|

|**Example**|
|-|
|`[Settings] Priority=Computers, Default  [Default] OSInstall=YES ScanStateArgs=/v:5 /o /c LoadStateArgs=/v:5 /c /lac  [Computers] SQLServer=NYC-SQL-01 SQLShare=SQL$ NetLib=DBNMPNTW Database=MDTDB Instance=SQLEnterprise2005 Table=MakeModelSettings Parameters=SerialNumber, AssetTag ParameterCondition=OR Order=Make, Model`|

###  <a name="OrgName"></a> OrgName
 The name of the organization that owns the target computer. This value is inserted into the appropriate configuration settings in Unattend.xml.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*org\_name*|The name of the organization that owns the target computer|

|**Example**|
|-|
|`[Settings] Priority=MACAddress, Default Properties=CustomProperty, ApplicationInstall  [Default] OSInstall=YES ScanStateArgs=/v:5 /o /c LoadStateArgs=/v:5 /c /lac UserDataLocation=NONE CustomProperty=TRUE OrgName=Woodgrove Bank  [00:0F:20:35:DE:AC] OSDNEWMACHINENAME=HPD530-1 ApplicationInstall=Custom FullName=Woodgrove Bank User  [00:03:FF:FE:FF:FF] OSDNEWMACHINENAME=BVMXP  ApplicationInstall=Minimum FullName=Woodgrove Bank Manager`|

###  <a name="OSArchitecture"></a> OSArchitecture
 The processor architecture type for the target operating system. This property is referenced during OEM deployments. Valid values are **x86** and **x64**.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**x86**|The processor architecture type for the operating system is 32 bit.|
|**x64**|The processor architecture type for the operating system is 64 bit.|

|**Example**|
|-|
|None|

###  <a name="OSCurrentBuild"></a> OSCurrentBuild
 The build number of the currently running operating system.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**7600**|Windows 7|
|**9600**|Windows 8.1|

|**Example**|
|-|
|None|

###  <a name="OSCurrentVersion"></a> OSCurrentVersion
 The version number of the currently running operating system.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*version_number*|The operating system major version, minor version, and build numbers (major.minor.build). For example, 6.3.9600 would represent Windows 8.1.|

|**Example**|
|-|
|None|

###  <a name="OSDAdapterxDescription"></a> OSDAdapterxDescription
 Specifies the name of the network connection as it appears in the Control Panel Network Connections item. The name can be between 0 and 255 characters in length.

 This property is for LTI only. For the equivalent property for ZTI, see [OSDAdapterxName](#OSDAdapterxName).

> [!NOTE]
>  The*x*in this properties name is a placeholder for a zero-based array that contains network adapter information, such as **OSDAdapter0Description** or **OSDAdapter1Description**.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|Description|The name of the network connection as it appears in the Control Panel Network Connections item|

|**Example**|
|-|
|None|

###  <a name="OSDAdapterxDNSDomain"></a> OSDAdapterxDNSDomain
 Specifies the DNS domain name (DNS suffix) that will be assigned to the network connection. This property is for ZTI only. For LTI, see the [OSDAdapterxDNSSuffix](#OSDAdapterxDNSSuffix) property.

> [!NOTE]
>  The*x*in this properties name is a placeholder for a zero-based array that contains network adapter information, such as **OSDAdapter0DNSDomain** or **OSDAdapter1DNSDomain**.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*DNS_domain_name*|A DNS domain name (DNS suffix) that will be assigned to the network connection|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSDAdapter0DNSDomain=WoodGroveBank.com`|

###  <a name="OSDAdapterxDNSServerList"></a> OSDAdapterxDNSServerList
 This is a comma-delimited list of DNS server IP addresses that will be assigned to the network connection.

> [!NOTE]
>  The*x*in this properties name is a placeholder for a zero-based array that contains network adapter information, such as **OSDAdapter0DNSServerList** or **OSDAdapter1DNSServerList**.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*DNS_servers*|A comma-delimited list of DNS server IP addresses that will be assigned to the network connection|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSDAdapter0DNSServerList=192.168.0.254,192.168.100.254`|

###  <a name="OSDAdapterxDNSSuffix"></a> OSDAdapterxDNSSuffix
 A DNS suffix that will be assigned to the network connection. This property is for LTI only. For ZTI, see the [OSDAdapterxDNSDomain](#OSDAdapterxDNSDomain) property.

> [!NOTE]
>  The*x*in this properties name is a placeholder for a zero-based array that contains network adapter information, such as **OSDAdapter0DNSSuffix** or **OSDAdapter1DNSSuffix**.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*DNS_suffix*|A DNS suffix that will be assigned to the network connection|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSDAdapter0DNSSuffix= WoodGroveBank.com`|

###  <a name="OSDAdapterxEnableDHCP"></a> OSDAdapterxEnableDHCP
 Specifies whether the network connection will be configured via DHCP.

> [!NOTE]
>  The*x*in this properties name is a placeholder for a zero-based array that contains network adapter information, such as **OSDAdapter0EnableDHCP** or **OSDAdapter1EnableDHCP**.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|The network connection will be configured via DHCP.|
|**FALSE**|The network connection will be configured with static configuration.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSDAdapter0EnableDHCP=TRUE`|

###  <a name="OSDAdapterxEnableDNSRegistration"></a> OSDAdapterxEnableDNSRegistration
 Specifies whether DNS registration is enabled on the network connection.

> [!NOTE]
>  The*x*in this properties name is a placeholder for a zero-based array that contains network adapter information, such as **OSDAdapter0EnableDNSRegistration** or **OSDAdapter1EnableDNSRegistration**.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|Enables DNS registration|
|**FALSE**|Disables DNS registration|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSDAdapter0EnableDNSRegistration=TRUE`|

###  <a name="OSDAdapterxEnableFullDNSRegistration"></a> OSDAdapterxEnableFullDNSRegistration
 Specifies whether full DNS registration is enabled on the network connection.

> [!NOTE]
>  The*x*in this properties name is a placeholder for a zero-based array that contains network adapter information, such as **OSDAdapter0EnableFullDNSRegistration** or **OSDAdapter1EnableFullDNSRegistration**.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|Enables full DNS registration|
|**FALSE**|Disables full DNS registration|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSDAdapter0EnableFullDNSRegistration=TRUE`|

###  <a name="OSDAdapterxEnableLMHosts"></a> OSDAdapterxEnableLMHosts
 Specifies whether LMHOSTS lookup is enabled on the network connection.

> [!NOTE]
>  The*x*in this properties name is a placeholder for a zero-based array that contains network adapter information, such as **OSDAdapter0EnableLMHosts** or **OSDAdapter1EnableLMHosts**.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|Enables LMHOSTS lookup|
|**FALSE**|Disables LMHOSTS lookup|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSDAdapter0EnableLMHosts=TRUE`|

###  <a name="OSDAdapterxEnableIPProtocolFiltering"></a> OSDAdapterxEnableIPProtocolFiltering
 This property specifies whether IP protocol filtering should be enabled on the network connection.

 The*x*in this property's name is a placeholder for a zero-based array that contains network adapter information, such as *OSDAdapter0EnableIPProtocolFiltering* or **OSDAdapter1EnableIPProtocolFiltering**.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|Enables IP protocol filtering|
|**FALSE**|Disables IP protocol filtering|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSDAdapter0EnableIPProtocolFiltering =TRUE`|

###  <a name="OSDAdapterxEnableTCPFiltering"></a> OSDAdapterxEnableTCPFiltering
 Specifies whether TCP\/IP filtering should be enabled on the network connection. This property is for ZTI only. For LTI, see the [OSDAdapterxEnableTCPIPFiltering](#OSDAdapterxEnableTCPIPFiltering) property.

> [!NOTE]
>  The*x*in this property's name is a placeholder for a zero\-based array that contains network adapter information, such as **OSDAdapter0EnableTCPFiltering** or **OSDAdapter1EnableTFiltering**.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|Enables TCP\/IP filtering|
|**FALSE**|Disables TCP\/IP filtering|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSDAdapter0EnableTCPFiltering=TRUE`|

###  <a name="OSDAdapterxEnableTCPIPFiltering"></a> OSDAdapterxEnableTCPIPFiltering
 Specifies whether TCP\/IP filtering should be enabled on the network connection. This property is for LTI only. For ZTI, see the [OSDAdapterxEnableTCPFiltering](#OSDAdapterxEnableTCPFiltering) property.

> [!NOTE]
>  The*x*in this properties name is a placeholder for a zero\-based array that contains network adapter information, such as **OSDAdapter0EnableTCPIPFiltering** or **OSDAdapter1EnableTCPIPFiltering**.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|Enables TCP\/IP filtering|
|**FALSE**|Disables TCP\/IP filtering|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSDAdapter0EnableTCPIPFiltering=TRUE`|

###  <a name="OSDAdapterxEnableWINS"></a> OSDAdapterxEnableWINS
 Specifies whether WINS will be enabled on the network connection.

> [!NOTE]
>  The*x*in this properties name is a placeholder for a zero\-based array that contains network adapter information, such as **OSDAdapter0EnableWINS** or **OSDAdapter1EnableWINS**.

> [!CAUTION]
>  This property value must be specified in uppercase letters so that the deployment scripts can properly read it.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|Enables WINS|
|**FALSE**|Disables WINS|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSDAdapter0EnableWINS=TRUE OSDAdapter0WINSServerList=192.168.0.1,192.168.100.1`|

###  <a name="OSDAdapterxGatewayCostMetric"></a> OSDAdapterxGatewayCostMetric
 A comma\-delimited list of Gateway Cost Metrics specified as either integers or the string "Automatic" \(if empty, uses "Automatic"\) that will be configured on the connection.

> [!NOTE]
>  The*x*in this properties name is a placeholder for a zero\-based array that contains network adapter information, such as **OSDAdapter0GatewayCostMetric** or **OSDAdapter1GatewayCostMetric**.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*cost\_metrics*|A comma\-delimited list of Gateway Cost Metrics|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSDAdapter0GatewayCostMetrics=Automatic`|

###  <a name="OSDAdapterxGateways"></a> OSDAdapterxGateways
 A comma\-delimited list of gateways to be assigned to the network connection.

> [!NOTE]
>  The*x*in this properties name is a placeholder for a zero\-based array that contains network adapter information, such as **OSDAdapter0Gateways** or **OSDAdapter1Gateways**.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*gateways*|A comma\-delimited list of gateways|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSDAdapter0Gateways=192.168.0.1,192.168.100.1`|

###  <a name="OSDAdapterxIPAddressList"></a> OSDAdapterxIPAddressList
 A comma\-delimited list of IP addresses to be assigned to the network connection.

> [!NOTE]
>  The*x*in this properties name is a placeholder for a zero\-based array that contains network adapter information, such as **OSDAdapter0IPAddressList** or **OSDAdapter1IPAddressList**.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*IP\_addresses*|A comma delimited list of IP addresses|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSDAdapter0IPAddressList=192.168.0.40,192.168.100.40 OSDAdapter0SubnetMask=255.255.255.0,255.255.255.0`|

###  <a name="OSDAdapterxIPProtocolFilterList"></a> OSDAdapterxIPProtocolFilterList
 A comma\-delimited list of IP protocol filters to be assigned to the network connection. This property can be configured using the CustomSettings.ini file or the MDT DB but not the Deployment Workbench. If using Configuration Manager it is also configurable using an **Apply Network Settings** task sequence step.

> [!NOTE]
>  The*x*in this properties name is a placeholder for a zero\-based array that contains network adapter information, such as **OSDAdapter0IPProtocolFilterList** or **OSDAdapter1IPProtocolFilterList**.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*protocol\_filter\_list*|A comma\-delimited list of IP protocol filters|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSDAdapter0IPProtocolFilterList=a list of approved IP protocols`|

###  <a name="OSDAdapterxMacAddress"></a> OSDAdapterxMacAddress
 Assign the specified configuration settings to the network interface card that matches the specified MAC address.

> [!NOTE]
>  The*x*in this properties name is a placeholder for a zero\-based array that contains network adapter information, such as **OSDAdapter0MacAddress** or **OSDAdapter1MacAddress**.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*MAC\_address*|Network adapter MAC address|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSDAdapter0MacAddress=00:0C:29:67:A3:6B`|

###  <a name="OSDAdapterxName"></a> OSDAdapterxName
 Assign the specified configuration settings to the network adapter that matches the specified name. This property is for ZTI only. For the equivalent property for LTI, see [OSDAdapterxDescription](#OSDAdapterxDescription).

> [!NOTE]
>  The*x*in this properties name is a placeholder for a zero\-based array that contains network adapter information, such as **OSDAdapter0Name** or **OSDAdapter1Name**.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*name*|Network adapter name|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSDAdapter0Name=3Com 3C920 Integrated Fast Ethernet Controller`|

###  <a name="OSDAdapterxSubnetMask"></a> OSDAdapterxSubnetMask
 A comma\-delimited list of IP subnet masks to be assigned to the network connection.

> [!NOTE]
>  The*x*in this properties name is a placeholder for a zero\-based array that contains network adapter information, such as **OSDAdapter0SubnetMask** or **OSDAdapter1SubnetMask**.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*subnet\_masks*|A comma\-delimited list of IP subnet masks|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSDAdapter0IPAddressList=192.168.0.40,192.168.100.40 OSDAdapter0SubnetMask=255.255.255.0,255.255.255.0`|

### OSDAdapterxTCPFilterPortList
 A comma\-delimited list of TCP filter ports to be assigned to the network connection. This property can be configured using the CustomSettings.ini file or the MDT DB but not the Deployment Workbench. If using Configuration Manager it is also configurable using an **Apply Network Settings** task sequence step.

> [!NOTE]
>  The*x*in this properties name is a placeholder for a zero\-based array that contains network adapter information, such as **OSDAdapter0TCPFilterPortList** or **OSDAdapter1TCPFilterPortList**.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*port\_list*|A comma\-delimited list of TCP\/IP filter ports|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSDAdapter0TCPFilterPortList=a list of approved TCP ports`|

###  <a name="OSDAdapterxTCPIPNetBiosOptions"></a> OSDAdapterxTCPIPNetBiosOptions
 Specifies the TCP\/IP NetBIOS options to be assigned to the network connection.

> [!NOTE]
>  The*x*in this properties name is a placeholder for a zero\-based array that contains network adapter information, such as **OSDAdapter0TCPIPNetBiosOptions** or **OSDAdapter1TCPIPNetBiosOptions**.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**0**|Disable IP forwarding.|
|**1**|Enable IP forwarding.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSDAdapter0TCPIPNetBiosOptions=0`|

###  <a name="OSDAdapterxUDPFilterPortList"></a> OSDAdapterxUDPFilterPortList
 A comma\-delimited list of User Datagram Protocol \(UDP\) filter ports to be assigned to the network connection. This property can be configured using the CustomSettings.ini file and the MDT DB but not the Deployment Workbench. If using Configuration Manager it is also configurable using an **Apply Network Settings** task sequence step.

> [!NOTE]
>  The*x*in this properties name is a placeholder for a zero\-based array that contains network adapter information, such as **OSDAdapter0UDPFilterPortList** or **OSDAdapter1UDPFilterPortList**.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*port\_list*|A comma\-delimited list of UDP filter ports|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSDAdapter0UDPFilterPortList=a list of approved UDP ports`|

###  <a name="OSDAdapterxWINSServerList"></a> OSDAdapterxWINSServerList
 A two\-element, comma\-delimited list of WINS server IP addresses to be assigned to the network connection.

> [!NOTE]
>  The*x*in this properties name is a placeholder for a zero\-based array that contains network adapter information, such as **OSDAdapter0WINSServerList** or **OSDAdapter1WINSServerList**.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*WINS\_server\_list*|A comma\-delimited list of WINS server IP addresses|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSDAdapter0EnableWINS=TRUE OSDAdapter0WINSServerList=192.168.0.1,192.168.100.1`|

###  <a name="OSDAdapterCount"></a> OSDAdapterCount
 Specifies the number of network connections that are to be configured.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|count|The number of network adapters|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSDAdapterCount=1 OSDAdapter0EnableDHCP=FALSE OSDAdapter0IPAddressList=192.168.0.40,192.168.100.40 OSDAdapter0SubnetMask=255.255.255.0,255.255.255.0 OSDAdapter0Gateways=192.168.0.1,192.168.100.1 OSDAdapter0EnableWINS=TRUE OSDAdapter0WINSServerList=192.168.0.1,192.168.100.1 OSDAdapter0TCPIPNetBiosOptions=0 OSDAdapter0MacAddress=00:0C:29:67:A3:6B OSDAdapter0GatewayCostMetrics=Automatic OSDAdapter0EnableTCPIPFiltering=TRUE OSDAdapter0EnableLMHosts=TRUE OSDAdapter0EnableFullDNSRegistration=TRUE OSDAdapter0EnableDNSRegistration=TRUE OSDAdapter0DNSSuffix=WoodGroveBank.com`|

### OSDAnswerFilePath
 Specifies the path to the answer file to be used during OEM deployments.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*file\_path*|Specifies the path to the answer file to be used during OEM deployments|

|**Example**|
|-|
|None|

###  <a name="OSDBitLockerCreateRecoveryPassword"></a> OSDBitLockerCreateRecoveryPassword
 A Boolean value that indicates whether the process creates a recovery key for BitLocker. The key is used for recovering data encrypted on a BitLocker volume. This key is cryptographically equivalent to a startup key. If available, the recovery key decrypts the VMK, which, in turn, decrypts the FVEK.

> [!NOTE]
>  This property value must be specified in uppercase letters so that the deployment scripts can properly read it.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**AD**|A recovery key is created.|
|Not specified|A recovery key is not created.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] BDEInstallSuppress=NO BDEDriveLetter=S: BDEDriveSize=2000 OSDBitLockerMode=TPMKey OSDBitLockerCreateRecoveryPassword=AD OSDBitLockerStartupKeyDrive=C:`|

###  <a name="OSDBitLockerMode"></a> OSDBitLockerMode
 The type of BitLocker installation to be performed. Protect the target computer using one of the following methods:

-   A TPM microcontroller

-   A TPM and an external startup key \(using a key that is typically stored on a UFD\)

-   A TPM and PIN

-   An external startup key

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TPM**|Protect the computer with TPM only. The TPM is a microcontroller that stores keys, passwords, and digital certificates. The microcontroller is typically an integral part of the computer motherboard.|
|**TPMKey**|Protect the computer with TPM and a startup key. Use this option to create a startup key and to save it on a UFD. The startup key must be present in the port each time the computer starts.|
|**TPMPin**|Protect the computer with TPM and a pin. Use this option in conjunction with the **BDEPin** property.<br /><br /> Note:<br /><br /> This value is not valid when using ZTI.|
|**Key**|Protect the computer with an external key \(the recovery key\) that can be stored in a folder, in AD DS, or printed.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] BDEInstallSuppress=NO BDEDriveLetter=S: BDEDriveSize=2000 OSDBitLockerMode=TPM OSDBitLockerCreateRecoveryPassword=AD`|

###  <a name="OSDBitLockerRecoveryPassword"></a> OSDBitLockerRecoveryPassword
 Instead of generating a random recovery password, the **Enable BitLocker** task sequence action uses the specified value as the recovery password. The value must be a valid numerical BitLocker recovery password.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*password*|A valid 48\-digit password|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] BDEInstallSuppress=NO BDEDriveLetter=S: BDEDriveSize=2000 OSDBitLockerMode=TPMKey OSDBitLockerCreateRecoveryPassword=AD OSDBitLockerRecoveryPassword=621280128854709621167486709731081433315062587367 OSDBitLockerStartupKeyDrive=C:`|

###  <a name="OSDBitLockerStartupKey"></a> OSDBitLockerStartupKey
 Instead of generating a random startup key for the key management option **Startup Key on USB only**, the **Enable BitLocker** task sequence action uses the value as the startup key. The value must be a valid, Base64\-encoded BitLocker startup key.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*startupkey*|Base64\-encoded BitLocker startup key|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] BDEInstallSuppress=NO BDEDriveLetter=S: BDEDriveSize=2000 BDEInstall=KEY OSDBitLockerCreateRecoveryPassword=AD OSDBitLockerStartupKey=8F4922B8-2D8D-479E-B776-12629A361049`|

###  <a name="OSDBitLockerStartupKeyDrive"></a> OSDBitLockerStartupKeyDrive
 The location for storing the BitLocker recovery key and startup key.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*location*|The storage location for the recovery key and startup key \(either local to the target computer or to a UNC that points to a shared network folder\)|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] BDEInstallSuppress=NO BDEDriveLetter=S: BDEDriveSize=2000 OSDBitLockerMode=TPMKey OSDBitLocker CreateRecoveryPassword=AD OSDBitLockerStartupKeyDrive=C:`|

###  <a name="OSDBitLockerTargetDrive"></a> OSDBitLockerTargetDrive
 Specifies the drive to be encrypted. The default drive is the drive that contains the operating system.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*drive*|The drive that is to be encrypted|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] BDEInstallSuppress=NO BDEDriveLetter=S: BDEDriveSize=2000 BDERecoveryPassword=TRUE OSDBitLockerMode=TPMKey OSDBitLockerCreateRecoveryPassword=AD OSDBitLockerTargetDrive=C:`|

###  <a name="OSDBitLockerWaitForEncryption"></a> OSDBitLockerWaitForEncryption
 Specifies that the deployment process should not proceed until BitLocker has completed the encryption process for all specified drives. Specifying TRUE could dramatically increase the time required to complete the deployment process.

> [!CAUTION]
>  This property value must be specified in uppercase letters so that the deployment scripts can properly read it.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|Specifies that the deployment process should wait for drive encryption to finish|
|**FALSE**|Specifies that the deployment process should not wait for drive encryption to finish|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] BDEInstallSuppress=NO BDEDriveLetter=S: BDEDriveSize=2000 OSDBitLockerMode=TPMKey OSDBitLockerStartupKeyDrive=C: OSDBitLockerCreateRecoveryPassword=AD OSDBitLockerWaitForEncryption=TRUE`|

###  <a name="OSDComputerName"></a> OSDComputerName
 The new computer name to assign to the target computer.

> [!NOTE]
>  This property can also be set within a task sequence using a customized **Set Task Sequence Variable** task sequence step.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*computer\_name*|The new computer name to assign to the target computer|

|**Example**|
|-|
|`[Default] OSDComputerName=%_SMSTSMachineName%`|

###  <a name="OSDDiskAlign"></a> OSDDiskAlign
 This property is used to pass a value to the **align** parameter of the **create partition primary** command in the **DiskPart** command. The **align** parameter is typically used with hardware RAID Logical Unit Number \(LUN\) arrays to improve performance when the logical units \(LUs\) are not cylinder aligned. The **align** parameter aligns a primary partition that is not cylinder aligned at the beginning of a disk and rounds the offset to the closest alignment boundary. For more information on the **align** parameter, see [Create partition primary](https://technet.microsoft.com/library/cc771243\(WS.10\).aspx).

> [!NOTE]
>  This property can be used in conjunction with the **OSDDiskOffset** property to set the **offset** parameter for the **create partition primary** command in the **DiskPart** command. For more information, see the [OSDDiskOffset](#OSDDiskOffset) property.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*alignment\_value*|Specifies the number of kilobytes \(KB\) from the beginning of the disk to the closest alignment boundary.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSDDiskAlign=1024 OSDDiskOffset=2048`|

###  <a name="OSDDiskIndex"></a> OSDDiskIndex
 Specifies the disk index that will be configured.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*disk\_index*|Specifies the disk index that will be configured \(The default value is **0**.\)|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSDDiskIndex=0`|

###  <a name="OSDDiskOffset"></a> OSDDiskOffset
 This property is used to pass a value to the **offset** parameter of the **create partition primary** command in the **DiskPart** command. For more information on the **offset** parameter, see [Create partition primary](https://technet.microsoft.com/library/cc771243\(WS.10\).aspx).

 This property can be used in conjunction with the **OSDDiskAlign** property to set the **align** parameter for the **create partition primary** command in the **DiskPart** command. For more information, see the [OSDDiskAlign](#OSDDiskAlign) property.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*offset\_value*|Specifies the byte offset at which to create the partition. For master boot record \(MBR\) disks, the offset rounds to the closest cylinder boundary.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSDDiskAlign=1024 OSDDiskOffset=2048`|

###  <a name="OSDDiskPartBiosCompatibilityMode"></a> OSDDiskPartBiosCompatibilityMode
 This property specifies whether to disable cache alignment optimizations when partitioning the hard disk for compatibility with certain types of BIOS.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|Enables cache alignment optimizations when partitioning the hard disk for compatibility with certain types of BIOS|
|**FALSE**|Disables cache alignment optimizations when partitioning the hard disk for compatibility with certain types of BIOS \(This is the default value.\)|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSDDiskPartBiosCompatibilityMode=TRUE`|

###  <a name="OSDImageCreator"></a> OSDImageCreator
 Specifies the name of the installation account that will be used during OEM deployments.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*image\_creator*|Specifies the name of the installation account that will be used during OEM deployments|

|**Example**|
|-|
|None|

###  <a name="OSDImageIndex"></a> OSDImageIndex
 Specifies the index of the image in the .wim file. This property is referenced during OEM deployments.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*index*|Specifies the index of the image in the WIM file|

|**Example**|
|-|
|None|

###  <a name="OSDImagePackageID"></a> OSDImagePackageID
 Specifies the package ID for the image to install during OEM deployments.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*package\_ID*|Specifies the package ID for the image to install during OEM deployments|

|**Example**|
|-|
|None|

###  <a name="OSDInstallEditionIndex"></a> OSDInstallEditionIndex
 Specifies the index of the image in the WIM file. This property is referenced during OEM deployments.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*index*|Specifies the index of the image in the WIM file|

|**Example**|
|-|
|None|

###  <a name="OSDInstallType"></a> OSDInstallType
 Specifies the installation type used for OEM deployments. The default is **Sysprep**.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*install\_type*|Specifies the installation type used for OEM deployments|

|**Example**|
|-|
|None|

###  <a name="OSDisk"></a> OSDisk
 Specifies the drive used to install the operating system during OEM deployments. The default value is **C:**.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*disk*|Specifies the drive used to install the operating system during OEM deployments|

|**Example**|
|-|
|None|

###  <a name="OSDPartitions"></a> OSDPartitions
 Specifies the number of defined partitions configurations. The maximum number of partitions that can be configured is two. The default is **None**.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*partitions*|Specifies the number of defined partitions configurations|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSDPartitions=1 OSDPartitions0Bootable=TRUE OSDPartitions0FileSystem=NTFS OSDPartitions0QuickFormat=TRUE OSDPartitions0Size=60 OSDPartitions0SizeUnits=GB OSDPartitions0Type=Primary OSDPartitions0VolumeName=OSDisk OSDPartitions0VolumeLetterVariable=NewDrive1`|

###  <a name="OSDPartitionsxBootable"></a> OSDPartitionsxBootable
 The partition at the specified index should be set bootable. The default first partition is set bootable.

> [!NOTE]
>  The*x* in this properties name is a placeholder for a zero-based array that contains partition configurations.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|The partition should be set to bootable.|
|**FALSE**|Do not set the partition to bootable.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSDPartitions0Bootable=TRUE`|

###  <a name="OSDPartitionsxFileSystem"></a> OSDPartitionsxFileSystem
 The type of file system for the partition at the specified index. Valid values are **NTFS** or **FAT32**.

> [!NOTE]
>  The*x* in this properties name is a placeholder for a zero-based array that contains partition configurations.

> [!CAUTION]
>  This property value must be specified in uppercase letters so that the deployment scripts can properly read it.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*file_system*|The type of file system for the partition|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSDPartitions0FileSystem=NTFS`|

###  <a name="OSDPartitionsxQuickFormat"></a> OSDPartitionsxQuickFormat
 The partition at the specified index should be quick formatted. The default is **TRUE**.

> [!NOTE]
>  The*x* in this properties name is a placeholder for a zero-based array that contains partition configurations.

> [!CAUTION]
>  This property value must be specified in uppercase letters so that the deployment scripts can properly read it.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|Quick-format the partition.|
|**FALSE**|Do not quick-format the partition.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSDPartitions0QuickFormat=TRUE`|

###  <a name="OSDPartitionsxSize"></a> OSDPartitionsxSize
 The size of the partition at the specified index.

> [!NOTE]
>  The*x* in this properties name is a placeholder for a zero-based array that contains partition configurations.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*Size*|Partition size|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSDPartitions0Size=60 OSDPartitions0SizeUnits=GB`|

###  <a name="OSDPartitionsxSizeUnits"></a> OSDPartitionsxSizeUnits
 The units of measure used when specifying the size of the partition. Valid values are **MB**, **GB**, or **%**. The default value is **MB**.

> [!NOTE]
>  The*x* in this properties name is a placeholder for a zero-based array that contains partition configurations.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*size_units*|The units of measure used when specifying the size of the partition|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSDPartitions0Size=60 OSDPartitions0SizeUnits=GB`|

###  <a name="OSDPartitionsxType"></a> OSDPartitionsxType
 The type of partition to be created at the specified index.

> [!NOTE]
>  The*x* in this properties name is a placeholder for a zero-based array that contains partition configurations.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**Primary**|Create a primary partition. This is the default value.|
|**Logical**|Create a logical partition.|
|**Extended**|Create an extended partition.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSDPartitions0Type=Primary`|

###  <a name="OSDPartitionsxVolumeLetterVariable"></a> OSDPartitionsxVolumeLetterVariable
 The property that receives the drive letter that is assigned to the partition being managed.

> [!NOTE]
>  The*x* in this properties name is a placeholder for a zero-based array that contains partition configurations.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*volume_letter_variable*|The name of the variable that will be assigned the drive letter of the partition being managed|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSDPartitions0VolumeLetterVariable=NewDrive1`|

###  <a name="OSDPartitionsxVolumeName"></a> OSDPartitionsxVolumeName
 The volume name that will be assigned to the partition at the specified index.

> [!NOTE]
>  The*x* in this properties name is a placeholder for a zero-based array that contains partition configurations.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*volume_name*|The volume name that will be assigned to the partition|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSDPartitions0VolumeName=OSDisk`|

###  <a name="OSDPreserveDriveLetter"></a> OSDPreserveDriveLetter
 This property is used to determine whether the **Apply OS** task sequence step should preserve the drive letter in the operating system image file (.wim file) being deployed to the target computer.

> [!NOTE]
>  This property should only be set in a task sequence step, not in the CustomSettings.ini file or in the MDT DB.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|The drive letters in the operating system image file (.wim file) and the operating system drives letters after deployment are identical to the drive letters in the .wim file.|
|**FALSE**|The drive letters in the operating system image file (.wim file) are ignored, which allows the task sequence to override the driver letters in the .wim file.<br /><br /> Note:<br /><br /> For MDT, this value should always be selected.|

|**Example**|
|-|
|None|

###  <a name="OSDStateStorePath"></a> OSDStateStorePath
 LTI and ZTI use this property to set the path where the user state migration data will be stored, which can be a UNC path, a local path, or a relative path.

> [!NOTE]
>  The **OSDStateStorePath** property takes precedence over the [StatePath](#StatePath) or [UserDataLocation](#UserDataLocation) property when those properties are also specified.

 In a Replace Computer deployment scenario in ZTI, the [Restore User State](#RestoreUserState) task sequence step is skipped if the **OSDStateStorePath** property is set to a valid local or UNC path. The workaround is to set the [USMTLocal](#USMTLocal) property to TRUE. Doing so forces ZTI UserState.wsf to recognize the path in the [OSDStateStorePath](#OSDStateStorePath) property. This is caused by the **Request State Store** task sequence step being skipped and the previous value in the **OSDStateStorePath** property being retained.

 In a Replace Computer deployment scenario in ZTI, where user state migration data and the entire computer are being backed up, the Backup.wim file is stored in the folder specified in the **OSDStateStorePath** property. This may be caused by specifying the wrong value for the [ComputerBackupLocation](#ComputerBackupLocation) property.

 For example, the following CustomSettings.ini file will cause the Backup.wim file to be stored in the same folder specified in the **OSDStateStorePath** property:

```
USMTLocal=True
OSDStateStorePath=\\fs1\Share\Replace

ComputerBackupLocation=NETWORK
BackupShare=\\fs1\Share\ComputerBackup
BackupDir=Client01
```

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*Path*|The path where the user state migration data will be stored, which can be a UNC path, a local path, or a relative path|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] USMTLocal=True OSDStateStorePath=\\fs1\Share\Replace ComputerBackupLocation=\\fs1\Share\ComputerBackup\Client01`|

###  <a name="OSDTargetSystemDrive"></a> OSDTargetSystemDrive
 Specifies the drive where the operating system will be installed during OEM deployments.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read-only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*system_drive*|Specifies the drive where the operating system will be installed during OEM deployments|

|**Example**|
|-|
|None|

###  <a name="OSDTargetSystemRoot"></a> OSDTargetSystemRoot
 Specifies the install path where the operating system will be installed during OEM deployments.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*system_root*|Specifies the install path where the operating system will be installed during OEM deployments|

|**Example**|
|-|
|None|

###  <a name="OSFeatures"></a> OSFeatures
 A comma-delimited list of server feature IDs that will be installed on the target computer.

> [!NOTE]
>  Not all features listed in the ServerManager.xml file are compatible with all server operating systems.

> [!CAUTION]
>  This property value must be specified in uppercase letters so that the deployment scripts can properly read it.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*ID1,ID2*|The server features that are to be installed on the target computer. Valid values are located in the *program_files*\Microsoft Deployment Toolkit\Bin\ServerManager.xml file on the MDT server.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSFeatures=CMAK,MSMQ-Multicasting,RSAT`|

###  <a name="OSInstall"></a> OSInstall
 Indicates whether the target computer is authorized to have the target operating system installed. If the **OSInstall** property is not listed, the default is to allow deployment of operating systems to any target computer.

> [!CAUTION]
>  This property value must be specified in uppercase letters so that the deployment scripts can properly read it.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**YES**|Deployment of an operating system to the target computer is authorized. This is the default value.|
|**NO**|Deployment of an operating system to the target computer is not authorized.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSInstall=YES`|

###  <a name="OSRoles"></a> OSRoles
 A comma-delimited list of server role IDs that will be installed on the target computer.

> [!NOTE]
>  Not all roles are compatible with all server operating systems.

> [!CAUTION]
>  This property value must be specified in uppercase letters so that the deployment scripts can properly read it.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*ID1,ID2*|The server role that is to be installed on the target computer.|

 See "C:\Program Files\Microsoft Deployment Toolkit\Bin\ServerManager.xml" for valid ID values.

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSRoles=ADDS`|

###  <a name="OSRoleServices"></a> OSRoleServices
 A comma-delimited list of server role service IDs that will be installed on the target computer.

> [!NOTE]
>  Not all server role service IDs are compatible with all server operating systems.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*ID*|The server role service that will be installed on the target computer. The valid value is:<br /><br /> - **ADDS-Domain-Controller**|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSRoleServices=ADDS-Domain-Controller`|

###  <a name="OSSKU"></a> OSSKU
 The edition of the currently running operating system. The operating system edition is determined by using the **OperatingSystemSKU** property of the **Win32_OperatingSystem WMI** class. For a list of the editions the **OperatingSystemSKU** property returns, see the section, "OperatingSystemSKU," at [Win32_OperatingSystem class](https://msdn.microsoft.com/library/windows/desktop/aa394239\(v=vs.85\).aspx).

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*edition*|The operating system edition. For example, "BUSINESS" for a Business edition of an operating system or "ENTERPRISE" for an Enterprise edition of an operating system.|

|**Example**|
|-|
|None|

###  <a name="OSVersion"></a> OSVersion
 The version of the currently running operating system. This property should only be used to detect if the currently running operating system is Windows PE. Use the [OSVersionNumber](#OSVersionNumber) property to detect other operating systems.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**WinPE**|Windows PE|
|**2008R2**|Windows Server 2008 R2|
|**Win7Client**|Windows 7|
|**Other**|Operating systems other than those listed, including Windows 8 and Windows Server 2012|

|**Example**|
|-|
|None|

###  <a name="OSVersionNumber"></a> OSVersionNumber
 The operating system major and minor version number. This property is referenced during OEM deployments.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*version_number*|The operating system major and minor version number|

|**Example**|
|-|
|None|

###  <a name="OverrideProductKey"></a> OverrideProductKey
 The Multiple Activation Key (MAK) string to be applied after the target operating is deployed to the target computer. The value specified in this property is used by the ZTILicensing.wsf script during the State Restore Phase to apply the MAK to the target operating system. The script also configures the volume licensing image to use MAK activation instead of Key Management Service (KMS). The operating system needs to be activated with Microsoft after the MAK is applied. This is used when the target computer is unable to access a server that is running KMS.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*MAK*|The MAK string to be provided to the target operating system|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] ProductKey=AAAAA-BBBBB-CCCCC-DDDDD-EEEEE-FFFFF OverrideProductKey=AAAAA-BBBBB-CCCCC-DDDDD-EEEEE-FFFFF`|

###  <a name="PackageGroup"></a> PackageGroup
 A list of text values that associates operating system packages with each other (typically based on the type of operating system package). An operating system package can be associated with one or more package groups. The **PackageGroup** property allows the operating system packages within one or more groups to be deployed to a target computer.

 The text values in the list can be any non-blank value. The **PackageGroup** property value has a numeric suffix (for example, **PackageGroup001** or **PackageGroup002**). After it is defined, a package group is associated with a computer. A computer can be associated with more than one package group.

> [!NOTE]
>  Operating system packages are created on the OS Packages node in the Deployment Workbench.

> [!NOTE]
>  The **PackageGroup** property can be specified in the format *PackageGroup1=Updates* or *PackageGroup001=Updates*.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*package_group_name*|Name of the package group to be deployed to the target computer|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] PackageGroup001=Updates`|

###  <a name="Packages"></a> Packages
 The list of Configuration Manager packages to be deployed to the target computer. The **Packages** property has a numeric suffix (for example, Packages001 or Packages002).

> [!NOTE]
>  The **PackageGroup** property can be specified in the format *PackageGroup1=Updates* or *PackageGroup001=Updates*.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*package_id:program_name*|Name of the package to be deployed to the target computer|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] Packages001=NYC00010:Install Packages002=NYC00011:Install`|

###  <a name="PackageSelectionProfile"></a> PackageSelectionProfile
 Profile name used during package installation.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*profile_name*|Profile name used during package installation|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] PackageSelectionProfile=CoreApplications`|

###  <a name="Parameters"></a> Parameters
 The parameters to be passed to a database query that returns property values from columns in the table specified in the **Table** property. The table is located in the database specified in the **Database** property on the computer specified in the **SQLServer** property. The instance of SQL Server on the computer is specified in the **Instance** property.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*parameter1, parameter2*|The list of parameters to pass to the database query|

|**Example**|
|-|
|`[Settings] Priority=Computers, Default  [Default] OSInstall=YES  [Computers] SQLServer=NYC-SQL-01 SQLShare=SQL$ Database=MDTDB Instance=SQLEnterprise2005 Table=Computers Parameters=SerialNumber, AssetTag ParameterCondition=OR`|

###  <a name="ParameterCondition"></a> ParameterCondition
 Indicator of whether a Boolean AND or OR operation is performed on the properties listed in the **Parameters** property.

> [!CAUTION]
>  This property value must be specified in uppercase letters so that the deployment scripts can properly read it.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**AND**|A Boolean AND operation is performed on the properties listed in the **Parameters** property. Only results that match all properties specified in the **Parameters** property are returned. This is the default value.|
|**OR**|A Boolean OR operation is performed on the properties listed in the **Parameters** property. Results that match any property specified in the **Parameters** property are returned.|

|**Example**|
|-|
|`[Settings] Priority=Computers, Default  [Default] OSInstall=YES  [Computers] SQLServer=NYC-SQL-01 SQLShare=SQL$ Database=MDTDB Instance=SQLEnterprise2005 Table=Computers Parameters=SerialNumber, AssetTag ParameterCondition=OR`|

###  <a name="ParentDomainDNSName"></a> ParentDomainDNSName
 Specifies the DNS domain name of an existing directory service domain when installing a child domain.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*name*|Specifies the DNS domain name of an existing directory service domain when installing a child domain|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] ParentDomainDNSName=WoodGroveBank.com`|

###  <a name="Password"></a> Password
 Specifies the password for the user name (account credentials) to use for promoting the member server to a domain controller.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*password*|Specifies the password for the user name (account credentials) to use for promoting the member server to a domain controller|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] Password=<complex_password>`|

###  <a name="Phase"></a> Phase
 The current phase of the deployment process. The Task Sequencer uses these phases to determine which tasks must be completed.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

> [!CAUTION]
>  This property value must be specified in uppercase letters so that the deployment scripts can properly read it.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**VALIDATION**|Identifies that the target computer is capable of running the scripts necessary to complete the deployment process.|
|**STATECAPTURE**|Saves any user state migration data before deploying the new target operating system.|
|**PREINSTALL**|Completes any tasks that need to be done (such as creating new partitions) before the target operating system is deployed.|
|**INSTALL**|Installs the target operating system on the target computer.|
|**POSTINSTALL**|Completes any tasks that need to be done before restoring the user state migration data. These tasks customize the target operating system before starting the target computer the first time (such as installing updates or adding drivers).|
|**STATERESTORE**|Restores the user state migration data saved during the State Capture Phase.|

|**Example**|
|-|
|None|

###  <a name="Port"></a> Port
 The number of the port that should be used when connecting to the SQL Server database instance that is used for querying property values from columns in the table specified in the **Table** property. The database resides on the computer specified in the **SQLServer** property. The instance of SQL Server on the computer is specified in the **Instance** property. The port used during connection is specified in the **Port** property.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*port*|The number of the port used when connecting to SQL Server|

|**Example**|
|-|
|`[Settings] Priority=Computers, Default  [Default] OSInstall=YES  [Computers] SQLServer=NYC-SQL-01 Database=MDTDB Instance=MDT2010 Port=1433 Table=Computers Parameters=SerialNumber, AssetTag ParameterCondition=OR`|

###  <a name="PowerUsers"></a> PowerUsers
 A list of user accounts and domain groups to be added to the local Power Users group on the target computer. The **PowerUsers** property is a list of text values that can be any non-blank value. The **PowerUsers** property has a numeric suffix (for example, **PowerUsers1** or **PowerUsers2**).

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*name*|Name of the user or group to be added to the local Power Users group|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] Administrators001=WOODGROVEBANK\NYC Help Desk Staff PowerUsers001=WOODGROVEBANK\User01 PowerUsers002=WOODGROVEBANK\User02`|

###  <a name="PrepareWinRE"></a> PrepareWinRE
 This property specifies if the LiteTouchPE.wim file, which includes Windows RE and optionally DaRT, is applied to the system drive as the recovery partition. This allows the target computer to use the LiteTouchPE.wim image to perform recovery tasks. DaRT may optionally be included in the image, which makes DaRT recovery features available on the target computer.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|YES|The LiteTouchPE.wim file, which includes Windows RE and optionally DaRT, is applied to the system drive as the recovery partition.|
|*any other value*|The LiteTouchPE.wim file, which includes Windows RE and optionally DaRT, is not applied to the system drive as the recovery partition. This is the default value.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] PrepareWinRE=YES`|

###  <a name="Priority"></a> Priority
 The reserved property that determines the sequence for finding configuration values. The **Priority** reserved property lists each section to be searched and the order in which the sections are searched. When a property value is found, the ZTIGather.wsf script quits searching for the property, and the remaining sections are not scanned for that property.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*section1, section2*|The sections to be searched in the order they are to be searched|

|**Example**|
|-|
|`[Settings] Priority=MACAddress, Default  [Default] UserDataLocation=NONE CustomProperty=TRUE  [00:0F:20:35:DE:AC] OSDNEWMACHINENAME=HPD530-1  [00:03:FF:FE:FF:FF] OSDNEWMACHINENAME=BVMXP`|

###  <a name="ProcessorSpeed"></a> ProcessorSpeed
 The speed of the processor installed on the target computer in MHz. For example, the value **1995** indicates the processor on the target computer is running at 1,995 MHz or 2 gigahertz.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*processor_speed*|The speed of the processor on the target computer in megahertz|

|**Example**|
|-|
|None|

###  <a name="Product"></a> Product
 The product name of the target computer. With some computer vendors, the make and model might not be sufficiently unique to identify the characteristics of a particular configuration (for example, hyperthreaded or non-hyperthreaded chipsets). The **Product** property can help to differentiate.

 The format for **Product** is undefined. Use this property to create a subsection that contains settings targeted to a specific product name for a specific computer model number for a specific computer manufacturer (most commonly in conjunction with the **Make** and **Model** properties).

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*product*|The product name of the target computer|

|**Example**|
|-|
|None|

###  <a name="ProductKey"></a> ProductKey
 The product key string to be configured for the target computer. Before the target operating system is deployed, the product key specified is automatically inserted into the appropriate location in Unattend.xml.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*product_key*|The product key to be assigned to the target computer|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] ProductKey=AAAAA-BBBBB-CCCCC-DDDDD-EEEEE-FFFFF`|

###  <a name="Properties"></a> Properties
 A reserved property that defines any custom, user-defined properties. These user-defined properties are located by the ZTIGather.wsf script in the CustomSettings.ini file, BootStrap.ini file, or the MDT DB. These properties are additions to the predefined properties in MDT.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|                 **Value**                  |                **Description**                 |
|--------------------------------------------|------------------------------------------------|
| <em>custom_property1,</em>custom_property2 | Custom, user-defined properties to be resolved |

|**Example**|
|-|
|`[Settings] Priority=MACAddress, Default Properties=CustomProperty, ApplicationInstall  [Default] OSInstall=YES ScanStateArgs=/v:5 /o /c LoadStateArgs=/v:5 /c /lac UserDataLocation=NONE CustomProperty=TRUE  [00:0F:20:35:DE:AC] OSDNEWMACHINENAME=HPD530-1 ApplicationInstall=Custom  [00:03:FF:FE:FF:FF] OSDNEWMACHINENAME=BVMXP ApplicationInstall=Minimum`|

###  <a name="ReplicaDomainDNSName"></a> ReplicaDomainDNSName
 Specifies the DNS domain name of the domain to replicate.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*name*|Specifies the DNS domain name of the domain to replicate|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] ReplicaDomainDNSName=WoodGroveBank.com`|

###  <a name="ReplicaOrNewDomain"></a> ReplicaOrNewDomain
 Specifies whether to install a new domain controller as the first domain controller in a new directory service domain or to install it as a replica directory service domain controller.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**Replica**|Installs the new domain controller as a replica directory service domain controller.|
|**Domain**|Installs the new domain controller as the first domain controller in a new directory service domain. You must specify the **TreeOrChild** entry with a valid value.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] ReplicaOrNewDomain=Domain`|

###  <a name="ReplicationSourceDC"></a> ReplicationSourceDC
 Indicates the full DNS name of the domain controller from which you replicate the domain information.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*name*|Indicates the full DNS name of the domain controller from which you replicate the domain information|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] ReplicationSourceDC=dc01.WoodGroveBank.com`|

###  <a name="ResourceDrive"></a> ResourceDrive
 The drive letter mapped to the **ResourceRoot** property for the ZTIDrivers.wsf and ZTIPatches.wsf scripts to use to install drivers and patches to the target computer.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*drive_letter*|The letter designation for the logical drive that contains the resources|

|**Example**|
|-|
|None|

###  <a name="ResourceRoot"></a> ResourceRoot
 The value of this property is used by the ZTIDrivers.wsf and ZTIPatches.wsf scripts to install drivers and patches to the target computer.

> [!NOTE]
>  For LTI, the scripts automatically set the **ResourceRoot** property to be the same as the **DeployRoot** property. For ZTI, the values in the **DeployRoot** and **ResourceRoot** properties can be unique.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*UNC_path*|The UNC path to the shared folder that contains the resources|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceDrive=R: ResourceRoot=\\NYC-AM-FIL-01\Resource$ UserDataLocation=NONE`|

###  <a name="Role"></a> Role
 The purpose of a computer based on the tasks performed by the user on the target computer. The **Role** property lists text values that can be any non-blank value. The **Role** property value has a numeric suffix (for example, **Role1** or **Role2**). When defined, a role is associated with a computer. A computer can perform more than one role.

 Typically, the value for the **Role** property is set by performing a database query in the MDT DB. The Deployment Workbench can assist in creating the role and property settings associated with the role, and then the Deployment Workbench can configure CustomSettings.ini to perform the database query for the **Role** property and the property settings associated with the role.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*Role*|The roles to be assigned to an individual computer or a group of computers|

|**Example 1**|
|-|
|`[Settings] Priority=RoleSettings, Default  [Default] SkipCapture=NO UserDataLocation=AUTO DeployRoot=\\W2K3-SP1\Distribution$ OSInstall=YES ScanStateArgs=/v:15 /o /c LoadStateArgs=/v:7 /c  [RoleSettings] SQLServer=w2k3-sp1 Instance=MDT2010 Database=MDTDB Netlib=DBNMPNTW SQLShare=SQL_Share Table=RoleSettings Parameters=Role`|

|**Example 2**|
|-|
|`[Settings] Priority=RoleSettings, Default  [Default] SkipCapture=NO UserDataLocation=AUTO DeployRoot=\\W2K3-SP1\Distribution$ OSInstall=YES Role1=Teller Role2=Woodgrove User  [RoleSettings] SQLServer=w2k3-sp1 Instance=MDT2010 Database=MDTDB Netlib=DBNMPNTW SQLShare=SQL_Share Table=RoleSettings Parameters=Role`|

###  <a name="SafeModeAdminPassword"></a> SafeModeAdminPassword
 Supplies the password for the administrator account when starting the computer in Safe mode or a variant of Safe mode, such as Directory Services Restore mode.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*password*|Supplies the password for the administrator account when starting the computer in Safe mode or a variant of Safe mode, such as Directory Services Restore mode|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] SafeModeAdminPassword=<complex_password>`|

###  <a name="ScanStateArgs"></a> ScanStateArgs
 Arguments passed to the **USMT Scanstate** process. The scripts call Scanstate.exe, and then insert the appropriate logging, progress, and state store parameters. If this value is not included in the settings file, the user state backup process is skipped.

> [!NOTE]
>  Use the **USMTMigFiles** property to specify the .xml files to be used by Scanstate.exe instead of using the /I parameter in the **ScanStateArgs** property. This prevents the ZTIUserState.wsf script from potentially duplicating the same list of .xml files.

> [!NOTE]
>  Do not add any of the following command line arguments when configuring this property: **/hardlink**, **/nocompress**, **/encrypt**, **/key**, or **/keyfile**. The MDT scripts will add these command-line arguments if applicable to the current deployment scenario.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*arguments*|The command-line arguments passed to Scanstate.exe.<br /><br /> The default arguments specified by the Deployment Workbench are as follows:<br /><br /> - **/v**. Enables verbose output in the Scanstate log. The default is **0**. Specify any number from 0 to 15. The value **5** enables verbose and status output.<br /><br /> - **/o**. Overwrites any existing data in the store. If not specified, Scanstate will fail if the store already contains data. This option cannot be specified more than once in a Command Prompt window.<br /><br /> -                             **/c**. When specified, Scanstate will continue to run even if there are nonfatal errors. Without the **/c** option, Scanstate exits on the first error.<br /><br /> For more information about these and other arguments, see the USMT Help files.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] ScanStateArgs=/v:5 /o /c LoadStateArgs=/v:5 /c /lac DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UDShare=\\NYC-AM-FIL-01\MigData$ UDDir=%OSDComputerName%`|

###  <a name="SerialNumber"></a> SerialNumber
 The serial number of the target computer. The format for serial numbers is undefined. Use this property to create a subsection that contains settings targeted to a specific computer.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*serial_number*|The format of the serial number is undefined and is determined by the serial number standard of each computer manufacturer.|

|**Example**|
|-|
|None|

###  <a name="SiteName"></a> SiteName
 Specifies the name of an existing site where you can place the new domain controller.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*name*|Specifies the name of an existing site where you can place the new domain controller|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] SiteName=FirstSite`|

###  <a name="SkipAdminAccounts"></a> SkipAdminAccounts
 Indicates whether the **Local Administrators** wizard page is skipped.

> [!NOTE]
>  This default value for this property is **YES**, which means that the **Local Administrators** wizard page will be skipped by default. To display this wizard page, you must specifically set the value of this property to **NO** in CustomSettings.ini or in the MDT DB.

 For other properties that must be configured when this property is set to **YES**, see [Providing Properties for Skipped Deployment Wizard Pages](#ProvidingPropertiesforSkippedDeploymentWizardPages).

> [!CAUTION]
>  This property value must be specified in uppercase letters so that the deployment scripts can properly read it.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**YES**|Wizard page is not displayed, and the information on that page is not collected. This is the default value.|
|**NO**|Wizard page is displayed, and the information on that page is collected.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=NO SkipAdminAccounts=NO SkipAdminPassword=NO SkipApplications=NO SkipComputerBackup=NO SkipDomainMembership=NO SkipUserData=NO SkipPackageDisplay=NO SkipLocaleSelection=NO SkipProductKey=YES`|

###  <a name="SkipAdminPassword"></a> SkipAdminPassword
 Indicates whether the **Administrator Password** wizard page is skipped.

 For other properties that must be configured when this property is set to **YES**, see [Providing Properties for Skipped Deployment Wizard Pages](#ProvidingPropertiesforSkippedDeploymentWizardPages).

> [!CAUTION]
>  This property value must be specified in uppercase letters so that the deployment scripts can properly read it.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**YES**|Wizard page is not displayed, and the information on that page is not collected.|
|**NO**|Wizard page is displayed, and the information on that page is collected. This is the default value.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=NO SkipAdminPassword=YES SkipApplications=NO SkipComputerBackup=NO SkipDomainMembership=NO SkipUserData=NO SkipPackageDisplay=NO SkipLocaleSelection=NO SkipProductKey=YES`|

###  <a name="SkipApplications"></a> SkipApplications
 Indicates whether the **Select one or more applications to install** wizard page is skipped.

 For other properties that must be configured when this property is set to **YES**, see [Providing Properties for Skipped Deployment Wizard Pages](#ProvidingPropertiesforSkippedDeploymentWizardPages).

> [!CAUTION]
>  This property value must be specified in uppercase letters so that the deployment scripts can properly read it.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**YES**|Wizard page is not displayed, and the information on that page is not collected.|
|**NO**|Wizard page is displayed, and the information on that page is collected. This is the default value.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=NO SkipAdminPassword=NO SkipApplications=YES SkipComputerBackup=NO SkipDomainMembership=NO SkipUserData=NO SkipPackageDisplay=NO SkipLocaleSelection=NO SkipProductKey=YES`|

###  <a name="SkipBDDWelcome"></a> SkipBDDWelcome
 Indicates whether the **Welcome to Windows Deployment** wizard page is skipped.

 For other properties that must be configured when this property is set to **YES**, see [Providing Properties for Skipped Deployment Wizard Pages](#ProvidingPropertiesforSkippedDeploymentWizardPages).

> [!NOTE]
>  For this property to function properly it must be configured in both CustomSettings.ini and BootStrap.ini. BootStrap.ini is processed before a deployment share (which contains CustomSettings.ini) has been selected.

> [!CAUTION]
>  This property value must be specified in uppercase letters so that the deployment scripts can properly read it.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**YES**|Wizard page is not displayed, and the information on that page is not collected.|
|**NO**|Wizard page is displayed, and the information on that page is collected. This is the default value.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=NO SkipAdminPassword=YES SkipApplications=NO SkipBDDWelcome=YES SkipComputerBackup=NO SkipDomainMembership=NO SkipUserData=NO SkipPackageDisplay=NO SkipLocaleSelection=NO SkipProductKey=YES`|

###  <a name="SkipBitLocker"></a> SkipBitLocker
 Indicates whether the **Specify the BitLocker configuration** wizard page is skipped.

 For other properties that must be configured when this property is set to **YES**, see [Providing Properties for Skipped Deployment Wizard Pages](#ProvidingPropertiesforSkippedDeploymentWizardPages).

> [!CAUTION]
>  This property value must be specified in uppercase letters so that the deployment scripts can properly read it.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**YES**|Wizard page is not displayed, and the information on that page is not collected.|
|**NO**|Wizard page is displayed, and the information on that page is collected. This is the default value.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=NO SkipApplications=NO SkipBDDWelcome=YES SkipBitLocker=YES SkipComputerBackup=NO SkipDomainMembership=NO SkipUserData=NO SkipPackageDisplay=NO SkipLocaleSelection=NO`|

###  <a name="SkipBuild"></a> SkipBuild
 Indicates whether the **Select a task sequence to execute on this computer** wizard page is skipped.

 For other properties that must be configured when this property is set to **YES**, see [Providing Properties for Skipped Deployment Wizard Pages](#ProvidingPropertiesforSkippedDeploymentWizardPages).

 This property value must be specified in uppercase letters so that the deployment scripts can properly read it.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**YES**|Wizard page is not displayed, and the information on that page is not collected.|
|**NO**|Wizard page is displayed, and the information on that page is collected. This is the default value.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=NO SkipAdminPassword=YES SkipApplications=NO SkipBDDWelcome=YES SkipBuild=YES SkipComputerBackup=NO SkipComputerName=NO SkipDomainMembership=NO SkipFinalSummary=NO SkipSummary=NO SkipUserData=NO SkipPackageDisplay=NO SkipLocaleSelection=NO`|

###  <a name="SkipCapture"></a> SkipCapture
 Indicates whether the **Specify whether to capture an image** wizard page is skipped.

 For other properties that must be configured when this property is set to **YES**, see [Providing Properties for Skipped Deployment Wizard Pages](#ProvidingPropertiesforSkippedDeploymentWizardPages).

> [!CAUTION]
>  This property value must be specified in uppercase letters so that the deployment scripts can properly read it.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**YES**|The wizard page is not displayed, and the information on that page is not collected.|
|**NO**|The wizard page is displayed, and the information on that page is collected. This is the default value.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=YES SkipApplications=NO SkipComputerBackup=NO SkipDomainMembership=NO SkipUserData=NO SkipPackageDisplay=NO SkipLocaleSelection=NO`|

###  <a name="SkipComputerBackup"></a> SkipComputerBackup
 Indicates whether the **Specify where to save a complete computer backup** wizard page is skipped.

 For other properties that must be configured when this property is set to **YES**, see [Providing Properties for Skipped Deployment Wizard Pages](#ProvidingPropertiesforSkippedDeploymentWizardPages).

> [!CAUTION]
>  This property value must be specified in uppercase letters so that the deployment scripts can properly read it.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**YES**|The wizard page is not displayed, and the information on that page is not collected.|
|**NO**|The wizard page is displayed, and the information on that page is collected. This is the default value.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=NO SkipAdminPassword=NO SkipApplications=NO SkipComputerBackup=YES SkipDomainMembership=NO SkipUserData=NO SkipPackageDisplay=NO SkipLocaleSelection=NO`|

###  <a name="SkipComputerName"></a> SkipComputerName
 Indicates whether the **Configure the computer name** wizard page is skipped.

 For other properties that must be configured when this property is set to **YES**, see [Providing Properties for Skipped Deployment Wizard Pages](#ProvidingPropertiesforSkippedDeploymentWizardPages).

> [!CAUTION]
>  This property value must be specified in uppercase letters so that the deployment scripts can properly read it.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**YES**|Wizard page is not displayed, and the information on that page is not collected.|
|**NO**|Wizard page is displayed, and the information on that page is collected. This is the default value.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=NO SkipAdminPassword=NO SkipApplications=NO SkipComputerBackup=NO SkipComputerName=YES SkipDomainMembership=NO SkipUserData=NO SkipPackageDisplay=NO SkipLocaleSelection=NO`|

###  <a name="SkipDomainMembership"></a> SkipDomainMembership
 Indicates whether the **Join the computer to a domain or workgroup** wizard page is skipped.

 For other properties that must be configured when this property is set to **YES**, see [Providing Properties for Skipped Deployment Wizard Pages](#ProvidingPropertiesforSkippedDeploymentWizardPages).

> [!CAUTION]
>  This property value must be specified in uppercase letters so that the deployment scripts can properly read it.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**YES**|The wizard page is not displayed, and the information on that page is not collected.|
|**NO**|The wizard page is displayed, and the information on that page is collected. This is the default value.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=NO SkipAdminPassword=NO SkipApplications=NO SkipComputerBackup=NO SkipUserData=NO SkipPackageDisplay=NO SkipLocaleSelection=NO SkipDomainMembership=NO`|

###  <a name="SkipFinalSummary"></a> SkipFinalSummary
 Indicates whether the **Operating system deployment completed successfully** wizard page is skipped.

 For other properties that must be configured when this property is set to **YES**, see [Providing Properties for Skipped Deployment Wizard Pages](#ProvidingPropertiesforSkippedDeploymentWizardPages).

> [!NOTE]
>  This property value must be specified in uppercase letters so that the deployment scripts can properly read it.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**YES**|The wizard page is not displayed, and the information on that page is not collected.|
|**NO**|The wizard page is displayed, and the information on that page is collected. This is the default value.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=NO SkipApplications=NO SkipBDDWelcome=YES SkipComputerBackup=NO SkipComputerName=NO SkipDomainMembership=NO SkipFinalSummary=NO SkipUserData=NO SkipPackageDisplay=NO SkipLocaleSelection=NO SkipProductKey=YES`|

###  <a name="SkipGroupSubFolders"></a> SkipGroupSubFolders
 By default, when specifying folders to be included when injecting drivers, patches \(packages\), and so on, values are specified something like:

```
DriverGroup001=TopFolder\SecondFolder
PackageGroup001=TopFolder\SecondFolder
```

 This would, by default, also include all sub\-folders located under the "SecondFolder." If **SkipGroupSubFolders** is set to **YES** in CustomSettings.ini, this behavior will change so that the subfolders will be excluded and only the contents of "SecondFolder" will be added.

 To exclude subfolders when matching against groups such as DriverGroup001, PackageGroup001, and so on, set **SkipGroupSubFolders** to **YES**.

> [!CAUTION]
>  This property value must be specified in uppercase letters so that the deployment scripts can properly read it.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**YES**|Do not include subfolders when matching against groups.|
|**NO**|Include subfolders when matching against groups. This is the default behavior.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] SkipGroupSubFolders=NO`|

###  <a name="SkipLocaleSelection"></a> SkipLocaleSelection
 Indicates whether the **Locale Selection** wizard page is skipped.

 For other properties that must be configured when this property is set to **YES**, see [Providing Properties for Skipped Deployment Wizard Pages](#ProvidingPropertiesforSkippedDeploymentWizardPages).

> [!CAUTION]
>  This property value must be specified in uppercase letters so that the deployment scripts can properly read it.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**YES**|The wizard page is not displayed, and the information on that page is not collected.|
|**NO**|The wizard page is displayed, and the information on that page is collected. This is the default value.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=NO SkipApplications=NO SkipComputerBackup=NO SkipDomainMembership=NO SkipUserData=NO SkipPackageDisplay=NO SkipLocaleSelection=NO`|

###  <a name="SkipPackageDisplay"></a> SkipPackageDisplay
 Indicates whether the **Packages** wizard page is skipped.

 For other properties that must be configured when this property is set to **YES**, see [Providing Properties for Skipped Deployment Wizard Pages](#ProvidingPropertiesforSkippedDeploymentWizardPages).

> [!CAUTION]
>  This property value must be specified in uppercase letters so that the deployment scripts can properly read it.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**YES**|The wizard page is not displayed, and the information on that page is not collected.|
|**NO**|The wizard page is displayed, and the information on that page is collected. This is the default value.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=NO SkipApplications=NO SkipComputerBackup=NO SkipDomainMembership=NO SkipUserData=NO SkipPackageDisplay=YES SkipLocaleSelection=NO`|

###  <a name="SkipProductKey"></a> SkipProductKey
 Indicates whether the **Specify the product key needed to install this operating system** wizard page is skipped.

 For other properties that must be configured when this property is set to **YES**, see [Providing Properties for Skipped Deployment Wizard Pages](#ProvidingPropertiesforSkippedDeploymentWizardPages).

> [!CAUTION]
>  This property value must be specified in uppercase letters so that the deployment scripts can properly read it.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**YES**|The wizard page is not displayed, and the information on that page is not collected.|
|**NO**|The wizard page is displayed, and the information on that page is collected. This is the default value.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=NO SkipAdminPassword=YES SkipApplications=NO SkipComputerBackup=NO SkipDomainMembership=NO SkipUserData=NO SkipPackageDisplay=NO SkipLocaleSelection=NO SkipProductKey=YES`|

###  <a name="SkipRearm"></a> SkipRearm
 This property is used to configure whether MDT rearms the Microsoft Office 2010 25\-day activation grace period. If Microsoft Office 2010 is captured in a custom image, the user sees activation notification dialog boxes immediately after the image is deployed instead of 25\-days after deployment.

 By default, MDT rearms the Microsoft Office 2010 25\-day activation grace period when running the LTISysprep.wsf script. You can set the value of this property to **YES** so that MDT skips the rearming of the Microsoft Office 2010 25\-day activation grace period.

> [!CAUTION]
>  This property value must be specified in uppercase letters so that the deployment scripts can properly read it.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**YES**|MDT does not rearm the Microsoft Office 2010 25\-day activation grace period.|
|**NO**|MDT rearms the Microsoft Office 2010 25\-day activation grace period. This is the default value.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSInstall=Y SkipCapture=YES SkipAdminPassword=NO SkipProductKey=YES SkipRearm=YES DoCapture=YES`|

###  <a name="SkipRoles"></a> SkipRoles
 Indicates whether the **Roles and Features** wizard page is skipped.

 For other properties that must be configured when this property is set to **YES**, see [Providing Properties for Skipped Deployment Wizard Pages](#ProvidingPropertiesforSkippedDeploymentWizardPages).

> [!CAUTION]
>  This property value must be specified in uppercase letters so that the deployment scripts can properly read it.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**YES**|The wizard page is not displayed, and the information on that page is not collected.|
|**NO**|The wizard page is displayed, and the information on that page is collected. This is the default value.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=NO SkipAdminPassword=YES SkipApplications=NO SkipBDDWelcome=YES SkipTaskSequence=Yes SkipComputerBackup=NO SkipComputerName=NO SkipDomainMembership=NO SkipFinalSummary=NO SkipRoles=YES SkipSummary=NO SkipUserData=NO SkipPackageDisplay=NO SkipLocaleSelection=NO`|

###  <a name="SkipSummary"></a> SkipSummary
 Indicates whether the **Ready to begin** wizard page is skipped.

 For other properties that must be configured when this property is set to **YES**, see [Providing Properties for Skipped Deployment Wizard Pages](#ProvidingPropertiesforSkippedDeploymentWizardPages).

> [!CAUTION]
>  This property value must be specified in uppercase letters so that the deployment scripts can properly read it.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**YES**|The wizard page is not displayed, and the information on that page is not collected.|
|**NO**|The wizard page is displayed, and the information on that page is collected. This is the default value.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=NO SkipAdminPassword=YES SkipApplications=NO SkipBDDWelcome=YES SkipTaskSequence=Yes SkipComputerBackup=NO SkipComputerName=NO SkipDomainMembership=NO SkipFinalSummary=NO SkipSummary=NO SkipUserData=NO SkipPackageDisplay=NO SkipLocaleSelection=NO`|

###  <a name="SkipTaskSequence"></a> SkipTaskSequence
 Indicates whether the **Select a task sequence to execute on this computer** wizard page is skipped.

 For other properties that must be configured when this property is set to **YES**, see [Providing Properties for Skipped Deployment Wizard Pages](#ProvidingPropertiesforSkippedDeploymentWizardPages).

> [!NOTE]
>  Specify the **SkipBuild** property when using the Deployment Workbench to configure the Deployment Wizard to skip the **Select a task sequence to execute on this computer** wizard page.

> [!CAUTION]
>  This property value must be specified in uppercase letters so that the deployment scripts can properly read it.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**YES**|The wizard page is not displayed, and the information on that page is not collected.|
|**NO**|The wizard page is displayed, and the information on that page is collected. This is the default value.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=NO SkipApplications=NO SkipBDDWelcome=YES SkipTaskSequence=NO SkipComputerBackup=NO SkipComputerName=NO SkipDomainMembership=NO SkipFinalSummary=NO SkipSummary=NO SkipUserData=NO SkipPackageDisplay=NO SkipLocaleSelection=NO`|

###  <a name="SkipTimeZone"></a> SkipTimeZone
 Indicates whether the **Set the Time Zone** wizard page is skipped.

 For other properties that must be configured when this property is set to **YES**, see [Providing Properties for Skipped Deployment Wizard Pages](#ProvidingPropertiesforSkippedDeploymentWizardPages).

> [!CAUTION]
>  This property value must be specified in uppercase letters so that the deployment scripts can properly read it.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**YES**|The wizard page is not displayed, and the information on that page is not collected.|
|**NO**|The wizard page is displayed, and the information on that page is collected. This is the default value.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=NO SkipAdminPassword=YES SkipApplications=NO SkipBDDWelcome=YES SkipTaskSequence=YES SkipComputerBackup=NO SkipComputerName=NO SkipDomainMembership=NO SkipFinalSummary=NO SkipSummary=NO SkipTimeZone=NO SkipUserData=NO SkipPackageDisplay=NO SkipLocaleSelection=NO`|

###  <a name="SkipUserData"></a> SkipUserData
 Indicates whether the **Specify whether to restore user data** and **Specify where to save your data and settings** wizard page is skipped.

 For other properties that must be configured when this property is set to **YES**, see [Providing Properties for Skipped Deployment Wizard Pages](#ProvidingPropertiesforSkippedDeploymentWizardPages).

> [!CAUTION]
>  This property value must be specified in uppercase letters so that the deployment scripts can properly read it.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**YES**|The wizard page is not displayed, and the information on that page is not collected.|
|**NO**|The wizard page is displayed, and the information on that page is collected. This is the default value.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] SkipWizard=NO SkipCapture=NO SkipAdminPassword=YES SkipApplications=NO SkipComputerBackup=NO SkipDomainMembership=NO SkipUserData=NO SkipPackageDisplay=NO SkipLocaleSelection=NO SkipProductKey=YES`|

###  <a name="SkipWizard"></a> SkipWizard
 Indicates whether the entire **Deployment Wizard** is skipped.

 For other properties that must be configured when this property is set to **YES**, see [Providing Properties for Skipped Deployment Wizard Pages](#ProvidingPropertiesforSkippedDeploymentWizardPages).

> [!CAUTION]
>  This property value must be specified in uppercase letters so that the deployment scripts can properly read it.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**YES**|The entire wizard is not displayed, and none of the information on the wizard pages is collected.|
|**NO**|The wizard is displayed, and the information on the enabled wizard pages is collected. This is the default value.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] SkipWizard=YES`|

###  <a name="SLShare"></a> SLShare
 The network shared folder in which the deployment logs are stored at the end of the deployment process.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*shared_folder*|The name of the network shared folder in which script logs are stored|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UDShare=\\NYC-AM-FIL-01\MigData$ UDDir=%OSDComputerName% SLShare=\\NYC-AM-FIL-01\Logs$ UDProfiles=Administrator, User-01, ExtranetUser UserDataLocation=NONE SkipCapture=NO SkipAdminPassword=YES SkipProductKey=YES`|

###  <a name="SLShareDynamicLogging"></a> SLShareDynamicLogging
 The network shared folder in which all MDT logs should be written during deployment. This is used for advanced real-time debugging only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*shared_folder*|The name of the network shared folder in which script logs are stored|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UDShare=\\NYC-AM-FIL-01\MigData$ UDDir=%OSDComputerName% SLShare=\\NYC-AM-FIL-01\Logs$ SLShareDynamicLogging=\\NYC-AM-FIL-01\Logs$ UDProfiles=Administrator, User-01, ExtranetUser UserDataLocation=NONE SkipCapture=NO SkipAdminPassword=YES SkipProductKey=YES`|

###  <a name="SMSTSAssignUserMode"></a> SMSTSAssignUserMode
 Specifies whether user device affinity (UDA) should be enabled and whether approval is required. This property only works with the UDA feature in Configuration Manager.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**Auto**|The affinity between a user and the target device is established, and approval is automatically performed.|
|**Pending**|The affinity between a user and the target device is established, and approval is submitted for Configuration Manager administrator approval.|
|**Disable**|The affinity between a user and the target device is not established.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] SMSTSAssignUserMode=Auto SMSTSUdaUsers=Fabrikam\Ken, Fabrikam\Pilar`|

###  <a name="SMSTSRunCommandLineUserName"></a> SMSTSRunCommandLineUserName
 Specifies the user name in *Domain\User_Name* format that should be used with a **Run Command Line** step that is configured to run as a user.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*user_name*|Specifies the user name in that should be used with a **Run Command Line** step|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] SMSTSRunCommandLineUserName=Fabrikam\Ken SMSTSRunCommandLineUserPassword=<complex_password>`|

###  <a name="SMSTSRunCommandLineUserPassword"></a> SMSTSRunCommandLineUserPassword
 Specifies the password that should be used with a **Run Command Line** step that is configured to run as a user.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*user_password*|Specifies the password that should be used with a **Run Command Line** step|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] SMSTSRunCommandLineUserName=Fabrikam\Ken SMSTSRunCommandLineUserPassword=<complex_password>`|

###  <a name="SMSTSUdaUsers"></a> SMSTSUdaUsers
 Specifies the users who will be assigned affinity with a specific device using the UDA feature, which is available only in Configuration Manager.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|     **Value**     |                                                                                                                                                                **Description**                                                                                                                                                                |
|-------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| *user1, user2, ...* | The comma-separated list of users in *Domain\User_Name* format that will be assigned affinity with the target device.<br /><br /> Note:<br /><br /> You can only use the NetBIOS domain name in this value, such as *Fabrikam\Ken*. You cannot use the fully qualified domain name (fabrikam.com\Ken) or the UPN notation (ken@fabrikam.com). |

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] SMSTSAssignUserMode=Auto SMSTSUdaUsers=Fabrikam\Ken, Fabrikam\Pilar`|

###  <a name="SQLServer"></a> SQLServer
 The identity of the computer running SQL Server that performs a database query that returns property values from columns in the table specified in the **Table** property. The query is based on parameters specified in the **Parameters** and **ParameterCondition** properties. The instance of SQL Server on the computer is specified in the **Instance** property.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*SQL_server*|The name of the computer running SQL Server|

|**Example**|
|-|
|`[Settings] Priority=Computers, Default  [Default] OSInstall=YES ScanStateArgs=/v:5 /o /c LoadStateArgs=/v:5 /c /lac  [Computers] SQLServer=NYC-SQL-01 SQLShare=SQL$ Database=MDTDB Instance=SQLEnterprise2005 Table=Computers Parameters=SerialNumber, AssetTag ParameterCondition=OR`|

###  <a name="SQLShare"></a> SQLShare
 The name of a shared folder on the computer running SQL Server (specified by the **SQLServer** property). The credentials used for authentication are provided by the **UserDomain**, **UserID**, and **UserPassword** properties (for LTI and ZTI) or by the Configuration Manager Advanced Client account credentials (ZTI only).

> [!NOTE]
>  This property must be specified to perform Integrated Windows authentication. This is the recommended authentication method, rather than using the **DBID** and **DBPwd** properties (which support the SQL Server authentication method).

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*shared_folder*|The name of a shared folder on the computer running SQL Server|

|**Example**|
|-|
|`[Settings] Priority=Computers, Default Properties=MyCustomProperty  [Default] OSInstall=YES ScanStateArgs=/v:5 /o /c LoadStateArgs=/v:5 /c /lac  [Computers] SQLServer=NYC-SQL-01 SQLShare=SQL$ Database=MDTDB Instance=MDT2010 Table=Computers Parameters=SerialNumber, AssetTag ParameterCondition=OR`|

###  <a name="StatePath"></a> StatePath
 This property is used to set the path where the user state migration data will be stored, which can be a UNC path, a local path, or a relative path. The [OSDStateStorePath](#OSDStateStorePath) property takes precedence over the **StatePath** or [UserDataLocation](#UserDataLocation) property when those properties are also specified.

> [!NOTE]
>  This property is provided for backward compatibility with previous versions of MDT. Use the [OSDStateStorePath](#UserDataLocation) property instead.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*Path*|The path where the user state migration data will be stored, which can be a UNC path, a local path, or a relative path|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] SitePath=\\fs1\Share\Replace ComputerBackupLocation=\\fs1\Share\ComputerBackup\Client01`|

###  <a name="StoredProcedure"></a> StoredProcedure
 The name of the stored procedure used when performing a database query that returns property values from columns in the table or view. The stored procedure is located in the database specified in the **Database** property. The computer running SQL Server is specified in the **SQLServer** property. The instance of SQL Server on the computer is specified in the **Instance** property. The name of the stored procedure is specified in the **StoredProcedure** property.

 For more information about using a stored procedure to query a SQL Server database, see the section, "Deploying Applications Based on Earlier Application Versions", in the MDT document *Microsoft Deployment Toolkit Samples Guide*.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*stored_procedure*|The name of the stored procedure used to query the SQL Server database|

|**Example**|
|-|
|`[Settings] Priority=DynamicPackages, Default  [Default] OSInstall=YES  [DynamicPackages] SQLDefault=DB_DynamicPackages  [DB_DynamicPackages] SQLServer=SERVER1 Database=MDTDB StoredProcedure=RetrievePackages Parameters=MacAddress SQLShare=Logs Instance=MDT2013 Port=1433 Netlib=DBNMPNTW`|

###  <a name="SupportsHyperVRole"></a> SupportsHyperVRole
 Specifies whether the processor resources on the target computer can support the Hyper-V server role in Windows Server. This property is True if the value for the following properties is set to **TRUE**:

- **SupportsNX**

- **SupportsVT**

- **Supports64Bit**

  Each of the previous properties is set using information from the **CPUID** interface. For further information collected about VMs and information returned from the **CPUID** interface, see the following properties:

- **IsHypervisorRunning**

- **IsVM**

- **SupportsNX**

- **SupportsVT**

- **Supports64Bit**

- **VMPlatform**

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|The processor resources of the target computer can support the Hyper-V server role in Windows Server.|
|**FALSE**|The processor resources of the target computer cannot support the Hyper-V server role in Windows Server.|

|**Example**|
|-|
|None|

###  <a name="SupportsNX"></a> SupportsNX
 Specifies whether the processor resources on the target computer support the No Execute (NX) technology. The NX technology is used in processors to segregate areas of memory for use by either storage of processor instructions (code) or for storage of data. This property is set using information from the **CPUID** interface.

 For further information collected about VMs and information returned from the **CPUID** interface, see the following properties:

-   **IsHypervisorRunning**

-   **IsVM**

-   **SupportsHyperVRole**

-   **SupportsVT**

-   **Supports64Bit**

-   **VMPlatform**

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|The processor resources of the target computer support NX technology.|
|**FALSE**|The processor resources of the target computer do not support NX technology.|

|**Example**|
|-|
|None|

###  <a name="SupportsVT"></a> SupportsVT
 Specifies whether the processor resources on the target computer support the Virtualization Technology (VT) feature. VT is used to support current virtualized environments, such as Hyper-V. This property is set using information from the CPUID interface.

 For further information collected about VMs and information returned from the CPUID interface, see the following properties:

-   **IsHypervisorRunning**

-   **IsVM**

-   **SupportsHyperVRole**

-   **SupportsNX**

-   **Supports64Bit**

-   **VMPlatform**

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|The processor resources of the target computer support VT technology.|
|**FALSE**|The processor resources of the target computer do not support VT technology.|

|**Example**|
|-|
|None|

###  <a name="Supports64Bit"></a> Supports64Bit
 Specifies whether the processor resources on the target computer support Windows 64-bit operating systems. Most modern virtualization environments require 64-bit processor architecture. This property is set using information from the **CPUID** interface.

 For further information collected about VMs and information returned from the **CPUID** interface, see the following properties:

-   **IsHypervisorRunning**

-   **IsVM**

-   **SupportsHyperVRole**

-   **SupportsNX**

-   **SupportsVT**

-   **VMPlatform**

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|The processor resources of the target computer support a Windows 64-bit operating system.|
|**FALSE**|The processor resources of the target computer do not support a Windows 64-bit operating system.|

|**Example**|
|-|
|None|

###  <a name="SysVolPath"></a> SysVolPath
 Specifies the fully qualified, non-UNC path to a directory on a fixed disk of the local computer.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*path*|Specifies the fully qualified, non-UNC path to a directory on a fixed disk of the local computer|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] SysVolPath=%DestinationLogicalDrive%\Windows\Sysvol`|

###  <a name="Table"></a> Table
 The name of the table or view to be used in performing a database query that returns property values from columns in the table or view. The query is based on parameters specified in the **Parameters** and **ParameterCondition** properties. The table or view is located in the database specified in the **Database** property. The computer running SQL Server is specified in the **SQLServer** property. The instance of SQL Server on the computer is specified in the **Instance** property.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*table_name*|The name of the table or view to be queried for property values|

|**Example**|
|-|
|`[Settings] Priority=Computers, Default  [Default] OSInstall=YES ScanStateArgs=/v:5 /o /c LoadStateArgs=/v:5 /c /lac  [Computers] SQLServer=NYC-SQL-01 SQLShare=SQL$ Database=MDTDB Instance=MDT2010 Table=Computers Parameters=SerialNumber, AssetTag ParameterCondition=OR`|

###  <a name="TaskSequenceID"></a> TaskSequenceID
 Identifies the operating system task sequence to be deployed to the target computer. The task sequence ID is created on the Task Sequences node in the Deployment Workbench. The **TaskSequenceID** property allows alphanumeric characters, hyphens (-), and underscores (\_). The **TaskSequenceID** property cannot be blank or contain spaces.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*task_sequence_id*|Identifier of the operating system task sequence defined in the Deployment Workbench for the target operating system being deployed<br /><br /> Note:<br /><br /> Be sure to use the **TaskSequenceID** specified in the Deployment Workbench UI, not the GUID of the **TaskSequenceID**.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] TaskSequenceID=BareMetal`|

###  <a name="TaskSequenceName"></a> TaskSequenceName
 Specifies the name of the task sequence being run.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*task_sequence_name*|Name of the task sequence being run, such as Deploy *Windows 8.1 to Reference Computer*|

|**Example**|
|-|
|None|

###  <a name="TaskSequenceVersion"></a> TaskSequenceVersion
 Specifies the version of the task sequence being run.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*task_sequence_version*|Version of the task sequence being run, such as *1.00*|

|**Example**|
|-|
|None|

###  <a name="TimeZoneName"></a> TimeZoneName
 The time zone in which the target computer is located. This value is inserted into the appropriate configuration settings in Unattend.xml.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*time_zone_name*|The text value that indicates the time zone where the target computer is located|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] TimeZoneName=Pacific Standard Time DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UDShare=\\NYC-AM-FIL-01\MigData$ UDDir=%OSDComputerName% SLShare=\\NYC-AM-FIL-01\Logs$ UDProfiles=Administrator, User-01, ExtranetUser UserDataLocation=NONE`|

###  <a name="ToolRoot"></a> ToolRoot
 Specifies the UNC path to the Tools\\*proc_arch* folder (where *proc_arch* is the processor architecture of the currently running operating system and can have a value of **x86** or **x64**), which is immediately beneath the root of the folder structure specified in the **DeployRoot** property. The Tools\\*proc_arch* folder contains utilities that MDT uses during the deployment process.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*path*|The UNC or local path to the Tools\\*proc_arch* folder (where *proc_arch* is the processor architecture of the currently running operating system and can have a value of **x86** or **x64**) immediately beneath the root of the folder structure specified by the **DeployRoot** property|

|**Example**|
|-|
|None|

###  <a name="TPMOwnerPassword"></a> TPMOwnerPassword
 The TPM password (also known as the *TPM administration password*) for the owner of the target computer. The password can be saved to a file or stored in AD DS.

> [!NOTE]
>  If the TPM ownership is already set or TPM ownership is not allowed, then the **TPMOwnerPassword** property is ignored. If the TPM password is needed and the **TPMOwnerPassword** property is not provided, the TPM password is set to the local Administrator password.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*password*|The TPM password for the owner of the target computer|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] BDEDriveLetter=S: BDEDriveSize=2000 BDEInstall=TPMKey BDERecoveryKey=TRUE BDEKeyLocation=C: TPMOwnerPassword=<complex_password> BackupShare=\\NYC-AM-FIL-01\Backup$ BackupDir=%OSDComputerName% DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UDShare=\\NYC-AM-FIL-01\MigData$ UDDir=%OSDComputerName%`|

###  <a name="UDDir"></a> UDDir
 The folder in which the user state migration data is stored. This folder exists beneath the network shared folder specified in **UDShare**.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*folder*|The name of the folder that exists beneath the network shared folder|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UDShare=\\NYC-AM-FIL-01\MigData$ UDDir=%OSDComputerName% SLShare=\\NYC-AM-FIL-01\Logs$ UDProfiles=Administrator, User-01, ExtranetUser UserDataLocation=NONE SkipCapture=NO`|

###  <a name="UDProfiles"></a> UDProfiles
 A comma-delimited list of user profiles that need to be saved by Scanstate.exe during the State Capture Phase.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*user_profiles*|The list of user profiles to be saved, separated by commas|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UDShare=\\NYC-AM-FIL-01\MigData$ UDDir=%OSDComputerName% SLShare=\\NYC-AM-FIL-01\Logs$ UDProfiles=Administrator, User-01, ExtranetUser UserDataLocation=NONE SkipCapture=NO`|

###  <a name="UDShare"></a> UDShare
 The network share where user state migration data is stored.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*UNC_path*|The UNC path to the network share where user state migration data is stored|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UDShare=\\NYC-AM-FIL-01\MigData$ UDDir=%OSDComputerName% SLShare=\\NYC-AM-FIL-01\Logs$ UDProfiles=Administrator, User-01, ExtranetUser UserDataLocation=NONE SkipCapture=NO`|

###  <a name="UILanguage"></a> UILanguage
 The default language to be used with the target operating system. If not specified, the **Deployment Wizard** uses the language configured in the image being deployed.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*UI_language*|The default language for the operating system on the target computer|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] UserLocale=en-us UILanguage=en-us KeyboardLocale=0409:00000409`|

###  <a name="UserDataLocation"></a> UserDataLocation
 The location in which USMT stores user state migration data.

> [!CAUTION]
>  This property value must be specified in uppercase letters so that the deployment scripts can properly read it.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|blank|If **UserDataLocation**is not specified or is left blank, the Deployment Wizard will default to using the AUTO behavior.|
|*UNC_path*|The UNC path to the network shared folder where the user state migration data is stored.|
|**AUTO**|The deployment scripts store the user state migration data on a local hard disk if space is available. Otherwise, the user state migration data is saved to a network location, which is specified in the **UDShare** and **UDDir** properties.|
|**NETWORK**|The user state migration data is stored in the location designated by the **UDShare** and **UDDir** properties.|
|**NONE**|The user state migration data is not saved.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSInstall=YES ScanStateArgs=/v:5 /o /c LoadStateArgs=/v:5 /c /lac DoCapture=YES BackupShare=\\NYC-AM-FIL-01\Backup$ BackupDir=%OSDComputerName% UserDataLocation=NETWORK DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UDShare=\\NYC-AM-FIL-01\MigData$ UDDir=%OSDComputerName%`|

###  <a name="UserDomain"></a> UserDomain
 The domain in which a user's credentials (specified in the **UserID** property) reside.

> [!NOTE]
>  For a completely automated LTI deployment, provide this property in both CustomSettings.ini and BootStrap.ini. However, note that storing the user credentials in these files stores the credentials in clear text and therefore is not secure.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*domain*|The name of the domain where the user account credentials reside|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSInstall=YES ScanStateArgs=/v:5 /o /c LoadStateArgs=/v:5 /c /lac DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UserDataLocation=NONE UserDomain=WOODGROVEBANK UserID=NYC Help Desk Staff UserPassword=<complex_password>`|

###  <a name="UserID"></a> UserID
 The user credentials for accessing network resources.

> [!NOTE]
>  For a completely automated LTI deployment, provide this property in both CustomSettings.ini and BootStrap.ini. However, note that storing the user credentials in these files stores the credentials in clear text and therefore is not secure.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*user_id*|The name of the user account credentials used to access the network resources|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSInstall=YES ScanStateArgs=/v:5 /o /c LoadStateArgs=/v:5 /c /lac DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UserDataLocation=NONE UserDomain=WOODGROVEBANK UserID=NYC-HelpDesk UserPassword=<complex_password>`|

###  <a name="UserLocale"></a> UserLocale
 The user locale to be used with the target operating system. If not specified, the **Deployment Wizard** uses the user locale configured in the image being deployed.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*user_locale*|The locale for the user on the target computer. The value is specified as a text value (en-us).|

|**Example 1**|
|-|
|`[Settings] Priority=Default  [Default] UserLocale=en-us KeyboardLocale=0409:00000409`|

|**Example 2**|
|-|
|`[Settings] Priority=Default  [Default] UserLocale=en-us KeyboardLocale=en-us`|

###  <a name="UserPassword"></a> UserPassword
 The password for user credentials specified in the **UserID** property.

> [!NOTE]
>  For a completely automated LTI deployment, provide this property in both CustomSettings.ini and BootStrap.ini. However, note that storing the user credentials in these files stores the credentials in clear text and therefore is not secure.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*user_password*|The password for the user account credentials|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] UserDataLocation=NONE UserDomain=WOODGROVEBANK UserID=NYC-HelpDesk UserPassword=<complex_password>`|

###  <a name="USMTConfigFile"></a> USMTConfigFile
 The USMT configuration XML file that should be used when running **Scanstate** and **Loadstate**.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*USMTConfigFile*|The name of the XML configuration file that should be used when running Scanstate.exe and Loadstate.exe|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSInstall=YES ScanStateArgs=/v:5 /o /c LoadStateArgs=/v:5 /c /lac DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UDShare=\\NYC-AM-FIL-01\MigData$ UDDir=%OSDComputerName% SLShare=\\NYC-AM-FIL-01\Logs$ USMTMigFiles1=MigApp.xml USMTMigFiles2=MigUser.xml USMTMigFiles3=MigSys.xml USMTMigFiles4=MigCustom.xml USMTConfigFile=USMTConfig.xml UserDataLocation=NONE`|

###  <a name="USMTLocal"></a> USMTLocal
 This property specifies whether the USMT user state information is stored locally on the target computer. This property is primarily used by the [ZTIUserState.wsf](#ZTIUserState.wsf) and [ZTIBackup.wsf](#ZTIBackup.wsf) scripts to indicate that the **Request State Store** and **Release State Store** task sequence steps for Configuration Manager deployments are skipped. For more information, see the [OSDStateStorePath](#OSDStateStorePath) property.

> [!NOTE]
>  This property should only be used in the circumstance described in the [OSDStateStorePath](#OSDStateStorePath) property).

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|The USMT user state information is stored locally on the target computer, and the **Request State Store** and **Release State Store** task sequence steps are skipped.|
|**FALSE**|The USMT user state information is not stored locally on the target computer, and the **Request State Store** and **Release State Store** task sequence steps are performed.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSInstall=YES ScanStateArgs=/v:5 /o /c LoadStateArgs=/v:5 /c /lac DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UDShare=\\NYC-AM-FIL-01\MigData$ UDDir=%OSDComputerName% SLShare=\\NYC-AM-FIL-01\Logs$ USMTLocal=TRUE USMTMigFiles001=MigApp.xml USMTMigFiles002=MigUser.xml USMTMigFiles003=MigSys.xml USMTMigFiles004=MigCustom.xml UserDataLocation=NONE`|

###  <a name="USMTMigFiles"></a> USMTMigFiles
 A list of files in XML format that are used by USMT (Scanstate.exe) to identify user state migration information to be saved. When this property is not specified, the ZTIUserState.wsf script uses MigApp.xml, MigUser.xml, and MigSys.xml. Otherwise, ZTIUserState.wsf uses the files explicitly referenced in this property. The **USMTMigFiles** property has a numeric suffix (for example, **USMTMigFiles001** or **USMTMigFiles002**).

> [!NOTE]
>  Use this property to specify the XML files to be used by Scanstate.exe instead of using the **/I** parameter in the **ScanStateArgs** property. This prevents the ZTIUserState.wsf script from potentially duplicating the same list of XML files.

> [!NOTE]
>  This property name can be specified using single-digit nomenclature (**USMTMigFiles1**) or triple-digit nomenclature (**USMTMigFiles001**).

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*USMTMigFile*|The name of the .xml file to be used as input for Scanstate.exe, on separate lines. If not specified, the default is MigApp.xml, MigUser.xml, and MigSys.xml.<br /><br /> Note:<br /><br /> If this value is specified, the default files (MigApp.xml, MigUser.xml, and MigSys.xml) must also be added to the list if these files are to be included.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSInstall=YES ScanStateArgs=/v:5 /o /c LoadStateArgs=/v:5 /c /lac DeployRoot=\\NYC-AM-FIL-01\Distribution$ ResourceRoot=\\NYC-AM-FIL-01\Resource$ UDShare=\\NYC-AM-FIL-01\MigData$ UDDir=%OSDComputerName% SLShare=\\NYC-AM-FIL-01\Logs$ USMTMigFiles001=MigApp.xml USMTMigFiles002=MigUser.xml USMTMigFiles003=MigSys.xml USMTMigFiles004=MigCustom.xml UserDataLocation=NONE`|

###  <a name="USMTOfflineMigration"></a> USMTOfflineMigration
 This property determines whether MDT uses USMT to perform an offline user state migration. In an offline migration, the capture is performed in Windows PE instead of the existing operating system.

 Offline migration is using USMT is performed for:

- UDI always, regardless of the setting of the **USMTOfflineMigration** property

- ZTI only for the MDT Refresh Computer deployment scenario and only when the **USMTOfflineMigration** property is set to **"TRUE"**

  > [!NOTE]
  >  You cannot perform USMT offline user state migration in the MDT New Computer deployment scenario using ZTI.

- LTI for the:

  1.  MDT New Computer deployment scenario using the **Move Data and Settings** wizard page in the Deployment Wizard

  2.  MDT Refresh Computer deployment scenario and only when the **USMTOfflineMigration** property is set to **"TRUE"**

  For more information about using MDT and USMT to perform an offline user state migration, see "Configure USMT Offline User State Migration".

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|MDT uses USMT to perform an offline user state migration.|
|*Any other value*|MDT does not perform an offline user state migration. Instead, user state migration is captured in the existing operating system. This is the default value.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] OSInstall=YES SkipUserData=YES USMTOfflineMigration=TRUE DoNotFormatAndPartition=YES OSDStateStorePath=\\WDG-MDT-01\StateStore$`|

###  <a name="UUID"></a> UUID
 The Universal Unique Identifier (UUID) stored in the System Management BIOS of the target computer.

 The format for UUID is a 16-byte value using hexadecimal digits in the following format: *12345678-1234-1234-1234-123456789ABC*. Use this property to create a subsection that contains settings targeted to a specific computer.

> [!NOTE]
>  This property is dynamically set by MDT scripts and cannot have its value set in CustomSettings.ini or the MDT DB. Treat this property as read only. However, you can use this property within CustomSettings.ini or the MDT DB, as shown in the following examples, to aid in defining the configuration of the target computer.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*UUID*|The UUID of the target computer|

|**Example**|
|-|
|None|

###  <a name="ValidateDomainCredentialsUNC"></a> ValidateDomainCredentialsUNC
 This property is used to specify a UNC path to a network shared folder that is used to validate the credentials provided for joining the target computer to a domain. The credentials being validated are specified in the **DomainAdmin**, **DomainAdminDomain**, and **DomainAdminPassword** properties.

> [!NOTE]
>  Ensure that no other properties in MDT use the server sharing the folder in this property. Using a server that is already referenced by other MDT properties could result in improper validation of the credentials.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*unc_path*|Specifies the fully qualified UNC path to a network shared folder|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] ValidateDomainCredentialsUNC=\\wdg-fs-01\Source$`|

###  <a name="VHDCreateDiffVHD"></a> VHDCreateDiffVHD
 This property is used to specify the name of a differencing VHD (also known as a *child VHD*) file. A differencing VHD is similar to a dynamically expanding VHD but contains only the modified disk blocks of the associated parent VHD. The parent VHD is read only, so you must modify the differencing VHD. The differencing VHD file is created in the same folder as the parent VHD file, so only the file name is specified in this property. This property is only valid for the MDT New Computer deployment scenario.

> [!NOTE]
>  All parent VHD files created by MDT are stored in the VHD folder in the root of the parent drive.

 This property is commonly set using a task sequence step created using the **Create Virtual Hard Disk (VHD)** task sequence type. You can override the value the **Create Virtual Hard Disk (VHD)** task sequence step sets by configuring this property in CustomSettings.ini.

> [!NOTE]
>  To configure this property in CustomSettings.ini, you must add this property to the **Properties** line in CustomSettings.ini.

 For related properties that are used with VHD files, see:

-   **VHDCreateFileName**

-   **VHDCreateSizeMax**

-   **VHDCreateSource**

-   **VHDCreateType**

-   **VHDDisks**

-   **VHDInputVariable**

-   **VHDOutputVariable**

-   **VHDTargetDisk**

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*filename*|Specifies the name of the differencing VHD file, which is located in the same folder as the parent VHD file<br /><br /> The differencing VHD file cannot have the same name as the parent VHD file.|
|**RANDOM**|Automatically generates a random name for the differencing VHD file, which is located in the same folder as the parent VHD file|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] VHDCreateDiffVHD=Win7Diff_C.vhd VHDInputVariable=VHDTargetDisk`|

###  <a name="VHDCreateFileName"></a> VHDCreateFileName
 This property is used to specify the name of a VHD file. The type of VHD file is based on the value of the **VHDCreateType** property. The property only includes the file name, not the path to the file name, and is valid only for the MDT New Computer deployment scenario.

> [!NOTE]
>  The VHD files created by MDT are stored in the VHD folder in the root of the parent drive.

 This property is commonly set using a task sequence step created using the **Create Virtual Hard Disk (VHD)** task sequence type. You can override the value the **Create Virtual Hard Disk (VHD)** task sequence step sets by configuring this property in CustomSettings.ini.

> [!NOTE]
>  To configure this property in CustomSettings.ini, you must add this property to the **Properties** line in CustomSettings.ini.

 For related properties that are used with VHD files, see:

-   **VHDCreateDiffVHD**

-   **VHDCreateSizeMax**

-   **VHDCreateSource**

-   **VHDCreateType**

-   **VHDDisks**

-   **VHDInputVariable**

-   **VHDOutputVariable**

-   **VHDTargetDisk**

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*file_name*|Specifies the name of the VHD file|
|**RANDOM**|Automatically generates a random name for the VHD file, which is located in the VHD folder in the root of the parent drive|
|Blank|Same a **RANDOM**|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] VHDCreateSizeMax=130048 VHDCreateType=EXPANDABLE VHDCreateFileName=Win7_C.vhd VHDInputVariable=VHDTargetDisk`|

###  <a name="VHDCreateSizeMax"></a> VHDCreateSizeMax
 This property is used to specify the maximum size of a VHD file in megabytes (MB). The size of the VHD file at creation time is based on the type of VHD file being created. For more information, see the [VHDCreateType](#VHDCreateType) property. This property is valid only for the MDT New Computer deployment scenario.

> [!NOTE]
>  If this property is not specified, the default value for the maximum size of a VHD file is 90% of the available disk space on the parent disk.

 This property is commonly set using a task sequence step created using the **Create Virtual Hard Disk (VHD)** task sequence type. You can override the value that the **Create Virtual Hard Disk (VHD)** task sequence step sets by configuring this property in CustomSettings.ini.

> [!NOTE]
>  To configure this property in CustomSettings.ini, you must add this property to the **Properties** line in CustomSettings.ini.

 For related properties that are used with VHD files, see:

-   **VHDCreateDiffVHD**

-   **VHDCreateFileName**

-   **VHDCreateSource**

-   **VHDCreateType**

-   **VHDDisks**

-   **VHDInputVariable**

-   **VHDOutputVariable**

-   **VHDTargetDisk**

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*size*|The maximum size of the VHD file specified in MB. For example, 130,048 MB equals 127 GB. The default value is 90% of the available disk space on the parent disk.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] VHDCreateSizeMax=130048 VHDCreateType=FIXED VHDCreateFileName=Win7_C.vhd VHDInputVariable=VHDTargetDisk`|

###  <a name="VHDCreateSource"></a> VHDCreateSource
 This property is used to specify the name of a VHD file that is used as a template (source) for creating a new VHD file. You can specify the file name using a UNC path, local path, relative path, or just the file name. If just the file name is specified, then MDT attempts to find the VHD file on the target computer. This property is valid only for the MDT New Computer deployment scenario.

 This property is commonly set using a task sequence step created using the **Create Virtual Hard Disk (VHD)** task sequence type. You can override the value that the <strong>Create Virtual Hard Disk (VHD)</strong>task sequence step sets by configuring this property in CustomSettings.ini.

> [!NOTE]
>  To configure this property in CustomSettings.ini, you must add this property to the **Properties** line in CustomSettings.ini.

 For related properties that are used with VHD files, see:

-   **VHDCreateDiffVHD**

-   **VHDCreateFileName**

-   **VHDCreateSizeMax**

-   **VHDCreateType**

-   **VHDDisks**

-   **VHDInputVariable**

-   **VHDOutputVariable**

-   **VHDTargetDisk**

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*name*|The file name, which can be specified using a UNC path, local path, relative path, or just the file name. If just the file name is specified, then MDT attempts to find the VHD file on the target computer.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] VHDCreateSizeMax=130048 VHDCreateSource=\\wdg-mdt-01\vhds\win7_template.vhd VHDCreateType=FIXED VHDCreateFileName=Win7_C.vhd VHDInputVariable=VHDTargetDisk`|

###  <a name="VHDCreateType"></a> VHDCreateType
 This property is used to specify the type of VHD file that is specified in the **VHDCreateFileName** property and can be one of the following VHD file types:

- **Fixed VHD file**. For this VHD type, the size of the VHD specified at creation is allocated and does not change automatically after creation. For example, if you create a 24\-gigabyte \(GB\) fixed VHD file, the file will be approximately 24 GB in size \(with some space used for the internal VHD structure\) regardless of how much information is stored in the VHD file.

- **Dynamically expanding VHD file**. For this VHD type, only a small percentage of the size of the VHD specified at creation time is allocated. Then, the VHD file continues to grow as more and more information is stored in it. However, the VHD file cannot grow beyond the size specified at creation. For example, if you create a 24 GB dynamically expanding VHD, it will be small at creation. However, as information is stored in the VHD file, the file will continue to grow but never exceed the maximum size of 24 GB.

  This property is only valid for the MDT New Computer deployment scenario.

> [!NOTE]
>  The maximum size of the VHD file is specified in the **VHDCreateSizeMax** property.

 This property is commonly set using a task sequence step created using the **Create Virtual Hard Disk \(VHD\)** task sequence type. You can override the value that the **Create Virtual Hard Disk \(VHD\)** task sequence step sets by configuring this property in CustomSettings.ini.

> [!NOTE]
>  To configure this property in CustomSettings.ini, you must add this property to the **Properties** line in CustomSettings.ini.

 For related properties that are used with VHD files, see:

-   **VHDCreateDiffVHD**

-   **VHDCreateFileName**

-   **VHDCreateSizeMax**

-   **VHDCreateSource**

-   **VHDDisks**

-   **VHDInputVariable**

-   **VHDOutputVariable**

-   **VHDTargetDisk**

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**EXPANDABLE**|Creates a fixed VHD file|
|**FIXED**|Creates a dynamically expanding VHD file|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] VHDCreateSizeMax=130048 VHDCreateType=EXPANDABLE VHDCreateFileName=Win7_C.vhd VHDInputVariable=VHDTargetDisk`|

###  <a name="VHDDisks"></a> VHDDisks
 This property contains a list of the physical drive numbers assigned to VHD files separated by spaces. Each time a VHD file is created, MDT adds the disk index of the newly created disk to this property using the **Index** property of the **Win32\_DiskDrive** WMI class.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

 This property is commonly set using a task sequence step created using the **Create Virtual Hard Disk \(VHD\)** task sequence type. You can override the value that the **Create Virtual Hard Disk \(VHD\)** task sequence step sets by configuring this property in CustomSettings.ini.

> [!NOTE]
>  To configure this property in CustomSettings.ini, you must add this property to the **Properties** line in CustomSettings.ini.

 For related properties that are used with VHD files, see:

-   **VHDCreateDiffVHD**

-   **VHDCreateFileName**

-   **VHDCreateSizeMax**

-   **VHDCreateSource**

-   **VHDCreateType**

-   **VHDInputVariable**

-   **VHDOutputVariable**

-   **VHDTargetDisk**

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*index1 index2 index3*|A list of the physical drive numbers assigned to the VHD files separated by spaces—for example, *1 2 5*.|

|**Example**|
|-|
|None|

###  <a name="VHDInputVariable"></a> VHDInputVariable
 This property contains a variable that contains the drive on the target computer where the VHD files will be created. MDT creates the VHD files in the VHD folder in the root of this drive.

> [!NOTE]
>  If this property is omitted, MDT attempts to create the VHD files in the VHD folder in the root of the first system drive.

 This property is commonly set using a task sequence step created using the **Create Virtual Hard Disk \(VHD\)** task sequence type. You can override the value that the **Create Virtual Hard Disk \(VHD\)** task sequence step sets by configuring this property in CustomSettings.ini.

> [!NOTE]
>  To configure this property in CustomSettings.ini, you must add this property to the **Properties** line in CustomSettings.ini.

 For related properties that are used with VHD files, see:

-   **VHDCreateDiffVHD**

-   **VHDCreateFileName**

-   **VHDCreateSizeMax**

-   **VHDCreateSource**

-   **VHDCreateType**

-   **VHDDrives**

-   **VHDOutputVariable**

-   **VHDTargetDisk**

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*variable*|Variable that contains the drive letter on the target computer where the VHD files will be created. MDT creates the VHD files in the VHD folder in the root of this drive. For example, if this property has a value of **VHDTargetDisk**, the **VHDTargetDisk** property contains the drive letter \(such as *H*\).|

|**Example**|
|-|
|`VHDCreateSizeMax=130048 VHDCreateType=EXPANDABLE VHDCreateFileName=Win7_C.vhd  VHDInputVariable=VHDTargetDisk`|

###  <a name="VHDOutputVariable"></a> VHDOutputVariable
 This property contains a variable that contains the physical drive number that was assigned to the newly created VHD file. Each time a VHD file is created, MDT sets this property to the disk index of the newly created disk using the **Index** property of the **Win32\_DiskDrive** WMI class.

 This property is commonly set using a task sequence step created using the **Create Virtual Hard Disk \(VHD\)** task sequence type. You can override the value that the **Create Virtual Hard Disk \(VHD\)** task sequence step sets by configuring this property in CustomSettings.ini.

> [!NOTE]
>  To configure this property in CustomSettings.ini, you must add this property to the **Properties** line in CustomSettings.ini.

 For related properties that are used with VHD files, see:

-   **VHDCreateDiffVHD**

-   **VHDCreateFileName**

-   **VHDCreateSizeMax**

-   **VHDCreateSource**

-   **VHDCreateType**

-   **VHDDisks**

-   **VHDInputVariable**

-   **VHDTargetDisk**

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*Variable*|Variable will contains the physical drive number assigned to the newly created VHD file. For example, if this property has a value of **OSDDiskIndex**, the **OSDDiskIndex** property will contain the physical drive number assigned to the newly created VHD file \(such as *4*\).|

|**Example**|
|-|
|None|

###  <a name="VHDTargetDisk"></a> VHDTargetDisk
 Specifies the drive on the target computer where the VHD is to be created. This property is later referenced in the [VHDInputVariable](#VHDInputVariable) property.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

 For related properties that are used with VHD files, see:

-   **VHDCreateDiffVHD**

-   **VHDCreateFileName**

-   **VHDCreateSizeMax**

-   **VHDCreateSource**

-   **VHDCreateType**

-   **VHDDisks**

-   **VHDInputVariable**

-   **VHDOutputVariable**

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*Disk*|Specifies the drive where the VHD is to be created|

|**Example**|
|-|
|None|

###  <a name="VMHost"></a> VMHost
 Specifies the name of the Hyper\-V host running the VM where MDT is running. This property is available only when the Hyper\-V Integration Components are installed and running.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

Table 4 lists the Windows operating systems that MDT supports and their corresponding Hyper\-V Integration Components support.

## Table 4. Windows Operating Systems and Hyper-V Integration Components Support

|**Operating system**|**Hyper-V Integration Components**|
|-|-|
|Windows PE|Integration Components are unavailable.|
|Windows 7|Available by default in Enterprise, Ultimate, and Professional editions.|
|Windows Server 2008 R2|Available by default in all editions.|

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*Name*|The name of the Hyper-V host running the VM where MDT is running|

|**Example**|
|-|
|None|

###  <a name="VMName"></a> VMName
 Specifies the name of the VM where MDT is running. This property is only available when the Hyper-V Integration Components are installed and running.

 Table 5 lists the Windows operating systems supported by MDT and their corresponding Hyper-V Integration Components support.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

## Table 5. Windows Operating Systems and Hyper-V Integration Components Support

|**Operating system**|**Hyper-V Integration Components**|
|-|-|
|Windows PE|Integration Components are unavailable.|
|Windows 7|Available by default in Enterprise, Ultimate, and Professional editions.|
|Windows Server 2008 R2|Available by default in all editions.|

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*name*|The name of the VM where MDT is running|

|**Example**|
|-|
|None|

###  <a name="VMPlatform"></a> VMPlatform
 Specifies specific information about the virtualization environment for the target computer when the target computer is a VM. The VM platform is determined by using WMI.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**Hyper-V**|Hyper-V|
|**VirtualBox**|Virtual Box|
|**VMware**|VMware virtualization platform|
|**Xen**|Citrix Xen Server|

|**Example**|
|-|
|None|

###  <a name="VRefresh"></a> VRefresh
 The vertical refresh rate for the monitor on the target computer. The vertical refresh rate is specified in Hertz. In the example, the value **60** indicates that the vertical refresh rate of the monitor is 60 Hz. This value is inserted into the appropriate configuration settings in Unattend.xml.

> [!NOTE]
>  The default values (in the Unattend.xml template file) are 1,024 pixels horizontal resolution, 768 pixels vertical resolution, 32-bit color depth, and 60 Hz vertical refresh rate.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*refresh_rate*|The vertical refresh rate for the monitor on the target computer in Hertz|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] BitsPerPel=32 VRefresh=60 XResolution=1024 YResolution=768`|

###  <a name="VSSMaxSize"></a> VSSMaxSize
 This property is used to pass a value to the **maxsize** parameter of the **vssadmin resize shadowstorage** command in the **Vssadmin** command. The **maxsize** parameter is used to specify the maximum amount of space on the target volume that can be used for storing shadow copies. For more information on the **maxsize** parameter, see [Vssadmin resize shadowstorage](https://technet.microsoft.com/library/cc788050\(WS.10\).aspx).

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*maxsize_value*|Specifies the maximum amount of space that can be used for storing shadow copies. The value can be specified in bytes or as a percentage of the target volume.<br /><br /> To specify the value:<br /><br /> - In bytes, the value must be 300 MB or greater and accept the following suffixes: KB, MB, GB, TB, PB and EB. You can also use B, K, M, G, T, P, and E as suffixes—for example:<br /><br /> `VSSMaxSize=60G`<br /><br /> - As a percentage, use the % character as the suffix to the numeric value—for example:<br /><br /> `VSSMaxSize=20%`<br /><br /> Note:<br /><br /> If a suffix is not supplied, the default suffix is bytes. For example, `VSSMaxSize=1024` indicates that the **VSSMaxSize** will be set to 1,024 bytes.<br /><br /> If the value is set to **UNBOUNDED**, then there is no limit placed on the amount of storage space that can be used—for example:<br /><br /> `VSSMaxSize=UNBOUNDED`|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] VSSMaxSize=25%`|

###  <a name="WDSServer"></a> WDSServer
 The computer running Windows Deployment Services that is used for installing Windows Deployment Services images. The default value is the server running Windows Deployment Services from which the image was initiated.

> [!NOTE]
>  This property is dynamically set by the MDT scripts and is not configured in CustomSettings.ini or the MDT DB. Treat this property as read only.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*WDS_server*|The name of the computer running Windows Deployment Services|

|**Example**|
|-|
|None|

###  <a name="WindowsSource"></a> WindowsSource
 MDT uses this property to set the location of the sources\sxs folder in a network shared folder that contains the operating system source files. This property is used when:

- MDT is running a custom task sequence or deploying a custom image

- MDT is installing roles or features in Windows 8 and Windows Server 2012

- The computer does not have access to the Internet

  When the situation described in the bulleted list above occurs, MDT may be unable to find the operating system source files locally, and the installation will attempt to download the files from the Internet. Because the computer does not have Internet access, the process will fail. Setting this property to the appropriate value helps prevent this problem from occurring.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|***folder_unc***|A UNC path to the Sources\sxs folder for the operating system being deployed.<br /><br /> Note:<br /><br /> The UNC path must include the Sources\sxs folder.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] WindowsSource=%DeployRoot%\Operating Systems\Windows 8\Sources\sxs`|

###  <a name="WipeDisk"></a> WipeDisk
 Specifies whether the disk should be wiped. If **WipeDisk** is TRUE, the ZTIWipeDisk.wsf script will clean the disk using the **Format** command. The **Format** command is not the most "secure" way of wiping the disk.

 Securely wiping the disk should be done so in a manner that follows the U.S. Department of Defense standard 5220.22-M, which states, "To clear magnetic disks, overwrite all locations three times (first time with a character, second time with its complement, and the third time with a random character)."

 When MDT wipes the disk, it uses the **Format** command with the **/P:3** switch, which instructs **Format** to zero every sector on the volume and to perform the operation three times. There is no way to tell the **Format** command to use a particular character or a random character.

> [!NOTE]
>  If the disk must be securely wiped, a non-Microsoft secure disk wipe tool should be added to the task sequence using the **Run Command Line** task sequence step.

> [!CAUTION]
>  This property value must be specified in uppercase letters so that the deployment scripts can properly read it.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|**TRUE**|If **WipeDisk** is set to **TRUE**, the Win32_DiskPartition at DiskIndex 0 and Index 0 will be formatted.|
|**FALSE**|The disk will not be formatted.|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] WipeDisk=TRUE`|

###  <a name="WizardSelectionProfile"></a> WizardSelectionProfile
 Profile name used by the wizard for filtering the display of various items.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*profile_name*|Profile name used by the wizard for filtering the display of various items|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] WizardSelectionProfile=SelectTaskSequenceOnly`|

###  <a name="WSUSServer"></a> WSUSServer
 This is the name of the Windows Server Update Services (WSUS) server that the target computer should use when scanning for, downloading, and installing updates.

 For more information about what script uses this property, see [ZTIWindowsUpdate.wsf](#ZTIWindowsUpdate.wsf).

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*server_name*|The name of the WSUS server, specified in HTTP format|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] WSUSServer=https://WSUSServerName[Settings] Priority=Default  [Default] WSUSServer=https://WSUSServerName`|

###  <a name="WUMU_ExcludeKB"></a> WUMU_ExcludeKB
 The list of Windows Update/Microsoft Update software updates to ignore (by associated Knowledge Base articles).

 Deployment project team members will want to periodically review the list of updates being installed by the ZTIWindowsUpdate.wsf script to verify that each update meets the project's needs and expectations. All updates are logged and recorded in the ZTIWindowsUpdate.log file, which is generated during deployment. Each update will indicate its status as INSTALL or SKIP and lists the UpdateID, the update name, and the QNumber associated with each update. If an update needs to be excluded, that update should be added to the CustomSettings.ini file (for LTI deployments).

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*WUMU_ExcludeKB*|The list of Windows Update/Microsoft Update software updates to ignore by QNumber|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] WUMU_ExcludeKB1=925471`|

### WUMU_ExcludeID
 The list of Windows Update/Microsoft Update software updates to ignore (by associated update ID).

 Deployment project team members will want to periodically review the list of updates being installed by the ZTIWindowsUpdate.wsf script to verify that each update meets the project's needs and expectations. All updates are logged and recorded in the ZTIWindowsUpdate.log file, which is generated during deployment. Each update will indicate its status as INSTALL or SKIP and lists the UpdateID, the update name, and the QNumber associated with each update. If an update should be excluded, that update should be added to the CustomSettings.ini file (for LTI deployments).

 For example, if the installation of the Windows Malicious Software Removal Tool should be excluded, look up the line in the ZTIWindowsUpdate.log that shows where the update was identified and installed, and then select the UpdateID number. For example, the UpdateID number for the Windows Malicious Software Removal Tool is adbe6425-6560-4d40-9478-1e35b3cdab4f.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*WUMU_ExcludeID*|The list of Windows Update/Microsoft Update software updates to ignore, by UpdateID number|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] WUMU_ExcludeID1={adbe6425-6560-4d40-9478-1e35b3cdab4f}[Settings] Priority=Default  [Default] WUMU_ExcludeID1={adbe6425-6560-4d40-9478-1e35b3cdab4f}`|

###  <a name="XResolution"></a> XResolution
 The horizontal resolution of the monitor on the target computer, specified in pixels. In the example, the value **1024** indicates the horizontal resolution of the monitor is 1,024 pixels. This value is inserted into the appropriate configuration settings in Unattend.xml.

> [!NOTE]
>  The default values (in the Unattend.xml template file) are 1,024 pixels horizontal resolution, 768 pixels vertical resolution, 32-bit color depth, and 60 Hz vertical refresh rate.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*horizontal_resolution*|The horizontal resolution of the monitor on the target computer in pixels|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] BitsPerPel=32 VRefresh=60 XResolution=1024 YResolution=768[Settings] Priority=Default  [Default] BitsPerPel=32 VRefresh=60 XResolution=1024 YResolution=768`|

###  <a name="YResolution"></a> YResolution
 The vertical resolution of the monitor on the target computer, specified in pixels. In the example, the value **768** indicates the vertical resolution of the monitor is 768 pixels. This value gets inserted into the appropriate configuration settings in Unattend.xml.

> [!NOTE]
>  The default values (in the Unattend.xml template file) are 1,024 pixels horizontal resolution, 768 pixels vertical resolution, 32-bit color depth, and 60 Hz vertical refresh rate.

|Property configured by|Property applies to|
|-|-|
|BootStrap.ini|LTI|
|CustomSettings.ini|-|
|MDT DB|ZTI|

|**Value**|**Description**|
|-|-|
|*vertical_resolution*|The vertical resolution of the monitor on the target computer in pixels|

|**Example**|
|-|
|`[Settings] Priority=Default  [Default] BitsPerPel=32 VRefresh=60 XResolution=1024 YResolution=768[Settings] Priority=Default  [Default] BitsPerPel=32 VRefresh=60 XResolution=1024 YResolution=768`|

##  <a name="ProvidingPropertiesforSkippedDeploymentWizardPages"></a> Providing Properties for Skipped Deployment Wizard Pages
 Table 6 lists the individual Deployment Wizard pages, the property to skip the corresponding wizard page, and the properties that must be configured when skipping the wizard page.

 If the **SkipWizard** property is used to skip all the Deployment Wizard pages, provide all the properties in the **Configure these properties** column. For examples of various deployment scenarios that skip Deployment Wizard pages, see the section, "Fully Automated LTI Deployment Scenario", in the MDT document *Microsoft Deployment Toolkit Samples Guide*.

> [!NOTE]
>  In instances where the **Configure These Properties** column is blank, no properties need to be configured when skipping the corresponding wizard page.

## Table 6. Deployment Wizard Pages

|**Skip this wizard page**|**Using this property**|**Configure these properties**|
|-|-|-|
|**Welcome**|SkipBDDWelcome||
|**Specify credentials for connecting to network shares**|Skipped by providing properties in next column|- UserID<br /><br /> - UserDomain<br /><br /> - UserPassword|
|**Task Sequence**|SkipTaskSequence|- TaskSequenceID|
|**Computer Details**|SkipComputerName,<br /><br /> SkipDomainMembership|- OSDComputerName<br /><br /> - JoinWorkgroup<br /><br /> –or–<br /><br /> - JoinDomain<br /><br /> - DomainAdmin|
|**User Data**|SkipUserData|- UDDir<br /><br /> - UDShare<br /><br /> - UserDataLocation|
|**Move Data and Settings**|SkipUserData|- UDDir<br /><br /> - UDShare<br /><br /> - UserDataLocation|
|**User Data (Restore)**|SkipUserData|- UDDir<br /><br /> - UDShare<br /><br /> - UserDataLocation|
|**Computer Backup**|SkipComputerBackup|- BackupDir<br /><br /> - BackupShare<br /><br /> - ComputerBackupLocation|
|**Product Key**|SkipProductKey|- ProductKey<br /><br /> –or–<br /><br /> - OverrideProductKey|
|**Language Packs**|SkipPackageDisplay|LanguagePacks|
|**Locale and Time**|SkipLocaleSelection, SkipTimeZone|- KeyboardLocale<br /><br /> - UserLocale<br /><br /> - UILanguage<br /><br /> - TimeZoneName|
|**Roles and Features**|SkipRoles|- OSRoles<br /><br /> - OSRoleServices<br /><br /> - OSFeatures|
|**Applications**|SkipApplications|Applications|
|**Administrator Password**|SkipAdminPassword|AdminPassword|
|**Local Administrators**|SkipAdminAccounts|- Administrators|
|**Capture Image**|SkipCapture|- ComputerBackupLocation|
|**Bitlocker**|SkipBitLocker|- BDEDriveLetter<br /><br /> - BDEDriveSize<br /><br /> - BDEInstall<br /><br /> - BDEInstallSuppress<br /><br /> - BDERecoveryKey<br /><br /> - TPMOwnerPassword<br /><br /> - OSDBitLockerStartupKeyDrive<br /><br /> - OSDBitLockerWaitForEncryption|
|**Ready to begin**|SkipSummary|–|
|**Operating system deployment completed successfully**|SkipFinalSummary|–|
|**Operating system deployment did not complete successfully**|SkipFinalSummary|–|
