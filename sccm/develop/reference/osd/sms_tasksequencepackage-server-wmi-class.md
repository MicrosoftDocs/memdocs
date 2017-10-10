---
title: "SMS_TaskSequencePackage Class"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: 753d2469-bb46-4bcd-bb3b-7078f4739531searchScope: - ConfigMgr SDK
caps.latest.revision: 27
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_TaskSequencePackage Server WMI Class
The `SMS_TaskSequencePackage` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a task sequence package that defines the steps to run for the task sequence.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TaskSequencePackage : SMS_PackageBaseclass  
{  
      UInt32 ActionInProgress;  
      String AlternateContentProviders;  
      String BootImageID;  
      String Category;  
      String CustomProgressMsg;  
      String DependentProgram;  
      String Description;  
      UInt32 Duration;  
      UInt8 ExtendedData[];  
      UInt32 ExtendedDataSize;  
      UInt32 ForcedDisconnectDelay;  
      Boolean ForcedDisconnectEnabled;  
      UInt32 ForcedDisconnectNumRetries;  
      UInt8 Icon[];  
      UInt32 IconSize;  
      Boolean IgnoreAddressSchedule;  
      UInt8 ISVData[];  
      UInt32 ISVDataSize;  
      String Language;  
      DateTime LastRefreshTime;  
      String LocalizedCategoryInstanceNames[];  
      String Manufacturer;  
      String MIFFilename;  
      String MIFName;  
      String MIFPublisher;  
      String MIFVersion;  
      String Name;  
      UInt32 NumOfPrograms;  
      String PackageID;  
      UInt32 PackageSize;  
      UInt32 PackageType;  
      UInt32 PkgFlags;  
      UInt32 PkgSourceFlag;  
      String PkgSourcePath;  
      String PreferredAddressType;  
      UInt32 Priority;  
      UInt32 ProgramFlags;  
      SMS_TaskSequence_Reference References[];  
      Boolean RefreshPkgSourceFlag;  
      SMS_ScheduleToken RefreshSchedule[];  
      String SecuredScopeNames[];  
      String SedoObjectVersion;  
      UInt32 ReferencesCount;  
      String Reserved;  
      String Sequence;  
      String ShareName;  
      UInt32 ShareType;  
      DateTime SourceDate;  
      String SourceSite;  
      UInt32 SourceVersion;  
      String StoredPkgPath;  
      UInt32 StoredPkgVersion;  
      SMS_OS_Details SupportedOperatingSystems[];  
      UInt32 TaskSequenceFlags;  
      UInt32 Type;  
      String Version;  
};  
```  

## Methods  
 The following table shows the methods in `SMS_TaskSequencePackage`.  

|Method|Description|  
|------------|-----------------|  
|[AddChangeNotification Method in Class SMS_TaskSequencePackage](../../../develop/reference/osd/addchangenotification-method-in-class-sms_tasksequencepackage.md)|Adds a task sequence package change notification.|  
|[AddDistributionPoints Method in Class SMS_TaskSequencePackage](../../../develop/reference/osd/adddistributionpoints-method-in-class-sms_tasksequencepackage.md)|Adds the distribution points for the task sequence package.|  
|[CheckReferencesShareType Method in Class SMS_TaskSequencePackage](../../../develop/reference/osd/checkreferencessharetype-method-in-class-sms_tasksequencepackage.md)|Checks all referred package for this task sequence and returns all that are not shared.|  
|[GetClientConfigPolicies Method in Class SMS_TaskSequencePackage](../../../develop/reference/osd/getclientconfigpolicies-method-in-class-sms_tasksequencepackage.md)|Gets all site-wide client configuration policies and their corresponding policy assignments.|  
|[GetContentHash Method in Class SMS_TaskSequencePackage](../../../develop/reference/osd/getcontenthash-method-in-class-sms_tasksequencepackage.md)|Gets the hash of specific System Center Configuration Manager content.|  
|[GetPackageDefaultHash Method in Class SMS_TaskSequencePackage](../../../develop/reference/osd/getpackagedefaulthash-method-in-class-sms_tasksequencepackage.md)|Gets the hash of a System Center Configuration Manager package.|  
|[GetPackageHash Method in Class SMS_TaskSequencePackage](../../../develop/reference/osd/getpackagehash-method-in-class-sms_tasksequencepackage.md)|Gets the certificate hash for the task sequence package.|  
|[GetSequence Method in Class SMS_TaskSequencePackage](../../../develop/reference/osd/getsequence-method-in-class-sms_tasksequencepackage.md)|Gets a task sequence from a task sequence package.|  
|[GetTsPolicies Method in Class SMS_TaskSequencePackage](../../../develop/reference/osd/gettspolicies-method-in-class-sms_tasksequencepackage.md)|Gets all policies associated with the specified task sequence.|  
|[GetTsPoliciesSaMedia Method in Class SMS_TaskSequencePackage](../../../develop/reference/osd/gettspoliciessamedia-method-in-class-sms_tasksequencepackage.md)|Gets all policies associated with the specified task sequence.|  
|[GetTSRelatedToDriverCategory Method in Class SMS_TaskSequencePackage](../../../develop/reference/osd/gettsrelatedtodrivercategory-method-in-class-sms_tasksequencepackage.md)|Get task sequence packages related to the specified category.|  
|[ImportSequence Method in Class SMS_TaskSequencePackage](../../../develop/reference/osd/importsequence-method-in-class-sms_tasksequencepackage.md)|Imports an `SMS_TaskSequence` object based on the provided XML.|  
|[RefreshPkgSource Method in Class SMS_TaskSequencePackage](../../../develop/reference/osd/refreshpkgsource-method-in-class-sms_tasksequencepackage.md)|Refreshes the package source at all distribution points when the package properties have not changed.|  
|[SetSequence Method in Class SMS_TaskSequencePackage](../../../develop/reference/osd/setsequence-method-in-class-sms_tasksequencepackage.md)|Updates a task sequence package with the input task sequence.|  
|[SetSourceSite Method in Class SMS_TaskSequencePackage](../../../develop/reference/osd/setsourcesite-method-in-class-sms_tasksequencepackage.md)|Sets the code of the source site for the task sequence package.|  
|[Unlock Method in Class SMS_TaskSequencePackage](../../../develop/reference/osd/unlock-method-in-class-sms_tasksequencepackage.md)|Sets the source site to the current site, which unlocks the task sequence package.|  

## Properties  
 `ActionInProgress`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `AlternateContentProviders`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [large, lazy]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `BootImageID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 ID of the boot image package if the task sequence contains a reference to a boot image in the `References` property. For information about the boot image package, see [SMS_BootImagePackage Server WMI Class](../../../develop/reference/osd/sms_bootimagepackage-server-wmi-class.md).  

 `Category`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 Task sequence package category. The default value is "". The category for the package is assigned using the `Category` property of [SMS_TaskSequence Server WMI Class](../../../develop/reference/osd/sms_tasksequence-server-wmi-class.md).  

 `CustomProgressMsg`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 A custom progress message specified in the Configuration Manager console.  

 `DependentProgram`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 A formatted text string defining any program that should be run before the current program. The format is "\<PackageID>;;\<ProgramName>". For more information, see [SMS_Program Server WMI Class](../../../develop/reference/core/servers/configure/sms_program-server-wmi-class.md).  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `Duration`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 The approximate time, in minutes, that the program takes to run. The default value is 0.  

 `ExtendedData`  
 Data type: `UInt8` Array  

 Access type: Read/Write  

 Qualifiers: [large, lazy]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `ExtendedDataSize`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `ForcedDisconnectDelay`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `ForcedDisconnectEnabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `ForcedDisconnectNumRetries`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `Icon`  
 Data type: `UInt8` Array  

 Access type: Read/Write  

 Qualifiers: [large]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `IconSize`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `IgnoreAddressSchedule`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `ISVData`  
 Data type: `UInt8` Array  

 Access type: Read/Write  

 Qualifiers: [large, lazy]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `ISVDataSize`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `Language`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `LastRefreshTime`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `LocalizedCategoryInstanceNames`  
 Data type: `String Array`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `Manufacturer`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `MIFFilename`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `MIFName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `MIFPublisher`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `MIFVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `NumOfPrograms`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `PackageID`  
 Data type: `String`  

 Access type: Read  

 Qualifiers [key]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `PackageSize`  
 Data type: `UInt32`  

 Access type: Read  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `PackageType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 For this class, the package type is PKG_TYPE_TASK_SEQUENCE (4).  

 `PkgFlags`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [bits]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `PkgSourceFlag`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `PkgSourcePath`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `PreferredAddressType`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `Priority`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `ProgramFlags`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [bits]  

 Flags identifying the installation characteristics of the program. The default flags are default program, UNATTENDED, UNCPATH, HIDEWINDOW, ADMINRIGHTS, and ANY_PLATFORM. The default value is 152084496.  

