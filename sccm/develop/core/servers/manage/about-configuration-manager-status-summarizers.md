---
title: "Configuration Manager Status Summarizers"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 99ab10c8-3095-4a73-966e-9c14091341d2
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# About Configuration Manager Status Summarizers
Summarizers are summary classes that help you determine the health, or status, of different aspects of your System Center Configuration Manager site. The summaries, which are produced from status messages, states, and counts, give you a real-time view of the health of System Center Configuration Manager sites, components, packages, and advertisements.  

 Status summarizer classes summarize the status message data. Most of the summarizers create two views of the messages: a site view and a site hierarchy view.  

 All the summaries, except site system, are event-driven summaries. They respond in real time to changes that are taking place in Configuration Manager. Only the site system status summary polls for its information, according to a schedule that you can set.  

> [!NOTE]
>  The `SMS_SummarizerStatus` class can be used to identify the registered summarizers.  

## Site and Component Status  
 These summarizers group summaries of two kinds of data: software component health and physical system health.  

 You can determine the overall health of your site by using the stoplight status value in the `SMS_SummarizerSiteStatus` class, or you can determine the health of your storage objects by using the `SMS_SiteSystemSummarizer` class. For more information, see [How to Determine the Health of a Configuration ManagerSite](../../../../develop/core/servers/manage/how-to-determine-the-health-of-a-configuration-manager-site.md). You can access these and other classes by getting, enumerating, and querying summarizer objects. However, the `SMS_ComponentSummarizer` and `SMS_SiteDetailSummarizer` classes can only be queried — you cannot get or enumerate these objects. Your queries must include a tally interval that defines the period of time from which you want summary information. For example, the following query asks for the count informational, warning, and error messages since Monday.  

```  
SELECT Infos, Warnings, Errors  
FROM SMS_SiteDetailSummarizer  
WHERE TallyInterval = "00011280001A2000"  
```  

> [!NOTE]
>  You cannot add other conditions like SiteCode to the WHERE clause. Adding other conditions will generate an error.  

 For information about using this query, see [How to Perform a Synchronous Configuration Manager Query by Using Managed Code](../../../../develop/core/understand/how-to-perform-a-synchronous-configuration-manager-query-by-using-managed-code.md) and [How to Perform a Synchronous Configuration Manager Query by Using WMI](../../../../develop/core/understand/how-to-perform-a-synchronous-configuration-manager-query-by-using-wmi.md).  

 For more information about using tally intervals, see [About Configuration Manager Tally Intervals](../../../../develop/core/servers/manage/about-configuration-manager-tally-intervals.md).  

 The component summarizers track the progress of advertised programs as they are advertised and run on the client computers.  

 Site system and package status summaries track the state changes instead of counting the error messages. For example, site system status summaries react to changes in free disk space on a site system. If the free space falls below the threshold you set, the site system's status summary health indicator changes.  

 The summarizer classes are:  

|Summarizer|Description|  
|----------------|-----------------|  
|[SMS_ComponentSummarizer Server WMI Class](../../../../develop/reference/core/servers/manage/sms_componentsummarizer-server-wmi-class.md)|Represents a component summarizer that reports on the health of individual Configuration Manager components.|  
|[SMS_SiteDetailSummarizer Server WMI Class](../../../../develop/reference/core/servers/manage/sms_sitedetailsummarizer-server-wmi-class.md)|Represents a site detail summarizer that reports on the per-site status of components and the system.|  
|[SMS_SiteSystemSummarizer Server WMI Class](../../../../develop/reference/core/servers/manage/sms_sitesystemsummarizer-server-wmi-class.md)|Represents a site system summarizer that reports physical system health data for each system and each system role in the Configuration Manager site.|  
|[SMS_SummarizerRootStatus Server WMI Class](../../../../develop/reference/core/servers/manage/sms_summarizerrootstatus-server-wmi-class.md)|Represents a summarizer for the overall health of the entire site hierarchy.|  
|[SMS_SummarizerSiteStatus Server WMI Class](../../../../develop/reference/core/servers/manage/sms_summarizersitestatus-server-wmi-class.md)|Represents a summarizer for the overall health of each site.|  

## Software Distribution Health  
 You can determine the status of advertisements and packages by using the software distribution summarizers.  

### Advertisement Summarizers  
 The advertisement summarizers track the progress of advertised programs as they are advertised and run on the client computers.  

 Advertisement status summaries count the different types of messages generated by advertisements.  

 The advertisement summarizers are:  

|Summarizer|Description|  
|----------------|-----------------|  
|[SMS_AdvertisementStatusRootSummarizer Server WMI Class](../../../../develop/reference/misc/sms_advertisementstatusrootsummarizer-server-wmi-class.md)|Tracks the progress of each advertisement and program as it is advertised and run on the client computers. The reported advertisement status is for all sites in the Configuration Manager hierarchy.|  
|[SMS_AdvertisementStatusSummarizer Server WMI Class](../../../../develop/reference/misc/sms_advertisementstatussummarizer-server-wmi-class.md)|Tracks the progress of each advertisement as it is advertised and run on the client computers. The reported advertisement status is for an individual site.|  

### Package Summarizers  
 Package summarizers are used to track the progress of packages as they are moved to their assigned distribution points. For more information, see [How to Determine Package Status](../../../../develop/core/servers/manage/how-to-determine-package-status.md)  

 Package status summaries track the state changes instead of counting the error messages. For example, The package status summaries track items such as how many clients have installed each package.  

 The package summarizer classes are:  

|Summarizer|Description|  
|----------------|-----------------|  
|[SMS_PackageStatusDetailSummarizer Server WMI Class](../../../../develop/reference/core/servers/configure/sms_packagestatusdetailsummarizer-server-wmi-class.md)|Tracks the progress of each package as it places the software source files on its distribution point. The reported package status is for an individual site.|  
|[SMS_PackageStatusDistPointsSummarizer Server WMI Class](../../../../develop/reference/core/servers/configure/sms_packagestatusdistpointssummarizer-server-wmi-class.md)|Tracks the progress of loading the package source files on the distribution point. The reported package status is for an individual site.|  
|[SMS_PackageStatusRootSummarizer Server WMI Class](../../../../develop/reference/core/servers/configure/sms_packagestatusrootsummarizer-server-wmi-class.md)|Tracks the progress of each package as it places the software source files on its distribution point. The reported package status is for all sites in the hierarchy.|  

## See Also  
 [About Configuration Manager Tally Intervals](../../../../develop/core/servers/manage/about-configuration-manager-tally-intervals.md)   
 [Configuration Manager Status and State](../../../../develop/core/servers/manage/configuration-manager-status-and-summarizers.md)   
 [Status Server WMI Classes](../../../../develop/reference/core/servers/manage/status-server-wmi-classes.md)   
 [How to Determine the Health of a Configuration Manager Site](../../../../develop/core/servers/manage/how-to-determine-the-health-of-a-configuration-manager-site.md)   
 [How to Read The Tally Intervals For a Configuration Manager Site](../../../../develop/core/servers/manage/how-to-read-the-tally-intervals-for-a-configuration-manager-site.md)
