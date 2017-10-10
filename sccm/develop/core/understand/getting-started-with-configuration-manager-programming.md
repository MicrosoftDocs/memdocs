---
title: "Configuration Manager Programming"
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
ms.assetid: 7dc6cb76-469e-4e4f-b79b-bb391fd4e758searchScope: - ConfigMgr SDK
caps.latest.revision: 16
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# Getting Started with Configuration Manager Programming
To get started with programming for System Center Configuration Manager, it’s beneficial to have a basic functional and architectural understanding of Configuration Manager. In addition, there are a number of key tools and resources that critical to validating and troubleshooting solutions. Below are tips and resources for someone new to programming for Configuration Manager.  

> [!IMPORTANT]
>  You should recognize that Configuration Manager, previously Systems Management Server (SMS), has quite a long history as a product. In reviewing namespaces, classes, methods, properties and log files you’ll find many references containing "SMS" – in fact, most WMI classes start with "SMS_" and the primary Configuration Manager WMI namespace is "SMS". Over the course of years, numerous legacy classes, methods and properties have accumulated – not apparent to an administrative user, but when programming the history/legacy can be confusing.  

## Functional Understanding  
 To successfully automate or extend Configuration Manager, it is incredibly important to gain a functional understanding of the product. Configuration Manager is multi-tiered, distributed management system, most often spread over numerous servers and numerous locations. See the below resources, for functional information on Configuration Manager.  

