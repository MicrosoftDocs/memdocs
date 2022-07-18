---
title: Manually register Azure AD apps
titleSuffix: Configuration Manager
description: Manually create the required apps in Azure Active Directory (Azure AD) to integrate the Configuration Manager site to support the cloud management gateway (CMG).
ms.date: 03/11/2022
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: how-to
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Manually register Azure AD apps for the CMG

*Applies to: Configuration Manager (current branch)*

The [second primary step](configure-azure-ad.md) to set up a cloud management gateway (CMG) is to integrate the Configuration Manager site with your Azure Active Directory (Azure AD) tenant. This integration allows the site to authenticate with Azure AD, which it uses to deploy and monitor the CMG service. If you can't use Configuration Manager to automate the creation of the apps during the Azure Service Wizard, you can use the wizard to import a previously created app. For example, if your Azure administrators require that they manually create all Azure AD app registrations, then use this process.

> [!TIP]
> This article provides prescriptive guidance to integrate the site specifically for the cloud management gateway. For more information on this process and other uses of the **Azure Services** node in the Configuration Manager console, see [Configure Azure services](../../../servers/deploy/configure/azure-services-wizard.md).

When you integrate the site, you create app registrations in Azure AD. The CMG requires two app registrations:

- **Web app** (also referred to as a _server_ app in Configuration Manager)
- **Native app** (also referred to as a _client_ app in Configuration Manager)

There are two methods to create these apps, both of which require a **global administrator** role in Azure AD:

- Use Configuration Manager to automate the creation of the apps when you integrate the site.
- Manually create the apps in advance, and then import them when you integrate the site.

This article provides the specific details for the second method. Pair these instructions with the procedures in the [Configure Azure AD for CMG](configure-azure-ad.md) article to complete the process.

## Get tenant details

> [!TIP]
> During this process, you'll need to note several values to use later. Open an app like Windows Notepad to paste in the values that you'll copy from the Azure Portal.

First, you need to make note of the **Azure AD tenant name** and **tenant ID**. These values are the first two pieces of information that you need to import the app registrations in Configuration Manager.

