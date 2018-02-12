---
title: Task sequence action variables
titleSuffix: "Configuration Manager"
description: "Use sequence action variables, such as network setting variables, to specify configuration settings for a single step in a Configuration Manager task sequence."
ms.custom: na
ms.date: 02/09/2018
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
manager: dougeby

---
# Task sequence action variables in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Task sequence action variables specify configuration settings that are used by a single step in a System Center Configuration Manager task sequence. By default, the task sequence step initializes its settings before it runs. These settings are available only while the associated task sequence step runs. In other words, the task sequence adds the action variable value to the task sequence environment before the task sequence step is run. The task sequence removes the value from the environment after the step runs.  

## Action Variable Example  
 For example, you can specify a start-in directory for a command-line action by using the **Run Command Line** task sequence step. This step includes a **Start In** property whose default value is stored in the task sequence environment as the **WorkingDirectory** variable. The **WorkingDirectory** environment variable is initialized before the **Run Command Line** task sequence action is run. During the **Run Command Line** step, the **WorkingDirectory** value can be accessed through the **Start In** property. After the step completes, the task sequence removes the value of the **WorkingDirectory** variable from the environment. If the sequence contains another **Run Command Line** task sequence step, the task sequence initializes a new **WorkingDirectory** variable, and sets it to the starting value for the current step.  

 The *default* value for a task sequence action variable is present when the task sequence step runs. If you set a *new* value, it is available to multiple steps in the task sequence. If you use one of the task sequence variable creation methods to override a built-in variable value, the new value remains in the environment and overrides the default value for other steps in the task sequence. For example, if you add a **Set Task Sequence Variable** step as the first step of the task sequence, which sets the **WorkingDirectory** variable to **C:\\**, any **Run Command Line** step in the task sequence uses the new starting directory value.  

