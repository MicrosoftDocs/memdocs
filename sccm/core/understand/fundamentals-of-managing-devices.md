---
title: "Fundamentals of managing devices | System Center Configuration Manager"
ms.custom: na
ms.date: 04/18/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2bca3db9-115a-451d-8c93-f073ceefe0c7
caps.latest.revision: 6
author: Mtillman

---
# Fundamentals of managing devices with System Center Configuration Manager
System Center Configuration Manager can manage two broad categories of devices.

The first, **clients** are devices such as workstations, laptops, servers, and mobile devices that have the Configuration Manager client software installed so that you can manage them.   

The second, **managed devices** can include clients, but typically means mobile devices that do not install the Configuration Manager client software and that you manage by using Microsoft Intune or by using Configuration Manager's built-in on-premises mobile device management.

In addition to managing devices with or without the Configuration Manager client, you can use user-centric management to help group and identify the devices you manage.

## Managing devices with the Configuration Manager client

 Management of clients includes operations like collecting inventory for hardware or software from devices, installing new software on a device, or defining settings that report on or enforce compliance to a specific configuration. Some management functions, like hardware inventory, require the device to run the configuration manager client software. Other operations, like installing (deploying) software to a device are supported for all managed devices.  

 To manage a device using the Configuration Manager client software, you must either discovery the device on your network and then deploy (install) the client software to that device, or  manually install the client software on a new computer and then have that computer join your site when it joins your network. To discover devices that do not yet have client software installed you run one or more of the built-in discovery methods. After a device is discovered, you can then use one of several methods to get the client software installed. For information on using discovery, see [Run discovery for System Center Configuration Manager](../../core/servers/deploy/configure/run-discovery.md).  

 After discovering devices that are supported to run the Configuration Manager client software, you can use one of several methods to get the software installed. After the software is installed and the client is assigned to a primary site, you can begin to manage the device.  Common installation methods include 'Client push installation', 'software update-based installation, using Group Policy,  manual installation on a computer, or including the client as part of an operating system image you deploy.  

 After the client is installed, you can simplify the tasks of managing devices by using collections. Collections are logical groups of devices or users that you create so that you can perform management tasks on multiple devices that share a common set of criteria. For example, you might want to install a mobile device application on all mobile devices that are enrolled by Configuration Manager. If this is the case, you could use the **All Mobile Devices** collection, which automatically excludes computers. You can create your own collections to logically group the devices that you manage, according to your business requirements.  

 For more information,  see the following topics:  

-   [Choose a device management solution for System Center Configuration Manager](../../core/plan-design/choose-a-device-management-solution.md)  

-   [Client installation methods in System Center Configuration Manager](../../core/clients/deploy/plan/client-installation-methods.md)  

-   [Introduction to collections in System Center Configuration Manager](../../core/clients/manage/collections/introduction-to-collections.md)  

### Client settings  
 When you first install Configuration Manager, all clients in the hierarchy are configured by using default client settings that you can change. These client settings include configuration options like how  frequently devices communicate with the site, whether the client is enabled for software updates and other management operations, or whether users can enroll their mobile devices to be managed by Configuration Manager.  

 If you need different client settings for groups of users or devices, you can create custom client settings and then assign them to collections.  Members of the collection are configured to have the custom settings and you can create multiple custom client settings that are applied in the order that you specify (by numerical order).  If there are conflicting settings, the setting that has the lowest order number overrides the other settings.  

 The following diagram shows an example of how you could create and apply custom client settings.  

 ![ClientSettings](../../core/understand/media/ClientSettings.gif "ClientSettings")  

 To learn more about client settings, see  
                [How to configure client settings in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md) and  [About client settings in System Center Configuration Manager](../../core/clients/deploy/about-client-settings.md).

## Managing devices without the Configuration Manager client  
 Configuration Manager supports managing some devices that have not installed the client software and that are not managed by interoperating with Microsoft Intune. For more information see [Manage mobile devices with on-premises infrastructure in System Center Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) and  [Manage mobile devices with System Center Configuration Manager and Exchange](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).  

## User-centric management  
 In addition to the collections for devices, there are also user collections that contain users from Active Directory Domain Services. When you use a user collection, you can install software on all computers that members of the collection log into, and configure **user device affinity** so that the software you deploy  installs on only the devices that are specified as a users main device. These main devices are called primary devices. A user can have one or more primary devices.  

 One of the ways in which users can control their software deployment experience is by using the computer client interface, **Software Center**. Software Center is automatically installed on client computers and accessed from the users' Start menu. The Software Center lets users manage their own software, as well as perform the following:  

-   Install software  

-   Schedule software to automatically install outside working hours  

-   Configure when Configuration Manager can install software on their device  

-   Configure access settings for remote control, if remote control is enabled in Configuration Manager  

-   Configure options for power management if an administrative user has enabled this  

 A link in Software Center lets users connect to the **Application Catalog**, where they can browse for, install, and request software. In addition,  the Application Catalog lets users configure some preference settings,  wipe their mobile devices, and (when you allow this configuration) specify their own primary devices for user device affinity. (Other methods of configuring the user device affinity information include importing the information from a file and automatic generation from usage data.)  

 Because Application Catalog is a website that is hosted in IIS, users can also access the Application Catalog directly from a browser, from the intranet, or from the Internet.  
