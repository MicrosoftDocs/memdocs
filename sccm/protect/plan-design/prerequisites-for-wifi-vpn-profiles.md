---
title: "Wi-Fi and VPN profile prerequisites"
titleSuffix: "Configuration Manager"
description: "Learn about the security permissions needed to manage certificate profiles, Wi-Fi profiles, and VPN profiles in System Center Configuration Manager."
ms.custom: na
ms.date: 11/23/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d2dacb2d-ab3b-42a2-8dc8-94da31f993c2
caps.latest.revision: 5
caps.handback.revision: 0
author: Nbigmanms.author: nbigmanmanager: angrobe

---
# Prerequisites for Wi-Fi and VPN Profiles in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
Wi-Fi and VPN profiles in System Center Configuration Manager have dependencies only within the product.  

 You must have the following security permissions to manage company resource access settings, such as certificate profiles, Wi-Fi profiles, and VPN profiles:  

-   To view and manage alerts and reports for Wi-Fi and profiles: **Create**, **Delete**, **Modify**, **Modify Report**, **Read**, and **Run Report** for the **Alerts** object.  

-   To create and manage certificate profiles: **Author Policy**, **Modify Report**, **Read**, and **Run Report** for the **Certificate Profile** object.  

-   To manage Wi-Fi, certificate, and VPN profile deployments: **Deploy Configuration Policies**, **Modify Client Status Alert**, **Read**, and **Read Resource** for the **Collection** object.  

-   To manage all configuration policies: **Create**, **Delete**, **Modify**, **Read**, and **Set Security Scope** for the **Configuration Policy** object.  

-   To run queries that are related to Wi-Fi and VPN profiles: **Read** permission for the **Query** object.  

-   To view Wi-Fi and VPN profiles information in the System Center Configuration Manager console: **Read** permission for the **Site** object.  

-   To view status messages for Wi-Fi and VPN profiles: **Read** permission for the **Status Messages** object.  

-   To create and modify the Trusted CA certificate profile: **Author Policy**, **Modify Report**, **Read**, and **Run Report** for the **Trusted CA Certificate Profile** object.  

-   To create and manage VPN profiles: **Author Policy**, **Modify Report**, **Read**, and **Run Report** for the **VPN Profile** object.  

-   To create and manage Wi-Fi profiles: **Author Policy**, **Modify Report**, **Read**, and **Run Report** for the **Wi-Fi Profile** object.  

 The **Company Resource Access Manager** security role includes these permissions that are required to manage Wi-Fi profiles in System Center Configuration Manager. For more information, see [Configure security in System Center Configuration Manager](../../core/plan-design/security/configure-security.md).
