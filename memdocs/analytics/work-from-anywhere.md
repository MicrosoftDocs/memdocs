---
title: Work from anywhere (preview) report in Endpoint analytics
titleSuffix: Microsoft Endpoint Manager
description: The Work from anywhere (preview) report in Endpoint analytics provides insights to help your end users be productive from anywhere.
ms.date: 05/14/2020
ms.prod: configuration-manager
ms.technology: configmgr-analytics
ms.topic: conceptual
ms.assetid: 2a77cfd2-7fa1-4b00-96b2-ff3baa7f5c77
author: mestew
ms.author: mstewart
manager: dougeby
ROBOTS: NOINDEX
---

# Work from anywhere (preview) report

The ability for employees to work from anywhere productively is essential in today’s world. This report offers insights into how prepared your workforce is to be productive from anywhere. The **Work from anywhere** report is an evolution of the [Recommended software report](recommended-software.md). From the report, you can review your scores and how they compare to the selected baseline. You may notice changes in your scores because the calculations were modified for the **Work from anywhere** report. Learn how to improve your scores by reviewing the insights and recommendations for each of them.  

## Work from anywhere score

The **Work from anywhere score** is a number between 0 and 100. The score represents a weighted average of the percent of devices that have deployed the various insights that help your end users be productive from anywhere. For instance, the current weighting of Windows Autopilot is lower than the weight of other metrics.


The following metrics are available in the **Work from anywhere** report:

- [Windows 10](#windows-10)
- [Cloud management](#cloud-management)
- [Cloud identity](#cloud-identity)
- [Windows Autopilot](#windows-autopilot)

Endpoint analytics computes the **Work from anywhere score** for all your Intune and Configuration Manager devices that have opted into Endpoint Analytics. The **Work from anywhere score** is computed for all your Intune and co-managed devices, regardless of whether they've been configured with the Intune [data collection policy](settings.md#bkmk_profile) or not. For Configuration Manager-managed devices, scores are only computed for [enrolled devices](enroll-configmgr./md#bkmk_cm_enroll).

### Windows 10

Windows 10 provides a better user experience than older versions of Windows. For more information about the cost savings and business benefits enabled by Windows 10, download the [Total Economic Impact (TEI) whitepaper](https://vc2prod.blob.core.windows.net/vc-resources/TEIStudies/TEI%20of%20Windows%2010.pdf).

The **Windows 10** metric measures the percent of devices on supported versions of Windows 10 versus unsupported versions. The recommended remediation action for moving devices from older versions of Windows is to create a deployment plan using [Desktop Analytics](../configmgr/desktop-analytics/overview.md) for co-managed and Intune devices and _____ for Configuration Manager-managed devices. Your score will be based on if these remediation actions have been completed or not.  

### Cloud management 

Configuration Manager and Intune provide integrated cloud-powered management tools and unique co-management options that allow your organization to provision, deploy, manage, and secure endpoints and applications. With cloud management, you can achieve several productivity benefits, including enabling access to corporate resources even when they're away from the corporate network, and eliminating the need for and performance overhead of Group Policy, resulting in a better end-user experience. 

### Cloud identity

### Windows Autopilot