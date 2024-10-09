---
# required metadata
title: Use Microsoft Entra ID to access the Windows 365 APIs in Microsoft Graph
titleSuffix:
description: Learn how to use Microsoft Entra ID to access the Windows 365 APIs in Microsoft Graph.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 03/27/2024
ms.topic: how-to
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: cohanley
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Use Microsoft Entra ID to access the Windows 365 APIs in Microsoft Graph

The Microsoft Graph API supports Windows 365 as Beta and V1.0 workloads with specific APIs and permission roles. The Microsoft Graph API uses Microsoft Entra ID for authentication and access control. Access to the Windows 365 APIs in Microsoft Graph requires:

- An application ID with:
  - Permission to call Microsoft Entra ID and the Microsoft Graph APIs.
  - Permission scopes relevant to the specific application tasks.
- User credentials with:
  - Permission to access the Microsoft Entra tenant associated with the application.
  - Role permissions required to support the application permission scopes.
- The end user to grant permissions to the app to perform application tasks for their Azure tenant.

This article:

- Shows how to register an application with access to Microsoft Graph API and relevant permission roles.
- Describes the Windows 365 API permission roles.

For more information about API versions, see [Versioning, support, and breaking change policies for Microsoft Graph](/graph/versioning-and-support). 

## Register apps to use the Microsoft Graph API

To register an app to use Microsoft Graph API:

1. Sign in to the [Microsoft Intune admin center](https://admin.microsoft.com/) using administrative credentials. As appropriate, you may use:
    - The tenant admin account.
    - A tenant user account with the **Users can register applications setting** enabled.
2. Select **All services** > **Azure Active Directory** > **Applications** >  **App registrations**.
3. Either choose **New registration** to create a new application or choose an existing application.
4. If you chose a new registration, in the **Register an application pane**, specify the following:
    - A name for the application.
    - The supported account type.
    - A redirect URI value (optional).
5. Select **Register**.
6. On the **Application** pane:
    - Note the **Application (client) ID** value.
    - Select **API permissions**.
7. On the **API permissions** pane, select **Add a permission** > **Microsoft APIs** > **Microsoft Graph** > select the type of permissions your application requires.
8. Choose the roles required for your app by selecting the checkbox next to the relevant names. For best results, choose the fewest roles needed to implement your application. For more information about Windows 365 and other Graph API permission scopes, see [Microsoft Graph permissions reference](/graph/permissions-reference).
9. When finished, select **Add permissions** to save your changes.

You can also choose to grant permission for all tenant accounts to use the app without providing credentials. To do so, you can grant permissions and accept the confirmation prompt. When you run the application for the first time, you’re prompted to grant the app permission to perform the selected roles.

<!-- ########################## -->
## Next steps

[Authorize access to web applications using OAuth 2.0 and Microsoft Entra ID](/azure/active-directory/develop/active-directory-protocols-oauth-code).

[Getting started with Microsoft Entra authentication](/azure/devops/integrate/get-started/authentication/oauth).

[Integrating applications with Microsoft Entra ID](/azure/active-directory/develop/active-directory-integrating-applications).

[Understand OAuth 2.0](https://oauth.net/2/).
