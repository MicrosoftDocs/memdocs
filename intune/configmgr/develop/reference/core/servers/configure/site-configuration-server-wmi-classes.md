---
title: Site Configuration Server WMI Classes
description: The site configuration server WMI classes in Configuration Manager relate to an installation that consists of one or more computers running the Configuration Manager components.
titleSuffix: Configuration Manager
ms.date: 03/13/2017
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: fac9263e-4e47-4e15-b07a-27a39c9ecd74
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Site configuration server WMI classes

This section contains detailed reference information about the site configuration server WMI classes in Configuration Manager. These classes include classes that relate to an installation of Configuration Manager that consists of one or more computers running the Configuration Manager components.  

You can configure the components of a site at any time to enhance the management of your site. Configuration information is contained in the install map and the site control file.  

When you install Configuration Manager, it creates an install map that describes the initial configuration of the installed features for the server, client, and Configuration Manager console. The install map configuration data is read-only and uses the following classes:  

- [SMS_SiteInstallMap Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteinstallmap-server-wmi-class.md)  

- [SMS_SiteInstallItemBase Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteinstallitembase-server-wmi-class.md)  

- [SMS_SiteInstallItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_siteinstallitem-server-wmi-class.md)  

- [SMS_SystemResourceList Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_systemresourcelist-server-wmi-class.md)  

Classes that are derived from `SMS_SiteInstallItem` use the naming convention `SMS_SII_*`**.** Classes that are derived from `SMS_SiteInstallItemBase` use the naming convention `SMS_SIIB_*`.  

The site control file describes the current configuration of the site and its components. Use the following classes to manage the site control file and the site configuration data:  

- [SMS_SiteControlFile Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolfile-server-wmi-class.md)  

- [SMS_SiteControlItem Server WMI Class](../../../../../develop/reference/core/servers/configure/sms_sitecontrolitem-server-wmi-class.md)  

Classes that are derived from `SMS_SiteControlItem` use the naming convention `SMS_SCI_*`. Use these classes to access and modify the configuration items that are contained in the site control file. For information about managing the site control file and changing component configuration, see [About the site control file](../../../../core/understand/about-the-configuration-manager-site-control-file.md).  
