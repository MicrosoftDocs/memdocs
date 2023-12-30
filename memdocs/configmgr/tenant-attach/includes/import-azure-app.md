---
author: Banreet
ms.author: banreetkaur
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: include
ms.localizationpriority: high
ms.date: 07/11/2022
manager: apoorvseth
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---
<!-- This include file is currently used by device-sync-actions.md and cloud-attach/enable.md. Note H2/H3s for this include file may be context driven by article. -->

## <a name="bkmk_aad_app"></a> Import a previously created Microsoft Entra application (optional)
<!--6479246-->

During a new onboarding, an administrator can specify a previously created application during onboarding to tenant attach. Don't share or reuse Microsoft Entra applications across multiple hierarchies. If you have multiple hierarchies, create separate Microsoft Entra applications for each.

From the onboarding page in the **Cloud Attach Configuration Wizard** (**Co-management Configuration Wizard** in versions 2103 and earlier), select **Optionally import a separate web app to synchronize Configuration Manager client data to Microsoft Intune Endpoint Manager center**. This option will prompt you to specify the following information for your Microsoft Entra app:

- Microsoft Entra tenant name
- Microsoft Entra tenant ID
- Application name
- Client ID 
- Secret key
- Secret key expiry
- App ID URI 

> [!Important]
> - The App ID URI must use one of the following formats:<!-- 10617402 -->
>    - `api://{tenantId}/{string}`, for example, `api://5e97358c-d99c-4558-af0c-de7774091dda/ConfigMgrService`
>    - `https://{verifiedCustomerDomain}/{string}`, for example, `https://contoso.onmicrosoft.com/ConfigMgrService`
>
>   For more information on creating a Microsoft Entra app, see [Configure Azure services](../../core/servers/deploy/configure/azure-services-wizard.md).
> - When you use an imported Microsoft Entra app, you aren't notified of an upcoming expiration date from [console notifications](../../core/servers/manage/admin-console-notifications.md). <!--10568158--> 

<a name='azure-ad-application-permissions-and-configuration'></a>

### Microsoft Entra application permissions and configuration

Using a previously created application during onboarding to tenant attach requires the following permissions:

- Configuration Manager Microservice permissions:
   - CmCollectionData.read
   - CmCollectionData.write

- Microsoft Graph permissions:
   - Directory.Read.All [Applications permission](/graph/permissions-reference#application-permissions)
   - Directory.Read.All [Delegated directory permission](/graph/permissions-reference#directory-permissions)

- Ensure **Grant admin consent for Tenant** is selected for the Microsoft Entra application. For more information, see [Grant admin consent in App registrations](/azure/active-directory/manage-apps/grant-admin-consent).

- The imported application needs to be configured as follows:
   - Registered for **Accounts in this organizational directory only**. For more information, see [Change who can access your application](/azure/active-directory/develop/quickstart-modify-supported-accounts#to-change-who-can-access-your-application).
   -  Has a valid application ID URI and secret.
