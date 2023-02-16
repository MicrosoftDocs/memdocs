---
title: Troubleshooting resource explorer
titleSuffix: Configuration Manager
description: Troubleshooting resource explorer for Intune tenant attach
ms.date: 01/25/2022
ms.topic: troubleshooting
ms.prod: configuration-manager
ms.technology: configmgr-core
manager: apoorvseth
author: Banreet
ms.author: banreetkaur
ms.localizationpriority: high
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Troubleshoot resource explorer for devices uploaded to the admin center
<!--6479284-->
*Applies to: Configuration Manager (current branch)*

Use the following to troubleshoot resource explorer for ConfigMgr devices in the Microsoft Intune admin center:

## Common errors from the Microsoft Intune admin center

### <a name="bkmk_intune"></a> You don’t have access to view this information
<!--7980141-->
**Error message:** You don’t have access to view this information. Make sure a proper user role is assigned from Intune.

**Possible cause:** The user account needs an [Intune role](../../intune/fundamentals/role-based-access-control.md) assigned. In some cases, this error may also occur during replication of information and it resolves without intervention after a few minutes.
### <a name="bkmk_noinfo"></a> Unable to get resource information

**Error message 1:** Unable to get resource information. Make sure Azure AD and AD user discovery are configured and the user is discovered by both. Verify that the user has proper permissions in Configuration Manager.

**Possible causes:** Typically, this error is caused by an issue with the admin account. Below are the most common issues with the administrative user account:

1. Use the same account to sign in to the admin center. The on-premises identity must be synchronized with and match the cloud identity.
1. Verify the account has **Read** permission for the device's **Collection** in Configuration Manager.
1. Make sure that Configuration Manager has discovered the administrative user account you're using to access the tenant attach features within Microsoft Intune admin center. In the Configuration Manager console, go to the **Assets and Compliance** workspace. Select the **Users** node, and find your user account.

    If your account isn't listed in the **Users** node, check the configuration of the site's [Active Directory User discovery](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).

1. Verify the discovery data. Select your user account. In the ribbon, on the **Home** tab select **Properties**. In the properties window, confirm the following discovery data:

    - **Azure Active Directory Tenant ID**: This value should be a GUID for the Azure AD tenant.
    - **Azure Active Directory User ID**: This value should be a GUID for this account in Azure AD.
    - **User Principal Name**: The format of this value is user@domain. For example, `jqpublic@contoso.com`.

    If the Azure AD properties are empty, check the configuration of the site's [Azure AD user discovery](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc).

### <a name="bkmk_sync"></a> The site information hasn't yet synchronized

**Error message:** The site information hasn't yet synchronized from Configuration Manager to the Microsoft Intune admin center. 

**Possible causes:**
- This error typically occurs when newly onboarding to tenant attach. Wait an hour for the information to synchronize.
- This error may also appear if the central administration site has been upgraded to a new Configuration Manager version but some child primary sites haven't been upgraded yet.

### <a name="bkmk_load"></a> Unable to load inventory classes

**Error message:** Unable to load inventory classes for your environment.

**Possible causes:**

- The list of entities may not have been uploaded from on-premises. Wait an hour then see if the error persists.
- An invalid **Tenant ID** or **Support ID** may have been specified. Check the service connection point and make sure it's functioning.
- Unable to successfully execute query to get classes. Wait 15 minutes to see if the error persists.

### <a name="bkmk_get"></a> Failed to get inventory classes with data

**Error message:** Failed to get inventory classes with data. On-premises error 500.

**Possible causes:** Unexpected errors are typically caused by either [service connection point](../core/servers/deploy/configure/about-the-service-connection-point.md), [administration service](../develop/adminservice/overview.md), or connectivity issues.

1. Verify the service connection point has connectivity to the cloud using the **CMGatewayNotificationWorker.log**.
1. Verify the administrative service is healthy by reviewing the SMS_REST_PROVIDER component from site component monitoring on the central site.
1. IIS must be installed on provider machine. For more information, see [Prerequisites for the administration service](../develop/adminservice/overview.md#prerequisites).

### <a name="bkmk_user"></a> The user does not have permissions

**Error message:** Failed to get inventory classes with data. The user does not have permissions.

**Possible causes:** The user may not have access to the collection that the device is a part of. Verify the following items:

1. Use the same account to sign in to the admin center. The on-premises identity must be synchronized with and match the cloud identity.
1. Verify the account has **Read** permission for the device's **Collection** in Configuration Manager.
1. Make sure that Configuration Manager has discovered the administrative user account you're using. In the Configuration Manager console, go to the **Assets and Compliance** workspace. Select the **Users** node, and find your user account.

    If your account isn't listed in the **Users** node, check the configuration of the site's [Active Directory User discovery](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).

## Known issues

### <a name="bkmk_import"></a> Newly imported inventory classes fail to load
<!--9391319, -->
**Scenario:** New hardware inventory classes are imported. You can see the newly imported classes in **Resource Explorer** from the Configuration Manager console. When you open **Resource explorer** from Microsoft Intune admin center, the newly imported class doesn't have data and **Failed** appears at the bottom of the results pane.

**Workaround:** The current workaround is to restart the `SMS_Executive` service on the provider machine for which the [administration service](../develop/adminservice/overview.md) handles service requests. You can determine where your administration service is by reviewing the **CMGatewayNotification.log** and looking for your server in the URL.

```log
Sending AdminService request with URL: https://CMsite.contoso.com/AdminService/v1.0/ ...
```

[!INCLUDE [Known issues shared across tenant attach features](includes/known-issues-shared.md)]

## Next steps

[Troubleshoot tenant attach](troubleshoot.md)