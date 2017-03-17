---
title: "Create Android applications | Microsoft Docs"
description: "See which considerations you must take into account when you create and deploy applications for Android devices."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e025c48c-1514-4ab7-836c-e0635aaa993a
caps.latest.revision: 6
author: robstackmsft
ms.author: robstack
manager: angrobe
---
# Create Android applications with System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

A System Center Configuration Manager application has one or more deployment types that comprise the installation files and information that are required to deploy software to a device. A deployment type also has rules that specify when and how the software is deployed.  

 You can create applications by using the following methods:  

-   Automatically create the application and deployment types by reading the application installation files.  

-   Manually create the application and then add deployment types later.  

-   Import an application from a file.  

See [Start the create application wizard](../../apps/deploy-use/create-applications.md#start-the-create-application-wizard) for the steps required to create Configuration Manager applications and deployment types. Also, keep the following considerations in mind  when you create and deploy applications for Android devices.  

## General considerations

Configuration Manager supports the deployment of the following app types for Android:

|Device type|Supported files|
|-|-|
|Android|.apk|

The following deployment actions are supported:

|Device type|Supported actions|
|-|-|
|Android|**Available**, **Required**. The user must consent to both installation and uninstallation.
