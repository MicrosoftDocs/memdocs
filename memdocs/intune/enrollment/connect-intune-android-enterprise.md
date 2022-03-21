---
# required metadata

title: Connect your Intune account to your Managed Google Play account.
titleSuffix: Microsoft Intune
description: Learn how to connect your Intune account to your Managed Google Play account.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/01/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
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
  - M365-identity-device-management
  - highpri
---

# Connect your Intune account to your Managed Google Play account

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

To support the following Android enrollment types, you must connect your Intune tenant account to your Managed Google Play account:

- [Android Enterprise personally-owned work profile](android-work-profile-enroll.md)
- [Android Enterprise corporate-owned work profile](android-corporate-owned-work-profile-enroll.md)
- [Android Enterprise fully managed](android-fully-managed-enroll.md)
- [Android Enterprise dedicated devices](android-kiosk-enroll.md)

Refer to the following support article from Google to ensure that Android Enterprise is available in your country or region: https://support.google.com/work/android/answer/6270910

Intune makes it easier for you to configure and use Android Enterprise management. After connecting to Google Play, Intune automatically adds these four common Android Enterprise related apps to the Intune admin console:

- **[Microsoft Intune](https://play.google.com/store/apps/details?id=com.microsoft.intune)** - Used for Android Enterprise fully managed, dedicated and corporate-owned work profile scenarios.
- **[Microsoft Authenticator](https://play.google.com/store/apps/details?id=com.azure.authenticator)** - Helps you sign in to your accounts if you use two-factor verification, and is also used for Android Enterprise dedicated devices that enroll with [Azure AD Shared device mode](/azure/active-directory/develop/msal-shared-devices).
- **[Intune Company Portal](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal)** - Used for Android Enterprise personally-owned work profile scenarios, as well as App Protection Policies (APP). 
- **[Managed Home Screen](https://play.google.com/store/apps/details?id=com.microsoft.launcher.enterprise)** - Used for multi-app kiosk mode on Android Enterprise dedicated devices. [Learn more about Managed Home Screen](https://techcommunity.microsoft.com/t5/intune-customer-success/how-to-setup-microsoft-managed-home-screen-on-dedicated-devices/ba-p/1388060). 

> [!NOTE]
> Due to interaction between Google and Microsoft domains, this step may require that you adjust your browser settings.  Make sure that "portal.azure.com" and "play.google.com" are in the same security zone in your browser.

1. If you haven't already, [set the mobile device management authority](../fundamentals/mdm-authority-set.md) to **Microsoft Intune**.
2. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **Android** > **Android enrollment** > **Managed Google Play**.  If you are using a custom Intune admin role, access to option this requires Organization Read and Update permissions.
   
   ![Android enterprise enrollment screen](./media/connect-intune-android-enterprise/android-work-bind.png)

3. Choose **I agree** to grant Microsoft permission to [send user and device information to Google](../protect/data-intune-sends-to-google.md). 
   
4. Choose **Launch Google to connect now** to open the Managed Google Play website. The website opens on a new tab in your browser.
  
5. On Google's sign-in page, enter the Google account that will be associated with all Android Enterprise management tasks for this tenant. This Google account is the one that your company's IT admins share to manage and publish apps in the Google Play console. You can use an existing Google account or create a new one. The account you choose must not be associated with a G-Suite domain.

   >[!Important]
   > Be sure to use or create an Enterprise account rather than a personal GMail account. Keep in mind that the account you use should be one that is easily shared or
   > transferred in the case that the person setting up the Managed Google Play connection leaves the company or moves teams.  
    
   > [!Note]
   > If you are using the Microsoft Edge browser, click **Sign-In** in the upper right corner to sign-in to your Google account.

6. Provide your company's name for **Organization name**. For **Enterprise mobility management (EMM) provider**, **Microsoft Intune** should be displayed.

7. Agree to the Android agreement, and then choose **Confirm**. Your request will be processed.

   > [!NOTE]
   > Choose a scope tag for your Managed Google Play apps. Under this section, you can select a scope tag that will apply to all newly-approved Managed Google Play apps. You must have the following permissions to interact with this section:<ul><li>Android Sync - Read</li><li>Android Sync – UpdateOnBoarding</li></ul><p>Admins without these permissions will not be able to remove the scope tag selected on the pane. Tenant admins, or admins who are in charge of giving admin permissions to others, can update permissions in Microsoft Endpoint Manager admin center by selecting **Tenant Administration** > **Roles**.
   
      >[!Important]
   > Only link 1 Intune account to a managed Google Play account. Linking multiple accounts is unsupported and prevents basic functionality from working as expected.  

## Disconnect your Android Enterprise administrative account

You can turn off Android Enterprise enrollment and management by following these steps:

1. [Retire](../remote-actions/devices-wipe.md#retire) all the following devices:
    - Android Enterprise personally-owned work profile devices
    - Android Enterprise corporate-owned work profile devices
    - Android Enterprise fully managed
    - Android Enterprise dedicated devices
2. As an Intune administrator, sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
3. Choose **Devices** > **Android** > **Android enrollment** > **Managed Google Play** > **Disconnect**.
4. Choose **Yes** to disconnect and unenroll all Android enterprise devices from Intune.

## Next steps

After connecting to the Managed Google Play account, you can set up Android Enterprise:
- [Personally-owned work profile devices](android-work-profile-enroll.md).
- [Corporate-owned work profile devices](android-corporate-owned-work-profile-enroll.md). 
- [Dedicated devices](android-kiosk-enroll.md).
- [Fully managed devices](android-fully-managed-enroll.md).
