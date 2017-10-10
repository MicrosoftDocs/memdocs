---
title: "Date and Time Formats"
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
ms.assetid: 3c397b79-1209-4fe3-8c48-b3a4970faba7searchScope: - ConfigMgr SDK
caps.latest.revision: 5
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# Configuration Manager Date and Time Formats
Actions, in System Center Configuration Manager, that include date and time values are common, such as get current date and time, 50 days from today is what date?, or find out what day of the week falls on a certain date. When you write queries or compose reports from information that is stored in the Configuration Manager site database, you can express the date and time in any valid SQL format. An example is any expression that has a SQL Server `datetime` data type or that can be converted implicitly, such as an appropriately formatted character string (for example, “1998.10.31��?).  

 The times that are stored in the Configuration Manager site database can be local or in Coordinated Universal Time (UTC). Status Message Viewer can convert to local time, but queries and reports cannot. What you see might be seven hours later than expected, if local time is Pacific Daylight time. Therefore, the user must be aware of the following:  

 Status messages are all in UTC.  

 Offers can be in UTC or local time, depending on a switch that is set in the Configuration Manager console. The property in `SMS_Advertisement` is `AssignedScheduleIsGMT` (`true`/`false`).  

 Inventory is always in local time.  

 This property is `lazy`, but you can view it by using WBEMtest.  

 Depending on the context, you might encounter time notations in the following format:  

 19981118175900000000+***  

 The following information corresponds to the values in the previous example.  

|Value|Description|  
|-----------|-----------------|  
|1998|Year|  
|11|Month|  
|18|Day|  
|1759|Hour|  
|00|Second|  
|000000|Microsecond|  
|+***|Offset from local time|  

 The following table lists valid `datetime` formats that you can use.  

|Style number without century|Style number with century|Type|Output Style|  
|----------------------------------|-------------------------------|----------|------------------|  
|-|0 or 100|Default|mon dd yyyy hh:mm|  
|1|101|USA|mm/dd/yyyy|  
|1|102|ANSI|yyyy.mm.dd|  
|3|103|British/French|dd/mm/yyyy|  
|4|104|German|dd.mm.yyyy|  
|5|105|Italian|dd-mm-yyyy|  
|6|106|–|dd-mon-yyyy|  
|7|107|–|mon.dd.yyy|  
|–|8 or 108|–|hh:mm:ss|  
|–|9 or 109|–|mon dd yyyy<br /><br /> hh:mi:ss:mmmAM (or PM)|  
|10|110|USA|mm-dd-yy|  
|11|111|JAPAN|yy/mm/dd|  
|12|112|ISO|yymmdd|  
|–|13 or 113|–|dd mon yyyy<br /><br /> hh:mi:ss:mmm (24 h)|  
|14|114|–|hh:mi:ss:mmm (24 h)|  

 Besides full `datetime` formats, you can also use `datepart` formats, which are also valid for Query Builder or for writing reports from the System Center Configuration Manager site database. `Datepart` formats provide only part of the full `datetime` format (for example, the year or just the day of the month). The following table lists valid `datepart` formats.  

|Datepart value|Abbreviations|Limits|  
|--------------------|-------------------|------------|  
|Year|Yy|1753-9999|  
|Month|Mm|1-12|  
|Day|Dd|1-31|  
|Hour|Hh|1-23|  
|Minute|Mi|0-59|  
|Second|Ss|0-59|  
|Millisecond|Ms|0-999|  

## See Also  
 [About Configuration Manager Objects](../../../develop/core/understand/about-configuration-manager-objects.md)
