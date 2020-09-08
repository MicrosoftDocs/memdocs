---
title: Troubleshooting resource explorer
titleSuffix: Configuration Manager
description: "Troubleshooting resource explorer for Configuration Manager tenant attach"
ms.date: 09/08/2020
ms.topic: troubleshooting
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 05829d36-2cbf-4921-bf4b-cfcdef4cfcc1
manager: dougeby
author: mestew
ms.author: mstewart
---

# Troubleshoot resource explorer for devices uploaded to the admin center (preview)
<!--6479284-->
*Applies to: Configuration Manager (current branch)*

Use the following to troubleshoot resource explorer for ConfigMgr devices in the Microsoft Endpoint Manager admin center:

> [!Important]
> This information relates to a preview feature which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

## Common errors from the Microsoft Endpoint Manager admin center

### <a name="bkmk_aad"></a> The necessary configuration is missing in Azure Active Directory

**Error message:** The necessary configuration is missing in Azure Active Directory. Make sure to attach the Configuration Manager site to your Azure tenant, and assign the proper user role in Azure AD.

**Possible cause:** The user account is likely missing the **Admin User** role for the Configuration Manager Microservice application in Azure AD. Add the role in Azure AD from **Enterprise applications** > **Configuration Manager Microservice** > **Users and groups** > **Add user**. Groups are supported if you have Azure AD premium. Changes to this permission can take up to an hour to take effect.

### <a name="bkmk_noinfo"></a> Unable to get resource information

**Error message 1:** Unable to get resource information. Make sure Azure AD and AD user discovery are configured and the user is discovered by both. Verify that the user has proper permissions in Configuration Manager.

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

### <a name="bkmk_sync"></a> The site information hasn't yet synchronized

**Error message:** The site information hasn't yet synchronized from Configuration Manager to the Microsoft Endpoint Manager admin center. 

**Possible causes:**
- This error typically occurs when newly onboarding to tenant attach. Wait an hour for the information to synchronize.
- This error may also appear if the central administration site has been upgraded to a new Configuration Manager version but some child primary sites haven't been upgraded yet.

### <a name="bkmk_load"></a> Unable to load inventory classes

**Error message:** Unable to load inventory classes for your environment.

**Possible causes:**

- The list of entities may not have been uploaded from on-premises. Wait an hour then see if the error persists.
- An invalid **Tenant ID** or **Hierarchy ID** may have been specified. Check the service connection point and make sure it's functioning.
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

[!INCLUDE [Known issues shared across tenant attach features](includes/known-issues-shared.md)]

## Next steps

[Troubleshoot tenant attach](troubleshoot.md)