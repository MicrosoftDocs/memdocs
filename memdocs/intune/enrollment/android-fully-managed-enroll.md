---
# required metadata

title: Set up enrollment for Android Enterprise fully managed devices
titleSuffix: Microsoft Intune
description: Set up enrollment in Intune for devices using the Android Enterprise fully managed device management solution.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/16/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: shthilla
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Set up enrollment for Android Enterprise fully managed devices  

Set up the *Android Enterprise fully managed device* solution in Microsoft Intune to enroll and manage corporate-owned devices. A fully managed device is associated with a single user and is intended for work, not personal use. As an Intune admin, you can manage the whole device and enforce policy controls that aren't available with Android Enterprise work profile, such as: 

- Allow app installation from Managed Google Play only.
- Block users from uninstalling managed apps.
- Prevent users from factory resetting devices.  

You and your device users can initiate enrollment by entering or scanning an enrollment token during device setup. This article describes the prerequisites for enrollment and how to create enrollment profiles and tokens. At the end of this article, you can enroll devices.  

## Step 1: Prerequisites  
Complete these prerequisites to ensure a successful enrollment.     

* You must have an Intune standalone tenant, with the [mobile device management (MDM) authority set to Microsoft Intune](../fundamentals/mdm-authority-set.md).  
* Devices must:  
  - Run Android OS version 10 and later. [Intune moving to support Android 10 and later for user-based management methods in October 2024](https://techcommunity.microsoft.com/blog/intunecustomersuccess/intune-moving-to-support-android-10-and-later-for-user-based-management-methods-/4055307)
  - Run an Android build that has Google Mobile Services connectivity. 
  - Have Google Mobile Services available and be able to connect to it.  
  
  There's no restriction on device manufacturer/OEM if all three requirements are met. 
 * Make sure Android Enterprise is supported in your region. For Android Enterprise requirements, see [Get started with Android Enterprise](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012).  
 * [Connect your Intune tenant account to your Android Enterprise account](connect-intune-android-enterprise.md).    
 * The Android setup process uses a Chrome tab to authenticate device users during enrollment. If you have a Microsoft Entra Conditional Access policy with the following configurations, you must exclude the Microsoft Intune cloud app from the policy:  
   
     * *Require a device to be marked as compliant* setting is used to grant or block access.
       
     * The policy applies to **All Cloud apps**, **Android**, and **Browsers**.   

## Step 2: Create new enrollment profile  
Intune automatically generates a default enrollment profile and enrollment token for fully managed devices. The default enrollment profile is named **Default Fully Managed Profile**. 

To create a new enrollment profile:       

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).   
1. Go to **Devices** > **Enrollment**.  
1. Select the **Android** tab.  
1. Under **Android Enterprise** > **Enrollment Profiles**, choose **Corporate-owned, fully managed user devices**. 
1. Select **Create policy**.  
1. Enter the basics for your profile:  
    - **Name**: Give the profile a name. Note the name down for later, because you need it when you set up the dynamic device group.   

    - **Description**: Enter a description for the profile. This setting is optional, but recommended.    

    - **Token type**: Choose the type of token you want to use to enroll corporate fully managed devices. For more information, see [Token types](#token-types) in this article. Your options:  

      - **Corporate-owned, fully managed (default)**
        
      - **Corporate-owned, fully managed, via staging**  

    - **Token expiration date**: Only available with the staging token. Enter the date you want the token to expire, up to 65 years in the future. Acceptable date format: `MM/DD/YYYY` or `YYYY-MM-DD` The token expires on the selected date at 12:59:59 PM in the time zone it was created.   

1. Select **Next** to continue to **Scope tags**.  
1. Apply one or more scope tags to limit profile visibility and management to certain admin users in Intune. Scope tags are optional. For more information about how to use scope tags, see [Use role-based access control (RBAC) and scope tags for distributed IT](../fundamentals/scope-tags.md).  
1. Select **Next** to continue to **Review + create**.    
1. Review the summary of your profile, and then select **Create** to finalize it.  

To review, make changes, or delete the profile:  

1. Select the profile.
   
2. Select **Overview** to review profile essentials and delete the profile.    

3. Select **Properties** > **Edit** to make changes to the profile basics or scope tags.  

4. Select **Token** to retrieve, revoke, or export the token.  

<a name='step-3-create-dynamic-azure-ad-group'></a>

## Step 3: Create dynamic Microsoft Entra group  
Optionally, create a dynamic Microsoft Entra group to automatically group devices based on a certain attribute or variable. In this case, we want to use the `enrollmentProfileName` property to group devices that are enrolling with the same profile. 

Add these configurations to your group:    

* **Group type**: Security  
* **Membership type**: Dynamic Device  
* Add a dynamic query with the following rule:  
  
    * **Property**: enrollmentProfileName
    * **Operator**: Equals
    * **Value**: Enter the name of the enrollment profile you created in [Step 2: Create new enrollment profile](#step-2-create-new-enrollment-profile). 

You can't use dynamic groups with the default enrollment profile. For more information about how to create a dynamic group with rules, see [Create a group membership rule](/azure/active-directory/enterprise-users/groups-create-rule#to-create-a-group-membership-rule).  

## Step 4: Enroll devices
> [!NOTE]
> The Microsoft Authenticator app automatically installs on fully managed devices during enrollment. This app is required for this enrollment method and cannot be uninstalled.

After you set up the enrollment profile, token, and dynamic group, you can use any of these provisioning methods to enroll devices as fully managed:  

* Near Field Communication (NFC)
* Token string or QR code   
* Zero-touch enrollment
* Samsung Knox Mobile Enrollment  

For the next steps, including how to enroll devices with each provisioning method, see [Enroll Android Enterprise corporate-owned devices](android-dedicated-devices-fully-managed-enroll.md).  

## Token types   
When you create the enrollment profile in the admin center, you have to select a token type. There are two types of tokens. Each type enables a different enrollment flow.   

The default token, *corporate-owned, fully managed*, enrolls devices into Microsoft Intune as standard Android Enterprise corporate fully managed devices. This token requires you to complete pre-provisioning steps before you distribute the devices. End users complete the remaining steps on the device when they sign in with their work or school account. 

The device staging token, *Corporate-owned, fully managed, via staging*, enrolls devices into Microsoft Intune in a staging mode so that you or a third party vendor can complete all pre-provisioning steps. End users complete the last step of provisioning by signing into the Microsoft Intune app with their work or school account. Devices are ready to use upon sign-in. Intune supports device staging for Android Enterprise devices running Android 10.  

For more information, see [Device staging overview](device-staging-overview.md).  

## Replace, remove, or export token  
Select a token in the admin center to access these management options:   

- **Replace token**: Generate a new token that's nearing expiration. 

- **Revoke token**: Immediately expire the token. After you revoke it, the token is no longer usable. This option is useful if you: 

  - Accidentally share the token with an unauthorized party. 

  - Complete all enrollments and no longer need the token. 

- **Export token**: Export the JSON content of the token. You can use this option to get the JSON content required for Google Zero Touch or Knox Mobile Enrollment configuration.  

When applied, these actions don't have any effect on devices that are already enrolled.    



