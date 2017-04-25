---
title: "Setup Skycure integration with Intune | Microsoft Docs"
description: "How to setup Skycure integration with Intune"
ms.custom: na
ms.date: 04/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 56634626-0f91-4e92-a00d-e986035a1897
caps.latest.revision:
author: andredm7
ms.author: andredm
manager: angrobe

---

# Setup the Skycure integration with Intune

*Applies to: System Center Configuration Manager (Current Branch)*

You need to add Skycure apps into Azure AD to have Single Sign On capabilities.

## Before you begin

### Azure AD account used to integrate Intune and Skycure

-   Make sure you have the Azure AD account properly configured in the [Skycure Management console](https://aad.skycure.com), before starting the Skycure Basic setup process.

### Full integration vs. Read-only

Skycure supports two modes of integration with Intune:

-   **Read-only integration (Basic setup):** Only inventories devices from Azure Active Directory and populates them in the Skycure console.
<br>
    -   If the **Report the health and risk of devices to Intune**, and **Also report security incidents to Intune** boxes are not selected in the Skycure Management console, the integration is read-only and therefore will never change a devices state (compliant or non-compliant) in Intune.
<br></br>
-   **Full integration:** Allows Skycure to report devices on risk and security incident details to Intune, which creates a bi-directional communication between both cloud services.

### How the Skycure apps are used with Azure AD and Intune?

-   **iOS app:** Allows end-users to sign in to Azure AD using an iOS app.

-   **Android app:** Allows end-users to sign in to Azure AD using an Android app.

-   **Management app:** This is the Skycure Azure AD multi-tenant app which enables service-to-service communication with Intune.

## To set up the read-only integration between Intune and Skycure

> [!IMPORTANT] 
> The Skycure admin credentials is an e-mail that must belong to a valid user in the Azure Active Directory, otherwise the login will fail. Skycure uses Azure Active Directory to authenticate its admin using Single Sign On (SSO).

1.  Go to [Skycure Management Console](https://aad.skycure.com).

2.  Enter your **Skycure admin credentials**, then click **Continue**.

3.  Go to **Settings**, choose **Basic Setup** under **Intune Integration**.

4.  On the **iOS App** label, click on **Add to Active Directory**.

    ![iOS app on Skycure Management console](../media/mtp/skycure-setup-1.png)

5.  Login page opens, enter your Intune credentials, then click **Accept**.

    ![iOS app Intune login prompt](../media/mtp/skycure-setup-2.png)

6.  Once the app is added into Azure AD, you can see an indication that the app was successfully added into Azure AD on the Skycure Management console.

    ![iOS app completation screen](../media/mtp/skycure-setup-3.png)

> [!NOTE] 
> Repeat the same process for the **Skycure Android** and **Management** apps.

### Add an Azure AD Security group into Skycure

You need to add an Azure AD security group that contains all devices running Skycure.

1.  Enter and select all the security groups of devices that are running Skycure, then click on **Apply changes**.

    ![Configure security group Skycure Management console](../media/mtp/skycure-setup-4.png)

Skycure syncs the devices running its Mobile Threat Defense service with the Azure AD security groups.

![Security group configuration completed on Skycure management console](../media/mtp/skycure-setup-5.png)

## Set up the full integration between Intune and Skycure

1.  Go to [Skycure Management Console](https://aad.skycure.com).

2.  Enter your **Skycure admin credentials**, then click **Continue**.

3.  Go to **Settings**, choose **Full Integration** under **Intune Integration**.

4.  Check the following settings:

    a.  Report the health and risk of device to Intune

    b.  Also report security incidents to Intune

5.  Click on **Apply changes**.

    ![Skycure full integration completed](../media/mtp/skycure-setup-6.png)

## Next steps

[Enable Skycure Mobile Threat Defense in Intune](https://docs.microsoft.com/sccm/mdm/deploy-use/enable-skycure-mobile-threat-defense-in-intune)
