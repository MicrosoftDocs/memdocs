---
# required metadata

title: Enroll macOS devices - Apple Business Manager or Apple School Manager
titleSuffix: 
description: Learn how to enroll macOS devices purchased through Apple Business Manager and Apple School Manager.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 07/11/2022
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

# Automatically enroll macOS devices with the Apple Business Manager or Apple School Manager

> [!IMPORTANT]
> Apple recently changed from using the Apple Device Enrollment Program (DEP) to Apple Automated Device Enrollment (ADE). Intune is in the process of updating the Intune user interface to reflect that. Until such changes are complete, you'll continue to see *Device Enrollment Program* in the Intune portal. Wherever that is shown, it now uses Automated Device Enrollment.

You can set up Intune enrollment for macOS devices purchased through Apple's [Apple Business Manager](https://business.apple.com/) or [Apple School Manager](https://school.apple.com/). You can use either of these enrollments for large numbers of devices without ever touching them. You can ship macOS devices directly to users. When the user turns on the device, Setup Assistant runs with preconfigured settings and the device enrolls into Intune management.

To set up enrollment, you use both the Intune and Apple portals. You create enrollment profiles containing settings that applied to devices during enrollment.

Neither Apple Business Manager enrollment or Apple School Manager work with the [device enrollment manager](device-enrollment-manager-enroll.md).

