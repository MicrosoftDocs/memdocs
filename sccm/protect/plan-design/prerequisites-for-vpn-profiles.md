---
title: "VPN profile prerequisites | System Center Configuration Manager"
ms.custom: na
ms.date: 2016-03-31
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 63e28bb5-aafb-4315-9c26-a941113f5271
caps.latest.revision: 9
author: Nbigman

---
# Prerequisites for VPN profiles in System Center Configuration Manager
You must have the following security permissions to manage company resource access settings, such as certificate profiles, Wi-Fi profiles, and VPN profiles:  
  
-   To view and manage alerts and reports for VPN profiles: **Create**, **Delete**, **Modify**, **Modify Report**, **Read**, and **Run Report** permissions for the **Alerts** object.  
  
-   To create and manage certificate profiles: **Author Policy**, **Modify Report**, **Read** and **Run Report** permissions for the **Certificate Profile** object.  
  
-   To manage Wi-Fi, certificate, and VPN profile deployments: **Deploy Configuration Policies**, **Modify Client Status Alert**, **Read**, and **Read Resource** permissions for the **Collection** object.  
  
-   To manage all configuration policies: **Create**, **Delete**, **Modify**, **Read** and **Set Security Scope** permissions for the **Configuration Policy** object.  
  
-   To run queries that are related to VPN profiles: **Read** permission for the **Query** object.  
  
-   To view VPN profiles information in the System Center Configuration Manager console: **Read** permission for the **Site** object.  
  
-   To view status messages for VPN profiles: **Read** permission for the **Status Messages** object.  
  
-   To create and modify the Trusted CA certificate profile: **Author Policy**, **Modify Report**, **Read** and **Run Report** permissions for the **Trusted CA Certificate Profile** object.  
  
-   To create and manage VPN profiles: **Author Policy**, **Modify Report**, **Read**, and **Run Report** permissions for the **VPN Profile** object.  
  
-   To create and manage Wi-Fi profiles: **Author Policy**, **Modify Report**, **Read**, and **Run Report** permissions for the **Wi-Fi Profile** object.  
  
 The **Company Resource Access Manager** security role includes these permissions that are required to manage VPN profiles in System Center Configuration Manager. For more information, see  [Configure role-based administration for System Center Configuration Manager](../../core/servers/deploy/configure/configure-role-based-administration.md).