1. In the [Azure portal](https://portal.azure.com/), select **Azure Active Directory**.

1. In the Azure AD menu, select **Custom domain names**.

1. Note the tenant name. For example, `contoso.onmicrosoft.com`.

1. In the Azure AD menu, select **Properties**.

1. Copy the **Tenant ID** GUID value.

## Register the web (server) app

1. In the Azure AD menu, select **App registrations**. Select **New registration** to create a new app.

1. In the _Register an application_ pane, specify the following information:

    - **Name**: A friendly name for the app. For example, `CMG-ServerApp`.
    - **Supported account types**: Leave this setting as the default option, **Accounts in this organizational directory only**.
    - **Redirect URI**: Leave this optional value blank.

1. Select **Register** to create the app.

1. In the properties of the new app, copy the following values:

    - **Display name**: This value is the friendly name for this app registration that you'll use later as the _application name_.
    - **Application (client) ID**: You'll use this GUID value later as the _client ID_.

1. In the menu of the app properties, select **Certificates & secrets**, then select **New client secret**.

    - **Description**: You can use any name for the secret or leave it blank.
    - **Expires**: Select either **12 months** or **24 months**.

    Select **Add**. Immediately copy the client secret string **Value** and **Expires**. If you leave this pane, you can't retrieve the same secret again. You'll use these values later as the _secret key_ and _secret key expiry_ values.

1. If you're going to use Azure AD User Discovery in Configuration Manager, you need to adjust the permissions on this app. In the menu of the app properties, select **API permissions**. By default it should have the **User.Read** permission for the **Microsoft Graph** API, which needs to change.

    1. Select **Microsoft Graph** to enumerate the list of available API permissions, then select **Application permissions**.

    1. Expand **Directory**, and then select **Directory.Read.All**.

    1. Switch to **Delegated permissions**.

    1. Expand **User**, and remove the **User.Read** permission.

    1. Select **Update permissions**.

    1. On the API permissions pane, select **Grant admin consent for...**, then select **Yes**.

1. In the menu of the app properties, select **Expose an API**.

    1. For the Application ID URI, select **Set**. Specify a URI that's unique for the tenant. You'll use this value later as the _App ID URI_. Use one of the following recommended formats:<!-- 10617402 -->

       - `api://{tenantId}/{string}`, for example, `api://5e97358c-d99c-4558-af0c-de7774091dda/ConfigMgrService`
       - `https://{verifiedCustomerDomain}/{string}`, for example, `https://contoso.onmicrosoft.com/ConfigMgrService`

        Select **Save**.

    1. Select **Add a scope**, and specify the following required information:

        - **Scope name**: `user_impersonation`
        - **Who can consent**: Select **Admins and users**
        - **Admin consent display name**: Specify a meaningful name. For example, `Access CMG-ServerApp`
        - **Admin consent description**: Specify a meaningful description. For example, `Allow the application to access CMG-ServerApp on behalf of the signed-in user.`

    1. Select **Add scope** to save.

1. In the menu of the app properties, select **Manifest**. Set the **oauth2AllowIdTokenImplicitFlow** entry to **true**. For example:

    ```json
    "oauth2AllowIdTokenImplicitFlow": true,
    ```

    Select **Save**.

The web (server) app for CMG is now registered in Azure AD.



## Register the native (client) app

1. In the Azure AD menu, select **App registrations**. Select **New registration** to create a new app.

1. In the _Register an application_ pane, specify the following information:

    - **Name**: A friendly name for the app. For example, `CMG-ClientApp`.
    - **Supported account types**: Leave this setting as the default option, **Accounts in this organizational directory only**.
    - **Redirect URI**: Leave this optional value blank.

1. Select **Register** to create the app.

1. In the properties of the new app, copy the following values:

    - **Display name**: This value is the friendly name for this app registration that you'll use later as the _application name_.
    - **Application (client) ID**: You'll use this GUID value later as the _client ID_.

1. In the menu of the app properties, select **Authentication**.

    1. Under Platform configurations, select **Add a platform**.

        1. In the Configure platforms pane, select **Mobile and desktop applications**.

        1. In the **Configure Desktop + devices** pane, under Custom redirect URIs, specify `ms-appx-web://Microsoft.AAD.BrokerPlugin/<ClientID>`. Use the app's client ID GUID, for example: `ms-appx-web://Microsoft.AAD.BrokerPlugin/2afe572e-d268-4c77-a22d-fdca617e2255`. <!-- this example GUID is just the ms.assetid of this article :) -->

        1. Select **Configure**.

    1. Under Advanced settings, set **Allow public client flows** to **Yes**. Select **Save**.

1. Adjust the permissions on this app. In the menu of the app properties, select **API permissions**. By default it should have the **User.Read** delegated permission for the **Microsoft Graph** API.

    1. On the API permissions pane, select **Add a permission**.

    1. Switch to the **My APIs** tab, and select your web (server) app. For example, **CMG-ServerApp**. Select the **user_impersonation** permission, and then select **Add permissions** to save.

    1. On the API permissions pane, select **Grant admin consent for...**, and then select **Yes**.

1. In the menu of the app properties, select **Manifest**. Set the **oauth2AllowIdTokenImplicitFlow** entry to **true**. For example:

    ```json
    "oauth2AllowIdTokenImplicitFlow": true,
    ```

    Select **Save**.

The native (client) app for CMG is now registered in Azure AD. This step also concludes the process in the Azure portal. The role of the Azure global administrator is done.

## Import the apps to Configuration Manager

After you manually register the two apps in the Azure portal, use the process in the article to [Configure Azure AD for CMG](configure-azure-ad.md#start-the-azure-services-wizard), but select the option to **Import** each of the apps.

These processes import metadata about the Azure AD apps into Configuration Manager. You don't require any Azure AD permissions to import these apps.

### Import web (server) app

When you select **Import** from the _Server app_ window, it opens the _Import apps_ window. Enter the following information about the Azure AD web app that's already registered in the Azure portal:

- **Azure AD Tenant Name**: The name of your Azure AD tenant.
- **Azure AD Tenant ID**: The GUID of your Azure AD tenant.
- **Application Name**: A friendly name for the app, the display name in the app registration.
- **Client ID**: The **Application (client) ID** value of the app registration. The format is a standard GUID.
- **Secret Key**: Copy the secret key when you register the app in Azure AD and create the secret key.
- **Secret Key Expiry**: Specify the same date as from the Azure portal.
- **App ID URI**: The value is the **Application ID URI** of the app registration entry in the Azure AD portal. The format is similar to `https://ConfigMgrService`.

After entering the information, select **Verify**. Then select **OK** to close the _Import apps_ window.

> [!Important]
> When you use an imported Azure AD app, you aren't notified of an upcoming expiration date from [console notifications](../../../servers/manage/admin-console-notifications.md). <!--10568158--> 

### Import native (client) app

When you select **Import** from the _Client app_ window, it opens the _Import apps_ window. Enter the following information about the Azure AD native app that's already registered in the Azure portal:

- The wizard autopopulates the Azure AD tenant name and tenant ID based on the web (server) app that you already specified.
- **Application Name**: A friendly name for the app.
- **Client ID**: The **Application (client) ID** value of the app registration. The format is a standard GUID.

After entering the information, select **Verify**. Then select **OK** to close the _Import apps_ window.

## Next steps

After you manually register the two apps in the Azure portal, use the process in the following article to import the apps:
  
> [!div class="nextstepaction"]
> [Configure Azure AD for CMG](configure-azure-ad.md)
