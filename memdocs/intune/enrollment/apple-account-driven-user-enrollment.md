---
# required metadata

title: Set up account driven Apple User Enrollment | Microsoft Docs
titleSuffix: Microsoft Intune
description: Set up account driven Apple User Enrollment for personal devices enrolling in Microsoft Intune.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/24/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: amanhaq
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Set up account driven Apple User Enrollment  

> [!IMPORTANT]
> This feature is in public preview. For more information, see [Public preview in Microsoft Intune](../fundamentals/public-preview.md).  

Set up account driven Apple User Enrollment for personal devices enrolling in Microsoft Intune. During *account driven* user enrollment, also referred to as *account-based* user enrollment, the owner of the device goes to the Settings app to initiate and carry out device enrollment.  

Account driven user enrollment provides a faster and more user-friendly enrollment experience than the [user enrollment option with Company Portal](apple-user-enrollment-with-company-portal.md). The device user triggers the enrollment profile installation simply by signing into their work account in the Settings app, and the profile installs silently in the background with minimal user interaction. Intune uses just-in-time registration, single sign-on (SSO), and the Microsoft Authenticator app for authentication to reduce the number of times that users have to sign in during enrollment and when accessing work apps.     

This article describes how to set up account driven user enrollment in Microsoft Intune. You will:   

* Set up just-in-time registration.   
* Assign Microsoft Authenticator as a required app.   
* Create an enrollment profile.   
* Create JSON configuration file to enable server discovery.   

## Prerequisites
Microsoft Intune supports account driven Apple User Enrollment on devices running iOS/iPadOS version 15 or later. Before beginning setup, complete the following tasks:    

