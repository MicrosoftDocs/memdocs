---
# required metadata

title: Enroll iOS/iPadOS devices by using ADE
titleSuffix: Microsoft Intune
description: Learn how to enroll corporate-owned iOS/iPadOS devices by using Automated Device Enrollment (ADE), previously known as Device Enrollment Program (DEP).
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/15/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 7ddbf360-0c61-11e8-ba89-0ed5f89f718b

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: annovich
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: seodec18
ms.collection:
  - M365-identity-device-management
  - highpri
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

To enable the Company Portal to update automatically and provide the Company Portal app on devices already enrolled with ADE, deploy the Company Portal app through Intune as a required VPP app with an [application configuration policy](../apps/app-configuration-policies-use-ios.md#configure-the-company-portal-app-to-support-ios-and-ipados-devices-enrolled-with-automated-device-enrollment) applied. Deploy the Company Portal app in this way to enable Device Staging for devices only without user affinity. With Device Staging, a device is fully enrolled and receives device policies before the addition of a user affinity. Device Staging can also be used to transition a device without user affinity, to a device with user affinity.

Specifically for the authentication method Setup Assistant with modern authentication, do not separately deploy the Company Portal app as a client app, with or without an app config targeted to it. ADE devices enrolling with Setup Assistant with modern authentication should be excluded from any separate Company Portal targeting in the tenant. The Company Portal is sent as a required app automatically when Setup Assistant with modern authentication is chosen as the authentication method in the assigned enrollment profile. 

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

3. (Optional.) If you want to apply [scope tags](../fundamentals/scope-tags.md) to this ADE token, click **Select scope tags**, and then select existing scope tags. Scope tags applied to a token are inherited by profiles and ADE enrolled devices added to the token. The devices that are being referred to are the devices that have synced over from ABM/ASM, and are enrolled through Automated Device Enrollment and show up within the specific token. 

    For more information on scope tags, see [Use role-based access control (RBAC) and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

4. On the **Review + create** tab, select **Create**.

With the push certificate, Intune can enroll and manage iOS/iPadOS devices by pushing policies to enrolled mobile devices. Intune automatically synchronizes with Apple to access your enrollment program account.

## Create an Apple enrollment profile

Now that you've installed your token, you can create an enrollment profile for ADE devices. A device enrollment profile defines the settings applied to a group of devices during enrollment. There's a limit of 1,000 enrollment profiles per ADE token.

> [!NOTE]
> Devices will be blocked if there aren't enough Company Portal licenses for a VPP token or if the token is expired. Intune alerts you when a token is about to expire or licenses are running low.

1. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **iOS/iPadOS** > **iOS/iPadOS enrollment** > **Enrollment program tokens**.
2. Select a token, and then select **Profiles**.
3. Select **Create profile** > **iOS/iPadOS**.
4. For **Basics**, give the profile a **Name** and **Description** for administrative purposes. Users don't see these details.
5. Select **Next**.

> [!IMPORTANT]
> If you make changes to existing enrollment profile settings, the new changes will not take effect on assigned devices until devices are reset back to factory settings and reactivated. Reactivation occurs when the Remote Management Payload is received on ADE devices. Renaming the device name template is the only change you can make that doesn't require a factory reset.  

6. In the **User Affinity** list, select an option that determines whether devices with this profile must enroll with or without an assigned user.
    - **Enroll with User Affinity**. Select this option for devices that belong to users who want to use Company Portal for services like installing apps.
    - **Enroll without User Affinity**. Select this option for devices that aren't affiliated with a single user. Use this option for devices that don't access local user data. This option is typically used for kiosk, point of sale (POS), or shared-utility devices.

      In some situations, you might want to associate a primary user on devices enrolled without user affinity. To do this task, you can send the `IntuneUDAUserlessDevice` key to the Company Portal app in an app configuration policy for managed devices. The first user that signs in to the Company Portal app is established as the primary user. If the first user signs out and a second user signs in, the first user remains the primary user of the device. For more information, see [Configure the Company Portal app to support iOS and iPadOS ADE devices](../apps/app-configuration-policies-use-ios.md#configure-the-company-portal-app-to-support-ios-and-ipados-devices-enrolled-with-automated-device-enrollment).

7. If you selected **Enroll with User Affinity** for the **User Affinity** field, you now have the option to choose the authentication method to use when authenticating users. For **Authentication method**, select one of the following options:

   ![Screenshot of authentication method options.](./media/device-enrollment-program-enroll-ios/authentication-method.png)

    - **Company Portal**: Authenticate with the Company Portal app if you want to:
        - Use multifactor authentication.
        - Prompt users to change their passwords when they first sign in.
        - Prompt users to reset their expired passwords during enrollment.

        These features aren't supported when you authenticate by using Apple Setup Assistant.
    - **Setup Assistant (legacy)**: Use the legacy Setup Assistant if you want users to experience the typical, out-of-box-experience for Apple products. This installs standard preconfigured settings when the device enrolls with Intune management. If you're using Active Directory Federation Services and you're using Setup Assistant to authenticate, a [WS-Trust 1.3 Username/Mixed endpoint](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff608241(v=ws.10)) is required. [Learn more](/powershell/module/adfs/get-adfsendpoint?view=win10-ps&preserve-view=true).
    - **Setup Assistant with modern authentication**: Devices running iOS/iPadOS 13.0 and later can use this method. Older iOS/iPadOS devices in this profile will fall back to using the **Setup Assistant (legacy)** process.  

        > [!NOTE]
        > MFA won't work for Setup Assistant with modern authentication if you're using a 3rd party MFA provider to present the MFA screen during enrollment. Only the Azure AD MFA screen works during enrollment. For the latest support updates about custom controls for MFA, see [Upcoming changes to Custom Controls](https://techcommunity.microsoft.com/t5/azure-active-directory-identity/upcoming-changes-to-custom-controls/ba-p/1144696).  

        This method provides the same security as Company Portal authentication but avoids the issue of leaving end users with a device they can't use until the Company Portal installs.  

        The Company Portal will be installed without user interaction (the user won't see the **Install Company Portal** option) in both of the following situations:

        - If you use the **Install Company Portal with VPP** option below (recommended).
        - If the end user sets up their Apple ID account during Setup Assistant.

        In both of these situations, the Company Portal will be a required app on the device. Also, when the end user gets to the home screen, the correct app configuration policy will automatically be applied to the device.

        Don't send a separate app configuration policy to the Company Portal for iOS/iPadOS devices after enrolling with Setup Assistant with modern authentication. Doing so will result in an error.

        If you don't use the VPP option, the user must supply an Apple ID to install the Company Portal (either during Setup Assistant or when Intune tries to install the Company Portal).

        If a conditional access policy that requires [multi-factor authentication (MFA) applies](multi-factor-authentication.md) at enrollment or during Company Portal sign in, then MFA is required. However, MFA is optional based on the AAD settings in the targeted Conditional Access policy.

        After completing all the Setup Assistant screens, the end user lands on the home page (at which point their user affinity is established). However, until the user signs in to the Company Portal using their Azure AD credentials and taps "Begin" at the "Setup *Company* access" screen, the device:

        - Won’t be fully registered with Azure AD.
        - Won’t show up in the user’s device list in the Azure AD portal.
        - Won’t have access to resources protected by conditional access.
        - Won’t be evaluated for device compliance.
        - Will be redirected to the Company Portal from other apps if the user tries to open any managed applications that are protected by conditional access.


8. If you selected **Setup Assistant (legacy)** for the authentication method but you also want to use Conditional Access or deploy company apps on the devices, you need to install Company Portal on the devices and sign in to complete the Azure AD registration. To do so, select **Yes** for **Install Company Portal**. If you want users to receive Company Portal without having to authenticate in to the App Store, in **Install Company Portal with VPP**, select a VPP token. Make sure the token doesn't expire and that you have enough device licenses for the Company Portal app to deploy correctly.

9. If you select a token for **Install Company Portal with VPP**, you can lock the device in Single App Mode (specifically, the Company Portal app) right after the Setup Assistant completes. Select **Yes** for **Run Company Portal in Single App Mode until authentication** to set this option. To use the device, the user must first authenticate by signing in with Company Portal.

    > [!NOTE]
    > Multifactor authentication isn't supported on a single device locked in Single App Mode. This limitation exists because the device can't switch to a different app to complete the second factor of authentication. If you want multifactor authentication on a Single App Mode device, the second factor must be on a different device.

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

12. If you selected **Enroll without User Affinity** and **Supervised** in the previous steps, you need to decide whether to configure the devices to be [Apple Shared iPad for Business devices](https://support.apple.com/guide/mdm/shared-ipad-overview-cad7e2e0cf56/web). Select **Yes** for **Shared iPad** to enable multiple users to sign in to a single device. Users will authenticate by using their Managed Apple IDs and federated authentication accounts or by using a temporary session (like the Guest account). This option requires iOS/iPadOS 13.4 or later. With Shared iPad, all Setup Assistant panes after activation are automatically skipped. 


    > [!NOTE]
    >- A device wipe will be required if an iOS/iPadOS enrollment profile with Shared iPad enabled is sent to an unsupported device. Unsupported devices include any iPhone models, and iPads running iPadOS/iOS 13.3 and earlier. Supported devices include iPads running iPadOS 13.3 and later.  
    >- To set up Apple Shared iPad for Business, configure these settings:
    >   - In the **User Affinity** list, select **Enroll without User Affinity**.
    >   - In the **Supervised** list, select **Yes**.
    >   - In the **Shared iPad** list, select **Yes**.

    If you're setting up Apple Shared iPad for Business devices, also configure:  

    * **Maximum cached users**: Enter the number of users that you expect to use the shared iPad. You can cache up to 24 users on a 32-GB or 64-GB device. If you choose a low number, it might take a while for your users' data to appear on their devices after they sign in. If you choose a high number, your users could run out of disk space.  

    * **Maximum seconds after screen lock before password is required**: Enter the number of seconds from 0 to 14,400. If the screen lock exceeds this amount of time, a device password will be required to unlock the device. Available for devices in Shared iPad mode running iPadOS 13.0 and later.  

    * **Maximum seconds of inactivity until user session logs out**: The minimum allowed value for this setting is 30. If there isn't any activity after the defined period, the user session ends and signs the user out. If you leave the entry blank or set it to zero (0), the session will not end due to inactivity. Available for devices in Shared iPad mode running iPadOS 14.5 and later.  

    * **Require Shared iPad temporary session only**: Configures the device so that users only see the guest version of the sign-in experience and must sign in as guests. They can't sign in with a Managed Apple ID. Available for devices in Shared iPad mode running iPadOS 14.5 and later.  
    
        When set to **Yes**, this setting cancels out the following shared iPad settings, because they are not applicable in temporary sessions:  

        - Maximum cached users
        - Maximum seconds after screen lock before password is required 
        - Maximum seconds of inactivity until user session logs out 

    * **Maximum seconds of inactivity until temporary session logs out**: The minimum allowed value for this setting is 30. If there isn't any activity after the defined period, the temporary session ends and signs the user out. If you leave the entry blank or set it to zero (0), the session will not end due to inactivity. Available for devices in Shared iPad mode running iPadOS 14.5 and later.  

        This setting is available when **Require Shared iPad temporary session only** is set to **Yes**.  


    > [!NOTE] 
    >- If temporary sessions are enabled, all of the user's data is deleted when they sign out of the session. This means that all targeted policies and apps will come down to the user when they sign-in, and they'll be erased when the user sign outs.  
    >-  To alter a Shared iPads configuration to not have temporary sessions, the device will need to be fully reset and a new enrollment profile with the updated configurations will need to be sent down to the iPad. 
         

13. In the **Sync with computers** list, select an option for the devices that use this profile. If you select **Allow Apple Configurator by certificate**, you need to choose a certificate under **Apple Configurator Certificates**.

     > [!NOTE]
     > If you set **Sync with computers** to **Deny all**, the port will be limited on iOS and iPadOS devices. The port will be limited to only charging. It will be blocked from using iTunes or Apple Configurator 2.
    >
    >If you set **Sync with computers** to **Allow Apple Configurator by certificate**, make sure you have a local copy of the certificate that you can use later. You won't be able to make changes to the uploaded copy, and it's important to retain an copy of this certificate. If you want to connect to the iOS/iPadOS device from a macOS device or PC, the same certificate must be installed on the device making the connection to the iOS/iPadOS device.

14. If you selected **Allow Apple Configurator by certificate** in the previous step, choose an Apple Configurator certificate to import.

15. You can specify a naming format for devices that's automatically applied when they're enrolled and upon each successive check-in. To create a naming template, select **Yes** under **Apply device name template**. Then, in the **Device Name Template** box, enter the template to use for the names that use this profile. You can specify a template format that includes the device type and serial number. This feature supports iPhone, iPad, and iPod Touch. The device name template entry cannot exceed the length of 63 characters, including the variables.

16. You can activate a cellular data plan. This setting applies to devices running iOS/iPadOS 13.0 and later. Configuring this option will send a command to activate cellular data plans for your eSim-enabled cellular devices. Your carrier must provision activations for your devices before you can activate data plans using this command. To activate cellular data plan, click **Yes** and then enter your carrier’s activation server URL.

17. Select **Next**.

18. On the **Setup Assistant** tab, configure the following profile settings:

    | Department setting | Description |
    |---|---|
    | **Department** | Appears when users tap **About Configuration** during activation. |
    |    **Department Phone**     | Appears when users tap the **Need Help** button during activation. |

    You can choose to hide Setup Assistant screens on the device during user setup.
    - If you select **Hide**, the screen won't be displayed during setup. After setting up the device, the user can still go to the **Settings** menu to set up the feature.
    - If you select **Show**, the screen will be displayed during setup, but only if there are steps to complete after the restore or after the software update. Users can sometimes skip the screen without taking action. They can then later go to the device's **Settings** menu to set up the feature.
    - With Shared iPad, all Setup Assistant panes after activation are automatically skipped regardless of the configuration. 

    | Setup Assistant features | What happens when visible |
    |------------------------------------------|------------------------------------------|
    | **Passcode** | Prompt the user for a passcode. Always require a passcode for unsecured devices unless access is controlled in some other way. (For example, a kiosk mode configuration that restricts the device to one app.) For iOS/iPadOS 7.0 and later. |
    | **Location Services** | Prompt the user for their location. For macOS 10.11 and later, and iOS/iPadOS 7.0 and later. |
    | **Restore** | Display the Apps & Data screen. This screen gives users the option to restore or transfer data from iCloud Backup when they set up the device. For macOS 10.9 and later, and iOS/iPadOS 7.0 and later. |
    | **Apple ID** | Give the user the options to sign in with their Apple ID and use iCloud. For macOS 10.9 and later, and iOS/iPadOS 7.0 and later.   |
    | **Terms and conditions** | Require the user to accept Apple's terms and conditions. For macOS 10.9 and later, and iOS/iPadOS 7.0 and later. |
    | **Touch ID and Face ID** | Give the user the option to set up fingerprint or facial identification on their device. For macOS 10.12.4 and later, and iOS/iPadOS 8.1 and later. On iOS/iPadOS 14.5 and later, the Passcode and Touch ID Setup Assistant screens during device setup aren’t working. If you use version 14.5+, then don't configure the Passcode or Touch ID Setup Assistant screens. If you require a passcode on devices, then use a device configuration policy or a compliance policy. After the user enrolls and they receive the policy, they're prompted for a passcode. |
    | **Apple Pay** | Give the user the option to set up Apple Pay on the device. For macOS 10.12.4 and later, and iOS/iPadOS 7.0 and later. |
    | **Zoom** | Give the user to the option to zoom the display when they set up the device. For iOS/iPadOS 8.3 and later. |
    | **Siri** | Give the user the option to set up Siri. For macOS 10.12 and later, and iOS/iPadOS 7.0 and later. |
    | **Diagnostics Data** | Display the Diagnostics screen. This screen gives the user the option to send diagnostic data to Apple. For macOS 10.9 and later, and iOS/iPadOS 7.0 and later. |  
    | **Display Tone** | Give the user the option to turn on Display Tone. For macOS 10.13.6 and later, and iOS/iPadOS 9.3.2 and later. |  
    | **Privacy** | Display the Privacy screen. For macOS 10.13.4 and later, and iOS/iPadOS 11.3 and later. |  
    | **Android Migration** | Give the user the option to migrate data from an Android device. For iOS/iPadOS 9.0 and later.|
    | **iMessage & FaceTime** | Give the user the option to set up iMessage and FaceTime. For iOS/iPadOS 9.0 and later. |  
    | **Onboarding** | Display onboarding informational screens for user education, like Cover Sheet and Multitasking and Control Center. For iOS/iPadOS 11.0 and later. |  
    | **Screen Time** | Display the Screen Time screen. For macOS 10.15 and later, and iOS/iPadOS 12.0 and later. |  
    | **SIM Setup** | Give the user the option to add a cellular plan. For iOS/iPadOS 12.0 and later. |
    | **Software Update** | Display the mandatory software update screen. For iOS/iPadOS 12.0 and later. |  
    | **Watch Migration** | Give the user the option to migrate data from a watch device. For iOS/iPadOS 11.0 and later.|
    | **Appearance** | Display the Appearance screen. For macOS 10.14 and later, and iOS/iPadOS 13.0 and later. |  
    | **Device to Device Migration** | Give the user the option to migrate data from an old device to this device. For iOS/iPadOS 13.0 and later. |
    | **Restore Completed** | Shows users the Restore Completed screen after a backup and restore is performed during Setup Assistant. |  
    | **Software Update Completed** | Shows the user all software updates that happen during Setup Assistant.|  
    | **Get Started**| Shows users the Get Started welcome screen.  

19. Select **Next**.

20. To save the profile, select **Create**.

> [!NOTE]
> If you need to re-enroll your Automated Device Enrollment device, you need to first wipe the device from the Intune admin console. To re-enroll:
> 1. Wipe the device from the Intune console.
>     - Alternatively, retire the device from the Intune console and factory reset the device using the Settings app, Apple Configurator 2, or iTunes.
> 2. Activate the device again and run through Setup Assistant to receive the *Remote Management Profile*.

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

   - A full sync can run no more than once every seven days. During a full sync, Intune fetches the complete updated list of serial numbers assigned to the Apple MDM server connected to Intune.  
      > [!IMPORTANT]
      > If a device is deleted from Intune, but remains assigned to the ADE enrollment token in the ASM/ABM portal, it will reappear in Intune on the next full sync. If you don't want the device to reappear in Intune, unassign it from the Apple MDM server in the ABM/ASM portal.   
   - If a device is released from ABM/ASM, it can take up to 45 days for it to be automatically deleted from the devices page in Intune. You can manually delete released devices from Intune one by one if needed. Released devices will be accurately reported as being Removed from ABM/ASM in Intune until they are automatically deleted within 30-45 days.
   - A delta sync is run automatically every 12 hours. You can also trigger a delta sync by selecting the **Sync** button (no more than once every 15 minutes). All sync requests are given 15 minutes to finish. The **Sync** button is disabled until a sync is completed. This sync will refresh existing device status and import new devices assigned to the Apple MDM server. If a delta sync fails for any reason, the next sync will be a full sync to hopefully resolve any issues. 

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

> [!NOTE]
> Ensure that **Device Type Restrictions** under **Enrollment Restrictions** does not have the default **All Users** policy set to block the iOS/iPadOS platform. This setting will cause automated enrollment to fail and your device will show as Invalid Profile, regardless of user attestation. To permit enrollment only by company-managed devices, block only personally owned devices, which will permit corporate devices to enroll. Microsoft defines a corporate device as a device that's enrolled via a Device Enrollment Program or a device that's manually entered under **Corporate device identifiers**.
  
## Distribute devices

You enabled management and syncing between Apple and Intune and assigned a profile so your ADE devices can be enrolled. You're now ready to distribute devices to users. Some things to know:

- Devices enrolled with user affinity require that each user be assigned an Intune license.
- Devices enrolled without user affinity typically don't have any associated users. These devices need to have an Intune device license. If devices enrolled without user affinity will be used by an Intune-licensed user, a device license isn't needed.

  To summarize, if a device has a user, the user needs to have an assigned Intune license. If the device doesn't have an Intune-licensed user, the device needs to have an Intune device license.

  For more information on Intune licensing, see [Microsoft Intune licensing](../fundamentals/licenses.md) and the [Intune planning guide](../fundamentals/intune-planning-guide.md).

- A device that's been activated needs to be wiped before it can enroll properly using ADE in Intune. After it's been wiped but before activating it again, you can apply the enrollment profile. See [Set up an existing iPhone, iPad, or iPod touch](https://support.apple.com/en-us/HT207516)

- If you're enrolling with ADE and user affinity, the following error can happen during setup:

  `The SCEP server returned an invalid response.`

   You can resolve this error by trying to download the management again within 15 minutes. If it's been more than 15 minutes, to resolve this error you'll need to factory reset the device. This error occurs because of a 15-minute time limit on SCEP certificates, which is enforced for security.
  
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
- There are no enrollment profiles under that token. 

To delete an enrollment profile token:

1. In [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **iOS/macOS** > **iOS/macOS enrollment** > **Enrollment Program Tokens**. Select the token, and then select **Devices**.
2. Delete all the devices assigned to the token.
3. Go to **Devices** > **iOS/macOS** > **iOS/macOS enrollment** > **Enrollment Program Tokens**. Select the token, and then select **Profiles**.
4. If there's a default profile or any other enrollment profile, they must all be deleted. 
5. Go to **Devices** > **iOS/macOS** > **iOS/macOS enrollment** > **Enrollment Program Tokens**. Select the token, and then select **Delete**.

## Next steps

[Backup and restore scenarios for iOS/iPadOS](backup-restore-ios.md)

[iOS/iPadOS enrollment overview](ios-enroll.md)
