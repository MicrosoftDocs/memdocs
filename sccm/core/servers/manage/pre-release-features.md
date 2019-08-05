---
title: Pre-release features
titleSuffix: Configuration Manager
description: Pre-release features are features that are in the Current Branch for early testing in a production environment.
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 6bce416b-761d-4b23-bd33-5b7c30edb10d
author: mestew
ms.author: mstewart
manager: dougeby
ms.collection: M365-identity-device-management
---

# Pre-release features in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Pre-release features are features that are in the current branch for early testing in a production environment. These features are fully supported, but still in active development. They might receive changes until they move out of the pre-release category.



## Give consent  

Before using pre-release features, give consent to use pre-release features. Giving consent is a one-time action per hierarchy that you can't undo. Until you give consent, you can't enable new pre-release features included with updates. After you turn on a pre-release feature, you can't turn it off.

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node.  

2. Click **Hierarchy Settings** in the ribbon.  

3. On the **General** tab of Hierarchy Settings Properties, enable the option to **Consent to use pre-release features**. Click **OK**.  



## Enabling pre-release features

When you install an update that includes pre-release features, those features are visible in the Updates and Servicing Wizard with the regular features included in the update.

#### If you have given consent
In the Updates and Servicing Wizard, enable pre-release features. Select the pre-release features as you would any other feature.     

Optionally, wait to enable pre-release features later from the **Features** node under **Updates and Servicing** in the **Administration** workspace. Select a feature, and then click **Turn on** in the ribbon. Until you give consent, this option isn't available for use.

#### If you haven't given consent
In the Updates and Servicing Wizard, pre-release features are visible but you can't enable them. After the update is installed, these features are visible in the **Features** node. However, you can't enable them until you give consent.


> [!Important]  
> In a multi-site hierarchy, you can only enable optional or pre-release features from the central administration site. This behavior ensures there are no conflicts across the hierarchy. <!--507197-->  
> 
> If you gave consent at a stand-alone primary site, and then expand the hierarchy by installing a new central administration site, you must give consent again at the central administration site.  

When you enable a pre-release feature, the Configuration Manager hierarchy manager (HMAN) must process the change before that feature becomes available. Processing of the change is often immediate. Depending on the HMAN processing cycle, it can take up to 30 minutes to complete. After the change is processed, restart the console before using the feature.



## <a name="bkmk_table"></a>Pre-release features

<!--Note/tip for target article

> [!Note]  
> In this version of Configuration Manager, <feature name> is a pre-release feature. To enable it, see [Pre-release features](/sccm/core/servers/manage/pre-release-features).  


> [!Tip]  
> This feature was first introduced in version 1702 as a [pre-release feature](/sccm/core/servers/manage/pre-release-features). Beginning with version 1906, it's no longer a pre-release feature.  

-->

<!-- With each current branch release, to help purge this list a bit, remove any entries that were added as a full feature in a version that's no longer supported -->
| Feature          | Added as pre-release | Added as a full feature |  
|------------------|----------------------|-------------------------|
| [Task sequence debugger](/sccm/osd/deploy-use/debug-task-sequence) <!--3612274,C3F37661-69E4-4D53-A39C-5D02F97E0E71--> | Version 1906 | ![Not yet](media/red_x.png) |
| [Application groups](/sccm/apps/deploy-use/create-app-groups) <!--3555907,EE16A1D8-EF1B-4094-845F-AC107E7C621D--> | Version 1906 | ![Not yet](media/red_x.png) |
| [Azure Active Directory user group discovery](/sccm/core/servers/deploy/configure/configure-discovery-methods#bkmk_azuregroupdisco) <!--3611956,023715E7-BFBA-4E9E-A80F-B5B626464ADD-->| Version 1906 | ![Not yet](media/red_x.png) |
| [Synchronize collection membership results to Azure Active Directory](/sccm/core/clients/manage/collections/create-collections#bkmk_aadcollsync) <!--3607475,C2127144-C8DE-49F6-9CB3-D4F5B59F9515-->| Version 1906| ![Not yet](media/red_x.png)|
| [CMPivot standalone](/sccm/core/servers/manage/cmpivot#bkmk_standalone) <!--3555890/4692885,no GUID--> | Version 1906 | ![Not yet](media/red_x.png) |
| [SMS Provider administration service](/sccm/core/plan-design/hierarchy/plan-for-the-sms-provider#bkmk_admin-service) <!--1359052--> | Version 1810 | Version 1906 |
| [Enhanced HTTP site system](/sccm/core/plan-design/hierarchy/enhanced-http) <!--1356889,1358228--> | Version 1806 | Version 1810 |
| [Client apps for co-managed devices](/sccm/comanage/workloads#client-apps) <!--1357892,CC3AE625-BF72-49B1-8AB1-AF0DCF2D6F4C--> | Version 1806 | ![Not yet](media/red_x.png) |
| [SCAP extensions](/sccm/compliance/plan-design/scap/about-scap) <!--3607889--> | Version 1806 | ![Not yet](media/red_x.png) |
| [Package conversion manager](/sccm/apps/pcm/package-conversion-manager) <!--1357861--> | Version 1806 | Version 1810 |
| [Support for Cisco AnyConnect 4.0.07x and later for iOS](/sccm/mdm/deploy-use/create-vpn-profiles) <!--1357393--> | Version 1802 | Version 1802 <br>with update 4163547 |
| [Phased deployments](/sccm/osd/deploy-use/create-phased-deployment-for-task-sequence) <!--1356837--> | Version 1802 | Version 1806 |
| [Run task sequence step](/sccm/osd/understand/task-sequence-steps#child-task-sequence) <!--1261338--> |  Version 1710 | Version 1802 |
| [Windows Defender Exploit Guard](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) <!--1355468--> | Version 1710 | Version 1802 |
| [Device health attestation assessment for conditional access compliance policies](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm) <!--1235616--> | Version 1710 | Version 1802 |
| [Create and run Windows PowerShell scripts](/sccm/apps/deploy-use/create-deploy-scripts) <!--1236459--> | Version 1706 | Version 1802 |
| [Device Guard management](/sccm/protect/deploy-use/use-device-guard-with-configuration-manager) <!--3600958 (fka 1355092 & 1319346)--> | Version 1702 | Version 1906 |
| [Cloud management gateway](/sccm/core/clients/manage/plan-cloud-management-gateway) <!--1101764--> | Version 1610 | Version 1802 |
| [Azure Log Analytics connector](/sccm/core/clients/manage/sync-data-log-analytics) <!--1236739--> | Version 1606 | Version 1802 |
| [Servicing a cluster-aware collection (Server groups)](/sccm/sum/deploy-use/service-a-server-group) <!--1081776,290B66D8-C735-4895-B59A-DD732D84A697--> | Version 1602 | ![Not yet](media/red_x.png) |

<!--Image used = ![Not yet](media/red_x.png) -->

> [!Tip]  
> For more information on non-pre-release features that you must enable first, see [Enable optional features from updates](/sccm/core/servers/manage/install-in-console-updates#bkmk_options).  
> 
> For more information on features that are only available in the technical preview branch, see [Technical Preview](/sccm/core/get-started/technical-preview).  
