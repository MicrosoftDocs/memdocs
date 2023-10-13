---
# required metadata

title: Overview of Apple Device Enrollment in Microsoft Intune  
titleSuffix: Microsoft Intune
description: Utilize Apple Device Enrollment to enroll and manage user-owned iOS/iPadOS devices in Microsoft Intune.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/25/2023
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: rishitasarin
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure 
ms.collection:
- tier2
- M365-identity-device-management
---

# Set up web-based device enrollment for iOS  
Set up web-based device enrollment in Microsoft Intune so that students and employees can initiate and complete device enrollment in Safari. This method of enrollment utilizes Apple Device Enrollment and enables you to manage user-owned iOS/iPadOS devices in Microsoft Intune. 

In this article, you will:   

* Set up just-in-time (JIT) registration.   
* Assign Microsoft Authenticator as a required app.   
* Create an enrollment profile for web-based enrollments.  

## Prerequisites  


## Best practices   
We recommend extra configurations to help improve the enrollment experience for device users. This section provides more information about each recommendation. 

### Deploy Company Portal web app 
Deploy the web app version of the Intune Company Portal website so that users have quick access to device status, device actions, and compliance information. The web app appears on the home screen and functions as a link to the [Company Portal website](https://portal.manage.microsoft.com/). Without the web app, devices users can still access the Company Portal website but have to open the browser and type the address into the search field. For more information about how to add a web app, see [Add web apps to Microsoft Intune](../apps/web-app.md).  

## Step 1: Set up just-in-time registration 
Create a single sign-on app extension policy to enable just-in-time (JIT) registration.  
1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. [Create an iOS/iPadOS device configuration policy](../configuration/device-features-configure.md) under **Device features** > **Category** > [**Single sign-on app extension**](../configuration/device-features-configure.md#single-sign-on-app-extension).  
3. For **SSO app extension type**, select **Microsoft Azure AD**.  
4. Add the [app bundle IDs](../configuration/bundle-ids-built-in-ios-apps.md) for any non-Microsoft apps using single sign-on (SSO). The SSO extension automatically applies to all Microsoft apps, so to avoid authentication problems, don't add Microsoft apps to your policy. 

   Don't add the Microsoft Authenticator app to the SSO extension either.  That process is done later in an app policy.     
5. Under **Additional configuration**, add the required key-value pair. Remove trailing spaces before and after the value and key. Otherwise just-in-time registration won't work.   
    * **Key**: device_registration
    * **Type**: String
    * **Value**: {{DEVICEREGISTRATION}}
4. (Recommended) Add the key-value pair that enables SSO in the Safari browser for all apps in the policy. Remove trailing spaces before and after the value and key. Otherwise just-in-time registration won't work.    
    * **Key**: browser_sso_interaction_enabled
    * **Type**: Integer
    * **Value**: 1
5. Select **Next**.  
6. For **Assignments**, assign the profile to all users, or select specific groups. 
7. Select **Next**.  
8. On the **Review + create** page, review your choices, and then select **Create** to finish creating the profile. 

## Step 2: Assign Microsoft Authenticator 
Go to **Apps** > **All apps** and assign Microsoft Authenticator to groups as a required app. 

## Step 3: Create enrollment profile  
Create an enrollment profile for devices enrolling via web-based device enrollment. The enrollment profile triggers the device user's enrollment experience, and enables them to initiate enrollment in Safari. 

1. In the Microsoft Intune admin center, go to **Devices** > **iOS/iPadOS** > **iOS/iPadOS enrollment**. 
2. Select **Enrollment types**.  
3. Select **Create profile** > **iOS/iPadOS**.  
4. On the **Basics** page, enter a name and description for the profile so that you can distinguish it from other profiles in the admin center. Device users don't see these details.  
5. Select **Next**.  
6. On the **Settings** page, for **Enrollment type**, select **Web based device enrollment**.  
7. Select **Next**.  
8. On the **Assignments** page, assign the profile to all devices, or select specific groups. Are user groups supported?  
9. Select **Next**.  
10. On the **Review + create** page, review your choices, and then select **Create** to finish creating the profile. 

Return to **Enrollment types** to see a list of your enrollment profiles. Intune applies enrollment profiles in the order you prioritize them. If a conflict occurs because a user is assigned more than one profile, Intune applies the profile with the higher priority. Drag and drop the profiles in the list to reposition them and change the order in which they're applied.   

## Step 4: Prepare employees for enrollment  
When an employee attempts to sign into a work app on their personal device, the app alerts them to the enrollment requirement and redirects them to the Company Portal website for enrollment.  Alternatively, you can provide a URL to the employee that opens the Company Portal website.  

This section describes the enrollment steps for device users. We recommend using this information in your organization's device onboarding documentation or for troubleshooting and support. 

1. Sign in to the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980) with your work or school account.  
2. Wait while Company Portal downloads a management profile on your device.
3. Go to your device settings app. Follow the onscreen prompts to install the management profile.  
4. Wait until Microsoft Authenticator is installed on the device before signing into a work or school app. The device won't be be ready for work use until MS Authenticator is on the device.  It could take a few minutes. 

Once MS Authenticator is on the device, the user can sign in and authenticate with any SSO extension approved app, such as Microsoft Teams.  

### Onboarding documentation resources    
For end user help and how-to guides, see <link to end user docs or specific articles>. You can use these articles as templates for your organization's onboarding resources.  

### Removing device from management
The volume and cryptographic keys created to manage the work data on the device are erased when the device unenrolls from Intune. 

## Troubleshooting  
For troubleshooting, see [Troubleshooting iOS/iPadOS device enrollment errors] in Microsoft Intune.


## Next steps  
For supported settings in Intune device configurations profiles, see:

   * [iOS and iPadOS device restrictions](../configuration/device-restrictions-ios.md)  
   * [iOS and iPadOS device features](../configuration/ios-device-features-settings.md)  

* For more details about Apple Device Enrollment features and functionality, see [Device Enrollment and MDM]( https://support.apple.com/guide/deployment/device-enrollment-and-mdm-depd1c27dfe6/web) on the Apple support website.  


