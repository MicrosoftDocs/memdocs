---
title: Introduction to the LTSB
titleSuffix: Configuration Manager
description: Learn about the long-term servicing branch of Configuration Manager.
ms.date: 08/23/2019
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: article
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz
---

# Introduction to the long-term servicing branch of Configuration Manager

*Applies to: System Center Configuration Manager (Long-Term Servicing Branch)*

The long-term servicing branch (LTSB) of Configuration Manager is a distinct branch that's designed as an install option available to all customers. However, it's the only option for customers who let lapse their Software Assurance (SA) or equivalent subscription rights for Configuration Manager.

Based on Configuration Manager version 1606, the LTSB has reduced functionality when compared to the current branch of Configuration Manager.

> [!TIP]
> The Configuration Manager LTSB isn't related to the System Center suite long-term servicing channel (LTSC). For more information, see [Overview of System Center release options](/system-center/ltsc-and-sac-overview).

## Features that aren't available

The current branch of Configuration Manager supports the following functionality that isn't available when you use the LTSB:

- In-console updates that add new features and improvements.
- Support for newly released operating systems to use as site servers and clients.
- On-premises MDM
- The Windows servicing dashboard and servicing plans, including support for recent Windows versions.
- Support for future releases of Windows Server and Windows 10 LTSB
- Asset Intelligence
- Cloud-based distribution points
- Exchange Online as an Exchange Connector

Although support for these features isn't available with the LTSB, some features remain visible in the Configuration Manager console, but can't be selected or used.

Cloud integrations, as well as any features included with Configuration Manager current branch version 1610 or later, aren't available to the LTSB. These features include, but aren't limited to the following:<!--SCCMDocs#1823-->

- Co-management
- Cloud management gateway
- Microsoft Entra integration
- Apps from the Microsoft Store for Business

## Find LTSB documentation

The LTSB is based on current branch version 1606. Use the [current branch documentation](../../index.yml), with caveats and limitations that are specific to the LTSB. Those caveats and limitations are identified in the following articles:

- [Install the LTSB](install-the-ltsb.md)
- [Upgrade the LTSB to the current branch](convert-to-current-branch.md)
- [Supported configurations for the LTSB](supported-configurations-for-ltsb.md)
- [Manage the LTSB of Configuration Manager](manage-the-ltsb.md)

When you reference current branch documentation for the LTSB, details that apply to version 1606 or earlier also apply to the LTSB. Features or details that are introduced with version 1610 or later aren't supported by the LTSB.

## Licensing overview for the LTSB

Customers with active Software Assurance (SA) on Configuration Manager licenses, or with equivalent subscription rights as of October 1, 2016, have rights to use the October 2016 version 1606 release of Configuration Manager. Customers with rights to Configuration Manager on or after October 1, 2016, will find two licensed options upon installation: current branch and long-term servicing branch (LTSB).

Customers that have perpetual rights to System Center Configuration Manager, or that allow SA or subscription to lapse after October 1, can install the version of System Center Configuration Manager LTSB that is current at the time of lapse.

For more information about these licenses, see the [Complete terms and conditions for the products you purchase through Microsoft Volume Licensing programs](https://www.microsoftvolumelicensing.com/DocumentSearch.aspx?mode=1).

For more information about licensing for Configuration Manager branches, see [Configuration Manager licensing and branches](learn-more-editions.md).

## Next Steps

If you decide that the Configuration Manager LTSB is the correct branch for your environment, [install a new LTSB](install-the-ltsb.md#install-a-new-site) site as part of a new hierarchy, or [upgrade a System Center 2012 Configuration Manager site](install-the-ltsb.md#upgrade-from-system-center-2012-configuration-manager) and hierarchy.