|Bit|Decimal|Hexadecimal|Description|  
|---------|-------------|-----------------|-----------------|  
|0|1|0x00000001|AUTHORIZED_DYNAMIC_INSTALL. The program is authorized for dynamic installation.|  
|1|2|0x00000002|USE_CUSTOM_PROGRESS_MSG. The program uses a customized progress message.|  
|8|256|0x00000100|WINDOWS_CE. Use Windows CE as the device program. If this value is set, the program is not offered to desktop clients.|  
|9|512|0x00000200|RUN_DEPENDANT_ALWAYS. Always run the immediate dependent of the program.|  
|10|1024|0x00000400|COUNTDOWN. Display the countdown dialog box.|  
|12|4096|0x00001000|DISABLED. The program is disabled.|  
|13|8192|0x00002000|UNATTENDED. The program requires no user interaction.|  
|14|16384|0x00004000|USERCONTEXT. The program needs to run in the user context. Always set the value to 0.|  
|15|32768|0x00008000|ADMINRIGHTS. The program must run under administrator rights.|  
|16|65536|0x00010000|EVERYUSER. The program must be run by every user for whom it is valid. This setting is valid only for mandatory jobs. Always set the value to 0.|  
|17|131072|0x00020000|NOUSERLOGGEDIN. The program is run only when no user is logged on.|  
|18|262144|0x00040000|OKTOQUIT. Program shutdown is enabled. Always set the value to 0.|  
|19|524288|0x00080000|OKTOREBOOT. Computer reboot is enabled. Always set the value to 0.|  
|20|1048576|0x00100000|USEUNCPATH. Program access uses a Universal Naming Convention (UNC) path.|  
|21|2097152|0x00200000|PERSISTCONNECTION. The program connection is persisted. Always set the value to 0.|  
|22|4194304|0x00400000|RUNMINIMIZED. Maximize the program window. Always set the value to 0.|  
|23|8388608|0x00800000|RUNMAXIMIZED. Minimize the program window. Always set the value to 0.|  
|24|16777216|0x01000000|HIDEWINDOW. Hide the program window.|  
|25|33554432|0x02000000|OKTOLOGOFF. Logoff is enabled. Always set the value to 0.|  
|26|67108864|0x04000000|RUNACCOUNT. Run the program using account access.|  
|27|134217728|0x08000000|ANY_PLATFORM. The program can run on any operating system.|  
|28|268435456|0x10000000|STILL_RUNNING. The program is currently running.|  
|29|536870912|0x20000000|SUPPORT_UNINSTALL. The program has an uninstall utility. Always set the value to 0.|  
|31|2147483648|0x80000000|SHOW_IN_ARP. Display the program in Add or Remove Programs.|  

 `References`  
 Data type: `SMS_TaskSequence_Reference` Array  

 Access type: Read-only  

 Qualifiers: [lazy, read]  

 [SMS_TaskSequence_Reference Server WMI Class](../../../develop/reference/osd/sms_tasksequence_reference-server-wmi-class.md) objects representing the packages/programs and applications referred to by steps in the task sequence.  

 `RefreshPkgSourceFlag`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `RefreshSchedule`  
 Data type: `SMS_ScheduleToken` Array  

 Access type:  

 Qualifiers: [max(15), lazy]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `ReferencesCount`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Size of the array indicated by the `References` property. This represents the number of package/programs and applications referred by the task sequence.  

 `Reserved`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 Used internally by the SMS Provider.  

 `SecuredScopeNames`  
 Data type: `String Array`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `SedoObjectVersion`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `Sequence`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [lazy, read]  

 XML-formatted data containing task sequence information.  

 `ShareName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `ShareType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `SourceDate`  
 Data type: `DateTime`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `SourceSite`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `SourceVersion`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `StoredPkgPath`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `StoredPkgVersion`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

 `SupportedOperatingSystems`  
 Data type: `SMS_OS_Details` Array  

 Access type: Read/Write  

 Qualifiers: [lazy]  

 SMS_OS_Details Server WMI Class objects that describe details for the platforms on which the program can run.  

 `TaskSequenceFlags`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [lazy, bits("DANGLING_REF(0)")]  

 Flags indicating task sequence package conditions. The only flag currently defined is DANGLING_REF (bit 0).  

