---
title: Create configuration items for Windows
titleSuffix: Configuration Manager
description: Create configuration items to manage settings for Windows 10 computers with on-premises mobile device management (MDM) in Configuration Manager.
ms.date: 01/14/2020
ms.subservice: mdm
ms.service: configuration-manager
ms.topic: conceptual
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Create configuration items for Windows devices with on-premises MDM in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Use the Configuration Manager **Windows 8.1 and Windows 10** configuration item to manage settings for Windows devices that you manage with on-premises mobile device management (MDM).

For more general information on compliance settings in Configuration Manager, see the following articles:

- [Get started with compliance settings](../../compliance/get-started/get-started-with-compliance-settings.md)

- [Plan for and configure compliance settings](../../compliance/plan-design/plan-for-and-configure-compliance-settings.md)

## Create a configuration item

1. In the Configuration Manager console, go to the **Assets and compliance** workspace, expand **Compliance Settings**, and then select the **Configuration Items** node.

1. On the **Home** tab of the ribbon, in the **Create** group, select **Create Configuration Item**.

1. On the **General** page of the **Create Configuration Item Wizard**, specify the following information:

    - **Name**: A unique name to identify this configuration item.

    - **Description**: An optional description to provide further information about its use.

    - Under **Settings for devices managed *without* the Configuration Manager client**, select **Windows 8.1 and Windows 10**.

    - **Categories**: You can create and assign categories to help you search and filter configuration items in the Configuration Manager console.

1. On the **Supported Platforms** page of the wizard, select the specific Windows platforms to evaluate this configuration item.

