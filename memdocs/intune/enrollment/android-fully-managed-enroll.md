---
# required metadata

title: Set up enrollment for Android Enterprise fully managed devices
titleSuffix: Microsoft Intune
description: Learn how to set up enrollment for devices using the Android Enterprise fully managed device management solution.   
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/22/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: shthilla
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure;seodec18
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

You and your device users can initiate enrollment by entering or scanning an enrollment token during device setup. This article describes the prerequisites for enrollment and how to create enrollment profiles and tokens. At the end of this article, you will be ready to enroll devices.  

## Step 1: Prerequisites  
Complete these prerequisites to ensure a successful enrollment.     

* You must have an Intune standalone tenant, with the [mobile device management (MDM) authority set to Microsoft Intune](../fundamentals/mdm-authority-set.md).  
* Devices must:  
  - Run Android OS version 8.0 and later.
  - Run an Android build that has Google Mobile Services connectivity. 
  - Have Google Mobile Services available and be able to connect to it.  
  
  There is no restriction on device manufacturer/OEM if all three requirements are met. 
 * Make sure Android Enterprise is supported in your region. For Android Enterprise requirements, see [Get started with Android Enterprise](https://support.google.com/work/android/answer/6174145?hl=en&ref_topic=6151012).  
 * [Connect your Intune tenant account to your Android Enterprise account](connect-intune-android-enterprise.md).    
 * The Android setup process uses a Chrome tab to authenticate device users during enrollment. If you have an Azure AD Conditional Access policy with the following configurations, you will need to exclude the Microsoft Intune cloud app from the policy:  
     * *Require a device to be marked as compliant* setting is used to grant or block access.  
    * The policy applies to **All Cloud apps**, **Android**, and **Browsers**.   

## Step 2: Create new enrollment profile  
Intune automatically generates a default enrollment profile and enrollment token for fully managed devices. The default enrollment profile is named **Default Fully Managed Profile**. 

To create a new enrollment profile:       

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Enroll devices**.    
3. Select **Android enrollment**  > **Corporate-owned, fully managed user devices**.
4. Under **Allow users to enroll corporate-owned user devices**, choose **Yes**. 
5. Select **Create profile**.  
6. Enter the basics for your profile:  
    - **Name**: Give the profile a name. Note the name down for later, because you'll need it when you set up the dynamic device group.   
    - **Description**: Optionally, add a profile description.  
7. Select **Next**. 
8. Optionally, on the **Scope tags** page, apply one or more scope tags to limit profile visibility and management to select admins in Intune. Admins who are assigned roles with these scope tags and have the proper permissions will be able to access the profile. For more information about how to use scope tags, see [Use role-based access control (RBAC) and scope tags for distributed IT](../fundamentals/scope-tags.md.  
9. Select **Next**.  
10. Review the summary of your profile, and then select **Create** to finalize it.    


To review, make changes, or delete the profile:  

1. Select the profile.  
2. Select **Overview** to review profile essentials and delete the profile.    
3. Select **Properties** > **Edit** to make changes to the profile basics or scope tags.  
4. Select **Token** to retrieve, revoke, or export the token.  

## Step 3: Create dynamic Azure AD group  
Optionally, create a dynamic Azure AD group to automatically group devices based on a certain attribute or variable. In this case, we want to use the `enrollmentProfileName` property to group devices that are enrolling with the same profile. 

Add these configurations to your group:    
* **Group type**: Security
* **Membership type**: Dynamic Device  
* Add a dynamic query with the following rule: 
    * **Property**: enrollmentProfileName
    * **Operator**: Equals
    * **Value**: Enter the name of the enrollment profile you created in [Step 2: Create new enrollment profile](#step-2-create-new-enrollment-profile). 

You cannot use dynamic groups with the default enrollment profile. For more information about how to create a dynamic group with rules, see [Create a group membership rule](/azure/active-directory/enterprise-users/groups-create-rule#to-create-a-group-membership-rule).  

## Step 4: Enroll devices  
Now that you've set up the enrollment profile, token, and dynamic group, you can use any of these provisioning methods to enroll devices as fully managed:  

* Near Field Communication (NFC)
* Token string or QR code   
* Zero-touch enrollment
* Samsung Knox Mobile Enrollment  

For the next steps, including how to enroll devices with each provisioning method, see [Enroll Android Enterprise corporate-owned devices](android-dedicated-devices-fully-managed-enroll.md).  
