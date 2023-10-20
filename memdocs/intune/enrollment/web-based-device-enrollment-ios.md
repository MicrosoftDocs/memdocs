---
# required metadata

title: Set up web-based device enrollment  
titleSuffix: Microsoft Intune
description: Set up web-based device enrollment to manage user-owned iOS/iPadOS devices in Microsoft Intune.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/23/2023
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

# Set up web based device enrollment for iOS  
**Applies to iOS/iPadOS**  

Set up web-based device enrollment in Microsoft Intune so that students and employees can initiate and complete device enrollment in a web browser. This method of enrollment utilizes Apple device enrollment and enables you to manage user-owned iOS/iPadOS devices in Microsoft Intune. 

In this article, you will:   

* Set up just-in-time (JIT) registration.  
* Create an enrollment profile for web-based enrollments.  
* Prepare employees and students for enrollment.  

## Prerequisites  
Microsoft Intune supports web-based device enrollment on devices running iOS/iPadOS version 15 or later. If you assign a web-based enrollment profile to device users running iOS/iPadOS 14.9 or earlier, Microsoft Intune will automatically enroll them via app-based device enrollment. App-based device enrollment requires the Company Portal app for iOS/iPadOS.     

Before beginning setup, complete the following tasks:    

- [Set mobile device management (MDM) authority](../fundamentals/mdm-authority-set.md)  
- [Get Apple MDM Push certificate](apple-mdm-push-certificate-get.md)  

## Best practices   
Deploy the web app version of Intune Company Portal so that device users have quick access to device status, device actions, and compliance information. The web app appears on the home screen and functions as a link to the [Company Portal website](https://portal.manage.microsoft.com/). For more information about how to add a web app, see [Add web apps to Microsoft Intune](../apps/web-app.md).  

Without the web app, devices users can still access the Company Portal website, but they have to open the browser and enter the website link.  

## Step 1: Set up just-in-time registration 
Create a single sign-on app extension policy to enable just-in-time (JIT) registration. For steps, see [Set up JIT registration in Intune](set-up-just-in-time-registration.md). Return to this article when you're done so you can continue to the next step.    

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
When an employee attempts to sign into a work app on their personal device, the app alerts them to the enrollment requirement and redirects them to the Company Portal website for enrollment.  Alternatively, you can provide a URL that opens the Company Portal website. It's necessary to share the link with device users in scenarios that don't utilize conditional access  because these scenarios don't redirect them to the web. The link is:  

 `portal.manage.microsoft.com`   

This section provides the high-level enrollment steps for device users. We recommend using this information in your organization's device onboarding documentation or for troubleshooting and support. 

1. Sign in to the [Company Portal website](https://portal.manage.microsoft.com) with your work or school account.  
2. Wait while Company Portal downloads a management profile on your device.
3. Go to your device settings app. Follow the onscreen prompts to install the management profile.  
4. Wait until Microsoft Authenticator is installed on the device before signing into a work or school app. The device won't be ready for work use until Authenticator is on the device, which can take a few minutes. 

After enrollment is complete, devices users can sign in and authenticate with any of the apps configured with the SSO app extension policy.   

### Removing device from management  
The volume and cryptographic keys created to manage the work data on the device are erased when the device unenrolls from Intune. 

### Onboarding documentation resources    
For end user help and how-to guides, see [Microsoft Intune user help docs](/mem/intune/user-help/). Feel free to use the articles in that doc set as templates for your organization's onboarding resources.  

For more details about Apple Device Enrollment features and functionality, see [Device Enrollment and MDM]( https://support.apple.com/guide/deployment/device-enrollment-and-mdm-depd1c27dfe6/web) on the Apple support website. 

### Troubleshooting  
For information about how to troubleshoot device enrollment issues in Microsoft Intune, see [Troubleshoot device enrollment](/troubleshoot/mem/intune/troubleshoot-device-enrollment-in-intune#device-cap-reached).  

 




