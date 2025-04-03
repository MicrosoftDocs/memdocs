---
title: Troubleshoot software updates for devices uploaded to the admin center
titleSuffix: Configuration Manager
description: Troubleshooting software updates for Intune tenant attach
ms.date: 07/11/2022
ms.subservice: core-infra
ms.service: configuration-manager
author: Banreet
ms.author: banreetkaur
ms.manager: apoorvseth
ms.topic: troubleshooting
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Troubleshoot software updates in the admin center
<!--13035723-->

When reviewing software updates in the admin center, you may run across some common errors. Use the following information about common error messages to troubleshoot software updates for tenant attached devices in the Microsoft Intune admin center:

## Common error messages

### You don’t have access to view this information

**Error message:** You don’t have access to view this information. Make sure a proper user role is assigned from Intune.

**Possible cause:** The user account needs an [Intune role](../../intune-service/fundamentals/role-based-access-control.md) assigned. In some cases, this error may also occur during replication of information, and it resolves without intervention after a few minutes.

### Unable to get software updates information

**Error message 1:** Device can't be found, or you don't have permission to access the device

**Possible causes:**

1. Verify that Configuration Manager's [role based access control](../../configmgr/core/understand/fundamentals-of-role-based-administration.md) for the admin user has the device in scope.
1. Verify the machine account of the [SMS Provider role](../../configmgr/core/plan-design/hierarchy/plan-for-the-sms-provider.md) for the primary site (or standalone site) isn't a member of either the **Pre-Windows 2000 Compatible Access** or **Windows Authorization Access** (WAA) groups in on-premises Active Directory. For more information, see [Some applications and APIs require access to authorization information on account objects](/troubleshoot/windows-server/identity/apps-apis-require-access).

**Error message 2:** Unable to get software updates information. Make sure Microsoft Entra ID and AD user discovery are configured and the user is discovered by both. Verify that the user has proper permissions in Configuration Manager.

**Possible causes for Configuration Manager versions 2103 and later:**

Typically, this error is caused by an issue with the admin account. Below are the most common issues with the administrative user account:

1. Use the same account to sign in to the admin center. The on-premises identity must be synchronized with and match the cloud identity.
1. Make sure that Configuration Manager has discovered the administrative user account you're using to access the tenant attach features within Microsoft Intune admin center. In the Configuration Manager console, go to the **Assets and Compliance** workspace. Select the **Users** node and find your user account.

    If your account isn't listed in the **Users** node, check the configuration of the site's [Active Directory User discovery](../../configmgr/core/servers/deploy/configure/about-discovery-methods.md).

1. Verify the discovery data. Select your user account. In the ribbon, on the **Home** tab select **Properties**. In the properties window, confirm the following discovery data:

    - **Microsoft Entra tenant ID:** This value should be a GUID for the Microsoft Entra tenant.
    - **Microsoft Entra user ID:** This value should be a GUID for this account in Microsoft Entra ID.
    - **User Principal Name:** The format of this value is user@domain. For example, jqpublic@contoso.com.

    If the Microsoft Entra properties are empty, check the configuration of the site's [Microsoft Entra user discovery](../../configmgr/core/servers/deploy/configure/about-discovery-methods.md).

### Error loading your content

**Error message:** Getting results timed out. Make sure the Configuration Manager service connection point is operational and has a connection to the cloud.

**Possible causes:**

1. Make sure the hierarchy is still tenant-attached and connected. For more information, see the **CMGatewayNotificationWorker.log** file.
1. If the service connection point or site server were recently rebooted, this error occurs temporarily.
1. A site upgrade or a transient network error can cause this message to occur temporarily.
1. For Configuration Manager versions 2103 and earlier, it's possible that the cache has expired, and the SQL connection is stale. Restart **SMS_Executive** service on the machine running the service connection point (SCP) role if you see errors similar to the following in the SCP's **CMGatewayNotificationWorker.log:**

    `[Critical][CMGatewayNotificationWorker][0][System.InvalidOperationException][0x80131509]
    ExecuteReader requires an open and available Connection. The connection's current state is closed.`

### Error validating request

**Error message:** Error validating request. Verify that the Configuration Manager service connection point can reach the internet endpoints required for tenant attach.

**Possible causes:** Typically, this error is seen when URLs that are needed by tenant attach are blocked. If the service connection point can't access the needed internet endpoints, a validation error will occur. For more information, see [Internet endpoints](prerequisites.md#internet-endpoints).

### Unexpected error occurred

**Error message:** unexpected error occurred

**Possible causes:** Unexpected errors are typically caused by either [service connection point](../../configmgr/core/servers/deploy/configure/about-the-service-connection-point.md), [administration service](../../configmgr/develop/adminservice/overview.md), or connectivity issues.

1. Verify the service connection point has connectivity to the cloud using the **CMGatewayNotificationWorker.log**.
1. Verify the administrative service is healthy by reviewing the SMS_REST_PROVIDER component from site component monitoring on both the central site and primary site that owns the device.
1. IIS must be installed on provider machine. For more information, see [Prerequisites for the administration service](../../configmgr/develop/adminservice/overview.md#prerequisites).


### Configuration Manager doesn't meet the minimum version prerequisite

**Error message:** Configuration Manager doesn't meet the minimum version prerequisite

**Possible cause:** Your Configuration Manager sites aren't running the [minimum version](software-updates.md#prerequisites) of Configuration Manager. The minimum required version is Configuration Manager version 2111 with [update rollup KB12896009](../hotfix/2111/12896009.md). This version, or a later version, needs to be installed on all sites in the hierarchy.

## Known issues

1. Some of the **Classification** resources aren't translated in some of the supported languages.
1. For consoles in Japanese, the current time format is YYYY/MM/DD.
