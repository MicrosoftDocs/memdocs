---
title: What is Configuration Manager?
titleSuffix: Configuration Manager
description: Learn the basics of Microsoft Endpoint Configuration Manager.
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: overview
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
ms.collection: highpri
---

# What is Configuration Manager?

*Applies to: Configuration Manager (current branch)*

Starting in version 1910, Configuration Manager is now part of Microsoft Endpoint Manager.

![Microsoft Endpoint Configuration Manager](media/4960084-endpoint-manager-logo.png)

Microsoft Endpoint Manager is an integrated solution for managing all of your devices. Microsoft brings together Configuration Manager and Intune, without a complex migration, and with simplified licensing. Continue to leverage your existing Configuration Manager investments, while taking advantage of the power of the Microsoft cloud at your own pace.

The following Microsoft management solutions are all now part of the **Microsoft Endpoint Manager** brand:

- [Configuration Manager](/configmgr)
- [Intune](/intune)
- [Desktop Analytics](../../desktop-analytics/overview.md)
- [Autopilot](/intune/enrollment/enrollment-autopilot)
- Other features in the [Device Management Admin Console](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/microsoft-intune-rolls-out-an-improved-streamlined-endpoint/ba-p/937760)

For more information, see [Microsoft Endpoint Configuration Manager FAQ](microsoft-endpoint-manager-faq.yml).

## Introduction

Use Configuration Manager to help you with the following systems management activities:

- Increase IT productivity and efficiency by reducing manual tasks and letting you focus on high-value projects.  
- Maximize hardware and software investments.  
- Empower user productivity by providing the right software at the right time.  

Configuration Manager helps you deliver more effective IT services by enabling:

- Secure and scalable deployment of applications, software updates, and operating systems.
- Real-time actions on managed devices.
- Cloud-powered analytics and management for on-premises and internet-based devices.
- Compliance settings management.  
- Comprehensive management of servers, desktops, and laptops.

Configuration Manager extends and works alongside many Microsoft technologies and solutions. For example, Configuration Manager integrates with:  

- Microsoft Intune to co-manage a wide variety of mobile device platforms
- Microsoft Azure to host cloud services to extend your management services
- Windows Server Update Services (WSUS) to manage software updates
- Certificate Services
- Exchange Server and Exchange Online
- Group Policy
- DNS
- Windows Automated Deployment Kit (Windows ADK) and the User State Migration Tool (USMT)
- Windows Deployment Services (WDS)
- Remote Desktop and Remote Assistance

Configuration Manager also uses:  

- Active Directory Domain Services and Azure Active Directory for security, service location, configuration, and to discover the users and devices that you want to manage.  
- Microsoft SQL Server as a distributed change management database—and integrates with SQL Server Reporting Services (SSRS) to produce reports to monitor and track management activities.  
- Site system roles that extend management functionality and use the web services of Internet Information Services (IIS).
- Delivery Optimization, Windows Low Extra Delay Background Transport (LEDBAT), Background Intelligent Transfer Service (BITS), BranchCache, and other peer caching technologies to help manage content on your networks and between devices.

To be successful with Configuration Manager in a production environment, thoroughly plan and test the management features. Configuration Manager is a powerful management application, with the potential to affect every computer in your organization. When you deploy and manage Configuration Manager with careful planning and consideration of your business requirements, Configuration Manager can reduce your administrative overhead and total cost of ownership.  

## User interfaces

### <a name="BKMK_Console"></a> The Configuration Manager console

After you install Configuration Manager, use the Configuration Manager console to configure sites and clients, and to run and monitor management tasks. This console is the main point of administration, and lets you manage multiple sites.  

You can install the Configuration Manager console on additional computers, and restrict access and limit what administrative users can see in the console by using Configuration Manager role-based administration.  

For more information, see [Use the Configuration Manager console](../servers/manage/admin-console.md).

### <a name="BKMK_ApplicationCatalog"></a> Software Center

**Software Center** is an application that's installed when you install the Configuration Manager client on a Windows device. Users use Software Center to request and install software that you deploy. Software Center lets users do the following actions:  

- Browse for and install applications, software updates, and new OS versions
- View their software request history
- View device compliance against your organization's policies

You can also show custom tabs in Software Center to meet additional business requirements.

For more information, see the [Software Center user guide](software-center.md).

## Next steps

Before you install Configuration Manager, familiarize yourself with the basic concepts and terms:

- If you're familiar with System Center 2012 Configuration Manager, see [What's changed from System Center 2012 Configuration Manager](../plan-design/changes/what-has-changed-from-configuration-manager-2012.md).

- For a high-level technical overview of Configuration Manager, see [Fundamentals of Configuration Manager](fundamentals.md).

When you're familiar with the basic concepts, use this documentation library to help you successfully deploy and use Configuration Manager. Start with the following articles:

- [Features and capabilities of Configuration Manager](../plan-design/changes/features-and-capabilities.md)  
- [Choose a device management solution](../plan-design/choose-a-device-management-solution.md)  
- [Evaluate Configuration Manager by building your own lab environment](../get-started/set-up-your-lab.md)
- [Find help for using Configuration Manager](find-help.md)