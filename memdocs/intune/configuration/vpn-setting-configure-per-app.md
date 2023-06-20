---
# required metadata

title: Set up per-app VPN for iOS/iPadOS devices in Microsoft Intune
description: See the prerequisites, create a group for the virtual private network (VPN) users, add a SCEP certificate profile, configure a per-app VPN profile, and assign some apps to the VPN profile in Microsoft Intune on iOS/iPadOS devices. Also lists the steps to verify the VPN connection on the device.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 05/17/2023
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
ms.collection:
- tier2
- M365-identity-device-management
---

# Set up per-app Virtual Private Network (VPN) for iOS/iPadOS devices in Intune

In Microsoft Intune, you can create and use Virtual Private Networks (VPNs) assigned to an app. This feature is called "per-app VPN". You choose the managed apps that can use your VPN on devices managed by Intune. When you use per-app VPNs, end users automatically connect through the VPN, and get access to organizational resources, such as documents.

This feature applies to:

- iOS 9 and newer
- iPadOS 13.0 and newer

Check your VPN provider's documentation to see if your VPN supports per-app VPN.

This article shows you how to create a per-app VPN profile, and assign this profile to your apps. Use these steps to create a seamless per-app VPN experience for your end users. For most VPNs that support per-app VPN, the user opens an app, and automatically connects to the VPN.

Some VPNs allow username and password authentication with per-app VPN. Meaning, users need to enter a username and password to connect to the VPN.

> [!IMPORTANT]
> 
> - There's a known issue in iOS/iPadOS 13. The issue prevents per-app VPN profiles from connecting in user enrollment environments that use certificate-based authentication. Apple plans to fix this in a future release of iOS.
> - On iOS/iPadOS, per-app VPN isn't supported for IKEv2 VPN profiles.

## Per-app VPN with Microsoft Tunnel or Zscaler

Microsoft Tunnel and Zscaler Private Access (ZPA) integrate with Azure Active Directory (Azure AD) for authentication. When using Tunnel or ZPA, you don't need the [trusted certificate](#create-a-trusted-certificate-profile) or [SCEP or PKCS certificate](#create-a-scep-or-pkcs-certificate-profile) profiles (described in this article).

If you have a per-app VPN profile set up for Zscaler, then opening one of the associated apps doesn't automatically connect to ZPA. Instead, the user needs to sign into the Zscaler app. Then, remote access is limited to the associated apps.

## Prerequisites for per-app VPN

> [!IMPORTANT]
> Your VPN vendor may have other requirements for per-app VPN, such as specific hardware or licensing. Be sure to check with their documentation, and meet those prerequisites before setting up per-app VPN in Intune.

To prove its identity, the VPN server presents the certificate that must be accepted without a prompt by the device. To confirm the automatic approval of the certificate, create a trusted certificate profile. This trusted certificate profile must include the VPN server's root certificate issued by the Certification Authority (CA).

### Export the certificate and add the CA

1. On your VPN server, open the administration console.
2. Confirm that your VPN server uses certificate-based authentication.
3. Export the trusted root certificate file. It has a `.cer` extension, and you add it when creating a trusted certificate profile.
4. Add the name of the CA that issued the certificate for authentication to the VPN server.

    If the CA presented by the device matches a CA in the Trusted CA list on the VPN server, then the VPN server successfully authenticates the device.

## Create a group for your VPN users

Create or choose an existing group in Azure Active Directory (Azure AD). This group must include the users or devices that will use per-app VPN. For the steps to create a new group, go to [Add groups to organize users and devices](../fundamentals/groups-add.md).

## Create a trusted certificate profile

Import the VPN server's root certificate issued by the CA into a profile created in Intune. The trusted certificate profile instructs the iOS/iPadOS device to automatically trust the CA that the VPN server presents.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Platform**: Select **iOS/iPadOS**.
    - **Profile**: Select **Trusted certificate**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the profile. Name your profiles so you can easily identify them later. For example, a good profile name is **iOS/iPadOS trusted certificate VPN profile for entire company**.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

