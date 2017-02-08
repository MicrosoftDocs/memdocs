---
title: "Create configuration items for Windows 8.1 and Windows 10 devices managed without the System Center Configuration Manager client | Microsoft Docs"
description: "Use the System Center Configuration Manager Windows 10 configuration item to manage settings for Windows 10 computers."
ms.custom: na
ms.date: 12/08/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 23e1e4dc-623a-4521-ad04-ae9482927097
caps.latest.revision: 20
caps.handback.revision: 0
author: robstackmsftms.author: robstackmanager: angrobe

---
# Create configuration items for Windows 8.1 and Windows 10 devices managed without the System Center Configuration Manager client*Applies to: System Center Configuration Manager (Current Branch)*

Use the System Center Configuration Manager **Windows 8.1 and Windows 10** configuration item to manage settings  for Windows 8.1, and Windows 10 devices that are enrolled in Microsoft Intune or managed on-premises by Configuration Manager.  

## Create a Windows 8.1 and Windows 10 configuration item  

1.  In the Configuration Manager console, click **Assets and compliance** > **Compliance Settings** > **Configuration Items**.  

3.  On the **Home** tab, in the **Create** group, click **Create Configuration Item**.  

4.  On the **General** page of the **Create Configuration Item Wizard**, specify a name, and optional description for the configuration item.  

5.  Under **Specify the type of configuration item that you want to create**, select **Windows 8.1 and Windows 10**.  

6.  Click **Categories** if you create and assign categories to help you search and filter configuration items in the Configuration Manager console.  

7.  On the **Supported Platforms** page, select the specific Windows platforms that will evaluate the configuration item.  

