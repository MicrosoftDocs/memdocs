---
title: "Choose Intune standalone or hybrid MDM | Microsoft Docs"
description: "Choose whether to deploy hybrid mobile device management with Intune and Configuration Manager or run Intune standalone."
ms.custom: na
ms.date: 11/07/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 73ff9bb9-e605-4b68-92a1-487684fed42d
caps.latest.revision: 10
author: Mtillman
ms.author: mtillman
manager: angrobe
---
# Choose between Microsoft Intune standalone and hybrid mobile device management with System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

One of the most commonly asked questions regarding mobile device management (MDM) with Microsoft Intune is "Should I integrate Intune with Configuration Manager (hybrid MDM) or run Intune standalone in the cloud only configuration?" To answer that questions, you should carefully compare the two options and consider updates coming in early 2017 to Intune standalone.

## What is Intune standalone?

Intune standalone is a cloud-only MDM solution that involves no on-premises resources and is managed using a web console that can be accessed from anywhere in the world. Intune datacenters are hosted in North America, Europe, and Asia. Because Intune is a cloud service, you can deploy Intune management to your devices in a relatively short timeframe. You may also choose Intune standalone if your organization is moving to the cloud.

## What is hybrid MDM with Configuration Manager?

Hybrid MDM is a solution that uses Intune as the delivery channel for policies, profiles, and applications to devices but uses Configuration Manager on-premises infrastructure to store and administer content and manage the devices. You may choose hybrid MDM if you already have a significant investment in Configuration Manager and want to extend it to manage mobile devices. A hybrid implementation gives you “single pane of glass” control, which means you can use the same on-premises infrastructure and administrative console to manage mobile devices with Intune as well as PCs and servers with the traditional Configuration Manager client.

## What’s coming to Intune standalone in early 2017

If you are choosing between standalone and hybrid, you should take into consideration features that are coming to Intune standalone in early 2017. Today, hybrid MDM has several advanced features that have historically been why some customers choose to manage their devices with hybrid MDM instead of Intune standalone:

-   Programmatic access (API) – SDK and PowerShell management options.

-   Custom reporting – create customized reports.

-   Role-based Access Control – restrict access to administrative functions based on assigned roles.

-   Scale – deploy and manage over 50,000 mobile devices.

-   Single pane of glass –manage both traditional PC clients and Intune-managed devices using the same console.

If you are beginning to plan your Intune deployment today and have a several-month window for piloting, acceptance testing, and deployment, you might consider choosing Intune standalone now with the understanding that updates coming to the cloud service will include more functionality. Throughout the first half of the 2017 calendar year, Intune standalone will receive updates that provide much of the advanced functionality of a hybrid deployment with Configuration Manager. Intune standalone will soon be moving to the Microsoft Azure cloud platform and with it will have enhanced scalability, role-based access through the Azure Portal, custom reporting, and programmatic access through the Azure Graph API.

You can switch from hybrid to Intune standalone, or from standalone to hybrid, but it requires help from Microsoft support and operations. It also requires unenrolling and re-enrolling all of the devices after the management authority is changed.  Microsoft is working on improving the experience of switching configurations in a future service update.
