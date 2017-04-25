---
# required metadata

title: Add Skycure apps, Microsoft Authenticator app and iOS configuration policy | Microsoft Docs
description: Add Skycure apps, Microsoft Authenticator app and iOS configuration policy into Intune classic console.
keywords:
author: andredm7
ms.author: andredm
manager: angrobe
ms.date: 03/16/2017
ms.topic: article
ms.prod:
ms.service: microsoft-intune
ms.technology:
ms.assetid: 018d26f4-4a75-4e27-bb04-54f54106cb2f

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: heenamac
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-classic

---

# Add Skycure apps, Microsoft Authenticator app and iOS configuration policy

[!INCLUDE[classic-portal](../includes/classic-portal.md)]

You need to use Intune to add and deploy the Skycure apps so end-users can receive notifications when a threat is identified in their mobile devices, and to receive guidance to remediate the threats.

Additionally, you need the [Microsoft Authenticator](https://docs.microsoft.com/azure/multi-factor-authentication/end-user/microsoft-authenticator-app-how-to) so users can have their identities checked by Azure AD, and the iOS app configuration policy which signals the Skycure iOS app to use Intune and Azure AD Single Sign On (SSO) so users don’t need to type username and password every time they log in the Skycure app.

## Before you begin

-   The below steps need to be completed in the [Intune classic console](https://manage.microsoft.com/).

-   Use the same Azure AD account previously configured in the Skycure Management console, which should be the same account used to log in into the Intune classic console.

-   You need to have the Skycure integration file ready to use. This is the .zip file previously downloaded from the Skycure Management console, which contains the file **skycure\_configuration.plist** with the iOS app configuration policy parameters.

-   Make sure you’re familiar with the process of:

    -   [Adding an app into Intune](https://docs.microsoft.com/intune/deploy-use/add-apps).

    -   [Adding an iOS app configuration policy into Intune](https://docs.microsoft.com/intune/deploy-use/configure-ios-apps-with-mobile-app-configuration-policies-in-microsoft-intune).

## To add the Skycure app for Android

1.  In the Intune classic console, choose **Apps** &gt; **Add Apps** to start the Intune Software Publisher, then click **Next**.

2.  On the **Software setup** page, choose **External link**, then paste the [Skycure app for Android url](https://play.google.com/store/apps/details?id=com.skycure.skycure) under **Specify the URL**.

    ![Intune Software Publisher Specify the URL](../media/mtp/skycure-add-apps-1.png)

3.  On the **Software description** page, enter the **Publisher**, **Name** and **Description**, select the option **Display this as a featured app and highlight it in the company portal**, then click **Next**.

    ![Intune Software Publisher Software description](../media/mtp/skycure-add-apps-2.png)

4.  Click **Upload**, then **Close**.

## To add the Skycure app for iOS

1.  In the Intune classic console, choose **Apps** &gt; **Add Apps** to start the Intune Software Publisher, then click **Next**.

2.  On the **Software setup** page, choose **Managed iOS App from the App Store**, then paste the [Skycure app for iOS url](https://itunes.apple.com/us/app/skycure/id695620821?mt=8) under **Specify the URL**.

    ![Intune Software Publisher Managed iOS app](../media/mtp/skycure-add-apps-3.png)

3.  On the **Software description** page, enter the **Publisher**, **Name** and **Description**, select the option **Display this as a featured app and highlight it in the company portal**, then click **Next**.

    ![Intune Software Publisher options](../media/mtp/skycure-add-apps-4.png)

4.  On the **Requirements** page, select the option **Any** under **Mobile device type**, then click **Next**.

5.  Click **Upload**, then **Close**.

## To add the Microsoft Authenticator app for iOS

1.  In the Intune classic console, choose **Apps** &gt; **Add Apps** to start the Intune Software Publisher, then click **Next**.

2.  On the **Software setup** page, choose **Managed iOS App from the App Store**, then paste the [Microsoft Authenticator app for iOS url](https://itunes.apple.com/us/app/microsoft-authenticator/id983156458?mt=8) under **Specify the URL**.

    ![Intune Software Publisher Managed iOS app 2](../media/mtp/skycure-add-apps-5.png)

3.  On the **Software description** page, enter the **Publisher**, **Name** and **Description**, select the option **Display this as a featured app and highlight it in the company portal**, then click **Next**.

    ![Intune Software Publisher Managed iOS app 3](../media/mtp/skycure-add-apps-6.png)

4.  On the **Requirements** page, select the option **Any** under **Mobile device type**, then click **Next**.

5.  Click **Upload**, then **Close**.

## To add the Skycure iOS app configuration policy

1.  In the Intune classic console, choose **Policy** &gt; **Overview &gt; Add Policy**.

2.  In the list of policies, expand **iOS**, choose **Mobile App Configuration Policy (iOS 8.0 and later)**, then choose **Create Policy**.

    ![iOS app configuration policy](../media/mtp/skycure-add-apps-7.png)

3.  In the **General** section of the **Create Policy** page, supply a name and an optional description for the iOS app configuration policy.

    a.  Open the **skycure\_configuration.plist** file using a text editor like notepad, copy the content and paste it into the **Mobile App Configuration Policy** body, choose **Validate**, then choose **Save Policy**.

       ![iOS app configuration policy 2](../media/mtp/skycure-add-apps-8.png)

## Next steps

[Deploy Skycure apps, Microsoft Authenticator app and iOS app configuration policy](https://docs.microsoft.com/intune/deploy-use/deploy-skycure-apps-microsoft-authenticator-app-and-ios-app-configuration-policy)
