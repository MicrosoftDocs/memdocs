---
# required metadata

title: macOS device feature settings in Microsoft Intune - Azure | Microsoft Docs
description: See the settings to configure macOS devices for AirPrint and customize the Login window to show or hide power buttons in Microsoft Intune. See the steps to get the IP address, path, and port settings of an AirPrint server in your network. Use these settings in a device configuration profile to configure macOS device features.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/09/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer:
ms.suite: ems
search.appverid:
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# macOS device feature settings in Intune

Intune includes some built-in settings to customize features on your macOS devices. For example, administrators can add AirPrint printers, choose how users sign in, configure the power controls, use single sign-on authentication, and more.

Use these features to control macOS devices as part of your mobile device management (MDM) solution.

This article lists these settings, and describes what each setting does. It also lists the steps to get the IP address, path, and port of AirPrint printers using the Terminal app (emulator). For more information on device features, go to [Add iOS/iPadOS or macOS device feature settings](device-features-configure.md).

## Before you begin

[Create a macOS device configuration profile](device-features-configure.md).

> [!NOTE]
> These settings apply to different enrollment types, with some settings applying to all enrollment options. For more information on the different enrollment types, see [macOS enrollment](../enrollment/macos-enroll.md).

## AirPrint

### Settings apply to: Device enrollment and Automated device enrollment 

