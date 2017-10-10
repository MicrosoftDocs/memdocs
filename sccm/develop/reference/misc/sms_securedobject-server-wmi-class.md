---
title: "SMS_SecuredObject Class"
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
ms.assetid: add642a3-26e1-4a6f-9d27-97297809a20asearchScope: - ConfigMgr SDK
caps.latest.revision: 16
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_SecuredObject Server WMI Class
The `SMS_SecuredObject` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents a secured object.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_SecuredObject : SMS_BaseClass  
{  
     UInt32 AvailableClassPermissions;  
     UInt32 AvailableInstancePermissions;  
     UInt32 DefaultClassPermissions;  
     UInt32 DefaultInstancePermissions;  
     UInt32 ObjectKey  
     String ObjectName;  
};  
```  

## Methods  
 The following table lists methods in `SMS_SecuredObject`.  

|Method|Description|  
|------------|-----------------|  
|[GetCollectionsWithResourcePermissions Method in Class SMS_SecuredObject](../../../develop/reference/misc/getcollectionswithresourcepermissions-method-in-class-sms_securedobject.md)|Gets the list of collection identifiers for the collections to which the user has the specified permissions.|  
|[RefreshNTGroupMembership Method in Class SMS_SecuredObject](../../../develop/reference/misc/refreshntgroupmembership-method-in-class-sms_securedobject.md)|Refreshes the information stored about the user's Windows group membership.|  
|[UserHasPermissions Method in Class SMS_SecuredObject](../../../develop/reference/misc/userhaspermissions-method-in-class-sms_securedobject.md)|Determines whether a user has permissions for an object.|  

## Properties  
 `AvailableClassPermissions`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [bits]  

 Set of available global permissions that can be set for the specified class. Possible values are listed below. The default value is 0.  

|||  
|-|-|  
|0|READ|  
|1|MODIFY|  
|2|DELETE|  
|3|DISTRIBUTE|  
|4|Not used|  
|5|REMOTE_CONTROL|  
|6|ADVERTISE|  
|7|MODIFY_RESOURCE|  
|8|ADMINISTER|  
|9|DELETE_RESOURCE|  
|10|CREATE|  
|11|VIEW_COLL_FILE|  
|12|READ_RESOURCE|  
|13|DELEGATE|  
|14|METER|  
|15|MANAGESQLCOMMAND|  
|16|MANAGESTATUSFILTER|  
|17|MANAGEFOLDER|  
|18|NETWORKACCESS|  
|19|IMPORTMACHINE|  
|20|CREATETSMEDIA|  
|21|MODIFYCOLLECTIONSETTING|  
|22|MANAGEOSDCERTIFICATE|  
|23|RECOVERUSERSTATE|  

 `AvailableInstancePermissions`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [bits]  

 Set of available permissions that can be set for an instance of the specified class. Possible values are listed below. The default value is 0.  

|||  
|-|-|  
|0|READ|  
|1|MODIFY|  
|2|DELETE|  
|3|DISTRIBUTE|  
|4|Not used|  
|5|REMOTE_CONTROL|  
|6|ADVERTISE|  
|7|MODIFY_RESOURCE|  
|8|ADMINISTER|  
|9|DELETE_RESOURCE|  
|10|CREATE|  
|11|VIEW_COLL_FILE|  
|12|READ_RESOURCE|  
|13|DELEGATE|  
|14|METER|  
|15|MANAGESQLCOMMAND|  
|16|MANAGESTATUSFILTER|  
|17|MANAGEFOLDER|  
|18|NETWORKACCESS|  
|19|IMPORTMACHINE|  
|20|CREATETSMEDIA|  
|21|MODIFYCOLLECTIONSETTING|  
|22|MANAGEOSDCERTIFICATE|  
|23|RECOVERUSERSTATE|  

 `DefaultClassPermissions`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [bits]  

 Set of default permissions that all users and groups are granted for the specified class. Possible values are listed below. The default value is 0.  

|||  
|-|-|  
|0|READ|  
|1|MODIFY|  
|2|DELETE|  
|3|DISTRIBUTE|  
|4|Not used|  
|5|REMOTE_CONTROL|  
|6|ADVERTISE|  
|7|MODIFY_RESOURCE|  
|8|ADMINISTER|  
|9|DELETE_RESOURCE|  
|10|CREATE|  
|11|VIEW_COLL_FILE|  
|12|READ_RESOURCE|  
|13|DELEGATE|  
|14|METER|  
|15|MANAGESQLCOMMAND|  
|16|MANAGESTATUSFILTER|  
|17|MANAGEFOLDER|  
|18|NETWORKACCESS|  
|19|IMPORTMACHINE|  
|20|CREATETSMEDIA|  
|21|MODIFYCOLLECTIONSETTING|  
|22|MANAGEOSDCERTIFICATE|  
|23|RECOVERUSERSTATE|  
|24|MANAGEBMC|  
|25|VIEWBMC|  

 `DefaultInstancePermissions`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [bits]  

 Set of default instance permissions that all users and groups are granted for the specified class. Possible values are listed below. The default value is 0.  

|||  
|-|-|  
|0|READ|  
|1|MODIFY|  
|2|DELETE|  
|3|DISTRIBUTE|  
|4|Not used|  
|5|REMOTE_CONTROL|  
|6|ADVERTISE|  
|7|MODIFY_RESOURCE|  
|8|ADMINISTER|  
|9|DELETE_RESOURCE|  
|10|CREATE|  
|11|VIEW_COLL_FILE|  
|12|READ_RESOURCE|  
|13|DELEGATE|  
|14|METER|  
|15|MANAGESQLCOMMAND|  
|16|MANAGESTATUSFILTER|  
|17|MANAGEFOLDER|  
|18|NETWORKACCESS|  
|19|IMPORTMACHINE|  
|20|CREATETSMEDIA|  
|21|MODIFYCOLLECTIONSETTING|  
|22|MANAGEOSDCERTIFICATE|  
|23|RECOVERUSERSTATE|  
|24|MANAGEBMC|  
|25|VIEWBMC|  

 `ObjectKey`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Numeric key that describes the type of secured object being specified. Possible values are listed below. The default value is 0.  

|||  
|-|-|  
|1|[SMS_Collection Server WMI Class](../../../develop/reference/core/clients/collections/sms_collection-server-wmi-class.md)|  
|2|[SMS_Package Server WMI Class](../../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md)|  
|3|[SMS_Advertisement Server WMI Class](../../../develop/reference/core/servers/configure/sms_advertisement-server-wmi-class.md)|  
|4|[SMS_StatusMessage Server WMI Class](../../../develop/reference/core/servers/manage/sms_statusmessage-server-wmi-class.md)|  
|5|(Not used)|  
|6|[SMS_Site Server WMI Class](../../../develop/reference/core/servers/configure/sms_site-server-wmi-class.md)|  
|7|[SMS_Query Server WMI Class](../../../develop/reference/core/clients/manage/sms_query-server-wmi-class.md)|  
|8|[SMS_Report Server WMI Class](../../../develop/reference/misc/sms_report-server-wmi-class.md)|  
|9|[SMS_MeteredProductRule Server WMI Class](../../../develop/reference/apps/sms_meteredproductrule-server-wmi-class.md)|  
|10|SMS_ApplicableUpdatesSummaryEx Server WMI Class|  
|11|[SMS_ConfigurationItem Server WMI Class](../../../develop/reference/compliance/sms_configurationitem-server-wmi-class.md)|  
|14|[SMS_OperatingSystemInstallPackage Server WMI Class](../../../develop/reference/osd/sms_operatingsysteminstallpackage-server-wmi-class.md)|  
|15|[SMS_Template Server WMI Class](../../../develop/reference/sum/sms_template-server-wmi-class.md)|  
|16|[SMS_UpdatesAssignment Server WMI Class](../../../develop/reference/sum/sms_updatesassignment-server-wmi-class.md)|  
|17|[SMS_StateMigration Server WMI Class](../../../develop/reference/osd/sms_statemigration-server-wmi-class.md)|  
|18|[SMS_ImagePackage Server WMI Class](../../../develop/reference/osd/sms_imagepackage-server-wmi-class.md)|  
|19|[SMS_BootImagePackage Server WMI Class](../../../develop/reference/osd/sms_bootimagepackage-server-wmi-class.md)|  
|20|[SMS_TaskSequencePackage Server WMI Class](../../../develop/reference/osd/sms_tasksequencepackage-server-wmi-class.md)|  
|21|[SMS_DeviceSettingPackage Server WMI Class](../../../develop/reference/mdm/sms_devicesettingpackage-server-wmi-class.md)|  
|22|[SMS_DeviceSettingItem Server WMI Class](../../../develop/reference/mdm/sms_devicesettingitem-server-wmi-class.md)|  
|23|[SMS_DriverPackage Server WMI Class](../../../develop/reference/osd/sms_driverpackage-server-wmi-class.md)|  
|24|[SMS_SoftwareUpdatesPackage Server WMI Class](../../../develop/reference/sum/sms_softwareupdatespackage-server-wmi-class.md)|  
|25|[SMS_Driver Server WMI Class](../../../develop/reference/osd/sms_driver-server-wmi-class.md)|  

 `ObjectName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Class name of the secured object.  

## Remarks  
 There are no special class qualifiers for this class. For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../develop/reference/misc/class-and-property-qualifiers.md).  

 The Configuration Manager objects that can be secured are defined by the `ObjectKey` property.  

 The DELEGATE permission applies to all objects listed in `ObjectKey` except `SMS_StatusMessage`.  

 METER only applies to the `SMS_Site` object and allows the targeting of metering rules to a site.  

 Manage SQL commands and Manage Status Filter only apply to `SMS_Site`. These permissions allow management of SQL commands and status filter rules, respectively. Because both of these permissions can allow arbitrary code to run with elevated privileges, they require special credentials.  

 For more information about SMS Provider rights, see [Classes and Instances for Object Security in Configuration Manager](http://go.microsoft.com/fwlink/?LinkId=110808).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
