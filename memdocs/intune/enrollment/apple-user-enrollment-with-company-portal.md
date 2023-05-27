---
# required metadata

title: Set up user enrollment with Company Portal for iOS | Microsoft Docs
titleSuffix: Microsoft Intune
description: Set up the profile based Apple User Enrollment option for personal devices enrolling in Microsoft Intune.    
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
ms.custom: intune-azure;seodec18
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Set up user enrollment with Company Portal  

Set up user enrollment with Company Portal for iOS/iPadOS personal devices enrolling in Microsoft Intune. This Apple User Enrollment method, also referred to as *profile based user enrollment* gives you access to a limited but appropriate set of device management settings and actions, so you can protect work data without affecting the device user's personal data or apps. 

When the device owner attempts to sign into an app with their work or school account, Intune prompts them to enroll their device and provides instructions for next steps. The device user authenticates and initiates enrollment by signing into the Intune Company Portal app. From there, they're redirected to Safari and the device settings app, where they download and install the enrollment profile. 

This article describes how to set up an enrollment profile in the Microsoft Intune admin center for Apple User Enrollment with Company Portal. 

## Prerequisites
User enrollment with Company Portal is supported on devices running iOS version 13 or later, and iPadOS version 13.1 or later. Before beginning setup, complete the following tasks:    

- [Set mobile device management (MDM) authority](../fundamentals/mdm-authority-set.md)
- [Get Apple MDM Push certificate](apple-mdm-push-certificate-get.md)
- [Create Managed Apple IDs for device users](https://support.apple.com/en-us/HT210737) (Opens Apple Support website)  

Additionally, review the following information:    

* User enrollment requires you to provide managed Apple IDs to your enrolling users. You can create the IDs manually, but we recommend using federated authentication to link Apple Business Manager with Azure AD. This lets users use their Azure AD usernames and passwords in place of the Managed Apple IDs to sign in to their device. For more information, see [Federated Authentication with Apple Business Manager](https://support.apple.com/en-euro/guide/apple-business-manager/axmb19317543/1/web/1) (opens Apple Business Manager User Guide).  

* Apple released iPadOS in September 2019, which introduced a change that can affect Microsoft Azure Active Directory (Azure AD) and Intune customers who use Conditional Access policies in their organization. For more information about how this affects your policies and what actions to take, see [Evaluate and update Conditional Access policies after new iPadOS release](https://support.microsoft.com/topic/action-required-evaluate-and-update-conditional-access-policies-after-new-ipados-release-23795067-9048-62ad-a5bd-ad63995fc488).  

## Create enrollment profile   

> [!NOTE]
> A user enrollment profile overrides an Intune enrollment restriction policy.  

Complete these steps to create an enrollment profile for devices enrolling via user enrollment with Company Portal.  

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Go to **Devices** > **iOS/iPadOS** > **iOS/iPadOS enrollment**. 
2. Select **Enrollment types**. 
3. Select **Create profile** > **iOS/iPadOS**. 
2. On the **Basics** page, enter a name and description for the profile so that you can distinguish it from other profiles in the admin center. Device users don't see these details. 

     >[!TIP]
     > You can use the name field to create a dynamic group in Azure Active Directory, and assign devices to the enrollment profile automatically. Use the profile name to define the *enrollmentProfileName* parameter. For more information, see [Azure Active Directory dynamic groups](/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices).  

3. Select **Next**.
  
4. On the **Settings** page, select **User enrollment with Company Portal**. 
  
   Alternatively, you can select **Determine based on user choice**, which lets assigned users select the enrollment type. If you select this option, users will be presented with these options during enrollment: 

   * **I own this device**: The user will need to select whether they want to secure the entire device or only secure work-related apps and data. 
   * **(Company) owns this device**: The device will be enrolled via Device Enrollment. 

   The device user's selection determines which enrollment process is carried out. Their choice is also reflected in the device ownership attribute shown in Intune. To learn more about the user experience and what they see onscreen during enrollment, see [Set up iOS/iPadOS device access to your company resources](../user-help/enroll-your-device-in-intune-ios.md).  
    
5. Select **Next**.  

6. On the **Assignments** page, assign the profile to all users, or select specific groups. Device groups aren't supported in user enrollment scenarios because user enrollment requires user identities.  

7. Select **Next**.  

8. On the **Review + create** page, review your choices, and then select **Create** to finish creating the profile.  

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

