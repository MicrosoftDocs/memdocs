---
title: Troubleshooting application installation
titleSuffix: Configuration Manager
description: Troubleshooting application installation for Configuration Manager tenant attach
ms.date: 07/11/2022
ms.topic: troubleshooting
ms.prod: configuration-manager
ms.technology: configmgr-core
manager: dougeby
author: mestew
ms.author: mstewart
ms.localizationpriority: high
---

# Troubleshoot application installation for devices uploaded to the admin center
<!--6374854, 6521921-->
*Applies to: Configuration Manager (current branch)*

Use the following to troubleshoot Configuration Manager applications in the Microsoft Endpoint Manager admin center:

## Common errors from the Microsoft Endpoint Manager admin center

When viewing or installing applications from the Microsoft Endpoint Manager admin center, you may run across one of these errors.  

### <a name="bkmk_intune"></a> You don’t have access to view this information
<!--7980141-->
**Error message:** You don’t have access to view this information. Make sure a proper user role is assigned from Intune.

**Possible cause:** The user account needs an [Intune role](../../intune/fundamentals/role-based-access-control.md) assigned. In some cases, this error may also occur during replication of information and it resolves without intervention after a few minutes.

### <a name="bkmk_noinfo"></a> Unable to get application information

**Error message 1:** Unable to get application information. Make sure Azure AD and AD user discovery are configured and the user is discovered by both. Verify that the user has proper permissions in Configuration Manager.

**Possible causes:** Typically, this error is caused by an issue with the admin account. Below are the most common issues with the administrative user account:

1. Use the same account to sign in to the admin center. The on-premises identity must be synchronized with and match the cloud identity.
1. Verify the account has **Read** permission for the device's **Collection** in Configuration Manager.
1. Make sure that Configuration Manager has discovered the administrative user account you're using to access the tenant attach features within Microsoft Endpoint Manager admin center. In the Configuration Manager console, go to the **Assets and Compliance** workspace. Select the **Users** node, and find your user account.

    If your account isn't listed in the **Users** node, check the configuration of the site's [Active Directory User discovery](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).

1. Verify the discovery data. Select your user account. In the ribbon, on the **Home** tab select **Properties**. In the properties window, confirm the following discovery data:

    - **Azure Active Directory Tenant ID**: This value should be a GUID for the Azure AD tenant.
    - **Azure Active Directory User ID**: This value should be a GUID for this account in Azure AD.
    - **User Principal Name**: The format of this value is user@domain. For example, `jqpublic@contoso.com`.

    If the Azure AD properties are empty, check the configuration of the site's [Azure AD user discovery](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc).

### <a name="bkmk_1603"></a> Unexpected error occurred

**Error message:** Unexpected error occurred

#### Error code 500 with an unexpected error occurred message

1. If you see `System.Security.SecurityException` in the **AdminService.log**, verify that your user principal name (UPN) discovered by [Active Directory User discovery](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser) isn't set to a cloud UPN rather than an on-premises UPN. An empty UPN value is also acceptable as it means the Active Directory discovered domain name is used. If you see cloud-only UPN (example: onmicrosoft.com) that's not valid domain UPN (contoso.com), you have an issue and may need to go [set the UPN suffix in Active Directory](/office365/enterprise/prepare-a-non-routable-domain-for-directory-synchronization#add-upn-suffixes-and-update-your-users-to-them).
1. Install [KB4576782 - Application blade times out in Microsoft Endpoint Manager admin center](https://support.microsoft.com/help/4576782) if you see the below error in the **AdminService.log**:
   ```log 
   System.Data.Entity.Core.EntityCommandExecutionException: An error occurred while executing the command definition. See the inner exception for details.
   System.Data.SqlClient.SqlException: Execution Timeout Expired.  The timeout period elapsed prior to completion of the operation or the server is not responding.
   System.ComponentModel.Win32Exception: The wait operation timed out
   ```

#### Error code 3 with an unexpected error occurred message

The Admin Service isn't running or IIS isn't installed. IIS must be installed on provider machine. For more information, see [Prerequisites for the administration service](../develop/adminservice/overview.md#prerequisites).

#### Other possible causes of unexpected errors

Unexpected errors are typically caused by either [service connection point](../core/servers/deploy/configure/about-the-service-connection-point.md), [administration service](../develop/adminservice/overview.md), or connectivity issues.

1. Verify the service connection point has connectivity to the cloud using the **CMGatewayNotificationWorker.log**.
1. Verify the administrative service is healthy by reviewing the SMS_REST_PROVIDER component from site component monitoring on the central site.
1. IIS must be installed on provider machine. For more information, see [Prerequisites for the administration service](../develop/adminservice/overview.md#prerequisites).


### <a name="bkmk_sync"></a> The site information hasn't yet synchronized

**Error message:** The site information hasn't yet synchronized from Configuration Manager to the Microsoft Endpoint Manager admin center. Wait up to 15 minutes after you attach the site to your Azure tenant.

**Possible causes:**
- This error typically occurs when newly onboarding to tenant attach. Wait up to an hour for the information to synchronize.
- This error may also appear if the central administration site has been upgraded to a new Configuration Manager version but some child primary sites haven't been upgraded yet.

### <a name="bkmk_installed"></a> Application shows as installed after creating a new deployment

**Symptom:** An application is shown as installed in the Microsoft Endpoint Manager admin center after creating a new device available requires approval deployment or a user available deployment.

**Possible cause:** The application state shown for that device is from another active or past deployment.

### <a name="bkmk_hfru"></a> Errors when searching or retrying an installation

**Symptom:** Errors occur when performing the following actions:
- Use search
- Select **Retry installation**

**Possible cause:**  Ensure that a supported version of Configuration Manager is installed. For more information, see [prerequisites for installing an application from the admin center](applications.md#prerequisites).

## Known issues


[!INCLUDE [Known issues shared across tenant attach features](includes/known-issues-shared.md)]


## Next steps

[Troubleshoot tenant attach](troubleshoot.md)