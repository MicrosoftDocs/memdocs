---
# required metadata

title: macOS device feature settings in Microsoft Intune
description: See the settings to configure macOS devices for AirPrint and customize the Login window to show or hide power buttons in Microsoft Intune. See the steps to get the IP address, path, and port settings of an AirPrint server in your network. Use these settings in a device configuration profile to configure macOS device features.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 11/29/2021
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: beflamm
ms.suite: ems
search.appverid:
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# macOS device feature settings in Intune

Intune includes built-in settings to customize features on your macOS devices. For example, administrators can add AirPrint printers, choose how users sign in, configure the power controls, use single sign-on authentication, and more.

Use these features to control macOS devices as part of your mobile device management (MDM) solution.

This article describes these settings. It also lists the steps to get the IP address, path, and port of AirPrint printers using the Terminal app (emulator). For more information on device features, go to [Add iOS/iPadOS or macOS device feature settings](device-features-configure.md).

> [!NOTE]
> The user interface may not match the enrollment types in this article. The information in this article is correct. The user interface is being updated in an upcoming release.

## Before you begin

Create a [macOS device features configuration profile](device-features-configure.md).

> [!NOTE]
> These settings apply to different enrollment types, with some settings applying to all enrollment options. For more information on the different enrollment types, see [macOS enrollment](../enrollment/macos-enroll.md).

## AirPrint

### Settings apply to: All enrollment types