|Bit|Description|  
|---------|-----------------|  
|0|Set if the task sequence references a package that is not defined on the site.|  

 `Type`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [lazy, read]  

 The type of task sequence represented by the package. Possible values are:  

|Value|Description|  
|-----------|-----------------|  
|1|Generic task sequence|  
|2|Operating system deployment task sequence|  

 `Version`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 See [SMS_PackageBaseclass Server WMI Class](../../../develop/reference/core/servers/configure/sms_packagebaseclass-server-wmi-class.md).  

## Remarks  
 Class qualifiers for this class include:  

-   Secured  

-   Icon("Package.ico")  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

 To get started using this class, see How to Create an Operating System Deployment Task Sequence Package.  

 You create an operating system deployment task sequence package by creating an instance of the `SMS_TaskSequencePackage` class to hold a task sequence. The task sequence itself is created by using the Operating System Deployment Task Sequence Object Model, and it is associated with the task sequence package by using the [SetSequence Method in Class SMS_TaskSequencePackage](../../../develop/reference/osd/setsequence-method-in-class-sms_tasksequencepackage.md) method. The package is advertised to clients who can then run the task sequence. For more information, see How to Create an Operating System Deployment Task Sequence Package.  

 For more information about the task sequence WMI objects, see About Operating System Deployment Task Sequences.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Operating System Deployment Server WMI Classes](../../../develop/reference/osd/operating-system-deployment-server-wmi-classes.md)   
 [SMS_TaskSequence Server WMI Class](../../../develop/reference/osd/sms_tasksequence-server-wmi-class.md)
