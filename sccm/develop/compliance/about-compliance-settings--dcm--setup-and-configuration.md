---
title: "About Compliance Settings Setup and Configuration"
titleSuffix: "Configuration Manager"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: 0ec16fc6-0775-4c7b-92db-a28f079c3404searchScope: - ConfigMgr SDK
caps.latest.revision: 6
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# About Compliance Settings (DCM) Setup and Configuration
To use desired configuration management on your System Center Configuration Manager site, the following needs to be in place:  

-   The site must be running System Center Configuration Manager.  

-   Clients must be running the System Center Configuration Manager client.  

-   The desired configuration management client agent must be enabled.  

-   Client computers must have installed the .NET Framework 2.0 or a later version.  

> [!NOTE]
>  The .NET Framework 2.0 is supplied with the latest operating systems, such as Windows Vista, and is also available to download through Windows Update. You can also download it from the [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=276779) and install it through software distribution or other deployment methods.  

 Enabling the desired configuration management client agent makes it possible for Configuration Manager clients that are assigned to this site to evaluate compliance with assigned configuration baselines. This client agent is enabled by default, but it will not evaluate its compliance until it downloads one or more configuration baselines and evaluates them at the configured schedule.  

 Disabling the desired configuration client agent prevents Configuration Manager clients that are assigned to this site from evaluating compliance with assigned configuration baselines.  

 This setting to enable or disable the desired configuration management client agent, together with any assigned configuration baselines, is downloaded to client computers according to the **Policy Polling Interval** in the **Computer Client Agent Properties** dialog box (by default, every 60 minutes).  

> [!NOTE]
>  When the desired configuration management client agent is enabled on client computers, the **Systems Management Properties** dialog box displays a **Configurations** tab that lists the downloaded configuration baselines and the results of its compliance evaluation. When the desired configuration management client agent is disabled, the **Configurations** tab is not visible. If the **Configurations** tab is not visible, the client is not running the desired configuration management client agent. This might be because the site is not enabled for desired configuration management, the client computer has not yet downloaded the policy to enable the desired configuration management client agent, a local policy has disabled the desired configuration management client agent, or the client is not a Configuration Manager client.  

## See Also  
 [Configuration Manager Desired Configuration Management &#91;SDK&#93;](../../develop/compliance/compliance-settings-dcm.md)
