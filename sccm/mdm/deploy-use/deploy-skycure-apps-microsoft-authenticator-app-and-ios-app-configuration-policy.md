---
title: "Deploy Skycure apps with Intune | Microsoft Docs"
description: "Deploy Skycure apps, Microsoft Authenticator app and iOS app configuration policy in the Intune classic console."
ms.custom: na
ms.date: 04/25/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e8a7ce22-a956-4c12-adf7-30207c825fa8
caps.latest.revision:
author: andredm7
ms.author: andredm
manager: angrobe

---

# Deploy Skycure apps, Microsoft Authenticator app and iOS app configuration policy

*Applies to: System Center Configuration Manager (Current Branch)*

## Before you begin

-   The below steps need to be completed in the [Intune classic console](https://manage.microsoft.com/).

-   Use the same Azure AD account previously configured in the Skycure Management console, which should be the same account used to log in into the Intune classic console.

-   Make sure you’re familiar with the process of:

    -   [Deploying an app with Intune](https://docs.microsoft.com/intune/deploy-use/deploy-apps-in-microsoft-intune).

    -   [Deploying an iOS app configuration policy](https://docs.microsoft.com/intune/deploy-use/configure-ios-apps-with-mobile-app-configuration-policies-in-microsoft-intune).

## To deploy Skycure apps, Microsoft Authenticator app and the iOS app configuration policy

1.  In the Intune classic console, choose **Apps** &gt; **Apps** to view the list of apps that you can manage.

2.  Select the following apps:

    a.  Microsoft Authenticator

    b.  Skycure app for Android

    c.  Skycure app for iOS

       ![Intune classic console all apps to deploy](../media/mtp/skycure-deploy-app-1.png)

3.  Choose **Manage Deployments,** select the Azure AD security group that has the Skycure users, then click **Next**.

4.  On the **Deployment Action** page, select the option **Required Install** from the **Approval** drop-down list, then click **Next**.

    ![Intune classic console Deployment Action](../media/mtp/skycure-deploy-app-2.png)

5.  On the **VPN profile** page, select the option **None** from the **VPN Policy** drop-down list, then click **Next**.

6.  On the **Mobile App Configuration** page, select the iOS App Configuration Policy previously created from the **App Configuration Policy** drop-down list, then click **Finish**.

    ![Intune classic console Mobile app configuration](../media/mtp/skycure-deploy-app-3.png)

## Next steps

[Setup the Skycure integration with Intune](https://docs.microsoft.com/sccm/mdm/deploy-use/setup-the-skycure-integration-with-Intune)
