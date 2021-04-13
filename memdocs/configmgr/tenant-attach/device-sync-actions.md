---
title: Microsoft Endpoint Manager tenant attach
titleSuffix: Configuration Manager
description: "Upload your Configuration Manager devices to the cloud service and take actions from the admin center."
ms.date: 04/13/2021
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.assetid: 7a597d9e-a878-48d0-a7ce-56a1dbfd0e5c
manager: dougeby
author: mestew
ms.author: mstewart
---

# <a name="bkmk_attach"></a> Microsoft Endpoint Manager tenant attach: Device sync and device actions
<!--3555758 live 3/4/2020-->
*Applies to: Configuration Manager (current branch)*

Microsoft Endpoint Manager is an integrated solution for managing all of your devices. Microsoft brings together Configuration Manager and Intune into a single console called **Microsoft Endpoint Manager admin center**.

Starting in Configuration Manager version 2002, you can upload your Configuration Manager devices to the cloud service and take actions from the **Devices** blade in the admin center.

## Prerequisites

- An account that is a *Global Administrator* for signing  in when applying this change. For more information, see [Azure Active Directory (Azure AD) administrator roles](/azure/role-based-access-control/rbac-and-directory-admin-roles#azure-ad-administrator-roles).
   - Onboarding creates a third-party app and a first party service principal in your Azure AD tenant.
   
- An Azure public cloud environment.
   - The **Upload to Microsoft Endpoint Manager admin center** option is disabled for Microsoft Azure China 21Vianet (Azure China Cloud) and Azure US Government Cloud. <!--8815787-->
- The user accounts triggering device actions have the following prerequisites:
   - The user account needs to be a synced user object in Azure AD (hybrid identity). This means that the user is synced to Azure Active Directory from Active Directory.
     - For Configuration Manager version 2103, and later: </br>
   Has been discovered with either [Azure Active Directory user discovery](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc) or [Active Directory user discovery](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser). <!--9089764-->
     - For Configuration Manager version 2010, and earlier: </br>
   Has been discovered with both [Azure Active Directory user discovery](../core/servers/deploy/configure/about-discovery-methods.md#azureaddisc) and [Active Directory user discovery](../core/servers/deploy/configure/about-discovery-methods.md#bkmk_aboutUser).
.
   
   - The **Initiate Configuration Manager action** permission under **Remote tasks** in the Microsoft Endpoint Manager admin center. 
      - For more information about adding or verifying permissions in the admin center, see [Role-based access control (RBAC) with Microsoft Intune](../../intune/fundamentals/role-based-access-control.md#roles).
      
- If your central administration site has a [remote provider](../core/plan-design/hierarchy/plan-for-the-sms-provider.md), then follow the instructions for the [CAS has a remote provider](../core/servers/manage/cmpivot-changes.md#cas-has-a-remote-provider) scenario in the CMPivot article. <!--7796824-->

This feature supports all OS versions that Configuration Manager currently supports as a client. For more information, see [Supported OS versions for clients and devices](../core/plan-design/configs/supported-operating-systems-for-clients-and-devices.md).<!-- MEMDocs#545 -->

## Internet endpoints

[!INCLUDE [Internet endpoints for tenant attach](../core/plan-design/network/includes/internet-endpoints-tenant-attach.md)]

Starting in version 2010, the service connection point validates important internet endpoints for tenant attach. These checks help make sure that the cloud service is available. It also helps you troubleshoot issues by quickly determining if network connectivity is a problem. For more information, see [Validate internet access](../core/servers/deploy/configure/about-the-service-connection-point.md#validate-internet-access).<!--8565578-->

## <a name="bkmk_edit"></a> Enable device upload when co-management is already enabled

If you have co-management enabled currently, you'll use the co-management properties to enable device upload. When co-management isn't already enabled, [Use the **Configure co-management** wizard](#bkmk_config) to enable device upload instead.

When co-management is already enabled, edit the co-management properties to enable device upload using the instructions below:

1. In the Configuration Manager admin console, go to **Administration** > **Overview** > **Cloud Services** > **Co-management**.
1. In the ribbon, select **Properties** for your co-management production policy.
1. In the **Configure upload** tab, select **Upload to Microsoft Endpoint Manager admin center**. Select **Apply**.
   - The default setting for device upload is **All my devices managed by Microsoft Endpoint Configuration Manager**. If needed, you can limit upload to a single device collection.
1. Check the option to **Enable Endpoint analytics for devices uploaded to Microsoft Endpoint Manager** if you also want to get insights to optimize the end-user experience in [Endpoint Analytics](../../analytics/overview.md).

> [!Important]
> When you enable Endpoint analytics data upload, your default client settings will be automatically updated to allow managed endpoints to send relevant data to your Configuration Manager site server. If you use custom client settings, you may need to update and re-deploy them for data collection to occur. For more details on this, as well as how to configure data collection, such as to limit collection only to a specific set of devices, see the section on [Configuring Endpoint analytics data collection](../../analytics/enroll-configmgr.md#bkmk_cm_enable).

   [![Upload devices to Microsoft Endpoint Manager admin center](../../analytics/media/6051638-configure-upload-configmgr.png)](../../analytics/media/6051638-configure-upload-configmgr.png#lightbox)
1. Sign in with your *Global Administrator* account when prompted.
1. Select **Yes** to accept the **Create AAD Application** notification. This action provisions a service principal and creates an Azure AD application registration to facilitate the sync.
1. Choose **OK** to exit the co-management properties once you've done making changes.


## <a name="bkmk_config"></a> Enable device upload when co-management isn't enabled

If you don't have co-management enabled, you'll use the **Configure co-management** wizard to enable device upload. You can upload your devices without enabling automatic enrollment for co-management or switching workloads to Intune. All Devices managed by Configuration Manager that have **Yes** in the **Client** column will be uploaded. If needed, you can limit upload to a single device collection. If co-management is already enabled in your environment, [Edit co-management properties](#bkmk_edit) to enable device upload instead.

When co-management isn't enabled, use the instructions below to enable device upload:

1. In the Configuration Manager admin console, go to **Administration** > **Overview** > **Cloud Services** > **Co-management**.
1. In the ribbon, select **Configure co-management** to open the wizard.
1. On the **Tenant onboarding** page, select **AzurePublicCloud** for your environment. Azure Government Cloud and Azure China 21Vianet aren't supported.
1. Select **Sign In**. Use your *Global Administrator* account to sign in.
1. Ensure the **Upload to Microsoft Endpoint Manager admin center** option is selected on the **Tenant onboarding** page.
   - Make sure the option **Enable automatic client enrollment for co-management** isn't checked if you don't want to enable co-management now. If you do want to enable co-management, select the option.
   - If you enable co-management along with device upload, you'll be given additional pages in the wizard to complete. For more information, see [Enable co-management](../comanage/how-to-enable.md).

   [![Co-management Configuration Wizard](./media/3555758-comanagement-wizard.png)](./media/3555758-comanagement-wizard.png#lightbox)
1. Choose **Next** and then **Yes** to accept the **Create AAD Application** notification. This action provisions a service principal and creates an Azure AD application registration to facilitate the sync.
     - Optionally, you can import a previously created Azure AD application during tenant attach onboarding (starting in version 2006). For more information, see the [Import a previously created Azure AD application](#bkmk_aad_app) section.
1. On the **Configure upload** page, select the recommended device upload setting for **All my devices managed by Microsoft Endpoint Configuration Manager**. If needed, you can limit upload to a single device collection.
    - Starting in Configuration Manager version 2010, when a single collection is selected, it's child collections are also uploaded. <!--8717629-->
1. Check the option to **Enable Endpoint analytics for devices uploaded to Microsoft Endpoint Manager** if you also want to get insights to optimize the end-user experience in [Endpoint Analytics](../../analytics/overview.md)
1. Select **Summary** to review your selection, then choose **Next**.
1. When the wizard is complete, select **Close**.  

## Perform device actions

1. In a browser, navigate to `endpoint.microsoft.com`
1. Select **Devices** then **All devices** to see the uploaded devices. You'll see **ConfigMgr** in the **Managed by** column for uploaded devices.
   [![All devices in Microsoft Endpoint Manager admin center](./media/3555758-all-devices.png)](./media/3555758-all-devices.png#lightbox)
1. Select a device to load its **Overview** page.
1. Choose any of the following actions:
   - **Sync Machine Policy**
   - **Sync User Policy**
   - **App Evaluation Cycle**

   [![Device overview in Microsoft Endpoint Manager admin center](./media/3555758-device-overview-actions.png)](./media/3555758-device-overview-actions.png#lightbox)

## <a name="bkmk_aad_app"></a> Import a previously created Azure AD application (optional)
<!--6479246-->
*(Introduced in version 2006)*

During a [new onboarding](#bkmk_config), an administrator can specify a previously created application during onboarding to tenant attach. Don't share or reuse Azure AD applications across multiple hierarchies. If you have multiple hierarchies, create separate Azure AD applications for each.

From the **Tenant onboarding** page in the **Co-management Configuration Wizard**, select **Optionally import a separate web app to synchronize Configuration Manager client data to Microsoft Endpoint Manager admin center**. This option will prompt you to specify the following information for your Azure AD app:

- Azure AD tenant name
- Azure AD tenant ID
- Application name
- Client ID
- Secret key
- Secret key expiry
- App ID URI

### Azure AD application permissions and configuration

Using a previously created application during onboarding to tenant attach requires the following permissions:

- Configuration Manager Microservice permissions:
   - CmCollectionData.read
   - CmCollectionData.write

- Microsoft Graph permissions:
   - Directory.Read.All [Applications permission](/graph/permissions-reference#application-permissions)
   - Directory.Read.All [Delegated directory permission](/graph/permissions-reference#directory-permissions)

- Ensure **Grant admin consent for Tenant** is selected for the Azure AD application. For more information, see [Grant admin consent in App registrations](/azure/active-directory/manage-apps/grant-admin-consent).

- The imported application needs to be configured as follows:
   - Registered for **Accounts in this organizational directory only**. For more information, see [Change who can access your application](/azure/active-directory/develop/quickstart-modify-supported-accounts#to-change-who-can-access-your-application).
   -  Has a valid application ID URI and secret

## Display the Configuration Manager connector status from the admin console
 <!--IN9229333, CM7138634-->
From the Microsoft Endpoint Manager admin center, you can review the status of your Configuration Manager connector. To display the connector status, go to **Tenant administration** > **Connectors and tokens** > **Microsoft Endpoint Configuration Manager**. Select a Configuration Manager hierarchy running version 2006, or later to display additional information about it.
   
:::image type="content" source="media/7138634-connector-status.png" alt-text="Microsoft Endpoint Configuration Manager connector in the admin center" lightbox="media/7138634-connector-status.png":::

> [!NOTE]
> Some information isn't available if the hierarchy is running Configuration Manager version 2006.

## Next steps

- [Enroll Configuration Manager devices into Endpoint analytics](../../analytics/enroll-configmgr.md#bkmk_cm_enroll)
- For information about the tenant attach log files, see [Troubleshoot tenant attach](troubleshoot.md).
