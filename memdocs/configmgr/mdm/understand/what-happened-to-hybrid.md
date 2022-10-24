---
title: What happened to hybrid MDM?
titleSuffix: Configuration Manager
description: Learn about the deprecation of hybrid mobile device management (MDM) in Configuration Manager
ms.date: 12/30/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# What happened to hybrid MDM?

*Applies to: Configuration Manager (current branch)*

> [!WARNING]
> Microsoft retired the hybrid MDM service offering as of September 1, 2019. Any remaining hybrid MDM devices won't receive policy, apps, or security updates.

## Remove hybrid MDM

If your Configuration Manager site had a Microsoft Intune Subscription, you need to remove it.

1. In the Configuration Manager console, go to the **Administration** workspace. Expand **Cloud Services**, and select the **Microsoft Intune Subscription** node. Delete your existing Intune Subscription.

1. In the **Remove Microsoft Intune Subscription Wizard**, select the option to **Remove Microsoft Intune Subscription from Configuration Manager**, and then click **Next**.

1. Complete the wizard.

## Deprecation announcement

The following note is the original deprecation announcement:

> [!NOTE]  
> As of August 14, 2018, hybrid mobile device management is a [deprecated feature](../../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md). Starting with the 1902 Intune service release, expected at the end of February 2019, new customers can't create a new hybrid connection.
> <!--Intune feature 2683117-->  
> Since launching on Azure over a year ago, Intune has added hundreds of new customer-requested and market-leading service capabilities. It now offers far more capabilities than those offered through hybrid mobile device management (MDM). Intune on Azure provides a more integrated, streamlined administrative experience for your enterprise mobility needs.
>
> As a result, most customers choose Intune on Azure over hybrid MDM. The number of customers using hybrid MDM continues to decrease as more customers move to the cloud. Therefore, on September 1, 2019, Microsoft will retire the hybrid MDM service offering.
>
> This change doesn't affect on-premises Configuration Manager or [co-management for Windows 10 devices](../../comanage/overview.md). If you're unsure whether you're using hybrid MDM, go to the **Administration** workspace of the Configuration Manager console, expand **Cloud Services**, and select **Microsoft Intune Subscriptions**. If you have a Microsoft Intune subscription set up, your tenant is configured for hybrid MDM.
>
> **How does this affect me?**
>
> - Microsoft will support your hybrid MDM usage for the next year. The feature will continue to receive major bug fixes. Microsoft will support existing functionality on new OS versions, such as enrollment on iOS 12. There will be no new features for hybrid MDM.  
>
> - If you migrate to Intune on Azure before the end of the hybrid MDM offering, there should be no end user impact.  
>
> - On September 1, 2019, any remaining hybrid MDM devices will no longer receive policy, apps, or security updates.  
>
> - Licensing remains the same. Intune on Azure licenses are included with hybrid MDM.  
>
> - The on-premises MDM feature in Configuration Manager isn't deprecated. Starting in Configuration Manager version 1810, you can use on-premises MDM without an Intune connection. For more information, see [An Intune connection is no longer required for new on-premises MDM deployments](../../core/plan-design/changes/whats-new-in-version-1810.md#bkmk_opmdm).
>
> - The on-premises conditional access feature of Configuration Manager is also deprecated with hybrid MDM. If you use conditional access on devices managed with the Configuration Manager client, make sure they are protected before you migrate.
>     1. Set up conditional access policies in Azure
>     2. Set up compliance policies in Intune portal
>     3. Finish hybrid migration, and set the MDM authority to Intune
>     4. Enable co-management
>     5. Move the compliance policies co-management workload to Intune
>
>     For more information, see [Conditional access with co-management](../../comanage/quickstart-conditional-access.md).
>
> **What do I need to do to prepare for this change?**
>
> - Start planning your migration for MDM from the ConfigMgr console to Azure. Many customers, including Microsoft IT, have gone through this process. For more information, see this [Microsoft case study](https://aka.ms/Intune_MSFT).  
>
> - Contact your partner of record or FastTrack for assistance. [FastTrack for Microsoft 365](https://aka.ms/hybrid_fasttrack) can assist in your migration from hybrid MDM to Intune on Azure.
>
> For more information, see [the Intune support blog post](https://aka.ms/hybrid_notification).

## Next steps

For more information on supported features for managing MDM devices, see the following articles:

- [What is Microsoft Intune?](/intune/what-is-intune)
- [What is on-premises MDM?](manage-mobile-devices-with-on-premises-infrastructure.md)
- [Device management with Exchange](../deploy-use/manage-mobile-devices-with-exchange-activesync.md)