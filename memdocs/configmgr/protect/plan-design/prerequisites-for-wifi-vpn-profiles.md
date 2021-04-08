---
title: Wi-Fi and VPN profile prerequisites
titleSuffix: Configuration Manager
description: Learn about the prerequisites to manage Wi-Fi profiles and VPN profiles in Configuration Manager
ms.date: 04/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: d2dacb2d-ab3b-42a2-8dc8-94da31f993c2
author: mestew
ms.author: mstewart
manager: dougeby
---

# Prerequisites for Wi-Fi and VPN profiles in Configuration Manager

*Applies to: Configuration Manager (current branch)*

> [!IMPORTANT]
> Starting in Configuration Manager version 2103, this company resource access feature is [deprecated](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).<!-- 9315387 --> Use Microsoft Intune to [deploy resource access profiles](../../../intune/configuration/device-profiles.md).

Wi-Fi and VPN profiles in Configuration Manager have dependencies only within the product.

You need the following security permissions to manage company resource access settings, such as certificate profiles, Wi-Fi profiles, and VPN profiles:  

- To view and manage alerts and reports for Wi-Fi and profiles: **Create**, **Delete**, **Modify**, **Modify Report**, **Read**, and **Run Report** for the **Alerts** object.  

- To create and manage certificate profiles: **Author Policy**, **Modify Report**, **Read**, and **Run Report** for the **Certificate Profile** object.  

- To manage Wi-Fi, certificate, and VPN profile deployments: **Deploy Configuration Policies**, **Modify Client Status Alert**, **Read**, and **Read Resource** for the **Collection** object.  

- To manage all configuration policies: **Create**, **Delete**, **Modify**, **Read**, and **Set Security Scope** for the **Configuration Policy** object.  

- To run queries that are related to Wi-Fi and VPN profiles: **Read** permission for the **Query** object.  

- To view Wi-Fi and VPN profiles information in the Configuration Manager console: **Read** permission for the **Site** object.  

- To view status messages for Wi-Fi and VPN profiles: **Read** permission for the **Status Messages** object.  

- To create and modify the Trusted CA certificate profile: **Author Policy**, **Modify Report**, **Read**, and **Run Report** for the **Trusted CA Certificate Profile** object.  

- To create and manage VPN profiles: **Author Policy**, **Modify Report**, **Read**, and **Run Report** for the **VPN Profile** object.  

- To create and manage Wi-Fi profiles: **Author Policy**, **Modify Report**, **Read**, and **Run Report** for the **Wi-Fi Profile** object.  

The **Company Resource Access Manager** built-in security role includes these permissions that are required to manage Wi-Fi profiles in Configuration Manager. For more information, see [Configure security](../../core/plan-design/security/configure-security.md).
