---
title: Update an Existing Resource Instance
titleSuffix: Configuration Manager
description: When the Data Discovery Manager, in Configuration Manager, finds an existing resource that matches the data discovery record, the resource instance is updated; otherwise, a new instance is created.
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: conceptual
ms.assetid: 0ccb114a-9666-40f5-a02c-894822f3d359
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# About Updating an Existing Resource Instance
When the Data Discovery Manager (DDM), in Configuration Manager, finds an existing resource that matches the data discovery record (DDR), the resource instance is updated; otherwise, a new instance is created. The DDM uses the following approach to find a resource match.  

## Unique Identifier Specified by DDR  
 If the DDR specifies the unique identifier property for the resource, it is used to find a matching resource instance.  

 If more than one match is found (in the case of cloned computers) or if a match is not found by using the specified unique identifier, the key properties are used to find a matching resource. All key values must match those of an existing resource. In the case of cloned computers, the DDM determines a match that is based on the first key match found.  

## No Unique Identifier Specified by DDR  
 If the DDR does not specify the unique identifier property, the key property values are used to find a matching resource. The DDM determines a match that is based on any single key value matching the same key value of an existing resource. In the case of multiple key matches, the match with the most matching keys is chosen.  

 In both cases, the record that was most recently discovered is chosen in the event of a tie.  

 Before you update an existing instance, you must know the key properties and unique identifier of the resource type. You can run the following query against the Configuration Manager SQL Server database to determine the key properties for a resource class.  

```  
SELECT * FROM DiscPropertyDefs WHERE (Flags & 0x8) = 0x8  
```  

 To determine the unique identifier property, use (Flags & 0x2) = 0x2 in the WHERE clause. The following table shows the unique identifier and key properties for the system, user, and user group resource classes.  

|Resource|Property String|Flag|  
|--------------|---------------------|----------|  
|System|NetbiosName<br /><br /> MAC Address<br /><br /> SMS Unique Identifier|Key.<br /><br /> Key.<br /><br /> Unique Identifier.|  
|User|Unique User Name|Key, unique identifier.|  
|User Group|Unique Usergroup Name|Key, unique identifier.|  

 System resources use a GUID value for the unique identifier that is stored on the Configuration Manager client in the system registry. For more information, see [How to Get the Unique Identifier Value for a Client](../../../../develop/core/servers/configure/how-to-get-the-unique-identifier-value-for-a-client.md).  

 For an example that updates the system resource type, see [How to Add New Properties to an Existing Resource Type](../../../../develop/core/servers/configure/how-to-add-new-properties-to-an-existing-resource-type.md).  

## Heartbeat DDR Processing  
 A Heartbeat DDR is processed if it comes with a time stamp that is earlier than any other DDR (except a Heartbeat DDR). A DDR with a time stamp that is later than the client's current site database time stamp for that discovery method is rejected. The only exception is a Heartbeat DDR, which will be processed.  

## See Also  

 [How to Get the Unique Identifier Value for a Client](../../../../develop/core/servers/configure/how-to-get-the-unique-identifier-value-for-a-client.md)   
 [How to Add New Properties to an Existing Resource Type](../../../../develop/core/servers/configure/how-to-add-new-properties-to-an-existing-resource-type.md)
