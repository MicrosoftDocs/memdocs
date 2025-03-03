---
# required metadata

title: Use Remote Help on Android to assist users authenticated by your organization. 
description: With the Remote Help app in Android, provide remote assistance to authenticated users who also run the Remote Help app.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 10/19/2023
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:
ms.reviewer: Karawang
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- highseo
---
 
# Remote Help on Android with Microsoft Intune

[!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)]

Remote Help is an add-on application that works with Intune and enables your support staff to remotely connect to a user's device. Remote Help is available on multiple platforms including Android.

During the session, you can view the device's display via screen sharing and if permitted by the device user, take full control to directly make configurations or take actions on the device. Remote Help for Android also supports unattended control allowing you to take full control of the device without needing user interaction on the device. This is helpful in cases like digital signage or for devices that need to be accessed during maintenance windows when no operators are on site.

In this article, we refer to the users who provide help as *helpers*, and devices that receive help as *sharers* as they share their session with the helper.

> [!IMPORTANT]
>
> Remote Help on Android is now generally available.

## Remote Help capabilities and requirements on Android

The Remote Help app supports the following capabilities on Android:

- **Screen sharing**: View of the remote screen. To minimize impact on end user privacy, this option is recommended unless full control is necessary.

- **Full control**: Full control of the remote device.

- **Unattended control**: Full control of the device without the presence of an end user.

- **Compliance warnings**: Before a helper connects to a user's device, the helper sees a non-compliance warning about that device if it's not compliant with its assigned policies. This warning doesn't block access but provides transparency about the risk of using sensitive data like administrative credentials during the session.

## Supported devices

- Samsung devices
- Zebra devices
  - Running MX version 8.3 or higher
  - Unattended control is only supported on MX version 9.3 and higher

- Devices must be either Samsung or Zebra and enrolled with Android Enterprise Dedicated.

## Prerequisites for Remote Help on Android

