---
description: Learn how to represent a program or command to run when software is distributed to a client computer using SMS_Program class.
title: "SMS_Program Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: e4f5186a-6b63-4a06-80c9-45664b383edd
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# SMS_Program Server WMI Class
The `SMS_Program` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a program or command to run when software is distributed to a client computer.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_Program : SMS_BaseClass  
{  
     UInt32 ActionInProgress;  
     String ApplicationHierarchy;  
     String CommandLine;  
     String Comment;  
     String DependentProgram;  
     String Description;  
     UInt32 DeviceFlags;  
     String DiskSpaceReq;  
     String DriveLetter;  
     UInt32 Duration;  
     UInt8 ExtendedData[];  
     UInt32 ExtendedDataSize;  
     UInt8 Icon[];  
     UInt32 IconSize;  
     UInt8 ISVData[];  
     UInt32 ISVDataSize;  
     String ISVString;  
     String MSIFilePath  
     String MSIProductID  
     String PackageID;  
     String PackageName  
     UInt32 PackageType  
     String PackageVersion  
     UInt32 ProgramFlags;  
     String ProgramName;  
     String RemovalKey;  
     String Requirements;  
     UInt32 SecuredTypeID  
     SMS_OS_Details SupportedOperatingSystems[];  
     UInt32   TransformReadiness=0;   
     Datetime TransformAnalysisDate;   
     String   TransformDtID;   
     String WorkingDirectory;  
};  
```  

## Methods  
 The `SMS_Program` class does not define any methods.  

## Properties  
 `ActionInProgress`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read, enumeration]  

 Current action being performed on the package that is associated with the program by Configuration Manager. Possible values are:  

|Value|Description|  
|-----------|-----------------|  
|0|NONE|  
|1|UPDATE|  
|2|ADD|  
|3|DELETE|  

 Use this property in a WHERE clause to filter out programs that have been marked for deletion but have not yet been deleted. For more information, see the Remarks section later in this topic.  

 `ApplicationHierarchy`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The application hierarchy for the program. The default value is "".  

 `CommandLine`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The command line that runs when the program is started. The default value is "".  

 `Comment`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Comment that describes the program in the Configuration Manager console. The default value is "".  

 `DependentProgram`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 A formatted text string defining any program that should be run prior to running this program. The format is defined as \<PackageID>;;\<ProgramName>. If the program is in the same package, the calling application can simply specify ;;\<ProgramName>. The default value is "".  

 The dependency is maintained only for the first time that the program runs. After the program has run, the dependency is ignored. For example, you cannot create a recurring scheduled job for which the dependency is maintained for each program run.  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Not used.  

 `DeviceFlags`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Flags describing the device associated with the program. Possible values are:  

|Hexadecimal (Bit)|Description|  
|-------------------------|-----------------|  
|0x01000000 (24)|Always assign program to the client.|  
|0x02000000 (25)|Assign only if the device is currently connected to a high-bandwidth connection (default above 60 KBps).|  
|0x04000000 (26)|Assign only if the device is docked, that is, it is attached to a desktop that is using ActiveSync.|  

 `DiskSpaceReq`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Approximate disk space that the program requires. The format is "\<size> \<KB&#124;MB&#124;GB>". The default value is "".  

 This information is used in the Configuration Manager console and the advertisement to provide alerts about program disk space requirements. The user can then decide to accept the advertisement or perform some disk management task first.  

 `DriveLetter`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [SizeLimit("1"), Range("a-z")]  

 Drive letter (one character in the range a-z) that the program maps to and runs from. The default value is "".  

 `Duration`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The approximate duration, in minutes, of program execution on the client computer. Specify this value as a whole number greater than or equal to 0 (default) or as Unknown (not recommended). If the property is set to Unknown, Configuration Manager sets the maximum allowed run time as 720 minutes (12 hours). For additional information, see the Remarks section later in this topic.  

> [!NOTE]
>  On client computers, the specified value for published programs appears in `Run Advertised Programs` in Control Panel.  

 `ExtendedData`  
 Data type: `UInt8` Array  

 Access type: Read/Write  

 Qualifiers: [large, lazy]  

 The XML blob for image deployment.  

 `ExtendedDataSize`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 The extended data size, in bytes. The default value is 0.  

 `Icon`  
 Data type: `UInt8` Array  

 Access type: Read/Write  

 Qualifiers: [large]  

 Icon information associated with the program icon, as displayed in the Configuration Manager console.  

 `IconSize`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 Size, in bytes, of the program icon. Set this property to 0 to clear the icon.  

 `ISVData`  
 Data type: `UInt8` Array  

 Access type: Read/Write  

 Qualifiers: [large, lazy]  

 Information that allows a single ISV to store data relating to an `SMS_Program` object.  

 There are no restrictions or defined formats for the ISV data. However, it is important to not overwrite the property after the ISV ownership has been established. Your application should read the existing data in this property first. If the data does not belong to the application, it should not be modified. You should include an identifier in the data for the program so that ownership can be established easily.  

 `ISVDataSize`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 The size, in bytes, of the data stored in `ISVData`. The default value is 0.  

 `ISVString`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 String for partner extensibility.  

 `MSIFilePath`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The file path of the Windows Installer package with which the program is associated. The default value is "".  

 `MSIProductID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The product ID of the Windows Installer package with which the program is associated. The default value is "".  

 `PackageID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key, Not_null]  

 ID of an existing package with which to associate the program. For more information, see the Remarks section later in this topic.  

 `PackageName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [None]  

 The name of the package the program belongs to.  

 `PackageType`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [None]  

 The type of the package the program belongs to.  

