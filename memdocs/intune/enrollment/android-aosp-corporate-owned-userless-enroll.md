---
# required metadata

title: Set up Intune enrollment for Android AOSP corporate-owned userless devices
titleSuffix: Microsoft Intune
description: Learn how to enroll corporate-owned userless devices built on the Android Open Source Project (AOSP). 
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 10/19/2021
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
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Set up Intune enrollment for AOSP corporate-owned userless devices    

*This feature is in public preview.*

Set up enrollment in Intune for corporate-owned, userless devices built on the Android Open Source Project (AOSP) platform. These types of devices are:  

* Not integrated with Google Mobile Services.
* Meant to be shared by more than one user. 
* Used to accomplish a specific set of tasks. 

This article describes how to set up Intune device management for AOSP and enroll RealWear devices for use at work. You will: 

1. Create an enrollment profile and manage tokens. 
2. Create a device group.  
3. Enroll devices.  

> [!IMPORTANT]
> This feature is in [public preview](../fundamentals/public-preview.md).  

## Prerequisites

To enroll and manage AOSP devices, you must have:

* A Microsoft Intune standalone tenant or Microsoft Endpoint Manager tenant enabled for public preview. 
* RealWear devices, updated to Firmware 11.2 or later.  

You must also: 

* [Set Microsoft Intune as the mobile device management (MDM) authority in your tenant](../fundamentals/mdm-authority-set.md). You only need to do this once, when you first set up Intune for mobile device management.  

* Assign valid Microsoft Endpoint Manager licenses to all RealWear device users. 


## Create an enrollment profile  
Create an enrollment profile to enable enrollment on devices. 

> [!TIP]
> Intune also generates a token in plain text form, but that one can't be used to enroll devices.   

1.	Sign in to the Microsoft Endpoint Manager admin center and select **Devices** > **Android** > **Android enrollment** > **Corporate-owned, userless devices**.  
2.	Select **Create** and fill out the required fields.
    - **Name**: Type a name to use when assigning the profile to the dynamic device group.  
    - **Description**: Add a profile description (optional).  
    - **Token expiration date**: The date when the token expires. Intune enforces a maximum of 90 days.  
    - **SSID**: The SSID that the device will connect to. You must provide Wi-Fi details, because the RealWear device does not have a self-service option that lets it connect to other devices.  
    - **Hidden Network**: Choose whether this is a hidden network. By default, this setting is disabled. 
    - **Wi-Fi Type**: Select the type of authentication needed for this network. If you select **WEP Pre-Shared Key** or **WPA Pre-Shared Key**, also enter:   
        - **Pre-shared key**: The pre-shared key that's used to authenticate with the network. 
3. Select **Next** and optionally, select scope tags. 
4. Select **Next**. Review the details of your profile and then select **Create** to save the profile.  

### Access enrollment token  
After you create a profile, Intune generates a token that's needed for enrollment. To access the token:

1. Go to **Corporate-owned, userless devices**.
2. From the list, select your enrollment profile. 
2. Select **Tokens**. 

Another way to find the token is:
1. Go to **Corporate-owned, userless devices**.
2. Locate your profile in the list, and then select the more menu (**...**) > **View enrollment token**. 

The token appears as a QR code. During device setup, when prompted to, scan the QR code to enroll the device in Intune.   

> [!IMPORTANT]
>- Intune also generates a token in plain text form, but that one can't be used to enroll devices. 
>- The QR code will contain any credentials provided in the profile in plain text to allow the device to successfully authenticate with the network. This is required as the user will not be able to join a network from the device.  
>- Because you're managing the device via Intune, you do not need to create a separate QR code via [Configure RealWear HMT](https://realwear.setupmyhmt.com/configure)(opens realware website) as well.   

### Replace token  
Generate a new token to replace one that's nearing its expiration date. Replacing a token does not affect devices that are already enrolled.  

1. Sign in to the Microsoft Endpoint Manager admin center.
2. Select **Devices** > **Android** > **Android enrollment** > **Corporate-owned, userless devices**.  
3. Choose the profile that you want to work with.
4. Select **Token** > **Replace token**.
5. Enter the new token expiration date. Tokens must be replaced at least every 90 days. 
6. Select **OK**.    

### Revoke token  
Revoke a token to immediately expire it and make it unusable. For example, it's appropriate to revoke a token when:

* You accidentally share the token/QR code with an unauthorized party.
* You complete all enrollments and no longer need the token.  

 Revoking a token does not affect devices that are already enrolled.

1.	Sign in to the Microsoft Endpoint Manager admin center.
2. Select **Devices** > **Android** > **Android enrollment** > **Corporate-owned, userless devices**.
2.	Choose the profile that you want to work with.
3.	Select **Token** > **Revoke token** > **Yes**.   

