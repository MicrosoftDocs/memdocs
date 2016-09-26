---
title: "Create configuration items for Windows 8.1 and Windows 10 devices managed without the System Center Configuration Manager client | System Center Configuration Manager"
ms.custom: na
ms.date: 06/22/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c262291a-80fe-47f3-a6d0-a605fe8b1f06
caps.latest.revision: 20
caps.handback.revision: 0
author: robstackmsft

---
# Create configuration items for Windows 8.1 and Windows 10 devices managed without the System Center Configuration Manager client
||  
|-|  
|This article contains information about [new functionality introduced in version 1602](https://technet.microsoft.com/library/mt622084.aspx) of System Center Configuration Manager \(current branch\). To use the new functionality, you must [install the 1602 update](https://technet.microsoft.com/library/mt607046.aspx). If you have not updated to the most recent version of Configuration Manager, you can [download the documentation for the version you use](https://gallery.technet.microsoft.com/Documentation-for-System-ea90eaf1) from the TechNet Gallery.|  
  
 Use the System Center Configuration Manager**Windows 8.1 and Windows 10** configuration item to manage settings  for Windows 8.1, and Windows 10 devices that are enrolled in Microsoft Intune or managed on-premises by Configuration Manager.  
  
## Create a Windows 8.1 and Windows 10 configuration item  
  
1.  In the Configuration Manager console, click **Assets and compliance** > **Compliance Settings** > **Configuration Items**.  
  
3.  On the **Home** tab, in the **Create** group, click **Create Configuration Item**.  
  
4.  On the **General** page of the **Create Configuration Item Wizard**, specify a name, and optional description for the configuration item.  
  
5.  Under **Specify the type of configuration item that you want to create**, select **Windows 8.1 and Windows 10**.  
  
6.  Click **Categories** if you create and assign categories to help you search and filter configuration items in the Configuration Manager console.  
  
7.  On the **Supported Platforms** page, select the specific Windows platforms that will evaluate the configuration item.  
  
8.  On the **Device Settings** page, select the settings group that you want to configure. See [Windows 8.1 and Windows 10 configuration item settings reference](#BKMK_Setref) in this topic for details, and then click **Next**.  
  
    > [!TIP]  
    >  If the setting that you want is not listed, select the **Configure additional settings that are not in the default setting groups check box**.  
  
9. On each settings page, configure the settings you require, and whether you want to remediate them when they are not compliant on devices (when this is supported).  
  
10. For each settings group, you can also configure the severity that will be reported when a configuration item is found to be noncompliant from:  
  
    -   **None** - Devices that fail this compliance rule do not report a failure severity for Configuration Manager reports.  
  
    -   **Information** - Devices that fail this compliance rule report a failure severity of **Information** for Configuration Manager reports.  
  
    -   **Warning** - Devices that fail this compliance rule report a failure severity of **Warning** for Configuration Manager reports.  
  
    -   **Critical** - Devices that fail this compliance rule report a failure severity of **Critical** for Configuration Manager reports.  
  
    -   **Critical with event** - Devices that fail this compliance rule report a failure severity of **Critical** for Configuration Manager reports. This severity level is also be logged as a Windows event in the application event log.  
  
11. On the **Platform Applicability** page, review any settings that are not compatible with the supported platforms you selected earlier. You can go back and remove these settings, or you can continue.  
  
    > [!TIP]  
    >  Unsupported settings are not assessed for compliance.  
  
12. Complete the wizard.  
  
 You can view the new configuration item in the **Configuration Items** node of the **Assets and Compliance** workspace.  
  
##  Windows 8.1 and Windows 10 configuration item settings reference  
  
### Password  
 These settings are for devices running Windows 10 and later only.  
  
|Setting|Details|  
|-------------|-------------|  
|**Require password settings on devices**|Require a password on supported devices.|  
|**Minimum password length (characters)**|The minimum length for the password.|  
|**Password expiration in days**|The number of days before a password must be changed.|  
|**Number of passwords remembered**|Prevents re-using previously used passwords.|  
|**Number of failed logon attempts before device is wiped**|Wipes the device if this number of login attempts fail.|  
|**Idle time before device is locked**|Specify the amount of time a device can be idle (have no user input) before it is locked.|  
|**Password complexity**|Choose whether you can specify a PIN such as ‘1234’, or whether you must supply a strong password.|  
|**Password quality**|Select the password complexity level required and also whether biometric devices can be used.|  
|**Send password recovery PIN to Exchange Server**||  
  
###  Device  
  
|Setting name|Details|  
|------------------|-------------|  
|**Screen capture**|Allows you to take a screenshot of the device display.<br /><br /> (Windows 10 only)|  
|**Diagnostic data submission (Windows 8.1 and earlier)**|Allow submission of app log files.<br /><br /> (Windows 8.1 only)|  
|**Diagnostic data submission (Windows 10)**|Allow submission of app log files.|  
|**Geolocation**|Allow the device to use location services information.<br /><br /> (Windows 10 only)|  
|**Copy and Paste**|Use copy and paste to transfer data between apps.<br /><br /> (Windows 10 only)|  
|**Bluetooth**|Allow use of the devices Bluetooth capability.|  
|**Bluetooth discoverable mode**|Allow the device to be discovered by other Bluetooth devices.<br /><br /> (Windows 10 only)|  
|**Bluetooth advertising**|Allow the use of Bluetooth advertising.<br /><br /> (Windows 10 only)|  
|**Voice recording**|Allow the use of the voice recording features of the device.<br /><br /> (Windows 10 only)|  
  
### Email management  
 These settings are for devices running Windows 8.1 and Windows 10.  
  
|Setting|Details|  
|-------------|-------------|  
|**POP and IMAP email**|Allows connection to email accounts that use the POP and IMAP standards.|  
|**Maximum time to keep email**|How long to keep email before it is deleted from the server.|  
|**Allowed message formats**|Specify whether user emails can be HTML, or plain text only.|  
|**Maximum size for plain text email (automatically downloaded)**|Controls the maximum size of plain text emails when automatically downloaded.|  
|**Maximum size for HTML email (automatically downloaded)**|Controls the maximum size of HTML emails when automatically downloaded.|  
|**Maximum size of an attachment (automatically downloaded)**|Configures the maximum size email that will be automatically downloaded.|  
|**Calendar synchronization**|Allow synchronization of calendars to the device.|  
|**Custom email account**|Allow using a non-Microsoft account on the device.|  
|**Make Microsoft Account optional in Windows Mail app**|Configure this to remove the requirement for a Microsoft account in Windows Mail.|  
  
### Store  
 These settings are for devices running Windows 10 and later only.  
  
|Setting|Details|  
|-------------|-------------|  
|**Application store**|Allows access to the app store on the device.|  
|**Enter a password to access the application store**|Users must enter a password to access the app store.|  
|**In-app purchases**|Allows users to make in-app purchases.|  
  
### Browser  
 These settings are for devices running Windows 8.1 and Windows 10.  
  
|Setting|Details|  
|-------------|-------------|  
|**Allow web browser**|Allow the use of the web browser on the device.|  
|**Autofill**|User can change autocomplete settings in the browser.|  
|**Active scripting**|Browser can run scripts, such as Active X scripts.|  
|**Plug-ins**|User can add plug-ins to Internet Explorer.|  
|**Pop-up blocker**|Enables or disables the browser pop-up blocker.|  
|**Cookies**|Allow cookies to be saved on the device.|  
|**Fraud warning**|Enable or disable warnings of potential fraudulent websites.|  
  
###  Internet Explorer  
 These settings are for devices running Windows 8.1 and Windows 10.  
  
|Setting name|Details|  
|------------------|-------------|  
|**Always send Do Not Track header**|Prevents browsing information from being sent to third-party sites.|  
|**Intranet security zone**|Assign a security level to the Intranet security zone.|  
|**Security lever for Internet zone**|Configure the security level for the Internet zone.|  
|**Security level for intranet zone**|Configure the security level for the intranet zone.|  
|**Security level for trusted sites zone**|Configure the security level for the trusted sites zone.|  
|**Security level for restricted sites zone**|Configure the security level for the restricted sites zone.|  
|**Namespaces for intranet zone**|Configure websites that will be added or removed from the intranet zone.|  
|**Go to intranet site for single word entry**|Enables or disables the setting that allows Internet Explorer to automatically go to an Intranet site if a valid site name is entered without a preceding HTTP:|  
|**Enterprise Mode menu option**|Allow users to activate and deactivate Enterprise Mode from the Internet Explorer **Tools** menu.|  
|**Logging report location (URL)**|Specify a URL where visited websites will be logged when Enterprise Mode is active.|  
|**Enterprise Mode site list location (URL)**|Specify the location of the list of websites that will use Enterprise Mode when it is active.|  
  
###  Cloud  
 These settings are for devices running Windows 8.1 and Windows 10.  
  
|Setting name|Details|Windows 8.1|Windows 10|  
|------------------|-------------|-----------------|----------------|  
|**Settings synchronization**|Allows synchronization of settings between devices.|Yes|Yes|  
|**Credentials synchronization**|Allows synchronization of credentials between devices.|Yes|Yes|  
|**Microsoft Account**|Allow the use of a Microsoft account on the device.|Yes|Yes|  
|**Settings synchronization over metered connections**|Allow settings to be synchronized when the Internet connection is metered.|Yes|Yes|  
  
###  Security  
  
|Setting name|Details|  
|------------------|-------------|  
|**Unsigned file installation**|Allows the loading of unsigned files.<br /><br /> (Windows 10 only)|  
|**Unsigned applications**|Allows the loading of unsigned apps.<br /><br /> (Windows 10 only)|  
|**SMS and MMS messaging**|Allow SMS and MMS messaging from the device.<br /><br /> (Windows 10 only)|  
|**Removable storage**|Allow use of removable storage, like an SD card on the device.<br /><br /> (Windows 10 only)|  
|**Camera**|Allow use of the device camera.<br /><br /> (Windows 10 only)|  
|**Near field communication (NFC)**|Allow communication using NFC on the device.<br /><br /> (Windows 10 only)|  
|**AntiTheft mode**|Controls whether Windows 10 AntiTheft mode is enabled.<br /><br /> (Windows 10 only)|  
|**Profile file**|Provisions a VPN profile for Windows RT devices.<br /><br /> Windows 8.1 only)|  
|**Profile name**|Provisions a VPN profile for Windows RT devices.<br /><br /> Windows 8.1 only)|  
|**Profile for all users**|Provisions a VPN profile for Windows RT devices.<br /><br /> Windows 8.1 only)|  
  
