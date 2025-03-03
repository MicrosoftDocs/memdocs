---
title: Microsoft Intune tenant attach prerequisites
titleSuffix: Configuration Manager
description: Prerequisites for Microsoft Intune tenant attach.
ms.date: 07/11/2022
ms.topic: article
ms.subservice: core-infra
ms.service: configuration-manager
manager: apoorvseth
author: Banreet
ms.author: banreetkaur
ms.localizationpriority: high
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Microsoft Intune tenant attach: Prerequisites
<!--3555758 live 3/4/2020  Configuration Manager version 2002 min-->
*Applies to: Configuration Manager (current branch)*

The Microsoft Intune family of products is an integrated solution for managing all of your devices. Microsoft brings together Configuration Manager and Intune into a single console called **Microsoft Intune admin center**. You can upload your Configuration Manager devices to the cloud service and take actions from the **Devices** page in the admin center. Some of the features you may want to use include:

- Run PowerShell [scripts](scripts.md)
- Install [applications](applications.md)
- Query devices with [CMPivot](../tenant-attach/cmpivot-samples-attached.md?toc=/mem/configmgr/cloud-attach/toc.json&bc=/mem/configmgr/cloud-attach/breadcrumb/toc.json)
- Display a [timeline](timeline.md) of events from the device

## Prerequisites

- An account that is a *Global Administrator* for signing in when applying this onboarding change. For more information, see [Microsoft Entra administrator roles](/azure/role-based-access-control/rbac-and-directory-admin-roles#azure-ad-administrator-roles).

  - Onboarding creates a third-party app and a first party service principal in your Microsoft Entra tenant.

- An Azure cloud environment.

  - The **Upload to Microsoft Endpoint Manager admin center** option is disabled for Microsoft Azure China 21Vianet (Azure China Cloud) and Azure US Government Cloud.<!--8815787--> Starting in version 2107, this option is available for US Government customers.

- Starting in version 2107, United States Government customers can use the following tenant attach features in the US Government cloud:<!-- 8353823 -->

  - Account onboarding
  - Tenant sync to Intune
  - Device sync to Intune
  - Device actions in the Microsoft Intune admin center
 
- The geographic location of the Azure tenant and the service connection point should be the same. 

- At least one Intune license for you as the administrator to access the Microsoft Intune admin center. <!--10254915-->

- The [administration service](../develop/adminservice/overview.md) in Configuration Manager needs to be set up and functional. <!--1104776-->

- If your central administration site has a [remote provider](../core/plan-design/hierarchy/plan-for-the-sms-provider.md), then follow the instructions for the [CAS has a remote provider](../core/servers/manage/cmpivot-changes.md#cas-has-a-remote-provider) scenario in the CMPivot article. <!--7796824-->

This feature supports all OS versions that Configuration Manager currently supports as a client. For more information, see [Supported OS versions for clients and devices](../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md).<!-- MEMDocs#545 -->

## Permissions

The user accounts performing device actions have the following prerequisites:

- The user account needs to be a synced user object in Microsoft Entra ID (hybrid identity). This means that the user is synced to Microsoft Entra ID from Active Directory.
  - For Configuration Manager version 2103, and later: </br>
   Has been discovered with either [Microsoft Entra user discovery](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc) or [Active Directory user discovery](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser). <!--9089764-->
- The **Initiate Configuration Manager action** permission under **Remote tasks** in the Microsoft Intune admin center.
  - For more information about adding or verifying permissions in the admin center, see [Role-based access control (RBAC) with Microsoft Intune](../../intune/fundamentals/role-based-access-control.md#roles).

## Internet endpoints

[!INCLUDE [Internet endpoints for tenant attach](../core/plan-design/network/includes/internet-endpoints-tenant-attach.md)]

The service connection point validates important internet endpoints for tenant attach. These checks help make sure that the cloud service is available. It also helps you troubleshoot issues by quickly determining if network connectivity is a problem. For more information, see [Validate internet access](../core/servers/deploy/configure/about-the-service-connection-point.md#validate-internet-access).<!--8565578-->

> [!NOTE]
> The service connection point checks the CRL. If this server doesn't have access to the URLs listed above, the CRL check fails. Consider setting a system proxy or use the following command: 'netsh winhttp set proxy'. For more information, see [How the Windows Update client determines which proxy server to use to connect to the Windows Update Web site](https://support.microsoft.com/topic/how-the-windows-update-client-determines-which-proxy-server-to-use-to-connect-to-the-windows-update-web-site-08612ae5-3722-886c-f1e1-d012516c22a1). Make sure that you include a bypass list for internal site communications. This configuration may be necessary as the proxy server settings within Configuration Manager only configure the proxy for Configuration Manager applications and not the underlying OS.

## Limitations
<!--IN12698976-->
Currently, Configuration Manager devices aren't included when retrieving a device list through a PowerShell script or through Microsoft Graph API. To work around this issue, use the **Export** option from the **All devices** page in the admin center.

## Next steps

- [Enable tenant attach](device-sync-actions.md)
