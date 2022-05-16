---
title: [Troubleshoot ConfigMgr Software Updates in the admin center]
titleSuffix: Intune
description: To troubleshoot ConfigMgr Software Updates in the Microsoft Endpoint Manager admin center
ms.date: 05/12/2022
ms.service: microsoft-intune
author: banreet
ms.author: banreetkaur
ms.manager: apoorvseth
ms.topic : include
---



<!--13035723-->

# <a name="SoftwareUpdates"></a> Troubleshoot ConfigMgr Software Updates in the admin center


When viewing the ConfigMgr Software Updates, you may run across some common errors. Use the following information of common error messages to troubleshoot ConfigMgr Software Updates in the Microsoft Endpoint Manager admin center:

## Minimum CM version error

### You don’t have access to view this information

**Error message:** You don’t have access to view this information. Make sure a proper user role is assigned from Intune.

**Possible cause:** The user account needs an [Intune role](../../intune/fundamentals/role-based-access-control.md) assigned. In some cases, this error may also occur during replication of information, and it resolves without intervention after a few minutes.

### Unable to get Software updates information

**Error message 1:** Device can't be found, or you don't have permission to access the device

**Possible causes:**

1. Verify that Configuration Manager's [role based access control](configmgr\core\understand\fundamentals-of-role-based-administration.md) for the admin user has the device in scope.
2. The machine account of [SMS Provider role](configmgr\core\plan-design\hierarchy\plan-for-the-sms-provider.md) of the primary site (or standalone site) is not a member of either the **Pre-Windows 2000 Compatible Access** or **Windows Authorization Access** (WAA) groups in on-premises Active Directory. For more information, see [Some applications and APIs require access to authorization information on account objects](https://docs.microsoft.com/en-us/troubleshoot/windows-server/identity/apps-apis-require-access).

**Error message 2:** Unable to get Software Updates information. Make sure Azure AD and AD user discovery are configured and the user is discovered by both. Verify that the user has proper permissions in Configuration Manager.

**Possible causes for Configuration Manager versions 2103 and later:**

Typically, this error is caused by an issue with the admin account. Below are the most common issues with the administrative user account:

1. Use the same account to sign in to the admin center. The on-premises identity must be synchronized with and match the cloud identity.
2. Make sure that Configuration Manager has discovered the administrative user account you're using to access the tenant attach features within Microsoft Endpoint Manager admin center. In the Configuration Manager console, go to the **Assets and Compliance** workspace. Select the **Users** node and find your user account.

    If your account isn't listed in the **Users** node, check the configuration of the site's [Active Directory User discovery](configmgr\core\servers\deploy\configure\about-discovery-methods.md).

3. Verify the discovery data. Select your user account. In the ribbon, on the **Home** tab select **Properties**. In the properties window, confirm the following discovery data:

    - **Azure Active Directory Tenant ID:** This value should be a GUID for the Azure AD tenant.
    - **Azure Active Directory User ID:** This value should be a GUID for this account in Azure AD.
    - **User Principal Name:** The format of this value is user@domain. For example, jqpublic@contoso.com.

    If the Azure AD properties are empty, check the configuration of the site's [Azure AD user discovery](configmgr/core/servers/deploy/configure/about-discovery-methods.md).

### Error loading your content

**Error message:** Getting results timed out. Make sure the Configuration Manager service connection point is operational and has a connection to the cloud.

**Possible causes:**

1. Make sure the hierarchy is still tenant-attached and connected. For more information, see the **CMGatewayNotificationWorker.log** file.
2. If the service connection point or site server were recently rebooted, this error occurs temporarily.
3. A site upgrade or a transient network error can cause this message to occur temporarily.
4. For Configuration Manager versions 2103 and earlier, it's possible that the cache has expired, and the SQL connection is stale. Restart **SMS_Executive** service on the machine running the service connection point (SCP) role if you see errors similar to the following in the SCP's **CMGatewayNotificationWorker.log:**

    `[Critical][CMGatewayNotificationWorker][0][System.InvalidOperationException][0x80131509]
    ExecuteReader requires an open and available Connection. The connection's current state is closed.`

### Error validating request

**Error message:** Error validating request. Verify that the Configuration Manager service connection point can reach the internet endpoints required for tenant attach.

**Possible causes:** Typically, this error is seen when URLs that are needed by tenant attach are blocked. If the service connection point can't access the needed internet endpoints, a validation error will occur. For more information, see [Internet endpoints](configmgr/tenant-attach/prerequisites#internet-endpoints.md).

### Unexpected error occurred

**Error message:** unexpected error occurred

**Possible causes:** Unexpected errors are typically caused by either [service connection point](configmgr/core/servers/deploy/configure/about-the-service-connection-point.md), [administration service](configmgr/develop/adminservice/overview.md), or connectivity issues.

1. Verify the service connection point has connectivity to the cloud using the **CMGatewayNotificationWorker.log**.
2. Verify the administrative service is healthy by reviewing the SMS_REST_PROVIDER component from site component monitoring on both the central site and primary site that owns the device.
3. IIS must be installed on provider machine. For more information, see [Prerequisites for the administration service](configmgr/develop/adminservice/overview#prerequisites.md).
4. For Configuration Manager version 2002, verify the clock on the service connection point is in sync. If the service connection point's clock is slightly behind, apply [KB4563473 - Update rollup for Configuration Manager version 2002 tenant attach issues](https://support.microsoft.com/help/4563473). Check **AdminService.log** on the provider machine for any errors.
5. For Configuration Manager version 2002, verify the device is in the security scope for the administrator's security role. For more information, see [Fundamentals of role-based administration](configmgr/core/understand/fundamentals-of-role-based-administration.md).

## Known issues

1. Few Software Update Classification resources are not translated in some of the supported languages.
2. The ‘Learn more about software update’ link goes to a page which is always in English.
3. For Japanese, the current time format is YYYY/MM/DD.