## Action Variables for Task Sequence Actions  
 Configuration Manager task sequence variables are grouped by their associated task sequence action. Use the following links to gather information about the action variables associated with a specific action. The task sequence variables govern how the task sequence action operates. The task sequence action reads and uses the variables that you mark as input variables. Alternatively, you can use the [Set Task Sequence Variable](task-sequence-steps.md#BKMK_SetTaskSequenceVariable) step or the TSEnvironment COM object to set the variables at runtime. Only the task sequence action marks variables as output variables. Actions that occur later in the task sequence read these output variables.  

> [!NOTE]  
>  Not all task sequence actions are associated with a set of task sequence variables. For example, although there are variables associated with the Enable BitLocker action, there are no variables associated with the Disable BitLocker action.  



###  <a name="BKMK_ApplyDataImage"></a> Apply Data Image   
 For more information, see [Apply Data Image](task-sequence-steps.md#BKMK_ApplyDataImage). 

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|OSDDataImageIndex<br /><br /> (input)|Specifies the index value of the image that is applied to the destination computer.|  
|OSDWipeDestinationPartition<br /><br /> (input)|Specifies whether to delete the files located on the destination partition.<br /><br /> Valid values:<br /><br /> **true** (default)<br /><br /> **false**|  



###  <a name="BKMK_ApplyDriverPackage"></a> Apply Driver Package   
For more information, see [Apply Driver Package](task-sequence-steps.md#BKMK_ApplyDriverPackage).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|OSDApplyDriverBootCriticalContentUniqueID<br /><br /> (input)|Specifies the content ID of the mass storage device driver to install from the driver package. If this variable is not specified, no mass storage driver is installed.|  
|OSDApplyDriverBootCriticalINFFile<br /><br /> (input)|Specifies the INF file of the mass storage driver to install.<br /><br /> <br /><br /> This task sequence variable is required if the OSDApplyDriverBootCriticalContentUniqueID is set.|  
|OSDApplyDriverBootCriticalHardwareComponent<br /><br /> (input)|Specifies whether a mass storage device driver is installed, this variable must be **scsi**.<br /><br /> This task sequence variable is required if the OSDApplyDriverBootCriticalContentUniqueID is set.|  
|OSDApplyDriverBootCriticalID<br /><br /> (input)|Specifies the boot critical ID of the mass storage device driver to install. This ID is listed in the **scsi** section of the device driver's txtsetup.oem file.<br /><br /> This task sequence variable is required if the OSDApplyDriverBootCriticalContentUniqueID is set.|  
|OSDAllowUnsignedDriver<br /><br /> (input)|Specifies whether to configure Windows to allow the installation of unsigned device drivers. This task sequence variable is not used when deploying the Windows Vista and later operating system.<br /><br /> Valid values:<br /><br /> **true**<br /><br /> **false** (default)|  



###  <a name="BKMK_ApplyNetworkSettings"></a> Apply Network Settings   
 For more information, see [Apply Network Settings](task-sequence-steps.md#BKMK_ApplyNetworkSettings).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|OSDAdapter<br /><br /> (input)|This task sequence variable is an array variable. Each element in the array represents the settings for a single network adapter on the computer. Access the settings for each adapter by combining the array variable name with the zero-based network adapter index and the property name.<br /><br />If this step configures multiple network adapters, it defines the properties for the second network adapter by using the index in the variable name. For example, OSDAdapter1EnableDHCP, OSDAdapter1IPAddressList, OSDAdapter1DNSDomain, OSDAdapter1WINSServerList, and OSDAdapter1EnableWINS.<br /><br />For example, use the following variable names to define the properties of the first network adapter for this task sequence step to configure:<br /><br /> <ul><li>**OSDAdapter0EnableDHCP**: **true** enables Dynamic Host Configuration Protocol (DHCP) for the adapter.<br />    This setting is required. Possible values are: **True** or **False**.</li><li>**OSDAdapter0IPAddressList**: Comma-delimited list of IP addresses for the adapter. This property is ignored unless **EnableDHCP** is set to **false**.<br />    This setting is required.</li><li>**OSDAdapter0SubnetMask**: Comma-delimited list of subnet masks. This property is ignored unless **EnableDHCP** is set to **false**.<br />    This setting is required.</li><li>**OSDAdapter0Gateways**: Comma-delimited list of IP gateway addresses. This property is ignored unless **EnableDHCP** is set to **false**.<br />    This setting is required.</li><li>**OSDAdapter0DNSDomain**: Domain Name System (DNS) domain for the adapter.</li><li>**OSDAdapter0DNSServerList**: Comma-delimited list of DNS servers for the adapter.<br />    This setting is required.</li><li>**OSDAdapter0EnableDNSRegistration**: **true** to register the IP address for the adapter in DNS.</li><li>**OSDAdapter0EnableFullDNSRegistration**: **true** to register the IP address for the adapter in DNS under the full DNS name for the computer.</li><li>**OSDAdapter0EnableIPProtocolFiltering**: **true** to enable IP protocol filtering on the adapter.</li><li>**OSDAdapter0IPProtocolFilterList**: Comma-delimited list of protocols allowed to run over IP. This property is ignored if **EnableIPProtocolFiltering** is set to **false**.</li><li>**OSDAdapter0EnableTCPFiltering**: **true** to enable TCP port filtering for the adapter.</li><li>**OSDAdapter0TCPFilterPortList**: Comma-delimited list of ports to be granted access permissions for TCP. This property is ignored if **EnableTCPFiltering** is set to **false**.</li><li>**OSDAdapter0TcpipNetbiosOptions**: Options for NetBIOS over TCP/IP. Possible values are as follows:<br /><br /> <ul><li>**0**: Use NetBIOS settings from DHCP server.</li><li>**1**: Enable NetBIOS over TCP/IP.</li><li>**2**: Disable NetBIOS over TCP/IP.</li></ul></li><li>**OSDAdapter0EnableWINS**: **true** to use WINS for name resolution.</li><li>**OSDAdapter0WINSServerList**: Comma-delimited list of WINS server IP addresses. This property is ignored unless **EnableWINS** is set to **true**.</li><li>**OSDAdapter0MacAddress**: MAC address used to match settings to physical network adapter.</li><li>**OSDAdapter0Name**: Name of the network connection as it appears in the network connections control panel program. The name is between 0 and 255 characters in length.</li><li>**OSDAdapter0Index**: Index of the network adapter settings in the array of settings.<br /><br />     OSDAdapterCount=1<br />    OSDAdapter0EnableDHCP=FALSE<br />    OSDAdapter0IPAddressList=192.168.0.40<br />    OSDAdapter0SubnetMask=255.255.255.0<br />    OSDAdapter0Gateways=192.168.0.1<br />    OSDAdapter0DNSSuffix=contoso.com</li></ul>|  
|OSDAdapterCount<br /><br /> (input)|Specifies the number of network adapters installed on the destination computer. When the **OSDAdapterCount** value is set, all the configuration options for each adapter must be set. For example, if you set the **OSDAdapterTCPIPNetbiosOptions** value for a specific adapter then all the values for that adapter must also be configured.<br /><br />If this value is not specified, all **OSDAdapter** values are ignored.|  
|OSDDNSDomain<br /><br /> (input)|Specifies the primary DNS server that is used by the destination computer.|  
|OSDDomainName<br /><br /> (input)|Specifies the name of the Windows domain that the destination computer joins. The specified value must be a valid Active Directory Domain Services domain name.|  
|OSDDomainOUName<br /><br /> (input)|Specifies the RFC 1779 format name of the organizational unit (OU) that the destination computer joins. If specified, the value must contain the full path.<br /><br /> Example:<br /><br /> **LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com**|  
|OSDEnableTCPIPFiltering<br /><br /> (input)|Specifies whether TCP/IP filtering is enabled.<br /><br /> Valid values:<br /><br /> **true**<br /><br /> **false** (default)|  
|OSDJoinAccount<br /><br /> (input)|Specifies the network account that is used to add the destination computer to a Windows domain.|  
|OSDJoinPassword<br /><br /> (input)|Specifies the network password that is used to add the destination computer to a Windows domain.|  
|OSDNetworkJoinType<br /><br /> (input)|Specifies whether the destination computer joins a Windows domain or a workgroup.<br /><br /> **0** indicates that the destination computer joins a Windows domain. **1** specifies that the computer joins a workgroup.<br /><br /> Valid values:<br /><br /> **0**<br /><br /> **1**|  
|OSDDNSSuffixSearchOrder<br /><br /> (input)|Specifies the DNS search order for the destination computer.|  
|OSDWorkgroupName<br /><br /> (input)|Specifies the name of the workgroup that the destination computer joins.<br /><br /> Specify either this value or the **OSDDomainName** value. The workgroup name can be a maximum of 32 characters.<br /><br /> Example:<br /><br /> **Accounting**|  



###  <a name="BKMK_ApplyOperatingSystem"></a> Apply Operating System Image   
 For more information, see [Apply Operating System Image](task-sequence-steps.md#BKMK_ApplyOperatingSystemImage).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|OSDConfigFileName<br /><br /> (input)|Specifies the file name of the operating system deployment answer file associated with the operating system deployment package.|  
|OSDImageIndex<br /><br /> (input)|Specifies the image index value of the WIM file that is applied to the destination computer.|  
|OSDInstallEditionIndex<br /><br /> (input)|Specifies the version of Windows Vista or later operating system that is installed. If no version is specified, Windows Setup determines which version to install using the referenced product key.<br /><br /> Use only a value of zero (0) if the following conditions are true:<br /><br /> -   You are installing a pre-Windows Vista operating system<br />-   You are installing a volume license edition of Windows Vista or later, and no product key is specified.<br /><br /> Valid values:<br /><br /> **0** (default)|  
|OSDTargetSystemDrive (output)|Specifies the drive letter of the partition that contains the operating system files.|  



###  <a name="BKMK_ApplyWindowsSettings"></a> Apply Windows Settings   
 For more information, see [Apply Windows Settings](task-sequence-steps.md#BKMK_ApplyWindowsSettings).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|OSDComputerName<br /><br /> (input)|Specifies the name of the destination computer.<br /><br /> Example:<br /><br /> **%_SMSTSMachineName%** (default)|  
|OSDProductKey<br /><br /> (input)|Specifies the Windows product key. The specified value must be between 1 and 255 characters.|  
|OSDRegisteredUserName<br /><br /> (input)|Specifies the default registered user name in the new operating system. The specified value must be between 1 and 255 characters.|  
|OSDRegisteredOrgName<br /><br /> (input)|Specifies the default registered organization name in the new operating system. The specified value must be between 1 and 255 characters.|  
|OSDTimeZone<br /><br /> (input)|Specifies the default time zone setting that is used in the new operating system.|  
|OSDServerLicenseMode<br /><br /> (input)|Specifies the Windows Server license mode that is used.<br /><br /> Valid values:<br /><br /> **PerSeat**<br /><br /> **PerServer**|  
|OSDServerLicenseConnectionLimit<br /><br /> (input)|Specifies the maximum number of connections allowed. The specified number must be in the range between 5 and 9999 connections.|  
|OSDRandomAdminPassword<br /><br /> (input)|Specifies a randomly generated password for the administrator account in the new operating system. If set to **true**, Windows Setup disables the local administrator account on the target computer. If set to **false**, Windows Setup enables the local administrator account on the target computer, and sets the account password to the value of **OSDLocalAdminPassword**.<br /><br /> Valid values:<br /><br /> **true** (default)<br /><br /> **false**|  
|OSDLocalAdminPassword<br /><br /> (input)|Specifies the local administrator password. If you enable **Randomly generate the local administrator password and disable the account on all supported platforms**, then the step ignores this variable. The specified value must be between 1 and 255 characters.|  



###  <a name="BKMK_AutoApplyDrivers"></a> Auto Apply Drivers   
 For more information, see [Auto Apply Drivers](task-sequence-steps.md#BKMK_AutoApplyDrivers).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|OSDAutoApplyDriverCategoryList<br /><br /> (input)|A comma-delimited list of the driver catalog category unique IDs. The **Auto Apply Driver** step only considers the drivers in at least one of the specified categories. This value is optional, and it is not set by default. Obtain the available category IDs by enumerating the list of **SMS_CategoryInstance** objects on the site.|  
|OSDAllowUnsignedDriver<br /><br /> (input)|Specifies whether Windows is configured to allow unsigned device drivers to be installed. This task sequence variable is not used when deploying Windows Vista and later operating systems.<br /><br /> Valid values:<br /><br /> **true**<br /><br /> **false** (default)|  
|OSDAutoApplyDriverBestMatch<br /><br /> (input)|If there are multiple device drivers in the driver catalog that are compatible with a hardware device, this variable determines the step's action. If set to **true**, the step only installs the best device driver. If **false**, the step installs all compatible device drivers, and Windows chooses the best driver to use.<br /><br /> Valid values:<br /><br /> **true** (default)<br /><br /> **false**|  
|SMSTSDriverRequestConnectTimeOut|When requesting the driver catalog, this variable is the number of seconds the task sequence waits for the HTTP server connection. If the connection takes longer than the timeout setting, the task sequence cancels the request. By default, the timeout is set to **60** seconds.|  
|SMSTSDriverRequestReceiveTimeOut|When requesting the driver catalog, this variable is the number of seconds the task sequence waits for a response. If the connection takes longer than the timeout setting, the task sequence cancels the request. By default, the timeout is set to **480** seconds.|
|SMSTSDriverRequestResolveTimeOut|When requesting the driver catalog, this variable is the number of seconds the task sequence waits for HTTP name resolution. If the connection takes longer than the timeout setting, the task sequence cancels the request. By default, the timeout is set to **60** seconds.|
|SMSTSDriverRequestSendTimeOut|When sending a request for the driver catalog, this variable is the number of seconds the task sequence waits to send the request. If the request takes longer than the timeout setting, the task sequence cancels the request. By default, the timeout is set to **60** seconds.|



###  <a name="BKMK_CaptureNetworkSettings"></a> Capture Network Settings   
 For more information, see [Capture Network Settings](task-sequence-steps.md#BKMK_CaptureNetworkSettings).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|OSDMigrateAdapterSettings<br /><br /> (input)|Specifies whether the network adapter settings (TCP/IP, DNS, and WINS) configuration information is captured.<br /><br /> Examples:<br /><br /> **true** (default)<br /><br /> **false**|  
|OSDMigrateNetworkMembership<br /><br /> (input)|Specifies whether the workgroup or domain membership information is migrated as part of the operating system deployment.<br /><br /> Examples:<br /><br /> **true** (default)<br /><br /> **false**|  



###  <a name="BKMK_CaptureOperatingSystemImage"></a> Capture Operating System Image   
 For more information, see [Capture Operating System Image](task-sequence-steps.md#BKMK_CaptureOperatingSystemImage).  

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



###  <a name="BKMK_CaptureUserState"></a> Capture User State   
 For more information, see [Capture User State](task-sequence-steps.md#BKMK_CaptureUserState).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (input)|The UNC or local path name of the folder where the user state is saved. No default.|  
|OSDMigrateAdditionalCaptureOptions<br /><br /> (input)|Additional user state migration tool (USMT) command-line options that the task sequence uses to capture user state. The step does not expose these settings in the task sequence editor. Specify these options as a string, which the task sequence appends to the automatically generated USMT command line.<br /><br />The USMT options specified with this task sequence variable are not validated for accuracy prior to running the task sequence.|  
|OSDMigrateMode<br /><br /> (input)|Allows you to customize the files that are captured by USMT. If this variable is set to **Simple**, then the task sequence only uses the standard USMT configuration files. If this variable is set to **Advanced**, then the task sequence variable OSDMigrateConfigFiles specifies the configuration files that USMT uses.<br /><br /> Valid values:<br /><br /> **Simple**<br /><br /> **Advanced**|  
|OSDMigrateConfigFiles<br /><br /> (input)|Specifies the configuration files used to control the capture of user profiles. This variable is used only if OSDMigrateMode is set to Advanced. This comma-delimited list value is set to perform customized user profile migration.<br /><br /> Example: miguser.xml,migsys.xml,migapps.xml|  
|OSDMigrateContinueOnLockedFiles<br /><br /> (input)|If USMT cannot capture some files, this variable allows the user state capture to proceed.<br /><br /> Valid values:<br /><br /> **true** (default)<br /><br /> **false**|  
|OSDMigrateEnableVerboseLogging<br /><br /> (input)|Enables verbose logging for USMT.<br /><br /> Valid values:<br /><br /> **true**<br /><br /> **false** (default)|  
|OSDMigrateSkipEncryptedFiles<br /><br /> (input)|Specifies whether encrypted files are captured.<br /><br /> Valid values:<br /><br /> **true**<br /><br /> **false** (default)|  
|_OSDMigrateUsmtPackageID<br /><br /> (input)|Specifies the package ID of the Configuration Manager package that contains the USMT files. This variable is required.|  



###  <a name="BKMK_CaptureWindowsSettings"></a> Capture Windows Settings   
 For more information, see [Capture Windows Settings](task-sequence-steps.md#BKMK_CaptureWindowsSettings).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|OSDMigrateComputerName<br /><br /> (input)|Specifies whether the computer name is migrated.<br /><br /> Valid values:<br /><br /> **true** (default)<br /><br /> **false**<br /><br /> If the value is **true**, then the OSDComputerName variable is set to the NetBIOS name of the computer.|  
|OSDComputerName<br /><br /> (output)|Set to the NetBIOS name of the computer. The value is set only if the OSDMigrateComputerName variable is set to **true**.|  
|OSDMigrateRegistrationInfo<br /><br /> (input)|Specifies whether the step migrates user and organization information.<br /><br /> Valid values:<br /><br /> **true** (default)<br /><br /> **false**<br /><br /> If the value is **true**, then the OSDRegisteredOrgName variable is set to the registered organization name of the computer.|  
|OSDRegisteredOrgName<br /><br /> (output)|Set to the registered organization name of the computer. The value is set only if the OSDMigrateRegistrationInfo variable is set to **true**.|  
|OSDMigrateTimeZone<br /><br /> (input)|Specifies whether the computer time zone is migrated.<br /><br /> Valid values:<br /><br /> **true** (default)<br /><br /> **false**<br /><br /> If the value is **true**, then the variable OSDTimeZone is set to the time zone of the computer.|  
|OSDTimeZone<br /><br /> (output)|Set to the time zone of the computer. The value is set only if the OSDMigrateTimeZone variable is set to **true**.|  



###  <a name="BKMK_ConnecttoNetworkFolder"></a> Connect to Network Folder   
 For more information, see [Connect To Network Folder](task-sequence-steps.md#BKMK_ConnectToNetworkFolder).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|SMSConnectNetworkFolderAccount<br /><br /> (input)|Specifies the administrator account that is used to connect to the network share.|  
|SMSConnectNetworkFolderDriveLetter<br /><br /> (input)|Specifies the network drive letter to connect to. This value is optional; if it is not specified, then the network connection is not mapped to a drive letter. If this value is specified, the value must be in the range from D: to Z:. In addition, do not use X: as it is the drive letter used by Windows PE during the Windows PE phase.<br /><br /> Examples:<br /><br /> **D:**<br /><br /> **E:**|  
|SMSConnectNetworkFolderPassword<br /><br /> (input)|Specifies the network password that is used to connect to the network share.|  
|SMSConnectNetworkFolderPath<br /><br /> (input)|Specifies the network path for the connection.<br /><br /> Example:<br /><br /> **\\\servername\sharename**|  



###  <a name="BKMK_EnableBitLocker"></a> Enable BitLocker   
 For more information, see [Enable BitLocker](task-sequence-steps.md#BKMK_EnableBitLocker).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|OSDBitLockerRecoveryPassword<br /><br /> (input)|Instead of generating a random recovery password, the **Enable BitLocker** task sequence action uses the specified value as the recovery password. The value must be a valid numerical BitLocker recovery password.|  
|OSDBitLockerStartupKey<br /><br /> (input)|Instead of generating a random startup key for the key management option **Startup Key on USB only,** the **Enable BitLocker** step uses the Trusted Platform Module (TPM) as the startup key. The value must be a valid, 256-bit Base64-encoded BitLocker startup key.|  



###  <a name="BKMK_FormatPartitionDisk"></a> Format and Partition Disk   
 For more information, see [Format and Partition Disk](task-sequence-steps.md#BKMK_FormatandPartitionDisk).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|OSDDiskIndex<br /><br /> (input)|Specifies the physical disk number to be partitioned.|  
|OSDDiskpartBiosCompatibilityMode<br /><br /> (input)|When partitioning the hard disk for compatibility with certain types of BIOS, this variable specifies whether to disable cache alignment optimizations. This is necessary when deploying Windows XP or Windows Server 2003 operating systems. For more information, see [article 931760](http://go.microsoft.com/fwlink/?LinkId=134081) and [article 931761](http://go.microsoft.com/fwlink/?LinkId=134082) in the Microsoft Knowledge Base.<br /><br /> Valid values:<br /><br /> **true**<br /><br /> **false** (default)| 
|OSDGPTBootDisk<br /><br /> (input)|Specifies whether to create an EFI partition on a GPT hard disk. EFI-based computers use this partition as the startup disk.<br /><br /> Valid values:<br /><br /> **true**<br /><br /> **false** (default)|  
|OSDPartitions<br /><br /> (input)|Specifies an array of partition settings; see the SDK topic for accessing array variables in the task sequence environment.<br /><br /> This task sequence variable is an array variable. Each element in the array represents the settings for a single partition on the hard disk. Access the settings defined for each partition by combining the array variable name with the zero-based disk partition number and the property name.<br /><br /> For example, use the following variable names to define the properties for the first partition that this step creates on the hard disk:<br /><br /> - **OSDPartitions0Type**: Specifies the type of partition. This property is required. Valid values are **Primary**, **Extended**, **Logical**, and **Hidden**.<br />-   **OSDPartitions0FileSystem**: Specifies the type of file system to use when formatting the partition. This property is optional. If you do not specify a file system, the step does not format the partition. Valid values are **FAT32** and **NTFS**.<br />-   **OSDPartitions0Bootable**: Specifies whether the partition is bootable. This property is required. If this value is set to **TRUE** for MBR disks, then the step marks this partition as active.<br />-   **OSDPartitions0QuickFormat**: Specifies the type of format that is used. This property is required. If this value is set to **TRUE**, the step performs a quick format. Otherwise, the step performs a full format.<br />-   **OSDPartitions0VolumeName**: Specifies the name that is assigned to the volume when it is formatted. This property is optional.<br />-   **OSDPartitions0Size**: Specifies the size of the partition. Units are specified by the **OSDPartitions0SizeUnits** variable. This property is optional. If this property is not specified, the partition is created using all remaining free space.<br />-   **OSDPartitions0SizeUnits**: The step uses these units to interpret the **OSDPartitions0Size** variable. This property is optional. Valid values are **MB** (default), **GB**, and **Percent**.<br />-   **OSDPartitions0VolumeLetterVariable**: When this step creates partitions, it always uses the next available drive letter in Windows PE. Use this optional property to specify the name of another task sequence variable. The step uses this variable to save the new drive letter for future reference.<br /><br />If you define multiple partitions with this task sequence action, the properties for the second partition are defined by using their index in the variable name. For example: **OSDPartitions1Type**, **OSDPartitions1FileSystem**, **OSDPartitions1Bootable**, **OSDPartitions1QuickFormat**, and **OSDPartitions1VolumeName**.|  
|OSDPartitionStyle<br /><br /> (input)|Specifies the partition style to use when partitioning the disk. **MBR** indicates the master boot record partition style, and **GPT** indicates the GUID Partition Table style.<br /><br /> Valid Values:<br /><br /> **GPT**<br /><br /> **MBR**|  



###  <a name="BKMK_InstallApplication"></a> Install Application   
 For more information, see [Install Application](task-sequence-steps.md#BKMK_InstallApplication).  

#### Details  

|Action Variable Name<br /><br /> (input)|Description|  
|----------------------------------------|-----------------|  
| TSErrorOnWarning |Specify whether the task sequence engine considers a detected warning as an error during this step. The task sequence sets the _TSAppInstallStatus variable to **Warning** when one or more applications, or a required dependency, did not install because it did not meet a requirement. When you set this variable to **True**, and the task sequence sets _TSAppInstallStatus to Warning, the outcome is an error. A value of **False** is the default behavior.| 
|SMSTSMPListRequestTimeoutEnabled|Use this variable to enable repeated MPList requests to refresh the client if the client is not on the intranet. <br />By default, this variable is set to **True**. When clients are on the internet, you can set this variable to **False** to avoid unnecessary delays. This variable is applicable only to the Install Application and Install Software Updates  task sequence steps.|  
|SMSTSMPListRequestTimeout|Specify how many milliseconds a task sequence waits before it retries to install an application after it fails to retrieve the management point list from location services. By default, the task sequence waits **60000** milliseconds (60 seconds) before it retries the step, and retries up to three times.|  



###  <a name="BKMK_InstallSoftwareUpdates"></a> Install Software Updates   
For more information, see [Install Software Updates](task-sequence-steps.md#BKMK_InstallSoftwareUpdates).  

#### Details  

|Action Variable Name<br /><br /> (input)|Description|  
|----------------------------------------|-----------------|  
|SMSInstallUpdateTarget<br /><br /> (input)|Specifies whether to install all updates or only mandatory updates.<br /><br /> Valid values:<br /><br /> **All**<br /><br /> **Mandatory**|  
|SMSTSSoftwareUpdateScanTimeout| Control the timeout for the software updates scan during this step. For example, increase the value if you expect numerous updates during the scan. The default value is **1800** seconds (30 minutes). The variable value is set in seconds. |
|SMSTSWaitForSecondReboot|This optional task sequence variable controls client behavior when a software update installation requires two restarts. Set this variable before this step to prevent a task sequence from failing because of a second restart from software update installation.<br /><br /> Set the SMSTSWaitForSecondReboot value in seconds to specify how long the task sequence pauses on this step while the computer restarts. Allow sufficient time in case there is a second restart. <br />For example, if you set SMSTSWaitForSecondReboot to 600, the task sequence pauses for 10 minutes after a restart before additional steps run. This variable is useful when a single Install Software Updates task sequence step installs hundreds of software updates.| 
|SMSTSMPListRequestTimeoutEnabled|Use this variable to enable repeated MPList requests to refresh the client if the client is not on the intranet. <br />By default, this variable is set to **True**. When clients are on the internet, you can set this variable to **False** to avoid unnecessary delays. This variable is applicable only to the Install Application and Install Software Updates  task sequence steps.|  
|SMSTSMPListRequestTimeout|Specify how many milliseconds a task sequence waits before it retries to install a software update after it fails to retrieve the management point list from location services. By default, the task sequence waits **60000** milliseconds (60 seconds) before it retries the step, and retries up to three times.|  



###  <a name="BKMK_JoinDomainWorkgroup"></a> Join Domain or Workgroup   
 For more information, see [Join Domain or Workgroup](task-sequence-steps.md#BKMK_JoinDomainorWorkgroup).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|OSDJoinAccount<br /><br /> (input)|Specifies the account that is used by the destination computer to join the Active Directory domain. This variable is required when joining a domain.|  
|OSDJoinDomainName<br /><br /> (input)|Specifies the name of an Active Directory domain the destination computer joins. The length of the domain name must be between 1 and 255 characters.|  
|OSDJoinDomainOUName<br /><br /> (input)|Specifies the RFC 1779 format name of the organizational unit (OU) that the destination computer joins. If specified, the value must contain the full path. The length of the OU name must be between 0 and 32,767 characters. This value is not set if the **OSDJoinType** variable is set to **1** (join workgroup).<br /><br /> Example:<br /><br /> **LDAP://OU=MyOu,DC=MyDom,DC=MyCompany,DC=com**|  
|OSDJoinPassword<br /><br /> (input)|Specifies the network password that the destination computer uses to join the Active Directory domain. If the task sequence environment does not include this variable, then Windows Setup tries a blank password. If the variable **OSDJoinType** variable is set to **0** (join domain), this value is required.|  
|OSDJoinSkipReboot<br /><br /> (input)|Specifies whether to skip restarting after the destination computer joins the domain or workgroup.<br /><br /> Valid values:<br /><br /> **true**<br /><br /> **false**|  
|OSDJoinType<br /><br /> (input)|Specifies whether the destination computer joins a Windows domain or a workgroup. To join the destination computer to a Windows domain, specify **0**. To join the destination computer to a workgroup, specify **1**.<br /><br /> Valid values:<br /><br /> **0**<br /><br /> **1**|  
|OSDJoinWorkgroupName<br /><br /> (input)|Specifies the name of a workgroup that the destination computer joins. The length of the workgroup name must be between 1 and 32 characters.<br /><br /> Example:<br /><br /> **Accounting**|  



###  <a name="BKMK_PrepareWindowsCapture"></a> Prepare Windows for Capture   
 For more information, see [Prepare Windows for Capture](task-sequence-steps.md#BKMK_PrepareWindowsforCapture).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|OSDBuildStorageDriverList<br /><br /> (input)|Specifies whether Sysprep builds a mass storage device driver list. This setting applies to only Windows XP and Windows Server 2003. This variable populates the [SysprepMassStorage] section of sysprep.inf with information on all the mass storage drivers that are supported by the image to be captured.<br /><br /> Valid values:<br /><br /> **true**<br /><br /> **false** (default)|  
|OSDKeepActivation<br /><br /> (input)|Specifies whether sysprep resets the product activation flag.<br /><br /> Valid values:<br /><br /> **true**<br /><br /> **false** (default)|  
|OSDTargetSystemRoot<br /><br /> (output)|Specifies the path to the Windows directory of the installed operating system on the reference computer. This operating system is verified as being a supported operating system for capture by Configuration Manager.|  



###  <a name="BKMK_ReleaseStateStore"></a> Release State Store   
 For more information, see [Release State Store](task-sequence-steps.md#BKMK_ReleaseStateStore).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (input)|The UNC or local pathname to the location from which the user state is restored. This value is used by both the **Capture User State** task sequence action and the **Restore User State** task sequence action.|  



###  <a name="BKMK_RequestState"></a> Request State Store   
  For more information, see [Release State Store](task-sequence-steps.md#BKMK_ReleaseStateStore).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|OSDStateFallbackToNAA<br /><br /> (input)|When the computer account fails to connect to the state migration point, this variable specifies whether the task sequence falls back to use the network access account (NAA).<br /><br /> Valid values:<br /><br /> **true**<br /><br /> **false** (default)|  
|OSDStateSMPRetryCount<br /><br /> (input)|Specifies the number of times that the task sequence step tries to find a state migration point before the step fails. The specified count must be between 0 and 600.|  
|OSDStateSMPRetryTime<br /><br /> (input)|Specifies the number of seconds that the task sequence step waits between retry attempts. The number of seconds can be a maximum of 30 characters.|  
|OSDStateStorePath<br /><br /> (output)|The UNC path to the folder on the state migration point where the user state is stored.|  



###  <a name="BKMK_RestartComputer"></a> Restart Computer   
 For more information, see [Restart Computer](task-sequence-steps.md#BKMK_RestartComputer).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|SMSRebootMessage<br /><br /> (input)|Specifies the message to be displayed to users before restarting the destination computer. If this variable is not set, the default message text is displayed. The specified message must not exceed 512 characters.<br /><br /> Example:<br /><br /> **Save your work before the computer restarts.**|  
|SMSRebootTimeout<br /><br /> (input)|Specifies the number of seconds that the warning is displayed to the user before the computer restarts. Specify zero seconds to indicate that no reboot message is displayed.<br /><br /> Examples:<br /><br /> **0** (default)<br /><br />  **60**|  



###  <a name="BKMK_RestoreUserState"></a> Restore User State   
  For more information, see [Restore User State](task-sequence-steps.md#BKMK_RestoreUserState).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|OSDStateStorePath<br /><br /> (input)|The UNC or local pathname of the folder from which the user state is restored.|  
|OSDMigrateContinueOnRestore<br /><br /> (input)|Continue the process, even if USMT cannot restore some files.<br /><br /> Valid values:<br /><br /> **true** (default)<br /><br /> **false**|  
|OSDMigrateEnableVerboseLogging<br /><br /> (input)|Enables verbose logging for the USMT tool. This value is required by the action.<br /><br /> Valid values:<br /><br /> **true**<br /><br /> **false** (default)|  
|OSDMigrateLocalAccounts<br /><br /> (input)|Specifies whether the local computer account is restored.<br /><br /> Valid values:<br /><br /> **true**<br /><br /> **false** (default)|  
|OSDMigrateLocalAccountPassword<br /><br /> (input)|If the **OSDMigrateLocalAccounts** variable is "true," this variable must contain the password assigned to all migrated local accounts. USMT assigns the same password to all migrated local accounts. Consider this password as temporary, and change it later by some other method.|  
|OSDMigrateAdditionalRestoreOptions<br /><br /> (input)|Specifies additional user state migration tool (USMT) command-line options that are used when restoring the user state. The additional options are specified in the form of a string that is appended to the automatically generated USMT command line. The USMT options specified with this task sequence variable are not validated for accuracy prior to running the task sequence.|  
|_OSDMigrateUsmtRestorePackageID<br /><br /> (input)|Specifies the package ID of the Configuration Manager package that contains the USMT files. This variable is required.|  



###  <a name="BKMK_RunCommand"></a> Run Command Line   
  For more information, see [Run Command Line](task-sequence-steps.md#BKMK_RunCommandLine).  

#### Details  

|Action Variable Name|Description|  
|--------------------------|-----------------|  
|SMSTSDisableWow64Redirection<br /><br /> (input)|By default on a 64-bit operating system, the task sequence locates and runs the program in the command line using the WOW64 file system redirector. This behavior allows the command to find 32-bit versions of operating system programs and DLLs. Setting this variable to **true** disables the use of the WOW64 file system redirector. The command finds native 64-bit versions of operating system programs and DLLs. This variable has no effect when running on a 32-bit operating system.|  
|WorkingDirectory<br /><br /> (input)|Specifies the starting directory for a command-line action. The specified directory name must not exceed 255 characters.<br /><br /> Examples:<br /><br /> -   **C:\\**<br />-   **%SystemRoot%**|  
|SMSTSRunCommandLineUserName<br /><br /> (input)|Specifies the account by which the command line is run. The value is a string of the form username or domain\username.|  
|SMSTSRunCommandLinePassword<br /><br /> (input)|Specifies the password for the account specified by the SMSTSRunCommandLineUserName variable.|  



### Set Dynamic Variables  
For more information, see [Set Dynamic Variables](task-sequence-steps.md#BKMK_SetDynamicVariables).  

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



###  <a name="BKMK_SetupWindows"></a> Setup Windows and ConfigMgr   
  For more information, see [Setup Windows and ConfigMgr](task-sequence-steps.md#BKMK_SetupWindowsandConfigMgr).  

#### Details  

|Action Variable Name<br /><br /> (input)|Description|  
|----------------------------------------|-----------------|  
|SMSClientInstallProperties<br /><br /> (input)|Specifies the client installation properties that are used when installing the Configuration Manager client.|  



### Upgrade Operating System  
 For more information, see [Upgrade Operating System](task-sequence-steps.md#BKMK_UpgradeOS).  

#### Details  

|Action Variable Name<br /><br /> (input)|Description|  
|----------------------------------------|-----------------|  
|OSDSetupAdditionalUpgradeOptions<br /><br /> (input)|Specifies the additional command-line options that are added to Windows Setup during a Windows 10 upgrade. The task sequence does not verify the command-line options.<br /><br /> For more information, see [Windows Setup Command-Line Options](/windows-hardware/manufacture/desktop/windows-setup-command-line-options).|  
