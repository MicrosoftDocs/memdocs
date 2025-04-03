---
author: Banreet
ms.author: banreetkaur
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: include
ms.date: 08/14/2020
ms.localizationpriority: high
manager: apoorvseth
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---
<!--Don't apply H2 in this include file since they are context driven by article-->

### <a name="bkmk_mfa"></a> When the Configuration Manager site is configured to require multi-factor authentication, most tenant attach features don't work
<!--7986450, 7988266-->
**Scenario:** If the [SMS provider](../../core/plan-design/hierarchy/plan-for-the-sms-provider.md) machine that communicates with the [service connection point](../../core/servers/deploy/configure/about-the-service-connection-point.md) is configured to use multi-factor authentication, you can't install applications, run CMPivot queries, and perform other actions from the admin console. You receive an error code 403, forbidden.  

**Workaround:** The current workaround is to configure the on-premises hierarchy to the default authentication level of **Windows authentication**. For more information, see the [Authentication section in the SMS provider article](../../core/plan-design/hierarchy/plan-for-the-sms-provider.md#authentication).

