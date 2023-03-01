---
# required metadata

title: Intune Data Warehouse application-only authentication
titleSuffix: Microsoft Intune
description: This topic describes Data Warehouse application-only authentication for Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/03/2022
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology:
ms.assetid: d7166563-6bb5-4624-b8c8-6b300a997c3a

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: jamiesil
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier3
- M365-identity-device-management
---

# Intune Data Warehouse application-only authentication

You can set up an application using Azure Active Directory (Azure AD) and authenticate to the Intune Data Warehouse. This process is useful for websites, apps, and background processes where the application should not have access to user credentials. Using the following steps, you authorize your application with Azure AD using OAuth 2.0.

## Authorization

Azure Active Directory (Azure AD) uses OAuth 2.0 to enable you to authorize access to web applications and web APIs in your Azure AD tenant. This guide shows you how to authenticate your application using C#. The OAuth 2.0 authorization code flow is described in section 4.1 of the OAuth 2.0 specification. For more information, see [Authorize access to web applications using OAuth 2.0 and Azure Active Directory](/azure/active-directory/develop/active-directory-protocols-oauth-code).


## Azure KeyVault

The following process uses a private method to process and convert an app key. This private method has been named SecureString. As an alternative, you could use Azure KeyVault to store the app key. For more information, see [Key Vault](https://azure.microsoft.com/services/key-vault/).

## Create a Web App

In this section, you provide details about the Web app you would like to point to at Intune. A web app is a client-server application. The server provides the web app, which includes the UI, content, and functionality. This type of app is separately maintained on the Web. You use Intune to grant a web app access to Intune. The data flow is initiated by the web app. 

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select  **All services** > **M365 Azure Active Directory** > **Azure Active Directory** > **App registrations**.
3. Click **New registration** to display the **Register an application** pane.
4. In the **Register an application** pane, add your app details:

    - An app name, such as *Intune App-Only Auth*.
    - The **Supported account type**. 
    - The **Redirect URI** of the application. This is the location users automatically navigate to during the authentication process. They are required to prove that they are who they say they are. For more information, see [What is application access and single sign-on with Azure Active Directory?](/azure/active-directory/active-directory-appssoaccess-whatis)

5. Click **Register**.

    >[!NOTE] 
    > Copy the **Application (client) ID** from the app pane to use later.

## Create a key (password)

In this section, Azure AD generates a key value for your app.

1. On the **App registrations** pane, select your newly created app to display the app pane.
2. Select **Certificates & secrets** near the top of the pane to display the **Certificates & secrets** pane.
3. Select **Client secrets** on the **Certificates & secrets** pane.
4. Add the key **Description** and an **Expires** duration for the key.
5. Click **Add** to save and update the application's keys.
6. You must copy the generated key value (base64 encoded).

    >[!NOTE] 
    > The key value disappears after you leave the **Certificates & secrets** pane. You cannot retrieve the key from this pane later. Copy it to use later.

## Grant application permissions

In this section, you grant permissions to the applications.

1. Select **API permissions** > **Add a permission** > **Intune** > **Application permissions**. 
5. Choose the **get_data_warehouse** option (*Get data warehouse information from Microsoft Intune*).
6. Click **Add permissions**.
7. Click **Done** from the **Add API access** pane.
8. Click **Grant admin consent** from the **API permissions** pane and click **Yes** when promoted to update any existing permissions this application already has.

## Generate token

Using Visual Studio, create a Console App (.NET Framework) project that supports the .NET Framework and uses C# as the coding language.

1. Select **File** > **New** > **Project** to display the **New Project** dialog box.
2. On the left, select **Visual C#** to display all .NET Framework projects.
3. Select **Console App (.NET Framework)**, add an app name, and then click **OK** to create the app.
4. In **Solution Explorer**, select **Program.cs** to display the code.
5. In Solution Explorer, add a reference to the assembly `System.Configuration`.
6. In the pop-up menu, select **Add** > **New item**. The **Add New Item** dialog box is displayed.
7. On the left, under **Visual C#**, select **Code**.
8. Select **Class**, change the name of the class to *IntuneDataWarehouseClass.cs*, and click **Add**.
9. Add the following code within the <code>Main</code> method:

    ``` csharp
         var applicationId = ConfigurationManager.AppSettings["appId"].ToString();
         SecureString applicationSecret = ConvertToSecureStr(ConfigurationManager.AppSettings["appKey"].ToString()); // Load as SecureString from configuration file or secret store (i.e. Azure KeyVault)
         var tenantDomain = ConfigurationManager.AppSettings["tenantDomain"].ToString();
         var msalContext = new AuthenticationContext($"https://login.windows.net/" + tenantDomain + "/oauth2/token");
    
         AuthenticationResult authResult = msalContext.AcquireTokenAsync(
             resource: "https://api.manage.microsoft.com/",
             clientCredential: new ClientCredential(
                 applicationId,
                 new SecureClientSecret(applicationSecret))).Result;
    ``` 

10. Add additional namespaces by adding the following code at the top of the code file:

    ``` csharp
     using System.Security;
     using Microsoft.IdentityModel.Clients.ActiveDirectory;
     using System.Configuration;
    ``` 

	> [!NOTE]
	> Azure Active Directory (Azure AD) Authentication Library (ADAL) and Azure AD Graph API will be deprecated. For more information, see [Update your applications to use Microsoft Authentication Library (MSAL) and Microsoft Graph API](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/update-your-applications-to-use-microsoft-authentication-library/ba-p/1257363).

11. After the <code>Main</code> method, add the following private method to process and convert the app key:

    ``` csharp
    private static SecureString ConvertToSecureStr(string appkey)
    {
        if (appkey == null)
            throw new ArgumentNullException("AppKey must not be null.");
    
        var secureAppKey = new SecureString();
    
        foreach (char c in appkey)
            secureAppKey.AppendChar(c);
    
        secureAppKey.MakeReadOnly();
        return secureAppKey;
    }
    ```

12. In the **Solution Explorer**, right-click on **References**, then select **Manage NuGet Packages**.
13. Search for *Microsoft.IdentityModel.Clients.ActiveDirectory* and install the related Microsoft NuGet package.
14. In **Solution Explorer** select and open the *App.config* file.
15. Add the <code>appSettings</code> section so that the xml appears as follows:

    ``` xml
    <?xml version="1.0" encoding="utf-8" ?>
    <configuration>
        <startup> 
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.6.1" />
        </startup>
        <appSettings>
          <add key="appId" value="App ID created from 'Create a Web App' procedure"/>
          <add key="appKey" value="Key created from 'Create a key' procedure" />
          <add key="tenantDomain" value="contoso.onmicrosoft.com"/>
        </appSettings>
    </configuration>
    ``` 

16. Update the <code>appId</code>, <code>appKey</code>, and <code>tenantDomain</code> values to match your unique app-related values.
17. Build your app.

    >[!NOTE] 
    > To see additional implementation code, see [Intune-Data-Warehouse code example](https://github.com/Microsoft/Intune-Data-Warehouse/tree/master/Samples/CSharp ).

## Next Steps
Learn more about Azure Key Vault by reviewing [What is Azure Key Vault?](/azure/key-vault/key-vault-whatis)
