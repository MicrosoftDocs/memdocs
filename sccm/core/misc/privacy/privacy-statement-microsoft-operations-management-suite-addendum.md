---
title: "Privacy statement - OMS addendum"
titleSuffix: "Configuration Manager"
ms.custom: na
ms.date: 11/06/2016
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aa91afee-45b5-46eb-ad8a-e9c7d3122b38
caps.latest.revision: 4
author: aaroncz
ms.author: aaroncz
manager: angrobe
---
# System Center Configuration Manager privacy statement - Microsoft Operations Management Suite addendum

*Applies to: System Center Configuration Manager (Current Branch)*

This privacy statement should be read in conjunction with the [System Center Configuration Manager privacy statement](https://www.microsoft.com/en-us/privacystatement/SystemCenterConfigurationManager/Default.aspx) as the provisions in that document are applicable. This privacy statement covers the features for the Microsoft Operations Management Suite Connector within System Center Configuration Manager. This disclosure focuses on high-level aspects of the Connector, and is not intended to be an exhaustive list.

### **What this feature does:**
The Microsoft Operations Management Suite Connector syncs data such as collections from System Center Configuration Manager to Microsoft Operations Management Suite. Collections are used in System Center Configuration Manager to organize resources into manageable units. This enables system administrators to create an organized structure that can be used to perform various management tasks on multiple resources, such as computers and servers, at one time.

### Information collected, processed, or transmitted:
The Microsoft Azure subscription ID and secret key are stored in the Configuration Manager database when an administrator configures the feature. Both the Azure Active Directory client secret and the Microsoft Operations Management Suite workspace shared key are stored in the on-premise System Center Configuration Manager database.

During configuration, a list of collections within System Center Configuration Manager appears. The administrator can select from these collections to allow them to be monitored from Microsoft Operations Management Suite. All communications between System Center Configuration Manager and Microsoft Operations Management Suite use HTTPS. No additional information about the collections are provided to Microsoft outside of randomized telemetry data. For details about what information is collected by Microsoft Operations Management Suite, see more [here about log analytics data security](https://azure.microsoft.com/en-us/documentation/articles/log-analytics-security/).

### Choice/control:
It is your choice to use the Microsoft Operations Management Suite Connector. This feature is not enabled by default, and requires the use of Microsoft web-based services. Additionally, the administrator is able to select which collections are synced, and can be terminated at any time. This will remove all synced data from Microsoft Operations Management Suite.
