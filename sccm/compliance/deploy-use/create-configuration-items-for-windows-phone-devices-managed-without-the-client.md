---
title: "How to create configuration items for Windows Phone devices managed without the System Center Configuration Manager client | System Center Configuration Manager"
ms.custom: na
ms.date: 11/18/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology: 
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fae7f9e0-d5e7-422f-a6ed-6f6d73f6a617
caps.latest.revision: 13
caps.handback.revision: 0
author: robstackmsftms.author: robstackmanager: angrobe

---
# How to create configuration items for Windows Phone devices managed without the System Center Configuration Manager client*Applies to: System Center Configuration Manager (Current Branch)*
Use the System Center Configuration Manager **Windows Phone** configuration item to manage settings for Windows Phone devices that are enrolled in Microsoft Intune or managed on-premises by Configuration Manager.  
  
## Create a Windows Phone configuration item  
  
1.  In the Configuration Manager console, click **Assets and compliance** > **Compliance Settings** > **Configuration Items**.  
  
3.  On the **Home** tab, in the **Create** group, click **Create Configuration Item**.  
  
4.  On the **General** page of the **Create Configuration Item Wizard**, specify a name, and optional description for the configuration item.  
  
5.  Under **Specify the type of configuration item that you want to create**, select **Windows Phone**.  
  
6.  Click **Categories** if you create and assign categories to help you search and filter configuration items in the Configuration Manager console.  
  
7.  On the **Supported Platforms** page, select the specific Windows Phone platforms that will evaluate the configuration item.  
  