###  Peak synchronization  
 These settings are for devices running Windows 10 and later only.  
  
|Setting name|Details|  
|------------------|-------------|  
|**Specify peak time**|Configure the peak time for mobile device synchronization.|  
|**Peak synchronization frequency**|Configure how often synchronization occurs during the peak hours you configured.|  
|**Off-peak synchronization frequency**|Configure how often synchronization occurs outside of the peak hours you configured.|  
  
###  Roaming  
  
|Setting name|Details|  
|------------------|-------------|  
|**Device management while roaming**|Allows the device to be managed by Configuration Manager when it is roaming.<br /><br /> (Windows 10 only)|  
|**Software download while roaming**|Allows the download of apps and software when roaming.<br /><br /> (Windows 10 only)|  
|**Email download while roaming**|Allows e-mail downloads when roaming.<br /><br /> (Windows 10 only)|  
|**Data roaming**|Allow roaming between networks when accessing data.|  
  
###  Encryption  
  
|Setting name|Details|  
|------------------|-------------|  
|**Storage card encryption**|Require any storage cards used with the device to be encrypted.<br /><br /> (Windows 10 only)|  
|**File encryption on device**|Requires that files on the device are encrypted.|  
|**Require email signing**|Requires that emails are signed before they are sent.|  
|**Signing algorithm**|Select the signing algorithm for signed emails.|  
|**Require email encryption**|Requires that emails are encrypted before they are sent.|  
|**Encryption algorithm**|Select the algorithm for encrypting emails.|  
  
