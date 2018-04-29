---
title: "SMS_AppDependencyData Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 907740f6-2b58-4cd3-b94e-b120ef9947e6
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_AppDependencyData Server WMI Class
The `SMS_AppDependencyData` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents application deployment dependency data.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_AppDependencyData : SMS_BaseClass  
{  
    UInt32 AssignmentID;  
    String AssignmentUniqueID;  
    String CollectionID;  
    UInt32 ComplianceState;  
    String DependencyGroup;  
    String DependentDTName;  
    UInt32 DTCI;  
    UInt32 DTModelID;  
    UInt64 DTResultID;  
    UInt32 EnforcementState;  
    UInt32 ErrorValue;  
    String MachineName;  
    String UserName;  
};  
```  

## Methods  
 The `SMS_AppDependencyData` class does not define any methods.  

## Properties  
 `AssignmentID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `AssignmentUniqueID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md)..  

 `CollectionID`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `ComplianceState`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `DependencyGroup`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Name of the Dependency group.  

 `DependentDTName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 Name of the dependent deployment type.  

 `DTCI`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `DTModelID`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `DTResultID`  
 Data type: `UInt64`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 `EnforcementState`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 Enforcement state. Possible values are:  

|||  
|-|-|  
|0|Enforcement State Unknown|  
|1|Enforcement started|  
|2|Enforcement waiting for content|  
|3|Waiting for another installation to complete|  
|4|Waiting for maintenance window before installing|  
|5|Restart required before installing|  
|6|General failure|  
|7|Pending installation|  
|8|Installing update|  
|9|Pending system restart|  
|10|Successfully installed update|  
|11|Failed to install update|  
|12|Downloading update|  
|13|Downloaded update|  
|14|Failed to download update|  

 `ErrorValue`  
 Data type: `UInt32`  

 Access type: Read-only  

 Qualifiers: [read]  

 Last return value.  

 `MachineName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

 Name of the computer that created the message.  

 `UserName`  
 Data type: `String`  

 Access type: Read-only  

 Qualifiers: [key, not_null, read]  

 See [SMS_AppDeploymentAssetDetails Server WMI Class](../../../develop/reference/apps/sms_appdeploymentassetdetails-server-wmi-class.md).  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Application Management Server WMI Classes](../../../develop/reference/apps/application-management-server-wmi-classes.md)