|Value|Description|  
|-----------|-----------------|  
|0|Regular software distribution package.|  
|3|Driver package.|  
|4|Task sequence package.|  
|5|Software update package.|  
|6|Device setting package.|  
|257|Image package.|  
|258|Boot image package.|  
|259|Operating system install package.|  

 `PackageVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [None]  

 The version of the package the program belongs to.  

 `ProgramFlags`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [bits]  

 Flags identifying the installation characteristics of the program. Possible values are listed below. The default values are EVERYUSER, USEUNCPATH, USERCONTEXT, and UNATTENDED.  

> [!NOTE]
>  When using `SMS_Program` programmatically, ensure that no conflicting values are selected. For example, NOUSERLOGGEDIN and USERCONTEXT should not be used together.  

 Possible values are:  

|Hexadecimal (Bit)|Description|  
|-------------------------|-----------------|  
|0x00000001 (0)|AUTHORIZED_DYNAMIC_INSTALL. The program is authorized for dynamic install.|  
|0x00000002 (1)|USECUSTOMPROGRESSMSG. The task sequence shows a custom progress user interface message.|  
|0x00000010 (4)|DEFAULT_PROGRAM. This is a default program|  
|0x00000020 (5)|DISABLEMOMALERTONRUNNING. Disables MOM alerts while the program runs.|  
|0x00000040 (6)|MOMALERTONFAIL. Generates MOM alert if the program fails.|  
|0x00000080 (7)|RUN_DEPENDANT_ALWAYS. If set, this program's immediate dependent should always be run.|  
|0x00000100 (8)|WINDOWS_CE. Indicates a device program. If set, the program is not offered to desktop clients.|  
|0x00000200 (9)|This value is not used.|  
|0x00000400 (10)|COUNTDOWN. The countdown dialog is not displayed.|  
|0x00000800 (11)|FORCERERUN. This value is not used.|  
|0x00001000 (12)|DISABLED. The program is disabled.|  
|0x00002000 (13)|UNATTENDED. The program requires no user interaction.|  
|0x00004000 (14)|USERCONTEXT. The program can run only when a user is logged on.|  
|0x00008000 (15)|ADMINRIGHTS. The program must be run as the local Administrator account.|  
|0x00010000 (16)|EVERYUSER. The program must be run by every user for whom it is valid. Valid only for mandatory jobs.|  
|0x00020000 (17)|NOUSERLOGGEDIN. The program is run only when no user is logged on.|  
|0x00040000 (18)|OKTOQUIT. The program will restart the computer.|  
|0x00080000 (19)|OKTOREBOOT. Configuration Manager restarts the computer when the program has finished running successfully.|  
|0x00100000 (20)|USEUNCPATH. Use a UNC path (no drive letter) to access the distribution point.|  
|0x00200000 (21)|PERSISTCONNECTION. Persists the connection to the drive specified in the DriveLetter property. The USEUNCPATH bit flag must not be set.|  
|0x00400000 (22)|RUNMINIMIZED. Run the program as a minimized window.|  
|0x00800000 (23)|RUNMAXIMIZED. Run the program as a maximized window.|  
x01000000 (24)|HIDEWINDOW. Hide the program window.|  
|0x02000000 (25)|OKTOLOGOFF. Logoff user when program completes successfully.|  
|0x04000000 (26)|RUNACCOUNT. This value is not used.|  
|0x08000000 (27)|ANY_PLATFORM. Override check for platform support.|  
|0x10000000 (28)|STILL_RUNNING. This value is not used.|  
|0x20000000 (29)|SUPPORT_UNINSTALL. Run uninstall from the registry key when the advertisement expires.|  
|0x40000000 (30)|The platform is not supported.|  
|0x80000000 (31)|SHOW_IN_ARP. This value is not used.|  

 `ProgramName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key, Not_null]  

 Unique name that represents this program.  

 `RemovalKey`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Registry key that identifies the uninstall script for the program. The script must reside in the `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall` registry path. The default value is "".  

 `Requirements`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Description of any additional requirements of the program. The default value is "".  

 `SecuredTypeID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [None]  

 Secured type of related package.  

 `SupportedOperatingSystems`  
 Data type: `SMS_OS_Details` Array  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 [SMS_OS_Details Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_os_details-server-wmi-class.md) objects representing the operating systems on which the program can run.  

 If you do not specify ANY_PLATFORM in the `ProgramFlags` property, you must specify one or more supported operating systems. [SMS_SupportedPlatforms Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_supportedplatforms-server-wmi-class.md) defines the list of platforms that Configuration Manager supports.  

 `TransformAnalysisDate`  
 Data type: `DateTime`  

 Access type: Read/Write  

 Qualifiers: [None]  

 For internal use only.  

 `TransformDtID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [None]  

 For internal use only.  

 `TransformReadiness`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [None]  

 For internal use only.  

 `WorkingDirectory`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The location from which the program runs. The default value is "".  

 The working directory can be an absolute path on the client or a path relative to the distribution point folder that contains the package. If a working directory is not specified, Configuration Manager uses the default distribution point folder.  

