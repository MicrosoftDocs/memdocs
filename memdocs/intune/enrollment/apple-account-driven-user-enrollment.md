---
# required metadata

title: Set up account driven Apple User Enrollment | Microsoft Docs
titleSuffix: Microsoft Intune
description: Set up account driven Apple User Enrollment for personal devices enrolling in Microsoft Intune.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 11/13/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.assetid:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: rishitasarin 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Set up account driven Apple User Enrollment  

Set up account driven Apple User Enrollment for personal devices enrolling in Microsoft Intune. Account driven user enrollment provides a faster and more user-friendly enrollment experience than [user enrollment with Company Portal](apple-user-enrollment-with-company-portal.md). The device user initiates enrollment by signing into their work account in the Settings app. After the user approves device management, the enrollment profile silently installs and Intune policies are applied. Intune uses just-in-time registration and the Microsoft Authenticator app for authentication to reduce the number of times users have to sign in during enrollment and when accessing work apps.      

This article describes how to set up account driven Apple User Enrollment in Microsoft Intune. You will:   

* Set up JIT registration.   
* Create an enrollment profile.   
* Prepare employees and students for enrollment.     

## Prerequisites
Microsoft Intune supports account driven Apple User Enrollment on devices running iOS/iPadOS version 15 or later. If you assign an account driven user enrollment profile to device users running iOS/iPadOS 14.9 or earlier, Microsoft Intune will automatically enroll them via user enrollment with Company Portal.   

Before beginning setup, complete the following tasks:    