- [Set mobile device management (MDM) authority](../fundamentals/mdm-authority-set.md)
- [Get Apple MDM Push certificate](apple-mdm-push-certificate-get.md)
- [Create Managed Apple IDs for device users](https://support.apple.com/en-us/HT210737) (Opens Apple Support website)  

If you assign an account driven user enrollment profile to device users running iOS/iPadOS 14.9 or earlier, Microsoft Intune will automatically enroll them via user enrollment with Company Portal.  

## Best practices   
We recommend extra configurations to help improve the enrollment experience for device users. This section provides more information about each recommendation.   

### Deploy Company Portal web app 
Deploy the web app version of the Intune Company Portal website so that users have quick access to device status, device actions, and compliance information. The web app appears on the employees home screen and functions as a link to the [Company Portal website](https://portal.manage.microsoft.com/). Without the web app, devices users can still access the Company Portal website but have to open the browser and type the address into the search field. For more information about how to add a web app, see [Add web apps to Microsoft Intune](../apps/web-app.md).  

### Enable federated authentication  
Use federated authentication to link Apple Business Manager with Azure AD. Apple User Enrollment typically requires you to create and provide managed Apple IDs to enrolling users. If you enable federated authentication, you won't have to create and provide unique Apple IDs to each user. Instead, a device user can sign in to their apps with the same credentials they use for their work account. For more information, see [Federated Authentication with Apple Business Manager](https://support.apple.com/en-euro/guide/apple-business-manager/axmb19317543/1/web/1) in the Apple Business Manager User Guide.  

## Step 1: Set up just-in-time registration and assign Microsoft Authenticator     
> [!IMPORTANT]
> This feature is in public preview. For more information, see [Public preview in Microsoft Intune](../fundamentals/public-preview.md).  

During account driven user enrollment, Microsoft Intune uses Microsoft Authenticator as the authentication authority for apps. Complete these steps in the Microsoft Intune admin center to configure just-in-time registration and assign Microsoft Authenticator as a required app.    

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. [Create an iOS/iPadOS device configuration policy](../configuration/device-features-configure.md) under **Device features** > **Category** > [**Single sign-on app extension**](../configuration/device-features-configure.md#single-sign-on-app-extension).  
3. For **SSO app extension type**, select **Microsoft Azure AD**.
4. Add the [app bundle IDs](../configuration/bundle-ids-built-in-ios-apps.md) for any non-Microsoft apps using single sign-on (SSO). The SSO extension automatically applies to all Microsoft apps, so to avoid authentication problems, don't add Microsoft apps to your policy. 

   Don't add the Microsoft Authenticator app to the SSO extension either.  That process is done later in an app policy.     
5. Under **Additional configuration**, add the required key-value pair. Remove trailing spaces before and after the value and key. Otherwise just-in-time registration won't work.   
    * **Key**: device_registration
    * **Type**: String
    * **Value**: {{DEVICEREGISTRATION}}
4. (Recommended) Add the key-value pair that enables SSO in the Safari browser for all apps in the policy. Remove trailing spaces before and after the value and key. Otherwise JIT registration won't work.    
    * **Key**: browser_sso_interaction_enabled
    * **Type**: Integer
    * **Value**: 1
5. Select **Next**.  
6. For **Assignments**, assign the profile to all users, or select specific groups. 
7. Select **Next**.  
8. On the **Review + create** page, review your choices, and then select **Create** to finish creating the profile.   
9. Go to **Apps** > **All apps** and assign Microsoft Authenticator to groups as a required, user-licensed volume-purchased app. For steps, see [Assign a volume-purchased app](../apps/vpp-apps-ios.md#assign-a-volume-purchased-app).   

## Step 2: Create enrollment profile 
Create an enrollment profile for devices enrolling via account driven user enrollment. The enrollment profile triggers the device user's enrollment experience, and enables them to initiate enrollment from the Settings app. 

1. In the Microsoft Intune admin center, go to **Devices** > **iOS/iPadOS** > **iOS/iPadOS enrollment**. 
2. Select **Enrollment types**.  
3. Select **Create profile** > **iOS/iPadOS**.  
4. On the **Basics** page, enter a name and description for the profile so that you can distinguish it from other profiles in the admin center. Device users don't see these details.  
5. Select **Next**.  
6. On the **Settings** page, for **Enrollment type**, select **Account driven user enrollment**.  
7. Select **Next**.  
8. On the **Assignments** page, assign the profile to all users, or select specific groups. Device groups aren't supported in user enrollment scenarios because user enrollment requires user identities.  
9. Select **Next**.  
10. On the **Review + create** page, review your choices, and then select **Create** to finish creating the profile.  

## Step 3: Create JSON configuration file to enable server discovery        
A device user can initiate enrollment by signing into an app with their work or school account.   Apple sends the enrollment request to Intune. Apple makes the request to the domain in the user's work email. For example, Apple would send the following HTTP GET request after a user signs in to their work account as *joe@contoso.com*: <br> </br>  

   `“https://contoso.com/.well-known/com.apple.remotemanagement”`  

To enable server discovery for Apple and ensure that enrollment requests go through, you have to build a JSON configuration file that contains your organization's enrollment information. Then save it on the domain where the user signs in. Apple requests the JSON file via an HTTP GET request, so use a domain that can handle HTTP GET requests. 

1. Copy and paste the JSON sample that aligns with your organization's environment. Your options:    

   Microsoft Intune:  <br> </br>
      `{"Servers":[{"Version":"mdm-byod", "BaseURL":"https://manage.microsoft.com/EnrollmentServer/PostReportDeviceInfoForUEV2?aadTenantId=*aadTenantID*" }]}` 

   Microsoft Intune for US Government: <br> </br>
      `{"Servers":[{"Version":"mdm-byod", "BaseURL":"https://manage.microsoft.us/EnrollmentServer/PostReportDeviceInfoForUEV2?aadTenantId=*aadTenantID*" }]}` 

   Microsoft Intune operated by 21 Vianet in China: <br> </br>
      `{"Servers":[{"Version":"mdm-byod", "BaseURL":"https://manage.microsoft.cn/EnrollmentServer/PostReportDeviceInfoForUEV2?aadTenantId=*aadTenantID*" }]}` 

2. Replace the *aadTenantID* variable in the URL with your organization's Azure AD tenant ID. Go to the Microsoft Intune admin center > **TBD** to find your Azure AD tenant ID and Intune Account ID. 

   The rest of the JSON sample is populated with all of the information you need, including:   
      * Version: The existing value, `mdm-byod`, is the server version.   
      * BaseURL: This URL is the location where the Intune service resides. 

3. Enter the path to your server using the following URL.  <br> </br> 

   Example formatting: 
    `“https://*yourmdmhost*.example.com/.well-known/com.apple.remotemanagement”` 

   Example of completed path: 
    `https://contoso.com/.well-known/com.apple.remotemanagement?user-identifier=joe@contoso.com1` 

4. For **Content Type**, enter **application/json**.   

5. Save the contents as a JSON file on the domain where the device user signs in.     

## Enroll personal devices     
To initiate device enrollment on a personal device, the device owner must go to the Settings app and sign in with their work or school account. If the attempt to sign into an app with their work or school account, the app will alert them to the enrollment requirement. The onscreen prompts and instructions walk them through the enrollment steps. 

This section describes the enrollment steps for device users. We recommend using this information in your organization's onboarding documentation or for troubleshooting support. 

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
11. You might receive more prompts to install work apps assigned by your organization. Select **Install** to approve installation.  

## Profile priority 

Intune applies enrollment profiles in the order you prioritize them. To change the order in which they're applied:    
1. Go back to **Enrollment types** to view your profiles.  
2. Drag and drop the profiles in the list to reorder their priority.  

If a conflict occurs because a user is assigned more than one profile, Intune applies the profile with the higher priority.  

## Removing device from management  
The volume and cryptographic keys created to manage the work data on the device are erased when the device unenrolls from Intune.  

## Next steps  
* For an overview of supported Apple User Enrollment features and management actions in Microsoft Intune, see [Overview of Apple User Enrollment in Microsoft Intune](ios-user-enrollment-supported-actions.md).  
* For troubleshooting, see [Troubleshooting iOS/iPadOS device enrollment errors in Microsoft Intune](/troubleshoot/mem/intune/device-enrollment/troubleshoot-ios-enrollment-errors).  
* For supported settings in Intune device configurations profiles, see:   

   * [iOS and iPadOS device restrictions](../configuration/device-restrictions-ios.md)
   * [iOS and iPadOS device features](../configuration/ios-device-features-settings.md)  
   * [Set up per-app Virtual Private Network (VPN)](../configuration/vpn-setting-configure-per-app.md)  