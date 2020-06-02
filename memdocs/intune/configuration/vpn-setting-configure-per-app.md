---
# required metadata

title: Set up per-app VPN for iOS/iPadOS devices in Microsoft Intune - Azure | Microsoft Docs
description: See the prerequisites, create a group for the virtual private network (VPN) users, add a SCEP certificate profile, configure a per-app VPN profile, and assign some apps to the VPN profile in Microsoft Intune on iOS/iPadOS devices. Also lists the steps to verify the VPN connection on the device.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/13/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: high
ms.technology:
ms.assetid: D9958CBF-34BF-41C2-A86C-28F832F87C94

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: tycast
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Set up per-app Virtual Private Network (VPN) for iOS/iPadOS devices in Intune

In Microsoft Intune, you can create and use Virtual Private Networks (VPNs) assigned to an app. This feature is called "per-app VPN". You choose the managed apps that can use your VPN on devices managed by Intune. When using a per-app VPNs, end users automatically connect through the VPN, and get access to organizational resources, such as documents.

This feature applies to:

- iOS 9 and newer
- iPadOS 13.0 and newer

Check your VPN provider's documentation to see if your VPN supports per-app VPN.

This article shows you how to create a per-app VPN profile, and assign this profile to your apps. Use these steps to create a seamless per-app VPN experience for your end users. For most VPNs that support per-app VPN, the user opens an app, and automatically connects to the VPN.

Some VPNs allow username and password authentication with per-app VPN. Meaning, users need to enter a username and password to connect to the VPN.

> [!IMPORTANT]
> Per-app VPN is not supported for IKEv2 VPN profiles for iOS/iPadOS.

## Per-app VPN with Zscaler

Zscaler Private Access (ZPA) integrates with Azure Active Directory (Azure AD) for authentication. When using ZPA, you don't need the [trusted certificate](#create-a-trusted-certificate-profile) or [SCEP or PKCS certificate](#create-a-scep-or-pkcs-certificate-profile) profiles (described in this article). If you have a per-app VPN profile set up for Zscaler, opening one of the associated apps doesn't automatically connect to ZPA. Instead, the user needs to sign into the Zscaler app first. Then, remote access is limited to the associated apps.

## Prerequisites for per-app VPN

> [!IMPORTANT]
> Your VPN vendor may have other requirements for per-app VPN, such as specific hardware or licensing. Be sure to check with their documentation, and meet those prerequisites before setting up per-app VPN in Intune.

To prove its identity, the VPN server presents the certificate that must be accepted without a prompt by the device. To confirm the automatic approval of the certificate, create a trusted certificate profile that includes the VPN server's root certificate issued by the Certification Authority (CA).

### Export the certificate and add the CA

1. On your VPN server, open the administration console.
2. Confirm that your VPN server uses certificate-based authentication. 
3. Export the trusted root certificate file. It has a .cer extension, and you add it when creating a trusted certificate profile.
4. Add the name of the CA that issued the certificate for authentication to the VPN server.

    If the CA presented by the device matches a CA in the Trusted CA list on the VPN server, then the VPN server successfully authenticates the device.

## Create a group for your VPN users

Create or choose an existing group in Azure Active Directory (Azure AD) for the users or devices that use per-app VPN. To create a new group, see [Add groups to organize users and devices](../fundamentals/groups-add.md).

## Create a trusted certificate profile

Import the VPN server's root certificate issued by the CA into a profile created in Intune. The trusted certificate profile instructs the iOS/iPadOS device to automatically trust the CA that the VPN server presents.

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Platform**: Select **iOS/iPadOS**.
    - **Profile**: Select **Trusted certificate**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the profile. Name your profiles so you can easily identify them later. For example, a good profile name is **iOS/iPadOS trusted certificate VPN profile for entire company**.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

