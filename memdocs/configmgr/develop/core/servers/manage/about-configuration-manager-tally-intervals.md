---
title: "Configuration Manager Tally Intervals"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 792581fa-e652-4009-a702-91c2aad49904
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# About Configuration Manager Tally Intervals
Configuration Manager is configured with 16 default tally intervals. The intervals for a site are maintained in the site control file. The values are stored in the order that is shown in the following table. For information about accessing these values in the site control file, see the example at the end of this topic.  

> [!NOTE]
>  You can use only the tally intervals that are listed in the table in your queries. When you use a tally interval that is not from the list, an object is returned that contains no data.  

|Schedule|Tally Interval|Class|  
|--------------|--------------------|-----------|  
|Since 12:00AM|0001128000100008|SMS_ST_RecurInterval|  
|Since 04:00AM|0081128000100008|SMS_ST_RecurInterval|  
|Since 08:00AM|0101128000100008|SMS_ST_RecurInterval|  
|Since 12:00PM|0181128000100008|SMS_ST_RecurInterval|  
|Since 04:00PM|0201128000100008|SMS_ST_RecurInterval|  
|Since 08:00PM|0281128000100008|SMS_ST_RecurInterval|  
|Since Sunday|0001128000192000|SMS_ST_RecurWeekly|  
|Since Monday|00011280001A2000|SMS_ST_RecurWeekly|  
|Since Tuesday|00011280001B2000|SMS_ST_RecurWeekly|  
|Since Wednesday|00011280001C2000|SMS_ST_RecurWeekly|  
|Since Thursday|00011280001D2000|SMS_ST_RecurWeekly|  
|Since Friday|00011280001E2000|SMS_ST_RecurWeekly|  
|Since Saturday|00011280001F2000|SMS_ST_RecurWeekly|  
|Since 1st of month|000A470000284400|SMS_ST_RecurMonthlyByDate|  
|Since 15th of month|000A4700002BC400|SMS_ST_NonRecurring|  
|Since site installation|0001128000080008|SMS_ST_NonRecurring|  

 The **Schedule** column is the beginning value of the tally interval. You interpret the beginning value of the tally interval as, "Give me the tallies since Monday." The end of the tally interval is always the current time. The complete tally interval is the same as saying, "Give me all the tallies from Monday to the current time."  

 The classes listed in the tally interval table are embedded schedule token classes that you can use to interpret the interval string. You use the `ReadFromString` method of the `SMS_ScheduleMethods` class to interpret an interval string. This method breaks the interval string into its components and returns the appropriate embedded object.  

 Tally intervals are commonly used in component (SMS_ComponentSummarizer) and site detail (SMS_SiteDetailSummarizer) summarizer queries. For more information, see [About Configuration Manager Status Summarizers](../../../../develop/core/servers/manage/about-configuration-manager-status-summarizers.md).  

## See Also  
 [About Configuration Manager Status Summarizers](../../../../develop/core/servers/manage/about-configuration-manager-status-summarizers.md)   
