---
# required metadata

title: Set up user enrollment with Company Portal for iOS | Microsoft Docs
titleSuffix: Microsoft Intune
description: Set up the profile based Apple User Enrollment option for personal devices enrolling in Microsoft Intune.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 01/23/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: amanhaq
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Set up user enrollment with Company Portal  

>[!NOTE]
> Microsoft Intune doesn't support this enrollment profile type for newly enrolled devices. This article is only applicable to existing devices with this profile type. We recommend [account-driven user enrollment](apple-account-driven-user-enrollment.md) for new enrollments.  

Set up user enrollment with Company Portal for iOS/iPadOS personal devices enrolling in Microsoft Intune. This Apple User Enrollment method gives you access to a limited but appropriate set of device management settings and actions, so you can protect work data without affecting the device user's personal data or apps. 

When the device owner attempts to sign into an app with their work or school account, Intune prompts them to enroll their device and provides instructions for next steps. The device user authenticates and initiates enrollment by signing into the Intune Company Portal app. From there, they're redirected to Safari and the device settings app, where they download and install the enrollment profile. 

This article describes how to set up an enrollment profile in the Microsoft Intune admin center for Apple User Enrollment with Company Portal. 

## Prerequisites
User enrollment with Company Portal is supported on devices running iOS version 13 or later, and iPadOS version 13.1 or later. Before beginning setup, complete the following tasks:    

- [Set mobile device management (MDM) authority](../fundamentals/mdm-authority-set.md)
- [Get Apple MDM Push certificate](apple-mdm-push-certificate-get.md)
- [Create Managed Apple IDs for device users](https://support.apple.com/en-us/HT210737) (Opens Apple Support website)  

Additionally, review the following information:    

* Apple User Enrollment requires you to create and provide managed Apple IDs to enrolling users. If you enable federated authentication, which consists of linking Apple Business Manager with Microsoft Entra ID, you don't have to create and provide unique Apple IDs to each user. Instead, a device user can sign in to their apps with the same credentials they use for their work account. For more information, see [Intro to federated authentication with Apple Business Manager](https://support.apple.com/guide/apple-business-manager/intro-to-federated-authentication-axmb19317543/1/web/1) in the Apple Business Manager User Guide.

* Apple released iPadOS in September 2019, which introduced a change that can affect Microsoft Entra ID and Intune customers who use Conditional Access policies in their organization. For more information about how this affects your policies and what actions to take, see [Evaluate and update Conditional Access policies after new iPadOS release](https://support.microsoft.com/topic/action-required-evaluate-and-update-conditional-access-policies-after-new-ipados-release-23795067-9048-62ad-a5bd-ad63995fc488).  

## Create enrollment profile   

> [!NOTE]
> A user enrollment profile overrides an Intune enrollment restriction policy.  

Complete these steps to create an enrollment profile for devices enrolling via user enrollment with Company Portal.  

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Go to **Devices** > **By platform** > **iOS/iPadOS** > **Device onboarding** > **Enrollment**. 
3. Under **Enrollment Options**, choose **Enrollment types**. 
4. Select **Create profile** > **iOS/iPadOS**.  
5. On the **Basics** page, enter a name and description for the profile so that you can distinguish it from other profiles in the admin center. Device users don't see these details. 

     >[!TIP]
     > You can use the name field to create a dynamic group in Microsoft Entra ID, and assign devices to the enrollment profile automatically. Use the profile name to define the *enrollmentProfileName* parameter. For more information, see [Microsoft Entra dynamic groups](/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices).  

6. Select **Next**.
  
7. On the **Settings** page, select **User enrollment with Company Portal**. 
    
8. Select **Next**.  

9. On the **Assignments** page, assign the profile to all users, or select specific groups. Device groups aren't supported in user enrollment scenarios because user enrollment requires user identities.  

10. Select **Next**.  

11. On the **Review + create** page, review your choices, and then select **Create** to finish creating the profile.  

## Profile priority  

Intune applies enrollment profiles in the order you prioritize them. To change the order in which they're applied:    
1. Go back to **Enrollment types** to view your profiles.  
2. Drag and drop the profiles in the list to reorder their priority.  

If a conflict occurs because a user is assigned more than one profile, Intune applies the profile with the higher priority.  

## Removing device from management  
The volume and cryptographic keys created to manage the work data on the device are erased when the device unenrolls from Intune.  

## Next steps  
* For an overview of supported user enrollment methods and management actions, see [Overview of Apple User Enrollment in Microsoft Intune ](ios-user-enrollment-supported-actions.md).  

* For more details about Apple User Enrollment features and functionality, see [User Enrollment and MDM](https://support.apple.com/guide/deployment/user-enrollment-and-mdm-dep23db2037d/web) on the Apple support website.   

* For troubleshooting, see [Troubleshooting iOS/iPadOS device enrollment errors in Microsoft Intune](/troubleshoot/mem/intune/device-enrollment/troubleshoot-ios-enrollment-errors).  

* For supported settings in Intune device configurations profiles, see:   

   * [iOS and iPadOS device restrictions](../configuration/device-restrictions-ios.md)
   * [iOS and iPadOS device features](../configuration/ios-device-features-settings.md)  
   * [Set up per-app Virtual Private Network (VPN)](../configuration/vpn-setting-configure-per-app.md)  
