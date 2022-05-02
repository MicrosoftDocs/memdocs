---
title: Optional features
titleSuffix: Configuration Manager
description: Updates to Configuration Manager include optional features, which you have to enable before use.
ms.date: 04/08/2022
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---

# Optional features in Configuration Manager

*Applies to: Configuration Manager (current branch)*

When an update includes one or more optional features, you can enable those features in your hierarchy. Enable features when the update installs, or return to the console later to enable the optional features.

To view available features and their status, in the console go to the **Administration** workspace, expand **Updates and Servicing**, and select the **Features** node. To enable a feature, select it in the list, and then select **Turn on** in the ribbon.

Your user account requires permissions to view and enable optional features. For more information, see [Permissions for in-console updates](prepare-in-console-updates.md#permissions).

When a feature isn't optional, it's automatically available for use. It doesn't appear in the **Features** node.

> [!IMPORTANT]
> In a multi-site hierarchy, enable optional or pre-release features only from the central administration site (CAS). This behavior makes sure there are no conflicts across the hierarchy.<!--507197-->

When you enable a new feature or pre-release feature, the Configuration Manager hierarchy manager (HMAN) must process the change before that feature becomes available. Processing of the change is often immediate. Depending on the HMAN processing cycle, it can take up to 30 minutes to complete. After the change is processed, restart the console before you can use the feature.

When new cloud-based features are available in the Microsoft Endpoint Manager admin center, or other attached cloud services for your on-premises Configuration Manager installation, you can opt in to these new features in the Configuration Manager console.<!--5834830-->

## List of optional features

The following features are optional in the latest version of Configuration Manager:<!--505213-->

<!--Note to include in target articles

> [!NOTE]
> Configuration Manager doesn't enable this optional feature by default. Before using it, you need to enable this feature. For more information, see [Enable optional features from updates](optional-features.md).

-->

- [Cloud management gateway with virtual machine scale set](../../clients/manage/cmg/plan-cloud-management-gateway.md#virtual-machine-scale-sets) <!--3601040,8959690-->
- [Orchestration groups](../../../sum/deploy-use/orchestration-groups.md)<!--3098816, 290B66D8-C735-4895-B59A-DD732D84A697-->
- [Task sequence deployment type](../../../apps/get-started/creating-windows-applications.md#bkmk_tsdt) <!-- 3555953, CB0CDFFB-9C6F-4B18-8954-A43A387302A2-->
- [Remove the central administration site](../deploy/install/remove-central-administration-site.md) <!-- 3607277 -->
- [BitLocker management](../../../protect/plan-design/bitlocker-management.md) <!-- 3601034,6DD56E46-C3EC-4E38-A16F-E98644BB6434 -->
- [Application groups](../../../apps/deploy-use/create-app-groups.md) <!--3555907,EE16A1D8-EF1B-4094-845F-AC107E7C621D-->
- [Task sequence debugger](../../../osd/deploy-use/debug-task-sequence.md) <!--3612274,C3F37661-69E4-4D53-A39C-5D02F97E0E71-->
- [Approve application requests for users per device](../../../apps/deploy-use/deploy-applications.md#bkmk_deploy-settings) <!--1357015,4BA987C9-08FC-48E2-BFFE-C9DCF35B496A-->
- [PFX create](../../../protect/deploy-use/introduction-to-certificate-profiles.md) <!--1321368,CED76B79-929C-4C45-981F-B9BCA6D38A17-->
- [Azure Log Analytics connector](/azure/azure-monitor/platform/collect-sccm) <!--1258052,73A7EC4D-EF22-4EA4-82A9-419C2A8CFC4D-->
- [Windows Defender Exploit Guard policy](../../../protect/deploy-use/create-deploy-exploit-guard-policy.md) <!--1355468,8491D4C8-8484-46B8-BCD6-17DC2CADBAEB-->
- [VPN for Windows](../../../protect/deploy-use/vpn-profiles.md) <!--1283610,EDBEBA3D-3A4D-4465-84D9-D71EB811E7F6-->
- [Windows Hello for Business](../../../protect/deploy-use/windows-hello-for-business-settings.md) (previously known as *Passport for Work*) <!--1245704,8BCA2642-3719-4862-A355-9D39C979E1B4-->

> [!TIP]
> For more information on features that require consent to enable, see [pre-release features](pre-release-features.md).
>
> For more information on features that are only available in the technical preview branch, see [Technical Preview](../../get-started/technical-preview.md).

## Next steps

The current branch includes pre-release features for early testing in a production environment. For more information, see [pre-release features](pre-release-features.md).

For answers to common questions, see [In-console updates FAQ](updates-faq.yml).
