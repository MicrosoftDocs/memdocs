---
# required metadata

title: Enable Apple User Enrollment for iOS/iPadOS in Microsoft Intune | Microsoft Docs
titleSuffix: Microsoft Intune
description: Enable Apple User Enrollment in Microsoft Intune for iOS/iPadOS devices.  
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 01/26/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure;seodec18
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Set up Apple User Enrollment for iOS/iPadOS 

> [!IMPORTANT]
> This feature is in public preview. For more information, see [Public preview in Microsoft Intune](../fundamentals/public-preview.md).  

Set up Intune to enroll user-owned iOS/iPadOS devices via Apple User Enrollment. *User Enrollment* enrolls devices that are a part of BYOD scenarios. Devices enrolled this way do not become supervised. Work data is securely kept on a separate volume on the device and in managed apps, away from the user's personal data.  As the admin, you get access to a limited but appropriate subset of Intune management options and restrictions to ensure that your organization's data stays safe. 

For more information about User Enrollment, see [User Enrollment and MDM](https://support.apple.com/guide/deployment/dep23db2037d/web) (opens Apple support website).  

## Prerequisites
The user enrollment option is supported on devices running iOS 13 or later, and iPadOS version 13.1 or later. Before beginning setup, complete the following tasks:    

- [Set mobile device management (MDM) authority](../fundamentals/mdm-authority-set.md)
- [Get Apple MDM Push certificate](apple-mdm-push-certificate-get.md)
- [Create Managed Apple IDs for device users](https://support.apple.com/en-us/HT210737) 

## You should know  

Review this information before you begin:    

* Apple released iPadOS in September 2019, which introduced a change that can affect Microsoft Azure Active Directory (Azure AD) and Intune customers who use Conditional Access policies in their organization. For more information about how this affects your policies and what actions to take, see [Evaluate and update Conditional Access policies after new iPadOS release](https://support.microsoft.com/topic/action-required-evaluate-and-update-conditional-access-policies-after-new-ipados-release-23795067-9048-62ad-a5bd-ad63995fc488).  

* User enrollment requires you to provide managed Apple IDs to your enrolling users. You can create the IDs manually, but we strongly recommend using federated authentication to link Apple Business Manager with Azure AD. This lets users use their Azure AD usernames and passwords in place of the Managed Apple IDs to sign in to their device. For more information, see [Federated Authentication with Apple Business Manager](https://support.apple.com/en-euro/guide/apple-business-manager/axmb19317543/1/web/1) (opens Apple Business Manager User Guide).  

## Create enrollment profile   

> [!NOTE]
> An iOS User Enrollment profile overrides an enrollment restriction policy.  

Complete these steps to create an enrollment profile for devices enrolling with the user enrollment option.  

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Go to **Devices** > **iOS/iPadOS** > **iOS/iPadOS enrollment**. 
2. Select **Enrollment types (preview)**. 
3. Select **Create profile** > **iOS/iPadOS**. In this profile,  you'll configure the enrollment experience for devices that aren't enrolled via an Apple enrollment program method, such as Apple Business Manager. You can edit this profile after you've created it.  
2. On the **Basics** page, enter a name and description for the profile so that you can distinguish it from other profiles in the admin center. Device users don't see these details. 

     >[!TIP]
     > You can use the name field to create a dynamic group in Azure Active Directory, and assign devices to the enrollment profile automatically. Use the profile name to define the *enrollmentProfileName* parameter. For more information, see [Azure Active Directory dynamic groups](/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices).  

3. Select **Next**.
  
4. On the **Settings** page, select **User enrollment**. All users assigned this profile will enroll via user enrollment. 
  
  Alternatively, you can select **Determine based on user choice**, which lets assigned users select the enrollment type. If you select this option, users will be presented with these options during enrollment: 

   * **I own this device**: The user will need to select whether they want to secure the entire device or only secure work-related apps and data. 
   * **(Company) owns this device**: The device will be enrolled via Device Enrollment. 

  The device user's selection determines which enrollment process is carried out. Their choice is also reflected in the device ownership attribute shown in Intune. To learn more about the user experience, see [Set up iOS/iPadOS device access to your company resources](../user-help/enroll-your-device-in-intune-ios.md).  
    
5. Select **Next**.  

6. On the **Assignments** page, assign the profile to all users, or select specific groups. Device groups aren't supported in user enrollment scenarios because user enrollment requires user identities.  

7. Select **Next**.  

8. On the **Review + create** page, review your choices, and then select **Create** to finish creating the profile.  

## Profile priority

After you've created more than one enrollment type profile, you can change the priority order in which they're applied. Intune applies the profiles in the order you prioritize them.  

1. Go back to **Enrollment types (preview)** to view your profiles.  
2. Drag and drop the profiles in the list to reorder their priority.  

If a conflict occurs because a user is assigned more than one profile, Intune applies the profile with the higher priority.  

## Removing device from management  
The volume and cryptographic keys created to manage the work data on the device are erased when the device unenrolls from Intune.  

## Next steps  
* Device users sign into the Intune Company Portal app with their work or school account to initiate the enrollment process. For a look at their experience, see [Set up iOS device access to your company resources](../user-help/enroll-your-device-in-intune-ios.md). Remember, if you don't set up federated authentication with Apple Business Manager, you'll need to provide Managed Apple ID credentials to your users so that they can complete enrollment. 

* For supported management actions, see [User Enrollment supported actions, passwords, and other options](ios-user-enrollment-supported-actions.md).  

* For troubleshooting, see [Troubleshooting iOS/iPadOS device enrollment errors in Microsoft Intune](/troubleshoot/mem/intune/device-enrollment/troubleshoot-ios-enrollment-errors).  

* For supported settings in Intune device configurations profiles, see:   

   * [iOS and iPadOS device restrictions](../configuration/device-restrictions-ios.md)
   * [iOS and iPadOS device features](../configuration/ios-device-features-settings.md)  
   * [Set up per-app Virtual Private Network (VPN)](../configuration/vpn-setting-configure-per-app.md)  

