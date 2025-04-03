---
title: Client management fundamentals
titleSuffix: Configuration Manager
description: Learn about tasks that you run to manage Configuration Manager clients.
ms.date: 12/30/2016
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: article
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Fundamentals of client management tasks for Configuration Manager

*Applies to: Configuration Manager (current branch)*

After you install the Configuration Manager clients, there are several tasks that you run to manage the clients.  Some of the tasks are run from the Configuration Manager console. Other tasks are run from the Configuration Manager client application. The Configuration Manager client application is installed with the Configuration Manager client software.

## Configuration Manager console tasks
 In the Configuration Manager console, you can perform various client management tasks:  

-   Deploy applications, software updates, maintenance scripts, and operating systems. Configure installation for a specific date and time, make the software available for users to install when they are requested, or configure applications to be uninstalled.  

-   Help protect computers from malware and security threats, and notify you when problems are detected.  

-   Define client configuration settings that you want to monitor, and remediate if they are out of compliance.  

-   Collect hardware and software inventory information, which includes monitoring and reconciling license information from Microsoft.  

-   Troubleshoot computers by using remote control.  

-   Implement power management settings to manage and monitor the power consumption of computers.  

The Configuration Manager console monitors the previous tasks in near real time. Notification and status information for each task is available in the Configuration Manager console. To capture data and historical trending, use the integrated reporting capabilities of SQL Server Reporting Services. Clients submit details to the site as client status.  Client status information provides data about the health of the client and client activity, and is viewed in the console or by using the built-in reports for Configuration Manager. This data helps identify computers that are not responding and in some cases, problems are automatically remediated.  

For more information about management tasks for clients, see [How to manage clients](../../core/clients/manage/manage-clients.md). To learn about using reports, see [Introduction to reporting](../../core/servers/manage/introduction-to-reporting.md).

## Configuration Manager client application  
 When you install the Configuration Manager client software, the Configuration Manager client application is installed too. Unlike Software Center, the Configuration Manager client application is designed for the help desk rather than for the end user. Some configuration options require local administrative permissions, and most options require technical knowledge about how the Configuration Manager client application works. You can use this application to perform the following tasks on a client:  

-   View properties about the client, such as the build number, its assigned site, the management point it is communicating with, and whether the client is using a public key infrastructure (PKI) certificate or a self-signed certificate.  

-   Confirm that the client has successfully downloaded a client policy after the client is installed for the first time. Also confirm that the client settings are enabled or disabled as expected, according to the client settings that are configured in the Configuration Manager console.  

-   Start client actions. For example, download the client policy if there was a recent configuration change in the Configuration Manager console, and you do not want to wait until the next scheduled time.  

-   Manually assign a client to a Configuration Manager site or try to find a site. Then specify the Domain Name System (DNS) suffix for management points that publish to DNS.  

-   Configure the client cache that temporarily stores files. Then delete files in the cache if you require more disk space to install software.  

-   Configure settings for Internet-based client management.  

-   View configuration baselines that were deployed to the client, initiate compliance evaluation, and view compliance reports.  