For general prerequisites, go to [Prerequisites for Remote Help](remote-help.md#prerequisites)

- Set up Managed Google Play for your tenant. For more information, go to [Connect your Intune account to your Managed Google Play account](../enrollment/connect-intune-android-enterprise.md)

- Install the Intune app on devices with a version higher than 5.0.5541.0

- Devices must NOT have device configuration policy set to block Screen capture

- Zebra devices only: Set up Zebra OEMConfig for your tenant. For more details, go to [Use OEMConfig on Android Enterprise devices in Microsoft Intune](../configuration/android-oem-configuration-overview.md)  

- The helper must be licensed to use the Remote Help add-on. For more details on licensing, go to [Use Intune Suite add-on capabilities - Microsoft Intune](../fundamentals/intune-add-ons.md)

- The helper must have appropriate RBAC permissions to use Remote Help on Android:

  - Category: Remote Help app

  - Permissions:

    - Take full control: Yes (required for control)

    - View screen: Yes (required for screen share)

    - Unattended control: Yes (required for unattended control)

    - If the user doesn't have the correct RBAC permissions for a particular mode, the corresponding options are disabled when attempting to start a Remote Help session.

## Setting up Remote Help for Android

To set up Remote Help for Android, you need to complete the following steps:

1. Deploy the Remote Help app.

2. Grant permissions.  

   - Configure camera permissions.

   - Configure permission setup for Zebra devices.

   - Configure permission setup for Samsung devices.

### Deploy Remote Help app

1. Using Managed Google Play, add the [Remote Help app from Microsoft](https://play.google.com/store/apps/details?id=com.microsoft.intune.remotehelp).

2. On devices that you want to use Remote Help, assign the app as **Required**.  This setting allows automatic installation of the app on those devices.

### Grant permissions

To protect user privacy on the device, both the Android OS and device OEMs require certain permissions to be granted to the Remote Help app.

#### Camera

The Remote Help app requires Camera permissions.

> [!NOTE]
> Remote Help does not store camera input. These permissions are only used to initiate a remote help session between the device and the Intune service.  

You can autogrant them through app configuration policy:

1. Go to **Apps** > **Configuration** > **Create** a new policy for **Managed devices**.

2. Create the policy for **Android Enterprise** with type **Fully managed, Dedicated, and Corporate-Owned Work Profile Only**. Target the policy to the **Remote Help** app that you approved earlier.

3. Under **Permissions**, add **CAMERA** permissions. Then, set the permission state to **Auto grant**.

4. Assign the profile to the devices on which you want to use Remote Help.

#### Permission setup for Zebra devices

On Zebra devices, permissions are granted through Zebra OEMConfig profiles.  

For instructions on how to set up OEMConfig, go to [Use OEMConfig on Android Enterprise devices in Microsoft Intune](../configuration/android-oem-configuration-overview.md).

If you're planning to use Remote Help on a device running on Android 11, you need to enable another Zebra package as a system app. For more information on how to enable system apps, see [Manage Android Enterprise system apps in Microsoft Intune](../apps/apps-ae-system.md)

|Build|System app to be enabled|
|--------|------------------------------|
|Any build of Android 11 that is earlier than 11-20-18.00-RG-U00 |com.symbol.tool.stagenow|
|11-20-18.00-RG-U00 or 11-20-18.00-RG-U02|com.zebra.devicemanager|
|Any build of Android 11 that is later than 11-20-18.00-RG-U02 |(None required)|

##### Instructions for Zebra OEMConfig powered by MX

*Zebra OEMConfig Powered by MX* is a new version of the OEMConfig app released in May 2023.

> [!NOTE]
> On Android 11, the new OEM Config schema (Zebra OEMConfig powered by MX) doesn't work if the BSP version is HE_FULL_UPDATE_11-20-18.00-RG-U00-STD-HEL-04. You must upgrade to a later BSP to use the new OEMConfig app. For instructions on updating supported Zebra devices with Intune, see [ Zebra LifeGuard Over-the-Air Integration with Microsoft Intune](../protect/zebra-lifeguard-ota-integration.md)

Use OEMConfig to deploy the following settings on devices that you want to use Remote Help with:

1. Under **Permission Access Configuration**, configure the following details:

  | Key                      | Value                                           |
  |-----------------------------------|-----------------------------------------------|
  | Package Name | com.microsoft.intune.remotehelp  |
  | Package Signing Certificate | ```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``` |

2. For the package you just created, under **Package > Permissions**, add a new permission as follows:
  
  | Key                      | Value                                           |
  |-----------------------------------|-----------------------------------------------|
  | Name| System Alert Window  |
  | State | Grant  |

3. For the package created in step 1, under **Package** > **Allowed Services**, add two allowed services:

- One allowed service with a Service Identifier of `com.zebra.eventinjectionservice`  

- Another allowed service with a Service Identifier of `com.zebra.remotedisplayservice`  


##### Instructions for Legacy Zebra OEMConfig

When using Legacy Zebra OEMConfig, OEMConfig profiles are applied as one-off actions, not persistent policy states. Make sure to deploy the OEMConfig profile after the Remote Help app is installed on the device. Also, if you uninstall and reinstall the Remote Help app on the device, you'll need to re-apply these OEMConfig settings after the app is reinstalled. You can create a new OEMConfig profile and assign it to the device, or edit the previously created OEMConfig profile.

Use OEMConfig to deploy the following settings on devices that you want to use Remote Help:

1. Under Permission Access Configuration, configure the following details:

  | Name                      | Description                                           |
  |-----------------------------------|-----------------------------------------------|
  | Permission Access Action | Grant |
  | Grant Permission Access Action | System Alert Window |
  | Grant Application Package | com.microsoft.intune.remotehelp |
  | Grant Application Signature |```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```|

> [!NOTE]
> The OEMConfig setting requires version MX 10.4 and higher on the device. For devices running a lower MX version, the display overlay permission must be manually granted to the Remote Help app. Contact Zebra for specific steps on your device or refer to the setup instructions for this permission on Samsung devices.

2. In a separate transaction step, under Service Access Configuration, create the following details:
  
  | Name                      | Description                                           |
  |-----------------------------------|-----------------------------------------------|
  | Service Binding Action | Allow |
  | Allow Service Identifier | com.zebra.eventinjectionservice  |
  | Service Caller Action | Allow |
  | Allow Service Identifier | com.zebra.eventinjectionservice |
  | Allow Caller Package | com.microsoft.intune.remotehelp |
  | Allow Caller Signature | ```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```|

3. In another transaction step, under Service Access Configuration, configure the following details:  
  
  | Name                      | Description                                           |
  |-----------------------------------|-----------------------------------------------|
  | Service Binding Action | Allow |
  | Allow Service Identifier | com.zebra.remotedisplayservice |
  | Service Caller Action | Allow |
  | Allow Service Identifier | com.zebra.remotedisplayservice |
  | Allow Caller Package | com.microsoft.intune.remotehelp |
  | Allow Caller Signature | ```MIIGDjCCA/agAwIBAgIEUiDePDANBgkqhkiG9w0BAQsFADCByDELMAkGA1UEBhMCVVMxEzARBgNVBAgTCldhc2hpbmd0b24xEDAOBgNVBAcTB1JlZG1vbmQxHjAcBgNVBAoTFU1pY3Jvc29mdCBDb3Jwb3JhdGlvbjErMCkGA1UECxMiV2luZG93cyBJbnR1bmUgU2lnbmluZyBmb3IgQW5kcm9pZDFFMEMGA1UEAxM8TWljcm9zb2Z0IENvcnBvcmF0aW9uIFRoaXJkIFBhcnR5IE1hcmtldHBsYWNlIChEbyBOb3QgVHJ1c3QpMB4XDTEzMDgzMDE4MDIzNloXDTM2MTAyMTE4MDIzNlowgcgxCzAJBgNVBAYTAlVTMRMwEQYDVQQIEwpXYXNoaW5ndG9uMRAwDgYDVQQHEwdSZWRtb25kMR4wHAYDVQQKExVNaWNyb3NvZnQgQ29ycG9yYXRpb24xKzApBgNVBAsTIldpbmRvd3MgSW50dW5lIFNpZ25pbmcgZm9yIEFuZHJvaWQxRTBDBgNVBAMTPE1pY3Jvc29mdCBDb3Jwb3JhdGlvbiBUaGlyZCBQYXJ0eSBNYXJrZXRwbGFjZSAoRG8gTm90IFRydXN0KTCCAiIwDQYJKoZIhvcNAQEBBQADggIPADCCAgoCggIBAKl5psvH2mb9nmMz1QdQRX3UFJrl4ARRp9Amq4HC1zXFL6oCzhq6ZkuOGFoPPwTSVseBJsw4FSaX21sDWISpx/cjpg7RmJvNwf0IC6BUxDaQMpeo4hBKErKzqgyXa2T9GmVpkSb2TLpL8IpLtkxih8+GB6/09DkXR10Ir+cE+Pdkd/4iV44oKLxTbLprX1Rspcu07p/4JS6jO5vgDVV9OqRLLcAwrlewqua9oTDbAp/mDldztp//Z+8XiY6j/AJCKFvn+cA4s6s5kYj/jsK4/wt9nfo5aD9vRzE2j2IIH1T0Qj6NLTNxB7+Ij6dykE8QHJ7Vd/Y5af9QZwXyyPdSvwqhvKafS0baSqy1gLaNLA/gc/1Sh/ASXaDEhKHHAsLChkVFCE7cPwKPnBHudNBmS6HQ6Zo3UMwYVQVe7u+6jjvfo4gqmZglMhhzhauekNrHV91E+GkY3NGH2cHDEbpbl0JAAdWsI4jtJSN8c9Y8lSX00D7KdQ2NJhYl7mJsS10/3Ex1HYr8nDRq/IlAhGdSVC/qc9RktfYiYcmfZ/Iel5n+KkQt1svrF1TDCHYg/bcC7BhCwlaoa4Nu0hvLHvSbrsnB+gKtovCCilswPwCnDdAYmSMnwsAtBwJXqxD6HXbBCNX4A+qUrR+sYhmFa8jIVzAXa4I3iTvVQkTvrf9YriP7AgMBAAEwDQYJKoZIhvcNAQELBQADggIBAEdMG13+y2OvUHP1lHP22CNXk5e2lVgKZaEEWdxqGFZPuNsXsrHjAMOM4ocmyPUYAlscZsSRcMffMlBqbTyXIDfjkICwuJ+QdD7ySEKuLA1iWFMpwa30PSeZP4H0AlF9RkFhl/J9a9Le+5LdQihicHaTD2DEqCAQvR2RhonBr4vOV2bDnVParhaAEIMzwg2btj4nz8R/S0Nnx1O0YEHoXzbDRYHfL9ZfERp+9I8rtvWhRQRdhh9JNUbSPS6ygFZO67VECfxCOZ1MzPY9YEEdCcpPt5rgMEKVh7VPH14zsBuky2Opf6rGGS1m1Q26edG9dPtnAYax5AIkUG6cI3tW957qmUVSnIvlMzt6+OMYSKf5R5fdPdRlH1l8hak9vMxO2l344HyD0vAmbk01dw44PhIfuoq2qNAIt3lweEhZna8m5s9r1NEaRTf1BrVHXloAM+sipd5vQNs6oezSCicU7vwvUH1hIz0FOiCsLPTyxlfHk3ESS5QsivJS82TLSIb9HLX07OyENRRm8cVZdDbz6rRR+UWn1ZNEM9q56IZ+nCIOCbTjYlw1oZFowJDCL1IH8i7nhKVGBWf7TfukucDzh8ThOgMyyv6rIPutnssxQqQ7ed6iivc1y4Graihrr9n2HODRo3iUCXi+G4kfdmMwp2iwJz+Kjhyuqf7lhdOld6cs```|

> [!NOTE]
> This setting enables unattended access and is only available on Zebra devices running MX 9.3 or later.

#### Permission setup for Samsung devices

In this section:

- Display overlay permission
- Knox KLMS Agent consent

##### Display overlay permission

> [!IMPORTANT]
> If the device is running in kiosk mode, the Settings app (which is where the permission is granted) needs to be designated as a system app so that it can launch. See [Granting overlay permissions to Managed Home Screen for Android Enterprise dedicated devices](https://techcommunity.microsoft.com/t5/intune-customer-success/granting-overlay-permissions-to-managed-home-screen-for-android/ba-p/3247041) for detailed instructions.

The Remote Help app needs the **Display over other apps** or **Appear on top** permission to display the Remote Help session UI. To grant this permission, create an OEMConfig profile that configures the permissions in the OEMConfig app. 

##### Knox KLMS Agent consent

On some devices, the user also needs to agree to Samsung's KLMS Agent terms and conditions before the app can work.

1. After installing the Remote Help app, launch it. The prompt is automatically displayed when the app is launched.

2. Agree to the terms and conditions and tap **Confirm**.  

> [!NOTE]
> - On Knox 2.8-3.7 (inclusive) this consent is revoked if the Remote Help app is uninstalled.
> - In some cases, if the user has already agreed to KLMS license terms earlier (they were requested by another app), then the prompt may not be displayed.  

## Using Remote Help for Android

1. In the admin console, navigate to the device you would like to remotely assist.

2. On the device actions toolbar, select **New remote assistance session** then select the session mode.

3. On the device, the user sees a prompt displaying a request to grant screen share or control of the device.  

    a. If starting an attended screen sharing or full control session, the user must select Accept to allow the session to begin. If the user doesn't accept within 5 minutes, the session times out.  

    b. If starting an unattended control session, the session will begin automatically after **30 seconds**.

4. During the session, the sharer device displays a floating **End Session** button. This button can be repositioned on the screen. Tap the button to end the session from the sharer device.

5. During a control session, use the buttons on the menu bar, keyboard or mouse input to interact with the sharer device. You can also long-press on the Power button in the menu bar to simulate a long press. This can be useful, for example, to open the power options menu on some devices.

6. At the end of the session, select **Leave** to end the session from the admin console.

> [!NOTE]
> On Android 13 devices, the device unlock UI (the PIN entry pad, or the pattern dot grid) cannot be displayed remotely. To unlock the device, you can still use keyboard input to enter a passcode. This is a security measure added by Android, not Remote Help, to protect the end user from a passcode or unlock pattern being captured if the device is unlocked while screen sharing.

## Next steps

[Get support in Microsoft Intune admin center](../../get-support.md)
