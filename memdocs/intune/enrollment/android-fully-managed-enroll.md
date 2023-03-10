---
# required metadata

title: Setup Intune enrollment for Android Enterprise fully managed devices
titleSuffix: Microsoft Intune
description: Learn how to enroll Android Enterprise fully managed devices in Intune.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 11/9/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure;seodec18
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Set up Intune enrollment of Android Enterprise fully managed devices

Use the *Android Enterprise fully managed device* solution with Microsoft Intune to enroll and manage corporate-owned devices that are associated with a single user. These types of devices are intended for work and not personal use. As an Intune admin, you can manage the whole device and enforce policy controls that aren't available with Android Enterprise work profile, such as: 

- Allow app installation from Managed Google Play only.
- Block users from uninstalling managed apps.
- Prevent users from factory resetting devices.  

You and your device users can initiate enrollment by entering or scanning an enrollment token during device setup. This article describes the prerequisites for enrollment, how to create enrollment profiles and tokens, and how to enroll devices.        

## Step 1: Prerequisites  
Complete these prerequisites to ensure a successful enrollment.     

* You must have an Intune standalone tenant, with the [mobile device management (MDM) authority set to Microsoft Intune](../fundamentals/mdm-authority-set.md).  
* Devices must:  
  - Run Android OS version 8.0 and later.
  - Run an Android build that has Google Mobile Services (GMS) connectivity. Devices must have GMS available and must be able to connect to GMS.  
  
  There is no restriction on device manufacturer/OEM if these requirements are met. 
 * Make sure Android Enterprise is supported in your region. For Android Enterprise requirements, see [Get started with Android Enterprise](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012).  
 * [Connect your Intune tenant account to your Android Enterprise account](connect-intune-android-enterprise.md).    

## Step 2: Enable corporate owned user devices  
Enable enrollment in your Intune tenant. During this process, Intune generates the default enrollment token and enrollment profile for your tenant. 

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). 
2. Select **Devices** > **Android**. 
3. Select **Android enrollment**  > **Corporate-owned, fully managed user devices**.
4. Under **Allow users to enroll corporate-owned user devices**, choose **Yes**. 
5. Under **Enrollment token**, copy either form of the enrollment token to share it with people enrolling devices.  

> [!NOTE]
> If you have an Azure AD Conditional Access policy with the following configurations, you will need to exclude the Microsoft Intune cloud app from the policy. This is because the Android setup process uses a Chrome tab to authenticate device users during enrollment. 
> * *Require a device to be marked as compliant* setting is used to grant or block access.  
> * The policy applies to **All Cloud apps**, **Android**, and **Browsers**.   

## Step 3: Create new enrollment profile  
Create a new enrollment profile for fully managed devices.  

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Android**.  
3. Select **Android enrollment**  > **Corporate-owned, fully managed user devices**.
4. Under **Allow users to enroll corporate-owned user devices**, choose **Yes**. 
5. Select **Create profile**.  
6. Enter the basics for your profile:  
    - **Name**: Type a name that you'll use when assigning the profile to the dynamic device group.
    - **Description**: Add a profile description (optional).  
7. Select **Next**. 
8. Optionally, on the **Scope tags** page, apply any desired scope tags, and then select **Next**.  
9. Review the summary of your profile, and then select **Create** to finalize it.    

Return to your list of enrollment profiles for corporate-owned devices to view your new profile. To review, make changes, or delete the profile:  

1. Select the profile.  
2. Select **Overview** to review profile essentials and delete the profile.    
3. Select **Properties** > **Edit** to make changes to the profile basics or scope tags.  
4. Select **Token** to retrieve, revoke, or export the token.  


## Step 3: Enroll devices  
> [!IMPORTANT]
>  Device users should not restart devices until enrollment is complete. If devices restart in the middle of enrollment, they may not be able to register with Microsoft Intune. Devices that restarted may appear to be enrolled, but they won't be protected by your Intune policies.  

Enroll new or factory-reset devices by providing device users with the enrollment token to type or scan. When you're ready for enrollment, share the token directly with targeted users or post it to your organization's support site for easy retrieval. The token works for all Intune-licensed users and doesn't expire. This enrollment method can't be used with device enrollment manager accounts.      

1. Turn on the device.  
2. On the **Welcome** screen, select your language.  
3. Connect to your wireless network, and then choose **NEXT**.  
4. Accept the Google Terms and conditions, and then choose **NEXT**.  
5. On the Google sign-in screen, enter **afw#setup** instead of a Gmail account, and then choose **NEXT**.
6. Choose **INSTALL** for the Android Device Policy app.  
7. Continue to install the policy. Some devices may require additional terms acceptance.
8. On the **Enroll this device** screen, allow your device to scan the QR code. Or, enter the token manually.
9. Follow the on-screen prompts to complete enrollment.   

As an Intune admin, you can scan the QR code directly from the enrollment profile to enroll a device.       
1. After you wipe the device, tap the first screen you see repeatedly to launch the QR reader.    
2. If prompted to, install a QR reader on your device. Devices running Android 9.0 and later are pre-installed with a QR reader.  
3. Scan the enrollment profile QR code and then follow the on-screen prompts to complete enrollment.  
    > [!TIP]
    > Browser zoom settings may prevent your device from scanning the QR code. Zoom in and try again if your device has difficulty scanning the code. 

## Next steps  

- [Add Android Enterprise fully managed device configuration policies](../configuration/device-restrictions-android-for-work.md#fully-managed-dedicated-and-corporate-owned-work-profile)
- [Configure app configuration policies for Android Enterprise fully managed devices](../apps/app-configuration-policies-use-android.md)