6. Select **Next**.
7. In **Configuration settings**, select the folder icon, and browse to your VPN certificate (.cer file) that you exported from your VPN administration console.
8. Select **Next**, and continue creating your profile. For more information, see [Create a VPN profile](vpn-settings-configure.md#create-the-profile).

    > [!div class="mx-imgBorder"]
    > ![Create a trusted certificate profile for iOS/iPadOS devices in Microsoft Intune](./media/vpn-setting-configure-per-app/vpn-per-app-create-trusted-cert.png)

## Create a SCEP or PKCS certificate profile

The trusted root certificate profile allows the device to automatically trust the VPN Server. The SCEP or PKCS certificate provides credentials from the iOS/iPadOS VPN client to the VPN server. The certificate allows the device to silently authenticate without prompting for a username and password. 

To configure and assign the client authentication certificate, see one of the following articles:

- [Configure infrastructure to support SCEP with Intune](../protect/certificates-scep-configure.md)
- [Configure and manage PKCS certificates with Intune](../protect/certficates-pfx-configure.md)

Be sure to configure the certificate for client authentication. You can set client authentication directly in SCEP certificate profiles (**Extended key usage** list > **Client authentication**). For PKCS, set client authentication in the certificate template in the certificate authority (CA).

> [!div class="mx-imgBorder"]
> ![Create a SCEP certificate profile in Microsoft Intune, including subject name format, key usage, extended key usage, and more](./media/vpn-setting-configure-per-app/vpn-per-app-create-scep-cert.png)

## Create a per-app VPN profile

The VPN profile includes the SCEP or PKCS certificate that has the client credentials, the VPN connection information, and the per-app VPN flag that enables the per-app VPN used by the iOS/iPadOS application.

1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Configuration profiles** > **Create profile**.
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Platform**: Select **iOS/iPadOS**.
    - **Profile**: Select **VPN**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the custom profile. Name your profiles so you can easily identify them later. For example, a good profile name is **iOS/iPadOS per-app VPN profile for entire company**.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

6. In **Configuration settings**, configure the following settings:

    - **Connection type**: Select your VPN client app.
    - **Base VPN**: Configure your settings. [iOS/iPadOS VPN settings](vpn-settings-ios.md) lists and describes all the settings. When using per-app VPN, be sure you set the following properties as listed:

      - **Authentication method**: Select **Certificates**. 
      - **Authentication certificate**: Select an existing SCEP or PKCS certificate > **OK**.
      - **Split tunneling**: Select **Disable** to force all traffic to use the VPN tunnel when the VPN connection is active. 

      > [!div class="mx-imgBorder"]
      > ![In a per-app VPN profile, enter a connection, IP address or FQDN, authentication method, and split tunneling in Microsoft Intune](./media/vpn-setting-configure-per-app/vpn-per-app-create-vpn-profile.png)

    For information on the other settings, see [iOS/iPadOS VPN settings](vpn-settings-ios.md).

    - **Automatic VPN** > **Type of automatic VPN** > **Per-app VPN**

      > [!div class="mx-imgBorder"]
      > ![In Intune, set Automatic VPN to per-app VPN on iOS/iPadOS devices](./media/vpn-setting-configure-per-app/vpn-per-app-automatic.png)

7. Select **Next**, and continue creating your profile. For more information, see [Create a VPN profile](vpn-settings-configure.md#create-the-profile).

## Associate an app with the VPN profile

After adding your VPN profile, associate the app and Azure AD group to the profile.

1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **All apps**.
2. Select an app from the list > **Properties** > **Assignments** > **Add group**.
3. In **Assignment type**, select **Required** or **Available for enrolled devices**.
4. Select **Included groups** > **Select groups to include** > Select the group [you created](#create-a-group-for-your-vpn-users) (in this article) > **Select**.
5. In **VPNs**, select the per-app VPN profile [you created](#create-a-per-app-vpn-profile) (in this article).

    > [!div class="mx-imgBorder"]
    > ![Assign an app to the per-app VPN profile in Microsoft Intune](./media/vpn-setting-configure-per-app/vpn-per-app-app-to-vpn.png)

6. Select **OK** > **Save**.

An association between an app and a profile is removed during the next device check-in, when all of the following conditions exist:

- The app was targeted with required install intent.
- Both the profile and the app are targeted to the same group.
- You remove the per-app VPN configuration from the app assignment.

An association between an app and a profile persists until the user requests a reinstall from Company Portal, when all of the following conditions exist:

- The app was targeted with available install intent.
- Both the profile and the app are targeted to the same group.
- The end user requested app install from Company Portal, which results in app and profile being installed on the device.
- You remove or change the per-app VPN configuration from the app assignment.

## Verify the connection on the iOS/iPadOS device

With your per-app VPN set-up and associated with your app, verify the connection works from a device.

### Before you attempt to connect

- Make sure you deploy all of the above mentioned policies to the same group. Otherwise, the per-app VPN experience won't work.
- If you're using the Pulse Secure VPN app or a custom VPN client app, you can choose to use app-layer or packet-layer tunneling. Set the **ProviderType** value to **app-proxy** for app-layer tunneling, or **packet-tunnel** for packet-layer tunneling. Check your VPN provider's documentation to make sure you're using the right value.

### Connect using the per-app VPN

Verify the zero-touch experience by connecting without having to select the VPN or type your credentials. The zero-touch experience means:

- The device doesn't ask you to trust the VPN server. That is, the user doesn't see the **Dynamic Trust** dialog box.
- The user doesn't have to type credentials.
- The user's device is connected to the VPN when the user opens one of the associated apps.

## Next steps

- To review iOS/iPadOS settings, see [VPN settings for iOS/iPadOS devices in Microsoft Intune](vpn-settings-ios.md).
- To learn more about VPN setting and Intune, see [configure VPN settings in Microsoft Intune](vpn-settings-configure.md).