###  Wireless communications  
 These settings are for devices running Windows 10 and later only.  
  
|Setting name|Details|  
|------------------|-------------|  
|**Wireless network connection**|Enable or disable the devices Wi-Fi capability.|  
|**Wi-Fi tethering**|Lets users use their device as a mobile hotspot.|  
|**Offload data to Wi-Fi when possible**|Configure this to use the Wi-Fi connection on the device when possible.|  
|**Wi-Fi hotspot reporting**||  
|**Manual Wi-Fi configuration**||  
  
##### To configure a wireless network connection  
  
1.  On the **Configure mobile device wireless communication settings** page, click **Add**.  
  
2.  In the **Wireless Network Connection** dialog box, specify the following information about the wireless connection that will be provisioned on mobile devices:  
  
    |Setting|More information|  
    |-------------|----------------------|  
    |**Network name (SSID)**|Enter the name of the Wi-Fi network.|  
    |**Network connection**|Choose from **Internet** or **Work**.|  
    |**Authentication**|Choose the authentication method for the wireless connection from:<br /><br /> - **Open**<br /><br /> - <br />                            **Shared**<br /><br /> - <br />                            **WPA**<br /><br /> - <br />                            **WPA-PSK**<br /><br /> - <br />                            **WPA2**<br /><br /> - <br />                            **WPA2-PSK**|  
    |**Data encryption**|Choose the encryption method used by this connection. The values you can select will differ depending on the **Authentication** method you selected:<br /><br /> - **Disabled**<br /><br /> - <br />                            **WEP**<br /><br /> - <br />                            **TKIP**<br /><br /> - <br />                            **AES**|  
    |**Key index**|Select a key index from **1** to **4** that will be used with a **Data encryption** setting of **WEP**.|  
    |**This network connects to the Internet**|Select this option if you want to supply proxy settings that let mobile devices on a wireless connection connect to the Internet.|  
    |**Proxy server settings**|Specify as required, **Server** and **Port** settings for **HTTP**, **WAP** and **Sockets**.|  
    |**Enable 802.1X network access**|Select this option if you want to secure the connection by specifying an EAP type.|  
    |**EAP type**|Choose the EAP type to use from:<br /><br /> - **PEAP**<br /><br /> - <br />                            **Smart card or certificate**|  
  
