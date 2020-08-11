---
title: Troubleshooting application installation
titleSuffix: Configuration Manager
description: "Troubleshooting application installation for Configuration Manager tenant attach"
ms.date: 08/11/2020
ms.topic: troubleshooting
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 75f47456-cd8d-4c83-8dc5-98b336a7c6c8
manager: dougeby
author: mestew
ms.author: mstewart
---

# Troubleshoot application installation for devices uploaded to the admin center (preview)
<!--6374854, 6521921-->
*Applies to: Configuration Manager (current branch)*

Use the following to troubleshoot Configuration Manager applications in the Microsoft Endpoint Manager admin center:

> [!Important]
> This information relates to a preview feature which may be substantially modified before it's commercially released. Microsoft makes no warranties, express or implied, with respect to the information provided here.

## Common errors from the Microsoft Endpoint Manager admin center

When viewing or installing applications from the Microsoft Endpoint Manager admin center, you may run across one of these errors.  

### <a name="bkmk_aad"></a> The necessary configuration is missing in Azure Active Directory

**Error message:** The necessary configuration is missing in Azure Active Directory. Make sure to attach the Configuration Manager site to your Azure tenant, and assign the proper user role in Azure AD.

**Possible cause:** The user account is likely missing the **Admin User** role for the Configuration Manager Microservice application in Azure AD. Add the role in Azure AD from **Enterprise applications** > **Configuration Manager Microservice** > **Users and groups** > **Add user**. Groups are supported if you have Azure AD premium. Changes to this permission can take up to an hour to take effect.

### <a name="bkmk_noinfo"></a> Unable to get application information

**Error message 1:** Unable to get application information. Make sure Azure AD and AD user discovery are configured and the user is discovered by both. Verify that the user has proper permissions in Configuration Manager.

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
1. IIS must be installed on provider machine. For more information, see [Prerequisites for the administration service](../develop/adminservice/overview.md#prerequisites).

### <a name="bkmk_sync"></a> The site information hasn't yet synchronized

**Error message:** The site information hasn't yet synchronized from Configuration Manager to the Microsoft Endpoint Manager admin center. Wait up to 15 minutes after you attach the site to your Azure tenant.

**Possible causes:**
- This error typically occurs when newly onboarding to tenant attach. Wait 15 minutes for the information to synchronize.
- This error may also appear if the central administration site has been upgraded to a new Configuration Manager version but some child primary sites haven't been upgraded yet.

### <a name="bkmk_installed"></a> Application shows as installed after creating a new deployment

**Symptom:** An application is shown as installed in the Microsoft Endpoint Manager admin center after creating a new device available requires approval deployment or a user available deployment.

**Possible cause:** The application state shown for that device is from another active or past deployment.

### <a name="bkmk_hfru"></a> Errors when searching or retrying an installation

**Symptom:** Errors occur when performing the following actions:
- Use search
- Select **Retry installation**

**Possible cause:**  Ensure that [Update Rollup for Microsoft Endpoint Configuration Manager version 2002](https://support.microsoft.com/help/4560496/) and the corresponding version of the console is installed. For more information, see [prerequisites for installing an application from the admin center](applications.md#prerequisites).

## Known issues

### Unexpected error occurred when getting applications

**Scenario:** Retrieving the list of applications takes longer than expected when you're running Configuration Manager version 2002 and you see `unexpected error occurred`.

**Error message:** AdminService.log will contain:

```log 
System.Data.Entity.Core.EntityCommandExecutionException: An error occurred while executing the command definition. See the inner exception for details.
System.Data.SqlClient.SqlException: Execution Timeout Expired.  The timeout period elapsed prior to completion of the operation or the server is not responding.
System.ComponentModel.Win32Exception: The wait operation timed out
```

**Workaround:** Currently, a workaround isn't available.

### Application installation times out if application requires restart

**Scenario:** If you're running Configuration Manager version 2002 and an application requires a restart to complete the installation process, the installation may time out.

**Symptoms:** The user will see `restart pending` notifications and in Software Center. From the Microsoft Endpoint Manager admin center, the application stays in the `Installing` state.  

**Workaround:** Once the user restarts the device, the correct status is displayed in the admin center.

## Next steps

[Troubleshoot tenant attach](troubleshoot.md)
