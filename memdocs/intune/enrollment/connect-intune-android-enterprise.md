---
# required metadata

title: Connect your Intune account to your Managed Google Play account.
titleSuffix: Microsoft Intune
description: Learn how to connect your Intune account to your Managed Google Play account.
keywords:
author: ErikjeMS 
ms.author: erikje
manager: dougeby
ms.date: 5/13/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Connect your Intune account to your Managed Google Play account

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

To support [Android Enterprise work profile](android-work-profile-enroll.md), [Android Enterprise fully managed](android-fully-managed-enroll.md), and [Android Enterprise dedicated devices](android-kiosk-enroll.md), you must connect your Intune tenant account to your Managed Google Play account.  

To make it easier for you to configure and use Android Enterprise management, upon connecting to Google Play, Intune will automatically add four common Android Enterprise related apps to the Intune admin console. The four Android Enterprise apps are the following:

- **[Microsoft Intune](https://play.google.com/store/intune/apps/details?id=com.microsoft.intune)** - Used for Android Enterprise fully managed scenarios.
- **[Microsoft Authenticator](https://play.google.com/store/intune/apps/details?id=com.azure.authenticator)** - Helps you sign-in to your accounts if you use two-factor verification.
- **[Intune Company Portal](https://play.google.com/store/intune/apps/details?id=com.microsoft.windowsintune.companyportal)** - Used for App Protection Policies (APP) and Android Enterprise work profile scenarios.
- [Managed Home Screen](https://play.google.com/store/intune/apps/details?id=com.microsoft.launcher.enterprise) - Used for Android Enterprise dedicated/kiosk scenarios.

> [!NOTE]
> Due to interaction between Google and Microsoft domains, this step may require that you adjust your browser settings.  Make sure that "portal.azure.com" and "play.google.com" are in the same security zone in your browser.

1. If you haven’t already, prepare for mobile device management by  [setting the mobile device management authority](../intune/fundamentals/mdm-authority-set.md) as **Microsoft Intune**.
2. Sign in to the [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **Android** > **Android enrollment** > **Managed Google Play**.  If you are using a custom Intune admin role, access to this requires Organization Read and Update permissions.
   
   ![Android enterprise enrollment screen](./media/connect-intune-android-enterprise/android-work-bind.png)

3. Choose **I agree** to grant Microsoft permission to [send user and device information to Google](../intune/protect/data-intune-sends-to-google.md). 
   
4. Choose **Launch Google to connect now** to open the Managed Google Play website. The website opens on a new tab in your browser.
  
5. On Google's sign in page, enter the Google account that will be associated with all Android Enterprise management tasks for this tenant. This is the Google account that your company's IT admins share to manage and publish apps in the Google Play console. You can use an existing Google account or create a new one. The account you choose must not be associated with a G-Suite domain.
    
    > [!Note]
    > If you are using the Microsoft Edge browser, click **Sign-In** in the upper right corner to sign-in to your Google account.

6. Provide your company's name for **Organization name**. For **Enterprise mobility management (EMM) provider**, **Microsoft Intune** should be displayed.

7. Agree to the Android agreement, and then choose **Confirm**. Your request will be processed.

## Disconnect your Android Enterprise administrative account

You can turn off Android Enterprise enrollment and management. To do this, you must first retire any enrolled Android Enterprise devices, including work profile devices, dedicated devices and fully managed devices. Then, choose **Disconnect** in the Intune administration console to remove all enrolled Android Enterprise work profile devices, dedicated devices and fully managed devices from enrollment. This also removes the relationship between the Managed Google Play account and Intune.

1. As an Intune administrator, sign in to the [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Choose **Devices** > **Android** > **Android enrollment** > **Managed Google Play** > **Disconnect**.
3. Choose **Yes** to disconnect and unenroll all Android enterprise devices from Intune.

## Next steps

After connecting to the Managed Google Play account, you can [set up Android Enterprise work profile devices](android-work-profile-enroll.md), 
[set up Android Enterprise dedicated devices](android-kiosk-enroll.md) and [set up Android Enterprise fully managed devices](android-fully-managed-enroll.md)
