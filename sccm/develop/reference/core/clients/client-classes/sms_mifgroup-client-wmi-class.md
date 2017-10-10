---
title: "SMS_MIFGroup Class"
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
ms.assetid: c1005ab0-1ae1-41c3-b2a6-c0a69c5a248asearchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# SMS_MIFGroup Client WMI Class
The `SMS_MifGroup` class is a client Windows Management Instrumentation (WMI) class, in Configuration Manager, that serves as a dynamic instance provider class allowing WMI reporting of Management Information Format (MIF) files that extend the client inventory.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
class   
{  
      String ArchitectureName;  
      String ComponentName;  
      String MIFGroupVerbatim;  
      String MIFClassVerbatim;  
      String MIFKeysVerbatim;  
      String AttributeKeyValues;  
      String MIFAttributesVerbatim[];  
      String MIFFile;  
      UInt64 MIFFileSize;  
      String MIFDirectory;  
};  
```  

## Properties  
 `ArchitectureName`  
 Data type: **String**  

 Access type: Read-only  

 Qualifiers: [key]  

 Architecture of the component and MIF groups. The default value is System.  

 `ComponentName`  
 Data type: **String**  

 Access type: Read-only  

 Qualifiers: [key]  

 Component for MIF groups. The default value is Workstation.  

 `MIFGroupVerbatim`  
 Data type: **String**  

 Access type: Read-only  

 Qualifiers: [key]  

 Group name in MIF syntax, for example, Name = \hotfix\\.  

 `MIFClassVerbatim`  
 Data type: **String**  

 Access type: Read-only  

 Qualifiers: [key]  

 Class name in MIF syntax, for example, Class = \MICROSOFT&#124;UPDATE&#124;1.0\\.  

 `MIFKeysVerbatim`  
 Data type: **String**  

 Access type: Read-only  

 Qualifiers: [key]  

 Reported key values, based on attribute IDs, in MIF syntax, for example, key = 1, 2.  

 `AttributeKeyValues`  
 Data type: **String**  

 Access type: Read-only  

 Qualifiers: [key]  

 Attribute key values, concatenated in string format, corresponding to the key attribute IDs. This property is primarily useful as a WMI instance key for MIF groups. It is not especially useful for MIF group translation.  

 `MIFAttributesVerbatim`  
 Data type: **String** array  

 Access type: Read-only  

 Qualifiers: None  

 Array of MIF attribute definitions and values in MIF syntax.  

 `MIFFile`  
 Data type: **String**  

 Access type: Read-only  

 Qualifiers: None  

 MIF file name queried, typically *.mif.  

 `MIFFileSize`  
 Data type: **UInt64**  

 Access type: Read-only  

 Qualifiers: None  

 Size of the MIF file containing the group. This property is used to limit reporting based on the MIF file size.  

 `MIFDirectory`  
 Data type: **String**  

 Access type: Read-only  

 Qualifiers: None  

 Not implemented. MIF directory queried.  

## Remarks  
 This class is used by the Inventory Client Agent to enumerate the third-party MIF files at a designated collection directory. For each file, the instance provider parses the file against the MIF syntax, validates the contents against Configuration Manager restrictions, and reports each individual MIF group in a generic form that is usable by the Inventory Client Agent and management point. The generic instance format is specifically designed to translate consistently and easily between MIF syntax for any number of MIF group definitions and values. This translation is especially important on the management point, where the Inventory Client Agent report is translated back into MIF format for processing at the Configuration Manager site server.  

 The preferred way to extend client inventory is through WMI instances (static or dynamic). However, this provider allows a migration step for SMS 2.0 MIF files already in use.  

 The `SMS_MIFGroup` class is specifically used to expose No Identification MIF files (NOIDMIFs) through WMI in client inventory. NOIDMIFs are used to extend client inventory beyond that requested for specific WMI instances in the site policy (see InventoryDataItem). For example, hardware vendors can supply asset information by using NOIDMIFs.  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Client Runtime Requirements](../../../../../develop/core/reqs/client-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Client Development Requirements](../../../../../develop/core/reqs/client-development-requirements.md).  

## See Also  
 [Inventory Agent Client WMI Classes](../../../../../develop/reference/core/clients/client-classes/inventory-agent-client-wmi-classes.md)   
 [FileCollectionAction Client WMI Class](../../../../../develop/reference/core/clients/client-classes/filecollectionaction-client-wmi-class.md)   
 [FileSystemFile Client WMI Class](../../../../../develop/reference/core/clients/client-classes/filesystemfile-client-wmi-class.md)   
 [InventoryDataItem Client WMI Class](../../../../../develop/reference/core/clients/client-classes/inventorydataitem-client-wmi-class.md)
