---
title: "Status Server WMI Classes"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 7b188e00-b566-4115-bb85-b8c6629e948f
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Status Server WMI Classes
The status server Windows Management Instrumentation (WMI) classes allow access to the Microsoft System Center Configuration Manager status system. You can use these classes to create and view status messages and to view status summarizers. The status system indicates the health of a Configuration Manager site and the progress of certain actions, such as software distribution. The status system includes three groups of classes:  

- Status summarizer classes, for example, [SMS_ComponentSummarizer Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_componentsummarizer-server-wmi-class.md)  

- Status reporting classes, for example, [SMS_StatMsgAttributes Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statmsgattributes-server-wmi-class.md)  

- Optimized status reporting classes, for example, [SMS_StatAttr Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statattr-server-wmi-class.md)  

  For more information about how the Configuration Manager status system works, see About Configuration Manager Status Summarizers.  

  The Configuration Manager server class schema is a set of WMI classes that represent the objects found on a server running Configuration Manager. Each Configuration Manager class is a template for a managed object and all instances of the object use the template. Classes can contain properties and methods. The properties describe the class data and the methods typically perform data management. For more information about developing applications using these classes, see [About Configuration Manager SDK Requirements](../../../../../develop/core/reqs/about-configuration-manager-sdk-requirements.md).  

## Status Server WMI Classes  

-   [SMS_ComponentSummarizer Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_componentsummarizer-server-wmi-class.md)  

-   [SMS_SecondarySiteStatus Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_secondarysitestatus-server-wmi-class.md)  

-   [SMS_SiteDetailSummarizer Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_sitedetailsummarizer-server-wmi-class.md)  

-   [SMS_SiteSystemSummarizer Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_sitesystemsummarizer-server-wmi-class.md)  

-   [SMS_StatAttr Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statattr-server-wmi-class.md)  

-   [SMS_StatInsStr Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statinsstr-server-wmi-class.md)  

-   [SMS_StatMsg Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statmsg-server-wmi-class.md)  

-   [SMS_StatMsgAttributes Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statmsgattributes-server-wmi-class.md)  

-   [SMS_StatMsgInsStrings Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statmsginsstrings-server-wmi-class.md)  

-   [SMS_StatMsgModuleNames Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statmsgmodulenames-server-wmi-class.md)  

-   [SMS_StatMsgWithInsStrings Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statmsgwithinsstrings-server-wmi-class.md)  

-   [SMS_StatusMessage Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_statusmessage-server-wmi-class.md)  

-   [SMS_SummarizerRootStatus Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_summarizerrootstatus-server-wmi-class.md)  

-   [SMS_SummarizationSettings Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_summarizationsettings-server-wmi-class.md)  

-   [SMS_SummarizerSiteStatus Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_summarizersitestatus-server-wmi-class.md)  

-   [SMS_SummarizerStatus Server WMI Class](../../../../../develop/reference/core/servers/manage/sms_summarizerstatus-server-wmi-class.md)  

## See Also  
 [Configuration Manager Status](../../../../../develop/reference/core/servers/manage/status-classes.md)   
 [Configuration Manager Reference](../../../../../develop/reference/configuration-manager-reference.md)
