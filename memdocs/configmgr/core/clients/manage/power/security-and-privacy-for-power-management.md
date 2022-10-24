---
title: Security and privacy for power management
titleSuffix: Configuration Manager
description: Get security and privacy information for power management in Configuration Manager.
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
author: sheetg09
manager: apoorvseth
ms.author: sheetg
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Security and privacy for power management in Configuration Manager

*Applies to: Configuration Manager (current branch)*

This section contains security and privacy information for power management in Configuration Manager.  

## Security best practices for power management  
 There are no security-related best practices for power management.  

## Privacy information for power management  
 Power management uses features that are built into Windows to monitor power usage and to apply power settings to computers during business hours and nonbusiness hours. Configuration Manager collects power usage information from computers, which includes data about when a user is using a computer. Although Configuration Manager monitors power usage for a collection rather than for each computer, a collection can contain just one computer. Power management is not enabled by default and must be configured by an administrator.  

 The power usage information is stored in the Configuration Manager database and is not sent to Microsoft. Detailed information is retained in the database for 31 days and summarized information is retained for 13 months. You cannot configure the deletion interval.  

 Before you configure power management, consider your privacy requirements.  
