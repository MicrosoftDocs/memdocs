---
# required metadata

title: Enroll iOS/iPadOS devices by using ADE
titleSuffix: Microsoft Intune
description: Learn how to enroll corporate-owned iOS/iPadOS devices by using Automated Device Enrollment (ADE), previously known as Device Enrollment Program (DEP).
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 12/21/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 7ddbf360-0c61-11e8-ba89-0ed5f89f718b

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: tisilver
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: seodec18
ms.collection: M365-identity-device-management
---

# Automatically enroll iOS/iPadOS devices by using Apple's Automated Device Enrollment

> [!IMPORTANT]
> Apple recently changed from using the Apple Device Enrollment Program (DEP) to using Apple Automated Device Enrollment (ADE). The Microsoft Intune user interface doesn't currently reflect that change. Currently, you'll still see *Device Enrollment Program* in the Intune portal. Wherever you see references to DEP, Intune now uses Automated Device Enrollment.

You can set up Intune to enroll iOS/iPadOS devices purchased through Apple's [Automated Device Enrollment (ADE)](https://deploy.apple.com). Automated Device Enrollment lets you enroll large numbers of devices without ever touching them. Devices like iPhones, iPads, and MacBooks can be shipped directly to users. When a user turns on the device, Setup Assistant, which includes the typical out-of-box-experience for Apple products, runs with preconfigured settings and the device enrolls into management.