1. On the **Device Settings** page, select the settings groups that you want to configure. For more information on the available settings, see [Settings reference](#bkmk_setref).

    > [!TIP]
    > If the setting that you want isn't listed, select the option to **Configure additional settings that are not in the default setting groups**. This option adds the **Additional Settings** page to the wizard.

1. On each settings page, configure the necessary settings. When the settings support it, you can also **Remediate noncompliant settings**. If a device evaluates the setting as not compliant with this configuration item, it will remediate the setting to be compliant.

    For each settings group, you can also configure the severity that it reports when the setting is noncompliant. Choose one of the following values for the **Noncompliance severity for reports** option:

    - **None**: Devices that fail this compliance rule don't report a failure severity for Configuration Manager reports.

    - **Information**

    - **Warning**

    - **Critical**

    - **Critical with event**: Devices that fail this compliance rule report a failure severity of **Critical** for Configuration Manager reports. It also logs the noncompliant state as a Windows event in the application event log.

1. On the **Platform Applicability** page of the wizard, review any settings that aren't compatible with the selected supported platforms. Go back and remove these settings, change the support platforms, or continue.

    > [!IMPORTANT]
    > Devices don't assess the compliance of unsupported settings.

1. Complete the wizard.

You can view the new configuration item in the **Configuration Items** node of the **Assets and Compliance** workspace.

## <a name="bkmk_setref"></a> Settings reference  

The following sections detail the specific settings available in each group. Configure these settings on the **Device Settings** page of the **Create Configuration Item Wizard** for **Windows 8.1 and Windows 10** devices managed *without* the Configuration Manager client.

### Password

These settings are only for devices running Windows 10 and later.

- **Require password settings on devices**: Require a password on supported devices.
- **Minimum password length (characters)**: The minimum length for the password.
- **Password expiration in days**: The number of days before the user must change their password.
- **Number of passwords remembered**: Prevents the reuse of previously used passwords.
- **Number of failed logon attempts before device is wiped**: If this number of login attempts fail, MDM wipes the device
- **Idle time before device is locked**: Specify the amount of time a device can be idle before it's locked. The device is idle when there's no user input.
- **Password complexity**: Choose whether you can specify a numeric PIN such as `1234`, or whether you must supply a strong password.
  - **Number of complex character sets required in password**: If the password complexity is **Strong**, select how many types of characters the password requires: uppercase letters, lowercase letters, numbers, or symbols. By default, this value is `2`.
- **Send password recovery PIN to Exchange Server**

### Device

- **Screen capture**: Enable this setting to allow the user to take a screenshot of the device display. (Windows 10 only)
- **Diagnostic data submission**: Enable this setting to allow Windows diagnostic data for analytics. (Windows 8.1 only)
- **Allow diagnostic data submission (Windows 10)**: Set the level of Windows diagnostic data for analytics: Disable, Basic, Enhanced, or Full. (Windows 10 only)
- **Geolocation**: Enable this setting to allow the device to use location services information. (Windows 10 only)
- **Copy and Paste**: Enable this setting to use copy and paste to transfer data between apps. (Windows 10 only)
- **Factory reset**: Enable this setting to allow the user to reset the device to its initial settings. (Windows 10 only)
- **Bluetooth**: Allow or prohibit the use of the device's Bluetooth capability.
- **Bluetooth discoverable mode**: Allow or prohibit the device to be discovered by other Bluetooth devices. (Windows 10 only)
- **Bluetooth advertising**: Allow or prohibit the use of Bluetooth advertising. (Windows 10 only)
- **Voice recording**: Allow or prohibit the use of the voice recording features of the device. (Windows 10 only)
- **Cortana**: Allow or prohibit the use of the Cortana voice assistant. (Windows 10 only)
- **Action Center notifications**: Enable or disable the notification pane in Windows 10. (Windows 10 only)
- **Region settings modification (desktop only)**: Allow or prohibit the user from changing the regional settings on the device.
- **Power and sleep settings modification (desktop only)**: Allow or prohibit the user from changing power and sleep settings on the device.
- **Language settings modification (desktop only)**: Allow or prohibit the user from changing the language settings on the device.
- **System time modification**: Allow or prohibit the user from changing the device date and time.
- **Device name modification**: Allow or prohibit the user from changing the device name.

### Email management

These settings are for devices running Windows 8.1 and Windows 10.  

- **POP and IMAP email**: Allow or prohibit connections to email accounts that use the POP and IMAP standards.
- **Maximum time to keep email**: How long to keep email before the server deletes it.
- **Allowed message formats**: Specify whether emails are **Plain Text** or **HTML and Plain Text**.
- **Maximum size for plain text email (automatically downloaded)**: Set the maximum size of plain text emails when they're automatically downloaded.
- **Maximum size for HTML email (automatically downloaded)**: Set the maximum size of HTML emails when they're automatically downloaded.
- **Maximum size of an attachment (automatically downloaded)**: Set the maximum size of email attachments that are automatically downloaded.
- **Calendar synchronization**: Allow or prohibit synchronization of calendars to the device.
- **Custom email account**: Allow or prohibit use of a non-organizational email account on the device.
- **Make Microsoft Account optional in Windows Mail app**: Enable this option to not require a Microsoft account in Windows Mail.

### Store

These settings are only for devices running Windows 10 and later.

- **Application store**: Allow or prohibit access to the Microsoft Store on the device.
- **Enter a password to access the application store**: Enable this option to require users to enter a password to access the Microsoft Store app.
- **In-app purchases**: Allow or prohibit users to make in-app purchases.
- **Store originated app launch**: Disable all apps that were pre-installed on the device or installed from the Microsoft Store.
- **Auto-update apps from store**: Allow or prohibit apps installed from the Microsoft Store to update automatically.
- **Install apps on system drive**: Allow or prohibit the device to install apps on the system drive, which is typically the `C:` drive.
- **Install app data on system volume**: Enable this option to allow apps to store data on the system drive.
- **Use private store only**: Require users to download apps from your private store.
- **Game DVR**: Disable Windows Game recording and broadcasting

### Browser

These settings are for devices running Windows 8.1 and Windows 10.

- **Allow web browser**: Allow or prohibit the use of the web browser on the device.
- **Autofill**: Allow or prohibit changing autocomplete settings in the browser.
- **Active scripting**: Allow or prohibit whether the browser can run scripts, such as ActiveX scripts.
- **Plug-ins**: Allow or prohibit adding plug-ins to Internet Explorer.
- **Pop-up blocker**: Allow or prohibit the browser pop-up blocker.
- **Cookies**: Allow or prohibit cookies to be saved on the device.
- **Fraud warning**: Allow or prohibit warnings of potential fraudulent websites.

### Internet Explorer

These settings are for devices running Windows 8.1 and Windows 10.

- **Always send Do Not Track header**: Allow or prohibit sending browsing information to third-party sites.
- **Intranet security zone**: Allow or prohibit assignment of a security level to the intranet security zone.
- **Security level for Internet zone**: Set the security level for the Internet zone: High, Medium-High, or Medium.
- **Security level for intranet zone**: Set the security level for the intranet zone: High, Medium-High, Medium, Medium-Low, or Low.
- **Security level for trusted sites zone**: Set the security level for the trusted sites zone: High, Medium-High, Medium, Medium-Low, or Low.
- **Security level for restricted sites zone**: Set the security level for the restricted sites zone: High.
- **Namespaces for intranet zone**: Configure websites to add or remove from the intranet zone.
- **Go to intranet site for single word entry**: Allow or prohibit Internet Explorer to automatically go to an intranet site if the user enters a valid site name without a preceding protocol, for example `https://`.
- **Enterprise Mode menu option**: Enable users to activate and deactivate Enterprise Mode from the Internet Explorer **Tools** menu.
  - **Logging report location (URL)**: When Enterprise Mode is active, specify a URL to log visited websites.
- **Enterprise Mode site list location (URL)**: When Enterprise Mode is active, specify the list of websites that use it.

### Cloud

These settings are for devices running Windows 8.1 and Windows 10.

- **Settings synchronization**: Allow or prohibit settings to synchronize between devices.
- **Credentials synchronization**: Allow or prohibit credentials to synchronize between devices.
- **Microsoft Account**: Enable this setting to allow the use of a Microsoft account on the device.
- **Settings synchronization over metered connections**: Allow or prohibit settings to synchronize when the network connection is metered.

### Security

- **Unsigned file installation**: Allows who can install an unsigned file. (Windows 10 only)
- **Unsigned applications**: Allow or prohibit installing unsigned apps. (Windows 10 only)
- **SMS and MMS messaging**: Allow or prohibit text message protocols on the device. (Windows 10 only)
- **Removable storage**: Allow or prohibit the use of removable storage, like an SD card. (Windows 10 only)
- **Camera**: Allow or prohibit the use of the device camera. (Windows 10 only)
- **Near field communication (NFC)**: Allow or prohibit communication using NFC. (Windows 10 only)
- **AntiTheft mode**: Allow or prohibit the use of Windows 10 AntiTheft mode. (Windows 10 only)
- **Allow USB connection**: Allow or prohibit other devices to connect to this device using a USB connection. (Windows 10 only)
- **Windows RT VPN profile**: Provisions a VPN profile for Windows RT devices (Windows 8.1 only)

### Peak synchronization

These settings are only for devices running Windows 10 and later.

- **Specify peak time**: Set the peak time and days of the week for mobile device synchronization.
- **Peak synchronization frequency**: Configure how often synchronization occurs during the peak hours.
- **Off-peak synchronization frequency**: Configure how often synchronization occurs outside of the peak hours.

### Roaming

- **Device management while roaming**: Allow or prohibit Configuration Manager from managing the device when it's roaming. (Windows 10 only)
- **Software download while roaming**: Allow or prohibit downloading apps and software when roaming. (Windows 10 only)
- **Email download while roaming**: Allow or prohibit e-mail downloads when roaming. (Windows 10 only)
- **Data roaming**: Allow or prohibit roaming between networks when accessing data.
- **VPN over cellular**: Allow or prohibit the device from using a VPN connection while connected to a cellular network. (Windows 10 only)
- **VPN roaming over cellular**: Allow or prohibit the device from using a VPN connection while roaming on a cellular network. (Windows 10 only)

### Encryption

- **Storage card encryption**: Set on to require the user to encrypt any storage cards used in the device. (Windows 10 only)
- **File encryption on device**: Set on to encrypt files stored on the device.
- **Require email signing**: The user has to digitally sign emails before they're sent.
  - **Signing algorithm**: Select the algorithm for signing emails: Default, SHA, or MD5
- **Require email encryption**: The user has to encrypt emails before they're sent.
  - **Encryption algorithm**: Select the algorithm for encrypting emails: Default, Triple DES, DES, RC2 128-bit, RC2 64-bit, RC2 40-bit

### Wireless communications

These settings are only for devices running Windows 10 and later.

- **Wireless network connection**: Allow or prohibit the device's Wi-Fi capability.
- **Wi-Fi tethering**: Enable the user to use the device as a mobile hotspot.
- **Offload data to Wi-Fi when possible**: Enable the device to use the Wi-Fi connection as much as possible.
- **Wi-Fi hotspot reporting**: Enable the device to send information about Wi-Fi connections to help the user discover nearby connections.
- **Manual Wi-Fi configuration**: Enable the user to manually configure wireless connections.

#### Configured wireless network connections

1. On the **Configure mobile device wireless communication settings** page, select **Add**.

1. In the **Wireless Network Connection** window, specify the following information about the wireless connection to provision on mobile devices:

    - **Network name (SSID)**: Enter the name of the Wi-Fi network.
    - **Network connection**: Choose either **Internet** or **Work**.
    - **Authentication**: Choose the authentication method for the wireless connection:
        - **Open**
        - **Shared**
        - **WPA**
        - **WPA-PSK**
        - **WPA2**
        - **WPA2-PSK**
    - **Data encryption**: Choose the encryption method used by this connection. The available values change based on the **Authentication** method you select:
        - **Disabled**
        - **WEP**
        - **TKIP**
        - **AES**
    - **Key index**: When you set **Data encryption** to **WEP**, select a key index from **1** to **4**.
    - **This network connects to the Internet**: Supply proxy settings to allow mobile devices on a wireless network to connect to the internet.
        - **Proxy server settings**: Configure your **Server** and **Port** settings for **HTTP**, **WAP**, and **Sockets** proxies.
    - **802.1X settings**:
        - **Enable 802.1X network access**: Secure the connection by specifying an EAP type.
        - **EAP type**: Choose one of the following authentication protocols:
            - **PEAP**
            - **Smart card or certificate**

### Certificates

Import certificates to install on mobile devices.

Select **Import**, and then specify the following values:

- **Certificate file**: Browse to and select a certificate file (**.cer**) to import.
- **Destination store**: Choose one or more of the following certificate stores:
  - **Root**
  - **CA**
  - **Normal**
  - **Privileged**
  - **SPC**
  - **Peer**
- **Role**: If you choose the **SPC** (Software Publisher Certificate) certificate store, choose the role to associate with the certificate:
  - **Mobile Operator**
  - **Manager**
  - **User Authenticated**
  - **IT Administrator**
  - **User Unauthenticated**
  - **Trusted Provisioning Server**

### System security

- **User Account Control**: Configure the behavior of Windows User Account Control on the device.
- **Network firewall**: Require Windows to enable the built-in firewall. (Windows 8.1)
- **Updates**: Configure the behavior of Windows software updates. (Windows 8.1)
  - **Minimum classification of updates**: Choose the minimum classification of updates to download and install: **None**, **Important**, or **Recommended**.
- **Updates (Windows 10)**: Configure the behavior Windows software updates. (Windows 10 only)
  - **Install day**: Choose the scheduled day when the device automatically installs updates and reboots. (Windows 10 only)
  - **Install time**: Choose the scheduled time when the device automatically installs updates and reboots. (Windows 10 only)
- **SmartScreen**: Enable or disable Windows Smart Screen.
- **Virus protection**: Require that Windows has antivirus software.
- **Virus protection signatures are up to date**: Require that the antivirus signature files are up to date.
- **Lock screen notification view**: Enable or disable notifications to display on the lock screen.
- **Pre-release features**: Configure whether the device accepts pre-release settings and features. (Windows 10 only)
- **Manual root certificate installation**: Enable or disable the user to manually install a root certificate, which enables trust for any certificate issued by that root. (Windows 10 only)
- **Allow manual unenrollment**: Allow or prohibit the user to unenroll the device from on-premises mobile device management with Configuration Manager.

### Windows Server Work Folders

These settings are for devices running Windows 8.1 and Windows 10.

- **Work Folders URL**: Specify the location of a Windows Server work folder that users can connect to from their device.

### Allowed and blocked apps list

These settings are only for devices running Windows Phone, which Configuration Manager on-premises MDM doesn't support. For more information, see [What happened to hybrid?](../understand/what-happened-to-hybrid.md).

### Windows 10 Team

These settings are only for devices running Windows 10 Team.

- **Allow screen to wake automatically when sensors detect someone in the room**: Allow or prohibit the device to wake automatically when its sensor detects someone in the room.
- **Require PIN for wireless projection**: Enable or disable whether you must enter a PIN before another device can connect wirelessly for projection.
- **Maintenance Window**: Enable this setting to configure the window when updates can install and restart the device.
  - **Start time**: Set the start time for the maintenance window.
  - **Duration (Hours)**: Set the length in hours of the maintenance window.
- **Azure Operational Insights**: Allow [Azure Operational Insights](https://azure.microsoft.com/resources/videos/azure-operational-insights-overview/) to collect, store, and analyze log file data from Windows 10 Team devices.
  - **Workspace ID**: Enter a valid workspace ID
  - **Workspace Key**: Enter the key for the associated workspace
- **Miracast wireless projection**: Allow Miracast-enabled devices to project to this Windows 10 Team device.
  - **Miracast channel**: Select a Miracast channel to project content.
- **Meeting information displayed on welcome screen**: Choose the type of information that the device displays on the **Meetings** tile of the **Welcome** screen:
  - **Show organizer and time only**
  - **Show organizer, time and subject (subject hidden for private meetings)**
- **Lockscreen background image URL**: Specify a URL to display a custom background on the **Welcome** screen of a Windows 10 Team device. Start the URL with `https://` and use the PNG format.

### Windows Information Protection  

For more information about how to configure enterprise data protection with Configuration Manager, see [Protect your enterprise data using Windows Information Protection (WIP)](/windows/security/information-protection/windows-information-protection/protect-enterprise-data-using-wip).

### Microsoft Edge Legacy

These settings are only for devices running Windows 10 and later.  

- **Allow search suggestions in address bar**: Let the search engine suggest sites as you type search phrases.
- **Allow do not track**: Inform websites that you don't want them to track your visit.
- **Enable SmartScreen**: Check that downloaded files don't contain malicious code.
- **Allow pop-ups**: Configure browser pop-ups.
- **Allow cookies**: Configure the use of cookies.
- **Allow Autofill**: Let the browser automatically fill forms with stored information like name, address, and phone.
- **Allow Password Manager**: Let the browser store and manage passwords for websites.
- **Developer Tools**: Allow or prohibit the developer tools feature of Edge.
- **Extensions**: Allow or prohibit Edge extensions.
- **InPrivate browsing**: Allow or prohibit InPrivate browsing, which doesn't store history or cookies.
- **WebRTC localhost IP address**: Allow or prohibit the device's localhost IP address to display when the user makes phone calls using the web RTC protocol.
- **Block access to about:flags**: Allow or prohibit the user to access the `about:flags` page, which contains developer and experimental settings.
- **SmartScreen prompt override for files**: Allow or prohibit the user to bypass SmartScreen filter warnings about downloading potentially malicious files.
- **SmartScreen prompt override**: Allow or prohibit the user to bypass SmartScreen filter warnings about potentially malicious websites.
- **First run URL**: Specify a website to display when a user opens Edge for the first time.

### Windows Defender Antivirus

These settings are only for devices running Windows 10 and later.

- **Allow real-time monitoring**: Enable real-time scanning for malware, spyware, and other unwanted software.
- **Allow behavior monitoring**: Defender checks for certain known patterns of suspicious activity on devices.
- **Enable Network Inspection System**: The Network Inspection System (NIS) helps to protect devices against network-based exploits. It uses the signatures of known vulnerabilities from the Microsoft Endpoint Protection Center to help detect and block malicious traffic.
- **Scan all downloads**: Defender scans all files that you download from the internet.
- **Allow script scanning**: Defender scans scripts that are used in Internet Explorer.
- **Monitor file and program activity**: Defender monitors file and program activity on devices.
  - **Files monitored**: Choose the type of files to monitor: all, incoming, or outgoing.
- **Days to track resolved malware**: Defender continues to track resolved malware for the number of days you specify. Then you can manually check previously affected devices. If you set the number of days to 0, malware remains in the Quarantine folder and isn't automatically removed. The maximum value is 90.
- **Allow client UI access**: Controls whether to hide the Defender user interface from users. When you change this setting, it takes effect the next time the device restarts.
- **Schedule a system scan**: Choose either a full or quick scan that occurs regularly on the day and time that you select:
  - **Day scheduled**: Choose the scheduled day when Defender runs the scan.
  - **Time scheduled**: Choose the scheduled time when Defender runs the scan.
- **Schedule a daily quick scan**: Choose the scheduled time when Defender runs a quick scan each day.
- **Limit CPU usage during a scan**: Set the percentage of the processor that Defender can utilize when it runs a scan. Enter a value from 1 to 100.
- **Scan archive files**: Defender scans compressed archives, like .zip or .cab files.
- **Scan email messages**: Defender scans email messages as they arrive on the device.
- **Scan removable drives**: Defender scans removable drives, like USB sticks.
- **Scan mapped drives**: Defender scans drives that are mapped to network shares. For example, `H:` is mapped to a user's personal drive. If the files on the drive are read-only, Defender can't remove any malware that it finds there.
- **Scan files opened from network shared folders**: Defender scans files when a user opens them from a shared network path. For example, `\\server\share\file.doc`. If the file on the share is read-only, Defender can't remove any malware that it finds.
- **Signature update interval**: Choose the time interval when Defender checks for new signature files.
- **Allow cloud protection**: Defender uses the Microsoft cloud to receive information about malware activity, and enable features like block at first sight.
- **Prompt users for samples submission**: Choose the behavior for Defender when files might require further analysis. For example, Defender can automatically send files to Microsoft to determine if they're malicious.
- **Potentially Unwanted Application detection**: Protects the device against running software that's classified by Defender as potentially unwanted. You can protect against these applications running, or use audit mode to report when a user installs a potentially unwanted application.
- **File and folder exclusions**: Add one or more files and folders to the exclusions list. For example, `C:\Path` or `%ProgramFiles%\Path\filename.exe`. Defender doesn't include these files and folders in any real-time or scheduled scans.
- **File extension exclusions**: Add one or more file extensions to the exclusions list. For example, `java` or `exe`. Defender doesn't include any files with these extensions in any real-time or scheduled scans.
- **Process exclusions**: Add specific processes to the exclusions list. For example, `C:\path\myproc.exe`. This exclusion type only supports the following extensions: `exe`, `com`, or `scr`. Defender doesn't include these processes in any real-time or scheduled scans.

### Additional Settings

On the **Device Settings** page of the wizard, if you select the option to **Configure additional settings that are not in the default setting groups**, use this **Additional Settings** page to configure those settings. Select **Add** and then choose from the list of available mobile settings. Choose **Select** to modify the built-in setting, or **Create Setting** to create a custom registry value or OMA URI setting type.

## Next steps

[Monitor compliance settings](../../compliance/deploy-use/monitor-compliance-settings.md)