---
title: Apple device feature settings in Microsoft Intune
description: See all the settings to configure iOS, iPadOS, and macOS devices for AirPrint, home screen layout, app notifications, shared devices, single sign-on, and web content filter settings in Microsoft Intune. Use these settings in a device configuration profile to configure iOS, iPadOS, and macOS devices to use these Apple features on your devices.
ms.date: 02/10/2026
ms.topic: reference
ms.reviewer: beflamm
ms.collection:
- M365-identity-device-management
zone_pivot_groups: platforms-apple
---

# Apple device feature settings in Microsoft Intune

> [!NOTE]
> [!INCLUDE [not-all-settings-are-documented](../includes/not-all-settings-are-documented.md)]

Intune has a built-in **Device Features** template profile for Apple devices. It includes built-in settings that admins can use to customize different Apple features on iOS/iPadOS and macOS devices. For example, you can add AirPrint printers, show notifications, use single sign-on authentication, and more.

As part of your mobile device management (MDM) solution, use these features to control and manage Apple features on your devices.

This article lists these settings and describes what each setting does. It also lists the steps to get the IP address, path, and port of AirPrint printers by using the Terminal app (emulator). For more information on the device features template, see [Add iOS/iPadOS or macOS device feature settings](device-features-configure.md).

These settings apply to different enrollment types, with some settings applying to all enrollment options. For more information on the different enrollment types, see [macOS enrollment](../enrollment/macos-enroll.md).

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]
:::column-end:::
:::column span="3":::
> This feature supports the following platforms:
>
> - iOS/iPadOS
> - macOS
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [rbac](../../includes/requirements/rbac.md)]
:::column-end:::
:::column span="3":::
> - [!INCLUDE [minimum-rbac-role-policy-profile-manager](../includes/minimum-rbac-role-policy-profile-manager.md)]
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [device-configuration](../../includes/requirements/device-configuration.md)]
:::column-end:::
:::column span="3":::
> - Create a [device features configuration profile](device-features-configure.md).
:::column-end:::
:::row-end:::

## AirPrint

### Settings apply to: All enrollment types

> [!NOTE]
> Add all printers to the same profile. Apple prevents multiple AirPrint profiles from targeting the same device.

