---
title: "SMS_TopThreatsDetected Class"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: d15d9933-913a-418e-8474-4310ddbc367b
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# SMS_TopThreatsDetected Server WMI Class
The `SMS_TopThreatsDetected` Windows Management Instrumentation (WMI) class is an SMS Provider server class, in Configuration Manager, that summarizes the top threats found in the last 24 hours per collection.  

 The following syntax is simplified from Managed Object Format (MOF) code and includes all inherited properties.  

## Syntax  

```  
Class SMS_TopThreatsDetected : SMS_BaseClass  
{  
    String CollectionID;  
    UInt32 MemberCount;  
    UInt32 Rank;  
    UInt32 ThreatCategoryID;  
    UInt64 ThreatID;  
    String ThreatName;  
    UInt32 TotalMemberCount;  
};  
```  

## Methods  
 The `SMS_TopThreatsDetected` class does not define any methods.  

## Properties  
 `CollectionID`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Identifier of the collection summarized.  

 `MemberCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Count of members with a threat.  

 `Rank`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Rank of threat exposure in collection (1 is greatest).  

 `ThreatCategoryID`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Category identifier of threat. Possible values are:  

|CategoryID|Category|  
|----------------|--------------|  
|1|Adware|  
|2|Spyware|  
|3|Password Stealer|  
|4|Trojan Downloader|  
|5|Worm|  
|6|Backdoor|  
|8|Trojan|  
|9|Email Flooder|  
|11|Dialer|  
|12|Monitoring Software|  
|13|Browser Modifier|  
|19|Joke Program|  
|21|Software Bundler|  
|22|Trojan Notifier|  
|23|Settings Modifier|  
|27|Potentially Unwanted Software|  
|30|Exploit|  
|32|Malware Creation Tool|  
|33|Remote Control Software|  
|34|Tool|  
|36|Trojan Denial of Service|  
|37|Trojan Dropper|  
|38|Trojan Mass Mailer|  
|39|Trojan Monitoring Software|  
|40|Trojan Proxy Server|  
|42|Virus|  
|43|Permitted|  
|44|Not Yet Classified|  
|46|Suspicious Behavior|  

 `ThreatID`  
 Data type: `UInt64`  

 Access type: Read/Write  

 Qualifiers: [key]  

 Threat identifier.  

 `ThreatName`  
 Data type: `String`  

 Access type: Read/Write  

 Qualifiers: none  

 Name of the threat.  

 `TotalMemberCount`  
 Data type: `UInt32`  

 Access type: Read/Write  

 Qualifiers: none  

 Total count of members in the collection.  

## Remarks  

## Requirements  

## Runtime Requirements  
 For more information, see [Configuration Manager Server Runtime Requirements](../../../develop/core/reqs/server-runtime-requirements.md).  

## Development Requirements  
 For more information, see [Configuration Manager Server Development Requirements](../../../develop/core/reqs/server-development-requirements.md).
