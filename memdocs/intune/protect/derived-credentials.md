---
# required metadata

title: Use derived credentials for mobile devices with Microsoft Intune
description: Use a third-party partners derived credential as an authentication method for Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/19/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.assetid:  

# optional metadata
 
#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- sub-certificates
---

# Use derived credentials with Microsoft Intune

Derived credentials are an implementation of the National Institute of Standards and Technology (NIST) guidelines for Derived Personal Identity Verification (PIV) credentials as part of [Special Publication (SP) 800-157](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-157.pdf) *(Link opens a .pdf file on nvlpubs.nist.gov)*.

*This article applies to:*

- *Android Enterprise fully managed devices that run version 7.0 and above*
- *iOS/iPadOS*
- *Windows 10*
- *Windows 11*

Organizations that require use of smart cards for authentication or encryption and signing can use Intune to provision mobile devices with a certificate that's derived from a user's smart card. That certificate is called a *derived credential*. Intune [supports several derived credential issuers](#supported-issuers), but use of only one issuer per tenant.

## About Intune's implementation

To use Intune derived credentials, an Intune administrator must configure the tenant to work with a supported derived credential issuer. You don't need to configure any Intune specific settings in the derived credential issuer's system.

- The Intune administrator specifies **Derived credential** as the *authentication method* for the following objects:

  **For Android Enterprise fully managed devices**:
  - Common profile types like Wi-Fi
  - App authentication

  **For iOS/iPadOS**:
  - Common profile types like Wi-Fi, VPN, and Email, which includes the iOS/iPadOS native mail app
  - App authentication
  - S/MIME signing and encryption

  **For Windows**:
  - Common profile types like Wi-Fi, and VPN
  
  > [!NOTE]
  > Currently, derived credentials as an authentication method for VPN profiles isn't working as expected on Windows devices. This behavior only affects VPN profiles on Windows devices and will be fixed in a future release (no ETA).

- For Android and iOS/iPadOS, users obtain a derived credential by using their smart card on a computer to authenticate to the derived credential issuer. The issuer then issues to the mobile device a certificate that's derived from their smart card. For Windows, users install an app from the derived credential provider that installs the certificate to the device for later use.
a
- After a device receives the derived credential, the credential is used for authentication and for S/MIME signing and encryption when apps or resource access profiles are configured to require the derived credential.

## Prerequisites

Review the following information before you configure your tenant to use derived credentials.

### Supported platforms

Intune supports derived credentials on the following platforms:

- iOS/iPadOS
- Android Enterprise:
  - Fully Managed devices (version 7.0 and above)
  - Corporate-Owned Work Profile
- Windows 10
- Windows 11

### Supported issuers

Intune supports a single derived credential issuer per tenant. The following issuers are supported:

- **DISA Purebred**: https://public.cyber.mil/pki-pke/purebred/
- **Entrust**: https://www.entrust.com/
- **Intercede**: https://www.intercede.com/

For important details about using the different issuers, review guidance for that issuer. For more information, see [Plan for derived credentials](#plan-for-derived-credentials) in this article.

> [!IMPORTANT]
> If you delete a derived credential issuer from your tenant, the derived credentials that were set up through that issuer will no longer function.
>
> See [Change the derived credential issuer](#change-the-derived-credential-issuer) later in this article.

### Required apps

Plan to deploy the relevant user-facing app to devices that enroll for a derived credential. Device users use the app to start the credential enrollment process.

- iOS devices use the Company Portal app. See [Add iOS store apps to Microsoft Intune](../apps/store-apps-ios.md).
- Android Enterprise Fully Managed and Corporate-Owned work profile devices use the Intune App. See  [Add Android store apps to Microsoft Intune](../apps/store-apps-android.md).

## Plan for derived credentials

Understand the following considerations before setting up a derived credential issuer for Android and iOS/iPadOS.

For Windows devices, see [Derived credentials for Windows](#derived-credentials-for-windows), later in this article.

### 1 - Review the documentation for your chosen derived credential issuer

Before you configure an issuer, review that issuer's documentation to understand how their system delivers derived credentials to devices.

Depending on the issuer you choose, you might need staff to be available at the time of enrollment to help users complete the process. Also review your current Intune configurations to ensure they don't block access that's necessary for devices or users to complete the credential request.

For example, you might use conditional access to block access to email for noncompliant devices. If you rely on email notifications to inform the user to start the derived credential enrollment process, your users might not receive those instructions until they're compliant with policy.

Similarly, some derived credential request workflows require the use of the device camera to scan an on-screen QR code. This code links that device to the authentication request that occurred against the derived credential issuer with the user's smart card credentials. If device configuration policies block camera use, the user can't complete the derived credential enrollment request.

**General information**:

- You can only configure a single issuer per tenant at a time, and that issuer is available to all users and supported devices in your tenant.

- Users aren't notified that they must enroll for derived credentials until you target them with a policy that requires derived credentials.

- Notification can be through app notification for the Company Portal, through email, or both. If you choose to use email notifications and you use enabled conditional access, users might not receive the email notification if their device isn't compliant.

  > [!IMPORTANT]
  > To ensure notifications related to device credentials are successfully received by end users, you should enable app notifications for the Company Portal, email notifications, or both.

### 2 - Review the end-user workflow for your chosen issuer

The following are key considerations for each supported partner. Become familiar with this information so you can ensure your Intune policies and configurations don't block users and devices from successfully completing enrollment for a derived credential from that issuer.

#### DISA Purebred

Review the platform-specific user workflow for the devices you'll use with derived credentials.

- [iOS and iPadOS](/mem/intune/user-help/enroll-ios-device-disa-purebred)
- [Android Enterprise](../user-help/enroll-android-device-disa-purebred.md) - *Corporate-Owned Work Profile* or *Fully managed devices*

**Key requirements include**:

- Users need access to a computer or KIOSK where they can use their smart card to authenticate to the issuer.
- iOS and iPadOS devices that will enroll for a derived credential must install the Intune Company Portal app. Android Fully Managed and Corporate-Owned Work Profile devices must install and use the Intune app.
- Use Intune to [deploy the DISA Purebred app](#deploy-the-disa-purebred-app) to devices that will enroll for a derived credential. This app must be deployed through Intune so that it's managed and can then work with the Intune Company Portal app or Intune App, which device users use to complete the derived credential request.
- To retrieve a derived credential from the Purebred app, the device must have access to the on-premises network. Access might be through corporate Wi-Fi or VPN.
- Device users must work with a live agent during the enrollment process. During enrollment, time-limited one-time passcodes are provided to the user as they continue through the enrollment process.
- When changes are made to a policy that uses derived credentials, such as creation of a new Wi-Fi profile, iOS and iPadOS users are notified to open the Company Portal app.
- Users are notified to open the applicable app when they need to renew their derived credential.

  The renewal process happens like this:

  - The derived credential issuer needs to issue new or updated certificates before the previous certificates are 80% of the way through their validity period.
  - The device checks in during the renewal period (the last 20% of the validity period).
  - Microsoft Intune notifies the user through email or an app notification to launch the Company Portal.
  - The user launches the Company Portal and taps the derived credential notification, and then the derived credential certificates are copied to the device.

For information getting and configuring the DISA Purebred app, see [Deploy the DISA Purebred app](#deploy-the-disa-purebred-app) later in this article.

#### Entrust

Review the platform-specific user workflow for the devices you'll use with derived credentials.

- [iOS and iPadOS](/mem/intune/user-help/enroll-ios-device-entrust-datacard)
- [Android Enterprise](../user-help/enroll-android-device-entrust-datacard.md)- *Corporate-Owned Work Profile* or *Fully managed devices*

**Key requirements include**:

- Users need access to a computer or KIOSK where they can use their smart card to authenticate to the issuer.
- iOS and iPadOS devices that will enroll for a derived credential must install the Intune Company Portal app. Android Fully Managed and Corporate-Owned Work Profile devices must install and use the Intune app.
- Use of a device camera to scan a QR code that links the authentication request to the derived credential request from the mobile device.
- Users are prompted by the Company Portal app or through email to enroll for derived credentials.
- When changes are made to a policy that uses derived credentials, such as creating a new Wi-Fi profile:
  - **iOS and iPadOS** - Users are notified to open the Company Portal app.
  - **Android Enterprise** *Corporate-Owned Work Profile* or *Fully managed devices* - The Company Portal app doesn't need to open.
- Users are notified to open the applicable app when they need to renew their derived credential.

  The renewal process happens like this:
  - The derived credential issuer needs to issue new or updated certificates before the previous certificates are 80% of the way through their validity period.
  - The device checks in during the renewal period (the last 20% of the validity period).
  - Microsoft Intune notifies the user through email or an app notification to launch the Company Portal.
  - The user launches the Company Portal and taps the derived credential notification, and then the derived credential certificates are copied to the device

#### Intercede

Review the platform-specific user workflow for the devices you'll use with derived credentials.

- [iOS and iPadOS](/mem/intune/user-help/enroll-ios-device-intercede)
- [Android Enterprise](../user-help/enroll-android-device-intercede.md) - *Corporate-Owned Work Profile* or *Fully managed devices*

**Key requirements include**:

- Users need access to a computer or KIOSK where they can use their smart card to authenticate to the issuer.
- iOS and iPadOS devices that will enroll for a derived credential must install the Intune Company Portal app. Android Fully Managed and Corporate-Owned Work Profile devices must install and use the Intune app.
- Use of a device camera to scan a QR code that links the authentication request to the derived credential request from the mobile device.
- Users are prompted by the Company Portal app or through email to enroll for derived credentials.
- When changes are made to a policy that uses derived credentials, such as creating a new Wi-Fi profile:
  - **iOS and iPadOS** - Users are notified to open the Company Portal app.
  - **Android Enterprise** *Corporate-Owned Work Profile* or *Fully managed devices* - The Company Portal app doesn't need to open.
- Users are notified to open the applicable app when they need to renew their derived credential.

  The renewal process happens like this:
  - The derived credential issuer needs to issue new or updated certificates before the previous certificates are 80% of the way through their validity period.
  - The device checks in during the renewal period (the last 20% of the validity period).
  - Microsoft Intune notifies the user through email or an app notification to launch the Company Portal.
  - The user launches the Company Portal and taps the derived credential notification, and then the derived credential certificates are copied to the device

### 3 - Deploy a trusted root certificate to devices

A trusted root certificate is used with derived credentials to verify that the derived credential certificate chain is valid and trusted. Even when not directly referenced by policy, a trusted root certificate is required. See [Configure a certificate profile for your devices in Microsoft Intune](certificates-configure.md).

### 4 - Provide end-user instructions for how to get the derived credential

Create and provide guidance to your users on how to start the derived credential enrollment process and to navigate you the derived credential enrollment workflow for your chosen issuer.

We recommend you provide a URL that hosts your guidance. You specify this URL when you configure the derived credential issuer for your tenant, and that URL is made available from within the Company Portal app. If you don't specify your own URL, Intune provides a link to generic details. These details can't cover all scenarios and might not be correct for your environment.

### 5 - Deploy Intune policies that require derived credentials

Create new policies or edit existing policies to use derived credentials. Derived credentials replace other authentication methods for the following objects:

- App authentication
- Wi-Fi
- VPN
- Email (iOS only)
- S/MIME signing and encryption, including Outlook (iOS only)

Avoid requiring use of a derived credential to access a process that you'll use as part of the process to get the derived credential, as that can prevent users from completing the request.

## Set up a derived credential issuer

Before you create policies that require use of a derived credential, set up a credential issuer in the Microsoft Intune admin center. A derived credential issuer is a tenant-wide setting. Tenants support only a single issuer at a time.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Tenant administration** > **Connectors and tokens** > **Derived Credentials**.

   :::image type="content" source="./media/derived-credentials/configure-provider.png" alt-text="Configure derived credentials in the Microsoft Intune admin center." lightbox="./media/derived-credentials/configure-provider.png":::

3. Specify a friendly **Display name** for the derived credential issuer policy. This name isn't shown to your device users.

4. For **Derived credential issuer**, select the derived credential issuer that you have chosen for your tenant:
   - DISA Purebred (iOS only)
   - Entrust
   - Intercede

5. Specify a **Derived credential help URL** to provide a link to a location that includes custom instructions to help users get derived credentials for your organization. The instructions should be specific to your organization and to the workflow that's necessary to get a credential from your chosen issuer. The link appears in the Company Portal app and should be accessible from the device.

   If you don't specify your own URL, Intune provides a link to generic details that can't cover all scenarios. This generic guidance might not be correct for your environment.

6. Select one or more options for **Notification type**. Notification types are the methods you use to inform users about the following scenarios:

   - Enroll a device with an issuer to get a new derived credential.
   - Get a new derived credential when the current credential is close to expiration.
   - Use a derived credential with a [supported object](#5---deploy-intune-policies-that-require-derived-credentials).

7. When ready, select **Save** to complete configuration of the derived credential issuer.

After you save the configuration, you can make changes to all fields except for the *Derived credential issuer*. To change the issuer, see [Change the derived credential issuer](#change-the-derived-credential-issuer).

## Deploy the DISA Purebred app

*This section applies only when you use DISA Purebred*.

To use **DISA Purebred** as your derived credential issuer for Intune, you must get the DISA Purebred app and then use Intune to deploy the app to devices. Then users request the derived credential from DISA Purebred by using the Company Portal App on their iOS/iPadOS device, or the Intune app on their Android devices.

In addition to deploying the DISA Purebred app with Intune, the device must have access to the on-premises network. To provide this access, consider using a VPN or corporate Wi-Fi.

**Complete the following tasks**:
  
1. Download the DISA Purebred application: https:\//cyber.mil/pki-pke/purebred/.

2. Deploy the DISA Purebred application in Intune.

   - See [Add an iOS line-of-business app to Microsoft Intune](../apps/lob-apps-ios.md).
   - See [Add an Android line-of-business app to Microsoft Intune](../apps/lob-apps-android.md)

   Extra settings for the Purebred app might be required. Speak to your Purebred agent to understand which values should be included in your policies, or if you have a DoD issued Common Access Card (CAC) you can access the Purebred documentation online at https:\//cyber.mil/pki-pke/purebred/.

3. If you choose to use a per-app VPN for the DISA Purebred application, see [Create a per-app VPN](../configuration/vpn-settings-configure.md).

## Use derived credentials for authentication and S/MIME signing and encryption

You can specify **Derived credential** for the following profile types and purposes:

- [Applications](#use-derived-credentials-for-app-authentication)
- Email:
  - [iOS and iPadOS](../configuration/email-settings-ios.md)
  - [Android Enterprise](../configuration/email-settings-android-enterprise.md)
- VPN:
  - [iOS and iPadOS](../configuration/vpn-settings-ios.md)
- [S/MIME signing and encryption](certificates-s-mime-encryption-sign.md)
- Wi-Fi:
  - [iOS and iPadOS](../configuration/wi-fi-settings-ios.md)
  - [Android Enterprise](../configuration/wi-fi-settings-android-enterprise.md)

  For Wi-Fi profiles, *Authentication method* is available only when the **EAP type** is set to one of the following values:
  - EAP – TLS
  - EAP-TTLS
  - PEAP

### Use derived credentials for app authentication

Use derived credentials for certificate-based authentication to web sites and applications. To deliver a derived credential for app authentication:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Manage devices** > **Configuration** > On the *Policies* tab, select **+ Create**.
3. Use the following settings:

   **For iOS and iPadOS**:

   - For *Platform*. select **iOS/iPadOS**, and then for *Profile type*, select **Templates > Derived credential**. Select **Create** to continue.
   - For *Name*, enter a descriptive name for the profile. Name your profiles so you can easily identify them later. For example, a good profile name is *Derived credential for iOS devices profile*.
   - For *Description*, enter a description that gives an overview of the setting, and any other important details.

   **For Android Enterprise**:

   - For *Platform*. select **Android Enterprise**, and then for *Profile type*, under *Fully Managed, Dedicated, and Corporate-Owned Work Profile*, select **Derived credential**. Select **Create** to continue.
   - For *Name*, enter a descriptive name for the profile. Name your profiles so you can easily identify them later. For example, a good profile name is **Derived credential for Android Enterprise devices profile**.
   - For *Description*, enter a description that gives an overview of the setting, and any other important details.
   - On the *Apps* page, configure **Certificate access** to manage how certificate access is granted to applications. Choose from:
     - **Require user approval for apps** *(default)* – Users must approve use of a certificate by all applications.
     - **Grant silently for specific apps (require user approval for other apps**) – With this option, select **Add apps**, and then select one or more apps that will silently use the certificate without user interaction.

4. On the **Assignments** page, select the groups that should receive the policy.

5. When finished, select **Create** to create the Intune profile. When complete, your profile is shown in the **Devices - Configuration profiles** list.

Users receive the app or email notification depending on the settings you specified when you set up the derived credential issuer. The notification informs the user to launch the Company Portal so that the derived credential policies can be processed.

## Derived credentials for Windows

You can use derived certificates as an authentication method for Wi-Fi and VPN profiles on Windows devices. The same providers that are supported by Android and iOS/iPadOS devices are supported as providers for Windows:

- **DISA Purebred**
- **Entrust**
- **Intercede**

> [!NOTE]
> Currently, derived credentials as an authentication method for VPN profiles isn't working as expected on Windows devices. This behavior only impacts VPN profiles on Windows devices and will be fixed in a future release (no ETA).

For Windows, users don't work through a smartcard registration process to obtain a certificate for use as a derived credential. Instead, the user needs to install the app for Windows, which is obtained from the derived credential provider. To use derived credentials with Windows, complete the following configurations:

1. **Install the app from the Derived Credential providers on the Windows device**.

   When you install the Windows app from a derived credential provider on a Windows device, the derived certificate is added to that device's Windows certificate store. After the certificate is added to the device, it becomes available for use a derived credential authentication method.

   After you get the app from your chosen provider, the app can be deployed to Users, or directly installed by the user of the device.

2. **Configure Wi-Fi and VPN profiles to use derived credentials as the authentication method**.

   When configuring a Windows profile for Wi-Fi or VPN, select **Derived credential** for the *Authentication Method*. With this configuration, the profile uses the certificate that installs on the device when the provider's app was installed.

## Renew a derived credential

Derived credentials for Android or iOS/iPadOS devices can't be extended or renewed. Instead, users must use the credential request workflow to request a new derived credential for their device. For Windows devices, consult the documentation for the App from your derived credential provider.

If you configure one or more methods for **Notification type**, Intune automatically notifies users when the current derived credential reaches 80% of its life span. The notification directs users to go through the credential request process to get a new derived credential.

After a device receives a new derived credential, policies that use derived credentials redeploy to that device.

## Change the derived credential issuer

At the tenant level, you can change your credential issuer, although only one issuer is supported by a tenant at a time.

After you change the issuer, users are prompted to get a new derived credential from the new issuer. They must do so before they can use a derived credential for authentication.

### Change the issuer for your tenant

> [!IMPORTANT]
> If you delete an issuer and immediately reconfigure that same issuer, you must still update profiles and devices to use derived credentials from that issuer. Derived credentials that were obtained before you delete the issuer are no longer valid.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Tenant administration** > **Connectors and tokens** > **Derived Credentials**.
3. Select **Delete** to remove the current derived credential issuer.
4. Configure a new issuer.

### Update profiles that use derived credentials

After you delete an issuer and then add a new one, edit each profile that uses derived credentials. This rule applies even if you restore the previous issuer. Any edit of the profile triggers an update, including a simple edit to the profile *Description*.

### Update derived credentials on devices

After you delete an issuer and then add a new one, device users must request a new derived credential. This rule applies even when you add the same issuer that you removed. The process to request the new derived credential is the same as for enrolling a new device or renewing an existing credential.

## Next steps

[Create device configuration profiles](../configuration/device-profile-create.md)
