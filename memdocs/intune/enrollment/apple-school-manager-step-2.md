---
# required metadata

title: Apple School Manager - create enrollment profile
titleSuffix: Microsoft Intune
description: Learn how to create the enrollment profile in Intune for Apple School Manager enrollment.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 01/06/2025
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.assetid: 4c35a23e-0c61-11e8-ba89-0ed5f89f718b

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.collection:
- tier1
- M365-identity-device-management
---

# Create an Apple enrollment profile  
After you get your Apple token, you can create an enrollment profile for school devices. An essential part of setup is creating enrollment profiles. The profiles contain the settings that apply to devices during device enrollment. 

## Create a profile  

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Enrollment**.    
1. Select the **Apple** tab.  
1. Under **Bulk Enrollment Methods**, Choose **Enrollment program tokens**.  
1. Select a token.
1. Select **Profiles** > **Create profile** > **iOS/iPadOS**.  

1. Under **Create Profile**, enter a **Name** and **Description** for the profile, for administrative purposes. Users don't see these details. 

 ![Example screenshot of the profile name and description fields in the admin center.](./media/apple-school-manager-set-up-ios/image05.png)

>[!TIP]
> You can use the name you enter here to create a dynamic group in Microsoft Entra ID. To assign devices with this enrollment profile, for example, use the name to define the enrollmentProfileName parameter in your dynamic group rules. For more information, see [Microsoft Entra dynamic groups](/azure/active-directory/active-directory-groups-dynamic-membership-azure-portal#rules-for-devices).  


1. For **User Affinity**, decide if devices with this profile must enroll with an assigned user or without an assigned user.  
    - **Enroll with User Affinity** - Choose this option for devices that belong to users and that want to use the company portal for services like installing apps. This option also lets users authenticate their devices by using the company portal. If using ADFS, user affinity requires [WS-Trust 1.3 Username/Mixed endpoint](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff608241(v=ws.10)). [Learn more](/powershell/module/adfs/get-adfsendpoint).   Apple School Manager's Shared iPad mode requires user enroll without user affinity.

    - **Enroll without User Affinity** - Choose this option for devices unaffiliated with a single user, such as a shared device. Use this option for devices that perform tasks without accessing local user data. Apps like the Company Portal app don't work.

1. If you chose **Enroll with User Affinity**, you can let users authenticate with Company Portal, Setup Assistant (legacy), and Setup Assistant with modern authentication. Select the option.  For more information about authentication methods, see [Authentication methods for automated device enrollment in Intune](automated-device-enrollment-authentication.md).  

    > [!NOTE]
    > If you want do any of the following, set **Authenticate with Company Portal instead of Apple Setup Assistant** to **Yes**.
    >    - use multifactor authentication
    >    - prompt users who need to change their password when they first sign in
    >    - prompt users to reset their expired passwords during enrollment
    >
    > These aren't supported when authenticating with Apple Setup Assistant.

1. Choose **Device Management Settings** and choose if you want devices using this profile to be supervised.
    **Supervised** devices give you more management options and disabled Activation Lock by default. Microsoft recommends using ADE as the mechanism for enabling Intune's supervised mode, especially for organizations that are deploying large numbers of iOS/iPadOS devices.

    Users are notified that their devices are supervised in two ways:

   - The lock screen says: "This iPhone is managed by Contoso."
   - The **Settings** > **General** > **About** screen says: "This iPhone is supervised. Contoso can monitor your Internet traffic and locate this device."

     > [!NOTE]
     > A device enrolled without supervision can only be reset to supervised by using the Apple Configurator. Resetting the device in this manner requires connecting an iOS/iPadOS device to a Mac with a USB cable. Learn more about this on [Apple Configurator docs](https://support.apple.com/guide/apple-configurator-mac).

1. Choose if you want locked enrollment for devices using this profile. **Locked enrollment** disables iOS/iPadOS settings that allow the management profile to be removed from the **Settings** menu. After device enrollment, you can't change this setting without wiping the device. Such devices must have the **Supervised** Management Mode set to *Yes*. 

1. You can let multiple users sign on to enrolled iPads by using a managed Apple ID. To do so, choose **Yes** under **Shared iPad** (this option requires **Enroll without User Affinity** and **Supervised** mode set to **Yes**.) Managed Apple IDs are created in the Apple School Manager portal. Learn more about [shared iPad](../fundamentals/education-settings-configure-ios-shared.md) and [Apple's shared iPad requirements](https://help.apple.com/classroom/ipad/2.0/#/cad7e2e0cf56).

1. Choose if you want the devices using this profile to be able to **Sync with computers**. **Deny All** means that all devices using this profile won't be able to sync with any data on any computer. If you choose **Allow Apple Configurator by certificate**, you must choose a certificate under **Apple Configurator Certificates**.

1. If you chose **Allow Apple Configurator by certificate** in the previous step, choose an Apple Configurator Certificate to import.

1. You can specify a naming format for devices that is automatically applied when they enroll. To do so, select **Yes** under **Apply device name template**. Then, in the **Device Name Template** box, enter the template to use for the names using this profile. You can specify a template format that includes the device type and serial number.

1. Choose **OK**.

1. Choose **Setup Assistant Settings** to configure the following profile settings:  

    |                 Setting                  |                                                                                               Description                                                                                               |
    |------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
    |     <strong>Department Name</strong>     |                                                             Appears when users tap <strong>About Configuration</strong> during activation.                                                              |
    |    <strong>Department Phone</strong>     |                                                          Appears when the user clicks the <strong>Need Help</strong> button during activation.                                                          |
    | <strong>Setup Assistant Options</strong> |                                                     The following optional settings can be set up later in the iOS/iPadOS <strong>Settings</strong> menu.                                                      |
    |        <strong>Passcode</strong>         | Prompt for passcode during activation. Always require a passcode for unsecured devices unless access is controlled in some other manner (like kiosk mode that restricts the device to one app). |
    |    <strong>Location Services</strong>    |                                                                 If enabled, Setup Assistant prompts for the service during activation.                                                                  |
    |         <strong>Restore</strong>         |                                                                If enabled, Setup Assistant prompts for iCloud backup during activation.                                                                 |
    |   <strong>iCloud and Apple ID</strong>   |                         If enabled, Setup Assistant prompts the user to sign in an Apple ID and the Apps & Data screen will allow the device to be restored from iCloud backup.                         |
    |  <strong>Terms and Conditions</strong>   |                                                   If enabled, Setup Assistant prompts users to accept Apple's terms and conditions during activation.                                                   |
    |        <strong>Touch ID</strong>         |                                                                 If enabled, Setup Assistant prompts for this service during activation.                                                                 |
    |        <strong>Apple Pay</strong>        |                                                                 If enabled, Setup Assistant prompts for this service during activation.                                                                 |
    |          <strong>Zoom</strong>           |                                                                 If enabled, Setup Assistant prompts for this service during activation.                                                                 |
    |          <strong>Siri</strong>           |                                                                 If enabled, Setup Assistant prompts for this service during activation.                                                                 |
    |     <strong>Diagnostic Data</strong>     |                                                                 If enabled, Setup Assistant prompts for this service during activation.                                                                 |


1. Choose **OK**.

1. To save the profile, choose **Create**.  

## Next steps  
This series of articles describes how to set up Microsoft Intune for devices purchased through Apple School Manager. 

1. [Prerequisites](apple-school-manager-set-up-ios.md)
1. [Get an Apple token and assign devices](apple-school-manager-step-1.md)  
1. 🡺 Create an Apple enrollment profile (*You are here*)  
1. [Sync managed devices](apple-school-manager-step-3.md) 

