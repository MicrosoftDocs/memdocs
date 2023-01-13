---
# required metadata

title: Enroll macOS devices - Apple Business Manager or Apple School Manager
titleSuffix: 
description: Prepare Macs purchased through Apple Business Manager and Apple School Manager for Intune enrollment.    
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 01/13/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: benflamm
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: seodec18
ms.collection: M365-identity-device-management
---

# Automatically enroll Macs with Apple Business Manager or Apple School Manager  

Set up automated device enrollment in Intune for new or wiped Macs purchased through an Apple enrollment program, such as Apple Business Manager or Apple School Manager. With this method, you don't need to have the devices with you to configure them. Intune automatically syncs with Apple to obtain device info from your enrollment program account, and deploys your preconfigured enrollment profiles to Macs over-the-air. 

Prepared devices can be shipped directly to employees or students. Setup Assistant and device enrollment begin when the device user turns on the Mac.     

This article describes how to set up an automated device enrollment profile for corporate-owned Macs. 

>[!NOTE]
> The steps in this article are the same for Apple Business Manager and Apple School Manager. For brevity, we'll refer to Apple Business Manager only, except where clarification is neccessary.     

<!--
**Steps to enable enrollment programs from Apple**
1. [Get an Apple DEP token and assign devices](#get-the-apple-dep-token)
2. [Create an enrollment profile](#create-an-apple-enrollment-profile)
3. [Synchronize DEP-managed devices](#sync-managed-device)
4. [Assign DEP profile to devices](#assign-an-enrollment-profile-to-devices)
5. [Distribute devices to users](#end-user-experience-with-managed-devices)
-->  

## Limitations  
Automated device enrollment via Apple Business Manager and Apple School Manager is not supported with [device enrollment manager accounts](device-enrollment-manager-enroll.md).    

## Prerequisites 

- Access to [Apple School Manager](https://school.apple.com/) or [Apple Business Manager](http://business.apple.com)  
- A list of device serial numbers or a purchase order number for devices purchased through Apple.    
- [MDM authority](../fundamentals/mdm-authority-set.md)
- [Apple MDM Push certificate](../enrollment/apple-mdm-push-certificate-get.md)  

## Create enrollment program token  

The enrollment program token is a neccessary component of enrollment because it enables the communication and device management capabilities between Intune and Apple. It allows Intune to sync information from your Apple Business Manager account, and apply profiles to devices.  

This section describes how to create the enrollment program token in Intune, which includes that you: 

* Create a MDM server for Intune in Apple Business Manager. 
* Download/upload the Intune server's public key certificate (a .pem file) to Apple Business Manager.
* Download/upload the MDM server token to Microsoft Intune.  

Optionally, after you create the MDM server, you can start assigning devices to it. We recommend assigning them since you're already in Apple Business Manager, but you can come back later if you're not ready.  

### Step 1. Download Intune server public key certificate 

The public key certificate is needed to request a trust-relationship certificate from Apple Business Manager.     

1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **macOS** > **macOS enrollment**. 
2. Select **Enrollment program tokens**. 
3. Select **Add**.  
4. Select **I agree** to grant permission to Microsoft to send user and device information to Apple. 
3. Select **Download your public key** and save the file (.pem) locally. You will need it to get the MDM server token in the next step.  

### Step 2. Add MDM server and download server token in Apple Business Manager 

1. In the admin center, select the link that corresponds with the Apple portal you use. Your options: 
    * **Create a token via Apple Business Manager** 
    * **Create a token via Apple School Manager**  

    Apple Business Manager or Apple School Manager will open in a new browser tab. You can safely switch to the new tab, but keep the tab with Microsoft Endpoint Manager open. You'll return to it later.  
2. Sign in to Apple Business Manager with your company Apple ID. Remember, this is the Apple ID you'll use to renew and manage the token going forward.  
3. Go to your account profile > **Preferences**.  
4. Go to your MDM server assignments.  
5. Select the option to add an MDM server.  
6. Name the MDM server. The name is for identification purposes only while in Apple Business Manager or Apple School Manager, and doesn't have to be the actual name or URL of the Microsoft Intune server. 
7. Upload your public key file, and then save your changes. 
8. Download the server token.   

### Step 3. Assign devices to MDM server   

While you're in Apple Business Manager, assign devices to the MDM server. You can use available features like *filters* and *bulk assignment* to simplify assignment selection.     

For more information and steps, see [Assign, reassign, or unassign devices in Apple Business Manager](https://support.apple.com/guide/apple-business-manager/axmf500c0851/web)(opens Apple Business Manager User Guide).  

### Step 4. Save Apple ID used to download server token

Return to the [admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and enter your Apple ID so that you have record of it in the future. This is the Apple ID you need to use to renew the token every year. Make sure future Intune admins are aware of the Apple ID used, in case you leave your organization and need to transition token management to them. 

![Screenshot highlighting the Apple ID field in the "Add enrollment program token" pane. ](./media/device-enrollment-program-enroll-ios/image03.png)  

### Step 5. Upload server token to Intune  

1. In the admin center, under **Apple token**, browse to the certificate (PEM file).
2. Choose **Open**, and then choose **Create**. 

The server token enables Intune to enroll your devices from Apple Business Manager and Apple School Manager, and deploy policies to enrolled devices. Intune will automatically connect with Apple to sync device information from your enrollment program account.  

## Create an Apple enrollment profile

Create an automated device enrollment profile in Intune for your Apple Business Manager devices. The device enrollment profile defines the enrollment experience for the Macs your organization owns, and enforces enrollment policies and settings on enrolling Macs. To continue, you must have an enrollment program token setup in Intune. If you haven't done that yet, see [Create enrollment program token](#create-enrollment-program-token) at the beginning of this article.   

At the end of this procedure, you will assign the enrollment profile to Azure AD device groups. The profile is deployed to the device over-the-air.       

1. In the [admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **macOS enrollment** > **Enrollment program tokens**.  
2. Select an enrollment program token. Remember, every token is associated with an MDM server and any Macs you assigned to the server in Apple Business Manager. 
3. Select **Profiles** > **Create profile** > **macOS**.  

    ![Create a profile screenshot.](./media/device-enrollment-program-enroll-macos/image04.png)  

4. On the **Basics** page, enter a name and description for the profile so that you can distinguish it from other enrollment profiles. These details aren't visible to device users.  

     >[!TIP]
     > You can use the name field to create a dynamic group in Azure Active Directory, and assign devices to the enrollment profile automatically. Use the profile name to define the *enrollmentProfileName* parameter. For more information, see [Azure Active Directory dynamic groups](/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices).  

4. For **Platform**, select **macOS**.  

5. Select **Next**. 

5. On the **Management Settings** page, configure **User Affinity**.  Your options: 

    * Option 1 - **Enroll without User Affinity**:  Enroll devices that aren't associated with a single user. Use this for shared devices and devices that don't need to access local user data. The Company Portal app doesn't work on these types of devices.  
    * Option 2 - **Enroll with User Affinity**: Enroll devices that are associated with an assigned user. Choose this option for work devices that belong to users, and if you want to require users to have the Company Portal app to install apps. Multifactor authentication (MFA) is available with this option.   

      This option requires additional configuration. Users must authenticate themselves before enrollment. Select one of the following authentication methods:   

      - **Setup Assistant with modern authentication**: This method requires users to complete all Setup Assistant screens and sign in to the Company Portal app with their Azure AD credentials before they can access resources.  After they sign in to Company Portal, the device:   

        - Registers with Azure AD.  
        - Becomes visible in the user’s device list in Azure AD.  
        - Gains access to resources protected by conditional access.
        - Can be evaluated for device compliance.

        If the user doesn't sign in to the Company Portal to complete registration, they'll be redirected to the Company Portal app each time they try to open a managed app that's protected by conditional access.  

        Devices running macOS 10.15 and later can use this method. Older macOS devices will fall back to using the legacy Setup Assistant method.  

        For more information about how to get the Company Portal app to Mac users, see [Add the Company Portal for macOS app](../apps/apps-company-portal-macos.md).    

      - **Setup Assistant (legacy)**: Use the legacy Setup Assistant if you want users to experience the typical, out-of-box-experience for Apple products. This method installs standard preconfigured settings when the device enrolls with Intune management. If you're using Active Directory Federation Services and you're using Setup Assistant to authenticate, a [WS-Trust 1.3 Username/Mixed endpoint](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff608241(v=ws.10)) is required. For more information about retrieving the ADFS endpoint, see [Get-ADfsEndpoint] (/powershell/module/adfs/get-adfsendpoint?view=win10-ps&preserve-view=true).   

8. You can enforce **Locked enrollment** to prevent users from unenrolling their devices from Intune. Select **Yes** to disable the Mac settings in System Preferences and Terminal that allow users to remove the management profile. After the device enrolls, you cannot change this setting without wiping the device.  

9. Select **Next**.   

10. On the **Setup Assistant** page, configure the Setup Assistant experience.      
    1. Enter your department information so that users know who to contact for support:  
        * **Department Name**: This name appears when device users select **About Configuration** during activation.  
        * **Department Phone**: This phone number appears when device users select **Need Help** during activation.   
    2. Select the Setup Assistant screens you want to show or hide during device setup. Your options:  
        * **Hide**: The screen doesn't appear to users during device setup. After device setup, the user can go to their device settings to set up the feature.  
        * **Show**: The screen appears to users during device setup. The user can still skip screens that don't require immediate action. After device setup, the user can go to their device settings to set up the feature.  
        
       The following table describes the purpose of each Setup Assistant screen during device setup.      

        | Setup Assistant screen  | Purpose |
        |------------------------------------------|------------------------------------------|
        | **Location Services** | Prompt the user for their location. For macOS 10.11 and later and iOS/iPadOS 7.0 and later. |
        | **Restore** | Display the Apps & Data screen. This screen gives the user the option to restore or transfer data from iCloud Backup when they set up the device. For macOS 10.9 and later, and iOS/iPadOS 7.0 and later. |
        | **Apple ID** | Give the user the options to sign in with their Apple ID and use iCloud. For macOS 10.9 and later, and iOS/iPadOS 7.0 and later.   |
        | **Terms and Conditions** | Require the user to accept Apple's terms and conditions. For macOS 10.9 and later, and iOS/iPadOS 7.0 and later. |
        | **Touch ID and Face ID** | Give the user the option to set up fingerprint identification for the device. For macOS 10.12.4 and later, and iOS/iPadOS 8.1 and later. |
        | **Apple Pay** | Give the user the option to set up Apple Pay on the device. For macOS 10.12.4 and later, and iOS/iPadOS 7.0 and later. |
        | **Siri** | Give the user the option to set up Siri. For macOS 10.12 and later, and iOS/iPadOS 7.0 and later. |
        | **Diagnostics Data** | Display the Diagnostics screen to the user. This screen gives the user the option to send diagnostic data to Apple. For macOS 10.9 and later, and iOS/iPadOS 7.0 and later. |  
        | **Display Tone** | Give the user the option to turn on Display Tone. For macOS 10.13.6 and later, and iOS/iPadOS 9.3.2 and later. |
        | **FileVault** | Display the FileVault 2 encryption screen to the user. For macOS 10.10 and later. |
        | **iCloud diagnostics** | Display the iCloud Analytics screen to the user. For macOS 10.12.4 and later. |  
        | **Registration** | Display the registration screen. For macOS 10.9 and later. |  
        | **iCloud Storage** | Display the iCloud Documents and Desktop screen to the user. For macOS 10.13.4 and later. |
        | **Appearance** | Display the Appearance screen to the user. For macOS 10.14 and later, and iOS/iPadOS 13.0 and later. |    
        | **Screen Time** | Display the Screen Time screen. For macOS 10.15 and later, and iOS/iPadOS 12.0 and later. |
        | **Privacy** | Display the Privacy screen to the user. For macOS 10.13.4 and later, and iOS/iPadOS 11.3 and later. |
        | **Accessibility** | Display the Accessibility screen to the user. If this screen is hidden, the user won't be able to use the Voice Over feature. Voice Over is supported on devices that:<br>- Run macOS 11.<br>- Are connected to the internet using Ethernet.<br>- Have the serial number appear in Apple School Manager or Apple Business Manager. |  
        | **Auto unlock with Apple Watch**| Give the user an option to use their Apple Watch to unlock their Mac. For macOS 12.0 and later. 

11. Select **Next**.

12. Select **Create** to finish creating the profile.   
 

## Sync managed devices

Sync your enrollment program token in the admin center to see all associated Apple devices and device info.     

1. Return to **Enrollment program tokens** and choose your enrollment program token. 

2. Select **Devices** > **Sync**.  

   ![Screenshot of Enrollment program token area in the admin center, highlighting the example token, "Devices" link, and "Sync" button.](./media/device-enrollment-program-enroll-macos/image06.png)  

### Sync restrictions  
To comply with Apple's terms for acceptable enrollment program traffic, Microsoft Intune imposes the following restrictions:  
 - A full sync can run no more than once every seven days. During a full sync, Intune fetches the complete updated list of serial numbers assigned to the Apple MDM server connected to Intune. If you delete a device from Intune without unassigning it from the Apple MDM server in Apple Business Manager or Apple School Manager, it won't be re-imported into Intune until the full sync is run. 
 - If a device is released from ABM/ASM, it can take up to 45 days for it to be automatically deleted from the devices page in Intune. You can manually delete released devices from Intune one by one if needed. Released devices will be accurately reported as being Removed from ABM/ASM in Intune until they are automatically deleted within 30-45 days.
 - A sync is run automatically every 24 hours. You can also sync by clicking the **Sync** button (no more than once every 15 minutes). All sync requests are given 15 minutes to finish. The **Sync** button is disabled until a sync is completed. This sync will refresh existing device status and import new devices assigned to the Apple MDM server.

## Assign an enrollment profile to devices

Assign an enrollment profile to Apple devices.    

1. Return to **Enrollment program tokens** and select a token.  
2. Select **Devices**. 
3. Choose your devices from the list, and then select **Assign profile**.  
3. Choose a profile to assign, and then select **Assign**.  

### Assign a default profile

Optionally, you can select a default enrollment profile. The default profile is deployed to enrolling devices that aren't assigned anything else.  

1. Return to **Enrollment program tokens** and select a token.  
2. Select **Set Default Profile**.
3. Choose a profile, and then select **Save**.  

## Distribute devices

>[!IMPORTANT]
> Devices with user affinity require that each user be assigned an Intune license. Devices without user affinity require a device license.  

Distribute prepared devices throughout your organization.

* New or wiped Macs: New or wiped Macs configured in Apple Business Manager or Apple School Manager will automatically enroll in Microsoft Intune during Setup Assistant when someone turns on the device. If you assigned the device to a macOS enrollment profile with user affinity, the device user must sign in to the Company Portal after Setup Assistant is done to finish Azure AD registration and conditional access requirements.  

* Existing Macs: You can enroll devices that have already gone through Setup Assistant. Complete these steps to enroll corporate-owned Macs running macOS 10.13 and later.    

  1. Ensure that: 
     * The device has been imported to Apple Business Manager or Apple School Manager.  
     * The device has been assigned a macOS enrollment profile in the admin center. 
  1. Sign in to the device with a local administrator account.  
  2. To trigger enrollment, on the **Home** page, open **Terminal** and run the following command:  

     `sudo profiles renew -type enrollment`  
  5. Enter the local administrator account's device password.  
  6. On **Device enrollment**, select **Details**.  
  7. On **System preferences**, select **Profiles**.
  8. Follow the onscreen prompts to download Microsoft Intune management profile, certificates, and policies. 
     >[!TIP]
     > You can confirm which profiles are on the device anytime by returning to **System Preferences** > **Profiles**.  
  9. If you assigned the device to a macOS enrollment profile with user affinity, sign in to the Company Portal app to complete Azure AD registration and conditional access requirements.  

## Renew enrollment program token  
Complete these steps to renew an enrollment program token that's about to expire. 

1. Sign in to [Apple Business Manager](http://business.apple.com) or [Apple School Manager](http://school.apple.com) with an administrator or content manager acount.  
2. Go to your account settings > MDM servers. Select the MDM server that's associated with the token you want to renew. Download the token.  

    ![Screenshot of Download Token.](./media/device-enrollment-program-enroll-macos/download-token.png)

3. Confirm that you want to download the server token.  
4. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and go to **Device enrollment** > **Apple Enrollment** > **Enrollment program tokens**. Select the enrollment program token.  
    ![Screenshot of enrollment program tokens.](./media/device-enrollment-program-enroll-ios/enrollmentprogramtokens.png)

5. Select **Renew token** and enter the Apple ID used to create the original token.  
    ![Screenshot of generate new token.](./media/device-enrollment-program-enroll-ios/renewtoken.png)

6. Upload the newly downloaded token.  
7. Select **Next**. You can update scope tags at this time if you want. Otherwise, continue to **Review + create**.   
8. Select **Create** to save your changes.  

## Next steps

Use [Microsoft Intune remote actions](../remote-actions/device-management.md) to remotely manage enrolled Macs.  