## Remarks  
 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

 A program is always associated with a parent package and typically represents the installation program for the package. Note that more than one program can be associated with the same package. The application uses the `PackageID` property to make this association. Your application cannot change this property after the `SMS_Program` object is created. To associate the program with a different package, the application must delete the object and create a new object with a new `PackageID` value.  

 When your application deletes an `SMS_Program` object, it is not deleted until its related components, such as its advertisements, are deleted. Instead, Configuration Manager sets the `ActionInProgress` property to DELETE (3) to mark the program for deletion. To ensure that a query does not retrieve programs that have been marked for deletion, add this case to the WHERE clause.  

> [!IMPORTANT]
>  If you are using maintenance windows for the collection on which the program is run, a conflict can occur if the value of the `Duration` property is longer than the scheduled maintenance window. If this property is set to Unknown, the program starts during the maintenance window, but continues to run until it completes or fails after the maintenance window is closed.  

 It is recommended that you not set the `Duration` property to Unknown because this property is used for the following two important purposes:  

- To monitor the results of the program.  

- To determine if the program will be launched when maintenance windows have been defined on the client computers.  

  If your application sets the `Duration` property but program run time exceeds this duration, then Configuration Manager stops monitoring the program but does not terminate the program. This allows Configuration Manager to continue with other software distribution functions, such as running other advertised programs. The manager does not:  

- Stop the program.  

- Free any drives that have been mapped for the advertised program.  

- Free any network connections made for the advertised program.  

- Free operating system resources used by Configuration Manager when advertised programs are running.  

  For additional information, see [About Maintenance Windows](../../../../../develop/core/servers/configure/about-maintenance-windows.md).  

## Requirements  

### Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

### Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [SMS_Package Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md)   
 [How to Create a Package](../../../../../develop/core/servers/configure/how-to-create-a-package.md)   
 [How to Create a Program](../../../../../develop/core/servers/configure/how-to-create-a-program.md)
