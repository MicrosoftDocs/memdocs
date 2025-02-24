---
# required metadata

title: Connect Intune account to managed Google Play account 
titleSuffix: Microsoft Intune
description: Learn how to connect your Intune account to your Managed Google Play account.  
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/21/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Connect your Intune account to your managed Google Play account


To manage Intune-enrolled devices with any of the supported Android Enterprise management options, you must connect your Microsoft Intune tenant to your managed Google Play account. Available management options include:  

- [Android Enterprise personally owned work profile](android-work-profile-enroll.md)
- [Android Enterprise corporate-owned work profile](android-corporate-owned-work-profile-enroll.md)
- [Android Enterprise fully managed](android-fully-managed-enroll.md)
- [Android Enterprise dedicated devices](android-kiosk-enroll.md)

This article describes how to link your accounts in the Microsoft Intune admin center. After you connect to Google Play, these common apps for Android Enterprise are added to the admin center:  

- **[Microsoft Intune](https://play.google.com/store/apps/details?id=com.microsoft.intune)** - Used for Android Enterprise fully managed, dedicated, and corporate-owned work profile scenarios.
- **[Microsoft Authenticator](https://play.google.com/store/apps/details?id=com.azure.authenticator)** - Helps you sign in to your accounts if you use two-factor verification, and is also used for Android Enterprise dedicated devices that enroll with [Microsoft Entra shared device mode](/azure/active-directory/develop/msal-shared-devices).
- **[Intune Company Portal](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal)** - Used with Android Enterprise work profile scenarios on personal devices and Intune App Protection Policies (APP). 
- **[Managed Home Screen](https://play.google.com/store/apps/details?id=com.microsoft.launcher.enterprise)** - Used for multi-app kiosk mode on Android Enterprise dedicated devices. [Learn more about Managed Home Screen](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-setup-microsoft-managed-home-screen-on-dedicated-devices/ba-p/1388060).

## Before you begin  

>[!IMPORTANT]
> As of August 2024, you can link your Microsoft Entra identity account to a Google account, instead of using an enterprise Gmail account. We recommend using your Microsoft Entra account to connect to Google Play. For more information about this change, see [Google blog: How we’re making Android Enterprise signup and access to Google services better](https://blog.google/products/android-enterprise/android-enterprise-signup-google-services/). Current Microsoft Intune tenants who have already associated a Gmail account with Intune will continue to be supported.  

- Confirm Android Enterprise availability in your country or region. For more information, see [Is Android Enterprise available in my country?](https://support.google.com/work/android/answer/6270910).  
- Confirm the Microsoft Entra account you want to use. This account is used to manage the Google Admin account and associated subscriptions, and will be associated with all Android Enterprise management tasks in your Microsoft Intune tenant.  
- Confirm that the Microsoft Entra account has a mailbox set up so that you can complete the validation process required by Google.  

## Connect accounts  
> [!TIP]
> Due to the interaction between Google and Microsoft domains, you might need to adjust your browser settings to complete this process. Make sure that portal.azure.com, play.google.com, and enterprise.google.com are in the same security zone in your browser. For instructions on how to perform these configurations in your browser, see [Per-site configuration by policy](/deployedge/per-site-configuration-by-policy).  

Complete these steps to enable Android Enterprise management options in Microsoft Intune.  

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Go to **Devices** > **Device onboarding** > **Enrollment**.   
3. Select the **Android** tab. 
4. Under **Prerequisites**, choose **Managed Google Play**.  If you're using a custom Intune role, access to this option requires organization *read* and *update* permissions.  
5. Select **I agree** to grant Microsoft permission to [send user and device information to Google](../protect/data-intune-sends-to-google.md). 
   
6. Select **Launch Google to connect now** to open the managed Google Play website. The website opens on a new tab in your browser.  
  
7. On the Google sign-in page, confirm that the prefilled Microsoft Entra account is the account you want to associate with all Android Enterprise management tasks for this tenant. 

  > [!IMPORTANT]
  > - This account is used to manage the Google Admin account and associated subscriptions, as appropriate. The Microsoft Entra account must have an active mailbox to complete the validation process required by Google.
  > - We recommend using the Microsoft Entra account you're signed into to create the Google Admin account. After you establish the connection, you can add and remove more administrators, if needed, in the Google admin console.

8. Follow the onscreen prompts to finish creating a Google Admin account.  

9. When prompted, select **Allow and create account** to allow Microsoft Intune to manage your Android Enterprise devices. 

> [!TIP]
> To choose a scope tag for your managed Google Play apps, go to **Tenant administration** > **Connectors and tokens** > **Managed Google Play** in the Microsoft Intune admin center.  Then select a scope tag to apply to all newly-approved managed Google Play apps. You must have the following permissions to interact with this area in the admin center and to remove the selected scope tag. Tenant admins, or admins who are in charge of giving admin permissions to others, can go to **Tenant Administration** > **Roles** to edit permissions.   
   >  - Android Sync - Read
   >  - Android Sync – UpdateOnBoarding  

## Disconnect your Android Enterprise administrative account  

You can disconnect the link between Microsoft Intune and Google in the admin center. Disconnecting the account disables Android Enterprise device management for your tenant. 

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) with an Intune Administrator account.  
2. [Retire](../remote-actions/devices-wipe.md#retire) all of the following devices:
    - Android Enterprise personally owned work profile devices
    - Android Enterprise corporate-owned work profile devices
    - Android Enterprise fully managed
    - Android Enterprise dedicated devices  
2. Go to **Devices** > **Enrollment**.   
3. Select the **Android** tab. 
3. Under **Prerequisites**, choose **Managed Google Play**.  
4. Select **Disconnect**.    
4. Choose **Yes** to disconnect and unenroll all Android enterprise devices from Intune.  

## Next steps

After you connect to a managed Google Play account, you can set up Microsoft Intune for these Android Enterprise scenarios:  
- [Personally owned work profile devices](android-work-profile-enroll.md).
- [Corporate-owned work profile devices](android-corporate-owned-work-profile-enroll.md). 
- [Dedicated devices](android-kiosk-enroll.md).
- [Fully managed devices](android-fully-managed-enroll.md). 
