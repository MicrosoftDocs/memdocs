---
# required metadata

title: Configure Email settings for iOS/iPadOS devices in Microsoft Intune
description: See a list of all the email settings you can configure and add to iOS and iPadOS devices in Microsoft Intune, including using Exchange servers, and getting attributes from Azure Active Directory. You can also enable SSL, authenticate users with certificates or username/password, and synchronize email on iOS/iPadOS devices using device configuration profiles in Microsoft Intune.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 11/17/2022
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: beflamm, tycast, japoehlm
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; seodec18
ms.collection:
- tier3
- M365-identity-device-management
---

# Add e-mail settings for iOS and iPadOS devices in Microsoft Intune

In Microsoft Intune, you can create and configure email to connect to an Exchange email server, choose how users authenticate, use S/MIME for encryption, and more. The email profile uses the native or built-in email app on the device, and allows users to connect to their organization email.

This feature applies to:

- iOS/iPadOS

This article describes all the email settings available for devices running iOS/iPadOS. You can create a device configuration profile to push or deploy these email settings to your iOS/iPadOS devices.

## Before you begin

- Deploy your email app. For more information, go to [Configure email apps](email-settings-configure.md).
- Create an [iOS/iPadOS e-mail device configuration profile](email-settings-configure.md).

> [!NOTE]
> These settings are available for all enrollment types. For more information on the enrollment types, see [iOS/iPadOS enrollment](/mem/intune/fundamentals/deployment-guide-enrollment-ios-ipados).
>
> These settings use the [Apple ExchangeActiveSync payload](https://developer.apple.com/documentation/devicemanagement/exchangeactivesync) (opens Apple's web site).

## Exchange ActiveSync account settings

- **Email server**: Enter the host name of your Exchange server.
- **Account name**: Enter the display name for the email account. This name is shown to users on their devices.
- **Username attribute from AAD**: This name is the attribute Intune gets from Azure Active Directory. Intune dynamically generates the username that's used by this profile. Your options:
  - **User Principal Name**: Gets the name, such as `user1` or `user1@contoso.com`
  - **Primary SMTP address**: Gets the name in email address format, such as `user1@contoso.com`
  - **sAM Account Name**: Requires the domain, such as `domain\user1`. Also enter:  
    - **User domain name source**: Choose **AAD** (Azure Active Directory) or **Custom**.
      - **AAD**: Get the attributes from Azure AD. Also enter:
        - **User domain name attribute from AAD**: Choose to get the **Full domain name** (`contoso.com`) or the **NetBIOS name** (`contoso`) attribute of the user.

      - **Custom**: Get the attributes from a custom domain name. Also enter:
        - **Custom domain name to use**: Enter a value that Intune uses for the domain name, such as `contoso.com` or `contoso`.

- **Email address attribute from AAD**: Choose how the email address for the user is generated. Make sure your users have email addresses that match the attribute you select. Your options:
  - **User principal name**: Use the full principal name as the email address, such as `user1@contoso.com` or `user1`.
  - **Primary SMTP address**: Use the primary SMTP address to sign in to Exchange, such as `user1@contoso.com`.
- **Authentication method**: Choose how users to authenticate to the email server. Your options:
  - **Certificate**: Select a client SCEP or PKCS certificate profile you previously created to authenticate the Exchange connection. This option provides the most secure and better experience for your users.
  - **Username and Password**: Users are prompted to enter their user name and password.
  - **Derived credential**: Use a certificate that's derived from a user's smart card. For more information, see [Use derived credentials in Microsoft Intune](../protect/derived-credentials.md).

  >[!NOTE]
  > Azure multi-factor authentication isn't supported.
  
- **SSL**: **Enable** uses Secure Sockets Layer (SSL) communication when sending emails, receiving emails, and communicating with the Exchange server.
- **OAuth**: **Enable** uses Open Authorization (OAuth) communication when sending emails, receiving emails, and communicating with Exchange. If your OAuth server uses certificate authentication, choose **Certificate** as the **Authentication method**, and include the certificate with the profile. Otherwise, choose **Username and password** as the **Authentication method**. When using OAuth, be sure to:

  - Confirm your email solution supports OAuth before targeting this profile to your users. Microsoft 365 Exchange Online supports OAuth. On-premises Exchange and other partner or third-party solutions may not support OAuth. On-premises Exchange can be configured for Modern Authentication. For more information, see [Hybrid modern authentication overview and prerequisites for on-premises Skype for Business and Exchange servers](/office365/enterprise/hybrid-modern-auth-overview).

    If the email profile uses Oauth, and the email service doesn't support it, then the **Re-Enter password** option appears broken. For example, nothing happens when the user selects **Re-Enter password** in Apple's device settings.

  - When OAuth is enabled, end users have a different "Modern Authentication" email sign-in experience that supports multifactor authentication (MFA). 

  - Some organizations disable the end user's ability to do [self-service application access](/azure/active-directory/manage-apps/manage-self-service-access). In this scenario, the Modern Authentication sign-in may fail until an Administrator creates the "iOS Accounts" enterprise app, and grant users access to the app in Azure AD.

    The default action is to add an application using the [Application Access Panel](/azure/active-directory/user-help/active-directory-saas-access-panel-introduction) **Add App** feature **without business approval**. For more information, see [assign users to applications](/azure/active-directory/manage-apps/ways-users-get-assigned-to-applications).

  > [!NOTE]
  > When you enable OAuth, the following happens:
  >
  > 1. Devices that are already targeted are issued a new profile.
  > 2. End users are prompted to enter their credentials again.

## Exchange ActiveSync profile configuration

> [!IMPORTANT]
> Configuring these settings deploys a new profile to the device, even when an existing email profile is updated to include these settings. Users are prompted to enter their Exchange ActiveSync account password. These settings take effect when the password is entered.

- **Exchange data to sync**: When using Exchange ActiveSync, choose the Exchange services that are synced on the device: Calendar, Contacts, Reminders, Notes, and Email. Your options:
  - **All data** (default): Sync is enabled for all services.
  - **Email only**: Sync is enabled for Email only. Sync is disabled for the other services.
  - **Calendar only**: Sync is enabled for Calendar only. Sync is disabled for the other services.
  - **Calendar and Contacts only**: Sync is enabled for Calendar and Contacts only. Sync is disabled for the other services.
  - **Contacts only**: Sync is enabled for Contacts only. Sync is disabled for the other services.

  This feature applies to:  
  - iOS 13.0 and newer
  - iPadOS 13.0 and newer

- **Allow users to change sync settings**: Choose if users can change the Exchange ActiveSync settings for the Exchange services on the device: Calendar, Contacts, Reminders, Notes, and Email. Your options:

  - **Yes** (default): Users can change the sync behavior of all services. Choosing **Yes** allows changes to *all* services.
  - **No**: Users can't change the sync settings of all the services. Choosing **No** blocks changes to *all* services.

  > [!TIP]
  > If you configured the **Exchange data to sync** setting to sync only some services, we recommend selecting **No** for this setting. Choosing **No** prevents users from changing the Exchange service that's synced.

  This feature applies to:  
  - iOS 13.0 and newer
  - iPadOS 13.0 and newer

## Exchange ActiveSync email settings

- **S/MIME**: S/MIME uses email certificates that provide extra security to your email communications by signing, encrypting, and decrypting. When you use S/MIME with an email message, you confirm the authenticity of the sender, and the integrity and confidentiality of the message.

  Your options:

  - **Disable S/MIME** (default): Doesn't use an S/MIME email certificate to sign, encrypt, or decrypt emails.
  - **Enable S/MIME**: Allows users to sign and/or encrypt email in the iOS/iPadOS native mail application. Also enter:

    - **S/MIME signing enabled**: **Disable** (default) doesn't allow users to digitally sign the message. **Enable** allows users to digitally sign outgoing email for the account you entered. Signing helps users who receive messages be certain that the message came from the specific sender, and not from someone pretending to be the sender.
      - **Allow user to change setting**: **Enable** allows users to change the signing options. **Disable** (default) prevents users from changing the signing, and forces users to use the signing you configured.
      - **Signing certificate type**: Your options:
        - **Not configured**: Intune doesn't update or change this setting.
        - **None**: As an administrator, you don't force a specific certificate. Select this option so users can choose their own certificate.
        - **Derived credential**: Use a certificate that's derived from a user's smart card. For more information, see [Use derived credentials in Microsoft Intune](../protect/derived-credentials.md).
        - **Certificates**: Select an existing PKCS or SCEP certificate profile that's used for signing email messages.
      - **Allow user to change setting**: **Enable** allows users to change the signing certificate. **Disable** (default) prevents users from changing the signing certificate, and forces users to use the certificate you configured.

        This feature applies to:  
        - iOS 12 and newer
        - iPadOS 12 and newer

    - **Encrypt by default**: **Enable** encrypts all messages as the default behavior. **Disable** (default) doesn't encrypt all messages as the default behavior.
      - **Allow user to change setting**: **Enable** allows users to change the default encryption behavior. **Disable** prevents users from changing the encryption default behavior, and forces users to use the encryption you configured.

        This feature applies to:  
        - iOS 12 and newer
        - iPadOS 12 and newer

    - **Force per-message encryption**: Per-message encryption allows users to choose which emails are encrypted before being sent.

      **Enable** shows the per-message encryption option when creating a new email. Users can then choose to opt in or opt-out of per-message encryption. If the **Encrypt by default** setting is also enabled, enabling per-message encryption allows users to opt out of encryption per message.

      **Disable** (default) prevents the per-message encryption option from showing. If the **Encrypt by default** setting is also disabled, enabling per-message encryption allows users to opt in to encryption per message.

      - **Encryption certificate type**: Your options:
        - **Not configured**: Intune doesn't update or change this setting.
        - **None**: As an administrator, you don't force a specific certificate. Select this option so users can choose their own certificate.
        - **Derived credential**: Use a certificate that's derived from a user's smart card. For more information, see [Use derived credentials in Microsoft Intune](../protect/derived-credentials.md).
        - **Certificates**: Select an existing PKCS or SCEP certificate profile that's used for signing email messages.
      - **Allow user to change setting**: **Enable** allow users to change the encryption certificate. **Disable** (default) prevents users from changing the encryption certificate, and forces users to use the certificate you configured.

        This feature applies to:  
        - iOS 12 and newer
        - iPadOS 12 and newer

- **Amount of email to synchronize**: Choose the number of days of email that you want to synchronize. Or select **Unlimited** to synchronize all available email.
- **Allow messages to be moved to other email accounts**: **Enable** (default) allows users to move email messages between different accounts the users configured on their devices.
- **Allow email to be sent from third-party applications**: **Enable** (default) allows users to select this profile as the default account for sending email. It allows third-party applications to open email in the native email app, such as attaching files to email.
- **Synchronize recently used email addresses**: **Enable** (default) allows users to synchronize the list of email addresses that have been recently used on the device with the server.
- **VPN profile for per account VPN**: Starting in iOS/iPadOS 14, email traffic for the native Mail app can be routed through a VPN based on the account the user is using. When set to **None**, Intune doesn't enable per-account VPN for this e-mail profile.

  Per-app VPN connections you create are shown in this list. If you select a VPN profile from the list, any email that's sent to and from this account in the Mail app uses the VPN tunnel. The per-app VPN connection automatically turns on when users use their organization account in the Mail app.

  This feature applies to:  
  - iOS 14 and newer
  - iPadOS 14 and newer

## Next steps

The profile is created, but it's not doing anything yet. Next, [assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).

Configure email settings on [Android](email-settings-android.md), [Android Enterprise](email-settings-android-enterprise.md), and [Windows 10](email-settings-windows-10.md) devices.
