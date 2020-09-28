---
title: Configure Azure AD for CMG
titleSuffix: Configuration Manager
description: Integrate the Configuration Manager site with Azure Active Directory to support the cloud management gateway.
ms.date: 09/18/2020
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: how-to
ms.assetid: 2afe572e-d268-4c77-a22d-fdca617e2255
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Configure Azure Active Directory for cloud management gateway

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

This article primarily follows the first method, but provides the necessary details for the second.

## The Azure Services wizard

Whether you're automating the process with Configuration Manager or manually importing the apps, you use the Azure Services wizard. Microsoft recommends using Configuration Manager to automate and simplify this process.

Before you start, make sure you have an Azure AD **global administrator** available.

> [!NOTE]
> If you plan to import precreated app registrations, you first need to create them in Azure AD. Start with the section below to [Manually create apps in Azure AD](#manually-create-apps-in-azure-ad). Then return to this section to run the Azure Services wizard and import the apps to Configuration Manager.

### Start the Azure Services wizard

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Cloud Services**, and select the **Azure Services** node.

1. On the _Home_ tab of the ribbon, in the _Azure Services_* group, select **Configure Azure Services**.

1. On the _Azure Services_ page of the Azure Services Wizard:

    1. Specify a **Name** for the object in Configuration Manager. This name is only to identify the connection in Configuration Manager.

    1. Specify an optional **Description** to further identify this service connection.

    1. Select the **Cloud Management** service.

1. On the _App_ page of the _Azure Services Wizard_, select the **Azure environment** for your tenant:

    - **AzurePublicCloud**: Your tenant is in the global Azure cloud.
    - **AzureUSGovernmentCloud**: Your tenant is in the Azure US Government cloud.

### Create the web (server) app registration

1. On the _App_ page of the _Azure Services Wizard_ window, for the **Web app**, select **Browse**.

    In the _Server App_ window, you have three options:

    - Use Configuration Manager to automate the creation of the app.

    - To reuse an Azure AD app that's already registered with the Configuration Manager site, select an existing app from the list. Then select **OK** to save and close the window.

    - Import the app to the site when you've worked with an Azure AD global admin to manually create the app. <!-- see new section below) -->

    The rest of this procedure follows the first method to automate and simplify the process. Select **Create**.

1. In the _Create Server Application_ window, specify the following information:

    - **Application name**: A friendly name for the app.

    - **HomePage URL**: This value isn't used by Configuration Manager, but required by Azure AD. By default this value is `https://ConfigMgrService`.  

    - **App ID URI**: This value needs to be unique in your Azure AD tenant. It's in the access token used by the Configuration Manager client to request access to the service. By default this value is `https://ConfigMgrService`.  

    - **Secret key validity period**: choose either **1 year** or **2 years** from the drop-down list. One year is the default value.

    - **Azure AD admin account**: Select **Sign in** to authenticate to Azure AD as a global administrator. Configuration Manager doesn't save these credentials. This persona doesn't require permissions in Configuration Manager, and doesn't need to be the same account that runs the Azure Services Wizard. After successfully authenticating to Azure, the page shows the **Azure AD tenant name** for reference.

1. Select **OK** to create the web app in Azure AD and close the _Create Server Application_ window.

1. In the _Server App_ window, make sure your new app is selected, then select **OK** to save and close the window.

### Create the native (client) app registration

1. On the _App_ page of the _Azure Services Wizard_ window, for the **Native Client app**, select **Browse**.

    In the _Client App_ window, you have three options:

    - Use Configuration Manager to automate the creation of the app.

    - To reuse an Azure AD app that's already registered with the Configuration Manager site, select an existing app from the list. Then select **OK** to save and close the window.

    - Import the app to the site when you've worked with an Azure AD global admin to manually create the app. <!-- see new section below) -->

    The rest of this procedure follows the first method to automate and simplify the process. Select **Create**.

1. In the _Create Client Application_ window, specify the following information:

    - **Application name**: A friendly name for the app.

    - **Azure AD admin account**: Select **Sign in** to authenticate to Azure AD as a global administrator. Configuration Manager doesn't save these credentials. This persona doesn't require permissions in Configuration Manager, and doesn't need to be the same account that runs the Azure Services Wizard. After successfully authenticating to Azure, the page shows the **Azure AD tenant name** for reference.

1. Select **OK** to create the native app in Azure AD and close the _Create Client Application_ window.

1. In the _Client App_ window, make sure your new app is selected, then select **OK** to save and close the window.

### Complete the Azure Services wizard

1. In the _Azure Services Wizard_, confirm both the **Web app** and **Native Client app** values are complete. Select **Next** to continue.

1. The _Discovery_ page of the wizard is only necessary in some scenarios. It's optional when you onboard the site to Azure AD, and not required to create the CMG. If you need it to support specific functionality in your environment, you can enable it later.

    For more information on the CMG scenarios that may require Azure AD user discovery, see [Configure client authentication: Azure AD](configure-authentication.md#azure-ad) and [Install clients using Azure AD](../../deploy/deploy-clients-cmg-azure.md).

    For more information on this discovery method, see [Configure Azure AD user discovery](../../../servers/deploy/configure/configure-discovery-methods.md#azureaadisc).

1. Review the settings and complete the wizard.

When the wizard closes, you'll see the new connection in the **Azure Services** node. You can also view the tenant and app registrations in the **Azure Active Directory Tenants** node of the Configuration Manager console.

## Manually create apps in Azure AD

If you can't use Configuration Manager to automate the creation of the apps during the Azure Service Wizard, you can use the wizard to import a previously created app. For example, if your Azure administrators require that they manually create all Azure AD app registrations, then use this process.

All of the following steps in the Azure portal require the **global administrator** role.

### Get tenant details

First, you need to make note of the **Azure AD tenant name** and **tenant ID**. These values are the first two pieces of information that you need to import the app registrations in Configuration Manager.

1. In the [Azure portal](https://portal.azure.com/), select **Azure Active Directory**.

1. In the Azure AD menu, select **Custom domain names**.

1. Note the tenant name. For example, `contoso.onmicrosoft.com`.

1. In the Azure AD menu, select **Properties**.

1. Copy the **Directory ID**. This GUID value is the tenant ID.

### Register the web (server) app

1. In the Azure AD menu, select **App registrations**. Select **New registration** to create a new app.

1. In the _Register an application_ pane, specify the following information:

    - **Name**: A friendly name for the app. For example, `CMG-ServerApp`.
    - **Supported account types**: Leave this setting as the default option, **Accounts in this organizational directory only**.
    - **Redirect URI**: Leave this value blank.

1. Select **Register** to create the app.

1. In the properties of the new app, note the following values:

    - **Display name**: This value is the friendly name for this app registration that you'll use later as the _application name_.
    - **Application (client) ID**: You'll use this GUID value later as the _client ID_.

1. In the menu of the app properties, select **Authentication**. Select the **ID tokens** option at the bottom.

1. In the menu of the app properties, select **Certificates & secrets**, then select **New client secret**.

    - **Description**: You can use any name for the secret.
    - **Expires**: Select either **In 1 year** or **In 2 years**. (The **Never** option isn't currently supported.)

    Select **Add**. Immediately note the client secret string **Value** and **Expires**. If you leave this pane, you can't retrieve the same secret again. You'll use these values later as the _secret key_ and _secret key expiry_ values.

1. If you're going to use Azure AD User Discovery in Configuration Manager, you need to adjust the permissions on this app. In the menu of the app properties, select **API permissions**. By default it should have the **User.Read** permission for the **Microsoft Graph** API, which needs to change.

    1. Select **Microsoft Graph** to enumerate the list of available API permissions, then select **Application permissions**.

    1. Under **Directory**, select **Directory.Read.All**.

    1. Under **User**, remove the **User.Read** permission.

    1. On the API permissions pane, select **Grant admin consent for...**.

1. In the menu of the app properties, select **Expose an API**.

    1. For the Application ID URI, select **Set**. Specify a URI that's unique for the tenant. You'll use this value later as the _App ID URI_. For example, `https://ConfigMgrService`.

    1. Select **Add a scope**, and specify the following required information:

        - **Scope name**: `user_impersonation`
        - **Who can consent**: Select **Admins and users**
        - **Admin consent display name**: Specify a meaningful name. For example, `Access CMG-ServerApp`
        - **Admin consent description**: Specify a meaningful description. For example, `Allow the application to access CMG-ServerApp on behalf of the signed-in user.`

    1. Select **Add scope** to save.

The web (server) app for CMG is now registered in Azure AD.

### Register the native (client) app

1. In the Azure AD menu, select **App registrations**. Select **New registration** to create a new app.

1. In the _Register an application_ pane, specify the following information:

    - **Name**: A friendly name for the app. For example, `CMG-ClientApp`.
    - **Supported account types**: Leave this setting as the default option, **Accounts in this organizational directory only**.
    - **Redirect URI**: Leave this value blank.

1. Select **Register** to create the app.

1. In the properties of the new app, note the following values:

    - **Display name**: This value is the friendly name for this app registration that you'll use later as the _application name_.
    - **Application (client) ID**: You'll use this GUID value later as the _client ID_.

1. In the menu of the app properties, select **Authentication**.

    1. In **Redirect URIs**:

        - **Type**: Select **Public client (mobile & desktops)**
        - **Redirect URI**:`ms-appx-web://Microsoft.AAD.BrokerPlugin/<ClientID>`. Specify the app's client ID GUID, for example: `ms-appx-web://Microsoft.AAD.BrokerPlugin/2afe572e-d268-4c77-a22d-fdca617e2255`. <!-- this example GUID is just the ms.assetid of this article :) -->

    1. Select the **ID tokens** option at the bottom.

1. If you're going to use Azure AD User Discovery in Configuration Manager, you need to adjust the permissions on this app. In the menu of the app properties, select **API permissions**. By default it should have the **User.Read** permission for the **Microsoft Graph** API, which needs to change.

    1. Select **Microsoft Graph** to enumerate the list of available API permissions. Expand **User**, and remove the **User.Read** permission.

    1. On the API permissions pane, select **Add a permission**. Select **Azure Active Directory Graph** from the list of Microsoft APIs. Select **Delegated permissions**. In the list of permissions, expand **Directory**, and select **Directory.Read.All**. Select **Add permissions** to save.

    1. Select **Add a permission** again. Switch to the **My APIs** tab, and select your web (server) app. For example, **CMG-ServerApp**. Make sure the **user_impersonation** permission is selected. Select **Add permissions** to save.

    1. On the API permissions pane, select **Grant admin consent for...**.

The native (client) app for CMG is now registered in Azure AD. This step also concludes the process in the Azure portal. The role of the Azure global administrator is done.

### Import the apps to Configuration Manager

After you manually register the two apps in the Azure portal, use the process in the section above for [The Azure Services wizard](#the-azure-services-wizard), but select the option to **Import** each of the apps.

These processes import metadata about the Azure AD apps into Configuration Manager. You don't require any Azure AD permissions to import these apps.

#### Import web (server) app

When you select **Import** from the _Server app_ window, it opens the _Import apps_ window. Enter the following information about the Azure AD web app that's already registered in the Azure portal:

- **Azure AD Tenant Name**: The name of your Azure AD tenant.
- **Azure AD Tenant ID**: The GUID of your Azure AD tenant.
- **Application Name**: A friendly name for the app, the display name in the app registration.
- **Client ID**: The **Application (client) ID** value of the app registration. The format is a standard GUID.
- **Secret Key**: Copy the secret key when you register the app in Azure AD and create the secret key.
- **Secret Key Expiry**: Specify the same date as from the Azure portal.
- **App ID URI**: The value is the **Application ID URI** of the app registration entry in the Azure AD portal. The format is similar to `https://ConfigMgrService`.

After entering the information, select **Verify**. Then select **OK** to close the _Import apps_ window.

#### Import native (client) app

When you select **Import** from the _Client app_ window, it opens the _Import apps_ window. Enter the following information about the Azure AD native app that's already registered in the Azure portal:

- The wizard autopopulates the Azure AD tenant name and tenant ID based on the web (server) app that you already specified.
- **Application Name**: A friendly name for the app.
- **Client ID**: The **Application (client) ID** value of the app registration. The format is a standard GUID.

After entering the information, select **Verify**. Then select **OK** to close the _Import apps_ window.

## Next steps

Continue your CMG setup by deciding which type of client authentication to use:
  
> [!div class="nextstepaction"]
> [Configure client authentication](configure-authentication.md)
