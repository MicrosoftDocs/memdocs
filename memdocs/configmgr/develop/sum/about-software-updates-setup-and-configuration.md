---
title: "Software Updates Setup and Configuration"
description: Before software update compliance assessment data is displayed in the Configuration Manager console and before software updates can be deployed to client computers, you must install and configure a software update point.
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: d8a9e6ba-f91e-4d2b-b215-8e4285f4eed9
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# About Software Updates Setup and Configuration
Before software update compliance assessment data is displayed in the Configuration Manager console and before software updates can be deployed to client computers, you must install and configure a software update point. In addition, consider the configuration and settings for other software updates components, such as the Windows Server Update Services (WSUS) server and the software updates client agent. For more information, see [Windows Server Update Services](/windows-server/administration/windows-server-update-services/get-started/windows-server-update-services-wsus).  

For more information about software updates, see [Deploy and manage software updates](../../sum/understand/software-updates-introduction.md).  

## Software Update Point  
 A software update point in Configuration Manager is a required component of software updates, and after it is installed, the software update point is displayed as a site system role in the Configuration Manager console. The software update point site system role must be created on a site system server that has Windows Server Update Services (WSUS) 3.0 installed.  

## WSUS Server and SSL  
 When a Configuration Manager site server is in native mode, or when the active software update point is configured to use Secure Sockets Layer (SSL), you must configure five virtual roots to use a secured channel on the active software update point server. The virtual roots are located on the Web site that the WSUS server uses, and they are modified by using the Internet Information Services (IIS) Manager. After you have configured the virtual roots, you must run the WSUSUtil tool to let the health monitoring component of WSUS know that it should use SSL.  

## Port Settings Used by WSUS  
 When you create and configure a software update point in Configuration Manager, you must specify the port settings that the WSUS 3.0 server uses.  

## Software Updates Client Agent  
 When the Software Updates Client Agent is enabled in Configuration Manager, it sends a policy to the client computers that are assigned to the site. This policy requests that the software updates components be enabled. The Software Updates Client Agent components work together to perform compliance assessment scans, install software updates at their configured deadline or when they are manually initiated, and reevaluate whether previously installed software updates are still installed, and if not, install them again. The Software Updates Client Agent properties are site-wide client settings.  