- **IP address**: Enter the IPv4 or IPv6 address of the printer. If you use hostnames to identify printers, you can get the IP address by pinging the printer in the terminal. [Get the IP address and path](#get-server-ip-address-resource-path-and-port) (in this article) provides more details.
- **Resource path**: The path is typically `ipp/print` for printers on your network. [Get the IP address and path](#get-server-ip-address-resource-path-and-port) (in this article) provides more details.
- **Port**: Enter the listening port of the AirPrint destination. If you leave this property blank, AirPrint uses the default port.

  This setting applies to:

  - iOS 11.0+
  - iPadOS 13.0+

- **Force TLS**: **Disable** (default) doesn't secure AirPrint connections with TLS. **Enable** secures AirPrint connections with Transport Layer Security (TLS).

  This setting applies to:

  - iOS 11.0+
  - iPadOS 13.0+

To add AirPrint servers, you can:

- Enter printer details to add an AirPrint destination to the list. You can add many AirPrint servers.
- **Import** a comma-separated file (.csv) with this information. Or, **Export** to create a list of the AirPrint servers you added.

### Get server IP address, resource path, and port

To add AirPrinter servers, you need the IP address of the printer, the resource path, and the port. The following steps show you how to get this information.

1. On a Mac that connects to the same local network (subnet) as the AirPrint printers, open the **Terminal** app (from **/Applications/Utilities**).
2. In the Terminal app, enter `ippfind`, and select enter.

    Note the printer information. For example, it can return something like `ipp://myprinter.local.:631/ipp/port1`. The first part is the name of the printer. The last part (`ipp/port1`) is the resource path.

3. In the Terminal app, enter `ping myprinter.local`, and select enter.

   Note the IP address. For example, it can return something like `PING myprinter.local (10.50.25.21)`.

4. Use the IP address and resource path values. In this example, the IP address is `10.50.25.21`, and the resource path is `/ipp/port1`.

::: zone pivot="ios-ipados"

## Home screen layout

This feature applies to:

- iOS 9.3 or newer
- iPadOS 13.0 and newer
- Automated device enrollment (supervised)

### What you need to know

- Add an app only once to the dock, page, folder on a page, or folder in the dock. If you add the same app in any two places, the app doesn't show on devices, and reporting errors can occur.

  For example, if you add the camera app to a dock and a page, the camera app isn't shown, and reporting might show an error for the policy. To add the camera app to the home screen layout, choose only the dock or a page, not both.

- When you apply a home screen layout, it overwrites any user-defined layout. So, we recommend you use home screen layouts on userless devices.

- You can have preexisting apps installed on the device that aren't included in the home screen layout configuration. These apps are shown in alphabetical order after the configured apps.

- When you use the Home Screen grid settings to add pages, or add pages and apps to the dock, the icons on the Home Screen and pages are locked. You can't move or delete them. This behavior might be by design with iOS/iPadOS and Apple's MDM policies.

- iOS/iPadOS web clips that are required to open in a managed browser don't appear in the order that you enter in the Home Screen layout policy.

### Home screen

Use this feature to add apps. You can see how these apps look on pages, the dock, and within folders. It also shows you the app icons. Volume Purchase Program (VPP) apps, line-of-business apps, and web link apps (web app URLs) are populated from the [client apps you add](../apps/apps-add.md).

- **Grid size**: Choose an appropriate grid size for the device's home screen. An app or folder takes up one place in the grid. If the target device doesn't support the selected size, some apps might not fit and are pushed to the next available position on a new page. For reference:

  - iPhone 5 supports 4 columns x 5 rows
  - iPhone 6 and later support 4 columns x 6 rows
  - iPads support 5 columns x 6 rows

- **+**: Select the add button to add apps.

- **Create folder or add apps**: Add an **App** or a **Folder**:

  - **App**: Select existing apps from the list. This option adds apps to the home screen on devices. If you don't have any apps, then [Add apps to Intune](../apps/apps-add.md).

    You can also search for apps by the app name, like `authenticator` or `drive`. Or, search by the app publisher, like `Microsoft` or `Apple`.

  - **Folder**: Adds a folder to the home screen. Enter the **Folder name**, and select existing apps from the list to go in the folder. This folder name is shown to users on their devices.

    You can also search for apps by the app name, like `authenticator` or `drive`. Or, search by the app publisher, like `Microsoft` or `Apple`.

    Apps are arranged from left to right, and in the same order as shown. Apps can be moved to other positions. You can only have one page in a folder. As a work-around, add nine (9) or more apps to the folder. Apps are automatically moved to the next page. You can add any combination of VPP apps, web links (web apps), store apps, line-of-business apps, and system apps.

### Dock

Add up to four (4) items for iPhones, and up to six (6) items for iPads (apps and folders combined) to the dock on the screen. Many devices support fewer items. For example, iPhone devices support up to four items. So, only the first four items you add are shown.

- **+**: Select the add button to add apps or folders to the dock.
- **Create folder or add apps**: Add an **App** or a **Folder**:

  - **App**: Select existing apps from the list. This option adds apps to the dock on the screen. If you don't have any apps, then [Add apps to Intune](../apps/apps-add.md).

    You can also search for apps by the app name, like `authenticator` or `drive`. Or, search by the app publisher, like `Microsoft` or `Apple`.

  - **Folder**: Adds a folder to the dock on the screen. Enter the **Folder name**, and select existing apps from the list to go in the folder. This folder name is shown to users on their devices.

    You can also search for apps by the app name, like `authenticator` or `drive`. Or, search by the app publisher, like `Microsoft` or `Apple`.

    Apps are arranged from left to right, and in the same order as shown. You can move apps to other positions. If you add more apps than can fit on a page, the apps are automatically moved to another page. You can add up to 20 pages in a folder on the dock. You can add any combination of VPP apps, web links (web apps), store apps, line-of-business apps, and system apps.

### Example

In the following example, the dock screen shows the Safari, Mail, and Stocks apps. The Stocks app is selected to show its properties:

:::image type="content" source="./media/device-features-apple/dock-screen-stocks-app.png" alt-text="Sample iOS/iPadOS Home screen layout dock settings in Microsoft Intune":::

When you assign the policy to an iPhone, the dock looks similar to the following image:

:::image type="content" source="./media/device-features-apple/safari-mail-stocks-apps-ios-dock.png" alt-text="Sample iOS/iPadOS dock layout on an iPhone device":::

::: zone-end

::: zone pivot="ios-ipados"

## App notifications

### Settings apply to: Automated device enrollment (supervised)

**Add**: Add notifications for apps:

:::image type="content" source="./media/device-features-apple/ios-ipados-app-notifications.png" alt-text="Add app notification in iOS/iPadOS device features configuration profile in Microsoft Intune":::

- **App bundle ID**: Enter the **App Bundle ID** of the app you want to add.

  To get the app bundle ID:

  - For some examples, see [Bundle IDs for built-in iOS/iPadOS apps](bundle-ids-built-in-ios-apps.md).
  - For apps added to Intune, [you can use the Intune admin center](../apps/get-app-bundle-id-intune-admin-center.md).

  When set to **Not configured** or left blank, Intune doesn't change or update this setting.
- **App name**: Enter the name of the app you want to add. This name is used for your reference in the Microsoft Intune admin center. It *isn't* shown on devices. When set to **Not configured** or left blank, Intune doesn't change or update this setting.
- **Publisher**: Enter the publisher of the app you're adding. This name is used for your reference in the Microsoft Intune admin center. It *isn't* shown on devices. When set to **Not configured** or left blank, Intune doesn't change or update this setting.
- **Notifications**: **Enable** or **Disable** the app from sending notifications to devices. When set to **Not configured** (default), Intune doesn't change or update this setting.

  When set to **Enable**, also configure:

  - **Show in notifications center**: **Enable** allows the app to show notifications in the device Notification Center. **Disable** prevents the app from showing notifications in the Notification Center. When set to **Not configured** or left blank, Intune doesn't change or update this setting.
  - **Show on Lock Screen**: **Enable** shows app notifications on the device lock screen. **Disable** prevents the app from showing notifications on the lock screen. When set to **Not configured** or left blank, Intune doesn't change or update this setting.
  - **Alert type**: When devices are unlocked, choose how the notification is shown. Your options:
    - **None**: No notification is shown.
    - **Banner**: A banner is briefly shown with the notification. This setting might also be known as Temporary Banner.
    - **Modal**: The notification is shown and users must manually dismiss it before continuing to use the device. This setting might also be known as Persistent Banner.
  - **Badge on app icon**: **Enable** adds a badge to the app icon. The badge means the app sent a notification. **Disable** doesn't add a badge to the app icon. When set to **Not configured**, Intune doesn't change or update this setting.
  - **Enable sounds**: **Enable** plays a sound when a notification is delivered. **Disable** doesn't play a sound when a notification is delivered. When set to **Not configured**, Intune doesn't change or update this setting.
  - **Show previews**: Shows a preview of recent app notifications. Select when to show the preview. The value you choose overrides the user configured value on the device (Settings > Notifications > Show Previews). Your options:
    - **Not configured**: Intune doesn't change or update this setting.
    - **When unlocked**: The preview only shows when the device is unlocked.
    - **Always**: The preview always shows on the lock screen.
    - **Never**: The preview never shows.

    This setting applies to:

    - iOS/iPadOS 14.0 and newer

::: zone-end

::: zone pivot="macos"

## Associated domains

In Intune, you can:

- Add many app-to-domain associations.
- Associate many domains with the same app.

This setting applies to:

- macOS 10.15 and newer

### Settings apply to: User approved device enrollment, and Automated device enrollment

These settings use the [AssociatedDomains.ConfigurationItem payload](https://developer.apple.com/documentation/devicemanagement/associateddomains/configurationitem) (opens Apple's web site).

- **Associated domains**: **Add** an association between your domain and an app. This setting shares sign on credentials between a Contoso app and a Contoso website. Also enter:

  - **App ID**: Enter the app identifier of the app to associate with a website. The app identifier includes the team ID and a bundle ID: `TeamID.BundleID`.

    The team ID is a 10-character alphanumerical (letters and numbers) string generated by Apple for your app developers, like `ABCDE12345`. [Locate your Team ID](https://help.apple.com/developer-account/#/dev55c3c710c) (opens Apple's web site) has more information.

    The bundle ID uniquely identifies the app, and typically is formatted in reverse domain name notation. For example, the bundle ID of Finder is `com.apple.finder`.

    To get the bundle ID:

    - Open the Terminal app and use AppleScript: `osascript -e 'id of app "ExampleApp"'`
    - For apps added to Intune, [you can use the Intune admin center](../apps/get-app-bundle-id-intune-admin-center.md).

  - **Domains**: Enter the website domain to associate with an app. The domain includes a service type and fully qualified hostname, like `webcredentials:www.contoso.com`.

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

::: zone-end

::: zone pivot="macos"

## Content caching

Content caching saves a local copy of content. Other Apple devices can get this information without connecting to the Internet. This caching accelerates downloads by saving software updates, apps, photos, and other content the first time they're downloaded. Since apps are downloaded once and shared to other devices, schools and organizations with many devices save bandwidth.

> [!NOTE]
> Use only one profile for these settings. If you assign multiple profiles with these settings, an error occurs.
>
> For more information on monitoring content caching, see [View content caching logs and statistics](https://support.apple.com/guide/mac-help/view-content-caching-logs-statistics-mac-mchl0d8533cd/10.15/mac/10.15) (opens Apple's web site).

This setting applies to:

- macOS 10.13.4 and newer

### Settings apply to: All enrollment types

For more information on these settings, see [Content Caching payload settings](https://support.apple.com/guide/deployment/content-caching-payload-settings-dep163612d39/web) (opens Apple's web site).

**Enable content caching**: **Yes** turns on content caching, and users can't disable it. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might turn it off.

- **Type of content to cache**: Your options:
  - **All content**: Caches iCloud content and shared content.
  - **User content only**: Caches user's iCloud content, including photos and documents.
  - **Shared content only**: Caches apps and software updates.

- **Maximum cache size**: Enter the maximum amount of disk space (in bytes) that's used to cache content. When left blank (default), Intune doesn't change or update this setting. By default, the OS might set this value to zero (`0`) bytes, which gives unlimited disk space to the cache.

  Be sure you don't exceed the space available on the devices. For more information on device storage capacity, see [How iOS and macOS report storage capacity](https://support.apple.com/HT201402) (opens Apple's web site).

- **Cache location**: Enter the path to store the cached content. The default location is `/Library/Application Support/Apple/AssetCache/Data`. Don't change this location.

  If you change this setting, your cached content isn't moved to the new location. To move it automatically, users need to change the location on the device (**System Preferences** > **Sharing** > **Content Caching**).

- **Port**: Enter the TCP port number on devices for the cache to accept download and upload requests, from 0-65535. Enter zero (`0`) (default) to use whatever port is available.
- **Block internet connection and cache content sharing**: Also known as tethered caching. **Yes** prevents Internet connection sharing, and prevents sharing cached content with iOS/iPadOS devices USB-connected to their Mac. Users can't enable this setting. When set to **Not configured** (default), Intune doesn't change or update this setting.

- **Enable internet connection sharing**: Also known as tethered caching. **Yes** allows Internet connection sharing, and allows sharing cached content with iOS/iPadOS devices USB-connected to their Mac. Users can't disable this setting. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might turn this off.

  This setting applies to:

  - macOS 10.15.4 and newer

- **Enable cache to log client details**: **Yes** logs the IP address and port number of the devices that request content. If you're troubleshooting device issues, this log file can help. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not log this information.

- **Always keep content from the cache, even when the system needs disk space for other apps**: **Yes** keeps the cache content, and makes sure nothing is deleted, even when disk space is low. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might purge content from the cache automatically when it needs storage space for other apps.

  This setting applies to:

  - macOS 10.15 and newer

- **Show status alerts**: **Yes** shows alerts as system notifications. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not show these alerts as system notifications.

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

  When a requested item isn't available on one content cache, it checks its peers for the item. If the item is available, it's downloaded from the content cache on the peer device. If it's still not available, the content cache downloads the item from:

  - A parent IP address, if you configure one

    OR,

  - From Apple using the Internet

  When more than one content cache is available, devices automatically select the right content cache.

  Your options:

  - **Not configured** (default): Intune doesn't change or update this setting.
  - **Content caches using the same local networks**: Content cache only peers with other content caches on the same immediate local network.
  - **Content caches using the same public IP address**: Content cache only peers with other content caches on the same public IP address.
  - **Content caches using custom local networks**: Content cache only peers with other content caches in the IP address listen range you enter:

    - **Peer listen ranges**: Enter the IPv4 or IPv6 start and ending IP addresses for your range. The content cache responds only to peer cache requests from content caches in the IP address ranges you enter.
    - **Peer filter ranges**: Enter the IPv4 or IPv6 start and ending IP addresses for your range. The content cache filters its list of peers using the IP address ranges you enter.

- **Parent IP addresses**: Enter the local IP address of another content cache to add as a parent cache. Your cache uploads and downloads content to these caches, instead of uploading or downloading directly from Apple. Only add a parent IP address once.
- **Parent selection policy**: When there are many parent caches, select how the parent IP address is chosen. Your options:
  - **Not configured** (default): Intune doesn't change or update this setting.
  - **Round robin**: Use the parent IP addresses in order. This option is good for load balancing scenarios.
  - **First available**: Always use the first available IP address in the list.
  - **Hash**: Creates a hash value for the path portion of the requested URL. This option makes sure the same parent IP address is always used for the same URL.
  - **Random**: Randomly use an IP address in the list. This option is good for load balancing scenarios.
  - **Sticky available**: Always use the first IP address in the list. If it's not available, then use the second IP address in the list. Continue to use the second IP address until it's not available, and so on.

::: zone-end

::: zone pivot="ios-ipados"

## Lock screen message

This feature applies to:

- iOS 9.3 and newer
- iPadOS 13.0 and newer

### Settings apply to: Automated device enrollment (supervised)

- **"If Lost, Return to..." Message**: If devices are lost or stolen, enter a note that might help get the device returned if found. You can enter any text you want. For example, enter something like `If found, call Contoso at ...`.

  The text you enter is shown on the sign in window and lock screen on devices.

- **Asset tag information**: Enter information about the asset tag of the device. For example, enter `Owned by Contoso Corp` or `Serial Number: {{serialnumber}}`.

  Use device tokens to add device-specific information to these fields. For example, to show the serial number, enter `Serial Number: {{serialnumber}}` or `Device ID: {{DEVICEID}}`. On the lock screen, the text shows similar to `Serial Number 123456789ABC`. When entering variables, be sure to use curly brackets `{{ }}`.

  The following device information variables are supported. The UI doesn't validate variables, and they're case sensitive. If you enter an incorrect variable, you see profiles saved with incorrect input. For example, if you enter `{{DeviceID}}` instead of `{{deviceid}}` or `{{DEVICEID}}`, the literal string shows instead of the device's unique ID. Be sure to enter the correct information. All lowercase or all uppercase variables are supported, but not a mix.

  - `{{AADDeviceId}}`: Microsoft Entra device ID
  - `{{AccountId}}`: Intune tenant ID or account ID
  - `{{AccountName}}`: Intune tenant name or account name
  - `{{AppleId}}`: Apple ID of the user
  - `{{Department}}`: Department assigned during Setup Assistant
  - `{{DeviceId}}`: Intune device ID
  - `{{DeviceName}}`: Intune device name
  - `{{domain}}`: Domain name
  - `{{EASID}}`: Exchange Active Sync ID
  - `{{EDUUserType}}`: Type of user
  - `{{IMEI}}`: IMEI of the device
  - `{{mail}}`: Email address of the user
  - `{{ManagedAppleId}}`: Managed Apple ID of the user
  - `{{MEID}}`: MEID of the device
  - `{{partialUPN}}`: UPN prefix before the @ symbol
  - `{{SearchableDeviceKey}}`: NGC Key ID
  - `{{SerialNumber}}`: Device serial number
  - `{{SerialNumberLast4Digits}}`: Last 4 digits of the device serial number
  - `{{SIGNEDDEVICEID}}`: Device ID blob assigned to client during Company Portal enrollment
  - `{{SignedDeviceIdWithUserId}}`: Device ID blob assigned to client with user-affinity during Apple Setup Assistant
  - `{{UDID}}`: Device UDID
  - `{{UDIDLast4Digits}}`: Last 4 digits of the device UDID
  - `{{UserId}}`: Intune user ID
  - `{{UserName}}`: User name
  - `{{userPrincipalName}}`: UPN of the user

::: zone-end

::: zone pivot="macos"

## Login items

### Settings apply to: All enrollment types

- **Add the files, folders, and custom apps that will launch at login**: **Add** the path of a file, folder, custom app, or system app that opens when users sign in to their devices. Also enter:

  - **Path of item**: Enter the path to the file, folder, or app. System apps, or apps built or customized for your organization are typically in the `Applications` folder, with a path similar to `/Applications/AppName.app`.

    You can add many files, folders, and apps. For example, enter:

    - `/Applications/Calculator.app`
    - `/Applications`
    - `/Applications/Microsoft Office/root/Office16/winword.exe`
    - `/Users/UserName/music/itunes.app`

    When adding any app, folder, or file, be sure to enter the correct path. Not all items are in the `Applications` folder. If users move an item from one location to another, then the path changes. This moved item isn't opened when the user signs in.

  - **Hide**: Choose to show or hide the app. Your options:
    - **Not configured** (default): Intune doesn't change or update this setting. By default, the OS might show items in the Users & Groups login items list with the hide option unchecked.
    - **Yes**: Hides the app in the Users & Groups login items list.

::: zone-end

::: zone pivot="macos"

## Login window

### Settings apply to: All enrollment types

#### Windows Layout

- **Show additional information in the menu bar**: When the time area on the menu bar is selected, **Yes** shows the host name and macOS version. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not show this information on the menu bar.
- **Banner**: Enter a message that's shows on the sign in screen on devices. For example, enter your organization information, a welcome message, lost and found information, and so on.
- **Require username and password text fields**: Choose how users sign in to devices. **Yes** requires users to enter a username and password. When set to **Not configured**, Intune doesn't change or update this setting. By default, the OS might require users to select their username from a list, and then type their password.

  When set to **Not configured**, also enter:

  - **Hide local users**: **Yes** hides the local user accounts in the user list, which can include the standard and admin accounts. Only the network and system user accounts are shown. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might show the local user accounts in the user list.
  - **Hide mobile accounts**: **Yes** hides mobile accounts in the user list. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might show the mobile accounts in the user list. Some mobile accounts can show as network users.
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

::: zone-end

::: zone pivot="ios-ipados"

## Single sign-on

### Settings apply to: Device enrollment, Automated device enrollment (supervised)

- **Microsoft Entra username attribute**: Intune looks for this attribute for each user in Microsoft Entra ID. Intune then populates the respective field, like the UPN, before generating the XML that gets installed on devices. Your options:

  - **Not configured**: Intune doesn't change or update this setting. By default, the OS prompts users for a Kerberos principal name when the profile is deployed to devices. A principal name is required for MDMs to install SSO profiles.
  - **User principal name**: The user principal name (UPN) is parsed in the following way:

    :::image type="content" source="./media/device-features-apple/user-name-attribute.png" alt-text="iOS/iPadOS Username SSO attribute in Microsoft Intune":::

    You can also overwrite the realm with the text you enter in the **Realm** text box.

    For example, Contoso has several regions, including Europe, Asia, and North America. Contoso wants their Asia users to use SSO, and the app requires the UPN in the `username@asia.contoso.com` format. When you select **User Principal Name**, the realm for each user is taken from Microsoft Entra ID, which is `contoso.com`. So for users in Asia, select **User Principal Name**, and enter `asia.contoso.com`. The user's UPN becomes `username@asia.contoso.com`, instead of `username@contoso.com`.

  - **Intune Device ID**: Intune automatically selects the Intune device ID. By default:

    - Apps only need to use the device ID. But if your app uses the realm and the device ID, enter the realm in the **Realm** text box.
    - If you use device ID, keep the realm empty.

  - **Azure AD Device ID**: The Microsoft Entra device ID
  - **SAM account name**: Intune populates the on-premises Security Accounts Manager (SAM) account name.

- **Realm**: Enter the domain part of the URL. For example, enter `contoso.com`.

- **URLs**: **Add** any URLs in your organization that require user single sign-on (SSO) authentication.

  For example, when a user connects to any of these sites, the iOS/iPadOS device uses the SSO credentials. Users don't need to enter credentials again. If multifactor authentication (MFA) is enabled, users are required to enter the second authentication.

  Also:

  - These URLs must be properly formatted FQDN. Apple requires the URLs be in the `http://<yourURL.domain>` format.

  - The URL matching patterns must begin with either `http://` or `https://`. A simple string match is run, so the `http://www.contoso.com/` URL prefix doesn't match `http://www.contoso.com:80/`. With iOS 10.0+ and iPadOS 13.0+, a single wildcard \* can be used to enter all matching values. For example, `http://*.contoso.com/` matches both `http://store.contoso.com/` and `http://www.contoso.com`.

    The `http://.com` and `https://.com` patterns match all HTTP and HTTPS URLs, respectively.

- **Apps**: **Add** apps on users devices that can use single sign-on.

  The `AppIdentifierMatches` array must include strings that match the app bundle IDs. These strings can be exact matches, like `com.contoso.myapp`, or enter a prefix match on the bundle ID using the `*` wildcard character. The wildcard character must appear after a period character (.), and can appear only once, at the end of the string, like `com.contoso.*`. When a wildcard is included, any app whose bundle ID begins with the prefix is granted access to the account.

  Use **App Name** to enter a user-friendly name to help you identify the bundle ID.

- **Credential renewal certificate**: If using certificates for authentication (not passwords), select the existing [SCEP](../protect/certificates-profile-scep.md) or [PFX](../protect/certificates-pfx-configure.md) certificate as the authentication certificate. Typically, this certificate is the same certificate that's deployed to users for other profiles, like VPN, Wi-Fi, or email.

::: zone-end

::: zone pivot="ios-ipados"

## Web content filter

### Settings apply to: Automated device enrollment (supervised)

These settings use Apple's Web Content Filter settings. For more information on these settings, go to [Apple's Platform Deployment site](https://support.apple.com/guide/deployment/web-content-filter-payload-settings-depc77c9609/web) (opens Apple's web site).

**Filter Type**: Choose to allow specific websites. Your options:

- **Not configured**: Intune doesn't change or update this setting.

- **Configure URLs**: Use Apple's built-in web filter that looks for adult terms, including profanity and sexually explicit language. This setting evaluates each web page as it loads, and identifies and blocks unsuitable content. You can also add URLs that you don't want checked by the filter. Or, block specific URLs, regardless of Apple's filter settings.

  - **Permitted URLs**: **Add** the URLs you want to allow. These URLs bypass Apple's web filter.

    The URLs you enter are the URLs you don't want evaluated by the Apple web filter. These URLs aren't a list of allowed websites. To create a list of allowed websites, set the **Filter Type** to **Specific websites only**.

  - **Blocked URLs**: **Add** the URLs you want to stop from opening, regardless of the Apple web filter settings.

- **Specific websites only** (for Safari web browser only): These URLs are added to the Safari browser's bookmarks. Users are **only** allowed to visit these sites; no other sites can be opened. Use this option only if you know the exact list of URLs that users can access.

  - **URL**: Enter the URL of the website you want to allow. For example, enter `https://www.contoso.com`.
  - **Bookmark Path**: Apple changed this setting. All bookmarks go into the **Allowed Sites** folder. Bookmarks don't go into the bookmark path you enter.
  - **Title**: Enter a descriptive title for the bookmark.

  If you don't enter any URLs, then users can't access any websites except for `microsoft.com`, `microsoft.net`, and `apple.com`. Intune automatically allows these URLs.

::: zone-end

## Single sign-on app extension

::: zone pivot="ios-ipados"

This feature applies to:

- iOS 13.0 and newer
- iPadOS 13.0 and newer

### Settings apply to: All enrollment types

::: zone-end

::: zone pivot="macos"

This feature applies to:

- macOS 10.15 and newer

> [!NOTE]
> On macOS devices, Microsoft recommends you use Platform SSO to enable single sign-on (SSO). For more information, go to [Configure Platform SSO for macOS devices in Microsoft Intune](platform-sso-macos.md).

### Settings apply to: User approved device enrollment, and Automated device enrollment

::: zone-end

**SSO app extension type**: Choose the type of SSO app extension. Your options:

#### Not configured

Intune doesn't change or update this setting. By default, the OS doesn't use app extensions. To disable an app extension, change the SSO app extension type to **Not configured**.

#### Microsoft Entra ID SSO app extension type

Uses the Microsoft Entra ID Enterprise SSO plug-in, which is a redirect-type SSO app extension. This plug-in provides SSO for on-premises Active Directory accounts across all applications that support [Apple's Enterprise single sign-on](https://developer.apple.com/documentation/authenticationservices) feature. Use this SSO app extension type to enable SSO on Microsoft apps, organization apps, and websites that authenticate using Microsoft Entra ID. The SSO plug-in acts as an advanced authentication broker that offers security and user experience improvements.

::: zone pivot="ios-ipados"

All apps that use the Microsoft Authenticator app for authentication continue to get SSO with the [Microsoft Enterprise SSO plug-in for Apple devices](/entra/identity-platform/apple-sso-plugin). For more information, see [Use the Microsoft Enterprise SSO plug-in on iOS/iPadOS devices](use-enterprise-sso-plug-in-ios-ipados-with-intune.md).

> [!IMPORTANT]
> To achieve SSO with the Microsoft Entra SSO app extension type, first install the iOS/iPadOS Microsoft Authenticator app on devices. The Authenticator app delivers the Microsoft Enterprise SSO plug-in to devices, and the MDM SSO app extension settings activate the plug-in. Once Authenticator and the SSO app extension profile are installed on devices, users must enter their credentials to sign in, and establish a session on their devices. This session is then used across different applications without requiring users to authenticate again. For more information about Authenticator, go to [What is the Microsoft Authenticator app](/azure/active-directory/user-help/user-help-auth-app-overview).

::: zone-end

::: zone pivot="macos"

For more information, go to [Use the Microsoft Enterprise SSO plug-in on macOSOS devices](use-enterprise-sso-plug-in-macos-with-intune.md).

> [!IMPORTANT]
> To achieve SSO with the Microsoft Entra SSO app extension type, install the macOS Company Portal app on devices. The Company Portal app delivers the Microsoft Enterprise SSO plug-in to devices. The MDM SSO app extension settings activate the plug-in. After the Company Portal app and the SSO app extension profile are installed on devices, users sign in with their credentials, and create a session on their devices. This session is used across different applications without requiring users to authenticate again.
>
> For more information about the Company Portal app, go to [What happens if you install the Company Portal app and enroll your macOS device in Intune](../user-help/what-happens-if-you-install-the-Company-Portal-app-and-enroll-your-device-in-intune-macos.md).
>
> You can also [download the Company Portal app](https://go.microsoft.com/fwlink/?linkid=853070).

::: zone-end

::: zone pivot="ios-ipados"

- **Enable shared device mode**: Choose **Yes** if you're deploying the Microsoft Enterprise SSO plug-in to iOS/iPadOS devices configured for Microsoft Entra shared device mode feature. Devices in shared mode allow many users to globally sign in and out of applications that support shared device mode. When set to **Not configured**, Intune doesn't change or update this setting. By default, iOS/iPadOS devices aren't intended to be shared among multiple users.

  For more information about shared device mode and how to enable it, see [Overview of shared device mode](/entra/identity-platform/msal-shared-devices).

  This setting applies to:

  - iOS/iPadOS 13.5 and newer

::: zone-end

- **App bundle IDs**: Enter the bundle IDs of any other apps that should get single sign-on through an extension on your devices. To get the bundle ID of an app added to Intune, [you can use the Intune admin center](../apps/get-app-bundle-id-intune-admin-center.md).

  - These apps use the Microsoft Enterprise SSO plug-in to authenticate the user without requiring a sign-in.
  - The app bundle IDs you enter have permission to use the Microsoft Entra SSO app extension if they don't use any Microsoft libraries, like Microsoft Authentication Library (MSAL).

    The experience for these apps might not be as seamless compared to the Microsoft libraries. Older apps that use MSAL authentication, or apps that don't use the newest Microsoft libraries, must be added to this list to work properly with the Microsoft Azure SSO app extension.

- **Additional configuration**: Enter more extension-specific data to pass to the SSO app extension:
  - **Key**: Enter the name of the item you want to add, like `user name` or `AppAllowList`.
  - **Type**: Enter the type of data. Your options:

    - String
    - Boolean: In **Configuration value**, enter `True` or `False`.
    - Integer: In **Configuration value**, enter a number.

  - **Value**: Enter the data.

#### Redirect SSO app extension type

Use a generic, customizable redirect app extension to use SSO with modern authentication flows.

- **Extension ID**: Enter the bundle identifier that identifies your SSO app extension, like `com.apple.extensiblesso`.
- **Team ID**: Enter the team identifier of your SSO app extension. A team identifier is a 10-character alphanumerical (numbers and letters) string generated by Apple, like `ABCDE12345`.

  [Locate your Team ID](https://help.apple.com/developer-account/#/dev55c3c710c) (opens Apple's website) has more information.

- **URLs**: Enter the URLs where your identity provider can be reached. When a user is redirected to these URLs, the SSO app extension intervenes and prompts for SSO. Each URL must be unique and can't already exist in another profile. Must use HTTP or HTTPS protocols.

  For example, when a user connects to any of these sites, the device uses the SSO credentials. Users don't need to enter credentials again. If multifactor authentication (MFA) is enabled, users are required to enter the second authentication.

  Also:

  - These URLs must be properly formatted FQDN. Apple requires the URLs be in the `http://<yourURL.domain>` format.
  - All the URLs in your Intune single sign-on app extension profiles must be unique. You can't repeat a domain in any SSO app extension profile, even if you're using different types of SSO app extensions.
  - The URLs must begin with `http://.com` or `https://.com`. A simple string match is run, so the `http://www.contoso.com/` URL prefix doesn't match `http://www.contoso.com:80/`.

  ::: zone pivot="ios-ipados"

  With iOS 10.0+ and iPadOS 13.0+, a single wildcard \* can be used to enter all matching values. For example, `http://*.contoso.com/` matches both `http://store.contoso.com/` and `http://www.contoso.com`.

  ::: zone-end

- **Additional configuration**: Enter more extension-specific data to pass to the SSO app extension:
  - **Key**: Enter the name of the item you want to add, like `user name` or `AppAllowList`.
  - **Type**: Enter the type of data. Your options:

    - String
    - Boolean: In **Configuration value**, enter `True` or `False`.
    - Integer: In **Configuration value**, enter a number.

  - **Value**: Enter the data.

#### Credential SSO app extension type

Use a generic, customizable credential app extension to use SSO with challenge-and-response authentication flows.

- **Extension ID**: Enter the bundle identifier that identifies your SSO app extension, like `com.apple.extensiblesso`.
- **Team ID**: Enter the team identifier of your SSO app extension. A team identifier is a 10-character alphanumerical (numbers and letters) string generated by Apple, like `ABCDE12345`.

  [Locate your Team ID](https://help.apple.com/developer-account/#/dev55c3c710c) (opens Apple's website) has more information.

- **Realm**: Enter the name of your authentication realm. The realm name should be capitalized, like `CONTOSO.COM`. Typically, your realm name is the same as your DNS domain name, but in all uppercase.

- **Domains**: Enter the domain or host names of the sites that can authenticate through SSO. For example, if your website is `mysite.contoso.com`, then `mysite` is the host name, and `.contoso.com` is the domain name. When users connect to any of these sites, the app extension handles the authentication challenge. This authentication allows users to use Face ID, Touch ID, or Apple pincode/passcode to sign in.

  - All the domains in your single sign-on app extension Intune profiles must be unique. You can't repeat a domain in any sign-on app extension profile, even if you're using different types of SSO app extensions.
  - These domains aren't case-sensitive.
  - The domain must begin with a period (`.`).

- **Additional configuration**: Enter more extension-specific data to pass to the SSO app extension:
  - **Key**: Enter the name of the item you want to add, like `user name` or `AppAllowList`.
  - **Type**: Enter the type of data. Your options:

    - String
    - Boolean: In **Configuration value**, enter `True` or `False`.
    - Integer: In **Configuration value**, enter a number.

  - **Value**: Enter the data.

#### Kerberos SSO app extension type

Use Apple's built-in Kerberos extension, which is a Kerberos-specific version of the **Credential** app extension.

The Kerberos extension is included in:

::: zone pivot="ios-ipados"

- iOS 13.0+ and iPadOS 13.0+

After users successfully sign in to the Authenticator app, they aren't prompted to sign in to other apps that use the SSO extension. The first time users open managed apps that don't use the SSO extension, the users are prompted to select the account that's signed in.

::: zone-end

::: zone pivot="macos"

- macOS Catalina 10.15 and newer

::: zone-end

> [!TIP]
> With the **Redirect** and **Credential** types, you add your own configuration values to pass through the extension. If you're using **Credential**, consider using built-in configuration settings provided by Apple in the **Kerberos** type.

- **Realm**: Enter the name of your authentication realm. The realm name should be capitalized, like `CONTOSO.COM`. Typically, your realm name is the same as your DNS domain name, but in all uppercase.

- **Domains**: Enter the domain or host names of the sites that can authenticate through SSO. For example, if your website is `mysite.contoso.com`, then `mysite` is the host name, and `.contoso.com` is the domain name. When users connect to any of these sites, the app extension handles the authentication challenge. This authentication allows users to use Face ID, Touch ID, or Apple pincode/passcode to sign in.

  - All the domains in your single sign-on app extension Intune profiles must be unique. You can't repeat a domain in any sign-on app extension profile, even if you're using different types of SSO app extensions.
  - These domains aren't case-sensitive.
  - The domain must begin with a period (`.`).

- **Block keychain usage**: **Yes** prevents passwords from being saved and stored in the keychain. If blocked, users aren't prompted to save their password, and need to reenter the password when the Kerberos ticket expires. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow passwords to be saved and stored in the keychain. Users aren't prompted to reenter their password when the ticket expires.
- **Require Face ID, Touch ID, or passcode**: **Yes** forces users to enter their Face ID, Touch ID, or device passcode when the credential is needed to refresh the Kerberos ticket. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not require users to use biometrics or device passcode to refresh the Kerberos ticket. If **Block keychain usage** is set to **Yes**, then this setting doesn't apply.
- **Set as default realm**: **Yes** sets the **Realm** value you entered as the default realm. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not set a default realm.

  - If you're configuring multiple Kerberos SSO app extensions in your organization, select **Yes**.
  - If you're using multiple realms, select **Yes**. It sets the **Realm** value you entered as the default realm.
  - If you only have one realm, select **Not configured** (default).

- **Block Autodiscover**: **Yes** prevents the Kerberos extension from automatically using LDAP and DNS to determine its Active Directory site name. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow the extension to automatically find the Active Directory site name.

- **Allow only managed apps**: When set to **Yes**, the Kerberos extension allows only managed apps, and any apps entered with the app bundle ID to access the credential. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow nonmanaged apps to access the credential.

  This setting applies to:

  ::: zone pivot="ios-ipados"

  - iOS/iPadOS 14 and newer

  ::: zone-end
  
  ::: zone pivot="macos"

  - macOS 12 and newer

  ::: zone-end

::: zone pivot="macos"

- **Block password changes**: **Yes** prevents users from changing the passwords they use to sign in to the domains you entered. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might allow password changes.
- **Enable local password sync**: Choose **Yes** to sync your users' local passwords to Microsoft Entra ID. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might disable password sync to Microsoft Entra ID.

  Use this setting as an alternative or backup to SSO. This setting doesn't work if users are signed in with an Apple mobile account.

- **Delay Kerberos extension setup**: When set to **Yes**, the user isn't prompted to set up the Kerberos extension until the extension is enabled by the admin, or a Kerberos challenge is received. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might immediately prompt the user to set up the Kerberos extension.

  This setting applies to:

  - macOS 11 and newer

- **Allow standard Kerberos utilities**: When set to **Yes**, the Kerberos extension allows any apps entered with the app bundle ID, managed apps, and standard Kerberos utilities, like TicketViewer and klist, to access and use the credential. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not allow listed apps to access and use the credential.

  This setting applies to:

  - macOS 12 and newer

- **Request credential**: When set to **Yes**, the credential is requested on the next matching Kerberos challenge or network state change. When the credential is expired or missing, a new credential is created. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not request a new credential.

  This setting applies to:

  - macOS 12 and newer

- **Require LDAP connections for TLS**: When set to **Yes**, LDAP connections are required to use Transport Layer Security (TLS). When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not require LDAP connections to use TLS.

  This setting applies to:

  - macOS 11 and newer

- **Require Active Directory password complexity**: Choose **Yes** to force user passwords to meet Active Directory's password complexity requirements. On devices, this setting shows a pop-up window with check boxes so users see they're completing the password requirements. It helps users know what they need to enter for the password. For more information, go to [Password must meet complexity requirements](/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements). When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not require users to meet Active Directory's password requirement.
- **Minimum password length**: Enter the minimum number of characters that can make up users passwords. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not enforce a minimum password length on the users.
- **Password reuse limit**: Enter the number of new passwords, from 1-24, that are used until a previous password can be reused on the domain. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not enforce a password reuse limit.
- **Minimum password age (days)**: Enter the number of days that a password is used on the domain before users can change it. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might not enforce a minimum age of passwords before they can be changed.
- **Password expiration notification (days)**: Enter the number of days before a password expires that users get notified that their password will expire. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might use `15` days.
- **Password expiration (days)**: Enter the number of days before the device password must change. When set to **Not configured** (default), Intune doesn't change or update this setting. By default, the OS might never expire passwords.
- **Password change URL**: Enter the URL that opens when users start a password change.
- **Custom user name**: Enter the text that replaces the user name shown in the extension. You can enter a name that matches the name of your company or organization. For example, you can enter `Contoso`.

  This setting applies to:

  - macOS 11 and newer

- **Kerberos extension use**: Select how other processes use the Kerberos Extension credential. Your options:
  - **Always**: The extension credential is always used if the SPN is listed in **Domains**. It isn't used if the calling app isn't listed in **App Bundle IDs**.
  - **When not specified**: The extension credential is only used when another credential isn't entered by the caller, and the SPN is listed in Domains. It's not used if the calling app isn't listed in **App Bundle IDs**.
  - **Kerberos default**: Intune doesn't change or update this setting. By default, the OS uses the default Kerberos processes for selecting credentials. This option is the same as not configuring this setting.

  This setting applies to:

  - macOS 11 and newer

  ::: zone-end

- **Principal name**: Enter the username of the Kerberos principal. You don't need to include the realm name. For example, in `user@contoso.com`, `user` is the principal name, and `contoso.com` is the realm name.

  - You can also use variables in the principal name by entering curly brackets `{{ }}`. For example, to show the username, enter `Username: {{username}}`.
  - Be careful with variable substitution. Variables aren't validated in the UI and they're case sensitive. Be sure to enter the correct information.

- **Active Directory site code**: Enter the name of the Active Directory site that the Kerberos extension should use. You might not need to change this value, as the Kerberos extension can automatically find the Active Directory site code.
- **Cache name**: Enter the Generic Security Services (GSS) name of the Kerberos cache. You most likely don't need to set this value.
- **Sign in window text**: Enter the text shown to users at the Kerberos sign in window.

  This setting applies to:

  ::: zone pivot="ios-ipados"

  - iOS/iPadOS 14 and newer

  ::: zone-end

  ::: zone pivot="macos"

  - macOS 11 and newer

  ::: zone-end

::: zone pivot="macos"

- **Password requirements message**: Enter a text version of your organization's password requirements that's shown to users. The message shows if you don't require Active Directory's password complexity requirements, or don't enter a minimum password length.

  When set to **Yes**, all existing user accounts are wiped from the devices. To avoid data loss, or prevent a factory reset, make sure you understand how this setting changes your devices.

  For more information about shared device mode, go to [Overview of shared device mode](/azure/active-directory/develop/msal-shared-devices).

::: zone-end

- **App bundle IDs**: Enter the bundle IDs of any other apps that should get single sign-on through an extension on your devices. To get the bundle ID of an app added to Intune, [you can use the Intune admin center](../apps/get-app-bundle-id-intune-admin-center.md).

  If you use the **Kerberos SSO app extension** type, then these apps:

  - Have access to the Kerberos Ticket Granting Ticket
  - Have access to the authentication ticket
  - Authenticate users to services they're authorized to access

- **Domain realm mapping**: Enter the domain DNS suffixes that should map to your realm. Use this setting when the DNS names of the hosts don't match the realm name. You most likely don't need to create this custom domain-to-realm mapping.

- **PKINIT certificate**: **Select** the Public Key Cryptography for Initial Authentication (PKINIT) certificate that can be used for Kerberos authentication. You can choose from [PKCS](../protect/certificates-pfx-configure.md) or [SCEP](../protect/certificates-scep-configure.md) certificates that you added in Intune.

  For more information about certificates, go to [Use certificates for authentication in Microsoft Intune](../protect/certificates-configure.md).

::: zone pivot="macos"

- **Preferred KDCs**: Enter the Key Distribution Centers (KDCs) to use for Kerberos traffic in order of preference. This list is used when the servers aren't discoverable using DNS. When the servers are discoverable, the list is used for both connectivity checks, and used first for Kerberos traffic. If the servers don't respond, then the device uses DNS discovery.

  This setting applies to:

  - macOS 12 and newer

::: zone-end

::: zone pivot="ios-ipados"

## Wallpaper

You might see unexpected behavior when you assign a profile with no image to devices that already have an existing image. For example, you create a profile without an image and assign it to devices that already have an image. In this scenario, the image can change to the device default, or the original image can stay on the device. Apple's MDM platform controls and limits this behavior.

### Settings apply to: Automated device enrollment (supervised)

- **Wallpaper Display Location**: Choose a location on devices that shows the image. Your options:
  - **Not configured**: Intune doesn't change or update this setting. A custom image isn't added to devices. By default, the OS might set its own image.
  - **Lock screen**: Adds the image to the lock screen.
  - **Home screen**: Adds the image to the home screen.
  - **Lock screen and Home screen**: Uses the same image on the lock screen and home screen.
- **Wallpaper Image**: Upload an existing .png, .jpg, or .jpeg image you want to use. Make sure the file size is less than 750 KB. You can also **remove** an image that you added.

> [!TIP]
>
> - When you configure a wallpaper policy, Microsoft recommends enabling the [Block modification of Wallpaper](device-restrictions-apple.md) setting. This setting prevents users from changing the wallpaper.
> - To display different images on the lock screen and home screen, create a profile with the lock screen image. Create another profile with the home screen image. Assign both profiles to your iOS/iPadOS user or device groups.

::: zone-end

## Related articles

- [Assign the profile](device-profile-assign.md) and [monitor its status](device-profile-monitor.md).
- Learn more about the [device feature configuration profile template](device-features-configure.md).
