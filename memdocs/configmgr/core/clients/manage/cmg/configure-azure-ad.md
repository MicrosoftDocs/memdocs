---
title: Configure Azure AD for CMG
titleSuffix: Configuration Manager
description: Integrate the Configuration Manager site with Azure Active Directory to support the cloud management gateway.
ms.date: 04/08/2022
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: how-to
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Configure Azure Active Directory for CMG

*Applies to: Configuration Manager (current branch)*

The second primary step to set up a cloud management gateway (CMG) is to integrate the Configuration Manager site with your Azure Active Directory (Azure AD) tenant. This integration allows the site to authenticate with Azure AD, which it uses to deploy and monitor the CMG service. If you choose the Azure AD authentication method for clients in the next step, then this integration is a prerequisite for that authentication method.

> [!TIP]
> This article provides prescriptive guidance to integrate the site specifically for the cloud management gateway. For more information on this process and other uses of the **Azure Services** node in the Configuration Manager console, see [Configure Azure services](../../../servers/deploy/configure/azure-services-wizard.md).

When you integrate the site, you create app registrations in Azure AD. The CMG requires two app registrations:

- **Web app** (also referred to as a _server_ app in Configuration Manager)
- **Native app** (also referred to as a _client_ app in Configuration Manager)

There are two methods to create these apps, both of which require a **global administrator** role in Azure AD:

- Use Configuration Manager to automate the creation of the apps when you integrate the site.
- Manually create the apps in advance, and then import them when you integrate the site.

This article primarily follows the first method. For more information on the other method, see [Manually register Azure AD apps for CMG](manually-register-azure-ad-apps.md).

Before you start, make sure you have an Azure AD **global administrator** available.

> [!NOTE]
> If you plan to import precreated app registrations, you first need to create them in Azure AD. Start with the article to [Manually register Azure AD apps for CMG](manually-register-azure-ad-apps.md). Then return to this article to run the Azure Services wizard and import the apps to Configuration Manager.

## Purpose of app registrations

These two Azure AD app registrations represent the server and client side of the CMG.

- The _client app_ represents managed clients and users that connect to the CMG. It defines what resources they have access to within Azure, including the CMG itself.

- The _server app_ represents the CMG components that are hosted in Azure. It defines what resources they have access to within Azure. The server app is used to facilitate authentication and authorization from managed clients, users, and the CMG connection point to the Azure-based CMG components. This communication includes traffic to on-premises management points and software update points, initial CMG provisioning in Azure, and Azure AD discovery.

If clients use PKI-issued client authentication certificates, then the two client apps aren't used for device-centric activity. For example, software distribution targeted to a device collection. User-centric activity always uses these two app registrations for authentication and authorization purposes.

## Start the Azure Services wizard

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Azure Services** node.

1. On the _Home_ tab of the ribbon, in the _Azure Services_* group, select **Configure Azure Services**.

1. On the _Azure Services_ page of the Azure Services Wizard:

    1. Specify a **Name** for the object in Configuration Manager. This name is only to identify the connection in Configuration Manager.

    1. Specify an optional **Description** to further identify this service connection.

    1. Select the **Cloud Management** service.

1. On the _App_ page of the _Azure Services Wizard_, select the **Azure environment** for your tenant:

    - **AzurePublicCloud**: Your tenant is in the global Azure cloud.
    - **AzureUSGovernmentCloud**: Your tenant is in the Azure US Government cloud.

## Create the web (server) app registration

1. On the _App_ page of the _Azure Services Wizard_ window, for the **Web app**, select **Browse**.

1. In the _Server App_ window, select **Create** to use Configuration Manager to automate the creation of the app.

1. In the _Create Server Application_ window, specify the following information:

    - **Application name**: A friendly name for the app.

    - **HomePage URL**: This value isn't used by Configuration Manager, but required by Azure AD. By default this value is `https://ConfigMgrService`.  

    - **App ID URI**: This value needs to be unique in your Azure AD tenant. It's in the access token used by the Configuration Manager client to request access to the service. By default this value is `https://ConfigMgrService`. Change the default to one of the following recommended formats:<!-- 10617402 -->

       - `api://{tenantId}/{string}`, for example, `api://5e97358c-d99c-4558-af0c-de7774091dda/ConfigMgrService`
       - `https://{verifiedCustomerDomain}/{string}`, for example, `https://contoso.onmicrosoft.com/ConfigMgrService`

    - **Secret key validity period**: choose either **1 year** or **2 years** from the drop-down list. One year is the default value.

    - **Azure AD admin account**: Select **Sign in** to authenticate to Azure AD as a global administrator. Configuration Manager doesn't save these credentials. This persona doesn't require permissions in Configuration Manager, and doesn't need to be the same account that runs the Azure Services Wizard. After successfully authenticating to Azure, the page shows the **Azure AD tenant name** for reference.

1. Select **OK** to create the web app in Azure AD and close the _Create Server Application_ window.