- **AirPrint destinations**: **Add** one or more AirPrint printers users can print from their devices. Also enter:
  - **IP address**: Enter the IPv4 or IPv6 address of the printer. For example, enter `10.0.0.1`. If you use host names to identify printers, you can get the IP address by pinging the printer in the Terminal app. [Get the IP address and path](#get-the-ip-address-and-path) (in this article) has more details.  
  - **Resource path**: Enter the resource path of the printer. The path is typically `ipp/print` for printers on your network. [Get the IP address and path](#get-the-ip-address-and-path) (in this article) has more details.
  - **Port** (iOS 11.0+, iPadOS 13.0+): Enter the listening port of the AirPrint destination. If you leave this property blank, AirPrint uses the default port.
  - **Force TLS** (iOS 11.0+, iPadOS 13.0+): Your options:  
    - **Disable** (default): Transport Layer Security (TLS) isn't enforced when connecting to AirPrint printers.
    - **Enable**: Secures AirPrint connections with Transport Layer Security (TLS).

- **Import** a comma-separated file (.csv) that includes a list of AirPrint printers. Also, after you add AirPrint printers in Intune, you can **Export** this list.

### Get the IP address and path

To add AirPrinter servers, you need the IP address of the printer, the resource path, and the port. The following steps show you how to get this information.

1. On a Mac that's connected to the same local network (subnet) as the AirPrint printers, open **Terminal** (from **/Applications/Utilities**).
2. In the Terminal app, type `ippfind`, and select enter.

    Note the printer information. For example, it may return something similar to `ipp://myprinter.local.:631/ipp/port1`. The first part is the name of the printer. The last part (`ipp/port1`) is the resource path.

3. In the Terminal, type `ping myprinter.local`, and select enter.

   Note the IP address. For example, it may return something similar to `PING myprinter.local (10.50.25.21)`.

4. Use the IP address and resource path values. In this example, the IP address is `10.50.25.21`, and the resource path is `/ipp/port1`.

## Associated domains

In Intune, you can:

- Add many app-to-domain associations.
- Associate many domains with the same app.

This setting applies to:

- macOS 10.15 and newer

### Settings apply to: User approved device enrollment, and Automated device enrollment

These settings use the [AssociatedDomains.ConfigurationItem payload](https://developer.apple.com/documentation/devicemanagement/associateddomains/configurationitem) (opens Apple's web site).

- **Associated domains**: **Add** an association between your domain and an app. This feature shares sign on credentials between a Contoso app and a Contoso website. Also enter:

  - **App ID**: Enter the app identifier of the app to associate with a website. The app identifier includes the team ID and a bundle ID: `TeamID.BundleID`.

    The team ID is a 10-character alphanumerical (letters and numbers) string generated by Apple for your app developers, such as `ABCDE12345`. [Locate your Team ID](https://help.apple.com/developer-account/#/dev55c3c710c) (opens Apple's web site) has more information.

    The bundle ID uniquely identifies the app, and typically is formatted in reverse domain name notation. For example, the bundle ID of Finder is `com.apple.finder`. To find the bundle ID, use the AppleScript in Terminal:

    `osascript -e 'id of app "ExampleApp"'`

  - **Domains**: Enter the website domain to associate with an app. The domain includes a service type and fully qualified hostname, such as `webcredentials:www.contoso.com`.

    You can match all subdomains of an associated domain by entering `*.` (an asterisk wildcard and a period) before the beginning of the domain. The period is required. Exact domains have a higher priority than wildcard domains. So, patterns from parent domains are matched *if* a match isn't found at the fully qualified subdomain.

    The service type can be:

    - **authsrv**: Single sign-on app extension
    - **applink**: Universal link
    - **webcredentials**: Password autofill

  - **Enable direct downloads**: **Yes** downloads the domain data directly from the device, instead of going through Apple's content delivery network (CDN). When set to **Not configured**, Intune doesn't change or update this setting. By default, the OS might download data through Apple's CDN dedicated to Associated Domains.

    This setting applies to:

    - macOS 11 and newer

> [!TIP]
> To troubleshoot, on your macOS device, open **System Preferences** > **Profiles**. Confirm the profile you created is in the device profiles list. If it's listed, be sure the **Associated Domains Configuration** is in the profile, and it includes the correct app ID and domains.

## Content caching

Content caching saves a local copy of content. This information can be retrieved by other Apple devices without connecting to the Internet. This caching accelerates downloads by saving software updates, apps, photos, and other content the first time they're downloaded. Since apps are downloaded once and shared to other devices, schools and organization with many devices save bandwidth.

> [!NOTE]
> Only use one profile for these settings. If you assign multiple profiles with these settings, an error occurs.
>
> For more information on monitoring content caching, see [View content caching logs and statistics](https://support.apple.com/guide/mac-help/view-content-caching-logs-statistics-mac-mchl0d8533cd/10.15/mac/10.15) (opens Apple's web site).

This setting applies to:

- macOS 10.13.4 and newer

### Settings apply to: All enrollment types

For more information on these settings, see [Content Caching payload settings](https://support.apple.com/guide/mdm/content-caching-mdm163612d39/1/web/1) (opens Apple's web site).

**Enable content caching**: **Yes** turns on content caching, and users can't disable it. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might turn it off.

- **Type of content to cache**: Your options:
  - **All content**: Caches iCloud content and shared content.
  - **User content only**: Caches user's iCloud content, including photos and documents.
  - **Shared content only**: Caches apps and software updates.

- **Maximum cache size**: Enter the maximum amount of disk space (in bytes) that's used to cache content. When left blank (default), Intune doesn't change or update this setting. By default, the OS might set this value to zero (`0`) bytes, which gives unlimited disk space to the cache.

  Be sure you don't exceed the space available on the devices. For more information on device storage capacity, see [How iOS and macOS report storage capacity](https://support.apple.com/HT201402) (opens Apple's web site).

- **Cache location**: Enter the path to store the cached content. The default location is `/Library/Application Support/Apple/AssetCache/Data`. It's recommended that you don't change this location.

  If you change this setting, your cached content isn't moved to the new location. To move it automatically, users need to change the location on the device (**System Preferences** > **Sharing** > **Content Caching**).

- **Port**: Enter the TCP port number on devices for the cache to accept download and upload requests, from 0-65535. Enter zero (`0`) (default) to use whatever port is available.
- **Block internet connection and cache content sharing**: Also known as tethered caching. **Yes** prevents Internet connection sharing, and prevents sharing cached content with iOS/iPadOS devices USB-connected to their Mac. Users can't enable this feature. When set to **Not configured** (default), Intune doesn't change or update this setting.

- **Enable internet connection sharing**: Also known as tethered caching. **Yes** allows Internet connection sharing, and allows sharing cached content with iOS/iPadOS devices USB-connected to their Mac. Users can't disable this feature. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might turn this off.

  This setting applies to:

  - macOS 10.15.4 and newer

- **Enable cache to log client details**: **Yes** logs the IP address and port number of the devices that request content. If you're troubleshooting device issues, this log file may help. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not log this information.

- **Always keep content from the cache, even when the system needs disk space for other apps**: **Yes** keeps the cache content, and makes sure nothing is deleted, even when disk space is low. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might purge content from the cache automatically when it needs storage space for other apps.

  This setting applies to:

  - macOS 10.15 and newer

- **Show status alerts**: **Yes** shows as alerts as system notifications. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not show these alerts as system notifications.

  This setting applies to:

  - macOS 10.15 and newer

- **Prevent the device from sleeping while caching is turned on**: **Yes** prevents the computer from going to sleep when caching is on. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow the device to sleep.

  This setting applies to:

  - macOS 10.15 and newer

- **Devices to cache**: Choose the devices that can cache content. Your options:
  - **Not configured** (default): Intune doesn't change or update this setting. 
  - **Devices using the same local network**: The content cache offers content to devices on the same immediate local network. No content is offered to devices on other networks, including devices reachable by the content cache.
  - **Devices using the same public IP address**: The content cache offers content to devices using the same public IP address. No content is offered to devices on other networks, including devices reachable by the content cache.
  - **Devices using custom local networks**: The content cache provides content to devices in the IP ranges you enter.
    - **Client listen ranges**: Enter the range of IP addresses that can receive the content cache.
  - **Devices using custom local networks with fallback**: The content cache provides content to devices in the listen ranges, peer listen ranges, and parents IP addresses.
    - **Client listen ranges**: Enter the range of IP addresses that can receive the content cache.

- **Custom public IP addresses**: Enter a range of public IP addresses. The cloud servers use this range to match client devices to caches.

- **Share content with other caches**: When your network has more than one content cache, the content caches on other devices automatically become peers. These devices can consult and share cached software. 

  When a requested item isn’t available on one content cache, it checks its peers for the item. If the item is available, it’s downloaded from the content cache on the peer device. If it’s still not available, the content cache downloads the item from:

  - A parent IP address, if any are configured
  
    OR,

  - From Apple through the Internet

  When more than one content cache is available, devices automatically select the right content cache. 

  Your options:

  - **Not configured** (default): Intune doesn't change or update this setting.
  - **Content caches using the same local networks**: Content cache only peers with other content caches on the same immediate local network.
  - **Content caches using the same public IP address**: Content cache only peers with other content caches on the same public IP address.
  - **Content caches using custom local networks**: Content cache only peers with other content caches in the IP address listen range you enter:

    - **Peer listen ranges**: Enter the IPv4 or IPv6 start and ending IP addresses for your range. The content cache responds only to peer cache requests from content caches in the IP address ranges you enter.
    - **Peer filter ranges**: Enter the IPv4 or IPv6 start and ending IP addresses for your range. The content cache filters its list of peers using the IP address ranges you enter.

- **Parent IP addresses**: Enter the local IP address of another content cache to add as a parent cache. Your cache uploads and downloads content to these caches, instead of uploading/downloading directly with Apple. Only add a parent IP address once.
- **Parent selection policy**: When there are many parent caches, select how the parent IP address is chosen. Your options:
  - **Not configured** (default): Intune doesn't change or update this setting.
  - **Round robin**: Use the parent IP addresses in order. This option is good for load-balancing scenarios.
  - **First available**: Always use the first available IP address in the list.
  - **Hash**: Creates a hash value for the path portion of the requested URL. This option makes sure the same parent IP address is always used for the same URL.
  - **Random**: Randomly use an IP address in the list. This option is good for load-balancing scenarios.
  - **Sticky available**: Always use the first IP address in the list. If it's not available, then use the second IP address in the list. Continue to use the second IP address until it's not available, and so on.

## Login items

### Settings apply to: All enrollment types

- **Add the files, folders, and custom apps that will launch at login**: **Add** the path of a file, folder, custom app, or system app that opens when users sign in to their devices. Also enter:

  - **Path of item**: Enter the path to the file, folder, or app. System apps, or apps built or customized for your organization are typically in the `Applications` folder, with a path similar to `/Applications/AppName.app`.

    You can add many files, folders, and apps. For example, enter:  
  
    - `/Applications/Calculator.app`
    - `/Applications`
    - `/Applications/Microsoft Office/root/Office16/winword.exe`
    - `/Users/UserName/music/itunes.app`
  
    When adding any app, folder, or file, be sure to enter the correct path. Not all items are in the `Applications` folder. If users move an item from one location to another, then the path changes. This moved item won't be opened when the user signs in.

  - **Hide**: Choose to show or hide the app. Your options:
    - **Not configured** (default): Intune doesn't change or update this setting. By default, the OS might show items in the Users & Groups login items list with the hide option unchecked.
    - **Yes**: Hides the app in the Users & Groups login items list.

## Login window

### Settings apply to: All enrollment types

#### Windows Layout  

- **Show additional information in the menu bar**: When the time area on the menu bar is selected, **Yes** shows the host name and macOS version. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not show this information on the menu bar.
- **Banner**: Enter a message that's shown on the sign in screen on devices. For example, enter your organization information, a welcome message, lost and found information, and so on.
- **Require username and password text fields**: Choose how users sign in to devices. **Yes** requires users to enter a username and password. When set to **Not configured**, Intune doesn't change or update this setting. By default, the OS may require users to select their username from a list, and then type their password.

  Also enter:

  - **Hide local users**: **Yes** hides the local user accounts in the user list, which may include the standard and admin accounts. Only the network and system user accounts are shown. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might show the local user accounts in the user list.
  - **Hide mobile accounts**: **Yes** hides mobile accounts in the user list. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might show the mobile accounts in the user list. Some mobile accounts may show as network users.
  - **Show network users**: Select **Yes** to list the network users in the user list. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not show the network user accounts in the user list.
  - **Hide computer's administrators**: **Yes** hides the administrator user accounts in the user list. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might show the administrator user accounts in the user list.
  - **Show other users**: Select **Yes** to list **Other...** users in the user list. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not show the other user accounts in the user list.  

#### Login screen power settings  

- **Hide shut down button**: **Yes** hides the shutdown button on the sign in screen. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might show the shutdown button.
- **Hide restart button**: **Yes** hides the restart button on the sign in screen. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might show the restart button.
- **Hide sleep button**: **Yes** hides the sleep button on the sign in screen. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might show the sleep button.
- **Disable user login from Console**: **Yes** hides the macOS command line used to sign in. For typical users, set this setting to **Yes**. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow advanced users to sign in using the macOS command line. To enter console mode, users enter `>console` in the Username field, and must authenticate in the console window.  

#### Apple Menu  
- **Disable Shut Down while logged in**: **Yes** prevents users from selecting the **Shutdown** option after they sign in. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to select the **Shutdown** menu item on devices.
- **Disable Restart while logged in**: **Yes** prevents users from selecting the **Restart** option after they sign in. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to select the **Restart** menu item on devices.
- **Disable Power Off while logged in**: **Yes** prevents users from selecting the **Power off** option after they sign in. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to select the **Power off** menu item on devices.
- **Disable Log Out while logged in** (macOS 10.13 and later): **Yes** prevents users from selecting the **Log out** option after they sign in. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to select the **Log out** menu item on devices.
- **Disable Lock Screen while logged in** (macOS 10.13 and later): **Yes** prevents users from selecting the **Lock screen** option after they sign in. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow users to select the **Lock screen** menu item on devices.  

## Single sign-on app extension

This setting applies to:

- macOS 10.15 and newer

### Settings apply to: User approved device enrollment, and Automated device enrollment

- **SSO app extension type**: Choose the type of SSO app extension. Your options:

  - **Not configured**: App extensions aren't used. To disable an app extension, switch the SSO app extension type to **Not configured**.
  - **Microsoft Azure AD**: Uses the Microsoft Enterprise SSO plug-in, which is a redirect-type SSO app extension. This plug-in provides SSO for Active Directory accounts across all macOS applications that support [Apple’s Enterprise Single Sign-On](https://developer.apple.com/documentation/authenticationservices) feature. Use this SSO app extension type to enable SSO on Microsoft apps, organization apps, and websites that authenticate using Azure AD.

    The SSO plug-in acts as an advanced authentication broker that offers security and user experience improvements.

    > [!IMPORTANT]
    > - The Microsoft Azure AD SSO extension is in public preview. This preview version is provided without a service level agreement (SLA). It's not recommended to use in production. Certain features might not be supported, or might have restricted behavior. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms).
    >
    > - To achieve SSO with the Microsoft Azure AD SSO app extension type, install the macOS Company Portal app on devices. The Company Portal app delivers the Microsoft Enterprise SSO plug-in to devices. The MDM SSO app extension settings activate the plug-in. After the Company Portal app and the SSO app extension profile are installed on devices, users sign in with their credentials, and create a session on their devices. This session is used across different applications without requiring users to authenticate again.
    >
    >   For more information about the Company Portal app, see [What happens if you install the Company Portal app and enroll your macOS device in Intune](../user-help/what-happens-if-you-install-the-Company-Portal-app-and-enroll-your-device-in-intune-macos.md). 
    > 
    >   You can also [download the Company Portal app](https://go.microsoft.com/fwlink/?linkid=853070).

  - **Redirect**: Use a generic, customizable redirect app extension to use SSO with modern authentication flows. Be sure you know the extension and team ID for your organization's app extension.
  - **Credential**: Use a generic, customizable credential app extension to use SSO with challenge-and-response authentication flows. Be sure you know the extension ID and team ID for your organization's SSO app extension.  
  - **Kerberos**: Use Apple's built-in Kerberos extension, which is included on macOS Catalina 10.15 and newer. This option is a Kerberos-specific version of the **Credential** app extension.

  > [!TIP]
  > With the **Redirect** and **Credential** types, you add your own configuration values to pass through the extension. If you're using **Credential**, consider using built-in configuration settings provided by Apple in the the **Kerberos** type.

- **Extension ID** (Redirect, Credential): Enter the bundle identifier that identifies your SSO app extension, such as `com.apple.ssoexample`.
- **Team ID** (Redirect, Credential): Enter the team identifier of your SSO app extension. A team identifier is a 10-character alphanumerical (numbers and letters) string generated by Apple, such as `ABCDE12345`. 

  [Locate your Team ID](https://help.apple.com/developer-account/#/dev55c3c710c) (opens Apple's website) has more information.

- **Realm** (Credential, Kerberos): Enter the name of your authentication realm. The realm name should be capitalized, such as `CONTOSO.COM`. Typically, your realm name is the same as your DNS domain name, but in all uppercase.

- **Domains** (Credential, Kerberos): Enter the domain or host names of the sites that can authenticate through SSO. For example, if your website is `mysite.contoso.com`, then `mysite` is the host name, and `.contoso.com` is the domain name. When users connect to any of these sites, the app extension handles the authentication challenge. This authentication allows users to use Face ID, Touch ID, or Apple pincode/passcode to sign in.

  - All the domains in your single sign-on app extension Intune profiles must be unique. You can't repeat a domain in any sign-on app extension profile, even if you're using different types of SSO app extensions.
  - These domains aren't case-sensitive.
  - The domain must start with a period (`.`).

- **URLs** (Redirect only): Enter the URL prefixes of your identity providers on whose behalf the redirect app extension uses SSO. When users are redirected to these URLs, the SSO app extension intervenes, and prompts for SSO.

  - All the URLs in your Intune single sign-on app extension profiles must be unique. You can't repeat a domain in any SSO app extension profile, even if you're using different types of SSO app extensions.
  - The URLs must begin with `http://` or `https://`.

- **Additional configuration** (Microsoft Azure AD, Redirect, Credential): Enter additional extension-specific data to pass to the SSO app extension:
  - **Key**: Enter the name of the item you want to add, such as `user name`.
  - **Type**: Enter the type of data. Your options:

    - String
    - Boolean: In **Configuration value**, enter `True` or `False`.
    - Integer: In **Configuration value**, enter a number.

  - **Value**: Enter the data.

- **Block keychain usage** (Kerberos only): **Yes** prevents passwords from being saved and stored in the keychain. When set to **Yes**, users aren't prompted to save their password, and need to reenter the password when the Kerberos ticket expires. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow passwords to be saved and stored in the keychain. Users aren't prompted to reenter their password when the ticket expires.
- **Require Face ID, Touch ID, or passcode** (Kerberos only): **Yes** forces users to enter their Face ID, Touch ID, or device passcode when the credential is needed to refresh the Kerberos ticket. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not require users to use biometrics or device passcode to refresh the Kerberos ticket. If **Keychain usage** is blocked, then this setting doesn't apply.
- **Set as default realm** (Kerberos only): Choose **Yes** to set the **Realm** value you entered as the default realm. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not set a default realm.

  > [!TIP]
  > - Select **Yes** for this setting if you're configuring multiple Kerberos SSO app extensions in your organization.
  > - Select **Yes** for this setting if you're using multiple realms. It sets the **Realm** value you entered as the default realm.
  > - If you only have one realm, leave it **Not configured** (default).

- **Block Autodiscover** (Kerberos only): When set to **Yes**, the Kerberos extension doesn't automatically use LDAP and DNS to determine its Active Directory site name. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow the extension to automatically find the Active Directory site name.

- **Allow only managed apps** (Kerberos only): When set to **Yes**, the Kerberos extension allows only managed apps, and any apps entered with the app bundle ID to access the credential. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow non-managed apps to access the credential.

  This feature applies to:
  
  - macOS 12 and newer

- **Block password changes** (Kerberos only): **Yes** prevents users from changing the passwords they use to sign in to the domains you entered. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow password changes.  
- **Enable local password sync** (Kerberos only): Choose **Yes** to sync your users' local passwords to Azure AD. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might disable password sync to Azure AD. Use this setting as an alternative or backup to SSO. This setting doesn't work if users are signed in with an Apple mobile account.

- **Delay Kerberos extension setup** (Kerberos only): When set to **Yes**, the user isn’t prompted to set up the Kerberos extension until the extension is enabled by the admin, or a Kerberos challenge is received. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might immediately prompt the user to set up the Kerberos extension.

  This feature applies to:
  
  - macOS 11 and newer

- **Allow standard Kerberos utilities** (Kerberos only): When set to **Yes**, the Kerberos extension allows any apps entered with the app bundle ID, managed apps, and standard Kerberos utilities, such as TicketViewer and klist, to access and use the credential. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not allow listed apps to access and use the credential.

  This feature applies to:
  
  - macOS 12 and newer

- **Request credential** (Kerberos only): When set to **Yes**, the credential is requested on the next matching Kerberos challenge or network state change. When the credential is expired or missing, a new credential is created. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not request a new credential.

  This feature applies to:
  
  - macOS 12 and newer

- **Require LDAP connections for TLS** (Kerberos only): When set to **Yes**, LDAP connections are required to use Transport Layer Security (TLS). When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not require LDAP connections to use TLS.

  This feature applies to:
  
  - macOS 11 and newer

- **Require Active Directory password complexity** (Kerberos only): Choose **Yes** to force user passwords to meet Active Directory's password complexity requirements. On devices, this setting shows a pop-up window with check boxes so users see they're completing the password requirements. It helps users know what they need to enter for the password. For more information, see [Password must meet complexity requirements](/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements). When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not require users to meet Active Directory's password requirement.
- **Minimum password length** (Kerberos only): Enter the minimum number of characters that can make up users passwords. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not enforce a minimum password length on the users.
- **Password reuse limit** (Kerberos only): Enter the number of new passwords, from 1-24, that are used until a previous password can be reused on the domain. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not enforce a password reuse limit.
- **Minimum password age (days)** (Kerberos only): Enter the number of days that a password is used on the domain before users can change it. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not enforce a minimum age of passwords before they can be changed.
- **Password expiration notification (days)** (Kerberos only): Enter the number of days before a password expires that users get notified that their password will expire. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might use `15` days.
- **Password expiration (days)** (Kerberos only): Enter the number of days before the device password must change. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might never expire passwords.
- **Password change URL** (Kerberos only): Enter the URL that opens when users start a Kerberos password change.
- **Custom user name** (Kerberos only): Enter the text that replaces the user name shown in the Kerberos extension. You can enter a name that matches the name of your company or organization. For example, you can enter `Contoso`.

  This feature applies to:
  
  - macOS 11 and newer

- **Kerberos extension use** (Kerberos only): Select how other processes use the Kerberos Extension credential. Your options: 
  - **Always**: The extension credential is always used if the SPN is listed in **Domains**. It's not used if the calling app isn't listed in **App Bundle IDs**. 
  - **When not specified**: The extension credential is only used when another credential isn’t entered by the caller, and the SPN is listed in Domains. It's not used if the calling app isn't listed in **App Bundle IDs**. 
  - **Kerberos default**: Intune doesn't change or update this setting. By default, the OS uses the default Kerberos processes for selecting credentials. This option is the same as not configuring this setting.

  This feature applies to:
  
  - macOS 11 and newer

- **Principal name** (Kerberos only): Enter the username of the Kerberos principal. You don't need to include the realm name. For example, in `user@contoso.com`, `user` is the principal name, and `contoso.com` is the realm name.

  > [!TIP]
  > - You can also use variables in the principal name by entering curly brackets `{{ }}`. For example, to show the username, enter `Username: {{username}}`. 
  > - However, be careful with variable substitution because variables aren't validated in the UI and they are case sensitive. Be sure to enter the correct information.
  
- **Active Directory site code** (Kerberos only): Enter the name of the Active Directory site that the Kerberos extension should use. You may not need to change this value, as the Kerberos extension may automatically find the Active Directory site code.
- **Cache name** (Kerberos only): Enter the Generic Security Services (GSS) name of the Kerberos cache. You most likely don't need to set this value.  
- **Sign in window text** (Kerberos only): Enter the text shown to users at the Kerberos sign in window.

  This feature applies to:
  
  - macOS 11 and newer

- **Password requirements message** (Kerberos only): Enter a text version of your organization's password requirements that's shown to users. The message shows if you don't require Active Directory's password complexity requirements, or don't enter a minimum password length.  

  When set to **Yes**, all existing user accounts are wiped from the devices. To avoid data loss, or prevent a factory reset, make sure you understand how this setting changes your devices.

  For more information about shared device mode, see [Overview of shared device mode](/azure/active-directory/develop/msal-shared-devices).

- **App bundle IDs** (Microsoft Azure AD, Kerberos): Enter the app bundle identifiers that should use single sign-on on your devices. These apps are granted access to the Kerberos Ticket Granting Ticket and the authentication ticket. The apps also authenticate users to services they're authorized to access.
- **Domain realm mapping** (Kerberos only): Enter the domain DNS suffixes that should map to your realm. Use this setting when the DNS names of the hosts don't match the realm name. You most likely don't need to create this custom domain-to-realm mapping.
- **PKINIT certificate** (Kerberos only): **Select** the Public Key Cryptography for Initial Authentication (PKINIT) certificate that can be used for Kerberos authentication. You can choose from [PKCS](../protect/certificates-pfx-configure.md) or [SCEP](../protect/certificates-scep-configure.md) certificates that you've added in Intune. For more information about certificates, see [Use certificates for authentication in Microsoft Intune](../protect/certificates-configure.md).
- **Preferred KDCs** (Kerberos only): Enter the Key Distribution Centers (KDCs) to use for Kerberos traffic in order of preference. This list is used when the servers are not discoverable using DNS. When the servers are discoverable, the list is used for both connectivity checks, and used first for Kerberos traffic. If the servers don’t respond, then the device uses DNS discovery.

  This feature applies to:
  
  - macOS 12 and newer

## Next steps

[Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).

You can also configure device features on [iOS/iPadOS](ios-device-features-settings.md).
