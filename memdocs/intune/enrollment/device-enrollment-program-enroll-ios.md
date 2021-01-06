---
# required metadata

title: Enroll iOS/iPadOS devices using Automated Device Enrollment
titleSuffix: Microsoft Intune
description: Learn how to enroll corporate-owned iOS/iPadOS devices using the Automated Device Enrollment (ADE), previously known as device enrollment program (DEP)
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

# Automatically enroll iOS/iPadOS devices with Apple's Automated Device Enrollment

> [!IMPORTANT]
> Apple recently changed from using the Apple Device Enrollment Program (DEP) to Apple Automated Device Enrollment (ADE). Intune is in the process of updating the Intune user interface to reflect that. Until such changes are complete, you'll continue to see *Device Enrollment Program* in the Intune portal. Wherever that is shown, it now uses Automated Device Enrollment.

You can set up Intune to enroll iOS/iPadOS devices purchased through Apple's [Automated Device Enrollment (ADE)](https://deploy.apple.com). Automated Device Enrollment lets you enroll large numbers of devices without ever touching them. Devices like iPhones, iPads, and MacBooks can be shipped directly to users. When the user turns on the device, Setup Assistant, which includes the typical out-of-box-experience for Apple products, runs with preconfigured settings and the device enrolls into management.

To enable ADE, you use both the Intune and [Apple Business Manager (ABM)](https://business.apple.com/) or [Apple School Manager (ASM)](https://school.apple.com/) portals. A list of serial numbers or a purchase order number is required so you can assign devices to Intune for management in either Apple portal. You create ADE enrollment profiles in Intune containing settings that are applied to devices during enrollment. ADE can't be used with a [device enrollment manager](device-enrollment-manager-enroll.md) account.

> [!NOTE]
> ADE sets device configurations that can't necessarily be removed by the end user. Therefore, before using ADE, the device must be wiped to return it to an out-of-box (new) state. For more information, see [Deployment guide: Enroll iOS and iPadOS devices](../fundamentals/deployment-guide-enrollment-ios-ipados.md).

If you experience any sync issues during this process, you can check for resolution options at [Troubleshoot iOS/iPadOS device enrollment problems](https://docs.microsoft.com/troubleshoot/mem/intune/troubleshoot-ios-enrollment-errors#error-messages).

## Automated Device Enrollment and the Company Portal

ADE enrollments aren't compatible with the app store version of the Company Portal app. You can give users access to the Company Portal app on an ADE device. You may want to provide this access to let users choose which corporate apps they wish to use on their device, to use modern authentication to complete the enrollment process, or to provide a staged enrollment in which the device is enrolled and receives device policies prior to a user authenticating in the Company Portal. 

To enable modern authentication during enrollment, push the app to the device using **Install Company Portal with VPP** (Volume Purchase Program) in the ADE profile. For more information, see [Automatically enroll iOS/iPadOS devices with Apple's ADE](device-enrollment-program-enroll-ios.md#create-an-apple-enrollment-profile).

To enable the Company Portal to update automatically and provide the Company Portal app on devices already enrolled with ADE, deploy the Company Portal app through Intune as a required Volume Purchase Program (VPP) app with an [Application Configuration policy](../apps/app-configuration-policies-use-ios.md) applied. Deploy the Company Portal app through Intune as a required VPP app with an Application Configuration policy to enable Device Staging, where a device is fully enrolled and receives device policies prior to the addition of a user affinity as well.

## What is supervised mode?

Apple introduced supervised mode in iOS/iPadOS 5. An iOS/iPadOS device in supervised mode can be managed with more controls, such as block screen capture and block installing apps from App Store. As such, it's especially useful for corporate-owned devices. Intune supports configuring devices for supervised mode as part of ADE.

Support for unsupervised ADE devices was deprecated in iOS/iPadOS 11. In iOS/iPadOS 11 and later, ADE configured devices should always be supervised. The ADE *is_supervised* flag will be ignored with iOS/iPadOS 13.0 and later. All iOS/iPadOS devices with version 13.0 and later are automatically supervised when enrolled with automated device enrollment. 

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
- [Mobile Device Management (MDM) Authority](../fundamentals/mdm-authority-set.md)
- [Apple MDM Push certificate](apple-mdm-push-certificate-get.md)

## Supported volume

- Maximum enrollment profiles per token: 1,000  
- Maximum Automated Device Enrollment devices per profile: within the maximum number of devices per token
- Maximum Automated Device Enrollment tokens per Intune account: 2,000
- Maximum Automated Device Enrollment devices per token: Intune recommends not exceeding 60,000 devices per token. Or, you might run into sync issues. If you have more than 60,000 devices, split the devices into multiple ADE tokens.

## Get an Apple Automated Device Enrollment token

Before you can enroll iOS/iPadOS devices with ADE, you need an ADE token (.p7m) file from Apple. This token lets Intune sync information about ADE devices that your corporation owns. It also permits Intune to upload enrollment profiles to Apple, and to assign devices to those profiles.

You use the [Apple Business Manager (ABM)](https://business.apple.com/) or [Apple School Manager (ASM)](https://school.apple.com/) portal to create a token. You also use the ABM/ASM portal to assign devices to Intune for management.

> [!NOTE]
> If you delete the token from the Intune classic portal before migrating to Azure, Intune might restore a deleted Apple ADE token. You can delete the ADE token again from the Azure portal.

### Step 1: Download the Intune public key certificate

1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **iOS/iPadOS** > **iOS/iPadOS enrollment**:

    :::image type="content" source="./media/device-enrollment-program-enroll-ios/ios-enroll.png" alt-text="Add or create a new iOS and iPadOS enrollment program token in Microsoft Intune and Endpoint Manager admin center.":::

2. Select **Enrollment Program Tokens** > **Add**.

3. In **Basics**:

    1. Select **I agree** to give permission to Microsoft to send user and device information to Apple:

        :::image type="content" source="./media/device-enrollment-program-enroll-ios/add-enrollment-program-token-pane.png" alt-text="Screenshot of Enrollment Program Token pane in Apple Certificates workspace to download public key in Microsoft Intune and Endpoint Manager admin center.":::
        
    2. Select **Download the Intune public key certificate required to create the token**. This step downloads and saves the encryption key (`.pem`) file locally. The `.pem` file is used to request a trust-relationship certificate from the Apple Business Manager portal.

        You will upload this `.pem` file in Apple Business Manager in [Step 2: Go to Apple Business Manager portal](#step-2-go-to-apple-business-manager-portal) (in this article).

    3. Keep this web browser tab and page open. Do not close the tab. If you do, then the following happens:
    
        - The certificate you downloaded is invalidated.
        - You will have to repeat the steps.
        - In **Review + create**, the **Create** button is grayed out, and you can't complete these steps.

### Step 2: Go to Apple Business Manager portal

Use the Apple Business Manager portal to create and renew your ADE token (MDM server). This token is added to Intune, and communicates between Intune and Apple.

> [!NOTE]
> The following steps state what you must do in Apple Business Manager. For the specific steps, refer to Apple's documentation. [Apple Business Manager User Guide](https://support.apple.com/guide/apple-business-manager/welcome/web) (opens Apple's web site) may help.

#### Download the Apple token

1. In [Apple Business Manager](https://business.apple.com), sign in with your company Apple ID.
2. In this portal, you must:

    - In settings, all the tokens are shown. Add an MDM server, and upload your public key certificate (`.pem` file) that you downloaded from Intune in [Step 1: Download the Intune public key certificate](#step-1-download-the-intune-public-key-certificate) (in this article).
    
      The server name is for you to identify the mobile device management (MDM) server. It isn't the name or URL of the Microsoft Intune service.
    
    - After you save the MDM server, select this MDM server, and download the token (`.p7m` file). You will upload this `.p7m` token in Intune in [Step 4: Upload your token and finish](#step-4-upload-your-token-and-finish) (in this article).

#### Assign devices to the Apple token (MDM server)

1. In [Apple Business Manager](https://business.apple.com) > Devices, select the devices you want to assign to this token. You can sort by different device properties, such as serial number. You can also select multiple devices simultaneously.
2. Edit device management, and select the MDM server you just added. This step assigns devices to the token.

### Step 3: Save the Apple ID

1. In your web browser, go back to the **Add enrollment program token** page in Intune. This page should have been kept open, as stated in [Step 1: Download the Intune public key certificate](#step-1-download-the-intune-public-key-certificate) (in this article).
2. In **Apple ID**, enter your Apple ID. This step saves your Apple ID, and can be used for future references.

    :::image type="content" source="./media/device-enrollment-program-enroll-ios/image03.png" alt-text="Enter the Apple ID that creates the enrollment program token in Microsoft Intune and Endpoint Manager admin center.":::

### Step 4: Upload your token and finish

1. In **Apple token**, browse to the `.p7m` certificate file > **Open**.

    You downloaded this `.p7m` token in [Step 2: Go to Apple Business Manager portal](#step-2-go-to-apple-business-manager-portal).

2. Select **Next**.

3. Optional. If you want to apply [scope tags](../fundamentals/scope-tags.md) to this ADE token, choose **Select scope tags**, and select existing scope tags. Scope tags applied to a token are inherited by profiles and devices added to this token.

    For more information on scope tags, see [Use role-based access control (RBAC) and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

3. In **Review + create**, select **Create**.

With the push certificate, Intune can enroll and manage iOS/iPadOS devices by pushing policies to enrolled mobile devices. Intune automatically synchronizes with Apple to see your enrollment program account.

## Create an Apple enrollment profile

Now that you've installed your token, you can create an enrollment profile for ADE devices. A device enrollment profile defines the settings applied to a group of devices during enrollment. There is a limit of 1000 enrollment profiles per ADE token.

> [!NOTE]
> Devices will be blocked if there aren't enough Company Portal licenses for a VPP token, or if the token has expired. Intune will display an alert when a token is about to expire or licenses are running low.
 

1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **iOS/iPadOS** > **iOS/iPadOS enrollment** > **Enrollment Program Tokens**.
2. Select a token, choose **Profiles** > **Create profile** > **iOS/iPadOS**.

    :::image type="content" source="./media/device-enrollment-program-enroll-ios/image04.png" alt-text="Create an iOS and iPadOS enrollment profile in Microsoft Intune and Endpoint Manager admin center.":::

3. On the **Basics** page, enter a **Name** and **Description** for the profile for administrative purposes. Users don't see these details. 

    :::image type="content" source="./media/device-enrollment-program-enroll-ios/image05.png" alt-text="Enter a name and description of the enrollment profile in Microsoft Intune and Endpoint Manager admin center.":::

4. Select **Next: Device Management Settings**.

5. For **User Affinity**, choose whether devices with this profile must enroll with or without an assigned user.
    - **Enroll with User Affinity** - Choose this option for devices that belong to users and that want to use the Company Portal for services like installing apps. If you're using ADFS and you're using Setup Assistant to authenticate, [WS-Trust 1.3 Username/Mixed endpoint](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff608241(v=ws.10)) [Learn more](/powershell/module/adfs/get-adfsendpoint?view=win10-ps&preserve-view=true) is required.

    - **Enroll without User Affinity** - Choose this option for devices unaffiliated with a single user. Use this option for devices that don't access local user data. This option is typically used for kiosk, point of sale (POS), or shared-utility devices.
    
      In some situations, you might want to associate a primary user on devices enrolled without user affinity. To do this task, you can send the `IntuneUDAUserlessDevice` key to the Company Portal app in an app configuration policy for managed devices. The first user that signs in to the Company Portal app is established as the primary user. If the first user signs out, and a second user signs in, then the first user remains the primary user of the device. For more information, see [Configure the Company Portal app to support iOS and iPadOS ADE devices](../apps/app-configuration-policies-use-ios.md#configure-the-company-portal-app-to-support-ios-and-ipados-devices-enrolled-with-automated-device-enrollment). 

6. If you chose **Enroll with User Affinity**, you can let users authenticate with Company Portal instead of the Apple Setup Assistant.

    :::image type="content" source="./media/device-enrollment-program-enroll-ios/authenticatewithcompanyportal.png" alt-text="Choose to authenticate with the Company Portal app on iOS and iPadOS devices in Microsoft Intune and Endpoint Manager admin center.":::

    > [!NOTE]
    > Authenticate with the Company Portal app if you want to:
    >
    >  - Use multifactor authentication (MFA).
    >  - When users first sign in, prompt them to change their password.
    >  - During enrollment, prompt users to reset their expired passwords.
    >
    > These features aren't supported when authenticating with Apple Setup Assistant.
    >
    > For more guidance on enrolling iOS/iPadOS devices, see [Deployment guide: Enroll iOS and iPadOS devices in Microsoft Intune](../fundamentals/deployment-guide-enrollment-ios-ipados.md).

7. If you chose **Company Portal** for **Authentication method**, you can use a VPP token to automatically install the Company Portal on the device. In this case, the user doesn't have to supply an Apple ID. To install the Company Portal with a VPP token, choose a token under **Install Company Portal with VPP**. Requires that the Company Portal has already been added to the VPP token. To ensure that the Company Portal app continue to be updated after enrollment, make sure that you have configured an app deployment in Intune (Intune>Client Apps). So that user interaction isn't required, you'll most likely want to have the Company Portal as a iOS/iPadOS VPP app, make it a required app, and use device licensing for the assignment. Make sure that the token doesn't expire and that you have enough device licenses for the Company Portal app. If the token expires or runs out of licenses, Intune installs the App Store Company Portal instead and prompts for an Apple ID. 

    > [!NOTE]
    > When **Authentication method** is to **Company Portal**, make sure that the device enrollment process is performed within the first 24 hours of the company portal being downloaded to the ADE device. Otherwise enrollment might fail, and a factory reset will be needed to enroll the device.
    
    :::image type="content" source="./media/device-enrollment-program-enroll-ios/install-cp-with-vpp.png" alt-text="Install the Company Portal app with VPP on iOS and iPadOS devices in Microsoft Intune and Endpoint Manager admin center.":::

8. If you chose **Setup Assistant** for **Authentication method**, but you also want to use Conditional Access or deploy company apps on the devices, you must install the Company Portal on the devices and sign in to complete the Azure AD registration. To do so, choose **Yes** for **Install Company Portal**.  If you would like users to receive the Company Portal without having to authenticate into the app store, choose to **Install Company Portal with VPP** and select a VPP token. Make sure that the token doesn't expire and that you have enough device licenses for the Company Portal app to deploy correctly.

9. If you chose a token for **Install Company Portal with VPP**, you can lock the device in Single App Mode (specifically, the Company Portal app) right after the Setup Assistant completes. Choose **Yes** for **Run Company Portal in Single App Mode until authentication** to set this option. To use the device, the user must first authenticate by signing in using the Company Portal.

    Multi-factor authentication isn't supported on a single device locked in Single App Mode. This limitation exists because the device can't switch to a different app to complete the second factor of authentication. Therefore, if you want multifactor authentication on a Single App Mode device, the second factor must be on a different device.

    This feature is only supported for iOS/iPadOS 11.3.1 and later.

   :::image type="content" source="./media/device-enrollment-program-enroll-ios/single-app-mode.png" alt-text="Run Company Portal app in single app mode on iOS and iPadOS devices in Microsoft Intune and Endpoint Manager admin center.":::

10. If you want devices using this profile to be supervised, choose **Yes** for **Supervised**.

    :::image type="content" source="./media/device-enrollment-program-enroll-ios/supervisedmode.png" alt-text="Enable supervised mode on iOS and iPadOS devices in enrollment profile in Microsoft Intune and Endpoint Manager admin center.":::

    **Supervised** devices give you more management options and disabled Activation Lock by default. Microsoft recommends using ADE as the mechanism for enabling supervised mode, especially if you're deploying large numbers of iOS/iPadOS devices. Apple Shared iPad for Business devices must be supervised.

    Users are notified that their devices are supervised in two ways:

   - The lock screen says: "This iPhone is managed by Contoso."
   - The **Settings** > **General** > **About** screen says: "This iPhone is supervised. Contoso can monitor your Internet traffic and locate this device."

     > [!NOTE]
     > A device enrolled without supervision can only be reset to supervised by using the Apple Configurator. Resetting the device in this manner requires connecting an iOS/iPadOS device to a Mac with a USB cable. Learn more about this on [Apple Configurator docs](http://help.apple.com/configurator/mac/2.3).

11. Choose if you want locked enrollment for devices using this profile. **Locked enrollment** disables iOS/iPadOS settings that allow the management profile to be removed from the **Settings** menu. After device enrollment, you can't change this setting without wiping the device. Such devices must have the **Supervised** Management Mode set to *Yes*. 

    > [!NOTE]
    > After the device is enrolled with **Locked enrollment**, users will not be able to use **Remove Device** or **Factory Reset** by in the Company Portal app. The options will be unavailable to the user. The user also won't be able to remove the device in the Company Portal website (https://portal.manage.microsoft.com).
    > Also, if a BYOD device is convereted to an Apple Automated Device Enrollment device and enrolled with a **Locked enrollment** enabled profile, the user will be allowed to use **Remove Device** and **Factory Reset** for 30 days, and then the options will be disabled or unavailable. Reference: https://help.apple.com/configurator/mac/2.8/#/cad99bc2a859.

12. If you chose **Enroll without User Affinity** and **Supervised** above, you must decide whether or not to configure the devices to be [Apple Shared iPad for Business devices](https://support.apple.com/guide/mdm/shared-ipad-overview-cad7e2e0cf56/web). By choosing **Yes** for **Shared iPad**, multiple users will be able to sign into the same device. The users will authenticate with their Managed Apple ID and federated authentication accounts or through a temporary session (such as the Guest account). This option requires iOS/iPadOS 13.4 or later.

    If you chose to configure your devices to be Apple Shared iPad for Business devices, you must set **Maximum cached users**. Set this value to the number of users that you expect to use the Shared iPad. You can cache up to 24 users on a 32 GB or 64 GB device. If you choose a very low number, it may take a while for your user’s data to come down to the device after sign-in. If you choose a very high number, your users may not have enough disk space.  

    > [!NOTE]
    > If you want to set up Apple Shared iPad for Business, set the following: 
    > - **User affinity** = **Enroll without User Affinity**. 
    > - **Supervised** = **Yes**. 
    > - **Shared iPad** = **Yes **.
    > Temporary sessions are enabled by default and allow your users to log into a Shared iPad without a Managed Apple ID account. You can disable temporary sessions on Shared iPad by configuring iOS/iPadOS Shared iPad [device restriction settings](../configuration/device-restrictions-ios.md).  

13. Choose if you want the devices using this profile to be able to **Sync with computers**. If you choose **Allow Apple Configurator by certificate**, you must choose a certificate under **Apple Configurator Certificates**. For iOS/iPadOS 13.0 and newer, this setting was deprecated by Apple. 

     > [!NOTE]
     > If **Sync with computers** is set to **Deny all**, the port will be limited on iOS and iPadOS devices. The port can only be used for charging and nothing else. The port will be blocked from using iTunes or Apple Configurator 2.
       If **Sync with computers** is set to **Allow Apple Configurator by certificate**, make sure you have a local copy of the certificate that you can access later. You won't be able to make changes to the uploaded copy and it is important to retain this certificate to be accessible in the future. To connect to the iOS/iPadOS device from a macOS device or PC, the same certificate must be installed on the device making the connection to the iOS/iPadOS device that was enrolled with the Automated Device Enrollment profile with this configuration and certificate.

14. If you chose **Allow Apple Configurator by certificate** in the previous step, choose an Apple Configurator Certificate to import.

15. You can specify a naming format for devices that is automatically applied when they enroll and upon each successive checkin. To create a naming template, select **Yes** under **Apply device name template**. Then, in the **Device Name Template** box, enter the template to use for the names using this profile. You can specify a template format that includes the device type and serial number. Device name template includes support for the iPhone, the iPad, and the iPod Touch. 
16. Choose **Next: Setup Assistant Customization**.

17. On the **Setup Assistant customization** page, configure the following profile settings:

    :::image type="content" source="./media/device-enrollment-program-enroll-ios/setupassistantcustom.png" alt-text="Customize Setup Assistant in iOS and iPadOS enrollment profile in Microsoft Intune and Endpoint Manager admin center.":::

    | Department settings | Description |
    |---|---|
    | <strong>Department Name</strong> | Appears when users tap <strong>About Configuration</strong> during activation. |
    |    <strong>Department Phone</strong>     | Appears when the user clicks the <strong>Need Help</strong> button during activation. |

    You can choose to hide Setup Assistant screens on the device during user setup.
    - If you choose **Hide**, the screen won't be displayed during setup. After setting up the device, the user can still go in to the **Settings** menu to set up the feature.
    - If you choose **Show**, the screen will be displayed during setup. The user can sometimes skip the screen without taking action. But they can then later go into the device's **Settings** menu to set up the feature. 


    | Setup Assistant screen settings | If you choose **Show**, during setup the device will... |
    |------------------------------------------|------------------------------------------|
    | <strong>Passcode</strong> | Prompt the user for a passcode. Always require a passcode for unsecured devices unless access is controlled in some other manner (like kiosk mode that restricts the device to one app). For iOS/iPadOS 7.0 and later. |
    | <strong>Location Services</strong> | Prompt the user for their location. For macOS 10.11 and later and iOS/iPadOS 7.0 and later. |
    | <strong>Restore</strong> | Display the Apps & Data screen. This screen gives the user the option to restore or transfer data from iCloud Backup when they set up the device. For macOS 10.9 and later, and iOS/iPadOS 7.0 and later. |
    | <strong>iCloud and Apple ID</strong> | Give the user the options to sign in with their Apple ID and use iCloud. For macOS 10.9 and later, and iOS/iPadOS 7.0 and later.   |
    | <strong>Terms and Conditions</strong> | Require the user to accept Apple's terms and conditions. For macOS 10.9 and later, and iOS/iPadOS 7.0 and later. |
    | <strong>Touch ID</strong> | Give the user the option to set up fingerprint identification for the device. For macOS 10.12.4 and later, and iOS/iPadOS 8.1 and later. |
    | <strong>Apple Pay</strong> | Give the user the option to set up Apple Pay on the device. For macOS 10.12.4 and later, and iOS/iPadOS 7.0 and later. |
    | <strong>Zoom</strong> | Give the user to the option to zoom the display when they set up the device. For iOS/iPadOS 8.3 and later. |
    | <strong>Siri</strong> | Give the user the option to set up Siri. For macOS 10.12 and later, and iOS/iPadOS 7.0 and later. |
    | <strong>Diagnostic Data</strong> | Display the Diagnostics screen to the user. This screen gives the user the option to send diagnostic data to Apple. For macOS 10.9 and later, and iOS/iPadOS 7.0 and later. |
    | <strong>Display Tone</strong> | Give the user the option to turn on Display Tone. For macOS 10.13.6 and later, and iOS/iPadOS 9.3.2 and later. |
    | <strong>Privacy</strong> | Display the Privacy screen to the user. For macOS 10.13.4 and later, and iOS/iPadOS 11.3 and later. |
    | <strong>Android Migration</strong> | Give the user the option to migrate date from an Android device. For iOS/iPadOS 9.0 and later.|
    | <strong>iMessage and FaceTime</strong> | Give the user the option to set up iMessage and FaceTime. For iOS/iPadOS 9.0 and later. |
    | <strong>Onboarding</strong> | Display onboarding informational screens for user education, such as Cover Sheet and Multitasking and Control Center. For iOS/iPadOS 11.0 and later. |
    | <strong>Watch Migration</strong> | Give the user the option to migrate data from a watch device. For iOS/iPadOS 11.0 and later.|
    | <strong>Screen Time</strong> | Display the Screen Time screen. For macOS 10.15 and later, and iOS/iPadOS 12.0 and later. |
    | <strong>Software Update</strong> | Display the mandatory software update screen. For iOS/iPadOS 12.0 and later. |
    | <strong>SIM Setup</strong> | Give the user the option to add a cellular plan. For iOS/iPadOS 12.0 and later. |
    | <strong>Appearance</strong> | Display the Appearance screen to the user. For macOS 10.14 and later, and iOS/iPadOS 13.0 and later. |
    | <strong>Device to Device Migration</strong> | Give the user the option to migrate data from their old device to this device. For iOS/iPadOS 13.0 and later. |
    | <strong>Registration</strong> | Display the registration screen to the user. For macOS 10.9 and later. |
    | <strong>FileVault</strong> | Display the FileVault 2 encryption screen to the user. For macOS 10.10 and later. |
    | <strong>iCloud diagnostics</strong> | Display the iCloud Analytics screen to the user. For macOS 10.12.4 and later. |
    | <strong>iCloud Storage</strong> | Display the iCloud Documents and Desktop screen to the user. For macOS 10.13.4 and later. |
    

18. Choose **Next** to go to the **Review + Create** page.

19. To save the profile, choose **Create**.

> [!NOTE]
> If you need to re-enroll your Automated Device Enrolled device, you must first [add the serial number of that device as a corporate identifier](corporate-identifiers-add.md). You might need to re-enroll your ADE device if you're troubleshooting an issue, like the device not receiving policy. In this case, you would:
> 1. Retire the device from the Intune console.
> 2. [Add the device's serial number as a corporate device identifier](corporate-identifiers-add.md).
> 3. Re-enroll the device by downloading the Company Portal and going through device enrollment.


### Dynamic groups in Azure Active Directory

You can use the enrollment **Name** field to create a dynamic group in Azure Active Directory. For more information, see [Azure Active Directory dynamic groups](/azure/active-directory/users-groups-roles/groups-dynamic-membership).

You can use the profile name to define the [enrollmentProfileName parameter](/azure/active-directory/users-groups-roles/groups-dynamic-membership#rules-for-devices) to assign devices with this enrollment profile.

For the fastest policy delivery on ADE devices with user affinity, make sure the enrolling user is a member, prior to device setup, of an Azure AD user group. 

Assigning dynamic groups to enrollment profiles can lead to some delay in delivering applications and policies to devices after the enrollment.


## Sync managed devices
Now that Intune has permission to manage your devices, you can synchronize Intune with Apple to see your managed devices in Intune in the Azure portal.

1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **iOS/iPadOS** > **iOS/iPadOS enrollment** > **Enrollment Program Tokens**.

2. Choose a token in the list > **Devices** > **Sync**.

    :::image type="content" source="./media/device-enrollment-program-enroll-ios/image06.png" alt-text="Sync iOS and iPadOS devices to enrollment program token in Microsoft Intune and Endpoint Manager admin center.":::

   To follow Apple's terms for acceptable enrollment program traffic, Intune imposes the following restrictions:
   - A full sync can run no more than once every seven days. During a full sync, Intune fetches the complete updated list of serial numbers assigned to the Apple MDM server connected to Intune. If an ADE device is deleted from the Intune portal, it should be unassigned from the Apple MDM server in the ADE portal. If it's not unassigned, it won't be reimported to Intune until the full sync is run.   
   - A sync is run automatically every 12 hours. You can also sync by clicking the **Sync** button (no more than once every 15 minutes). All sync requests are given 15 minutes to finish. The **Sync** button is disabled until a sync is completed. This sync will refresh existing device status and import new devices assigned to the Apple MDM server.   


## Assign an enrollment profile to devices

Before devices can enroll, you must assign an enrollment program profile to the devices.

>[!NOTE]
>You can also assign serial numbers to profiles from the **Apple Serial Numbers** blade.

1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **iOS/iPadOS** > **iOS/iPadOS enrollment** > **Enrollment Program Tokens** > choose a token in the list.
2. Choose **Devices** > choose devices in the list > **Assign profile**.
3. Under **Assign profile**, choose a profile for the devices > **Assign**.

### Assign a default profile

You can pick a default profile to be applied to all devices enrolling with a specific token.

1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **iOS/iPadOS** > **iOS/iPadOS enrollment** > **Enrollment Program Tokens** > choose a token in the list.
2. Choose **Set Default Profile**, choose a profile in the drop-down list, and then choose **Save**. This profile will be applied to all devices that enroll with the token.

## Distribute devices

You enabled management and syncing between Apple and Intune, and assigned a profile so your ADE devices can enroll. Now, you're ready to distribute devices to users. Some things to know: 

- Devices enrolled with user affinity require each user be assigned an Intune license.
- Devices enrolled without user affinity typically don't have any associated users. So, the devices must have an Intune device license. If devices enrolled without user affinity will be used by an Intune-licensed user, then a device license isn't needed.

  To summarize, if a device has a user, then the user must have an assigned Intune license. If the device doesn't have an Intune-licensed user, then the device must have an Intune device license.

  For more information on Intune licensing, see [Microsoft Intune licensing](../fundamentals/licenses.md) and the [Intune planning guide](../fundamentals/intune-planning-guide.md).

- A device that's been activated must be wiped before it can enroll in Intune. After it's been wiped, the enrollment profile can be applied.

- When enrolling with ADE and user affinity, the following error can happen during setup. To resolve this error, you must factory reset the device. Due to security reasons, this error occurs because of a 15-minute time limit on SCEP certificates.

  `The SCEP server returned an invalid response.`
  
For information on the end user experience, see [Enroll your iOS/iPadOS device in Intune using ADE](../user-help/enroll-your-device-dep-ios.md).

## Renew an Automated Device Enrollment token  

You need to renew your tokens:

- Renew your ADE token yearly. The Endpoint Manager admin center shows the expiration date.
- If the Apple ID password changes for the user who set up the token in Apple Business Manager, then renew your enrollment program token within Intune and Apple Business Manager.
- If the user who set up the token in Apple Business Manager leaves the organization, then renew your enrollment program token within Intune and Apple Business Manager.

### Renew your tokens

1. Go to [business.apple.com](http://business.apple.com) and sign in with an account that has the role of Administrator or Device Enrollment Manager.
2. Choose **Settings** > under **MDM Servers** choose your MDM server associated with the token file that you want to renew > **Download Token**.

    :::image type="content" source="./media/device-enrollment-program-enroll-macos/download-token.png" alt-text="Renew and download the Apple token in Apple Business Manager":::

3. Choose **Download Server Token**.

    > [!NOTE]
    > Do not click **"Download server token"** if you do not intent to renew the token, as mentioned in the prompt, doing so will invalidate the token currently being used by Intune (or any other MDM solution for that matter). If you already downloaded the token, makes sure you continue with the next steps until the token is renewed.

4. After downloading the token, go to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431). Select **Devices** > **iOS/iPadOS** > **iOS/iPadOS enrollment** > **Enrollment Program Tokens** > choose the token.

    :::image type="content" source="./media/device-enrollment-program-enroll-ios/enrollmentprogramtokens.png" alt-text="Select the Apple enrollment program token in Microsoft Intune and Endpoint Manager admin center.":::

5. Choose **Renew token** and enter the Apple ID used to create the original token (if not automatically populated).  

    :::image type="content" source="./media/device-enrollment-program-enroll-ios/renewtoken.png" alt-text="Renew the Apple enrollment program token in Microsoft Intune and Endpoint Manager admin center.":::

6. Upload the newly downloaded token.

7. Select **Next** to go to the **Scope tags** page and assign scope tags if you want.

8. Choose **Renew token**. You'll see the confirmation that the token was renewed.

    :::image type="content" source="./media/device-enrollment-program-enroll-ios/confirmation.png" alt-text="Renew token shows as successful when it completes successfully in Microsoft Intune and Endpoint Manager admin center.":::

## Delete an Automated Device Enrollment token from Intune

You can delete enrollment profile tokens from Intune as long as
- no devices are assigned to the token
- no devices are assigned to the default profile

1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **iOS/macOS** > **iOS/macOS enrollment** > **Enrollment Program Tokens** > choose the token > **Devices**.
2. Delete all the devices assigned to the token.
3. Go to **Devices** > **iOS/macOS** > **iOS/macOS enrollment** > **Enrollment Program Tokens** > choose the token > **Profiles**.
4. If there is a default profile, delete it.
5. Go to **Devices** > **iOS/macOS** > **iOS/macOS enrollment** > **Enrollment Program Tokens** > choose the token > **Delete**.

## Next steps

[Backup and restore scenarios for iOS/iPadOS](backup-restore-ios.md)

[iOS/iPadOS enrollment overview](ios-enroll.md).
