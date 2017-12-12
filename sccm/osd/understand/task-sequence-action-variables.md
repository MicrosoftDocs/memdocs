---
title: Task sequence action variables
titleSuffix: "Configuration Manager"
description: "Use sequence action variables, such as network setting variables, to specify configuration settings for a single step in a Configuration Manager task sequence."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e2269031-0977-4f01-a274-420e00630575
caps.latest.revision: 10
caps.handback.revision: 0
author: aczechowski
ms.author: aaroncz
manager: angrobe

---
# Task sequence action variables in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Task sequence action variables specify configuration settings that are used by a single step in a System Center Configuration Manager task sequence. By default, the settings used by a task sequence step are initialized before the step is run and available only while the associated task sequence step is run. In other words, the task sequence variable setting is added to the task sequence environment before the task sequence step is run, and the value is removed from the task sequence environment after the task sequence step has run.  

## Action Variable Example  
 For example, you can specify a start-in directory for a command-line action by using the **Run Command Line** task sequence step. This step includes a **Start In** property whose default value is stored in the task sequence environment as the **WorkingDirectory** variable. The **WorkingDirectory** environment variable is initialized before the **Run Command Line** task sequence action is run. During the **Run Command Line** step, the **WorkingDirectory** value can be accessed through the **Start In** property. Then after the task sequence step is completed, the value of the **WorkingDirectory** variable is removed from the task sequence environment. If the sequence contains another **Run Command Line** task sequence step, the new **WorkingDirectory** variable is initialized and set to the starting value for that task sequence step.  

 Whereas the default value for a task sequence action setting is present while the task sequence step is run, any new value that you set can be used by multiple steps in the sequence. If you use one of the task sequence variable creation methods to override a built-in variable value, the new value remains in the environment and overrides the default value for other steps in the task sequence. In the previous example, if a **Set Task Sequence Variable** step is added as the first step of the task sequence and sets the **WorkingDirectory** environment variable to the value **C:\\**, both **Run Command Line** steps in the task sequence will use the new starting directory value.  

## Action Variables for Task Sequence Actions  
 Configuration Manager task sequence variables are grouped by their associated task sequence action. Use the following links to gather information about the action variables associated with a specific action. The task sequence variables govern how the task sequence action operates. The task sequence action reads and uses the variables that you mark as input variables. Alternatively, you can use the Set Task Sequence Variable action or the TSEnvironment COM object to set the variables at runtime. Only the task sequence action marks variables as output variables, which are read by actions that occur later in the task sequence.  

> [!NOTE]  
>  Not all task sequence actions are associated with a set of task sequence variables. For example, although there are variables associated with the Enable BitLocker action, there are no variables associated with the Disable BitLocker action.  

