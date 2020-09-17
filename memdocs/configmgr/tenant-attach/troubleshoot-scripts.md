---
title: Troubleshoot scripts for devices uploaded to the admin center
titleSuffix: Configuration Manager
description: "Troubleshooting scripts for Configuration Manager tenant attach"
ms.date: 09/08/2020
ms.topic: troubleshooting
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: a0eb1e8f-2c85-4f48-a0b5-945b3e5f63f3
manager: dougeby
author: mestew
ms.author: mstewart
---

# Troubleshoot scripts (preview) for devices uploaded to the admin center
<!--6024392-->
*Applies to: Configuration Manager (current branch)*

Use the following to troubleshoot scripts in the Microsoft Endpoint Manager admin center:

> [!Important]
> This information relates to a preview feature which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

## Common issues

### <a name="bkmk_aad"></a> The necessary configuration is missing in Azure Active Directory

**Error message:** The necessary configuration is missing in Azure Active Directory. Make sure to attach the Configuration Manager site to your Azure tenant, and assign the proper user role in Azure AD.

**Possible cause:** The user account is likely missing the **Admin User** role for the Configuration Manager Microservice application in Azure AD. Add the role in Azure AD from **Enterprise applications** > **Configuration Manager Microservice** > **Users and groups** > **Add user**. Groups are supported if you have Azure AD premium. Changes to this permission can take up to an hour to take effect.

### <a name="bkmk_403"></a> Unable to get Scripts information

**Error message:** Unable to get Scripts information. Make sure Azure AD and AD user discovery are configured and the user account accessing tenant attach features from the Microsoft Endpoint Manager admin center is discovered by both. Verify that the user has proper permissions in Configuration Manager.

**Possible causes:** Typically, this error is caused by an issue with the admin account. Below are the most common issues with the administrative user account:

1. Use the same account to sign in to the admin center. The on-premises identity must be synchronized with and match the cloud identity.
1. Verify the account has **Read** permission for the device's **Collection** in Configuration Manager.
1. Verify the account has **Read Resource** permission for the device's **Collection** in Configuration Manager.
1. Make sure that Configuration Manager has discovered the administrative user account you're using to access the tenant attach features within Microsoft Endpoint Manager admin center. In the Configuration Manager console, go to the **Assets and Compliance** workspace. Select the **Users** node, and find your user account.

    If your account isn't listed in the **Users** node, check the configuration of the site's [Active Directory User discovery](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).

1. Verify the discovery data. Select your user account. In the ribbon, on the **Home** tab select **Properties**. In the properties window, confirm the following discovery data:

    - **Azure Active Directory Tenant ID**: This value should be a GUID for the Azure AD tenant.
    - **Azure Active Directory User ID**: This value should be a GUID for this account in Azure AD.
    - **User Principal Name**: The format of this value is user@domain. For example, `jqpublic@contoso.com`.

    If the Azure AD properties are empty, check the configuration of the site's [Azure AD user discovery](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc).


### <a name="bkmk_noinfo"></a> Unable to get device information

**Error message:** Unable to get device information. Make sure Azure AD and AD user discovery are configured and the user is discovered by both. Verify that the user has proper permissions in Configuration Manager.

**Possible cause:** Make sure that Configuration Manager has discovered the administrative user account you're using to access the tenant attach features within Microsoft Endpoint Manager admin center. In the Configuration Manager console, go to the **Assets and Compliance** workspace. Select the **Users** node, and find your user account.

    If your account isn't listed in the **Users** node, check the configuration of the site's [Active Directory User discovery](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).

1. Verify the discovery data. Select your user account. In the ribbon, on the **Home** tab select **Properties**. In the properties window, confirm the following discovery data:

    - **Azure Active Directory Tenant ID**: This value should be a GUID for the Azure AD tenant.
    - **Azure Active Directory User ID**: This value should be a GUID for this account in Azure AD.
    - **User Principal Name**: The format of this value is user@domain. For example, `jqpublic@contoso.com`.

    If the Azure AD properties are empty, check the configuration of the site's [Azure AD user discovery](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc).


### <a name="bkmk_1603"></a> Unexpected error occurred

**Error message:** Unexpected error occurred

**Possible cause:** Verify the account has **Read Resource** permission for the device's **Collection** in Configuration Manager.


### <a name="bkmk_version"></a> Configuration Manager doesn't meet the minimum version prerequisite

**Error message:** Configuration Manager doesn't meet the minimum version prerequisite.

**Possible causes:** Your Configuration Manager sites are not running the minimum version of Configuration Manager 2006 with [KB4580678 - Tenant attach rollup for Configuration Manager current branch, version 2006](https://support.microsoft.com/help/4580678) installed. Verify the following:
 - Configuration Manager version 2006 or higher is installed.
 - That [KB4580678](https://support.microsoft.com/help/4580678) on sites running Configuration Manager version 2006.
 - That every site in the hierarchy meets the minimums listed above.

## Known issues

[!INCLUDE [Known issues shared across tenant attach features](includes/known-issues-shared.md)]
