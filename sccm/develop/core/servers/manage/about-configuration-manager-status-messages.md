---
title: "Configuration Manager Status Messages"
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
ms.assetid: f3011860-6a66-407d-b3fc-93e4f6f892e1searchScope: - ConfigMgr SDK
caps.latest.revision: 7
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# About Configuration Manager Status Messages
In System Center Configuration Manager, status messages are the universal means for components to communicate information about their health to the System Center Configuration Manager administrator. Status messages are similar to Windows NT Events; they have a severity, ID, description, and so on.  

 The Configuration Manager Status System is a fully-distributed, enterprise-wide aggregation and summarization system for status messages. Status messages flow from components to the Configuration Manager site servers and up the Configuration Manager site hierarchy.  

 The administrator configures how Configuration Manager processes the status messages at each site server in the hierarchy. This processing can include storing the status messages in a SQL database, replicating the messages to the parent Configuration Manager site, reporting the messages as Windows Events on the site server, and exporting the messages to another eventing or alerting application.  

 Certain kinds of status messages are automatically processed by Summarizer components that are running on the site servers. The Summarizers produce high-level data about the raw flows of status messages. Administrators monitor this data in the Configuration Manager console.  

 Status messages are similar to Windows events; they have a severity, ID, and description. They also support message insertion strings and named attribute values. This allows user-defined messages to be reported through the site.  

## Types of Status Messages  

### Predefined Status Messages  
 Each Configuration Manager component has a set of predefined status messages assigned to it. It is important that the context in which an application reports a predefined status message matches exactly the purpose of the Configuration Manager component status message. Otherwise, the integrity of the site might be affected by Configuration Manager misinterpreting the meaning of the status message. For more information, see [About Configuration Manager Component Status Messages](../../../../develop/core/servers/manage/about-configuration-manager-component-status-messages.md).  

### User-defined Generic Status Messages  
 Configuration Manager provides three types of user-defined generic status messages.  

-   Information  

-   Warning  

-   Error  

 Along with the message type, insertion strings and attributes can be supplied. The text that is provided as the insertion string, when creating the status message, is the text seen in the user interface. This makes using generic messages simple, but it does not allow for localization. For more information, see [How to Read User-Defined Status Messages](../../../../develop/core/servers/manage/how-to-read-user-defined-status-messages.md).  

## Creating Status Messages on the Client  
 You can create events on client computers in the following ways:  

### SMSEvent  
 [SMSEvent Class](../../../../develop/reference/core/servers/manage/smsevent-class.md) is a COM automation class that you use to raise user-defined status messages on a client. As a COM Automation object, it can readily be used by VBScript. For more information, see [SMSEvent Class](../../../../develop/reference/core/servers/manage/smsevent-class.md).  

### SMSCSTAT.DLL  
 SMSCSTAT.DLL is a Win32 dynamic link library that is available on clients. It has been installed on System Center Configuration Manager clients since SMS 2.0 Service Pack 1. It cannot be easily be used by VBScript. For more information, see [About Using SMSCSTAT.DLL to Create Status Messages](../../../../develop/core/servers/manage/about-using-smscstat.dll-to-create-status-messages.md).  

### Management Point Interface  
 Using the management point interfaces, you can raise status messages that are defined by XML from client computers. The management point interfaces cannot be used by VBScript. Using the management point interface is recommended for raising status messages on client computers that are not running a Windows operating system.  

## Creating Status Messages on the Site Server  
 You raise events on the server by creating instances of `SMS_StatusMessage`. For more information, see [How to Report User-Defined Status Messages](../../../../develop/core/servers/manage/how-to-report-user-defined-status-messages.md).  

## See Also  
 [About Using SMSCSTAT.DLL to Create Status Messages](../../../../develop/core/servers/manage/about-using-smscstat.dll-to-create-status-messages.md)   
 [Configuration Manager Status and Summarizers](../../../../develop/core/servers/manage/configuration-manager-status-and-summarizers.md)   
 [How to Report User-Defined Status Messages](../../../../develop/core/servers/manage/how-to-report-user-defined-status-messages.md)   
 [How to Read User-Defined Status Messages](../../../../develop/core/servers/manage/how-to-read-user-defined-status-messages.md)   
 [SMSEvent Class](../../../../develop/reference/core/servers/manage/smsevent-class.md)