###  <a name="BKMK_ApplyDataImage"></a> Apply Data Image Task Sequence Action Variables  
 The variables for this action specify which image of a WIM file is applied to the destination computer and whether to delete the files on the destination partition. For more information about the task sequence step associated with these variables, see [Apply Data Image Task Sequence Step](task-sequence-steps.md#BKMK_ApplyDataImage).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|OSDDataImageIndex<br /><br /> (input)|Specifies the index value of the image that is applied to the destination computer.|  
|OSDWipeDestinationPartition<br /><br /> (input)|Specifies whether to delete the files located on the destination partition.<br /><br /> Valid values:<br /><br /> **"true"** (default)<br /><br /> **"false"**|  

###  <a name="BKMK_ApplyDriverPackage"></a> Apply Driver Package Task Sequence Action Variables  
 The variables for this action specify information the installation of mass storage drivers and whether to install unsigned drivers. For more information about the task sequence step associated with these variables, see [Apply Driver Package](task-sequence-steps.md#BKMK_ApplyDriverPackage).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|OSDApplyDriverBootCriticalContentUniqueID<br /><br /> (input)|Specifies the content ID of the mass storage device driver to install from the driver package. If this is not specified, no mass storage driver is installed.|  
|OSDApplyDriverBootCriticalINFFile<br /><br /> (input)|Specifies the INF file of the mass storage driver to install.<br /><br /> <br /><br /> This task sequence variable is required if the OSDApplyDriverBootCriticalContentUniqueID is set.|  
|OSDApplyDriverBootCriticalHardwareComponent<br /><br /> (input)|Specifies whether a mass storage device driver is installed, this must be **scsi**.<br /><br /> <br /><br /> This task sequence variable is required if the OSDApplyDriverBootCriticalContentUniqueID is set.|  
|OSDApplyDriverBootCriticalID<br /><br /> (input)|Specifies the boot critical ID of the mass storage device driver to install. This ID is listed in the "**scsi**" section of the device driver's txtsetup.oem file.<br /><br /> <br /><br /> This task sequence variable is required if the OSDApplyDriverBootCriticalContentUniqueID is set.|  
|OSDAllowUnsignedDriver<br /><br /> (input)|Specifies whether to configure Windows to allow the installation of unsigned device drivers. This task sequence variable is not used when deploying the Windows Vista and later operating system.<br /><br /> Valid values:<br /><br /> **"true"**<br /><br /> **"false"** (default)|  

###  <a name="BKMK_ApplyNetworkSettings"></a> Apply Network Settings Task Sequence Action Variables  
 The variables for this action specify network settings for the destination computer, such as settings for the network adapters of the computer, domain settings and workgroup settings. For more information about the task sequence step associated with these variables, see [Apply Network Settings Step](task-sequence-steps.md#BKMK_ApplyNetworkSettings).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|OSDAdapter<br /><br /> (input)|This task sequence variable is an array variable. Each element in the array represents the settings for a single network adapter on the computer. The settings defined for each adapter are accessed by combining the array variable name with the zero-based network adapter index and the property name.<br /><br /> <br /><br /> If multiple network adapters will be configured with this task sequence action, the properties for the second network adapter are defined by using their index in the variable name; for example, OSDAdapter1EnableDHCP, OSDAdapter1IPAddressList, OSDAdapter1DNSDomain, OSDAdapter1WINSServerList, OSDAdapter1EnableWINS, and so on.<br /><br /> <br /><br /> For example, the following variable names can be used to define the properties for the first network adapter that will be configured by this task sequence action:<br /><br /> <ul><li>**OSDAdapter0EnableDHCP** - true to enable Dynamic Host Configuration Protocol (DHCP) for the adapter.<br />    This setting is required. Possible values are:  True or False.</li><li>**OSDAdapter0IPAddressList** - Comma-delimited list of IP addresses for the adapter. This property is ignored unless **EnableDHCP** is set to **false**.<br />    This setting is required.</li><li>**OSDAdapter0SubnetMask** - Comma-delimited list of subnet masks. This property is ignored unless **EnableDHCP** is set to **false**.<br />    This setting is required.</li><li>**OSDAdapter0Gateways** - Comma-delimited list of IP gateway addresses. This property is ignored unless **EnableDHCP** is set to **false**.<br />    This setting is required.</li><li>**OSDAdapter0DNSDomain** - Domain Name System (DNS) domain for the adapter.</li><li>**OSDAdapter0DNSServerList** - Comma-delimited list of DNS servers for the adapter.<br />    This setting is required.</li><li>**OSDAdapter0EnableDNSRegistration** - **true** to register the IP address for the adapter in DNS.</li><li>**OSDAdapter0EnableFullDNSRegistration** - **true** to register the IP address for the adapter in DNS under the full DNS name for the computer.</li><li>**OSDAdapter0EnableIPProtocolFiltering** - **true** to enable IP protocol filtering on the adapter.</li><li>**OSDAdapter0IPProtocolFilterList** - Comma-delimited list of protocols allowed to run over IP. This property is ignored if **EnableIPProtocolFiltering** is set to **false**.</li><li>**OSDAdapter0EnableTCPFiltering** - **true** to enable TCP port filtering for the adapter.</li><li>**OSDAdapter0TCPFilterPortList** - Comma-delimited list of ports to be granted access permissions for TCP. This property is ignored if **EnableTCPFiltering** is set to **false**.</li><li>**OSDAdapter0TcpipNetbiosOptions** - Options for NetBIOS over TCP/IP. Possible values are as follows:<br /><br /> <ul><li>0 Use NetBIOS settings from DHCP server.</li><li>1 Enable NetBIOS over TCP/IP.</li><li>2 Disable NetBIOS over TCP/IP.</li></ul></li><li>**OSDAdapter0EnableWINS** - **true** to use WINS for name resolution.</li><li>**OSDAdapter0WINSServerList** - Comma-delimited list of WINS server IP addresses. This property is ignored unless **EnableWINS** is set to **true**.</li><li>**OSDAdapter0MacAddress** - Media access controller (MAC) address used to match settings to physical network adapter.</li><li>**OSDAdapter0Name** - Name of the network connection as it appears in the network connections control panel program. The name is between 0 and 255 characters in length.</li><li>**OSDAdapter0Index** - Index of the network adapter settings in the array of settings.<br /><br />     OSDAdapterCount=1<br />    OSDAdapter0EnableDHCP=FALSE<br />    OSDAdapter0IPAddressList=192.168.0.40<br />    OSDAdapter0SubnetMask=255.255.255.0<br />    OSDAdapter0Gateways=192.168.0.1<br />    OSDAdapter0DNSSuffix=contoso.com</li></ul>|  
|OSDAdapterCount<br /><br /> (input)|Specifies the number of network adapters installed on the destination computer. When the **OSDAdapterCount** value is set, all the configuration options for each adapter must be set. For example, if you set the **OSDAdapterTCPIPNetbiosOptions** value for a specific adapter then all the values for that adapter must also be configured.<br /><br /> <br /><br /> If this value is not specified, all **OSDAdapter** values are ignored.|  
|OSDDNSDomain<br /><br /> (input)|Specifies the primary DNS server that is used by the destination computer.|  
|OSDDomainName<br /><br /> (input)|Specifies the name of the Windows domain that the destination computer joins. The specified value must be a valid Active Directory Domain Services domain name.|  
|OSDDomainOUName<br /><br /> (input)|Specifies the RFC 1779 format name of the organizational unit (OU) that the destination computer joins. If specified, the value must contain the full path.<br /><br /> Example:<br /><br /> **LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com**|  
|OSDEnableTCPIPFiltering<br /><br /> (input)|Specifies whether TCP/IP filtering is enabled.<br /><br /> Valid values:<br /><br /> **"true"**<br /><br /> **"false"** (default)|  
|OSDJoinAccount<br /><br /> (input)|Specifies the network account that is used to add the destination computer to a Windows domain.|  
|OSDJoinPassword<br /><br /> (input)|Specifies the network password that is used to add the destination computer to a Windows domain.|  
|OSDNetworkJoinType<br /><br /> (input)|Specifies whether the destination computer joins a Windows domain or a workgroup.<br /><br /> **"0"** indicates that the destination computer joins a Windows domain. **"1"** specifies that the computer joins a workgroup.<br /><br /> Valid values:<br /><br /> **"0"**<br /><br /> **"1"**|  
|OSDDNSSuffixSearchOrder<br /><br /> (input)|Specifies the DNS search order for the destination computer.|  
|OSDWorkgroupName<br /><br /> (input)|Specifies the name of the workgroup that the destination computer joins.<br /><br /> You must specify either this value or the **OSDDomainName** value. The workgroup name can be a maximum of 32 characters.<br /><br /> Example:<br /><br /> **"Accounting"**|  

###  <a name="BKMK_ApplyOperatingSystem"></a> Apply Operating System Image Task Sequence Action Variables  
 The variables for this action specify settings for the operating system that you want to install on the destination computer. For more information about the task sequence step associated with these variables, see [Apply Operating System Image](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|OSDConfigFileName<br /><br /> (input)|Specifies the file name of the operating system deployment answer file associated with the operating system deployment package.|  
|OSDImageIndex<br /><br /> (input)|Specifies the image index value of the WIM file that is applied to the destination computer.|  
|OSDInstallEditionIndex<br /><br /> (input)|Specifies the version of Windows Vista or later operating system that is installed. If no version is specified, Windows setup will determine which version to install using the referenced product key.<br /><br /> Use only a value of zero (0) if the following conditions are true:<br /><br /> -   You are installing a pre-Windows Vista operating system<br />-   You are installing a volume license edition of Windows Vista or later, and no product key is specified.<br /><br /> Valid values:<br /><br /> **"0"** (default)|  
|OSDTargetSystemDrive (output)|Specifies the drive letter of the partition that contains the operating system files.|  

###  <a name="BKMK_ApplyWindowsSettings"></a> Apply Windows Settings Task Sequence Action Variables  
 The variables for this action specify Windows settings for the destination computer, such as the computer name, Windows product key, registered user and organization, and the local administrator password. For more information about the task sequence step associated with these variables, see [Apply Windows Settings](task-sequence-steps.md#BKMK_ApplyWindowsSettings).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|OSDComputerName<br /><br /> (input)|Specifies the name of the destination computer.<br /><br /> Example:<br /><br /> **"%_SMSTSMachineName%"** (default)|  
|OSDProductKey<br /><br /> (input)|Specifies the Windows product key. The specified value must be between 1 and 255 characters.|  
|OSDRegisteredUserName<br /><br /> (input)|Specifies the default registered user name in the new operating system. The specified value must be between 1 and 255 characters.|  
|OSDRegisteredOrgName<br /><br /> (input)|Specifies the default registered organization name in the new operating system. The specified value must be between 1 and 255 characters.|  
|OSDTimeZone<br /><br /> (input)|Specifies the default time zone setting that is used in the new operating system.|  
|OSDServerLicenseMode<br /><br /> (input)|Specifies the Windows Server license mode that is used.<br /><br /> Valid values:<br /><br /> **"PerSeat"**<br /><br /> **"PerServer"**|  
|OSDServerLicenseConnectionLimit<br /><br /> (input)|Specifies the maximum number of connections allowed. The specified number must be in the range between 5 and 9999 connections.|  
|OSDRandomAdminPassword<br /><br /> (input)|Specifies a randomly generated password for the administrator account in the new operating system. If set to **true**, the local administrator account will be disabled on the target computer. If set to **false**, the local administrator account will be enabled on the target computer, and the local administrator account password will be assigned the value of the variable **OSDLocalAdminPassword**.<br /><br /> Valid values:<br /><br /> **"true"** (default)<br /><br /> **"false"**|  
|OSDLocalAdminPassword<br /><br /> (input)|Specifies the local administrator password. This value is ignored if the **Randomly generate the local administrator password and disable the account on all supported platforms** option is enabled. The specified value must be between 1 and 255 characters.|  

###  <a name="BKMK_AutoApplyDrivers"></a> Auto Apply Drivers Task Sequence Action Variables  
 The variables for this action specify which Windows drivers are installed on the destination computer and whether unsigned drivers are installed. For more information about the task sequence step associated with these variables, see [Auto Apply Drivers](task-sequence-steps.md#BKMK_AutoApplyDrivers).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|OSDAutoApplyDriverCategoryList<br /><br /> (input)|A comma-delimited list of the driver catalog category unique IDs. If specified, the **Auto Apply Driver** task sequence action considers only those drivers that are in at least one of these categories when installing drivers. This value is optional, and it is not set by default. The available category IDs can be obtained by enumerating the list of **SMS_CategoryInstance** objects on the site.|  
|OSDAllowUnsignedDriver<br /><br /> (input)|Specifies whether Windows is configured to allow unsigned device drivers to be installed. This task sequence variable is not used when deploying Windows Vista and later operating systems.<br /><br /> Valid values:<br /><br /> **"true"**<br /><br /> **"false"** (default)|  
|OSDAutoApplyDriverBestMatch<br /><br /> (input)|Specifies what the task sequence action does if there are multiple device drivers in the driver catalog that are compatible with a hardware device. If set to **"true"**, only the best device driver will be installed.  If **false**, all compatible device drivers will be installed, and the operating system will choose the best driver to use.<br /><br /> Valid values:<br /><br /> **"true"** (default)<br /><br /> **"false"**|  

###  <a name="BKMK_CaptureNetworkSettings"></a> Capture Network Settings Task Sequence Action Variables  
 The variables for this action specify whether the network adapter settings (TCP/IP, DNS, and WINS) configuration information is captured and whether the workgroup or domain membership information is migrated as part of the operating system deployment. For more information about the task sequence step associated with these variables, see [Capture Network Settings](task-sequence-steps.md#BKMK_CaptureNetworkSettings).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|OSDMigrateAdapterSettings<br /><br /> (input)|Specifies whether the network adapter settings (TCP/IP, DNS, and WINS) configuration information is captured.<br /><br /> Examples:<br /><br /> **"true"** (default)<br /><br /> **"false"**|  
|OSDMigrateNetworkMembership<br /><br /> (input)|Specifies whether the workgroup or domain membership information is migrated as part of the operating system deployment.<br /><br /> Examples:<br /><br /> **"true"** (default)<br /><br /> **"false"**|  

###  <a name="BKMK_CaptureOperatingSystemImage"></a> Capture Operating System Image Task Sequence Action Variables  
 The variables for this action specify information about the operating system image that is being captured, such as where the image is stored, who created the image, and a description of the image. For more information about the task sequence step associated with these variables, see [Capture Operating System Image](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|OSDCaptureAccount<br /><br /> (input)|Specifies a Windows account name that has permissions to store the captured image on a network share.|  
|OSDCaptureAccountPassword<br /><br /> (input)|Specifies the password for the Windows account used to store the captured image on a network share.|  
|OSDCaptureDestination<br /><br /> (input)|Specifies the location where the captured operating system image is saved. The maximum directory name length is 255 characters.|  
|OSDImageCreator<br /><br /> (input)|An optional name of the user who created the image. This name is stored in the WIM file. The maximum length of the user name is 255 characters.|  
|OSDImageDescription<br /><br /> (input)|An optional user-defined description of the captured operating system image. This description is stored in the WIM file. The maximum length of the description is 255 characters.|  
|OSDImageVersion<br /><br /> (input)|An optional user-defined version number to assign to the captured operating system image. This version number is stored in the WIM file. This value can be any combination of letters with a maximum length of 32 characters.|  
|OSDTargetSystemRoot<br /><br /> (input)|Specifies the path to the Windows directory of the installed operating system on the reference computer. This operating system is verified as being a supported operating system for capture by Configuration Manager.|  

###  <a name="BKMK_CaptureUserState"></a> Capture User State Task Sequence Action Variables  
 The variables for this action specify information used by the User State Migration Tool (USMT), such as the folder where the user state is saved, command-line options for USMT, and the configuration files used to control the capture of the user profiles.  For more information about the task sequence step associated with these variables, see [Capture User State](task-sequence-steps.md#BKMK_CaptureUserState).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (input)|The UNC or local path name of the folder where the user state is saved. No default.|  
|OSDMigrateAdditionalCaptureOptions<br /><br /> (input)|Specifies user state migration tool (USMT) command line options that are used when capturing the user state, but not exposed in the Configuration Manager user interface. The additional options are specified in the form of a string that is appended to the automatically generated USMT command line.<br /><br /> <br /><br /> The USMT options specified with this task sequence variable are not validated for accuracy prior to running the task sequence.|  
|OSDMigrateMode<br /><br /> (input)|Allows you to customize the files that are captured by USMT. If this variable is set to "Simple," then only the standard USMT configuration files are used. If this variable is set to "Advanced," then the task sequence variable OSDMigrateConfigFiles specifies the configuration files that the USMT uses.<br /><br /> Valid values:<br /><br /> **"Simple"**<br /><br /> **"Advanced"**|  
|OSDMigrateConfigFiles<br /><br /> (input)|Specifies the configuration files used to control the capture of user profiles. This variable is used only if OSDMigrateMode is set to "Advanced". This comma-delimited list value is set to perform customized user profile migration.<br /><br /> Example: miguser.xml,migsys.xml,migapps.xml|  
|OSDMigrateContinueOnLockedFiles<br /><br /> (input)|Allows the user state capture to proceed if some files cannot be captured.<br /><br /> Valid values:<br /><br /> **"true"** (default)<br /><br /> **"false"**|  
|OSDMigrateEnableVerboseLogging<br /><br /> (input)|Enables verbose logging for the USMT.<br /><br /> Valid values:<br /><br /> **"true"**<br /><br /> **"false"** (default)|  
|OSDMigrateSkipEncryptedFiles<br /><br /> (input)|Specifies whether encrypted files are captured.<br /><br /> Valid values:<br /><br /> **"true"**<br /><br /> **"false"** (default)|  
|_OSDMigrateUsmtPackageID<br /><br /> (input)|Specifies the package ID of the Configuration Manager package that will contain the USMT files. This variable is required.|  

###  <a name="BKMK_CaptureWindowsSettings"></a> Capture Windows Settings Task Sequence Action Variables  
 The variables for this action specify whether specific Windows settings are migrated to the destination computer, such as the name of the computer, the register organization name, and time zone information. For more information about the task sequence step associated with these variables, see [Capture Windows Settings](task-sequence-steps.md#BKMK_CaptureWindowsSettings).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|OSDMigrateComputerName<br /><br /> (input)|Specifies whether the computer name is migrated.<br /><br /> Valid values:<br /><br /> **"true"** (default)<br /><br /> **"false"**<br /><br /> If the value is "true," then the OSDComputerName variable is set to the NetBIOS name of the computer.|  
|OSDComputerName<br /><br /> (output)|Set to the NetBIOS name of the computer. The value is set only if the OSDMigrateComputerName variable is set to "true."|  
|OSDMigrateRegistrationInfo<br /><br /> (input)|Specifies whether the computer user and organizational information is migrated.<br /><br /> Valid values:<br /><br /> **"true"** (default)<br /><br /> **"false"**<br /><br /> If the value is "true," then the OSDRegisteredOrgName variable is set to the registered organization name of the computer.|  
|OSDRegisteredOrgName<br /><br /> (output)|Set to the registered organization name of the computer. The value is set only if the OSDMigrateRegistrationInfo variable is set to "true."|  
|OSDMigrateTimeZone<br /><br /> (input)|Specifies whether the computer time zone is migrated.<br /><br /> Valid values:<br /><br /> **"true"** (default)<br /><br /> **"false"**<br /><br /> If the value is "true," then the variable OSDTimeZone is set to the time zone of the computer.|  
|OSDTimeZone<br /><br /> (output)|Set to the time zone of the computer. The value is set only if the OSDMigrateTimeZone variable is set to "true."|  

###  <a name="BKMK_ConnecttoNetworkFolder"></a> Connect to Network Folder Task Sequence Action Variables  
 The variables for this action specify information about a folder on a network, such as the account used and password to connect to the network folder, the drive letter of the folder, and the path to the folder. For more information about the task sequence step associated with these variables, see [Connect To Network Folder](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|SMSConnectNetworkFolderAccount<br /><br /> (input)|Specifies the administrator account that is used to connect to the network share.|  
|SMSConnectNetworkFolderDriveLetter<br /><br /> (input)|Specifies the network drive letter to connect to. This value is optional; if it is not specified, then the network connection is not mapped to a drive letter. If this value is specified, the value must be in the range from D: to Z:.  In addition, do not use X: as it is the drive letter used by Windows PE during the Windows PE phase.<br /><br /> Examples:<br /><br /> **"D:"**<br /><br /> **"E:"**|  
|SMSConnectNetworkFolderPassword<br /><br /> (input)|Specifies the network password that is used to connect to the network share.|  
|SMSConnectNetworkFolderPath<br /><br /> (input)|Specifies the network path for the connection.<br /><br /> Example:<br /><br /> **"\\\servername\sharename"**|  

###  <a name="BKMK_EnableBitLocker"></a> Enable BitLocker Task Sequence Action Variables  
 The variables for this action specify the recovery password and startup key options used to enable BitLocker on the destination computer. For more information about the task sequence step associated with these variables, see [Enable BitLocker](task-sequence-steps.md#BKMK_EnableBitLocker).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|OSDBitLockerRecoveryPassword<br /><br /> (input)|Instead of generating a random recovery password, the **Enable BitLocker** task sequence action uses the specified value as the recovery password. The value must be a valid numerical BitLocker recovery password.|  
|OSDBitLockerStartupKey<br /><br /> (input)|Instead of generating a random startup key for the key management option **Startup Key on USB only,** the **Enable BitLocker** task sequence action uses the Trusted Platform Module (TPM) as the startup key. The value must be a valid, 256-bit Base64-encoded BitLocker startup key.|  

###  <a name="BKMK_FormatPartitionDisk"></a> Format and Partition Disk Task Sequence Action Variables  
 The variables for this action specify information for formatting and partitioning a physical disk, such as the disk number and an array of partition settings. For more information about the task sequence step associated with these variables, see [Format and Partition Disk](task-sequence-steps.md#BKMK_FormatandPartitionDisk).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|OSDDiskIndex<br /><br /> (input)|Specifies the physical disk number to be partitioned.|  
|OSDDiskpartBiosCompatibilityMode<br /><br /> (input)|Specifies whether to disable cache alignment optimizations when partitioning the hard disk for compatibility with certain types of BIOS. This can be necessary when deploying Windows XP or Windows Server 2003 operating systems. For more information, see [article 931760](http://go.microsoft.com/fwlink/?LinkId=134081) and [article 931761](http://go.microsoft.com/fwlink/?LinkId=134082) in the Microsoft Knowledge Base.<br /><br /> Valid values:<br /><br /> **"true"**<br /><br /> **"false"** (default)|  
|OSDGPTBootDisk<br /><br /> (input)|Specifies whether to create an EFI partition on a GPT hard disk so that it can be used as the startup disk on EFI-based computers.<br /><br /> Valid values:<br /><br /> **"true"**<br /><br /> **"false"** (default)|  
|OSDPartitions<br /><br /> (input)|Specifies an array of partition settings; see the SDK topic for accessing array variables in the task sequence environment.<br /><br /> This task sequence variable is an array variable. Each element in the array represents the settings for a single partition on the hard disk. The settings defined for each partition can be accessed by combining the array variable name with the zero-based disk partition number and the property name.<br /><br /> For example, the following variable names can be used to define the properties for the first partition that will be created by this task sequence action on the hard disk:<br /><br /> - **OSDPartitions0Type** - Specifies the type of partition. This is a required property. Valid values are "**Primary**", "**Extended**", "**Logical**", and "**Hidden**".<br />-   **OSDPartitions0FileSystem** - Specifies the type of file system to use when formatting the partition. This is an optional property; if no file system is specified, the partition will not be formatted. Valid values are "**FAT32**" and "**NTFS**".<br />-   **OSDPartitions0Bootable** - Specifies whether the partition is bootable. This is a required property. If this value is set to "**TRUE**" for MBR disks, then this will be made the active partition.<br />-   **OSDPartitions0QuickFormat** - Specifies the type of format that is used. This is a required property. If this value is set to "**TRUE**", a quick format will be performed; otherwise, a full format will be performed.<br />-   **OSDPartitions0VolumeName** - Specifies the name that is assigned to the volume when it is formatted. This is an optional property.<br />-   **OSDPartitions0Size** - Specifies the size of the partition. Units are specified by the **OSDPartitions0SizeUnits** variable. This is an optional property. If this property is not specified, the partition is created using all remaining free space.<br />-   **OSDPartitions0SizeUnits** - Specifies the units that will be used when interpreting the **OSDPartitions0Size** task sequence variable. This is an optional property. Valid values are "**MB**" (default), "**GB**", and "**Percent**".<br />-   **OSDPartitions0VolumeLetterVariable** - Partitions will always use the next available drive letter in Windows PE when they are created. Use this optional property to specify the name of another task sequence variable, which will be used to save the new drive letter for future reference.<br /><br /> <br /><br /> If multiple partitions will be defined with this task sequence action, the properties for the second partition can be defined by using their index in the variable name; for example, **OSDPartitions1Type**, **OSDPartitions1FileSystem**, **OSDPartitions1Bootable**, **OSDPartitions1QuickFormat**, **OSDPartitions1VolumeName,** and so on.|  
|OSDPartitionStyle<br /><br /> (input)|Specifies the partition style to use when partitioning the disk. "**MBR**" indicates the master boot record partition style, and "**GPT**" indicates the GUID Partition Table style.<br /><br /> Valid Values:<br /><br /> **"GPT"**<br /><br /> **"MBR"**|  

###  <a name="BKMK_InstallSoftwareUpdates"></a> Install Software Updates Task Sequence Action Variables  
 The variable for this action specifies whether to install all updates or only mandatory updates. For more information about the task sequence step associated with these variables, see [Install Software Updates](task-sequence-steps.md#BKMK_InstallSoftwareUpdates).  

#### Details  

|Action Variable Name<br /><br /> (input)|Description|  
|----------------------------------------|-----------------|  
|SMSInstallUpdateTarget<br /><br /> (input)|Specifies whether to install all updates or only mandatory updates.<br /><br /> Valid values:<br /><br /> **"All"**<br /><br /> **"Mandatory"**|  

###  <a name="BKMK_JoinDomainWorkgroup"></a> Join Domain or Workgroup Task Sequence Action Variables  
 The variables for this action specify information needed to join the destination computer to a Windows domain or workgroup. For more information about the task sequence step associated with these variables, see [Join Domain or Workgroup](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|OSDJoinAccount<br /><br /> (input)|Specifies the account that is used by the destination computer to join the Windows domain. This variable is required when joining a domain.|  
|OSDJoinDomainName<br /><br /> (input)|Specifies the name of a Windows domain the destination computer joins. The length of the Windows domain name must be between 1 and 255 characters.|  
|OSDJoinDomainOUName<br /><br /> (input)|Specifies the RFC 1779 format name of the organizational unit (OU) that the destination computer joins. If specified, the value must contain the full path. The length of the Windows domain OU name must be between 0 and 32,767 characters. This value is not set if the **OSDJoinType** variable is set to "1" (join workgroup).<br /><br /> Example:<br /><br /> **LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com**|  
|OSDJoinPassword<br /><br /> (input)|Specifies the network password that is used by the destination computer to join the Windows domain. If the variable is not specified then a blank password is tried. This value is required if the variable **OSDJoinType** variable is set to "**0**" (join domain).|  
|OSDJoinSkipReboot<br /><br /> (input)|Specifies whether to skip restarting after the destination computer joins the domain or workgroup.<br /><br /> Valid values:<br /><br /> **"true"**<br /><br /> **"false"**|  
|OSDJoinType<br /><br /> (input)|Specifies whether the destination computer joins a Windows domain or a workgroup. To join the destination computer to a Windows domain specify "**0**". To join the destination computer to a workgroup specify "**1**".<br /><br /> Valid values:<br /><br /> **"0"**<br /><br /> **"1"**|  
|OSDJoinWorkgroupName<br /><br /> (input)|Specifies the name of a workgroup that the destination computer joins. The length of the workgroup name must be between 1 and 32 characters.<br /><br /> Example:<br /><br /> **"Accounting"**|  

###  <a name="BKMK_PrepareWindowsCapture"></a> Prepare Windows for Capture Task Sequence Action Variables  
 The variables for this action specify information used to capture the Windows operating system from the target computer. For more information about the task sequence step associated with these variables, see [Prepare ConfigMgr Client for Capture](task-sequence-steps.md#BKMK_PrepareConfigMgrClientforCapture).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|OSDBuildStorageDriverList<br /><br /> (input)|Specifies whether sysprep builds a mass storage device driver list. This setting applies to only Windows XP and Windows Server 2003. It will populate the [SysprepMassStorage] section of sysprep.inf with information on all the mass storage drivers that are supported by the image to be captured.<br /><br /> Valid values:<br /><br /> **"true"**<br /><br /> **"false"** (default)|  
|OSDKeepActivation<br /><br /> (input)|Specifies whether sysprep resets the product activation flag.<br /><br /> Valid values:<br /><br /> **"true"**<br /><br /> **"false"** (default)|  
|OSDTargetSystemRoot<br /><br /> (output)|Specifies the path to the Windows directory of the installed operating system on the reference computer. This operating system is verified as being a supported operating system for capture by Configuration Manager.|  

###  <a name="BKMK_ReleaseStateStore"></a> Release State Store Sequence Action Variables  
 The variables for this action specify information used to release the stored user state. For more information about the task sequence step associated with these variables, see [Release State Store](task-sequence-steps.md#BKMK_ReleaseStateStore).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (input)|The UNC or local pathname to the location from which the user state is restored. This value is used by both the **Capture User State** task sequence action and the **Restore User State** task sequence action.|  

###  <a name="BKMK_RequestState"></a> Request State Store Task Sequence Action Variables  
 The variables for this action specify information used to request the stored user state, such as the folder on the state migration point where the user data is stored. For more information about the task sequence step associated with these variables, see [Release State Store](../../osd/understand/task-sequence-steps.md#BKMK_ReleaseStateStore).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|OSDStateFallbackToNAA<br /><br /> (input)|Specifies whether the Network Access Account is used as a fallback when the computer account fails to connect to the state migration point.<br /><br /> Valid values:<br /><br /> **"true"**<br /><br /> **"false"** (default)|  
|OSDStateSMPRetryCount<br /><br /> (input)|Specifies the number of times that the task sequence step tries to find a state migration point before the step fails. The specified count must be between 0 and 600.|  
|OSDStateSMPRetryTime<br /><br /> (input)|Specifies the number of seconds that the task sequence step waits between retry attempts. The number of seconds can be a maximum of 30 characters.|  
|OSDStateStorePath<br /><br /> (output)|The UNC path to the folder on the state migration point where the user state is stored.|  

###  <a name="BKMK_RestartComputer"></a> Restart Computer Task Sequence Action Variables  
 The variables for this action specify information used to restart the destination computer. For more information about the task sequence step associated with these variables, see [Restart Computer](task-sequence-steps.md#BKMK_RestartComputer).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|SMSRebootMessage<br /><br /> (input)|Specifies the message to be displayed to users before restarting the destination computer. If this variable is not set, the default message text is displayed. The specified message must not exceed 512 characters.<br /><br /> Example:<br /><br /> -   "This computer will be restarted; please save your work."|  
|SMSRebootTimeout<br /><br /> (input)|Specifies the number of seconds that the warning is displayed to the user before the computer restarts. Specify zero seconds to indicate that no reboot message is displayed.<br /><br /> Examples:<br /><br /> **"0"** (default)<br /><br /> **"5"**<br /><br /> **"10"**|  

###  <a name="BKMK_RestoreUserState"></a> Restore User State Task Sequence Action Variables  
 The variables for this action specify information used to restore the user state of the destination computer, such as pathname of the folder from which the user state is restored and whether the local computer account is restored. For more information about the task sequence step associated with these variables, see [Restore User State](task-sequence-steps.md#BKMK_RestoreUserState).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (input)|The UNC or local pathname of the folder from which the user state is restored.|  
|OSDMigrateContinueOnRestore<br /><br /> (input)|Specifies that the user state restoration continues even if some files cannot be restored.<br /><br /> Valid values:<br /><br /> **"true"** (default)<br /><br /> **"false"**|  
|OSDMigrateEnableVerboseLogging<br /><br /> (input)|Enables verbose logging for the USMT tool. This value is required by the action; it must be set to "true" or "false".<br /><br /> Valid values:<br /><br /> **"true"**<br /><br /> **"false"** (default)|  
|OSDMigrateLocalAccounts<br /><br /> (input)|Specifies whether the local computer account is restored.<br /><br /> Valid values:<br /><br /> **"true"**<br /><br /> **"false"** (default)|  
|OSDMigrateLocalAccountPassword<br /><br /> (input)|If the **OSDMigrateLocalAccounts** variable is "true," this variable must contain the password that is assigned to all local accounts that are migrated. Because the same password is assigned to all migrated local accounts, it is   considered a temporary password that will be changed later by some method other than Configuration Manager operating system deployment.|  
|OSDMigrateAdditionalRestoreOptions<br /><br /> (input)|Specifies additional user state migration tool (USMT) command line options that are used when restoring the user state. The additional options are specified in the form of a string that is appended to the automatically generated USMT command line. The USMT options specified with this task sequence variable are not validated for accuracy prior to running the task sequence.|  
|_OSDMigrateUsmtRestorePackageID<br /><br /> (input)|Specifies the package ID of the Configuration Manager package that contains the USMT files. This variable is required.|  

###  <a name="BKMK_RunCommand"></a> Run Command Line Task Sequence Action Variables  
 The variables for this action specify information used to run a command from the command line, such as the working directory where the command is run. For more information about the task sequence step associated with these variables, see [Run Command Line](task-sequence-steps.md#BKMK_RunCommandLine).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|SMSTSDisableWow64Redirection<br /><br /> (input)|By default, when running on a 64-bit operating system, the program in the command line is located and run using the WOW64 file system redirector so that 32-bit versions of operating system programs and DLLs are found. Setting this variable to "true" disables the use of the WOW64 file system redirector so that native 64-bit versions of operating system programs and DLLs can be found. This variable has no effect when running on a 32-bit operating system.|  
|WorkingDirectory<br /><br /> (input)|Specifies the starting directory for a command-line action. The specified directory name must not exceed 255 characters.<br /><br /> Examples:<br /><br /> -   **"C:\\"**<br />-   **"%SystemRoot%"**|  
|SMSTSRunCommandLineUserName<br /><br /> (input)|Specifies the account by which the command line is run. The value is a string of the form username or domain\username.|  
|SMSTSRunCommandLinePassword<br /><br /> (input)|Specifies the password for the account specified by the SMSTSRunCommandLineUserName variable.|  

### Set Dynamic Variables  
 The variables for this action are automatically set when you add the Set Dynamic Variables task sequence step. For more information about the task sequence step associated with these variables, see [Set Dynamic Variables](task-sequence-steps.md#BKMK_SetDynamicVariables).  

#### Details  

|Action Variable Name<br /><br /> (input)|Description|  
|----------------------------------------|-----------------|  
|_SMSTSMake|Specifies the make of the computer.|  
|_SMSTSModel|Specifies the model of the computer.|  
|_SMSTSMacAddresses|Specifies the MAC addresses used by the computer.|  
|_SMSTSIPAddresses|Specifies the IP addresses used by the computer.|  
|_SMSTSSerialNumber|Specifies the serial number of the computer.|  
|_SMSTSAssetTag|Specifies the asset tag for the computer.|  
|_SMSTSUUID|Specifies the UUID of the computer.|  
|_SMSTSDefaultGateways|Specifies the default gateways used by the computer.|  

###  <a name="BKMK_SetupWindows"></a> Setup Windows and ConfigMgr Task Sequence Action Variables  
 The variable for this action specifies the client installation properties that are used when installing the Configuration Manager client. For more information about the task sequence step associated with these variables, see [Setup Windows and ConfigMgr](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).  

#### Details  

|Action Variable Name<br /><br /> (input)|Description|  
|----------------------------------------|-----------------|  
|SMSClientInstallProperties<br /><br /> (input)|Specifies the client installation properties that are used when installing the Configuration Manager client.|  

### Upgrade Operating System  
 The variable for this action specifies additional command-line options that are not available in the Configuration Manager console are added to Setup for a Windows 10 upgrade. For more information about the task sequence step associated with this variable, see [Upgrade Operating System](task-sequence-steps.md#BKMK_UpgradeOS).  

#### Details  

|Action Variable Name<br /><br /> (input)|Description|  
|----------------------------------------|-----------------|  
|OSDSetupAdditionalUpgradeOptions<br /><br /> (input)|Specifies the additional command-line options that are added to Setup during a Windows 10 upgrade. The command-line options are not verified. Therefore, check that the option you enter is accurate.<br /><br /> For more information, see [Windows Setup Command-Line Options](https://msdn.microsoft.com/library/windows/hardware/dn938368\(v=vs.85\).aspx).|  
