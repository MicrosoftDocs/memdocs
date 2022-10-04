---
title: Security and privacy for compliance settings
titleSuffix: Configuration Manager
description: Learn about the security guidance and recommendations for compliance settings in Configuration Manager.
ms.date: 05/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
author: sheetg09
manager: apoorvseth
ms.author: sheetg
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Security and privacy for compliance settings in Configuration Manager

*Applies to: Configuration Manager (current branch)*

## Security guidance

### Don't monitor sensitive data

To help avoid information disclosure, don't configure configuration items to monitor potentially sensitive information.

### Don't configure compliance rules that use data that can be modified by end users

If you create a compliance rule based on data that users can modify, such as registry settings for configuration choices, the compliance results won't be reliable.

### Only import configuration packs from external sources that are digitally signed

Import configuration packs and other configuration data from external sources only if they have a valid digital signature from a trusted publisher.

Published configuration data can be digitally signed so that you can verify the publishing source and make sure that the data hasn't been tampered with. If the digital signature verification check fails, you're warned and prompted to continue with the import. If you can't verify the source and integrity of the data, don't import unsigned data.

### Implement access controls to protect reference computers

Make sure that when an administrative user configures a registry or file system setting by browsing to a reference computer, the reference computer isn't compromised.

### Secure the communication channel when you browse to a reference computer

To prevent tampering of the data when it's transferred over the network, use internet protocol security (IPsec) or server message block (SMB) signing between the computer that runs the Configuration Manager console and the reference computer.

### Restrict and monitor role-based administration for compliance settings

Restrict and monitor the administrative users who are granted the **Compliance Settings Manager** role-based security role.

Administrative users with this role can deploy configuration items to all devices and all users in the hierarchy. Configuration items are powerful and can include, for example, scripts and registry reconfiguration.

## Privacy information

You can use compliance settings to evaluate whether your client devices are compliant with configuration items that you deploy in configuration baselines. Some settings can be automatically remediated if they out of compliance. Compliance information is sent to the site server by the management point and stored in the site database. The information is encrypted when devices send it to the management point, but not stored in encrypted format in the site database. Compliance information isn't sent to Microsoft.

By default, devices don't evaluate compliance settings. You configure the configuration items and configuration baselines, and then deploy them to devices.
