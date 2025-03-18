---
# required metadata

title: Tutorial - Use Apple Business Manager to enroll iOS/iPadOS devices in Intune
titleSuffix: Microsoft Intune
description: In this tutorial, you'll set up Apple corporate device enrollment features with Intune to enroll iOS/iPadOS devices purchased through Apple Business Manager.  
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/05/2025
ms.topic: tutorial
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.assetid: 
Customer intent: As an Intune admin, I want to set up automated device enrollment for iOS/iPadOS devices I purchased through Apple Business Manager.  

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: maholdaa 
ms.custom: intune
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---  

# Tutorial: Set up Microsoft Intune enrollment for iOS/iPadOS devices in Apple Business Manager  
Use Apple Business Manager with Microsoft Intune to simplify and automate device enrollment for iOS/iPadOS devices procured through Apple Business Manager. *Automated device enrollment*, which we'll set up in this tutorial, enables secure automatic enrollment the first time the user turns on the device by deploying the enrollment profile to the device over-the-air.  

In this tutorial, you'll learn how to:
> [!div class="checklist"]
> * Get an Apple device enrollment token
> * Sync managed devices to Intune
> * Create an enrollment profile
> * Assign the enrollment profile to devices  

At the end of this tutorial, devices will be ready to distribute for enrollment. 