1. In the _Server App_ window, make sure your new app is selected, then select **OK** to save and close the window.

## Create the native (client) app registration

1. On the _App_ page of the _Azure Services Wizard_ window, for the **Native Client app**, select **Browse**.

1. In the _Client App_ window, select **Create** to use Configuration Manager to automate the creation of the app.

1. In the _Create Client Application_ window, specify the following information:

    - **Application name**: A friendly name for the app.

    - **Azure AD admin account**: Select **Sign in** to authenticate to Azure AD as a global administrator. Configuration Manager doesn't save these credentials. This persona doesn't require permissions in Configuration Manager, and doesn't need to be the same account that runs the Azure Services Wizard. After successfully authenticating to Azure, the page shows the **Azure AD tenant name** for reference.

1. Select **OK** to create the native app in Azure AD and close the _Create Client Application_ window.

1. In the _Client App_ window, make sure your new app is selected, then select **OK** to save and close the window.

## Complete the Azure Services wizard

1. In the _Azure Services Wizard_, confirm both the **Web app** and **Native Client app** values are complete. Select **Next** to continue.

1. The _Discovery_ page of the wizard is only necessary in some scenarios. It's optional when you onboard the site to Azure AD, and not required to create the CMG. If you need it to support specific functionality in your environment, you can enable it later.

    For more information on the CMG scenarios that may require Azure AD user discovery, see [Configure client authentication: Azure AD](configure-authentication.md#azure-ad) and [Install clients using Azure AD](../../deploy/deploy-clients-cmg-azure.md).

    For more information on this discovery method, see [Configure Azure AD user discovery](../../../servers/deploy/configure/configure-discovery-methods.md#azureaadisc).

1. Review the settings and complete the wizard.

When the wizard closes, you'll see the new connection in the **Azure Services** node. You can also view the tenant and app registrations in the **Azure Active Directory Tenants** node of the Configuration Manager console.

### Disable Azure AD authentication for non-device or user tenants
<!--8537319-->

If your devices are in an Azure AD tenant that's separate from the tenant with a subscription for the CMG compute resources, you can disable authentication for tenants not associated with users and devices.

1. Open the properties of the **Cloud Management** service.

1. Switch to the **Applications** tab.

1. Select the option to **Disable Azure Active Directory authentication for this tenant**.

For more information, see [Configure Azure services](../../../servers/deploy/configure/azure-services-wizard.md#disable-authentication).

## Configure Azure resource providers

The CMG service requires that you register specific resource providers in your Azure subscription. When you deploy the CMG to a virtual machine scale set, register the following resource providers:<!--3601040-->

- Microsoft.KeyVault
- Microsoft.Storage
- Microsoft.Network
- Microsoft.Compute

> [!NOTE]
> If you previously deployed the CMG using a classic cloud service, your Azure subscription requires the following two resource providers:
>
> - Microsoft.ClassicCompute
> - Microsoft.Storage
>
> Starting in version 2203, the option to deploy a CMG as a **cloud service (classic)** is removed.<!-- 13235079 --> All CMG deployments should use a [virtual machine scale set](plan-cloud-management-gateway.md#virtual-machine-scale-sets).<!--10966586--> For more information, see [Removed and deprecated features](../../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).

Your Azure AD account needs permission to do the `/register/action` operation for the resource provider. By default, the **Contributor** and **Owner** roles include this permission.

The following steps summarize the process to register a resource provider. For more information, see [Azure resource providers and types](/azure/azure-resource-manager/management/resource-providers-and-types#azure-portal).

1. Sign in to the [Azure portal](https://portal.azure.com/).

1. On the Azure portal menu, search for **Subscriptions**. Select it from the available options.

1. Select the subscription you want to view.

1. On the left menu, under **Settings**, select **Resource providers**.

1. Find the resource provider you want to register, and select **Register**. To maintain least privileges in your subscription, only register those resource providers that you're ready to use.

## Automate with PowerShell

You can optionally automate aspects of these configurations using PowerShell.<!--6978300-->

1. Use the [Import-CMAADServerApplication](/powershell/module/configurationmanager/Import-CMAADServerApplication) cmdlet to define the Azure AD web/server app in Configuration Manager.

1. Use the [Import-CMAADClientApplication](/powershell/module/configurationmanager/Import-CMAADClientApplication) cmdlet to define the Azure AD native/client app in Configuration Manager.

1. Use the [Get-CMAADApplication](/powershell/module/configurationmanager/Get-CMAADApplication) cmdlet to get the imported app objects.

1. Then pass the app objects to the [New-CMCloudManagementAzureService](/powershell/module/configurationmanager/New-CMCloudManagementAzureService) cmdlet to create the Azure service for **Cloud Management** in Configuration Manager.

## Next steps

Continue your CMG setup by deciding which type of client authentication to use:
  
> [!div class="nextstepaction"]
> [Configure client authentication](configure-authentication.md)