To enable ADE, you use the Intune portal and either the [Apple Business Manager (ABM)](https://business.apple.com/) portal or the [Apple School Manager (ASM)](https://school.apple.com/) portal. In either Apple portal, you need a list of serial numbers or a purchase order so you can assign devices to Intune for management. You create ADE enrollment profiles in Intune. These profiles contain settings that are applied to devices during enrollment. ADE can't be used with a [Device Enrollment Manager](device-enrollment-manager-enroll.md) account.

> [!NOTE]
> ADE sets device configurations that can't necessarily be removed by end users. Therefore, before ADE is used, the device must be wiped to return it to an out-of-box (new) state. For more information, see [Deployment guide: Enroll iOS and iPadOS devices](../fundamentals/deployment-guide-enrollment-ios-ipados.md).

If you experience sync problems during the enrollment process, you can look for solutions at [Troubleshoot iOS/iPadOS device enrollment problems](/troubleshoot/mem/intune/troubleshoot-ios-enrollment-errors#error-messages).

## Automated Device Enrollment and Company Portal

ADE enrollments aren't compatible with the App Store version of the Company Portal app. You can give users access to the Company Portal app on an ADE device. You might want to provide this access for one of the following reasons: 
- To let users choose which corporate apps they want to use on their devices 
- To use modern authentication to complete the enrollment process
- To provide a staged enrollment in which the device is enrolled and receives device policies before users authenticate in Company Portal 

To enable modern authentication during enrollment, push the app to the device by using **Install Company Portal with VPP** (Volume Purchase Program) in the ADE profile. For more information, see [Automatically enroll iOS/iPadOS devices with Apple's ADE](device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile).

To enable Company Portal to update automatically and provide the Company Portal app on devices already enrolled with ADE, deploy the Company Portal app through Intune as a required VPP app with an [application configuration policy](../apps/app-configuration-policies-use-ios.md) applied. Deploy the Company Portal app in this way to enable Device Staging. With Device Staging, a device is fully enrolled and receives device policies before the addition of a user affinity.

## What is supervised mode?

Apple introduced supervised mode in iOS/iPadOS 5. An iOS/iPadOS device in supervised mode provides more management control, like blocking of screen captures and blocking of the installation of apps from App Store. So it's especially useful for corporate-owned devices. Intune supports configuring devices for supervised mode as part of ADE.

Support for unsupervised ADE devices was deprecated in iOS/iPadOS 11. In iOS/iPadOS 11 and later, ADE-configured devices should always be supervised. The ADE *is_supervised* flag will be ignored in iOS/iPadOS 13.0 and later. All iOS/iPadOS devices with version 13.0 and later are automatically supervised when enrolled with Automated Device Enrollment. 

<!--
**Steps to enable enrollment programs from Apple**
1. [Get an Apple DEP token and assign devices](#get-the-apple-dep-token)
2. [Create an enrollment profile](#create-an-apple-enrollment-profile)
3. [Synchronize DEP-managed devices](#sync-managed-device)
4. [Assign DEP profile to devices](#assign-an-enrollment-profile-to-devices)
5. [Distribute devices to users](#end-user-experience-with-managed-devices)
-->
## Prerequisites
- Devices purchased in [Apple's ADE](https://deploy.apple.com)
- [Mobile device management (MDM) authority](../fundamentals/mdm-authority-set.md)
- An [Apple MDM push certificate](apple-mdm-push-certificate-get.md)

## Supported volume

- Maximum enrollment profiles per token: 1,000.  
- Maximum Automated Device Enrollment devices per profile: Same as the maximum number of devices per token (200,000 devices per token).
- Maximum Automated Device Enrollment tokens per Intune account: 2,000.
- Maximum Automated Device Enrollment devices per token: We recommend that you don't exceed 200,000 devices per token. Otherwise you might have sync problems. If you have more than 200,000 devices, split the devices into multiple ADE tokens.
    - About 3,000 devices per minute sync from ABM/ASM over to Intune. We recommend that you wait to manually sync again from the admin console until enough time has passed for all of the devices to sync over (total number of devices/3,000 devices per minute).

## Get an Apple Automated Device Enrollment token

Before you can enroll iOS/iPadOS devices with ADE, you need an ADE token (.p7m) file from Apple. This token lets Intune sync information about ADE devices that your corporation owns. It also allows Intune to upload enrollment profiles to Apple and to assign devices to those profiles.

You use the [Apple Business Manager (ABM)](https://business.apple.com/) or [Apple School Manager (ASM)](https://school.apple.com/) portal to create a token. You also use the ABM or ASM portal to assign devices to Intune for management.

> [!NOTE]
> You can use either the ABM portal or the ASM portal to enable ADE. The rest of this article refers to the ABM portal, but the steps are the same for both portals. 

### Step 1: Download the Intune public key certificate

1. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **iOS/iPadOS** > **iOS/iPadOS enrollment**:

    :::image type="content" source="./media/device-enrollment-program-enroll-ios/ios-enroll.png" alt-text="Screenshot that shows Microsoft Endpoint Manager admin center.":::

2. Select **Enrollment Program Tokens** > **Add**.

3. On the **Basics** tab:

    1. Select **I agree** to give permission to Microsoft to send user and device information to Apple:

        :::image type="content" source="./media/device-enrollment-program-enroll-ios/add-enrollment-program-token-pane.png" alt-text="Screenshot that shows the Add enrollment program token screen.":::
        
    2. Select **Download the Intune public key certificate required to create the token**. This step downloads and saves the encryption key (.pem) file locally. The .pem file is used to request a trust-relationship certificate from the Apple Business Manager portal.

        You'll upload this .pem file in Apple Business Manager in [Step 2: Go to the Apple Business Manager portal](#step-2-go-to-the-apple-business-manager-portal) (in this article).

    3. Keep this web browser tab and page open. If you close the tab:
    
        - The certificate you downloaded is invalidated.
        - You have to repeat steps.
        - On the **Review + create** tab, the **Create** button isn't available, and you can't complete this procedure.

### Step 2: Go to the Apple Business Manager portal

Use the Apple Business Manager portal to create and renew your ADE token (MDM server). This token is added to Intune and communicates between Intune and Apple.

> [!NOTE]
> The following steps describe what you need to do in Apple Business Manager. For the specific steps, refer to Apple's documentation. [Apple Business Manager User Guide](https://support.apple.com/guide/apple-business-manager/welcome/web) (on Apple's website) might be helpful.

#### Download the Apple token

1. In [Apple Business Manager](https://business.apple.com), sign in with your company's Apple ID.
2. In this portal, complete the following steps.

    - In settings, all tokens are shown. Add an MDM server, and upload the public key certificate (.pem file) that you downloaded from Intune in [Step 1: Download the Intune public key certificate](#step-1-download-the-intune-public-key-certificate) (in this article).
    
      Use the server name to identify the mobile device management (MDM) server. It isn't the name or URL of the Microsoft Intune service.
    
    - After you save the MDM server, select it, and then download the token (.p7m file). You'll upload this .p7m token in Intune in [Step 4: Upload your token and finish](#step-4-upload-your-token-and-finish) (in this article).

#### Assign devices to the Apple token (MDM server)

1. In [Apple Business Manager](https://business.apple.com) > **Devices**, select the devices you want to assign to this token. You can sort by various device properties, like serial number. You can also select multiple devices simultaneously.
2. Edit device management, and select the MDM server you just added. This step assigns devices to the token.

### Step 3: Save the Apple ID

1. In your web browser, go back to the **Add enrollment program token** page in Intune. You should have kept this page open, as noted in [Step 1: Download the Intune public key certificate](#step-1-download-the-intune-public-key-certificate) (in this article).
2. In **Apple ID**, enter your ID. This step saves the ID. The ID can be used in the future.

    :::image type="content" source="./media/device-enrollment-program-enroll-ios/image03.png" alt-text="Sreenshot that shows the Apple ID box on the Basics tab.":::

### Step 4: Upload your token and finish

1. In **Apple token**, browse to the .p7m certificate file, and then select **Open**.

    You downloaded this .p7m token in [Step 2: Go to the Apple Business Manager portal](#step-2-go-to-the-apple-business-manager-portal).

2. Select **Next**.

3. (Optional.) If you want to apply [scope tags](../fundamentals/scope-tags.md) to this ADE token, click **Select scope tags**, and then select existing scope tags. Scope tags applied to a token are inherited by profiles and devices added to the token.

    For more information on scope tags, see [Use role-based access control (RBAC) and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

3. On the **Review + create** tab, select **Create**.

With the push certificate, Intune can enroll and manage iOS/iPadOS devices by pushing policies to enrolled mobile devices. Intune automatically synchronizes with Apple to access your enrollment program account.

## Create an Apple enrollment profile

Now that you've installed your token, you can create an enrollment profile for ADE devices. A device enrollment profile defines the settings applied to a group of devices during enrollment. There's a limit of 1,000 enrollment profiles per ADE token.

> [!NOTE]
> Devices will be blocked if there aren't enough Company Portal licenses for a VPP token or if the token is expired. Intune will display an alert when a token is about to expire or licenses are running low.
 

1. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **iOS/iPadOS** > **iOS/iPadOS enrollment** > **Enrollment Program Tokens**.
2. Select a token, and then select **Profiles** > **Create profile** > **iOS/iPadOS**:

    :::image type="content" source="./media/device-enrollment-program-enroll-ios/image04.png" alt-text="Screenshot that shows how to create an iOS and iPadOS enrollment profile in Microsoft Endpoint Manager admin center.":::

3. On the **Basics** tab, enter a **Name** and **Description** for the profile for administrative purposes. Users don't see these details. 

    :::image type="content" source="./media/device-enrollment-program-enroll-ios/image05.png" alt-text="Screenshot that shows the Name and Description boxes in Microsoft Endpoint Manager admin center.":::

4. Select **Next**.

5. In the **User Affinity** list, select an option that determines whether devices with this profile must enroll with or without an assigned user.
    - **Enroll with User Affinity**. Select this option for devices that belong to users who want to use Company Portal for services like installing apps. If you're using Active Directory Federation Services and you're using Setup Assistant to authenticate, a [WS-Trust 1.3 Username/Mixed endpoint](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff608241(v=ws.10)) is required. [Learn more](/powershell/module/adfs/get-adfsendpoint?view=win10-ps&preserve-view=true).

    - **Enroll without User Affinity**. Select this option for devices that aren't affiliated with a single user. Use this option for devices that don't access local user data. This option is typically used for kiosk, point of sale (POS), or shared-utility devices.
    
      In some situations, you might want to associate a primary user on devices enrolled without user affinity. To do this task, you can send the `IntuneUDAUserlessDevice` key to the Company Portal app in an app configuration policy for managed devices. The first user that signs in to the Company Portal app is established as the primary user. If the first user signs out and a second user signs in, the first user remains the primary user of the device. For more information, see [Configure the Company Portal app to support iOS and iPadOS ADE devices](../apps/app-configuration-policies-use-ios.md#configure-the-company-portal-app-to-support-ios-and-ipados-devices-enrolled-with-automated-device-enrollment). 

6. If you chose **Enroll with User Affinity**, you can let users authenticate with Company Portal instead of the Apple Setup Assistant:

    :::image type="content" source="./media/device-enrollment-program-enroll-ios/authenticatewithcompanyportal.png" alt-text="Screenshot that shows the User Affinity & Authentication Method section.":::

    > [!NOTE]
    > Authenticate with the Company Portal app if you want to:
    >
    >  - Use multifactor authentication.
    >  - Prompt users to change their passwords when they first sign in.
    >  - Prompt users to reset their expired passwords during enrollment.
    >
    > These features aren't supported when you authenticate by using Apple Setup Assistant.
    >
    > For more information on enrolling iOS/iPadOS devices, see [Deployment guide: Enroll iOS and iPadOS devices in Microsoft Intune](../fundamentals/deployment-guide-enrollment-ios-ipados.md).

7. If you selected **Company Portal** for your authentication method, you can use a VPP token to automatically install Company Portal on the device. In this case, the user doesn't have to provide an Apple ID. To install Company Portal by using a VPP token, select a token in **Install Company Portal with VPP**. You need to have already added Company Portal to the VPP token. To ensure that Company Portal continues to be updated after enrollment, make sure that you've configured an app deployment in Intune (In Endpoint Manager select **Apps** > **All apps** > **Add**). 
 
   To ensure that user interaction isn't required, you'll probably want to make Company Portal an iOS/iPadOS VPP app, make it a required app, and use device licensing for the assignment. Make sure that the token doesn't expire and that you have enough device licenses for Company Portal. If the token expires or runs out of licenses, Intune installs the App Store Company Portal instead and prompts for an Apple ID. 

    > [!NOTE]
    > If you set the authentication method to **Company Portal**, make sure that the device enrollment process is completed within the first 24 hours of the Company Portal download to the ADE device. Otherwise enrollment might fail, and a factory reset will be needed to enroll the device.
    
    :::image type="content" source="./media/device-enrollment-program-enroll-ios/install-cp-with-vpp.png" alt-text="Screenshot that shows the options for installing the Company Portal app with VPP.":::

8. If you selected **Setup Assistant** for the authentication method but you also want to use Conditional Access or deploy company apps on the devices, you need to install Company Portal on the devices and sign in to complete the Azure AD registration. To do so, select **Yes** for **Install Company Portal**. If you want users to receive Company Portal without having to authenticate in to the App Store, in **Install Company Portal with VPP**, select a VPP token. Make sure the token doesn't expire and that you have enough device licenses for the Company Portal app to deploy correctly.

9. If you select a token for **Install Company Portal with VPP**, you can lock the device in Single App Mode (specifically, the Company Portal app) right after the Setup Assistant completes. Select **Yes** for **Run Company Portal in Single App Mode until authentication** to set this option. To use the device, the user must first authenticate by signing in with Company Portal.

    Multifactor authentication isn't supported on a single device locked in Single App Mode. This limitation exists because the device can't switch to a different app to complete the second factor of authentication. If you want multifactor authentication on a Single App Mode device, the second factor must be on a different device.

    This feature is supported only for iOS/iPadOS 11.3.1 and later.

   :::image type="content" source="./media/device-enrollment-program-enroll-ios/single-app-mode.png" alt-text="Screenshot that shows the Run Company Portal in Single App Mode option.":::

10. If you want devices using this profile to be supervised, select **Yes** in the **Supervised** list:

    :::image type="content" source="./media/device-enrollment-program-enroll-ios/supervisedmode.png" alt-text="Screenshot that shows the Supervised option.":::

    Supervised devices give you more management options and disabled Activation Lock by default. Microsoft recommends that you use ADE as the mechanism for enabling supervised mode, especially if you're deploying large numbers of iOS/iPadOS devices. Apple Shared iPad for Business devices must be supervised.

    Users are notified that their devices are supervised in two ways:

    - The lock screen says: **This iPhone is managed by *company name*.**
    - The **Settings** > **General** > **About** screen says: **This iPhone is supervised. *Company name* can monitor your Internet traffic and locate this device.**

     > [!NOTE]
     > If a device is enrolled without supervision, you need to use Apple Configurator if you want to set it to supervised. To reset the device in this way, you need to connect it to a Mac with a USB cable. For more information, see [Apple Configurator Help](http://help.apple.com/configurator/mac/2.3).

11. In the **Locked enrollment** list, select **Yes** or **No**. Locked enrollment disables iOS/iPadOS settings that allow the management profile to be removed from the **Settings** menu. After device enrollment, you can't change this setting without wiping the device. To use this option, the device must have the **Supervised** management option set to **Yes**. 

    > [!NOTE]
    > If a device is enrolled with locked enrollment, the user won't be able to use **Remove Device** or **Factory Reset** in the Company Portal app. The options will be unavailable to the user. Also, the user won't be able to remove the device on the [Company Portal website](https://portal.manage.microsoft.com).
    >
    > If a BYOD device is converted to an Apple ADE device and enrolled with a profile that has locked enrollment enabled, the user will be allowed to use **Remove Device** and **Factory Reset** for 30 days. After 30 days, the options will be disabled or unavailable. For more information, see [Prepare devices manually](https://help.apple.com/configurator/mac/2.8/#/cad99bc2a859).

12. If you selected **Enroll without User Affinity** and **Supervised** in the previous steps, you need to decide whether to configure the devices to be [Apple Shared iPad for Business devices](https://support.apple.com/guide/mdm/shared-ipad-overview-cad7e2e0cf56/web). If you select **Yes** for **Shared iPad**, multiple users will be able to sign in to a single device. Users will authenticate by using their Managed Apple IDs and federated authentication accounts or by using a temporary session (like the Guest account). This option requires iOS/iPadOS 13.4 or later.

    If you configured your devices as Apple Shared iPad for Business devices, you need to set **Maximum cached users**. Set this value to the number of users that you expect to use the shared iPad. You can cache up to 24 users on a 32-GB or 64-GB device. If you choose a low number, it might take a while for your users' data to appear on their devices after they sign in. If you choose a high number, your users might not have enough disk space.  

    > [!NOTE]
    > If you want to set up Apple Shared iPad for Business, configure these settings: 
    > - In the **User Affinity** list, select **Enroll without User Affinity**.
    > - In the **Supervised** list, select **Yes**. 
    > - In the **Shared iPad** list, select **Yes**.
    >
    > Temporary sessions are enabled by default and allow your users to sign in to a shared iPad without a Managed Apple ID account. You can disable temporary sessions on shared iPads by configuring iOS/iPadOS Shared iPad [device restriction settings](../configuration/device-restrictions-ios.md).  

13. In the **Sync with computers** list, select an option for the devices that use this profile. If you select **Allow Apple Configurator by certificate**, you need to choose a certificate under **Apple Configurator Certificates**. 

     > [!NOTE]
     > If you set **Sync with computers** to **Deny all**, the port will be limited on iOS and iPadOS devices. The port will be limited to only charging. It will be blocked from using iTunes or Apple Configurator 2.
    >      
    >If you set **Sync with computers** to **Allow Apple Configurator by certificate**, make sure you have a local copy of the certificate that you can use later. You won't be able to make changes to the uploaded copy, and it's important to retain an copy of this certificate. If you want to connect to the iOS/iPadOS device from a macOS device or PC, the same certificate must be installed on the device making the connection to the iOS/iPadOS device.

14. If you selected **Allow Apple Configurator by certificate** in the previous step, choose an Apple Configurator certificate to import.

15. You can specify a naming format for devices that's automatically applied when they're enrolled and upon each successive check-in. To create a naming template, select **Yes** under **Apply device name template**. Then, in the **Device Name Template** box, enter the template to use for the names that use this profile. You can specify a template format that includes the device type and serial number. This feature supports iPhone, iPad, and iPod Touch. 

1. Select **Next: Setup Assistant Customization**.

17. On the **Setup Assistant Customization** tab, configure the following profile settings:


    | Department setting | Description |
    |---|---|
    | <strong>Department</strong> | Appears when users tap <strong>About Configuration</strong> during activation. |
    |    <strong>Department Phone</strong>     | Appears when users tap the <strong>Need Help</strong> button during activation. |

    You can choose to hide Setup Assistant screens on the device during user setup.
    - If you select **Hide**, the screen won't be displayed during setup. After setting up the device, the user can still go to the **Settings** menu to set up the feature.
    - If you select **Show**, the screen will be displayed during setup, but only if there are steps to complete after the restore or after the software update. Users can sometimes skip the screen without taking action. They can then later go to the device's **Settings** menu to set up the feature.


    | Setup Assistant Screens setting | If you select Show, during setup the device will... |
    |------------------------------------------|------------------------------------------|
    | <strong>Passcode</strong> | Prompt the user for a passcode. Always require a passcode for unsecured devices unless access is controlled in some other way. (For example, a kiosk mode configuration that restricts the device to one app.) For iOS/iPadOS 7.0 and later. |
    | <strong>Location Services</strong> | Prompt the user for their location. For macOS 10.11 and later, and iOS/iPadOS 7.0 and later. |
    | <strong>Restore</strong> | Display the **Apps & Data** screen. This screen gives users the option to restore or transfer data from iCloud Backup when they set up the device. For macOS 10.9 and later, and iOS/iPadOS 7.0 and later. |
    | <strong>iCloud and Apple ID</strong> | Give the user the options to sign in with their Apple ID and use iCloud. For macOS 10.9 and later, and iOS/iPadOS 7.0 and later.   |
    | <strong>Terms and conditions</strong> | Require the user to accept Apple's terms and conditions. For macOS 10.9 and later, and iOS/iPadOS 7.0 and later. |
    | <strong>Touch ID</strong> | Give the user the option to set up fingerprint identification for the device. For macOS 10.12.4 and later, and iOS/iPadOS 8.1 and later. |
    | <strong>Apple Pay</strong> | Give the user the option to set up Apple Pay on the device. For macOS 10.12.4 and later, and iOS/iPadOS 7.0 and later. |
    | <strong>Zoom</strong> | Give the user to the option to zoom the display when they set up the device. For iOS/iPadOS 8.3 and later. |
    | <strong>Siri</strong> | Give the user the option to set up Siri. For macOS 10.12 and later, and iOS/iPadOS 7.0 and later. |
    | <strong>Diagnostics Data</strong> | Display the **Diagnostics** screen. This screen gives the user the option to send diagnostic data to Apple. For macOS 10.9 and later, and iOS/iPadOS 7.0 and later. |
    | <strong>Restore Completed</strong> | Display the **Restore Completed** screen after a backup and restore is performed on the device. If this screen isn't shown, the user can't see whether a restore from backup was completed during Setup Assistant. |
    | <strong>Software Update Completed</strong> | Display the **Software Update Completed** screen if a software update is performed during Setup Assistant. If this screen isn't shown, the user can’t see whether a software update is performed during Setup Assistant.|
    | <strong>Display Tone</strong> | Give the user the option to turn on Display Tone. For macOS 10.13.6 and later, and iOS/iPadOS 9.3.2 and later. |
    | <strong>Privacy</strong> | Display the **Privacy** screen. For macOS 10.13.4 and later, and iOS/iPadOS 11.3 and later. |
    | <strong>Android Migration</strong> | Give the user the option to migrate data from an Android device. For iOS/iPadOS 9.0 and later.|
    | <strong>iMessage & FaceTime</strong> | Give the user the option to set up iMessage and FaceTime. For iOS/iPadOS 9.0 and later. |
    | <strong>Onboarding</strong> | Display onboarding informational screens for user education, like Cover Sheet and Multitasking and Control Center. For iOS/iPadOS 11.0 and later. |
    | <strong>Watch Migration</strong> | Give the user the option to migrate data from a watch device. For iOS/iPadOS 11.0 and later.|
    | <strong>Screen Time</strong> | Display the **Screen Time** screen. For macOS 10.15 and later, and iOS/iPadOS 12.0 and later. |
    | <strong>Software Update</strong> | Display the mandatory software update screen. For iOS/iPadOS 12.0 and later. |
    | <strong>SIM Setup</strong> | Give the user the option to add a cellular plan. For iOS/iPadOS 12.0 and later. |
    | <strong>Appearance</strong> | Display the **Appearance** screen. For macOS 10.14 and later, and iOS/iPadOS 13.0 and later. |
    | <strong>Device to Device Migration</strong> | Give the user the option to migrate data from an old device to this device. For iOS/iPadOS 13.0 and later. |
    | <strong>Registration</strong> | Display the registration screen. For macOS 10.9 and later. |
    | <strong>FileVault</strong> | Display the FileVault 2 encryption screen. For macOS 10.10 and later. |
    | <strong>iCloud diagnostics</strong> | Display the **iCloud Analytics** screen. For macOS 10.12.4 and later. |
    | <strong>iCloud Storage</strong> | Display the **iCloud Documents and Desktop** screen. For macOS 10.13.4 and later. |
    

18. Select **Next** to go to the **Review + create** tab.

19. To save the profile, select **Create**.

> [!NOTE]
> If you need to re-enroll your Automated Device Enrollment device, you need to first [add the serial number of the device as a corporate identifier](corporate-identifiers-add.md). You might need to re-enroll your ADE device if you're troubleshooting a problem, like if the device isn't receiving policy. To re-enroll:
> 1. Retire the device from the Intune console.
> 2. [Add the device's serial number as a corporate device identifier](corporate-identifiers-add.md).
> 3. Re-enroll the device by downloading Company Portal and completing device enrollment.


### Dynamic groups in Azure Active Directory

You can use the enrollment **Name** field to create a dynamic group in Azure Active Directory (Azure AD). For more information, see [Azure Active Directory dynamic groups](/azure/active-directory/users-groups-roles/groups-dynamic-membership).

You can use the profile name to define the [enrollmentProfileName parameter](/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices) to assign devices with this enrollment profile.

For the fastest policy delivery on ADE devices that have user affinity, make sure the enrolling user is a member, before device setup, of an Azure AD user group. 

If you assign dynamic groups to enrollment profiles, there might be a delay in delivering applications and policies to devices after the enrollment.


## Sync managed devices
Now that Intune has permission to manage your devices, you can synchronize Intune with Apple to see your managed devices in Intune in the Azure portal.

1. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **iOS/iPadOS** > **iOS/iPadOS enrollment** > **Enrollment Program Tokens**.

2. Select a token in the list, and then select **Devices** > **Sync**:

    :::image type="content" source="./media/device-enrollment-program-enroll-ios/image06.png" alt-text="Screenshot that shows how to sync iOS and iPadOS devices to an enrollment program token.":::

   To follow Apple's terms for acceptable enrollment program traffic, Intune imposes the following restrictions:
   - A full sync can run no more than once every seven days. During a full sync, Intune fetches the complete updated list of serial numbers assigned to the Apple MDM server connected to Intune. If an ADE device is deleted from the Intune portal, it should be unassigned from the Apple MDM server in the ADE portal. If it's not unassigned, it won't be reimported to Intune until the full sync is run.   
   - If a device is released from ABM/ASM, it can take up to 45 days for it to be automatically deleted from the devices page in Intune. You can manually delete released devices from Intune one by one if needed. Released devices will be accurately reported as being Removed from ABM/ASM in Intune until they are automatically deleted within 30-45 days. 
   - A sync is run automatically every 12 hours. You can also sync by selecting the **Sync** button (no more than once every 15 minutes). All sync requests are given 15 minutes to finish. The **Sync** button is disabled until a sync is completed. This sync will refresh existing device status and import new devices assigned to the Apple MDM server.   


## Assign an enrollment profile to devices

Before devices can be enrolled, you need to assign an enrollment program profile to them.

>[!NOTE]
>You can also assign serial numbers to profiles in the **Apple Serial Numbers** pane.

1. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **iOS/iPadOS** > **iOS/iPadOS enrollment** > **Enrollment Program Tokens**. Select a token in the list.
2. Select **Devices**. Select devices in the list, and then select **Assign profile**.
3. Under **Assign profile**, choose a profile for the devices, and then select **Assign**.

### Assign a default profile

You can pick a default profile to be applied to all devices that enroll with a specific token.

1. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **iOS/iPadOS** > **iOS/iPadOS enrollment** > **Enrollment Program Tokens**. Select a token in the list.
2. Select **Set Default Profile**, select a profile in the list, and then select **Save**. The profile will be applied to all devices that enroll with the token.

## Distribute devices

You enabled management and syncing between Apple and Intune and assigned a profile so your ADE devices can be enrolled. You're now ready to distribute devices to users. Some things to know: 

- Devices enrolled with user affinity require that each user be assigned an Intune license.
- Devices enrolled without user affinity typically don't have any associated users. These devices need to have an Intune device license. If devices enrolled without user affinity will be used by an Intune-licensed user, a device license isn't needed.

  To summarize, if a device has a user, the user needs to have an assigned Intune license. If the device doesn't have an Intune-licensed user, the device needs to have an Intune device license.

  For more information on Intune licensing, see [Microsoft Intune licensing](../fundamentals/licenses.md) and the [Intune planning guide](../fundamentals/intune-planning-guide.md).

- A device that's been activated needs to be wiped before it can enroll in Intune. After it's been wiped, you can apply the enrollment profile.

- If you're enrolling with ADE and user affinity, the following error can happen during setup:

  `The SCEP server returned an invalid response.`

   To resolve this error, you need to factory reset the device. This error occurs because of a 15-minute time limit on SCEP certificates, which is enforced for security.
  
For information on the end-user experience, see [Enroll your iOS/iPadOS device in Intune by using ADE](../user-help/enroll-your-device-dep-ios.md).

## Renew an Automated Device Enrollment token  

You'll sometimes need to renew your tokens:

- Renew your ADE token yearly. The Endpoint Manager admin center shows the expiration date.
- If the Apple ID password changes for the user who set up the token in Apple Business Manager, renew your enrollment program token in Intune and Apple Business Manager.
- If the user who set up the token in Apple Business Manager leaves the organization, renew your enrollment program token in Intune and Apple Business Manager.

### Renew your tokens

1. Go to [business.apple.com](http://business.apple.com) and sign in with an account that has an Administrator or Device Enrollment Manager role.
2. Select **Settings**. Under **MDM Servers**, select the MDM server associated with the token file that you want to renew. Select **Download Token**:

    :::image type="content" source="./media/device-enrollment-program-enroll-macos/download-token.png" alt-text="Screenshot that shows how to renew and download an Apple token in Apple Business Manager.":::

3. Select **Download Server Token**.

    > [!NOTE]
    > As it says in the prompt, don't select **Download Server Token** if you don't intend to renew the token. Doing so will invalidate the token being used by Intune (or any other MDM solution). If you already downloaded the token, be sure to continue with the next steps until the token is renewed.

4. After you download the token, go to [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431). Select **Devices** > **iOS/iPadOS** > **iOS/iPadOS enrollment** > **Enrollment program tokens**. Select the token.


5. Select **Renew token**. Enter the **Apple ID** used to create the original token (if it's not automatically populated):  

    :::image type="content" source="./media/device-enrollment-program-enroll-ios/renewtoken.png" alt-text="Screenshot that shows the Renew token page.":::

6. Upload the newly downloaded token.

7. Select **Next** to go to the **Scope tags** page. Assign scope tags if you want to.

8. Select **Renew token**. You'll see a confirmation that the token is renewed:

    :::image type="content" source="./media/device-enrollment-program-enroll-ios/confirmation.png" alt-text="Screenshot that shows the confirmation message.":::

## Delete an Automated Device Enrollment token from Intune

You can delete an enrollment profile token from Intune as long as:
- No devices are assigned to the token.
- No devices are assigned to the default profile.

To delete an enrollment profile token: 

1. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **iOS/macOS** > **iOS/macOS enrollment** > **Enrollment Program Tokens**. Select the token, and then select **Devices**.
2. Delete all the devices assigned to the token.
3. Go to **Devices** > **iOS/macOS** > **iOS/macOS enrollment** > **Enrollment Program Tokens**. Select the token, and then select **Profiles**.
4. If there's a default profile, delete it.
5. Go to **Devices** > **iOS/macOS** > **iOS/macOS enrollment** > **Enrollment Program Tokens**. Select the token, and then select **Delete**.

## Next steps

[Backup and restore scenarios for iOS/iPadOS](backup-restore-ios.md)

[iOS/iPadOS enrollment overview](ios-enroll.md)
