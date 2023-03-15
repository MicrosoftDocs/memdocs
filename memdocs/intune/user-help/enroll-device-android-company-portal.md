---
# required metadata

title: Enroll Android device with Intune Company Portal | Microsoft Docs
description: Describes how to enroll an Android device in Intune with the Company Portal app. 
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 01/19/2022
ms.topic: end-user-help
ms.prod:
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology:
ms.assetid: 0ed3a002-7533-4001-ae24-e10b64b66620
searchScope:
 - User help

# optional metadata

ROBOTS:  
#audience:

ms.reviewer: esmich
ms.suite: ems  
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection:
- tier1
---

# Enroll your device with Company Portal  
Enroll your personal or corporate-owned Android device with Intune Company Portal to get secure access to company email, apps, and data. 

Company Portal supports devices running Android 8.0 and later, including devices secured by Samsung KNOX Standard 2.4 and later. To learn how to update your Android device, see [Check & update your Android version](https://support.google.com/android/answer/7680439).  
  

> [!VIDEO https://www.youtube.com/embed/k0Q_sGLSx6o]


> [!NOTE]
> Samsung Knox is a type of security that certain Samsung devices use for additional 
> protection outside of what native Android provides. To check if you have a Samsung Knox device, go to **Settings** > **About device**. If you don't see **Knox version** listed there, you have a native Android device.  

## Install Company Portal app  
Install the Intune Company Portal app [from Google Play](https://play.google.com/store/apps/details?id=com.microsoft.windowsintune.companyportal). See [Install Company Portal app in People's Republic of China](install-company-portal-android-china.md) for a list of stores that offer the app in People's Republic of China.

1. Tap **Home** > **Play Store**.

2. Search for and install **Intune Company Portal**.  

    ![android-search-company-portal](./media/android-search-company-portal-2101.png)  

3. When prompted about app permissions, tap **ACCEPT**.  

## Enroll device  
During enrollment, you might be asked to choose a category that best describes how you use your device. Your company support uses your answer to check the apps that you have access to.  

1. Open the Company Portal app and sign in with your work or school account.  

2. If you're prompted to accept your organization's terms and conditions, tap **ACCEPT ALL**.  

   ![Example image of the Company Portal, Terms screen, highlighting "Accept all" button.](./media/accept-terms-1911.png)  


3. Review what your organization can and can't see. Then tap **CONTINUE**.


    ![Example image of Company Portal, We care about your privacy screen, highlighting the Continue button.](./media/android-privacy-screen-1911.png)  
4. Review what to expect in the upcoming steps. Then tap **NEXT**.  

    ![Example image of Company Portal, What's next screen, highlighting the Next button.](./media/android-whats-next-1911.png)  


5. Depending on your version of Android, you might be prompted to allow access to certain parts of your device. These prompts are required by Google and not controlled by Microsoft.  

    Tap **Allow** for the following permissions:  
    * **Allow Company Portal to make and manage phone calls**: This permission enables your device to share its international mobile station equipment identity (IMEI) number with Intune, your organization's device management provider. It's safe to allow this permission. Microsoft will never make or manage phone calls.  
    * **Allow Company Portal to access your contacts**: This permission lets the Company Portal app create, use, and manage your work account.  It's safe to allow this permission. Microsoft will never access your contacts. 

    If you deny permission, you'll be prompted again the next time you sign in to Company Portal. To turn off these messages, select **Never ask again**. To manage app permissions, go to the Settings app > **Apps** > **Company Portal** > **Permissions** > **Phone**.  

6. Activate the device admin app. 

    Company Portal needs device administrator permissions to securely manage your device. Activating the app lets your organization identify possible security issues, such as repeated failed attempts to unlock your device, and respond appropriately.  

    ![Example image of the Activate device administrator screen, highlighting the activate button.](./media/activate-device-administrator-1911.png)  

> [!NOTE]
> Microsoft does not control the messaging on this screen. We understand that its phrasing can seem somewhat drastic. Company Portal can't specify which restrictions and access are relevant to your organization. If you have questions about how your organization uses the app, contact your IT support person. Go to the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980) to find your organization's contact information.  


7. Your device begins enrolling. If you're using a Samsung Knox device, you'll be prompted to review and acknowledge the ELM Agent privacy policy first.   

    ![Example image of the Samsung Knox privacy policy screen that appears during enrollment.](./media/and-enroll-7-knox-privacy-policy.png)  

8. On the **Company Access Setup** screen, check that your device is enrolled. Then tap **CONTINUE**.  

    ![Example image of Company Portal, Company Access Setup screen, showing Get your device managed is complete.](./media/update-settings-1911.png)  

9. Your organization might require you to update your device settings. Tap **RESOLVE** to adjust a setting. When you're done updating settings, tap **CONTINUE**.  

   ![Example image of Company Portal, Update device settings, highlighting Resolve and Continue buttons.](./media/resolve-settings-1911.png)  

10. When setup is complete, tap **DONE**.    

    ![Example image of Company Portal, Company Access Setup screen, showing completed setup and highlighting Done button.](./media/android-enrollment-done-1911.png) 

## Next steps  

Before you try to install a school or work app, go to **Settings** > **Security**, and turn on **Unknown sources**. If you don't turn on this option, you'll see the following message when you try to install an app: "Install blocked. For security reasons, your device is set to block installations of apps obtained from unknown sources." You can tap **Settings** on the message to go directly to **Unknown sources**.  

> [!Note]
> If your organization is using telecom expense management software, you will have an additional few steps to complete before your device is fully enrolled. Find out more [here](enroll-your-device-with-telecom-expense-management-android.md).

If you get an error while you try to enroll your device in Intune, you can [email your company support](send-logs-to-your-it-admin-by-email-android.md).  

Still need help? Contact your company support. For contact information, check the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980).  
