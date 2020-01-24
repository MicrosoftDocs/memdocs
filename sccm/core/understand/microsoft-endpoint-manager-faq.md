---
title: Microsoft Endpoint Configuration Manager FAQ
titleSuffix: Configuration Manager
description: Frequently asked questions about Microsoft Endpoint Configuration Manager
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual


ms.assetid: be276b34-e283-4386-8b45-5629e431c50d
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Microsoft Endpoint Configuration Manager FAQ

*Applies to: Configuration Manager (current branch, technical preview branch)*

Starting in version 1910, Configuration Manager is now part of Microsoft Endpoint Manager. This article provides answers to frequently asked questions.

## Summary

Start by watching the following two-minute video from Brad Anderson, Microsoft corporate vice president for Microsoft 365:

> [!VIDEO https://www.youtube.com/embed/GS7oNPInFuw]

## FAQs

### What is Microsoft Endpoint Manager?

Microsoft Endpoint Manager is an integrated solution for managing all of your devices. Microsoft brings together Configuration Manager and Intune with simplified licensing. Continue to leverage your existing Configuration Manager investments, while taking advantage of the power of the Microsoft cloud at your own pace.

The following Microsoft management solutions are all now part of the **Microsoft Endpoint Manager** brand:

- [Configuration Manager](https://docs.microsoft.com/configmgr)
- [Intune](https://docs.microsoft.com/intune)
- [Desktop Analytics](/configmgr/desktop-analytics/overview)
- [Autopilot](https://docs.microsoft.com/intune/enrollment/enrollment-autopilot)
- Other features in the [Device Management Admin Console](https://go.microsoft.com/fwlink/?linkid=2109094)

For more information, see the following posts from Brad Anderson, Microsoft corporate vice president for Microsoft 365:

- [Announcement blog post](https://aka.ms/cmannounce)
- [Vision paper](https://aka.ms/MEMVisionPaper)

### What things change in Configuration Manager with Microsoft Endpoint Manager?

In version 1910, aside from the name change, Configuration Manager still functions the same.

Most notably, the Start menu folder names changed for common components, such as the [Configuration Manager console](/configmgr/core/servers/manage/admin-console#bkmk_open) and [Software Center](/configmgr/core/understand/software-center#bkmk_open).

### How do we refer to the product now?

- When referring to the entire solution that includes all components: **Microsoft Endpoint Manager**

- When referring to the on-premises component:
  - On first reference, use the full brand name: **Microsoft Endpoint Configuration Manager**
  - For general use: **Configuration Manager**
  - For space-constrained use: **ConfigMgr**, only in instances where the general use name doesn't fit

### Are there any licensing changes?

Yes! As announced at Microsoft Ignite 2019, if you're licensed for Configuration Manager, then you're also now licensed for Intune to [co-manage](/configmgr/comanage/overview) your Windows PCs. For more information, see the [Product and licensing FAQ](/configmgr/core/understand/product-and-licensing-faq#bkmk_mem).

### Why do I still see "System Center Configuration Manager" some places?

It takes time to make changes across all products, services, and supporting materials like documentation.

There are also some fundamental components that may never change. The main Windows service on site servers is still **SMS_Executive**. The GitHub repository that supports this documentation will continue to be **SCCMDocs**.

## Next steps

Learn about the [what's new in Configuration Manager incremental versions](/configmgr/core/plan-design/changes/whats-new-incremental-versions).
