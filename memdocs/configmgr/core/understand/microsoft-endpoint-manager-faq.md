---
title: Microsoft Endpoint Configuration Manager FAQ
titleSuffix: Configuration Manager
description: Frequently asked questions about Microsoft Endpoint Configuration Manager
ms.date: 04/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: be276b34-e283-4386-8b45-5629e431c50d
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Microsoft Endpoint Configuration Manager FAQ

*Applies to: Configuration Manager (current branch, technical preview branch)*

Since October 2019, Configuration Manager is part of Microsoft Endpoint Manager. This article provides answers to frequently asked questions.

## Summary

Start by watching the following two-minute video from Brad Anderson, former Microsoft corporate vice president for Microsoft 365:

> [!VIDEO https://www.youtube.com/embed/GS7oNPInFuw]

## FAQs

### What is Microsoft Endpoint Manager?

Microsoft Endpoint Manager is an integrated solution for managing all of your devices. Microsoft brings together Configuration Manager and Intune with simplified licensing. Continue to use your existing Configuration Manager investments, while taking advantage of the power of the Microsoft cloud at your own pace.

The following Microsoft management solutions are all now part of the **Microsoft Endpoint Manager** brand:

- [Configuration Manager](../../index.yml)
- [Intune](../../../intune/index.yml)
- [Desktop Analytics](../../desktop-analytics/overview.md)
- [Autopilot](../../../autopilot/enrollment-autopilot.md)
- Other features in the [Microsoft Endpoint Manager admin console](https://techcommunity.microsoft.com/t5/enterprise-mobility-security/microsoft-intune-rolls-out-an-improved-streamlined-endpoint/ba-p/937760)

For more information, see the following posts from Brad Anderson, former Microsoft corporate vice president for Microsoft 365:

- [Announcement blog post](https://aka.ms/cmannounce)
- [Vision paper](https://aka.ms/MEMVisionPaper)

### What things change in Configuration Manager with Microsoft Endpoint Manager?

Aside from the name change, Configuration Manager still functions the same.

Most notably, the Start menu folder names changed for common components, such as the [Configuration Manager console](../servers/manage/admin-console.md#bkmk_open) and [Software Center](software-center.md#bkmk_open).

### How do we refer to the product now?

- When referring to the entire solution that includes all components: **Microsoft Endpoint Manager**

- When referring to the on-premises component:
  - On first reference, use the full brand name: **Microsoft Endpoint Configuration Manager**
  - For general use: **Configuration Manager**
  - For space-constrained use: **ConfigMgr**, only in instances where the general use name doesn't fit

### Are there any licensing changes?

Yes! As announced at Microsoft Ignite 2019, if you're licensed for Configuration Manager, then you're also now licensed for Intune to [co-manage](../../comanage/overview.md) your Windows PCs. For more information, see the [Product and licensing FAQ](product-and-licensing-faq.md#bkmk_mem).

### Why do I still see "System Center Configuration Manager" some places?

It takes time to make changes across all products, services, and supporting materials like documentation.

There are also some fundamental components that may never change. The main Windows service on site servers is still **SMS_Executive**.

## Next steps

Learn about the [what's new in Configuration Manager incremental versions](../plan-design/changes/whats-new-incremental-versions.md).
