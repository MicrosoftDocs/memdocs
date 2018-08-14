---
title: "SMS_AzureService Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: a7506056-7433-4903-8a9a-b3dcd417bf8c
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_AzureService Server WMI Class
The `SMS_AzureService` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that represents an Windows Azure service which is a Cloud Distribution Point for Configuration Manager.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_AzureService : SMS_BaseClass  
{  
    UInt32 AzureServiceID;  
    String DeploymentSlot;  
    String Description;  
    UInt32 Flags;  
    String Fqdn;  
    String ManagementCertificate;  
    UInt32 ManagementCertificateType;  
    String ManagementThumbprint;  
    String NALPath;  
    String Name;  
    UInt32 NumberOfInstances;  
    String Region;  
    String ServiceCertificate;  
    String ServiceCName;  
    String ServiceThumbprint;  
    String ServiceThumbprintAlgorithm;  
    String ServiceType;  
    String SiteCode;  
    UInt32 State;  
    UInt32 StatusDetails;  
    UInt32 StorageCriticalThreshold;  
    Boolean StorageQuotaGrow;  
    UInt32 StorageQuotaInGB;  
    String StorageServiceName;  
    UInt32 StorageUsage;  
    UInt32 StorageWarningThreshold;  
    String SubscriptionID;  
    UInt32 TrafficCriticalThreshold;  
    UInt32 TrafficOutInGB;  
    Boolean TrafficOutStopService;  
    UInt32 TrafficOutUsage;  
    UInt32 TrafficWarningThreshold;  
};  
```  

## Methods  
 The following table lists the methods in the `SMS_AzureService` class.  

|Method|Description|  
|------------|-----------------|  
|[Start Method in Class SMS_AzureService](../../../../../develop/reference/core/servers/configure/start-method-in-class-sms_azureservice.md)|Method used to start a Windows Azure Service (in this case the Cloud Distribution point).|  
|[Stop Method in Class SMS_AzureService](../../../../../develop/reference/core/servers/configure/stop-method-in-class-sms_azureservice.md)|Method used to stop a Windows Azure Service (in this case the Cloud Distribution point).|  

## Properties  
 `AzureServiceID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [key, not_null]  

 Identifier of the Windows Azure service.  

 `DeploymentSlot`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 Deployment slot. Possible values are:  

|Value|
|-|  
|Production|  
|Staging|  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 Description of the Windows Azure service.  

 `Flags`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [bits]  

 Flags for configuring the Windows Azure service. Possible values are:  

|Value|
|-|  
|WAD_LOGS_DONT_DELETE(0)|  

 `Fqdn`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 The concatenation of the property "Name" with ".cloudapp.net".  

 `ManagementCertificate`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Management certificate.  

 `ManagementCertificateType`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [enumeration]  

 Management certificate type. Possible values are:  

|||  
|-|-|  
|0|PAIR|  
|1|PUBLICONLY|  

 `ManagementThumbprint`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Management thumbprint.  

 `NALPath`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 NAL path for the corresponding Distribution Point.  

 `Name`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 Name of the Windows Azure service based on restrictions imposed by Windows Azure.  

 `NumberOfInstances`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 Number of instances to deploy.  

 `Region`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 This is the value selected from the list of regions eligible for your Windows Azure subscription ID, obtained either by using the Configuration Manager Administrator console or the Windows Azure management console.  

 `ServiceCertificate`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Service certificate.  

 `ServiceCName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Should be the same as the CName on the `ServiceCertificate` property.  

 `ServiceThumbprint`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Service certificate thumbprint algorithm supported by Windows Azure. The only thumbprint algorithm supported is SHA1.  

 `ServiceThumbprintAlgorithm`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Service certificate thumbprint algorithm supported by Windows Azure. Possible values below:  

|Thumbprint Algorithm|  
|--------------------------|  
|SHA1|  

 `ServiceType`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 Type of Windows Azure service. Possible values below:  

|Windows Asure Service|  
|---------------------------|  
|CloudDistributionPoint|  

 `SiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 Site code of the primary site.  

 `State`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Current state.  

 `StatusDetails`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Current status details.  

 `StorageCriticalThreshold`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Indicates the threshold percent at which critical alerts will be generated for storage.  

 `StorageQuotaGrow`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 `true` if Indicates whether storage quota should automatically grow dynamically.  

 This property is not currently used.  

 `StorageQuotaInGB`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 Storage quota in gigabytes.  

 `StorageServiceName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 Name of Windows Azure Storage service, based on restrictions imposed on by Windows Azure.  

 `StorageUsage`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Indicates the storage usage of the Windows Azure Storage service in gigabytes.  

 `StorageWarningThreshold`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Indicates the threshold percent at which warning alerts will be generated for storage.  

 `SubscriptionID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 Subscription identifier of the Windows Azure service.  

 `TrafficCriticalThreshold`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Indicates the threshold percent at which critical alerts will be generated for traffic out.  

 `TrafficOutInGB`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 Traffic out in gigabytes.  

 `TrafficOutStopService`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: [not_null]  

 Indicates whether the service should be stopped when the traffic out threshold is met.  

 This property is not currently used.  

 `TrafficOutUsage`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Indicates the traffic out usage.  

 `TrafficWarningThreshold`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Indicates the threshold percent at which warning alerts will be generated for traffic out.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).
