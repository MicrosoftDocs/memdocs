---
title: Troubleshoot client details
titleSuffix: Configuration Manager
description: "Troubleshoot client details for Configuration Manager tenant attach"
ms.date: 07/07/2020
ms.topic: troubleshooting
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 44c2eb8a-3ccc-471f-838b-55d7971bb79e
manager: dougeby
author: mestew
ms.author: mstewart
---

# Troubleshoot ConfigMgr client details in the admin center (preview)
<!--6374854, 6521921-->
Use the following to troubleshoot ConfigMgr client details in the Microsoft Endpoint Manager admin center:

> [!Important]
> This information relates to a preview feature which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

## Common errors from the Microsoft Endpoint Manager admin center

When viewing the ConfigMgr client details, you may run across one of these errors.  

### <a name="bkmk_aad"></a> The necessary configuration is missing in Azure Active Directory

**Error message:** The necessary configuration is missing in Azure Active Directory. Make sure to attach the Configuration Manager site to your Azure tenant, and assign the proper user role in Azure AD.

**Possible cause:** The user account is likely missing the **Admin User** role for the Configuration Manager Microservice application in Azure AD. Add the role in Azure AD from **Enterprise applications** > **Configuration Manager Microservice** > **Users and groups** > **Add user**. Groups are supported if you have Azure AD premium. Changes to this permission can take up to an hour to take effect.

### <a name="bkmk_noinfo"></a> Unable to get device or collection information

**Error message 1:** Unable to get client details (or collection) information. Make sure Azure AD and AD user discovery are configured and the user is discovered by both. Verify that the user has proper permissions in Configuration Manager.

**Possible causes:** Typically, this error is caused by an issue with the admin account. Below are the most common issues with the administrative user account:

1. Use the same account to sign in to the admin center. The on-premises identity must be synchronized with and match the cloud identity.
1. Verify the account has **Read** permission for the device's **Collection** in Configuration Manager.
1. Make sure that Configuration Manager has discovered the administrative user account you're using. In the Configuration Manager console, go to the **Assets and Compliance** workspace. Select the **Users** node, and find your user account.

    If your account isn't listed in the **Users** node, check the configuration of the site's [Active Directory User discovery](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).

1. Verify the discovery data. Select your user account. In the ribbon, on the **Home** tab select **Properties**. In the properties window, confirm the following discovery data:

    - **Azure Active Directory Tenant ID**: This value should be a GUID for the Azure AD tenant.
    - **Azure Active Directory User ID**: This value should be a GUID for this account in Azure AD.
    - **User Principal Name**: The format of this value is user@domain. For example, `jqpublic@contoso.com`.

    If the Azure AD properties are empty, check the configuration of the site's [Azure AD user discovery](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc).


### <a name="bkmk_1603"></a> Unexpected error occurred

**Error message:** Unexpected error occurred

**Possible causes:** Unexpected errors are typically caused by either [service connection point](../core/servers/deploy/configure/about-the-service-connection-point.md), [administration service](../develop/adminservice/overview.md), or connectivity issues.

1. Verify the service connection point has connectivity to the cloud using the **CMGatewayNotificationWorker.log**.
1. Verify the administrative service is healthy by reviewing the SMS_REST_PROVIDER component from site component monitoring on the central site.
1. IIS must be installed on provider machine. For more information, see [Prerequisites for the administration service](../develop/adminservice/overview.md#prerequisites)
1. Verify the clock on the service connection point is in sync. If the service connection point's clock is slightly behind, apply [KB4563473 - Update rollup for Configuration Manager version 2002 tenant attach issues](https://support.microsoft.com/help/4563473). Check **AdminService.log** on the provider machine for any errors.

## Known issues

### Getting results timed out

**Scenario:** If you have a remote service connection point and you installed 2002 early update ring before March 30, 2020, you'll see a timeout error in the admin center.

**Error message:** Getting results timed out. Make sure the Configuration Manager service connection point is operational and has a connection to the cloud.

**Workaround:** Copy the `Microsoft.ConfigurationManagement.ManagementProvider.dll` from site server's `bin\x64` folder to the remote service connection point's `bin\x64` folder.  Restart the `SMS_EXECUTIVE` service on the service connection point server.

### Boundary groups list is empty

**Error message**: No boundary groups found or the user may not have permissions to view boundary group information.

This is a known issue for Configuration Manager version 2002 when you have a hierarchy of Configuration Manager sites.

### Logged on user is blank

The logged on user field shows `---` until the user signs out and then signs in on that device after the client is installed. This is a known issue for Configuration Manager version 2002.

:::image type="content" source="media/6024387-known-issue-device-details.png" alt-text="Boundary group list is empty and last logged on user is listed as ---" lightbox="media/6024387-known-issue-device-details.png":::

## Next steps

[Troubleshoot tenant attach](troubleshoot.md)