<!--
**Steps to enable enrollment programs from Apple**
1. [Get an Apple DEP token and assign devices](#get-the-apple-dep-token)
2. [Create an enrollment profile](#create-an-apple-enrollment-profile)
3. [Synchronize DEP-managed devices](#sync-managed-device)
4. [Assign DEP profile to devices](#assign-an-enrollment-profile-to-devices)
5. [Distribute devices to users](#end-user-experience-with-managed-devices)
-->

## Prerequisites

- Devices purchased in [Apple School Manager](https://school.apple.com/) or [Apple's Automated Device Enrollment](http://deploy.apple.com)
- A list of serial numbers or a purchase order number.
- [MDM Authority](../fundamentals/mdm-authority-set.md)
- [Apple MDM Push certificate](../enrollment/apple-mdm-push-certificate-get.md)

## Get an Apple ADE token

Before you can enroll macOS devices with ADE or Apple School Manager, you need a token (.p7m) file from Apple. This token lets Intune sync information about the devices that your organization owns. It also lets Intune upload enrollment profiles to Apple and assign these profiles to devices.

You use the Apple portal to create a token. You also use the Apple portal to assign devices to Intune for management.

### Step 1. Download the Intune public key certificate required to create the token

1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **macOS** > **macOS enrollment**. 
2. Select **Enrollment program tokens**. 
3. Select **Add**.  
4. Select **I agree** to grant permission to Microsoft to send user and device information to Apple. 
3. Select **Download your public key** and save it locally. The PEM file (.pem) is an encryption key used to request a trust-relationship certificate from Apple Business Manager.    

### Step 2. Use your key to download a token from Apple  

1. Select the Apple portal used by your organization. Your options: 
    * **Create a token via Apple Business Manager** 
    * **Create a token via Apple School Manager**  
2. Sign in to Apple Business Manager or Apple School Manager with your company Apple ID. You can use this Apple ID to renew your token.
3. Select your account name, and then go to **Preferences**. 
4. Go to your MDM server assignments.  
5. Select the option to add an MDM server.  
6. Name the MDM server. The name is for identification purposes only while in Apple Business Manager or Apple School Manager, and doesn't have to be the actual name or URL of the Microsoft Intune server. 
7. Upload your public key file and then save your changes. 
8. Download the server token.  

### Best practices  

While you're in Apple Business Manager or Apple School Manager, apply device filters and assign devices to the MDM server.   

   * Apply filters: To filter devices before assigning them to your MDM server, go to **Devices** > **Filter**. You can filter devices by:  

        * Device management    
        * Source  
        * Order number 
        * Device type  
        * Storage size  

   * Bulk assign devices: Assign all eligible devices to an MDM server at the same time.     
        1. Go to your devices and select the ones you want to assign.  
        2. Select **Edit MDM Server**.  
        3. Select the MDM server you want to use and then continue to the next step. 
        5. When prompted to, confirm your changes. A notification appears to confirm that the devices have been assigned to the new MDM server.  

Apple Business Manager and Apple School Manager keep track of your activity and changes. Go to your activity area in the portal to view assignment results and download logs.   

### Step 3. Save the Apple ID used to create this token

Return to the [admin center](https://go.microsoft.com/fwlink/?linkid=2109431) and enter your Apple ID so that you have record of it in the future.   

![Screenshot highlighting the Apple ID field in the "Add enrollment program token" pane. ](./media/device-enrollment-program-enroll-ios/image03.png)  

### Step 4. Upload your token

Under **Apple token**, browse to the certificate (PEM file). Choose **Open**, and then choose **Create**. The push certificate enables Intune to enroll devices, and deploy policies to enrolled devices. Intune automatically connects with Apple Business Manager or Apple School Manager to sync your enrollment program account.  

## Create an Apple enrollment profile

Now that you've installed your token, you can create an enrollment profile for devices. A device enrollment profile defines the settings applied to a group of devices during enrollment.

1. In the [admin center](https://go.microsoft.com/fwlink/?linkid=2109431), return to **macOS Enrollment** > **Enrollment program tokens**.  
2. Select a token.
3. Select **Profiles** > **Create profile** > **macOS**.  

    ![Create a profile screenshot.](./media/device-enrollment-program-enroll-macos/image04.png)

4. On the **Basics** page, enter a name and description for the profile for administrative purposes. Users do not see these details. 

   >[!TIP]
   > You can use the name field to create a dynamic group in Azure Active Directory, and assign devices to the enrollment profile automatically. Use the profile name to define the *enrollmentProfileName* parameter. For more information, see [Azure Active Directory dynamic groups](/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices).  

4. For **Platform**, select **macOS**.  

5. Select **Next**. 

5. On the **Management Settings** page, configure **User Affinity**.  Your options: 

    * Option 1 - **Enroll with User Affinity**: Enroll devices that are associated with a single user. Choose this option for personal devices that belong to employees or students. Users need to use the Company Portal app to install apps. Multifactor authentication (MFA) is available with this option.   

      This option requires users to authenticate before enrollment. Select one of the following authentication methods:   

      - **Setup Assistant with modern authentication**: This method requires users to complete all Setup Assistant screens and sign in to the Company Portal app with their Azure AD credentials before they can access resources.  After they sign in to Company Portal, the device:   

        - Registers with Azure AD.  
        - Becomes visible in the user’s device list in Azure AD.  
        - Gains access to resources protected by conditional access.
        - Can be evaluated for device compliance.

        If the user doesn't sign in to the Company Portal to complete registration, they'll be redirected to the Company Portal app each time they try to open a managed app that's protected by conditional access.  

        Devices running macOS 10.15 and later can use this method. Older macOS devices will fall back to using the legacy Setup Assistant method.  

        For more information about how to get the Company Portal app to Mac users, see [Add the Company Portal for macOS app](../apps/apps-company-portal-macos.md).    

      - **Setup Assistant (legacy)**: Use the legacy Setup Assistant if you want users to experience the typical, out-of-box-experience for Apple products. This method installs standard preconfigured settings when the device enrolls with Intune management. If you're using Active Directory Federation Services and you're using Setup Assistant to authenticate, a [WS-Trust 1.3 Username/Mixed endpoint](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff608241(v=ws.10)) is required. For more information about retrieving the ADFS endpoint, see [Get-ADfsEndpoint] (/powershell/module/adfs/get-adfsendpoint?view=win10-ps&preserve-view=true).

  - Option 2 - **Enroll without User Affinity**:  Enroll devices that aren't associated with a single user. Use this for shared devices and devices that don't need to access local user data. The Company Portal app doesn't work on these types of devices.   

8. For **Locked enrollment**, choose whether or not users can unenroll their  devices. Select **Yes** to disable the macOS settings that allow users to remove the management profile in System Preferences or Terminal. After device enrollment, you cannot change this setting without wiping the device.  

9. Select **Next**.   

10. On the **Setup Assistant** page, configure the Setup Assistant experience.
    
    1. Enter the following information: 
        * **Department Name**: This name appears when device users select **About Configuration** during activation. 
        * **Department Phone**: This phone number appears when device users select **Need Help** during activation.   
    2. Show or hide Setup Assistant screens during device setup. Your options:  
        * **Hide**: The screen doesn't appear to users during setup. After device setup, the user can still go to their device settings to set up the feature.  
        * **Show**: The screen appears during device setup. The user can skip screens that don't require immediate action. After device setup, the user can go to their device settings to set up the feature. 
       For a description of all Setup Assistant screens you can configure, see [Setup Assistant screens](#setup-assistant-screens) in this article. 

11. Select **Next**.

12. Select **Create** to finish creating the profile.   

### Setup Assistant screens  
This table describes the purpose of each Setup Assistant screen during device setup.  

| Setup Assistant screen settings | If you choose **Show**, during setup the device will... |
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

## Sync managed devices

Now that Intune has permission to manage your devices, you can sync Intune with Apple, and see your managed devices in the admin center.  

1. Return to **Enrollment program tokens** and choose your enrollment program token. 

2. Select **Devices** > **Sync**.  

   ![Screenshot of Enrollment program token area in the admin center, highlighting the example token, "Devices" link, and "Sync" button.](./media/device-enrollment-program-enroll-macos/image06.png)  

To comply with Apple's terms for acceptable enrollment program traffic, Microsoft Intune imposes the following restrictions:  
 - A full sync can run no more than once every seven days. During a full sync, Intune fetches the complete updated list of serial numbers assigned to the Apple MDM server connected to Intune. If you delete a device from Intune without unassigning it from the Apple MDM server in Apple Business Manager or Apple School Manager, it won't be re-imported into Intune until the full sync is run. 
 - If a device is released from ABM/ASM, it can take up to 45 days for it to be automatically deleted from the devices page in Intune. You can manually delete released devices from Intune one by one if needed. Released devices will be accurately reported as being Removed from ABM/ASM in Intune until they are automatically deleted within 30-45 days.
 - A sync is run automatically every 24 hours. You can also sync by clicking the **Sync** button (no more than once every 15 minutes). All sync requests are given 15 minutes to finish. The **Sync** button is disabled until a sync is completed. This sync will refresh existing device status and import new devices assigned to the Apple MDM server.

## Assign an enrollment profile to devices

You must assign an enrollment program profile to devices before they can enroll.

1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **macOS** > **macOS Enrollment** > **Enrollment program tokens** > choose a token in the list.
2. Choose **Devices** > choose devices in the list > **Assign profile**.
3. Under **Assign profile**, choose a profile for the devices > **Assign**.

### Assign a default profile

You can pick a default macOS and iOS/iPadOS profile to be applied to all devices enrolling with a specific token.

1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **macOS** > **macOS Enrollment** > **Enrollment program tokens** > choose a token in the list.
2. Choose **Set Default Profile**, choose a profile in the drop-down list, and then choose **Save**. This profile will be applied to all devices that enroll with the token.

## Distribute devices

You have enabled management and syncing between Apple and Intune, and assigned a profile to let your devices enroll. You can now distribute devices to users. Devices with user affinity require each user be assigned an Intune license. Devices without user affinity require a device license.

Devices registered with ABM/ASM and assigned a profile in Intune can be enrolled:

- During Setup Assistant for new devices or wiped devices.
- After Setup Assistant using the profiles command.

### Enroll your macOS device registered in ABM/ASM with Automated Device Enrollment during Setup Assistant

Devices configured in ABM/ASM will automatically enroll into management with Intune during Setup Assistant with a Remote Management prompt.

> [!NOTE]
> If the device was assigned to a macOS enrollment profile with user affinity, you must sign in to the Company Portal for Azure AD registration and Conditional Access.

### Enroll your macOS device registered in ABM/ASM with Automated Device Enrollment after Setup Assistant

For macOS 10.13 and later devices, you can follow these steps to enroll.

1. In the Apple Business Manager or Apple School Manager portal, import the device.
2. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), make sure that the device is assigned a macOS enrollment profile with or without user affinity.
3. Log in to the device as a local administrator account.
4. To trigger enrollment, on the **Home** page, open **Terminal** and run the following command:
    sudo profiles renew -type enrollment
5. Enter your device password for the local administrator account.
6. In the **Device enrollment** window, choose **Details**.
7. In the **System preferences** window, choose **Profiles**.
8. Follow the prompts that will download the management profile, certs, and policies from Intune. You can view the profiles on the device anytime by going to **System Preferences** > **Profiles**.
9. If the device was assigned to a macOS enrollment profile with user affinity, you must sign in to the Company Portal for Azure AD registration and Conditional Access.

## Renew an ADE token

1. Go to [business.apple.com](http://business.apple.com) and sign in with an account that has the role of Administrator or Device Enrollment Manager.
2. Choose **Settings** > under **MDM Servers** choose your MDM server associated with the token file that you want to renew > **Download Token**.

    ![Screenshot of Download Token.](./media/device-enrollment-program-enroll-macos/download-token.png)

3. Choose **Download Server Token**.
4. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Device enrollment** > **Apple Enrollment** > **Enrollment program tokens** > choose the token.
    ![Screenshot of enrollment program tokens.](./media/device-enrollment-program-enroll-ios/enrollmentprogramtokens.png)

5. Choose **Renew token** and enter the Apple ID used to create the original token.  
    ![Screenshot of generate new token.](./media/device-enrollment-program-enroll-ios/renewtoken.png)

6. Upload the newly downloaded token.  
7. Choose **Renew token**. You'll see the confirmation that the token was renewed.
    ![Screenshot of confirmation.](./media/device-enrollment-program-enroll-macos/confirmation.png)

## Next steps

After enrolling macOS devices, you can start [managing them](../remote-actions/device-management.md).
