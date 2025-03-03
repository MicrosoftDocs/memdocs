---
# required metadata

title: Set up Android (AOSP) device management in Intune for corporate-owned user-associated devices  
titleSuffix: Microsoft Intune
description: Set up Intune for corporate-owned user-associated devices built on the Android Open Source Project (AOSP) platform. 
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 09/24/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: priyar
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
---

# Set up Intune enrollment for Android (AOSP) corporate-owned user-associated devices 

Set up enrollment in Intune for corporate-owned, user-associated devices built on the Android Open Source Project (AOSP) platform. Intune offers an *Android (AOSP)* device management solution for corporate-owned Android devices that are:  

* Not integrated with Google Mobile Services.
* Intended to be used by a single user. 
* Used exclusively for work.    

This article describes how to set up Android (AOSP) device management and enroll AOSP devices for use at work.  

## Prerequisites  

>[!NOTE]
> Beginning October 1st, AOSP devices must have the Microsoft Intune app, version 24.7.0 or later to sync with the Microsoft Intune service.  

To enroll and manage AOSP devices, you must have:

* An active Microsoft Intune tenant. 
* [A supported device.](../fundamentals/supported-devices-browsers.md#android)  

You must also:  

* [Set Microsoft Intune as the mobile device management (MDM) authority in your tenant](../fundamentals/mdm-authority-set.md). You only need to do this once, when you first set up Intune for mobile device management.  

* Assign valid licenses to all specialized device users. For more information, see [Microsoft Intune licensing](../fundamentals/licenses.md) and [Managing specialty devices with Microsoft Intune](../fundamentals/specialty-devices-with-intune.md).

## Create an enrollment profile   
Create an enrollment profile to enable enrollment on devices. 

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Go to **Devices** > **Enrollment**.  
3. Select the **Android** tab.  
4. Under **Android Open Source Project (AOSP)**, choose **Corporate-owned, user-associated devices**.  
5. Select **Create profile**.  
6. Enter the basics for your profile:
    - **Name**: Give the profile a name. Note the name down for later, because you'll need it when you set up the dynamic device group.  
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.  
    - **Token expiration date**: Select the date the token expires, which can be up to 65 years in the future.    
    - **SSID**: Identifies the network that the device will connect to.  
    
        > [!NOTE]
        > Wi-Fi details are required if the device doesn't have a button or option that lets it automatically connect to a network.  

    - **Hidden network**: Choose whether this is a hidden network. By default, this setting is disabled, which means the network can broadcast its SSID. 
    - **Wi-Fi type**: Select the type of authentication needed for this network.  

        If you select **WEP Pre-shared key** or **WPA Pre-shared key**, also enter:  

        - **Pre-shared key**: The pre-shared key that's used to authenticate with the network.  
    - **For Microsoft Teams devices (preview)**: Select **Enabled** if this profile is applicable for Microsoft Teams Android devices. This setting should only be used for [Microsoft Teams Android devices](/microsoftteams/devices/teams-ip-phones). 

7. Select **Next** and optionally, select scope tags. 
8. Select **Next**. Review the details of your profile and then select **Create** to save the profile.  

### Access enrollment token  
After you create a profile, Intune generates a token that's needed for enrollment. The token appears as a QR code. During device setup, when prompted to, scan the QR code to enroll the device in Intune.

To view the token as a QR code, select your enrollment profile from the enrollment profile list. Then select **Token**.   
You can also export the enrollment profile JSON file. To create a JSON file, select **Export**.  

> [!IMPORTANT]
>- The QR code will contain any credentials provided in the profile in plain text to allow the device to successfully authenticate with the network. This is required as the user will not be able to join a network from the device.
>- Consider using a staging network with limited permissions for provisioning devices and completing the enrollment process. For example, you could use an internet-connected network with limited permissions and no corporate access to do the initial set up.
>- On RealWear devices, you should skip the first time setup. The Intune QR code is the only thing you need to set up the device.  


### Replace a token  
You can generate a new token to replace one that's nearing its expiration date. The replacement token doesn't affect devices that are already enrolled.  

1. In the [admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Enrollment**.  
2. Select the **Android** tab.  
3. In the **Android Open Source Project (AOSP)** section, choose **Corporate-owned, user-associated devices**.   
3. Choose the profile that you want to work with.
4. Select **Token** > **Replace token**.
5. Enter the token's new expiration date, which can be up to 65 years in the future. 
6. Select **OK**. 

### Revoke a token  
Revoke a token to immediately expire it and make it unusable. For example, it's appropriate to revoke a token when:

* You accidentally share the token/QR code with an unauthorized party.
* You complete all enrollments and no longer need the token.  

 Revoking a token has no effect on devices that are already enrolled.

1. In the [admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Enrollment**.  
2. Select the **Android** tab.  
3. In the **Android Open Source Project (AOSP)** section, choose **Corporate-owned, user-associated devices**.
4.	Choose the profile that you want to work with.  
5.	Select **Token** > **Revoke token** > **Yes**.   

## Create a device group  
You can create *assigned device groups* or *dynamic device groups* in Intune. For more information about groups, see [Add groups to organize users and devices](../fundamentals/groups-add.md).

Dynamic device groups are configured to automatically add and remove devices based on a set of rules and parameters. For example, you can group devices by enrollment profile name. 

Complete the following steps to create a dynamic Microsoft Entra device group for devices enrolled with an Android (AOSP) corporate-owned, user-associated enrollment profile.  

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and choose **Groups** > **All groups** > **New group**.
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
    
    For more information about dynamic membership rules, see [Dynamic membership rules for groups in Microsoft Entra ID](/azure/active-directory/users-groups-roles/groups-dynamic-membership).  
5. Choose **Add query** > **Create**.  


## Enroll devices via QR code
   
After you set up and assign the Android (AOSP) enrollment profiles, you can enroll devices via QR code. 

1. Turn on your new or factory-reset device.    

2. When the device prompts you to, scan the token's QR code. 

> [!TIP]
> To access the token in Intune, go to **Devices** > **Enrollment**. Then select the **Android* tab > **Corporate-owned, user-associated devices**. Select your enrollment profile, and then choose **Token**.  

3. Step through the on-screen prompts to finish enrolling and registering the device. The following apps are automatically installed during this time and used for enrollment: 

    * Microsoft Intune app  
    * Intune Company Portal app  
    * Microsoft Authenticator app  

To use JSON to enroll devices, refer to instructions provided by the device manufacturer.

## After enrollment 

### Update apps    
The Microsoft Intune app automatically updates itself. When an app update becomes available, the Intune app closes and installs the update. The app must remain closed to install the update. The app also installs updates for Microsoft Authenticator and the Company Portal app.    

### Manage devices remotely  

The following remote actions are available for Android (AOSP) devices:

* Wipe  
* Delete  

You can take action on one device at a time. For more information about where to find remote actions in Intune, see [Remove devices by using wipe, retire, or manually unenrolling the device](../remote-actions/devices-wipe.md).  

> [!NOTE]
> After you wipe an Android (AOSP) device, the device remains in a **Pending** state until it's fully restored to its factory default settings. Then Intune removes it from the device list. When you delete a device, the device is removed from the device list immediately, with no pending status, and the factory reset happens the next time the device checks in.  

## Troubleshooting  

### View app versions  

Find out which version of the Intune app or Microsoft Authenticator app is installed on a device. 

1. Go to **Devices** and select the device name.    
2. Select **Discovered apps**. 
3. Find your app and then look in the **Application Version** column for the version number.  

### Troubleshooting + Support  
Select **Troubleshooting + Support** in the admin center to:

* See a list of Android (AOSP) devices enrolled by a user
* Enable troubleshooting of Android (AOSP) devices the same way you can troubleshoot other user devices. 

### Share app logs with Microsoft  
If you experience problems with enrollment or access to work resources, you can share diagnostic logs with Microsoft in the Intune app or Company Portal app. After you submit the logs, you'll receive an incident ID to share with your Microsoft support person.   

## Known limitations  

The following are known limitations when working with AOSP devices in Intune:  

* You cannot enforce certain password types via device compliance and device restrictions profiles. Password types include:   
    * Password required, no restriction 
    * Alphabetic  
    * Alphanumeric  
    * Alphanumeric with symbols    
    * Weak biometric   
* Device compliance reporting is not available for Android (AOSP).  
* Android (AOSP) management is not supported with Intune operated by 21Vianet.  

## Next steps  

* [Create an Android (AOSP) device configuration policy](../configuration/device-restrictions-android-aosp.md) to restrict settings on devices. 

* [Create an Android (AOSP) device compliance policy](../protect/compliance-policy-create-android-aosp.md).   

* Create a policy that requires users to accept your [terms and conditions](terms-and-conditions-create.md) before enrollment. 

* For more information about how to get started with AOSP, see [Android source requirements](https://source.android.com/setup/build/requirements)(opens Android source documentation). 