8.  On the **Device Settings** page, select the settings group that you want to configure. See [Windows 8.1 and Windows 10 configuration item settings reference](#windows-81-and-windows-10-configuration-item-settings-reference) in this topic for details, and then click **Next**.  

    > [!TIP]  
    >  If the setting that you want is not listed, select the **Configure additional settings that are not in the default setting groups check box**.  

9. On each settings page, configure the settings you require, and whether you want to remediate them when they are not compliant on devices (when this is supported).  

10. For each settings group, you can also configure the severity that will be reported (in Configuration Manager reports) when a configuration item is found to be noncompliant from:  

    -   **None** - Devices that fail this compliance rule do not report a failure severity.  

    -   **Information** - Devices that fail this compliance rule report a failure severity of **Information**.  

    -   **Warning** - Devices that fail this compliance rule report a failure severity of **Warning**.  

    -   **Critical** - Devices that fail this compliance rule report a failure severity of **Critical**.  

    -   **Critical with event** - Devices that fail this compliance rule report a failure severity of **Critical**. This severity level is also be logged as a Windows event in the application event log.  

11. On the **Platform Applicability** page, review any settings that are not compatible with the supported platforms you selected earlier. You can go back and remove these settings, or you can continue.  

    > [!TIP]  
    >  Unsupported settings are not assessed for compliance.  

12. Complete the wizard.  

 You can view the new configuration item in the **Configuration Items** node of the **Assets and Compliance** workspace.  

##  Windows 8.1 and Windows 10 configuration item settings reference  

### Password  

|Setting|Details|  
|-------------|-------------|  
|**Require password settings on devices**|Require a password on supported devices.|  
|**Minimum password length (characters)**|The minimum length for the password.|  
|**Password expiration in days**|The number of days before a password must be changed.|  
|**Number of passwords remembered**|Prevents re-using previously used passwords.|  
|**Number of failed logon attempts before device is wiped**|Wipes the device if this number of login attempts fail.|  
|**Idle time before device is locked**|Specify the amount of time a device can be idle (have no user input) before it is locked.|  
|**Password complexity**|Choose whether you can specify a PIN such as ‘1234’, or whether you must supply a strong password.<br>(Windows 10 only)|  
|**Password complexity** - **Number of complex character sets required in password**|If you selected a **Strong** password, use this setting to configure the number of complex character sets required. For a strong password, this should be set to at least **3** which means both letters and numbers are required. Select **4** if you want to enforce a password that additionally requires special characters such as **(%$**.<br>(Windows 10 only)|
|**Send password recovery PIN to Exchange Server**|Set to **Enabled** or **Disabled**.<br>(Windows 10 only)|  

###  Device  

|Setting name|Details|  
|------------------|-------------|  
|**Screen capture**|Allows you to take a screenshot of the device display.<br> (Windows 10 only)|  
|**Diagnostic data submission**|Allow submission of app log files.<br>(Windows 8.1 only)|  
|**Diagnostic data submission (Windows 10)**|Allow submission of app log files.<br>(Windows 10 only)|  
|**Geolocation**|Allow the device to use location services information.<br>(Windows 10 only)|  
|**Copy and Paste**|Use copy and paste to transfer data between apps.<br>(Windows 10 only)|
|**Factory reset**|Controls whether the user can factory reset their device.|
|**Bluetooth**|Allow use of the devices Bluetooth capability.|  
|**Bluetooth discoverable mode**|Allow the device to be discovered by other Bluetooth devices.<br>(Windows 10 only)|  
|**Bluetooth advertising**|Allow the use of Bluetooth advertising.<br> (Windows 10 only)|  
|**Voice recording**|Allow the use of the voice recording features of the device.<br>(Windows 10 only)|
|**Cortana**|Enable or disable the Cortana voice assistant.|

### Email management  

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

|Setting|Details|  
|-------------|-------------|  
|**Allow web browser**|Allow the use of the web browser on the device.<br>(Windows 10 only)|  
|**Autofill**|User can change autocomplete settings in the browser.|  
|**Active scripting**|Browser can run scripts, such as Active X scripts.|  
|**Plug-ins**|User can add plug-ins to Internet Explorer.|  
|**Pop-up blocker**|Enables or disables the browser pop-up blocker.|  
|**Cookies**|Allow cookies to be saved on the device.|  
|**Fraud warning**|Enable or disable warnings of potential fraudulent websites.|  

###  Internet Explorer  
 These settings are only for devices running Windows 8.1.  

|Setting name|Details|  
|------------------|-------------|  
|**Always send Do Not Track header**|Prevents browsing information from being sent to third-party sites.|  
|**Intranet security zone**|Assign a security level to the Intranet security zone.|  
|**Security level for Internet zone**|Configure the security level for the Internet zone.|  
|**Security level for intranet zone**|Configure the security level for the intranet zone.|  
|**Security level for trusted sites zone**|Configure the security level for the trusted sites zone.|  
|**Security level for restricted sites zone**|Configure the security level for the restricted sites zone.|  
|**Namespaces for intranet zone**|Configure websites that will be added or removed from the intranet zone.|  
|**Go to intranet site for single word entry**|Enables or disables the setting that allows Internet Explorer to automatically go to an Intranet site if a valid site name is entered without a preceding HTTP:|  
|**Enterprise Mode menu option**|Allow users to activate and deactivate Enterprise Mode from the Internet Explorer **Tools** menu.|  
|**Logging report location (URL)**|Specify a URL where visited websites will be logged when Enterprise Mode is active.|  
|**Enterprise Mode site list location (URL)**|Specify the location of the list of websites that will use Enterprise Mode when it is active.|

### Microsoft Edge  
 These settings are for devices running Windows 10 and later.  

|Setting name|Details|  
|------------------|-------------|  
|**Allow search suggestions in address bar**|Lets your search engine suggest sites as you type search phrases.|  
|**Allow sending intranet traffic to Internet Explorer**|Lets users open intranet websites in Internet Explorer.|  
|**Allow do not track**|Do not track informs websites that you do not want them to track your visit to a site.|  
|**Enable SmartScreen**|Use SmartScreen to check files your users download do not contain malicious code.|  
|**Allow pop-ups**|Allow or disable browser pop-ups.|  
|**Allow cookies**|Allow or disable cookies.|  
|**Allow Autofill**|Allow the use of the Autofill feature of the Edge browser.|  
|**Allow Password Manager**|Allow the use of the password manager feature of the Edge browser.|  
|**Enterprise Mode site list location**|Specifies where to find the list of web sites that will open in Enterprise mode. Users cannot edit this list.|  

### Windows Defender

 These settings are for devices running Windows 10 November Update (1511) and later.  

|Setting name|Details|  
|------------------|-------------|
|**Allow real-time monitoring**|Enables real-time scanning for malware, spyware, and other unwanted software.|
|**Allow behavior monitoring**|Lets Defender check for certain known patterns of suspicious activity on devices.|
|**Enable Network Inspection System**|The Network Inspection System (NIS) helps to protect devices against network-based exploits by using the signatures of known vulnerabilities from the Microsoft Endpoint Protection Center to help detect and block malicious traffic.|
|**Scan all downloads**|Controls whether Defender scans all files downloaded from the Internet.|
|**Allow script scanning**|Lets Defender scan scripts that are used in Internet Explorer.|
|**Monitor file and program activity**|Enable this setting to allow Defender to monitor file and program activity on devices.|
|**Files monitored**|If you enabled **Monitor file and program activity**, you can then select whether to monitor incoming files, outgoing files, or all files.|
|**Days to track resolved malware**|Lets Defender continue to track resolved malware for the number of days you specify so that you can manually check previously affected devices. If you set the number of days to 0, malware remains in the Quarantine folder and is not automatically removed.|
|**Allow client UI access**|Controls whether the Windows Defender user interface is hidden from end users. When this setting is changed, it will take effect the next time the end user's PC is restarted.|
|**Schedule a system scan**|Lets you schedule a full or quick system scan that occurs regularly on the day and time you select.|
|**Schedule a quick daily scan**|Lets you schedule a quick scan that occurs daily at the time you select.|
|**Limit CPU usage during a scan**|Lets you limit the amount of CPU that scans are allowed to use (from **1** to **100**)|
|**Scan archive files**|Allows Defender to scan archived files such as Zip or Cab files.|
|**Scan email messages**|Allows Defender to scan email messages as they arrive on the device.|
|**Scan removable drives**|Lets Defender scan removable drives like USB sticks.|
|**Scan mapped drives**|Lets Defender scan files on mapped network drive.<br>If the files on the drive are read-only, Defender will be unable to remove any malware found in them.|
|**Scan files opened from network shared folders**|Lets Defender scan files on shared network drives (for instance, those accessed from a UNC path.<br>If the files on the drive are read-only, Defender will be unable to remove any malware found in them.|
|**Signature update interval**|Specify the interval at which Defender will check for new signature files.|
|**Allow cloud protection**|Allow or block the Microsoft Active Protection Service from receiving information about malware activity from devices you manage. This information is used to improve the service in the future.|
|**Prompt users for samples submission**|Controls whether files that might require further analysis by Microsoft to determine if they are malicious are automatically sent to Microsoft.|
|**Potentially Unwanted Application detection**|This setting can be used to protect enrolled Windows desktop devices against running software classified by Windows Defender as potentially unwanted. You can protect against these applications running, or use audit mode to report when a potentially unwanted application is installed.|
|**File and folder exclusions**|Add one or more files and folders like C:\Path or %ProgramFiles%\Path\filename.exe to the exclusions list. These files and folders will not be included in any real-time, or scheduled scans.|
|**File extension exclusions**|Add one or more file extensions like jpg or txt to the exclusions list. Any files with these extensions will not be included in any real-time, or scheduled scans.|
|**Process exclusions**|Add one or more processes of the type .exe, .com, or .scr to the exclusions list. These processes will not be included in any real-time, or scheduled scans.|



###  Cloud  

|Setting name|Details|  
|------------------|-------------|  
|**Settings synchronization**|Allows synchronization of settings between devices.|  
|**Credentials synchronization**|Allows synchronization of credentials between devices.|  
|**Microsoft Account**|Allow the use of a Microsoft account on the device.<br>(Windows 10 only)|  
|**Settings synchronization over metered connections**|Allow settings to be synchronized when the Internet connection is metered.|  

###  Security  

|Setting name|Details|  
|------------------|-------------|  
|**Unsigned file installation**|Allows the loading of unsigned files.<br>(Windows 10 only)|  
|**Unsigned applications**|Allows the loading of unsigned apps.<br>(Windows 10 only)|  
|**SMS and MMS messaging**|Allow SMS and MMS messaging from the device.<br>(Windows 10 only)|  
|**Removable storage**|Allow use of removable storage, like an SD card on the device.<br> (Windows 10 only)|  
|**Camera**|Allow use of the device camera.<br>(Windows 10 only)|  
|**Near field communication (NFC)**|Allow communication using NFC on the device.<br> (Windows 10 only)|  
|**AntiTheft mode**|Controls whether Windows 10 AntiTheft mode is enabled.<br>(Windows 10 only)|
|**Allow USB connection**|Controls whether devices can access external storage devices through a USB connection.<br>(Windows 10 only)|  
|**Profile file**|Provisions a VPN profile for Windows RT devices.<br>(Windows 8 only)|  
|**Profile name**|Provisions a VPN profile for Windows RT devices.<br>(Windows 8 only)|  
|**Profile for all users**|Provisions a VPN profile for Windows RT devices.<br>(Windows 8 only)|  

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
|**Device management while roaming**|Allows the device to be managed by Configuration Manager when it is roaming.<br>(Windows 10 only)|  
|**Software download while roaming**|Allows the download of apps and software when roaming.<br>(Windows 10 only)|  
|**Email download while roaming**|Allows e-mail downloads when roaming.<br>(Windows 10 only)|  
|**Data roaming**|Allow roaming between networks when accessing data.|
|**VPN over cellular**|Controls whether the device can access VPN connections when connected to a cellular network.<br>(Windows 10 only)|
|**VPN roaming over cellular**|Controls whether the device can access VPN connections when roaming on a cellular network.<br>(Windows 10 only)|

###  Encryption  

|Setting name|Details|  
|------------------|-------------|  
|**Storage card encryption**|Require any storage cards used with the device to be encrypted.<br>(Windows 10 only)|  
|**File encryption on device**|Requires that files on the device are encrypted.|  
|**Require email signing**|Requires that emails are signed before they are sent.<br>(Windows 10 only)|  
|**Signing algorithm**|Select the signing algorithm for signed emails.<br>(Windows 10 only)|  
|**Require email encryption**|Requires that emails are encrypted before they are sent.<br>(Windows 10 only)|  
|**Encryption algorithm**|Select the algorithm for encrypting emails.<br>(Windows 10 only)|  

###  Wireless communications  
 These settings are for devices running Windows 10 and later only.  

|Setting name|Details|  
|------------------|-------------|  
|**Wireless network connection**|Enable or disable the devices Wi-Fi capability.|  
|**Wi-Fi tethering**|Lets users use their device as a mobile hotspot.|  
|**Offload data to Wi-Fi when possible**|Configure this to use the Wi-Fi connection on the device when possible.|  
|**Wi-Fi hotspot reporting**|Sends information about Wi-Fi connections to help the user discover nearby connections.|  
|**Manual Wi-Fi configuration**|Controls whether the user can configure their own Wi-Fi connections, or whether they can only use connections configured by a Wi-Fi profile.|  

#### To configure a wireless network connection  

1.  On the **Configure mobile device wireless communication settings** page, click **Add**.  

2.  In the **Wireless Network Connection** dialog box, specify the following information about the wireless connection that will be provisioned on mobile devices:  

|Setting|More information|  
|-------------|----------------------|  
|**Network name (SSID)**|Enter the name of the Wi-Fi network.|  
|**Network connection**|Choose from **Internet** or **Work**.|  
|**Authentication**|Choose the authentication method for the wireless connection from:<br>- **Open**<br>-                             **Shared**<br>- **WPA**<br>- **WPA-PSK**<br>- **WPA2**<br>- **WPA2-PSK**|  
|**Data encryption**|Choose the encryption method used by this connection. The values you can select will differ depending on the **Authentication** method you selected:<br>- **Disabled**<br>- **WEP**<br>- **TKIP**<br>- **AES**|  
|**Key index**|Select a key index from **1** to **4** that will be used with a **Data encryption** setting of **WEP**.|  
|**This network connects to the Internet**|Select this option if you want to supply proxy settings that let mobile devices on a wireless connection connect to the Internet.|  
|**Proxy server settings**|Specify as required, **Server** and **Port** settings for **HTTP**, **WAP** and **Sockets**.|  
|**Enable 802.1X network access**|Select this option if you want to secure the connection by specifying an EAP type.|  
|**EAP type**|Choose the EAP type to use from:<br>- **PEAP**<br>- **Smart card or certificate**|  


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
|**Network firewall**|Enables or disables Windows Firewall.<br>(Windows 8.1 only)|  
|**Updates (Windows 8.1 and earlier)**|Choose how Windows software updates will be downloaded to computers. For example, you can automatically download updates, but let the user choose when to install them.|  
|**Minimum classification of updates**|Choose the minimum classification of updates that will be downloaded to Windows computers, **None**, **Important**, or **Recommended**.|  
|**Updates (Windows 10)**|Choose how Windows software updates will be downloaded to computers. For example, you can automatically download updates, but let the user choose when to install them.<br>(Windows 10 only)|  
|**Install day**|Choose the day when updates will be installed.<br>(Windows 10 only)|  
|**Install time**|Choose the time when updates will be installed.<br>(Windows 10 only)|  
|**SmartScreen**|Enable or disable Windows Smart Screen.|  
|**Virus protection**|Select to ensure that antivirus software is installed on the device.|  
|**Virus protection signatures are up to date**|Select to ensure that the antivirus signature files are up to date.|  
|**Pre-release features**|Allows Microsoft to deploy pre-release settings and features to the device.<br>(Windows 10 only)|  
|**Manual root certificate installation**|(Windows 10 only)|
|**Allow manual unenrollment**|Lets the user manually delete the workplace account from the device.<br>(Windows 10 only)|

###  Windows Server Work Folders  
 These settings are for devices running Windows 8.1 and Windows 10.  

|Setting name|Details|  
|------------------|-------------|  
|**Work Folders URL**|Configures the location of a Windows Server work folder that users can connect to from their device.|  

### Windows 10 Team  
 These settings are for devices running Windows 10 Team only.  

|Setting name|Details|  
|------------------|-------------|  
|**Allow screen to wake automatically when sensors detect someone in the room**|Allows the device to wake automatically when its sensor detects someone in the room.|  
|**Required PIN for wireless projection**|Specifies whether you must enter a PIN before you can use the wireless projection capabilities of the device.|  
|**Maintenance Window**|Configures the window when updates can take place to the device. You can configure the start time of the window and the duration (from 1-5 hours).|
|**Azure Operational Insights**|Azure Operational Insights , part of the Microsoft Operations Manager suite collects, stores, and analyzes log file data from Windows 10 Team devices.<br>To connect to Azure Operational insights, you must specify a **Workspace ID** and a **Workspace Key**.|
|**Miracast wireless projection**|Enable this option if you want to let the Windows 10 Team device use Miracast enabled devices to project.<br>If you enable this option, from **Choose Miracast channel** select the Miracast channel used to project content.|
|**Meeting information displayed on welcome screen**|If you enable this option, you can choose the information that will be displayed on the **Meetings** tile of the Welcome screen. You can:<br>- **Show organizer and time only**<br>- **Show organizer, time and subject (subject hidden for private meetings)**|
|**Lockscreen background image URL**|Enable this setting to display a custom background on the **Welcome** screen of Windows 10 Team devices from the URL you specify.<br>The image must be in PNG format and the URL must begin with **https://**.|

### Windows Information Protection
 These settings are for devices running Windows 10 only.

With the increase of employee-owned devices in the enterprise, there’s also an increasing risk of accidental data leaks through apps and services, like email, social media, and the public cloud, which are outside of the enterprise’s control. For example, when an employee sends the latest engineering pictures from their personal email account, copies and pastes product info into a tweet, or saves an in-progress sales report to their public cloud storage.

Windows Information Protection (WIP) helps to protect against this potential data leakage without otherwise interfering with the employee experience. WIP also helps to protect enterprise apps and data against accidental data leaks on enterprise-owned devices and personal devices that employees bring to work without requiring changes to your environment or other apps.

 Configuration Manager WIP configuration items manage the list of apps protected by WIP, enterprise network locations, protection level, and encryption settings.

For information about how to configure Windows Information Protection with Configuration Manager, see [Protect your enterprise data using Windows Information Protection (WIP)](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip).

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
