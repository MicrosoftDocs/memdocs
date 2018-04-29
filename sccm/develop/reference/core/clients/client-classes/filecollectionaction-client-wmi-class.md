---
title: "FileCollectionAction Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 83a2cce8-789b-4599-9823-98d02a8e733f
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# FileCollectionAction Client WMI Class
In Configuration Manager, the **FileCollectionAction** class is a client Windows Management Instrumentation (WMI) class that associates a set of file collection rules with reporting details, tying together files to collect with the destination of the report.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class FileCollectionAction : SMS_FileCollectionAgent_Policy  
{  
      String CollectionType;  
      UInt32 DefaultTimeout;  
      Boolean DeleteFilesAfterCollection;  
      String Description;  
      String FileCollectionActionID;  
      String FileDestination;  
      String FileType;  
      UInt32 MaxTotalFileSize;  
      String PolicyID;  
      String PolicyInstanceID;  
      UInt32 PolicyPrecedence;  
      String PolicyRuleID;  
      String PolicySource;  
      String PolicyVersion;  
      Boolean ReportFileDetails;  
      UInt32 ReportTimeout;  
      UInt32 ScanInterval;  
      String SkipScan;  
};  
```  

## Methods  
 The `FileCollectionAction` class does not define any methods.  

## Properties  
 `CollectionType`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Type of file collection report. The possible values are:  

|||  
|-|-|  
|Full|Report contains all files collected by the associated **CollectableFileItem** queries.|  
|Delta|Report contains files that have changed since the last report.|  
|Resync|Report contains files in full report and also contains all files collected, but it is triggered by a site policy resynchronization request.|  

 `DefaultTimeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Timeout value, in milliseconds, for each file system inventory provider query executed. The default value is 7,200,000 milliseconds.  

 `DeleteFilesAfterCollection`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 Value used to indicate whether collected files should be deleted from the client after collection.  

 For IDMIF collection, this value is `true`. The collection results are similar to moving the files from the client to the destination.  

 For software file collection, this value is `false`. The collection results are similar to copying the files from the client to the destination.  

 `Description`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Text field that describes the file collection action. The predefined description values are File Collection and IDMIF Collection.  

 `FileCollectionActionID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [realkey]  

 Unique ID for the file collection action. Possible values are:  

|||  
|-|-|  
|Software File Collection|{00000000-0000-0000-0000-000000000010}|  
|IDMIF Collection|{00000000-0000-0000-0000-000000000012}|  

 `FileDestination`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Destination address for the generated report.  

 `FileType`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 Type of collected file attachments for a report. Possible values are:  

-   FILECOLL  

-   IDMIF  

 `MaxTotalFileSize`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Cumulative maximum size of collected files in a generated report. The Inventory Agent ensures that the overall file attachment size does not exceed this value.  

 `PolicyID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Unique ID of the policy.  

 `PolicyInstanceID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Unique ID of the policy instance.  

 `PolicyPrecedence`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Precedence for the policy.  

 `PolicyRuleID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: Key  

 Unique ID of the rule used to create the policy.  

 `PolicySource`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Source of the policy.  

 `PolicyVersion`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Version of the policy.  

 `ReportFileDetails`  
 Data type: `Boolean`  

 Access type: Read/Write  

 Qualifiers: None  

 `true` to include external file details for each file attachment in the generated report for software file collection. The generated report contains the original file name, path, size, and modified date.  

 `ReportTimeout`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Timeout value used by the client framework for expiring the inventory report (message) sent by the Inventory Agent to the management point. If the inventory report cannot be sent to the management point, the client framework continues to hold on to the message until the report timeout interval. It periodically tries to resend the message.  

 `ScanInterval`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: None  

 Delay, in milliseconds, to pass to the file system inventory provider for the file collection scan.  

 `SkipScan`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: None  

 File name used to prevent the scanning of a directory. This value is typically set to Skpswi.dat for software file collection. It is typically not set for IDMIF collection.  

## Remarks  
 This class is similar to the **InventoryAction**, with the main difference being the type of collection files for file collection and WMI instances for inventory.  

 Two predefined file collection actions are provided through the site policy: software file collection and IDMIF collection. For each of these file collection actions, the Inventory Agent generates a report with attachments, based on queries built from **CollectableFileItem** instances. The generated report is sent to the specified destination.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Inventory Agent Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/inventory-agent-client-wmi-classes.md)   
 [InventoryAction Client WMI Class](../../../../../develop/reference/core/clients/client-classes/inventoryaction-client-wmi-class.md)   
 [CollectableFileItem Client WMI Class](../../../../../develop/reference/core/clients/client-classes/collectablefileitem-client-wmi-class.md)
