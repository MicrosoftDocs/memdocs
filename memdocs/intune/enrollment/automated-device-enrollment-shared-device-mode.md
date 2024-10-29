---
# required metadata

title: Set up automated device enrollment for shared device mode 
titleSuffix: Microsoft Intune
description: Learn how to set up Apple automated device enrollment for iOS/iPadOS devices in shared device mode, a feature of Microsoft Entra.    
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 11/15/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: amanh 
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---  

# Set up enrollment for devices in shared device mode  

*Applies to iOS/iPadOS*  

Set up automated device enrollment for devices in [shared device mode](/azure/active-directory/develop/msal-ios-shared-devices). *Shared device mode* is a feature of Microsoft Entra ID that enables frontline workers to securely share a single device throughout the day, signing in and out as needed. This experience utilizes the [Microsoft Enterprise SSO plug-in](../configuration/use-enterprise-sso-plug-in-ios-ipados-with-intune.md) to limit the number of times employees have to sign in during a session.      

Corporate-owned devices purchased through Apple Business Manager or Apple School Manager can be enrolled in Intune via automated device enrollment.  Microsoft Intune supports zero-touch provisioning for devices in shared device mode, which means that the device can be set up and enrolled in Intune with minimal interaction from the frontline worker.     

In this article, you will:  

* Create an Apple enrollment policy
* Create a dynamic Microsoft Entra group for automatic grouping
* Create an assignment filter for fast provisioning
* Create a device configuration policy for single-sign on (SSO) app extension
* Assign Microsoft Authenticator app (VPP version)     

## Prerequisites 
Before you create an enrollment policy in Microsoft Intune:  

* Complete all [prerequisites for Apple Automated Device Enrollment](device-enrollment-program-enroll-ios.md#prerequisites).  
* Read [Before you begin](device-enrollment-program-enroll-ios.md#before-you-begin) for best practices and recommendations for automated device enrollment.  

## Step 1: Create an Apple enrollment policy  
Create an Apple automated device enrollment policy in Microsoft Intune for devices enrolling in shared device mode. Include these configurations:    
* **User affinity**: Enroll with Microsoft Entra ID shared mode  
* **Locked enrollment**: Yes  
* **Apply device name template**: Yes (optional)  
* **Device Name Template** (optional): {{DEVICETYPE}}-{{SERIAL}}   
* **Toggle All** (optional): Hide 

 Although optional, we recommend applying a device name template with the recommended formatting. You can also hide all or some Setup Assistant screens to speed up provisioning and user onboarding. When you're done configuring the rest of the enrollment profile, assign it to devices. 

 For more information about how-to create an enrollment policy, see [Create an Apple enrollment profile](device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile).  

<a name='step-2-create-a-dynamic-azure-ad-group'></a>

## Step 2: Create a dynamic Microsoft Entra group
Create a dynamic Microsoft Entra group using the `enrollmentProfileName` property to automatically group devices that enroll with a specific enrollment policy. In this case, we want to group devices that are in share device mode and enrolling with the policy you created in Step 1. Include these configurations in your dynamic group policy:  
* **Group type**: Security
* **Membership type**: Dynamic Device  
* Add a dynamic query with the following rule: 
    * **Property**: enrollmentProfileName
    * **Operator**: Equals
    * **Value**: Enter the name of the enrollment policy you created for devices in  shared device mode. 

For more information about how to create a dynamic group for shared devices in Microsoft Entra ID, see [Create a group membership rule](/azure/active-directory/enterprise-users/groups-create-rule#to-create-a-group-membership-rule).  

## Step 3: Create an assignment filter

Create an assignment filter to quickly target devices assigned to your enrollment policy. Add a rule with the following parameters:   
* **Property**: enrollmentProfileName  
* **Operator**: Equals
* **Value**: Enter the name of the enrollment profile you created for devices in shared device mode.  

For more information about how to create an assignment filter rule, see [Create a filter](../fundamentals/filters.md#prerequisites).  

## Step 4: Create a device configuration policy
Configure a single-sign on (SSO) app extension policy for shared device mode. Create a device configuration policy and include these configurations:   
* **Profile type**: Templates
* **Template name**: Device features
* Expand **Single sign-on app extension**, and then configure:    
    * **SSO app extension type**: Microsoft Entra ID
    * **Enable shared device mode**: Yes  
    * **Key**: device_registration
    * **Type**: String
    * **Value**: {{DEVICEREGISTRATION}} 

You can configure the rest of the policy to meet your organization's needs. When you're done configuring the policy, assign it to **All devices** and then add the assignment filter you created in [Step 3](#step-3-create-an-assignment-filter).  

For more information about creating an SSO app extension policy, see:  
* [Create a device configuration profile](../configuration/device-features-configure.md#create-the-profile)  
* [Single-sign on (SSO) app extension settings](../configuration/device-features-configure.md#single-sign-on-sso)  

## Step 5: Assign the Microsoft Authenticator app
Assign the Microsoft Authenticator app to targeted devices. Assign the app as *required* to **All devices**. Then add the assignment filter you created in [Step 3](#step-3-create-an-assignment-filter). You must have purchased the Microsoft Authenticator app through an Apple volume-purchase program.      

For more information about assigning a volume-purchased app, see [Assign a volume purchased app](../apps/vpp-apps-ios.md#assign-a-volume-purchased-app).    

## Step 6: Distribute devices   

Shared devices, which are enrolled without user affinity, require minimal user interaction from the frontline worker. Upon receiving the device, the frontline worker will need to open the Microsoft Authenticator app to make sure the device is in shared device mode.   

[!INCLUDE [users-dont-like-enroll](../includes/users-dont-like-enroll.md)]  