6. Select **Next**.
7. In **Configuration settings**, select the folder icon, and browse to your VPN certificate (`.cer` file) that you exported from your VPN administration console.
8. Select **Next**, and continue creating your profile. For more information, go to [Create a VPN profile](vpn-settings-configure.md#step-2---create-the-profile).

    :::image type="content" source="./media/vpn-setting-configure-per-app/vpn-per-app-create-trusted-cert.png" alt-text="Create a trusted certificate profile for iOS/iPadOS devices in Microsoft Intune and Intune admin center.":::

## Create a SCEP or PKCS certificate profile

The trusted root certificate profile allows the device to automatically trust the VPN Server. The SCEP or PKCS certificate provides credentials from the iOS/iPadOS VPN client to the VPN server. The certificate allows the device to silently authenticate without prompting for a username and password.

To configure and assign the client authentication certificate, go to one of the following articles:

- [Configure infrastructure to support SCEP with Intune](../protect/certificates-scep-configure.md)
- [Configure and manage PKCS certificates with Intune](../protect/certificates-pfx-configure.md)

Be sure to configure the certificate for client authentication. You can set client authentication directly in SCEP certificate profiles (**Extended key usage** list > **Client authentication**). For PKCS, set client authentication in the certificate template in the certificate authority (CA).

:::image type="content" source="./media/vpn-setting-configure-per-app/vpn-per-app-create-scep-cert.png" alt-text="Create a SCEP certificate profile in Microsoft Intune and Intune admin center. Include the subject name format, key usage, extended key usage, and more.":::

## Create a per-app VPN profile

This VPN profile includes the SCEP or PKCS certificate that has the client credentials, the VPN connection information, and the per-app VPN flag that enables the per-app VPN used by the iOS/iPadOS application.

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Configuration profiles** > **Create profile**.
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Platform**: Select **iOS/iPadOS**.
    - **Profile**: Select **VPN**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the custom profile. Name your profiles so you can easily identify them later. For example, a good profile name is **iOS/iPadOS per-app VPN profile for myApp**.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.

6. In **Configuration settings**, configure the following settings:

    - **Connection type**: Select your VPN client app.
    - **Base VPN**: Configure your settings. [iOS/iPadOS VPN settings](vpn-settings-ios.md) describes all the settings. When using per-app VPN, be sure you configure the following properties as listed:

      - **Authentication method**: Select **Certificates**. 
      - **Authentication certificate**: Select an existing SCEP or PKCS certificate > **OK**.
      - **Split tunneling**: Select **Disable** to force all traffic to use the VPN tunnel when the VPN connection is active. 

      :::image type="content" source="./media/vpn-setting-configure-per-app/vpn-per-app-create-vpn-profile.png" alt-text="Screenshot that shows a per-app VPN profile, IP address or FQDN, authentication method, and split tunneling in Microsoft Intune and Intune admin center.":::

      For information on the other settings, go to [iOS/iPadOS VPN settings](vpn-settings-ios.md).

    - **Automatic VPN** > **Type of automatic VPN** > **Per-app VPN**

      :::image type="content" source="./media/vpn-setting-configure-per-app/vpn-per-app-automatic.png" alt-text="Screenshot that shows the Automatic VPN set to per-app VPN on iOS/iPadOS devices in Microsoft Intune.":::

7. Select **Next**, and continue creating your profile. For more information, go to [Create a VPN profile](vpn-settings-configure.md#step-2---create-the-profile).

## Associate an app with the VPN profile

After adding your VPN profile, associate the app and Azure AD group to the profile.

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **All apps**.
2. Select an app from the list > **Properties** > **Assignments** > **Edit**.
3. Go to the **Required** or **Available for enrolled devices** section.
4. Select **Add group** > Select the group [you created](#create-a-group-for-your-vpn-users) (in this article) > **Select**.
5. In **VPNs**, select the per-app VPN profile [you created](#create-a-per-app-vpn-profile) (in this article).

    :::image type="content" source="./media/vpn-setting-configure-per-app/vpn-per-app-app-to-vpn.png" alt-text="Two screenshots that show assigning an app to the per-app VPN profile in Microsoft Intune and Intune admin center.":::

6. Select **OK** > **Save**.

When all of the following conditions exist, an association between an app and a profile is removed during the next device check-in:

- The app was targeted with **required** install intent.
- The profile and the app are assigned to the same group.
- You remove the per-app VPN configuration from the app assignment.

When all of the following conditions exist, an association between an app and a profile remains until the user requests a reinstall from the Company Portal app:

- The app was targeted with **available** install intent.
- The profile and the app are assigned to the same group.
- The end user requested the app install in the Company Portal app. This request results in the app and profile being installed on the device.
- You remove or change the per-app VPN configuration from the app assignment.

## Verify the connection on the iOS/iPadOS device

With your per-app VPN set-up and associated with your app, verify the connection works from a device.

### Before you attempt to connect

- Make sure you deploy all the policies described in this article to the same group. Otherwise, the per-app VPN experience won't work.
- If you're using the Pulse Secure VPN app or a custom VPN client app, then you can choose to use app-layer or packet-layer tunneling. For app-layer tunneling, set the **ProviderType** value to **app-proxy**. For packet-layer tunneling, set **ProviderType** value to **packet-tunnel**. Check your VPN provider's documentation to make sure you're using the correct value.

### Connect using the per-app VPN

Verify the zero-touch experience by connecting without having to select the VPN or type your credentials. The zero-touch experience means:

- The device doesn't ask you to trust the VPN server. Meaning, the user doesn't see the **Dynamic Trust** dialog box.
- The user doesn't have to enter credentials.
- When the user opens one of the associated apps, the user's device is connected to the VPN.

## Next steps

- To review iOS/iPadOS settings, go to [VPN settings for iOS/iPadOS devices in Microsoft Intune](vpn-settings-ios.md).
- To learn more about VPN setting and Intune, go to [configure VPN settings in Microsoft Intune](vpn-settings-configure.md).
