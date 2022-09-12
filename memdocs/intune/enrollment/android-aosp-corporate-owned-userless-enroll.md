---
# required metadata

title: Set up Android (AOSP) device management in Intune for corporate-owned userless devices 
titleSuffix: Microsoft Intune
description: Set up Intune for corporate-owned userless devices built on the Android Open Source Project (AOSP) platform. 
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 09/20/2022
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

# Set up Intune enrollment for Android (AOSP) corporate-owned userless devices    

Set up enrollment in Microsoft Intune for corporate-owned, userless devices built on the Android Open Source Project (AOSP) platform. Intune offers an *Android (AOSP)* device management solution for corporate-owned Android devices that are:   

* Not integrated with Google Mobile Services.
* Intended to be shared by more than one user. 
* Used to accomplish a specific set of tasks at work. 

This article describes how to set up Android (AOSP) device management and enroll RealWear devices for use at work. 

## Prerequisites

To enroll and manage AOSP devices, you must have:

* An active Microsoft Intune tenant. 
* RealWear devices, updated to Firmware 11.2 or later.  

You must also: 

* [Set Microsoft Intune as the mobile device management (MDM) authority in your tenant](../fundamentals/mdm-authority-set.md). You only need to do this once, when you first set up Intune for mobile device management.  

* Assign valid licenses to all RealWear device users. For more information, see [Microsoft Intune licensing](../fundamentals/licenses.md).  


## Create an enrollment profile  
Create an enrollment profile to enable enrollment on devices. 

> [!TIP]
> Intune also generates a token in plain text form, but that one can't be used to enroll devices.   

1.	Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and select **Devices** > **Android** > **Android enrollment** > **Corporate-owned, userless devices**.  
2.	Select **Create** and fill out the required fields.
    - **Name**: Type a name to use when assigning the profile to the dynamic device group.  
    - **Description**: Add a profile description (optional).  
    - **Token expiration date**: The date when the token expires. Intune enforces a maximum of 90 days.  
    - **SSID**: Identifies the network that the device will connect to.  

        > [!NOTE]
        > Wi-Fi details are required because the RealWear device does not have a button or option that lets it automatically connect to other devices.  

    - **Hidden Network**: Choose whether this is a hidden network. By default, this setting is disabled. 
    - **Wi-Fi Type**: Select the type of authentication needed for this network.  

        If you select **WEP Pre-Shared Key** or **WPA Pre-Shared Key**, also enter:   

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
2. Locate your profile in the list, and then select the **More** (**...**) menu that's next to it.
3. Select **View enrollment token**.  

The token appears as a QR code. During device setup, when prompted to, scan the QR code to enroll the device in Intune.   

> [!IMPORTANT]
>- The QR code will contain any credentials provided in the profile in plain text to allow the device to successfully authenticate with the network. This is required as the user will not be able to join a network from the device.  
>- Since you're managing the device via Intune, you should skip the RealWear first time setup. The Intune QR codes is the only thing you need to set up the device.   

### Replace token  
Generate a new token to replace one that's nearing its expiration date. Replacing a token does not affect devices that are already enrolled.  

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
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

1.	Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).  
2. Select **Devices** > **Android** > **Android enrollment** > **Corporate-owned, userless devices**.
2.	Choose the profile that you want to work with.
3.	Select **Token** > **Revoke token** > **Yes**.   

## Create a device group  
You can create *assigned device groups* or *dynamic device groups* in Intune. For more information about both groups, see [Add groups to organize users and devices](../fundamentals/groups-add.md).

Dynamic device groups are configured to automatically add and remove devices based on a set of rules and parameters. For example, you can group devices by enrollment profile name. 

Complete the following steps to create a dynamic Azure AD device group for devices enrolled with an Android (AOSP) corporate-owned, userless enrollment profile.  

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


## Enroll devices    
After you set up and assign the Android (AOSP) enrollment profiles, you can enroll devices via QR code. 

1. Turn on your new or factory-reset device.  

2. When the device prompts you to, scan the token's QR code.     

> [!TIP]
> To access the token in Intune, select **Devices** > **Android** > **Android enrollment** > **Corporate-owned, userless devices**. Select your enrollment profile, and then select **Tokens**. 

3. Follow the on-screen prompts to finish enrolling and registering the device. During setup, Intune automatically installs and opens the apps that are needed for enrollment. Those apps include:  

    *  Microsoft Authenticator app  
    *  Microsoft Intune app  
    *  Intune Company Portal app  

## After enrollment 

### App updates    
The Microsoft Intune app automatically installs available app updates for itself, Authenticator, and Company Portal. When an update becomes available, the Intune app closes and installs the update. The app must be closed completely to install the update.   

### Manage devices remotely    

The following remote actions are available for Android (AOSP) devices:     

* Wipe  
* Delete

You can take action on one device at a time. For more information about where to find remote actions in Intune, see [Remove devices by using wipe, retire, or manually unenrolling the device](../remote-actions/devices-wipe.md).  

> [!NOTE]
> After you wipe an Android (AOSP) device, the device remains in a **Pending** state until it's fully restored to its factory default settings. Then Intune removes it from the device list. When you delete a device, the device is removed from the device list immediately, with no pending status, and the factory reset happens the next time the device checks in. 

## Troubleshooting  

### View version of Microsoft Intune and Microsoft Authenticator apps
To find out which version of the Microsoft Intune app or Microsoft Authenticator app is installed on a device:

1. Go to **Devices** and select the device name.    
2. Select **Discovered apps**. 
3. Find your app and then look in the **Application Version** column for the version number.  

### Troubleshooting + Support     
Select **Troubleshooting + Support** from the Microsoft Endpoint Manager navigation menu to:

* See a list of Android (AOSP) devices enrolled by a user
* Enable troubleshooting of Android (AOSP) devices the same way you can troubleshoot other user devices. 

### Share app logs with Microsoft  
If you experience problems with enrollment or the Microsoft Intune app, you can use the Intune app to upload and send app logs to Microsoft. After you submit the logs, you'll receive an incident ID to share with your Microsoft support person.   

## Known limitations  

The following are known limitations when working with AOSP devices in Intune:  

* You cannot enforce certain password types via device compliance and device restrictions profiles. Password types include:
    * Password required, no restriction 
    * Alphabetic  
    * Alphanumeric  
    * Alphanumeric with symbols    
    * Weak biometric   
*  Device compliance reporting is not available for Android (AOSP).   

* Android (AOSP) management is not supported in these environments:  
    * Intune for Government Community Cloud (GCC) High and Department of Defense (D0D)  
    * Intune operated by 21Vianet  

## Next steps  

* [Create an Android (AOSP) device configuration policy](../configuration/device-restrictions-android-aosp.md) to restrict settings on devices. 

* [Create an Android (AOSP) device compliance policy](../protect/compliance-policy-create-android-aosp.md).   

* For more information about how to get started with AOSP, see [Android source requirements](https://source.android.com/setup/build/requirements)(opens Android source documentation).   