## Prerequisites
- Set [mobile device management (MDM) authority](../fundamentals/mdm-authority-set.md).      
- Get [Apple MDM Push certificate](apple-mdm-push-certificate-get.md).   
- Have new or wiped devices purchased from Apple Business Manager.    
- Add purchase information under device management settings in [Apple Business Manager](https://business.apple.com).    

If you don't have an Intune subscription, [sign up for a free trial account](../fundamentals/free-trial-sign-up.md).    

## Step 1: Add MDM server      
Create an MDM server profile for Microsoft Intune in Apple Business Manager. The token you download in this step will enable the connection between Microsoft Intune and Apple Business Manager in a later step.    

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Go to **Devices** and expand **By platform**. Select **iOS/iPadOS**.
3. Expand **Device onboarding**, and then select **Enrollment**.  
4. Select **Enrollment program tokens**.  
5. Select **Create**.  
6. Select **I agree** to grant permission to Microsoft to send user and device information to Apple.  
7. Select **Download your public key** to download the server's public key certificate (a .pem file) to your local drive. 
8. Select **Create a token via Apple Business Manager** and sign in to Apple Business Manager with your company Apple ID.  

    >[!IMPORTANT] 
    > While you're in Apple Business Manager, don't close the browser tab with Microsoft Intune. You'll return to it later.  

6. Add an MDM server called *TestMDMServer* and download the server token for it in Apple Business Manager. For details and instructions, see [Link to a third-party MDM server](https://support.apple.com/guide/apple-business-manager/axm1c1be359d/web)(opens Apple Business Manager User Guide). Save the server token locally as a P7M file (.p7m). Then continue to [Step 2: Assign devices](tutorial-use-device-enrollment-program-enroll-ios.md#step-2-assign-devices).  

## Step 2: Assign devices  

While you're in Apple Business Manager, assign devices to your new MDM server (*TestMDMServer* or whatever you named it). For details and instructions, see [Assign, reassign, or unassign devices in Apple Business Manager](https://support.apple.com/guide/apple-business-manager/axmf500c0851/web)(opens Apple Business Manager User Guide). When you're done assigning devices, continue to [Step 3: Upload MDM server token](tutorial-use-device-enrollment-program-enroll-ios.md#step-3-upload-mdm-server-token).   

## Step 3: Upload MDM server token     
Return to the Microsoft Intune admin center to upload the MDM server token to Intune. After you upload the token, Microsoft Intune can sync and enroll iOS/iPadOS devices assigned to *TestMDMServer*.   

1. For **Apple ID**, enter the Apple ID you used to create the token.  
2. For **Apple token**, upload the server token you saved earlier. The file must be in P7M format.     
3. Select **Next**.  
4. Optionally, apply scope tags to the enrollment token to limit other admins from accessing or making changes to it. For more information about scope tags, see [Use role-based access control (RBAC) and scope tags for distributed IT](../fundamentals/scope-tags.md). 
5. Select **Next**.  
6. On **Review + create**, select **Create** to finish linking Microsoft Intune and Apple Business Manager.  

Microsoft Intune automatically syncs with Apple Business Manager. Devices can take up to 12 hours to appear in the admin center. You can wait for these devices to sync, or manually start the sync. To start the sync yourself, select your token from the list in the admin center, and then choose **Devices** > **Sync**.  

## Step 4: Create an Apple enrollment profile  
Create an enrollment profile for corporate-owned iOS/iPadOS devices. A device enrollment profile defines the settings applied to a group of devices during enrollment.

1. Select your token in the admin center, and then choose **Profiles**.
   
1. Select **Create profile** > **iOS/iPadOS**.  

1. On the **Basics** page, enter *TestProfile* for **Name** and *Testing ADE for iOS/iPadOS devices* for **Description**. Users don't see these details.

1. Select **Next**.

1. Decide if you want your devices to enroll with or without **User Affinity**. User Affinity is designed for devices that will be used by particular users. If your users will want to use the Company Portal for services like installing apps, choose **Enroll with User Affinity**. If your users don't need the Company Portal or you want to provision the device for many users, choose **Enroll without User Affinity**.

   * If you chose to enroll with User Affinity, the **Select where users must authenticate** option appears. Decide if you want to Authenticate with Company Portal or Apple Setup Assistant (legacy), or Setup Assistant with modern authentication. For more information about authentication methods, see [Authentication methods for automated device enrollment in Intune](../enrollment/automated-device-enrollment-authentication.md).
   
1. If you chose to enroll with User Affinity and Authenticate with Company Portal, the **Install Company Portal with VPP** option appears. If you install the Company Portal with a VPP token, your user won't have to enter an Apple ID and Password to download the Company Portal from the app store during enrollment. Choose **Use Token:** under **Install Company Portal with VPP** to select a VPP token that has free licenses of the Company Portal available. If you don't want to use VPP to deploy the Company Portal, choose **Don't use VPP**. 

   * If you chose to enroll with User Affinity, Authenticate with Company Portal, and Install Company Portal with VPP, decide if you want to run the Company Portal in Single App Mode until Authentication. With this setting, you can ensure the user doesn't have access to other apps until they finish the corporate enrollment. If you want to restrict the user to this flow until enrollment is completed, choose **Yes** under **Run Company Portal in Single App Mode until authentication**. 

1. Under **Device Management Settings**, choose **Yes** for **Supervised**. Supervision gives you more management options and disables Apple Activation Lock by default. Microsoft recommends using automated device enrollment as the mechanism for enabling Intune's supervised mode, especially for organizations that are deploying large numbers of iOS/iPadOS devices.

1. Choose **Yes** under **Locked enrollment** to ensure your users can't remove device management from their corporate device. 

1. Choose an option under **Sync with Computers** to determine if the iOS/iPadOS devices can sync with computers. **Deny All** means that devices using this profile can't sync with any data on any computer.

1. By default, Apple names the device with the device type, such as *iPad*. If you want to provide a different name template, choose **Yes** under **Apply device name template**. Enter the name you want to apply to the devices, where the strings *{{SERIAL}}* and *{{DEVICETYPE}}* will substitute each device's serial number and device type. Otherwise, choose **No** under **Apply device name template**.

1. Choose **Next**.

1. On the **Setup Assistant** page, enter *Tutorial department* for **Department Name**. This string is what users see when they tap **About configuration** during device activation.

1. Under **Department Phone**, enter a phone number. This number appears when users tap the **Need help** button during activation.

1. You can **Show** or **Hide** various screens during device activation. For the most seamless enrollment experience, set all screens to **Hide**.  

1. Choose **Next**.  
   
1. Review the profile settings. To save the profile, select **Create**  

## Step 5: Assign an enrollment profile to iOS/iPadOS devices

You must assign an enrollment program profile to devices before they can enroll. These devices are synced to Intune from Apple, and must be assigned to the proper MDM server token in the ABM, ASM, or ADE portal.

1. In the admin center, return to **Enrollment program tokens**. Choose your token from the list.  
2. Select **Devices**, and then choose the devices you want to assign.
3. Select **Assign profile**. Then select a profile for the devices.  
4. Select **Assign**.  

> [!NOTE]
> Ensure that **Device Type Restrictions**, found within your tenant's **Enrollment Restrictions**, does not have the default **All Users** policy set to block the iOS/iPadOS platform. This setting will cause automated enrollment to fail and your device will show as an *invalid profile*, regardless of user attestation. To permit enrollment only by company-managed devices, block only personally owned devices, which will permit corporate devices to enroll. Microsoft defines a corporate device as a device that's enrolled via a device enrollment program or a device that's manually entered in the admin center under **Corporate device identifiers**.  

## Step 6: Distribute devices to users

You've set up management and syncing between Apple and Intune, and assigned a profile to let your ADE devices enroll. You can now distribute devices to users. Devices with user affinity require each user be assigned an Intune license.

## Next steps

You can find more information about other options available for enrolling iOS/iPadOS devices.

> [!div class="nextstepaction"]
> [Technical docs for iOS/iPadOS automated device enrollment](device-enrollment-program-enroll-ios.md)  
