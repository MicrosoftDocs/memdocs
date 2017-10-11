---
title: "Get started with compliance settings"
titleSuffix: "Configuration Manager"
description: "Learn how compliance settings work in System Center Configuration Manager. Also learn about core concepts that you need to know."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: a2742d52-851e-4abc-b623-d12d91684c0b
caps.latest.revision: 11
author: andredm7ms.author: andredmmanager: angrobe

---
# Get started with compliance settings in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
Before you start to create System Center Configuration Manager configuration items, you should review this topic to understand how compliance settings work, and to learn about the core concepts you'll need to know.  

## How compliance settings works  
 Compliance settings let you manage the configuration and compliance of servers, laptops, desktop computers, and mobile devices in your organization.  

 Configuration items fall into two main categories:  

-   **Settings for devices that are managed with the Configuration Manager client** - typically devices on which you've installed Configuration Manager client software to let you manage the device.  

-   **Settings for devices that are managed without the Configuration Manager client** - typically devices that are managed with Microsoft Intune, or with Configuration Manager on-premises device management.  

## What devices are supported?  


|Device type|More information|  
|------------|----------------------|  
|Windows PCs (with the Configuration Manager client)|Allows you to create custom configuration items that let you assess items such as registry keys, files, and Active Directory attributes.<br /><br /> When you use the Windows 10 configuration item type, you select the settings you want from a predefined list.|  
|Windows PCs (enrolled with Microsoft Intune)|Select the settings you want from a predefined list.|  
|iOS devices (enrolled with Microsoft Intune)|Select the settings you want from a predefined list.|  
|Android devices (enrolled with Microsoft Intune)|Select the settings you want from a predefined list.|  
|Windows Phone devices (enrolled with Microsoft Intune)|Select the settings you want from a predefined list.|  
|Mac computers (with the Configuration Manager client)|Allows you to create custom configuration items that let you assess items such as Mac OS X preferences (property list) values, and the results returned by a script.|  
|Mac computers (enrolled with Microsoft Intune)|Select the settings you want from a predefined list.|  

## What is a configuration item?  
 A configuration item can be thought of as a container that stores the following information (the information you configure will depend on the configuration item type:  

-   **Detection method information** (for Windows configuration items that contain application settings only) - Lets you detect whether an application is installed by detecting the Windows installer file for the application, or by using a custom script.  

-   **Settings** - Settings represent the business or technical conditions that are used to assess compliance on client devices. You can configure a new setting or browse to an existing setting on a reference computer.  

-   **Compliance rules** - Compliance rules specify the conditions that define the compliance of a configuration item setting. Before a setting can be evaluated for compliance, it must have at least one compliance rule. Some settings let you remediate values that are found to be noncompliant. You can create new rules or browse to an existing setting in any configuration item to select rules in it.  

-   **Supported platforms** - These are the device platforms you define on which the configuration item will be evaluated for compliance. If you deploy a configuration item to a device that is not in the supported platforms list, it will not be evaluated for compliance.  

## What is a configuration baseline?  
 Compliance is evaluated by defining a configuration baseline that contains the configuration items that you want to evaluate and settings and rules that describe the level of compliance you must have. You can import this configuration data from the web in Microsoft System Center Configuration Manager Configuration Packs as best practices that are defined by Microsoft and other vendors, in Configuration Manager, and that you then import into Configuration Manager. Or, you can create new configuration items and configuration baselines.  

 After a configuration baseline is defined, you can deploy it to users and devices through collections and evaluate its settings for compliance on a schedule. Devices can have multiple configuration baselines deployed to them. This provides you with a high level of control.  

 Client devices evaluate their compliance against each deployed configuration baseline and immediately report the results to the site by using state messages and status messages. If a client device is currently not connected to the network, but has downloaded the configuration items that are referenced in a deployed configuration baseline, the configuration baseline is evaluated for compliance. The compliance information is sent on reconnection.  

 You can monitor the results of the configuration baseline evaluation compliance from the **Deployments** node in the **Monitoring** workspace in the Configuration Manager console to view the most common causes of noncompliance, errors, and the number of users and devices that are affected. You can also run compliance settings reports to find additional details, such as which devices are compliant or noncompliant, and which element of the configuration baseline is causing a computer to be noncompliant. You can also view compliance evaluation results from Windows computers running the Configuration Manager client software by using the **Configurations** tab in **Configuration Manager** in Control Panel.  

## User data and profiles configuration items  
 User data and profiles configuration items contain settings that control how users in your hierarchy manage folder redirection, offline files, and roaming profiles on computers that run Windows 8 and later. You can deploy them to collections of users and then monitor their compliance from the **Monitoring** node of the Configuration Manager console. Unlike other configuration items, you do not add these to configuration baselines before you deploy them. You can deploy them directly with the **Deploy User Data and Profiles Configuration Item** dialog box.  

 For details, see [Create user data and profiles configuration items](/sccm/compliance/deploy-use/create-user-data-and-profiles-configuration-items).  

## Remote connection profiles  
 Remote connection profiles provide a set of tools and resources to help you create, deploy, and monitor remote connection settings to devices in your organization. By deploying these settings, you minimize the effort that end users require to connect to their computers on the corporate network.  

For details, see [Create remote connection profiles](/sccm/compliance/deploy-use/create-remote-connection-profiles).  

## Windows edition upgrade
The Edition Upgrade Policy lets you automatically upgrade devices that run certain versions of Windows 10 to a newer edition by supplying a new product key or license file.

For details, see [Upgrade Windows devices with the edition upgrade policy](/sccm/compliance/deploy-use/upgrade-windows-version)
