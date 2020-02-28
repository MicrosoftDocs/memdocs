---
# required metadata

title: Intune Data Warehouse application-only authentication
titleSuffix: Microsoft Intune
description: This topic describes Data Warehouse application-only authentication for Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/04/2019
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology:
ms.assetid: d7166563-6bb5-4624-b8c8-6b300a997c3a

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: aanavath
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Intune Data Warehouse application-only authentication

You can set up an application using Azure Active Directory (Azure AD) and authenticate to the Intune Data Warehouse. This process is useful for websites, apps, and background processes where the application should not have access to user credentials. Using the following steps, you authorize your application with Azure AD using OAuth 2.0.

## Authorization

Azure Active Directory (Azure AD) uses OAuth 2.0 to enable you to authorize access to web applications and web APIs in your Azure AD tenant. This guide shows you how to authenticate your application using C#. The OAuth 2.0 authorization code flow is described in section 4.1 of the OAuth 2.0 specification. For more information, see [Authorize access to web applications using OAuth 2.0 and Azure Active Directory](https://docs.microsoft.com/azure/active-directory/develop/active-directory-protocols-oauth-code).


## Azure KeyVault

The following process uses a private method to process and convert an app key. This private method has been named SecureString. As an alternative, you could use Azure KeyVault to store the app key. For more information, see [Key Vault](https://azure.microsoft.com/services/key-vault/).

## Create a Web App

In this section, you provide details about the Web app you would like to point to at Intune. A web app is a client-server application. The server provides the web app, which includes the UI, content, and functionality. This type of app is separately maintained on the Web. You use Intune to grant a web app access to Intune. The data flow is initiated by the web app. 

1. Sign in to the [Azure portal](https://portal.azure.com).
2. Using **Search resources, services and docs** field near the top of the Azure portal, search for **Azure Active Directory**.
3. In the dropdown menu, select **Azure Active Directory** under **Services**.
4. Select **App registrations**.
5. Click **New application registration** to display the **Create** blade.
6. In the **Create** blade, add your app details:

    - An app name, such as *Intune App-Only Auth*.
    - The **Application type**. Choose **Web app / API** to add an app that represents a web application, a web API, or both.
    - The **Sign-on URL** of the application. This is the location users automatically navigate to during the authentication process. They are required to prove that they are who they say they are. For more information, see [What is application access and single sign-on with Azure Active Directory?](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)

7. Click **Create** at the bottom of the **Create** blade.

    >[!NOTE] 
    > Copy the **Application ID** from the **Registered app** blade to use later.

## Create a key

In this section, Azure AD generates a key value for your app.

1. On the **App registrations** blade, select your newly created app to display the app blade.
2. Select **Settings** near the top of the blade to display the **Settings** blade.
3. Select **Keys** on the **Settings** blade.
4. Add the key **Description**, an **Expires** duration, and **Value** for the key.
5. Click **Save** to save and update the application's keys.
6. You must copy the generated key value (base64 encoded).

    >[!NOTE] 
    > The key value disappears after you leave the **keys** blade. You cannot retrieve the key from this blade later. Copy it to use later.

## Grant application permissions

In this section, you grant permissions to the applications.

1. Select **Required permissions** on the **Settings** blade.
2. Click **Add**.
3. Select **Add an API** to display the **Select an API** blade.
4. Select **Microsoft Intune API (MicrosoftIntuneAPI)** and then click **Select** from the **Select an API** blade. The **Select permissions** step is selected and the **Enable Access** blade is displayed.
5. Choose the **Get data warehouse information from Microsoft Intune** option from the **Application Permissions** section.
6. Click **Select** from the **Enable Access** blade.
7. Click **Done** from the **Add API access** blade.
8. Click **Grant Permissions** from the **Required permissions** blade and click **Yes** when promoted to update any existing permissions this application already has.

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
         var adalContext = new AuthenticationContext($"https://login.windows.net/" + tenantDomain + "/oauth2/token");
    
         AuthenticationResult authResult = adalContext.AcquireTokenAsync(
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
Learn more about Azure Key Vault by reviewing [What is Azure Key Vault?](https://docs.microsoft.com/azure/key-vault/key-vault-whatis)