3.  When you are finished, click **OK**.  
  
### Certificates  
 Lets you import certificates to install on mobile devices.  
  
 Click **Import**, and then specify the following values:  
  
-   **Certificate file** – Click Browse and then select the certificate file with the extension **.cer** that you want to import.  
  
-   **Destination store** – Choose one or more destination stores where the imported certificate will be added on the mobile device from:  
  
    -   **Root**  
  
    -   **CA**  
  
    -   **Normal**  
  
    -   **Privileged**  
  
    -   **SPC**  
  
    -   **Peer**  
  
-   **Role** – If **SPC** (Software Publisher Certificate) is selected as the destination store, choose the role that will be associated with the certificate from:  
  
    -   **Mobile Operator**  
  
    -   **Manager**  
  
    -   **User Authenticated**  
  
    -   **IT Administrator**  
  
    -   **User Unauthenticated**  
  
    -   **Trusted Provisioning Server**  
  
### System security  
  
|Setting|Details|  
|-------------|-------------|  
|**User Account Control**|Enables or disables Windows User Account Control on the device.|  
|**Network firewall**|Enables or disables Windows Firewall.<br /><br /> (Windows 8.1 only)|  
|**Updates (Windows 8.1 and earlier)**|Choose how Windows software updates will be downloaded to computers. For example, you can automatically download updates, but let the user choose when to install them.|  
|**Minimum classification of updates**|Choose the minimum classification of updates that will be downloaded to Windows computers, **None**, **Important**, or **Recommended**.|  
|**Updates (Windows 10)**|Choose how Windows software updates will be downloaded to computers. For example, you can automatically download updates, but let the user choose when to install them.<br /><br /> (Windows 10 only)|  
|**Install day**|Choose the day when updates will be installed.<br /><br /> (Windows 10 only)|  
|**Install time**|Choose the time when updates will be installed.<br /><br /> (Windows 10 only)|  
|**SmartScreen**|Enable or disable Windows Smart Screen.|  
|**Virus protection**|Select to ensure that antivirus software is installed on the device.|  
|**Virus protection signatures are up to date**|Select to ensure that the antivirus signature files are up to date.|  
|**Pre-release features**|Allows Microsoft to deploy pre-release settings and features to the device.<br /><br /> (Windows 10 only)|  
|**Manual root certificate installation**|(Windows 10 only)|  
  