## Create a device group  
You can create *assigned device groups* or *dynamic device groups* in Intune. For more information about both groups, see [Add groups to organize users and devices](../fundamentals/groups-add.md).

Dynamic device groups are configured to automatically add and remove devices based on a set of rules and parameters. For example, you can group devices by enrollment profile name. 

Complete the following steps to create a dynamic Azure AD device group for devices enrolled with an AOSP corporate-owned, userless enrollment profile.  

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and choose **Groups** > **All groups** > **New group**.
2. In the **Group** blade, fill out the required fields as follows:
    - **Group type**: Security
    - **Group name**: Type an intuitive name (like Factory 1 devices)
    - **Membership type**: Dynamic device
3. Choose **Add dynamic query**.
4. In the **Dynamic membership rules** blade, fill out the fields as follows:
    - **Add dynamic membership rule**: Simple rule
    - **Add devices where**: enrollmentProfileName
    - In the middle box, choose **Equals**.
    - In the last field, enter the enrollment profile name that you created earlier.  

    For more information about dynamic membership rules, see [Dynamic membership rules for groups in Azure AD](/azure/active-directory/users-groups-roles/groups-dynamic-membership). 
5. Choose **Add query** > **Create**.  


### Enroll devices    
After you set up and assign the AOSP enrollment profiles, you can enroll devices via QR code. 

1. Start the setup process on a new or factory-reset device.

2. When the device prompts you to, scan the token's QR code.   

> [!TIP]
> To access the token in Intune, select **Devices** > **Android** > **Android enrollment** > **Corporate-owned, userless devices**. Select your enrollment profile, and then select **Tokens**. 

3. Follow the on-screen prompts to finish enrolling and registering the device. 

The Intune AOSP agent and Azure Authenticator automatically install and open on the device, which allows the device to be provisioned. You'll be locked in the provisioning process until it's complete. 

## After enrollment 

### Update Microsoft Intune and Microsoft Authenticator  
The Microsoft Intune app automatically installs available updates for itself and the Microsoft Authenticator app. When an update becomes available, Microsoft Intune closes and installs the update. The app must be closed completely to install the update. 

> [!TIP]
> Starting with the August 2021 service release (2108), the Intune AOSP agent and the Azure Authenticator will be automatically updated during provisioning. To allow the apps to update, all devices will need to be re-enrolled with the latest version of the apps.  

### Use remote actions on AOSP devices  

The following remote actions are available for AOSP devices:

* Wipe  
* Delete

For more information about where to find remote actions in Intune, see [Remove devices by using wipe, retire, or manually unenrolling the device](../remote-actions/devices-wipe.md). Bulk actions are not supported for AOSP devices so you can only take action on one device at a time. 

> [!NOTE]
> When you wipe an AOSP device, the device remains in a **Pending** state until the device is fully restored to its factory default. It's then removed from the devices list in Intune. When you delete a device, the device  is removed from the device list immediately, with no pending status. The factory reset happens the next time the device checks in. 

## Troubleshooting  

## View version of Microsoft Intune and Microsoft Authenticator apps
To find out which version of the Microsoft Intune app or Microsoft Authenticator app is installed on a device:

1. Go to **Devices** and select the AOSP device name.    
2. Select **Discovered apps**. 
3. Find your app and then look in the **Application Version** column for the version number.  

## Troubleshooting + Support  
Select **Troubleshooting + Support** from the Microsoft Endpoint Manager navigation menu to:

* See a list of AOSP devices enrolled by a user
* Enable troubleshooting of AOSP devices the same way you can troubleshoot other user devices. 

## Share Microsoft Intune app logs with Microsoft
If you experience problems with enrollment or the Microsoft Intune app, you can upload your diagnostic logs in the Microsoft Intune app and send them to Microsoft. You'll receive an incident ID that you can share with your Microsoft support person to reference your logs. 

## Known limitations  

The following are known limitations when working with AOSP devices in Intune:  

* Some password types cannot be managed on AOSP devices via device compliance and device restrictions profiles. These include:
    * Password required, no restriction 
    * Alphabetic  
    * Alphanumeric  
    * Alphanumeric with symbols    
    * Weak biometric   
* Device compliance reporting for AOSP devices is not available in Intune.  



## Next steps  

* [Create a device configuration policy](../configuration/device-restrictions-android-aosp.md) to restrict settings on AOSP devices. 

* [Create a device compliance policy](../protect/compliance-policy-create-android-aosp.md) for AOSP devices.  

* For more information about how to get started on AOSP, see [Android source requirements](https://source.android.com/setup/build/requirements)(opens Android source documentation).   