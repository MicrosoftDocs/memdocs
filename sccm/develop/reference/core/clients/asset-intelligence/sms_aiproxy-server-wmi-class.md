---
title: "SMS_AIProxy Class"
titleSuffix: "Configuration Manager"
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
ms.assetid: dbd4b08e-979f-426e-979b-4dce5dce48dcsearchScope: - ConfigMgr SDK
caps.latest.revision: 10
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_AIProxy Server WMI Class
The `SMS_AIProxy` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in System Center Configuration Manager, that represents an Asset Intelligence proxy computer.  

> [!NOTE]
>  This class can be accessed only on the central administration site.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_AIProxy : SMS_BaseClass   
{   
      string CatalogWatermark;   
      uint32 CategoryChangeCount;   
      uint32 CPUChangeCount;   
      uint32 HWReqChangeCount;   
      datetime LastCatalogUpdateCompletion;   
      datetime LastCatalogUpdateRequest;   
      uint32 LastSCOReturnCode;   
      boolean PeriodicCatalogUpdateEnabled;   
      string PeriodicCatalogUpdateSchedule;   
      uint32 Port;   
      string ProxyCertPath;   
      boolean ProxyEnabled;   
      string ProxyName;   
      uint32 ProxyPollingInterval;   
      uint32 ProxyState;   
      boolean RelevancyOptOut;   
      string SCOURL;   
      string SiteCode;    
      uint32 SoftwareTitlesChangeCount;   
};  
```  

## Methods  
 The following table lists the methods in the `SMS_AIProxy` class.  

|Method|Description|  
|------------|-----------------|  
|[RequestCatalogUpdate Method in Class SMS_AIProxy](../../../../../develop/reference/core/clients/asset-intelligence/requestcatalogupdate-method-in-class-sms_aiproxy.md)|Initiates a System Center Online (SCO) catalog.|  

## Properties  
 `CatalogWatermark`  
 Data type: `String`  

 Access type: Read Only  

 Qualifiers: None  

 The System Center Online catalog watermark, used for internal purposes. This is the watermark that was obtained during the last successful SCO catalog update. This watermark is sent up to the SCO again to request the next batch of updates.  

 `CategoryChangeCount`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 An incrementing count of how many times the category catalog from SCO has been changed since this proxy was installed.  

 `CPUChangeCount`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 An incrementing count of how many times the CPU catalog from SCO has been changed since this proxy was installed.  

 `HWReqChangeCount`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 An incrementing count of how many times the hardware requirements catalog from SCO has been changed since this proxy was installed.  

 `LastCatalogUpdateCompletion`  
 Data type: `DateTime`  

 Access type: Read Only  

 Qualifiers: None  

 The last successful completion of an SCO catalog update.  

 `LastCatalogUpdateRequest`  
 Data type: `DateTime`  

 Access type: Read Only  

 Qualifiers: None  

 Indicates the last time a manually triggered Request Catalog Update was done by the user.  

 `LastSCOReturnCode`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 Last HTTPS return code by SCO.  

 `PeriodicCatalogUpdateEnabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if the user has enabled periodic catalog updates.  

 `PeriodicCatalogUpdateSchedule`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 User-defined schedule of when the SCO catalog updates occur.  

 `Port`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Secure Sockets Layer (SSL) port to use for SCO connection.  

|Type|Value|  
|----------|-----------|  
|Default|443|  
|Minimum|1|  
|Maximum|65535|  

 `ProxyCertPath`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Full Universal Naming Convention (UNC) path of the authentication certificate file.  

 `ProxyEnabled`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if the user has enabled the proxy operations.  

 `ProxyName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: key  

 Fully qualified domain name (FQDN) name of the proxy computer.  

 `ProxyPollingInterval`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None)  

 Polling interval between proxy computer and database, in seconds.  

|Type|Value|  
|----------|-----------|  
|Default|900 (15 Minutes)|  
|Minimum|60 (1 Minute)|  
|Maximum|86400 (24 Hours)|  

 `ProxyState`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: Enumeration  

 Indicates the last SCO communication state. This comes from the proxy to the Asset Intelligence server processor through file replication.  

|Value|Definition|  
|-----------|----------------|  
|0|Not installed|  
|1|Installed|  
|2|Bad configuration|  
|3|Reserved state|  
|4|Bad certificate|  
|5|SCO is online|  
|6|SCO is offline|  

 `RelevancyOptOut`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` if the user has opted out of sending relevancy information.  

 `SCOURL`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 The URL of the SCO.  

 `SiteCode`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Three-letter site code for the site.  

 `SoftwareTitlesChangeCount`  
 Data type: `UInt32`  

 Access type: Read Only  

 Qualifiers: None  

 An incrementing count of how many times the software title catalog from SCO has been changed since this proxy was installed.  

## Remarks  
 Class qualifiers for this class include:  

-   DisplayName("AI Proxy Table")  

-   Dynamic  

-   Provider("ExtnProv")  

-   Secured  

 For more information about both the class qualifiers and the property qualifiers included in the Properties section, see [Configuration Manager Class and Property Qualifiers](../../../../../develop/reference/misc/class-and-property-qualifiers.md).  

## Requirements  

## Return Values  
 An `SInt32` data type that is 0 to indicate success or non-zero to indicate failure.  

 For information about handling returned errors, see [About Configuration Manager Errors](../../../../../develop/core/understand/about-configuration-manager-errors.md).  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../../../develop/core/reqs/server-development-requirements.md).  

## See Also  
 [Configuration Manager Asset Intelligence](../../../../../develop/core/clients/asset-intelligence/asset-intelligence.md)
