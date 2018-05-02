---
title: "Features and capabilities"
titleSuffix: "Configuration Manager"
description: "Learn about the primary management capabilities of System Center Configuration Manager."
ms.date: 12/29/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 5d388399-07ca-431c-a9b2-56c69771aa87
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Features and capabilities of System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

The following are the primary management capabilities of System Center Configuration Manager. Each capability has its own prerequisites, and the capabilities that you want to use might influence the design and implementation of your Configuration Manager hierarchy. For example, if you want to deploy software to devices in your hierarchy, you must install the distribution point site system role.  

 For more information about how to plan and install Configuration Manager to support these management capabilities in your environment, see [Get ready for System Center Configuration Manager](../../../core/plan-design/get-ready.md).  

 **Application management**  

 Provides a set of tools and resources that can help you create, manage, deploy, and monitor applications to a range of different devices that you manage. Additionally, Configuration Manager provides you with tools that help you protect your company data in user's apps. See [Introduction to application management](/sccm/apps/understand/introduction-to-application-management).

 **Company resource access**  

 Provides a set of tools and resources that enable you to give users in your organization access to data and applications from remote locations. These tools include Wi-Fi profiles, VPN profiles, certificate profiles, and conditional access to Exchange and SharePoint online. See [Protect data and site infrastructure with System Center Configuration Manager](../../../protect/understand/protect-data-and-site-infrastructure.md) and [Manage access to services in System Center Configuration Manager](../../../protect/deploy-use/manage-access-to-services.md).  

 **Compliance settings**  

 Provides a set of tools and resources that can help you to assess, track, and remediate the configuration compliance of client devices in the enterprise. Additionally, you can use compliance settings to configure a range of features and security settings on devices you manage. See [Ensure device compliance with System Center Configuration Manager](../../../compliance/understand/ensure-device-compliance.md).  

 **Endpoint Protection**  

 Provides security, antimalware, and Windows Firewall management for computers in your enterprise. See [Endpoint Protection in System Center Configuration Manager](../../../protect/deploy-use/endpoint-protection.md).  

 **Inventory**  

 Provides a set of tools to help identify and monitor assets:  

-   **Hardware inventory**: Collects detailed information about the hardware of devices in your enterprise. See [Introduction to hardware inventory in System Center Configuration Manager](../../../core/clients/manage/inventory/introduction-to-hardware-inventory.md).  

-   **Software inventory**: Collects and reports information about the files that are stored on client computers in your organization. See [Introduction to software inventory in System Center Configuration Manager](../../../core/clients/manage/inventory/introduction-to-software-inventory.md).  

-   **Asset Intelligence**: Provides tools to collect inventory data and to monitor software license usage in your enterprise. See [Introduction to Asset Intelligence in System Center Configuration Manager](../../../core/clients/manage/asset-intelligence/introduction-to-asset-intelligence.md).  

**Mobile device management with Microsoft Intune**  

 You can use Configuration Manager to manage iOS, Android (including Samsung KNOX Standard), Windows Phone, and Windows devices by using the Microsoft Intune service over the Internet.

 Although you use the Intune service, management tasks are completed by using the service connection point site system role available through the Configuration Manager console. See [Hybrid mobile device management (MDM) with System Center Configuration Manager and Microsoft Intune](../../../mdm/understand/hybrid-mobile-device-management.md).  

 **On-premises Mobile Device Management**  

 Enrolls and manages PCs and mobile devices by using the on-premises Configuration Manager infrastructure and management functionality built into the device platforms (instead of relying on a separately installed Configuration Manager client). Currently supports managing Windows 10 Enterprise and Windows 10 Mobile devices. See [Manage mobile devices with on-premises infrastructure in System Center Configuration Manager](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

 **Operating system deployment**  

 Provides a tool to create operating system images. You can then use these images to deploy the operating systems to computers, by using PXE boot or bootable media such as a CD set, DVD, or USB flash drives. Note that this applies to computers that are managed by Configuration Manager, as well as unmanaged computers. See [Introduction to operating system deployment in System Center Configuration Manager](../../../osd/understand/introduction-to-operating-system-deployment.md).  

 **Power management**  

 Provides a set of tools and resources that you can use to manage and monitor the power consumption of client computers in the enterprise. See [Introduction to power management in System Center Configuration Manager](../../../core/clients/manage/power/introduction-to-power-management.md).  

 **Queries**  

 Provides a tool to retrieve information about resources in your hierarchy and information about inventory data and status messages. You can then use this information for reporting, or for defining collections of devices or users for software deployment and configuration settings. See [Introduction to queries in System Center Configuration Manager](../../../core/servers/manage/introduction-to-queries.md).  

 **Remote connection profiles**  

 Provides a set of tools and resources to help you to create, deploy, and monitor remote connection settings to devices in your organization. By deploying these settings, you minimize the effort required by users to connect to their computers on the corporate network. See [Working with remote connection profiles in System Center Configuration Manager](/sccm/compliance/deploy-use/create-remote-connection-profiles).  

 **User data and profiles configuration items**  

 User data and profiles configuration items in Configuration Manager contain settings that can manage folder redirection, offline files, and roaming profiles on computers that run Windows 8 and later for users in your hierarchy. See [Working with user data and profiles configuration items in System Center Configuration Manager](/sccm/compliance/deploy-use/create-user-data-and-profiles-configuration-items).  

 **Remote control**  

 Provides tools to remotely administer client computers from the Configuration Manager console. See [Introduction to remote control in System Center Configuration Manager](../../../core/clients/manage/remote-control/introduction-to-remote-control.md).  

 **Reporting**  

 Provides a set of tools and resources that help you use the advanced reporting capabilities of SQL Server Reporting Services from the Configuration Manager console. See [Introduction to reporting in System Center Configuration Manager](../../../core/servers/manage/introduction-to-reporting.md).  

 **Software metering**  

 Provides tools to monitor and collect software usage data from Configuration Manager clients. See [Monitor app usage with software metering in System Center Configuration Manager](../../../apps/deploy-use/monitor-app-usage-with-software-metering.md).  

 **Software updates**  

 Provides a set of tools and resources that can help you manage, deploy, and monitor software updates in the enterprise. See [Introduction to software updates in System Center Configuration Manager](/sccm/sum/understand/software-updates-introduction).  
