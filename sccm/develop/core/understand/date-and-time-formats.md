---
title: "Date and Time Formats | Microsoft Docs"
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
ms.assetid: cdbb74bf-b446-409e-b5a7-6ecf4a78f4a7
caps.latest.revision: 5
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# Date and Time Formats
Actions that include date and time values are common, such as get current date and time, 50 days from today is what date?, or find out what day of the week falls on a certain date. When you write queries by using the SMS Query Builder interface or you compose reports from information stored in the SMS site database, you can express the date and time in any valid SQL format. An example is any expression that has a SQL Server **datetime** data type or that can be converted implicitly, such as an appropriately formatted character string (for example, 1998.10.31).  

 The times that are stored in the SMS site database can be local or in Greenwich Mean Time (GMT). Status Message Viewer can convert to local time, but queries and reports cannot. What you see might be seven hours later than expected, if local time is Pacific Daylight. Therefore, the user must be aware of the following:  

-   Status messages are all in GMT.  

-   Offers can be in GMT or local time, depending on a switch that is set in the SMS Administrator console. The property in **SMS_AdvertisementisAssignedScheduleIsGMT** (TRUE/FALSE).  

-   Inventory is always in local time.  

 This property is lazy, meaning it is not exposed to Query Builder, but you can view it using WBEMtest.  

 Depending on the context, you might encounter time notations in the following universal format:  

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

 The following table lists valid datetime formats that you can use with Query Builder.  

|Style number without century|Style number<br /><br /> with century|Type|Output style|  
|----------------------------------|-----------------------------------|----------|------------------|  
||0 or 100|Default|mon dd yyyy hh:mm|  
|1|101|USA|mm/dd/yyyy|  
|2|102|ANSI|yyyy.mm.dd|  
|3|103|British/French|dd/mm/yyyy|  
|4|104|German|dd.mm.yyyy|  
|5|105|Italian|dd-mm-yyyy|  
|6|106||dd-mon-yyyy|  
|7|107||mon.dd.yyy|  
||8 or 108||hh:mm:ss|  
||9 or 109||mon dd yyyy<br /><br /> hh:mi:ss:mmmAM (or PM)|  
|10|110|USA|mm-dd-yy|  
|11|111|JAPAN|yy/mm/dd|  
|12|112|ISO|yymmdd|  
||13 or 113||dd mon yyyy<br /><br /> hh:mi:ss:mmm (24 h)|  
|14|114||hh:mi:ss:mmm (24 h)|  

 Besides full datetime formats, you can also use datepart formats, which are also valid for Query Builder or for writing reports from the SMS site database. Datepart formats provide only part of the full datetime format (for example, the year or just the day of the month). The following table lists valid datepart formats.  

|Datepart value|Abbreviation|Limits|  
|--------------------|------------------|------------|  
|Year|Yy|1753-9999|  
|Month|Mm|1-12|  
|Day|Dd|1-31|  
|Hour|Hh|0-23|  
|Minute|Mi|0-59|  
|Second|Ss|0-59|  
|Millisecond|Ms|0-999|