###  Windows Server Work Folders  
 These settings are for devices running Windows 8.1 and Windows 10.  
  
|Setting name|Details|  
|------------------|-------------|  
|**Work Folders URL**|Configures the location of a Windows Server work folder that users can connect to from their device.|  
  
### Allowed and blocked apps (Windows Phone only)  
 Lets you specify a list of Intune managed apps that are compliant, or not compliant in your company. Windows Phone can allow, or block the installation of these apps.  
  
 You cannot specify both compliant and noncompliant apps in the same configuration item.  
  
#### To specify apps that will be allowed or blocked  
  
1.  On the **Allowed and Blocked Apps list** page, specify the following information:  
  
    |Setting|More information|  
    |-------------|----------------------|  
    |**Blocked apps list**|Select this option if you want to specify a list of apps that users are not allowed to install.|  
    |**Allowed apps list**|Select this option if you want to specify a list of apps that users are allowed to install. Any other apps will be blocked from installing.|  
    |**Add**|Adds an app to the selected list. Specify a name of your choice, optionally the app publisher, and the URL to the app in the app store.<br /><br /> To specify the URL, from the Windows Store, search for the app you want to use.<br /><br /> Open the app’s page, and copy the URL to the clipboard. You can now use this as the URL in either the allowed or blocked apps list.<br /><br /> **Example:** Search the store for the **Skype** app. The URL you use will be **http://www.windowsphone.com/store/app/skype/c3f8e570-68b3-4d6a-bdbb-c0a3f4360a51**.|  
    |**Edit**|Lets you edit the name, publisher and URL of the selected app.|  
    |**Remove**|Deletes the selected app from the list.|  
    |**Import**|Imports a list of apps you have specified in a comma-separated values file. Use the format, application name, publisher, app URL in the file.|  
  
### Windows 10 Team  
 These settings are for devices running Windows 10 Team only.  
  
|Setting name|Details|  
|------------------|-------------|  
|**Allow screen to wake automatically when sensors detect someone in the room**|Allows the device to wake automatically when its sensor detects someone in the room.|  
|**Required PIN for wireless projection**|Specifies whether you must enter a PIN before you can use the wireless projection capabilities of the device.|  
|**Maintenance Window**|Configures the window when updates can take place to the device. You can configure the start time of the window and the duration (from 1-5 hours).|  
  
### Microsoft Edge  
 These settings are for devices running Windows 10 and later.  
  
|Setting name|Details|  
|------------------|-------------|  
|**Allow search suggestions in address bar**|Lets your search engine suggest sites as you type search phrases.|  
|**Allow sending intranet traffic to Internet Explorer**||  
|**Allow do not track**|Do not track informs websites that you do not want them to track your visit to a site.|  
|**Enable SmartScreen**|Use SmartScreen to check files your users download do not contain malicious code.|  
|**Allow pop-ups**|Allow or disable browser pop-ups.|  
|**Allow cookies**|Allow or disable cookies.|  
|**Allow Autofill**|Allow the use of the Autofill feature of the Edge browser.|  
|**Allow Password Manager**|Allow the use of the password manager feature of the Edge browser.|  
|**Enterprise Mode site list location**|Specifies where to find the list of web sites that will open in Enterprise mode. Users cannot edit this list.|  
  
### Windows Information Protection (formerly Enterprise Data Protection) 

With the increase of employee-owned devices in the enterprise, there’s also an increasing risk of accidental data leaks through apps and services, like email, social media, and the public cloud, which are outside of the enterprise’s control. For example, when an employee sends the latest engineering pictures from their personal email account, copies and pastes product info into a tweet, or saves an in-progress sales report to their public cloud storage.

Windows Information Protection (WIP) helps to protect against this potential data leakage without otherwise interfering with the employee experience. WIP also helps to protect enterprise apps and data against accidental data leaks on enterprise-owned devices and personal devices that employees bring to work without requiring changes to your environment or other apps.

 Configuration Manager WIP configuration items manage the list of apps protected by WIP, enterprise network locations, protection level, and encryption settings.
  
For information about how to configure enterprise data protection with Configuration Manager, see [Protect your enterprise data using Windows Information Protection (WIP)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip).
  