- [Set mobile device management (MDM) authority](../fundamentals/mdm-authority-set.md)
- [Get Apple MDM Push certificate](apple-mdm-push-certificate-get.md)
- [Create Managed Apple IDs for device users](https://support.apple.com/en-us/HT210737) (Opens Apple Support website)  

You also need to set up service discovery so that Apple can reach the Intune service and retrieve enrollment information. To do this, set up and publish an HTTP well-known resource file on the same domain that employees sign into. Apple retrieves the file via an HTTP GET request to `“https://contoso.com/.well-known/com.apple.remotemanagement”`, with your organization's domain in place of `contoso.com`. Publish the file on a domain that can handle HTTP GET requests.    

Create the file in JSON format, with the content type set to `application/json`.  We've provided the following JSON samples that you can copy and paste into your file. Use the one that aligns with your environment. Replace the *YourAADTenantID* variable in the base URL with your organization's Microsoft Entra tenant ID.   

   Microsoft Intune environments:  
   ```json
   {"Servers":[{"Version":"mdm-byod", "BaseURL":"https://manage.microsoft.com/EnrollmentServer/PostReportDeviceInfoForUEV2?aadTenantId=YourAADTenantID"}]}
   ```

   Microsoft Intune for US Government environments: 

   ```json      
   {"Servers":[{"Version":"mdm-byod", "BaseURL":"https://manage.microsoft.us/EnrollmentServer/PostReportDeviceInfoForUEV2?aadTenantId=YourAADTenantID"}]}
   ``` 

   Microsoft Intune operated by 21 Vianet in China environments:  

   ```json
   {"Servers":[{"Version":"mdm-byod", "BaseURL":"https://manage.microsoft.cn/EnrollmentServer/PostReportDeviceInfoForUEV2?aadTenantId=YourAADTenantID"}]}
   ```  

The rest of the JSON sample is populated with all of the information you need, including:   
* Version: The server version is `mdm-byod`.     
* BaseURL: This URL is the location where the Intune service resides.  

## Best practices   
We recommend extra configurations to help improve the enrollment experience for device users. This section provides more information about each recommendation.   

### Deploy Company Portal web app 
Deploy the web app version of the Intune Company Portal website so that users have quick access to device status, device actions, and compliance information. The web app appears on the home screen and functions as a link to the [Company Portal website](https://portal.manage.microsoft.com/). Without the web app, devices users can still access the Company Portal website but have to open the browser and type the address into the search field. For more information about how to add a web app, see [Add web apps to Microsoft Intune](../apps/web-app.md).  

### Enable federated authentication  
Apple User Enrollment requires you to create and provide managed Apple IDs to enrolling users. If you enable federated authentication, which consists of linking Apple Business Manager with Microsoft Entra ID, you don't have to create and provide unique Apple IDs to each user. Instead, a device user can sign in to their apps with the same credentials they use for their work account. For more information, see [Intro to federated authentication with Apple Business Manager](https://support.apple.com/guide/apple-business-manager/intro-to-federated-authentication-axmb19317543/1/web/1) in the Apple Business Manager User Guide.  

## Step 1: Set up just in time registration and assign Microsoft Authenticator     

Configure just-in-time registration and assign Microsoft Authenticator as a required app. For steps, see [Set up JIT registration in Intune](set-up-just-in-time-registration.md). Return to this article when you're done so you can continue to the next step.  

## Step 2: Create enrollment profile 
Create an enrollment profile for devices enrolling via account driven user enrollment. The enrollment profile triggers the device user's enrollment experience, and enables them to initiate enrollment from the Settings app. 

1. In the Microsoft Intune admin center, go to **Devices** > **Enrollment**.  
1. Select the **Apple** tab. 
1. Under **Enrollment options**, choose **Enrollment types**.  
1. Select **Create profile** > **iOS/iPadOS**.  
1. On the **Basics** page, enter a name and description for the profile so that you can distinguish it from other profiles in the admin center. Device users don't see these details.  
1. Select **Next**.  
1. On the **Settings** page, for **Enrollment type**, select how you want to enroll devices. You can choose the enrollment method or allow users to make their own choice. Their choice determines the enrollment process that Microsoft Intune carries out. It's also reflected in the device ownership attribute in Intune. To learn more about the user's experience and what they see onscreen during enrollment, see [Set up personal iOS device for work or school](../user-help/enroll-your-device-in-intune-ios.md).  

   Your options:
   
   - **Account driven user enrollment**: Assigned users who initiate enrollment are enrolled via account driven user enrollment.
     
   - **Determine based on user choice**: Assigned users who initiate enrollment can select how they want to enroll their device. Their options:  
     
       - **I own this device:** More settings appear with this selection. The user has the option to secure their entire device or only secure work-related apps and data.  
         
       - **(Company) owns this device:** The device enrolls via Apple Device Enrollment. For more information about this enrollment method, see [Device Enrollment and MDM](https://support.apple.com/guide/deployment/device-enrollment-and-mdm-depd1c27dfe6/web) on the Apple Support website.  

1. Select **Next**.  
1. On the **Assignments** page, assign the profile to all users, or select specific groups. Device groups aren't supported in user enrollment scenarios because user enrollment requires user identities.  
1. Select **Next**.  
1. On the **Review + create** page, review your choices, and then select **Create** to finish creating the profile.  

## Step 3: Prepare employees for enrollment  
To initiate device enrollment on a personal device, the device owner must go to the Settings app and sign in with their work or school account. If they attempt to sign into an app with their work or school account, the app alerts them to the enrollment requirement and tells them how to proceed. 

This section describes the enrollment steps for device users. We recommend using this information in your organization's device onboarding documentation or for troubleshooting and support. 

1. Open the **Settings** app on your device.
2. Select **General**. 
3. Select **VPN & Device Management**. 
4. Sign in with your work or school account, or with the Apple ID provided to you by your organization.   
5. Select **Sign In to iCloud**.  
6. Enter the password for the username that's shown on screen. Then select **Continue**.   
7. Select **Allow Remote Management**.  
8. Wait a few minutes while your device is configured and the management profile is installed.  
9. To confirm your device is ready to use for work, go to **VPN & Device Management**. Confirm that your work account is listed under **MANAGED ACCOUNT**.  
10. Microsoft Authenticator is required to access work apps. Wait a few minutes after enrollment for Authenticator to install on your device. An error message appears if you try to sign in to a work app without Authenticator.  
11. You might receive more prompts asking for your approval to install work apps. Select **Install** to approve installation.  

## Profile priority 

Intune applies enrollment profiles in the order you prioritize them. To change the order in which they're applied:    
1. Go back to **Enrollment types** to view your profiles.  
2. Drag and drop the profiles in the list to reorder their priority.  

If a conflict occurs because a user is assigned more than one profile, Intune applies the profile with the higher priority.  

## Removing device from management  
The volume and cryptographic keys created to manage the work data on the device are erased when the device unenrolls from Intune.  

## Known issues  
This section describes the current known issues with account driven Apple User Enrollment and Microsoft Intune.       

### Enrollment fails because of enrollment SSO application   
If the Microsoft Authenticator app is on the device before enrollment begins, enrollment will fail when the device user tries signing in with their work or school account in the Settings app. The message they receive says:  

* Title: Sign In Failed  
* Description: The Enrollment SSO application has been installed on the device.  

To get around this issue, the device user must uninstall the Microsoft Authenticator app and restart enrollment.  

## Next steps  
* For an overview of supported Apple User Enrollment features and management actions in Microsoft Intune, see [Overview of Apple User Enrollment in Microsoft Intune](ios-user-enrollment-supported-actions.md).  
* For more information about Apple User Enrollment, see [User Enrollment and MDM](https://support.apple.com/guide/deployment/user-enrollment-and-mdm-dep23db2037d/web) on the Apple support website.  
* For troubleshooting, see [Troubleshooting iOS/iPadOS device enrollment errors in Microsoft Intune](/troubleshoot/mem/intune/device-enrollment/troubleshoot-ios-enrollment-errors).  
* For supported settings in Intune device configurations profiles, see:   

   * [iOS and iPadOS device restrictions](../configuration/device-restrictions-ios.md)
   * [iOS and iPadOS device features](../configuration/ios-device-features-settings.md)  
   * [Set up per-app Virtual Private Network (VPN)](../configuration/vpn-setting-configure-per-app.md)  
