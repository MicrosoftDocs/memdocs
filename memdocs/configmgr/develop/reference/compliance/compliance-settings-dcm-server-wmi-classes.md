---
title: Compliance settings classes
titleSuffix: Configuration Manager
ms.date: 08/02/2019
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: reference
ms.assetid: 4dbfce7f-1b58-4998-9b38-f5f3c3ba77c6
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---

# About compliance settings server WMI classes

In Configuration Manager, compliance settings server WMI classes assist you in assessing computer compliance. You can consider a number of configurations, for example, installation and configuration of the correct versions of Windows operating systems. You can also use these classes to check for compliance with software updates and security settings.  

The main classes supporting the compliance settings feature are:  

- [SMS_ConfigurationItem server WMI class](sms_configurationitem-server-wmi-class.md), representing a generic configuration item.  

- [SMS_ConfigurationBaselineInfo server WMI class](sms_configurationbaselineinfo-server-wmi-class.md), representing information for a baseline configuration item.  

- [SMS_BaselineAssignment server WMI class](sms_baselineassignment-server-wmi-class.md), representing an assignment of a baseline configuration item.  

For more information, see [About configuration baselines and configuration items](../../compliance/about-configuration-baselines-and-configuration-items.md).  

> [!NOTE]
> Some of the classes for compliance settings, for example, [SMS_ConfigurationBaselineInfo server WMI class](sms_configurationbaselineinfo-server-wmi-class.md), are specific to baseline configuration items. Some of the classes can also be used to reference software update configuration items, although applications use the software updates feature to manipulate these items. For more information, see [About software update deployments](../../sum/about-software-updates-deployments.md).  

The Configuration Manager server class schema is a set of WMI classes that represent the objects on a server running Configuration Manager. Each Configuration Manager class is a template for a managed object and all instances of the object use the template. Classes can contain properties and methods. The properties describe the class data, and the methods typically perform data management. For more information about developing applications using these classes, see [About Configuration Manager SDK requirements](../../core/reqs/about-configuration-manager-sdk-requirements.md).  