8.  On the **Device Settings** page, select the settings group that you want to configure. See [Windows Phone configuration item settings reference](/sccm/compliance/deploy-use/create-configuration-items-for-windows-phone-devices-managed-without-the-client#windows-phone-configuration-item-settings-reference) in this topic for details, and then click **Next**.  
  
    > [!TIP]  
    >  If the setting that you want is not listed, select the **Configure additional settings that are not in the default setting groups check box**.  
  
9. On each settings page, configure the settings you require, and whether you want to remediate them when they are not compliant on devices (when this is supported).  
  
10. For each settings group, you can also configure the severity that will be reported (in Configuration Manager reports) when a configuration item is found to be noncompliant from:  
  
    -   **None** - Devices that fail this compliance rule do not report a failure severity.  
  
    -   **Information** - Devices that fail this compliance rule report a failure severity of **Information**.  
  
    -   **Warning** - Devices that fail this compliance rule report a failure severity of **Warning**.  
  
    -   **Critical** - Devices that fail this compliance rule report a failure severity of **Critical**.  
  
    -   **Critical with event** - Devices that fail this compliance rule report a failure severity of **Critical**.   
  
11. On the **Platform Applicability** page, review any settings that are not compatible with the supported platforms you selected earlier. You can go back and remove these settings, or you can continue.  
  
    > [!TIP]  
    >  Unsupported settings are not assessed for compliance.  
  
12. Complete the wizard.  
  
 You can view the new configuration item in the **Configuration Items** node of the **Assets and Compliance** workspace.  
  
##  Windows Phone configuration item settings reference  
  
### Password  
 These settings apply to both Windows Phone 8 and Windows Phone 8.1.  
  
|Setting|Details|  
|-------------|-------------|  
|**Require password settings on devices**|Require a password on supported devices.|  
|**Minimum password length (characters)**|The minimum length for the password.|  
|**Password expiration in days**|The number of days before a password must be changed.|  
|**Number of passwords remembered**|Prevents re-using previously used passwords.|  
|**Number of failed logon attempts before device is wiped**|Wipes the device if this number of login attempts fail.|
|**Idle time before device is locked**|Specifies the amount of time a device must remain idle before the screen is automatically locked.|  
|**Password complexity**|Choose whether you can specify a PIN such as ‘1234’, or whether you must supply a strong password.| 
|**Allow simple passwords**|Specifies that simple passwords such as ‘0000’ and ‘1234’ can be used.| 
|**Send password recovery PIN to Exchange Server**|-|  
  
### Device  
  
|Setting|Details|  
|-------------|-------------|  
|**Screen capture**|Allow the user to take a screenshot of the device display.<br /><br /> (Windows Phone 8.1 only)|  
|**Diagnostic data submission**|Allow submission of app log files.|  
|**Geolocation**|Allow the device to use location services information.<br /><br /> (Windows Phone 8.1 only)|  
|**Copy and Paste**|Use copy and paste to transfer data between apps.<br /><br /> (Windows Phone 8.1 only)|  
|**Bluetooth**|Allows use of the Bluetooth capability of the device.|  
  
### Email management  
 These settings apply to both Windows Phone 8 and Windows Phone 8.1.  
  
|Setting|Details|  
|-------------|-------------|  
|**POP and IMAP email**|Allows connection to email accounts that use the POP and IMAP standards.|  
|**Maximum time to keep email**|How long to keep email before it is deleted from the server.|  
|**Allowed message formats**|Specify whether user emails can be HTML, or plain text only.|  
|**Maximum size for plain text email (automatically downloaded)**|Controls the maximum size of plain text emails when automatically downloaded.|  
|**Maximum size for HTML email (automatically downloaded)**|Controls the maximum size of HTML emails when automatically downloaded.|  
|**Maximum size of an attachment (automatically downloaded)**|Configures the maximum size email that will be automatically downloaded.|  
|**Calendar synchronization**|Lets users synchronize calendar appointments in addition to email.|  
|**Custom email account**|Allow using a non-Microsoft account on the device.|  
|**Make Microsoft Account optional in Windows Mail app**|-|  
  
### Store  
 These settings apply to Windows Phone 8.1 devices only.  
  
|Setting|Details|  
|-------------|-------------|  
|**Application store**|Allows access to the app store on the device.|  
  
### Browser  
 These settings apply to both Windows Phone 8 and Windows Phone 8.1.  
  
|Setting|Details|  
|-------------|-------------|  
|**Allow web browser**|User can change the default Internet browser.|  
|**Autofill**|User can change autocomplete settings in the browser.|  
|**Active scripting**|Browser can run scripts, such as Active X scripts.|  
|**Plug-ins**|User can add plug-ins to Internet Explorer.|  
|**Pop-up blocker**|Enables or disables the browser pop-up blocker.|  
|**Cookies**|Allow cookies to be saved on the device.|  
|**Fraud warning**|Enable or disable warnings of potential fraudulent websites.|  
  
### Internet Explorer  
 These settings apply to both Windows Phone 8 and Windows Phone 8.1.  
  
|Setting|Details|  
|-------------|-------------|  
|**Always send Do Not Track header**|Prevents browsing information from being sent to third-party sites.|  
|**Intranet security zone**|-|  
|**Security level for Internet zone**|Configure the security level for the Internet zone.|  
|**Security level for intranet zone**|Configure the security level for the intranet zone.|  
|**Security level for trusted sites zone**|Configure the security level for the trusted sites zone.|  
|**Security level for restricted sites zone**|Configure the security level for the restricted sites zone.|  
|**Namespaces for intranet zone**|-|  
|**Go to intranet site for single word entry**|Enables or disables the setting that allows Internet Explorer to automatically go to an Intranet site if a valid site name is entered without a preceding HTTP:|  
|**Enterprise mode menu option**|Allow users to activate and deactivate Enterprise Mode from the Internet Explorer **Tools** menu.|  
|**Logging report location (URL)**|Specify a URL where visited websites will be logged when Enterprise Mode is active.|  
|**Enterprise Mode site list location (URL)**|Specify the location of the list of websites that will use Enterprise Mode when it is active.|  
  
### Cloud  
  
|Setting|Details|  
|-------------|-------------|  
|**Settings synchronization**|Allows synchronization of settings between devices.|  
|**Credentials synchronization**|Allows synchronization of credentials between devices.|  
|**Microsoft Account**|Allow the use of a Microsoft account on the device.<br /><br /> (Windows Phone 8.1 only)|  
|**Settings synchronization over metered connections**|Allow settings to be synchronized when the Internet connection is metered.|  
  
### Security  
  
|Setting|Details|  
|-------------|-------------|  
|**Unsigned file installation**|Allows the loading of unsigned files.|  
|**Unsigned applications**|Allows the loading of unsigned apps.|  
|**SMS and MMS messaging**|Allow SMS and MMS messaging from the device.|  
|**Removable storage**|Allow use of removable storage, like an SD card on the device.|  
|**Camera**|Allow use of the device camera.|  
|**Near field communication (NFC)**|Allow communication using NFC on the device.<br /><br /> (Windows Phone 8.1 only)| 
|**Allow USB connection**|Controls whether devices can access external storage devices through a USB connection.| 
  
### Peak synchronization  
 These settings apply to both Windows Phone 8 and Windows Phone 8.1.  
  
|Setting|Details|  
|-------------|-------------|  
|**Specify peak time**|Configure the peak time for mobile device synchronization.|  
|**Peak synchronization frequency**|Configure how often synchronization occurs during the peak hours you configured.|  
|**Off-peak synchronization frequency**|Configure how often synchronization occurs outside of the peak hours you configured.|  
  
### Roaming  
 These settings apply to both Windows Phone 8 and Windows Phone 8.1.  
  
|Setting|Details|  
|-------------|-------------|  
|**Device management while roaming**|Allows the device to be managed by Configuration Manager when it is roaming.|  
|**Software download while roaming**|Allows the download of apps and software when roaming.|  
|**Email download while roaming**|Allows e-mail downloads when roaming.|  
|**Data roaming**|Allow roaming between networks when accessing data.|  
  
### Encryption  
 These settings apply to both Windows Phone 8 and Windows Phone 8.1.  
  
|Setting|Details|  
|-------------|-------------|  
|**Storage card encryption**|Require any storage cards used with the device to be encrypted.|  
|**File encryption on device**|Requires that files on the mobile device are encrypted.|  
|**Require email signing**|Require emails to be signed before they are sent.|  
|**Signing algorithm**|Select the algorithm used to sign emails.|  
|**Require email encryption**|Require emails to be encrypted before they are sent.|  
|**Encryption algorithm**|Select the algorithm used to encrypt emails.|  
  
###  Wireless communications  
 These settings apply to both Windows Phone 8 and Windows Phone 8.1.  
  
|Setting name|Details|  
|------------------|-------------|  
|**Wireless network connection**|Enable or disable the devices Wi-Fi capability.|  
|**Wi-Fi tethering**|Let’s users use their device as a mobile hotspot.|  
|**Offload data to Wi-Fi when possible**|Configure this to use the Wi-Fi connection on the device when possible.|  
|**Wi-Fi hotspot reporting**|Sends information about Wi-Fi connections to help the user discover nearby connections.|  
  
#### To configure a wireless network connection  
  
1.  On the **Configure mobile device wireless communication settings** page, click **Add**.  
  
2.  In the **Wireless Network Connection** dialog box, specify the following information about the wireless connection that will be provisioned on mobile devices, then click **OK**:

|Setting|More information|  
|-------------|----------------------|  
|**Network name (SSID)**|Enter the name of the Wi-Fi network.|  
|**Network connection**|Choose from **Internet** or **Work**.|  
|**Authentication**|Choose the authentication method for the wireless connection from:<br><br>- **Open**<br>-                    **Shared**<br>- **WPA**<br>- **WPA-PSK**<br>- **WPA2**<br>- **WPA2-PSK**|  
|**Data encryption**|Choose the encryption method used by this connection. The values you can select will differ depending on the **Authentication** method you selected:<br><br>- **Disabled**<br>- **WEP**<br>- **TKIP**<br>- **AES**|  
|**Key index**|Select a key index from **1** to **4** that will be used with a **Data encryption** setting of **WEP**.|  
|**This network connects to the Internet**|Select this option if you want to supply proxy settings that let mobile devices on a wireless connection connect to the Internet.|  
|**Proxy server settings**|Specify as required, **Server** and **Port** settings for **HTTP**, **WAP** and **Sockets**.|  
|**Enable 802.1X network access**|Select this option if you want to secure the connection by specifying an EAP type.|  
|**EAP type**|Choose the EAP type to use from:<br><br>- **PEAP**<br>- **Smart card or certificate**|  

  
###  Certificates  
 Let’s you import certificates to install on mobile devices.  
  
 Click **Import**, and then specify the following values:  
  
-   **Certificate file** – Click **Browse** and then select the certificate file with the extension **.cer** that you want to import.  
  
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
 These settings apply to both Windows Phone 8 and Windows Phone 8.1.  
  
|Setting|Details|  
|-------------|-------------|  
|**User Account Control**|Enables or disables Windows User Account Control on the device.|  
|**Network firewall**|Enables or disables Windows Firewall.|  
|**Updates**|Choose how Windows software updates will be downloaded to computers. For example, you can automatically download updates, but let the user choose when to install them.|  
|**Minimum classification of updates**|Choose the minimum classification of updates that will be downloaded to Windows computers, **None**, **Important**, or **Recommended**.|  
|**SmartScreen**|Enable or disable Windows Smart Screen.|  
|**Virus protection**|Ensure that the device is protected by antivirus software|  
|**Virus protection signatures are up to date**|Ensure that the antivirus software signatures are up to date.|
|**Allow manual unenrollment**|-|  
  
### Windows Server Work Folders  
 These settings apply to both Windows Phone 8 and Windows Phone 8.1.  
  
|Setting|Details|  
|-------------|-------------|  
|**Work Folders URL**|Configures the location of a Windows Server work folder that users can connect to from their device.|  
  
### Windows Phone allowed and blocked apps list (Windows Phone 8.1 only)  
 Let’s you specify a list of Windows Phone apps that are compliant, or not compliant in your company. Apps that you specify as blocked cannot be installed by users. If you specify a list of allowed apps, users can only install apps in the list.  
  
 You cannot specify both allowed and blocked apps in the same configuration item.  
  
> [!IMPORTANT]  
>  If you specify a list of allowed apps, you must ensure that the company portal app, and any apps you have deployed to Windows Phone 8.1 devices are in the **Allowed** apps list.  
  
#### To specify an allowed or blocked apps list  
  
1.  On the **Allowed and Blocked Apps list (Windows Phone 8.1)** page, specify the following information:  
  
|Setting|More information|  
|-|-|  
|**Blocked apps list**|Select this option if you want to specify a list of apps that users will not be allowed to install.|  
|**Allowed apps list**|Select this option if you want to specify a list of apps that users are allowed to install.|  
|**Add**|Adds an app to the selected list. Specify a name of your choice, optionally the app publisher, and the URL to the app in the app store.<br /><br /> To specify the URL, from the Windows Phone Store page, search for the app you want to use.<br /><br /> **Example:** Search the store for the **Skype** app. The URL you use will be http://www.windowsphone.com/en-us/store/app/skype/c3f8e570-68b3-4d6a-bdbb-c0a3f4360a51.<br /><br /> For the company portal app, or line of business apps, you do not have to specify a full URL, only the app GUID.|  
|**Edit**|Let’s you edit the name, publisher and URL of the selected app.|  
|**Remove**|Deletes the selected app from the list.|  
|**Import**|Imports a list of apps you have specified in a comma-separated values file. Use the format, application name, publisher, app URL in the file.|  
  

