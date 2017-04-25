---
# required metadata

title: Configure Skycure to use Azure Active Directory Single Sign On | Microsoft Docs
description: Configure Skycure to use Azure Active Directory Single Sign On (SSO)
keywords:
author: andredm7
ms.author: andredm
manager: angrobe
ms.date: 03/16/2017
ms.topic: article
ms.prod:
ms.service: microsoft-intune
ms.technology:
ms.assetid: 34d5d359-5c7c-4225-a205-8ce890b6f890

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: heenamac
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-classic

---

# Configure Skycure to use Azure Active Directory Single Sign On (SSO)

[!INCLUDE[classic-portal](../includes/classic-portal.md)]

Azure AD SSO is used when you integrate Intune with Skycure. Here are the main benefits:

-   **Admins** can use the same credentials without having to type it again every time they log in and out from the Microsoft portals (Intune, Azure) and Skycure Management console.

-   **End-users** can use the same Azure AD credentials without having to type it again every time they log in and out from the Skycure apps.

Below are the steps to integrate Skycure with Azure Active Directory Single Sign On (SSO).

## To retrieve the Azure Active Directory Tenant ID

You need to retrieve the Azure AD Tenant ID.

1.  Go to the [Azure portal](https://portal.azure.com/) and sign in with your credentials.

2.  You can see the **Dashboard,** choose **Azure Active Directory**.

![Azure AD Dashboard](../media/mtp/skycure-sso-1.png)

1.  The **Azure Active Directory** blade opens, choose **Properties**.

![Azure AD Properties blade](../media/mtp/skycure-sso-2.png)

1.  Click on the **Copy icon** under the **Tenant Directory ID** at **Azure Active Directory Properties** blade.

> Paste the copied Directory ID value in a text file so you can use it later. The Directory ID value will be required later in the Skycure and Intune integration process.

![Azure AD Dashboard](../media/mtp/skycure-sso-3.png)

## Allow Skycure to communicate with Azure Active Directory

1.  Enter the below URL in your browser. Instead of **DIRECTORY_ID**, enter your Azure Active Directory Tenant ID previously copied to the text file.

		https://login.microsoftonline.com/<DIRECTORY_ID>/oauth2/authorize?client_id=28fd67fdb1794629a8b0dad420b697c7&prompt=admin_consent&redirect_uri=https%3A%2F%2Fmc.skycure.com%2Fapi%2Fexternal%2Fmdm%2Faad_app_consent%2Fmanagement_callback&response_type=code

2.  You need to login using your Azure Active Directory credentials. Click **Accept** to continue.

![Azure AD Dlogin page](../media/mtp/skycure-sso-4.png)

## Create an Azure AD Security group for Skycure (optional)

You might want to create a dedicated user group which contain users running Skycure (e.g Skycure users). This can be helpful when analyzing Skycure activity through the reports.

-   Learn more [how to create a group and add members in Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-groups-create-azure-portal).

> [!NOTE] 
> You can also use an existing Azure AD security group.

## Configure the Azure AD account to integrate Intune with Skycure

1.  From the [Skycure Management Console](https://aad.skycure.com/), enter the Azure Active Directory Tenant ID previously saved in the text file.

![Skycure Management console Azure AD Tenant ID field](../media/mtp/skycure-sso-5.png)

> [!IMPORTANT] 
> Skycure validates if the Azure AD Tenant ID exists by querying Azure AD, once Skycure finds it, the admin can proceed to next step, which is the Basic setup.

## Next steps

[Download Skycure iOS app configuration policy](https://docs.microsoft.com/intune/deploy-use/download-skycure-ios-app-configuration-policy)
