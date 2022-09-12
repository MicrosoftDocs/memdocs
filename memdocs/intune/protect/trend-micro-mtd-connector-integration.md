---
# required metadata

title: Set up Trend Micro MTD integration with Intune
titleSuffix: Intune on Azure
description: "Trend Micro Mobile Security connector integration with Intune"
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/20/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: aanavath
#ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
#ms.custom:
ms.collection: M365-identity-device-management
---

# Connect Trend Micro Mobile Security with Microsoft Intune

Connect the Trend Micro MTD connector to monitor and mitigate device risk levels on Intune-managed devices. Trend Micro Mobile Security works by reporting device risk levels to Microsoft Intune. Intune then uses that information to enforce the appropriate app configuration and risk assessment policies. For more information about Trend Micro Mobile Security, see [Getting Started with Mobile Security](https://docs.trendmicro.com/en-us/enterprise/trend-micro-vision-one/mobile-security/getting-started-with_003.aspx) in the Trend Micro documentation.

This article describes the requirements and steps to connect the MTD connector in your tenant.

## Before you begin

The following subscriptions and accounts are required to integrate Trend Micro Mobile Security with Microsoft Intune.

- Microsoft Intune subscription
- Azure Active Directory (Azure AD) account with Global Administrator rights to grant the following permissions:
  - Sign in and read user profile
  - Access the directory as the signed-in user
  - Read directory data
  - Send device information to Intune
- Admin sign-in credentials to access the Trend Micro Vision One management console

### App authorization

The following authorization process happens when you connect the Trend Micro Mobile Security MTD connector:

- Allow Trend Micro Mobile Security to communicate information related to device health state back to Intune. To grant these permissions, you must use Global Administrator credentials. Granting permissions is a one-time operation. After the permissions are granted, the Global Administrator credentials aren't needed for day-to-day operation.
- Allow Trend Micro Mobile Security to sync Azure AD enrollment group membership to populate its device's database.
- Allow Trend Micro Vision One management console to use Azure AD Single Sign On (SSO).
- Allow Trend Micro Mobile Agent app to sign in using Azure AD SSO.

For more information about consent and Azure AD applications, see [Request the permissions from a directory admin](/azure/active-directory/develop/v2-permissions-and-consent#request-the-permissions-from-a-directory-admin).

## Set up Trend Micro MTD connector

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) with an Intune administrator account.
2. Go to **All services** > **Tenant administration**.
3. Select **Connectors and tokens**.
4. Under **Cross platform**, select **Mobile Threat Defense**.
5. Select **Add**.
6. For **Select the Mobile Threat Defense connector to setup**, choose **Trend Micro**.
7. Select Open the Trend Micro admin console. Keep the Microsoft Endpoint Manager tab open for later.
8. Sign in with your Azure AD account, and then follow the instructions in [Setting up Intune Integration](https://docs.trendmicro.com/en-us/enterprise/trend-micro-vision-one/mobile-security/getting-started-with_003/integration-with-int/setting-up-intune-in.aspx) (opens Trend Micro Mobile Security documentation) to complete setup.
9. After you finish setup in the Trend Micro Vision One console, return to your tab in the Microsoft Endpoint Manager admin center.
10. Under **Compliance policy evaluation**, turn on the following settings:

    - **Connect Android devices version 7.0 and above to Trend Micro**
    - **Connect iOS/iPadOS devices version 11.0 and above to Trend Micro**

These settings allow Trend Micro Mobile Security to evaluate the devices in your organization.

Configure additional settings to meet your organization’s requirements.  

11. Select **Create** to save your connector configurations.

## Next steps

- [Set up Trend Micro Mobile Agent app for enrolled devices](https://docs.microsoft.com/en-us/mem/intune/protect/mtd-apps-ios-app-configuration-policy-add-assign)
