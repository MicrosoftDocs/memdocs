---
# required metadata

title: Connect Intune account to Managed Google Play account 
titleSuffix: Microsoft Intune
description: Learn how to connect your Intune account to your Managed Google Play account.  
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 01/23/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: chmaguir
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Connect your Intune account to your Managed Google Play account


To manage Intune-enrolled devices with any of the supported Android Enterprise management options, you must connect your Intune tenant to your Managed Google Play account. Those management options include:  

- [Android Enterprise personally owned work profile](android-work-profile-enroll.md)
- [Android Enterprise corporate-owned work profile](android-corporate-owned-work-profile-enroll.md)
- [Android Enterprise fully managed](android-fully-managed-enroll.md)
- [Android Enterprise dedicated devices](android-kiosk-enroll.md)

After you connect your account to Google Play, these common apps for Android Enterprise are added to the admin center:  

- **[Microsoft Intune](https://play.google.com/store/apps/details?id=com.microsoft.intune)** - Used for Android Enterprise fully managed, dedicated and corporate-owned work profile scenarios.
- **[Microsoft Authenticator](https://play.google.com/store/apps/details?id=com.azure.authenticator)** - Helps you sign in to your accounts if you use two-factor verification, and is also used for Android Enterprise dedicated devices that enroll with [Microsoft Entra shared device mode](/azure/active-directory/develop/msal-shared-devices).
- **[Intune Company Portal](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal)** - Used with Android Enterprise work profile scenarios on personal devices and Intune App Protection Policies (APP). 
- **[Managed Home Screen](https://play.google.com/store/apps/details?id=com.microsoft.launcher.enterprise)** - Used for multi-app kiosk mode on Android Enterprise dedicated devices. [Learn more about Managed Home Screen](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-setup-microsoft-managed-home-screen-on-dedicated-devices/ba-p/1388060). 

To verify Android Enterprise availability in your country or region, see [Is Android Enterprise available in my country?](https://support.google.com/work/android/answer/6270910)

> [!NOTE]
> Due to interaction between Google and Microsoft domains, this step may require that you adjust your browser settings.  Make sure that "portal.azure.com" and "play.google.com" are in the same security zone in your browser.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Go to **Devices** > **Enrollment**.   
3. Select the **Android** tab. 
3. Under **Prerequisites**, choose **Managed Google Play**.  If you're using a custom Intune admin role, access to this option requires organization *read* and *update* permissions.  
4. Select **I agree** to grant Microsoft permission to [send user and device information to Google](../protect/data-intune-sends-to-google.md). 
   
5. Select **Launch Google to connect now** to open the Managed Google Play website. The website opens on a new tab in your browser.  
  
6. On the Google sign-in page, enter the Google account you want to associate with all Android Enterprise management tasks for this tenant. This Google account will be the one that your company's IT admins share to manage and publish apps in the Google Play console. You can use an existing Google account or create a new one. The account you choose must not be associated with a G-Suite domain.  

   >[!Important]
   > Be sure to use or create an Enterprise account rather than a personal GMail account. Keep in mind that the account you use should be one that is easily shared or
   > transferred in the case that the person setting up the Managed Google Play connection leaves the company or moves teams.  
    
   > [!Note]
   > If you're using the Microsoft Edge browser, make sure to **Sign-In** to the browser with your Google account.  

7. Enter the following details:  
   * **Organization name**: Your company name. 
   * **Enterprise mobility management (EMM) provider**: Verify that **Microsoft Intune** is shown.  

8. Agree to the Android agreement, and then select **Confirm**.  

> [!TIP]
> To choose a scope tag for your Managed Google Play apps, go to **Tenant administration** > **Connectors and tokens** > **Managed Google Play** in the Microsoft Intune admin center.  Then select a scope tag to apply to all newly-approved Managed Google Play apps. You must have the following permissions to interact with this area in the admin center and to remove the selected scope tag. Tenant admins, or admins who are in charge of giving admin permissions to others, can go to **Tenant Administration** > **Roles** to edit permissions.   
   >  - Android Sync - Read
   >  - Android Sync – UpdateOnBoarding

   > [!Important]
   > Only link one Intune account to a managed Google Play account. Linking multiple accounts is unsupported and prevents basic functionality from working as expected. Disconnecting a single managed Google Play account from just one of its multilinked Intune accounts could cause the managed Google Play account to disconnect from all Intune accounts. In addition, Android Enterprise devices that already enrolled in those tenants could stop working properly. 

## Disconnect your Android Enterprise administrative account

You can turn off Android Enterprise enrollment and management by following these steps:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) with your Intune administrator account.  
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

After you connect to the Managed Google Play account, you can set up Microsoft Intune for these Android Enterprise scenarios:  
- [Personally owned work profile devices](android-work-profile-enroll.md).
- [Corporate-owned work profile devices](android-corporate-owned-work-profile-enroll.md). 
- [Dedicated devices](android-kiosk-enroll.md).
- [Fully managed devices](android-fully-managed-enroll.md).