- **IP address**: Enter the IPv4 or IPv6 address of the printer. If you use host names to identify printers, you can get the IP address by pinging the printer in the Terminal app. [Get the IP address and path](#get-the-ip-address-and-path) (in this article) provides more details.
- **Path**: Enter the path of the printer. The path is typically `ipp/print` for printers on your network. [Get the IP address and path](#get-the-ip-address-and-path) (in this article) provides more details.
- **Port** (iOS 11.0+, iPadOS 13.0+): Enter the listening port of the AirPrint destination. If you leave this property blank, AirPrint uses the default port.
- **TLS** (iOS 11.0+, iPadOS 13.0+): Select **Enable** to secure AirPrint connections with Transport Layer Security (TLS).

- **Add** The AirPrint server. You can add many AirPrint servers.

You can also **Import** a comma-separated file (.csv) that includes a list of AirPrint printers. Also, after you add AirPrint printers in Intune, you can **Export** this list.

### Get the IP address and path

To add AirPrinter servers, you need the IP address of the printer, the resource path, and the port. The following steps show you how to get this information.

1. On a Mac that's connected to the same local network (subnet) as the AirPrint printers, open **Terminal** (from **/Applications/Utilities**).
2. In the Terminal app, type `ippfind`, and select enter.

    Note the printer information. For example, it may return something similar to `ipp://myprinter.local.:631/ipp/port1`. The first part is the name of the printer. The last part (`ipp/port1`) is the resource path.

3. In the Terminal, type `ping myprinter.local`, and select enter.

   Note the IP address. For example, it may return something similar to `PING myprinter.local (10.50.25.21)`.

4. Use the IP address and resource path values. In this example, the IP address is `10.50.25.21`, and the resource path is `/ipp/port1`.

## Login items

### Settings apply to: All enrollment types

- **Files, folders, and custom apps**: **Add** the path of a file, folder, custom app, or system app you want to open when a user signs in to the device. System apps, or apps built or customized for your organization are typically in the `Applications` folder, with a path similar to `/Applications/AppName.app`. 

  You can add many files, folders, and apps. For example, enter:  
  
  - `/Applications/Calculator.app`
  - `/Applications`
  - `/Applications/Microsoft Office/root/Office16/winword.exe`
  - `/Users/UserName/music/itunes.app`
  
  When adding any app, folder, or file, be sure to enter the correct path. Not all items are in the `Applications` folder. If a user moves an item from one location to another, then the path changes. This moved item won't be opened when the user signs in.

## Login window

### Settings apply to: Device enrollment and Automated device enrollment

#### Window Layout

- **Show additional information in the menu bar**: When the time area on the menu bar is selected, **Allow** shows the host name and macOS version. **Not configured** (default) doesn't show this information on the menu bar.
- **Banner**: Enter a message that's shown on the sign in screen on the device. For example, enter your organization information, a welcome message, lost and found information, and so on.
- **Choose login format**: Choose how users sign in to the device. Your options:
  - **Prompt for username and password** (default): Requires users to enter a username and password.
  - **List all users, prompt for password**: Requires users to select their username from a user list, and then enter their password. Also configure:

    - **Local users**: **Hide** doesn't show the local user accounts in the user list, which may include the standard and admin accounts. Only the network and system user accounts are shown. **Not configured** (default) shows the local user accounts in the user list.
    - **Mobile accounts**: **Hide** doesn't show mobile accounts in the user list. **Not configured** (default) shows the mobile accounts in the user list. Some mobile accounts may show as network users.
    - **Network users**: Select **Show** to list the network users in the user list. **Not configured** (default) doesn't show the network user accounts in the user list.
    - **Admin users**: **Hide** doesn't show the administrator user accounts in the user list. **Not configured** (default) shows the administrator user accounts in the user list.
    - **Other users**: Select **Show** to list **Other...** users in the user list. **Not configured** (default) doesn't show the other user accounts in the user list.

#### Login screen power settings

- **Shut Down button**: **Hide** doesn't show the shutdown button on the sign in screen. **Not configured** (default) shows the shutdown button.
- **Restart button**: **Hide** doesn't show the restart button on the sign in screen. **Not configured** (default) shows the restart button.
- **Sleep button**: **Hide** doesn't show the sleep button on the sign in screen. **Not configured** (default) shows the sleep button.

#### Other

- **Disable user login from Console**: **Disable** hides the macOS command line used to sign in. For typical users, **Disable** this setting. **Not configured** (default) allows advanced users to sign in using the macOS command line. To enter console mode, users enter `>console` in the Username field, and must authenticate in the console window.

#### Apple Menu

After users sign in to the devices, the following settings impact what they can do.

- **Disable Shut Down**: **Disable** prevents users from selecting the **Shutdown** option after the user signs in. **Not configured** (default) allows users to select the **Shutdown** menu item on the device.
- **Disable Restart**: **Disable** prevents users from selecting the **Restart** option after the user signs in. **Not configured** (default) allows users to select the **Restart** menu item on the device.
- **Disable Power Off**: **Disable** prevents users from selecting the **Power off** option after the user signs in. **Not configured** (default) allows users to select the **Power off** menu item on the device.
- **Disable Log Out** (macOS 10.13 and later): **Disable** prevents users from selecting the **Log out** option after the user signs in. **Not configured** (default) allows users to select the **Log out** menu item on the device.
- **Disable Lock Screen** (macOS 10.13 and later): **Disable** prevents users from selecting the **Lock screen** option after the user signs in. **Not configured** (default) allows users to select the **Lock screen** menu item on the device.

## Single sign-on app extension

This feature applies to:

- macOS 10.15 and newer

### Settings apply to: All enrollment types 

- **SSO app extension type**: Choose the type of credential SSO app extension. Your options:

  - **Not configured**: App extensions aren't used. To disable an app extension, switch the SSO app extension type to **Not configured**.
  - **Redirect**: Use a generic, customizable redirect app extension to perform SSO with modern authentication flows. Be sure you know the extension and team ID for your organization's app extension.
  - **Credential**: Use a generic, customizable credential app extension to perform SSO with challenge-and-response authentication flows. Be sure you know the extension ID and team ID for your organization's SSO app extension.  
  - **Kerberos**: Use Apple's built-in Kerberos extension, which is included on macOS Catalina 10.15 and newer. This option is a Kerberos-specific version of the **Credential** app extension.

  > [!TIP]
  > With the **Redirect** and **Credential** types, you add your own configuration values to pass through the extension. If you're using **Credential**, consider using built-in configuration settings provided by Apple in the the **Kerberos** type.

- **Extension ID** (Redirect and Credential): Enter the bundle identifier that identifies your SSO app extension, such as `com.apple.ssoexample`.
- **Team ID** (Redirect and Credential): Enter the team identifier of your SSO app extension. A team identifier is a 10-character alphanumerical (numbers and letters) string generated by Apple, such as `ABCDE12345`. 

  [Locate your Team ID](https://help.apple.com/developer-account/#/dev55c3c710c) (opens Apple's website) has more information.

- **Realm** (Credential and Kerberos): Enter the name of your authentication realm. The realm name should be capitalized, such as `CONTOSO.COM`. Typically, your realm name is the same as your DNS domain name, but in all uppercase.

- **Domains** (Credential and Kerberos): Enter the domain or host names of the sites that can authenticate through SSO. For example, if your website is `mysite.contoso.com`, then `mysite` is the host name, and `contoso.com` is the domain name. When users connect to any of these sites, the app extension handles the authentication challenge. This authentication allows users to use Face ID, Touch ID, or Apple pincode/passcode to sign in.

  - All the domains in your single sign-on app extension Intune profiles must be unique. You can't repeat a domain in any sign-on app extension profile, even if you're using different types of SSO app extensions.
  - These domains aren't case-sensitive.

- **URLs** (Redirect only): Enter the URL prefixes of your identity providers on whose behalf the redirect app extension performs SSO. When a user is redirected to these URLs, the SSO app extension will intervene and prompt SSO.

  - All the URLs in your Intune single sign-on app extension profiles must be unique. You can't repeat a domain in any SSO app extension profile, even if you're using different types of SSO app extensions.
  - The URLs must begin with http:// or https://.

- **Additional configuration** (Redirect and Credential): Enter additional extension-specific data to pass to the SSO app extension:
  - **Key**: Enter the name of the item you want to add, such as `user name`.
  - **Type**: Enter the type of data. Your options:

    - String
    - Boolean: In **Configuration value**, enter `True` or `False`.
    - Integer: In **Configuration value**, enter a number.
    
  - **Value**: Enter the data.
  
  - **Add**: Select to add your configuration keys.

- **Keychain usage** (Kerberos only): Choose **Block** to prevent passwords from being saved and stored in the keychain. If blocked, user aren't prompted to save their password, and need to re-enter the password when the Kerberos ticket expires. **Not configured** (default) allows passwords to be saved and stored in the keychain. Users aren't prompted to re-enter their password when the ticket expires.
- **Face ID, Touch ID, or passcode** (Kerberos only): **Require** forces users to enter their Face ID, Touch ID, or device passcode when the credential is needed to refresh the Kerberos ticket. **Not configured** (default) doesn't require users to use biometrics or device passcode to refresh the Kerberos ticket. If **Keychain usage** is blocked, then this setting doesn't apply.
- **Default realm** (Kerberos only): Choose **Enable** to set the **Realm** value you entered as the default realm. **Not configured** (default) doesn't set a default realm.

  > [!TIP]
  > - **Enable** this setting if you're configuring multiple Kerberos SSO app extensions in your organization.
  > - **Enable** this setting if you're using multiple realms. It sets the **Realm** value you entered as the default realm.
  > - If you only have one realm, leave it **Not configured** (default).

- **Autodiscover** (Kerberos only): When set to **Block**, the Kerberos extension doesn't automatically use LDAP and DNS to determine its Active Directory site name. **Not configured** (default) allows the extension to automatically find the Active Directory site name.
- **Password changes** (Kerberos only): **Block** prevents users from changing the passwords they use to sign in to the domains you entered. **Not configured** (default) allows password changes.  
- **Password sync** (Kerberos only): Choose **Enable** to sync your users' local passwords to Azure AD. **Not configured** (default) disables password sync to Azure AD. Use this setting as an alternative or backup to SSO. This setting doesn't work if users are signed in with an Apple mobile account.
- **Windows Server Active Directory password complexity** (Kerberos only): Choose **Require** to force user passwords to meet Active Directory's password complexity requirements. See [Password must meet complexity requirements](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements) for more information. **Not configured** (default) doesn't require users to meet Active Directory's password requirement.
- **Minimum password length** (Kerberos only): Enter the minimum number of characters that can make up a user's password. **Not configured** (default) doesn't enforce a minimum password length on the users.
- **Password reuse limit** (Kerberos only): Enter the number of new passwords, from 1-24, that must be used until a previous password can be reused on the domain. **Not configured** (default) doesn't enforce a password reuse limit.
- **Minimum password age** (Kerberos only): Enter the number of days that a password must be used on the domain before a user can change it. **Not configured** (default) doesn't enforce a minimum age of passwords before they can be changed.
- **Password expiration notification** (Kerberos only): Enter the number of days before a password expires that users get notified that their password will expire. **Not configured** (default) uses `15` days.
- **Password expiration** (Kerberos only): Enter the number of days before the device password must be changed. **Not configured** (default) means user passwords never expire.
- **Password change URL** (Kerberos only): Enter the URL that launches when the user initiates a Kerberos password change.
- **Principal name** (Kerberos only): Enter the username of the Kerberos principal. You don't need to include the realm name. For example, in `user@contoso.com`, `user` is the principal name, and `contoso.com` is the realm name.

  > [!TIP]
  > - You can also use variables in the principal name by entering curly brackets `{{ }}`. For example, to show the username, enter       `Username: {{username}}`. 
  > - However, be careful with variable substitution because variables aren't validated in the UI and they are case sensitive. Be sure to enter the correct information.
  
- **Active Directory site code** (Kerberos only): Enter the name of the Active Directory site that the Kerberos extension should use. You may not need to change this value, as the Kerberos extension may automatically find the Active Directory site code.
- **Cache name** (Kerberos only): Enter the Generic Security Services (GSS) name of the Kerberos cache. You most likely don't need to set this value.  
- **Password requirements message** (Kerberos only): Enter a text version of your organization's password requirements that's shown to users. The message is shown if you don't require Active Directory's password complexity requirements, or don't enter a minimum password length.  
- **App bundle IDs** (Kerberos only): **Add** the app bundle identifiers that should use single sign-on on your devices. These apps are granted access to the Kerberos Ticket Granting Ticket, the authentication ticket, and authenticate users to services they're authorized to access.
- **Domain realm mapping** (Kerberos only): **Add** the domain DNS suffixes that should map to your realm. Use this setting when the DNS names of the hosts don't match the realm name. You most likely don't need to create this custom domain-to-realm mapping.
- **PKINIT certificate** (Kerberos only): **Select** the Public Key Cryptography for Initial Authentication (PKINIT) certificate that can be used for Kerberos authentication. You can choose from [PKCS](../protect/certficates-pfx-configure.md) or [SCEP](../protect/certificates-scep-configure.md) certificates that you've added in Intune. For more information about certificates, see [Use certificates for authentication in Microsoft Intune](../protect/certificates-configure.md).

## Associated domains

In Intune, you can:

- Add many app-to-domain associations.
- Associate many domains with the same app.

This feature applies to:

- macOS 10.15 and newer

### Settings apply to: All enrollment types

- **App ID**: Enter the app identifier of the app to associate with a website. The app identifier includes the team ID and a bundle ID: `TeamID.BundleID`.

  The team ID is a 10-character alphanumerical (letters and numbers) string generated by Apple for your app developers, such as `ABCDE12345`. [Locate your Team ID](https://help.apple.com/developer-account/#/dev55c3c710c) (opens Apple's web site) has more information.

  The bundle ID uniquely identifies the app, and typically is formatted in reverse domain name notation. For example, the bundle ID of Finder is `com.apple.finder`. To find the bundle ID, use the AppleScript in Terminal:

  `osascript -e 'id of app "ExampleApp"'`

- **Domain**: Enter the website domain to associate with an app. The domain includes a service type and fully qualified hostname, such as `webcredentials:www.contoso.com`.

  You can match all subdomains of an associated domain by entering `*.` (an asterisk wildcard and a period) before the beginning of the domain. The period is required. Exact domains have a higher priority than wildcard domains. So, patterns from parent domains are matched *if* a match isn't found at the fully qualified subdomain.

  The service type can be:

  - **authsrv**: Single sign-on app extension
  - **applink**: Universal link
  - **webcredentials**: Password autofill

- **Add**: Select to add your apps and associated domains.

> [!TIP]
> To troubleshoot, on your macOS device, open **System Preferences** > **Profiles**. Confirm the profile you created is in the device profiles list. If it's listed, be sure the **Associated Domains Configuration** is in the profile, and it includes the correct app ID and domains.

## Next steps

[Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).

You can also configure device features on [iOS/iPadOS](ios-device-features-settings.md).