-   [Documentation for System Center Configuration Manager](https://technet.microsoft.com/en-us/library/mt346023.aspx)  

-   [Fundamentals of System Center Configuration Manager](https://technet.microsoft.com/en-us/library/mt622643.aspx)  

-   [TechNet Virtual Labs](http://go.microsoft.com/fwlink/?LinkId=329809) (See: Virtual Lab: Introduction to Configuration Manager 2012 SP1)  

### More Resources  
 **Books:** There are numerous books available for Configuration Manager. A few example books are listed below.  

-   [System Center 2012 Configuration Manager: Mastering the Fundamentals](http://www.amazon.com/System-Center-2012-Configuration-Manager/dp/9197939048)  

-   [System Center 2012 Configuration Manager (SCCM) Unleashed](http://www.amazon.com/System-Center-Configuration-Manager-Unleashed/dp/0672334372/ref=sr_1_1?s=books&ie=UTF8&qid=1382812114&sr=1-1&keywords=System+Center+2012+Configuration+Manager+%28SCCM%29+Unleashed)  

-   [Microsoft System Center 2012 Configuration Manager: Administration Cookbook](http://www.amazon.com/Microsoft-System-Center-Configuration-Manager/dp/1849684944/ref=sr_1_1?s=books&ie=UTF8&qid=1382812164&sr=1-1&keywords=Microsoft+System+Center+2012+Configuration+Manager%3A+Administration+Cookbook)  

 **Videos:** There are numerous videos available for Configuration Manager. A few example videos are listed below.  

-   [Channel 9: Microsoft System Center 2012 Configuration Manager Overview](http://channel9.msdn.com/Events/TechEd/NorthAmerica/2012/MGT309)  

-   [Vimeo: Configuration Manager 2012 &#124; Windows 8 & SP1 Features – Wally Mead](http://vimeo.com/55952501)  

-   [YouTube: Technical Deep Dive: System Center Configuration Manager 2012 Technical Overview](http://www.youtube.com/watch?v=qLACm3910_A)  

 **Forums:** There are numerous forums available for Configuration Manager. A few example forums are listed below.  

-   [TechNet: Configuration Manager 2012 - General](http://social.technet.microsoft.com/Forums/home?forum=configmanagergeneral)  

-   [windows-noob.com: Configuration Manager 2012](http://www.windows-noob.com/forums/index.php?/forum/92-setup-sccm-2012/)  

## Architectural Understanding  
 Configuration Manager is multi-tiered, distributed management system. It’s important to understand the general architecture of Configuration Manager. Below is a link to an overview of the Configuration Manager architecture.  

-   [Architectural Overview](../../../develop/core/understand/architectural-overview.md)  

 In addition to the architectural information, there are several key points that commonly confuse administrators and programmers new to Configuration Manager.  

-   **Server:** In a general sense, most programming actions (in particular, automation) take place on a Configuration Manager site server. Actions or configuration changes are propagated throughout the Configuration Manager hierarchy to the clients via policy. Policy is pulled down by the client on a configurable polling interval **NOT** pushed immediately to the client by the server. In general, once a client is installed, there is no direct communication from the site server to the client or the client to the site server – all communication takes place through intermediary server roles.  

-   **Client:**  Configuration Manager clients are systems and devices managed by Configuration Manager. A ‘server’ can be a Configuration Manger client. So, an Exchange Server, an Active Directory Server and Configuration Manager Server can all be Configuration Manager clients – if they are managed by Configuration Manager. In addition, Windows 8.1, Windows Phone and an iPhone can all be Configuration Manager clients – if they are managed by Configuration Manager.  

     Configuration Manager clients receive policy by periodically polling a Configuration Manager Management Point. The polling interval for retrieving basic policy is configurable, as are other settings. Because of this, there are inherent delays in client targeted actions initiated from the Configuration Manager site server.  

-   **Console:** Remote Configuration Manager console binaries and files are not automatically updated when changes are made on the site server. Modifications and extensions must be copied to systems running the Configuration Manager console, either manually or using Configuration Manager Application Management/Software Distribution.  

-   **SMS Provider vs SQL Server:** Although Configuration Manager leverages SQL Server for data storage, SQL Server is **NOT** the primary programming interface to Configuration Manager. The primary programming interface to Configuration Manager is the SMS Provider (WMI) - object creation and modification **must** be done via the SMS Provider. You should consider SQL Server as providing read-only access to Configuration Manager data for querying and reporting purposes. This is not a matter of permissions, rather matter of maintaining data integrity.  

## Namespaces and Classes  

### Server  
 **Primary WMI Namespace:** ROOT\SMS\SITE_\<site code>  

 **Server WMI Classes:** [Configuration Manager Reference](../../../develop/reference/configuration-manager-reference.md)  

### Client  
 **Primary WMI Namespace:** ROOT\CCM  

 **Client WMI Classes:** [Configuration Manager Client SDK WMI Classes](../../../develop/reference/core/clients/sdk/client-sdk-wmi-classes.md)  

> [!IMPORTANT]
>  The client-side programming story for Configuration Manager is evolving to be primarily WMI-based. In the past, a set of client-side COM classes were the primary method used to access client functionality, although additional client-side WMI classes/methods were also used. With the release of System Center 2012 Configuration Manager, the focus is shifting to a set of WMI classes in the namespace: **root/ccm/ClientSDK**. Understandably, an abstraction, in the form of COM or specific SDK classes, provides a useful abstraction from underlying architectural changes over the course of product updates.  

### Console  
 **Console-related Managed Classes:**  

-   Microsoft.configurationmanagement.exe  

-   Microsoft.configurationmanagement.managementprovider.dll  

-   Microsoft.ConfigurationManagement.DialogFoundation.dll  

-   AdminUI.DialogFoundation.dll  

 **Introductory Configuration Manager Console topics:**  

-   [About Configuration Manager Console Extension](../../../develop/core/servers/console/about-configuration-manager-console-extension.md)  

-   [Configuration Manager Console Extension Architecture](../../../develop/core/servers/console/console-extension-architecture.md)  

## Programming Fundamentals  
 The Configuration Manager Programming Fundamentals section of the SDK provides examples of how to work with the various types of objects and structures available in Configuration Manager. Configuration Manager contains some objects/concepts that can be initially confusing. Of particular interest are **embedded properties** (used primary with the Site Control File) and **lazy properties** (used throughout the Configuration Manager classes). Below are links to the Programming Fundamentals (and other sub-sections) of the SDK. These sections contain code examples showing how to work with the various object types.  

> [!IMPORTANT]
>  The SDK most often provides code examples in VBScript and C#. This does not mean that other languages will not work with the SMS Provider. The SMS Provider is language agnostic, as long as the correct objects and constructs can be exchanged. Use the language (tool) that is most appropriate for your environment. C# is used internally as a baseline for testing the SDK code snippets, so examples of object manipulation and code constructs will most often be provided in C#. If you use another language, you should be comfortable translating from C# to your language of choice.  

-   [Configuration Manager Programming Fundamentals](../../../develop/core/understand/configuration-manager-programming-fundamentals.md)  

-   [SMS Provider in Configuration Manager](../../../develop/core/understand/sms-provider-in-configuration-manager.md)  

-   [Configuration Manager Objects](../../../develop/core/understand/configuration-manager-objects.md)  

-   [Configuration Manager Site Control File](../../../develop/core/understand/site-control-file.md)  

-   [Configuration Manager Errors](../../../develop/core/understand/configuration-manager-errors.md)  

## Basic Tools  

### WBEMTEST  
 If you spend much time around Configuration Manager you become aware that much of it runs through WMI.  WMI is "Windows Management Instrumentation" and is Microsoft’s implementation of an Internet standard called Web Based Enterprise Management (WBEM). There are many WMI tools out there.  However, WBEMTEST is immediately available on most systems, rather than having to be downloaded first. You might think of it like Notepad.exe – there are text editors with richer capabilities available, but Notepad.exe is always there when you need to view or create a text file.  

-   [Introduction to WBEMTEST](../../../develop/core/understand/introduction-to-wbemtest.md)  

> [!TIP]
>  Internally, the most commonly used tool when troubleshooting SMS Provider related issues (object creation, modification and deletion) is WBEMTEST.  

### CMTrace  
 **CMTrace:** CMTrace is a customized log file viewer that is useful in monitoring and troubleshooting Configuration Manager. CMTrace provides a continuous view of the log file changes (rather than having to reload to monitor logged activity) and is particularly useful when monitoring/troubleshooting object creation or modification via the SMS Provider (see the SMSProv.log below).  

 CMTrace can be found on the Configuration Manager site server, under the "\<Configuration Manager Installation Directory>\tools\" folder.  

 **SMSProv.log:** SMS Provider log file (\<Configuration Manager Installation Directory>\Logs\SMSProv.log) logs the activity of the SMS Provider and provides low-level information that is useful to monitor/troubleshoot issues when programmatically creating or modifying Configuration Manager objects via the SMS Provider.  

### Client Spy and Policy Spy  
 **Client Spy:** A tool that helps you troubleshoot issues related to software distribution, inventory, and software metering on System Center 2012 Configuration Manager clients.  

 **Policy Spy:** A policy viewer that helps you review and troubleshoot the policy system on System Center 2012 Configuration Manager clients.  

 Client Spy and Policy Spy are both tools contained in the [System Center 2012 Configuration Manager Toolkit](http://www.microsoft.com/download/details.aspx?id=29265)  

## Basic Configuration Manager Program Example  
 Below is link to a very simple Configuration Manager program showing some basic operations common to many Configuration Manager programs:  

-   `Connect` to the SMS Provider  

-   `List` all programs  

-   **Create** a new program  

-   **Modify** an existing program  

-   **Delete** an existing program  

-   [Simple Example of List, Create, Modify, and Delete](../../../develop/core/understand/simple-example-of-list--create--modify--and-delete.md)
