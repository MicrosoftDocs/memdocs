---
title: "Protect data with remote wipe, lock, or passcode reset"
titleSuffix: "Configuration Manager"
description: "Protect device data with full wipe, selective wipe, remote lock, or passcode reset by using System Center Configuration Manager."
ms.date: 10/27/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: 770da7bd-02dd-474a-9604-93ff1ea0c1e4
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Protect data with remote wipe, lock, or passcode reset by using System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager provides selective wipe, full wipe, remote lock, and passcode reset capabilities. Mobile devices can store sensitive corporate data and provide access to many corporate resources. To help protect devices, you can issue:  

- A full wipe to restore the device to its factory settings.  

- A selective wipe to remove only company data.  

- A remote lock to help secure a device that might be lost.  

- A reset of the device passcode.  

## Full wipe  
You might issue a wipe command to a device when you need to secure a lost device or when you retire a device from active use.  

Issue a **full wipe** to a device to restore the device to its factory defaults. This removes all company and user data and settings. You can do a full wipe on Windows Phone, iOS, Android, and Windows 10 devices.  

> [!NOTE]
> You can only perform a full wipe on company-owned devices.

> [!NOTE]
> Wiping Windows 10 devices on versions earlier than version 1511 with less than 4 GB of RAM might leave the device unresponsive. [Learn more](https://technet.microsoft.com/library/mt592024.aspx#full-wipe-disables-windows-10-devices-with-less-than-4-gb-ram).

#### To initiate a remote wipe from the Configuration Manager console  

1. In the Configuration Manager console, choose **Assets and Compliance** and choose **Devices**. Alternatively, you can choose **Device Collections** and select a collection.  

2. Select the device that you want to retire/wipe.  

3. Choose **Remote Device Actions** in **Device Group**, and then choose **Retire/Wipe**.  

## Selective wipe  
Issue a **selective wipe** to a device to remove only company data. The following table describes, by platform, what data is removed and the effect on data that remains on the device after a selective wipe.  

**iOS**  

|Content removed when you're retiring a device|iOS|  
|--------------------------------------------|---------|  
|Company apps and associated data installed by using Configuration Manager and Intune|Apps are uninstalled. Company app data is removed.|  
|VPN and Wi-Fi profiles|Removed.|  
|Certificates|Removed and revoked.|  
|Settings|Removed, except for: **Allow voice roaming**, **Allow data roaming**, and **Allow automatic synchronization while roaming**.|  
|Management agent|Management profile is removed.|  
|Email profiles|For email profiles set up by Intune, the email account and email are removed.|  

**Android and Android Samsung KNOX Standard**  

|Content removed when you're retiring a device|Android|Samsung KNOX Standard|  
|--------------------------------------------|-------------|------------------|  
|Company apps and associated data installed by using Configuration Manager and Intune|Apps and data remain installed.|Apps are uninstalled.|  
|VPN and Wi-Fi profiles|Removed.|Removed.|  
|Certificates|Revoked.|Revoked.|  
|Settings|Requirements are removed.|Requirements are removed.|  
|Management agent|Device Administrator privilege is revoked.|Device Administrator privilege is revoked.|  
|Email profiles|Not applicable.|For email profiles set up by Intune, the email account and email are removed.|  

**Android for Work**

Doing a selective wipe on an Android for Work device removes the work profile along with all data, apps, and settings in the work profile on that device. This retires the device from management with Configuration Manager and Intune. Full wipe is not supported for Android for Work.

 **Windows 10, Windows 8.1, Windows RT 8.1, and Windows RT**  

|Content removed when you're retiring a device|Windows 10, Windows 8.1 and Windows RT 8.1|  
|---------------------------------|-------------|
|Company apps and associated data installed by using Configuration Manager and Intune|Apps are uninstalled and sideloading keys are removed. Apps that use Windows Selective Wipe will have the encryption key revoked, and data will no longer be accessible.|  
|VPN and Wi-Fi profiles|Removed.|  
|Certificates|Removed and revoked.|  
|Settings|Requirements are removed.|
|Management agent|Not applicable. Management agent is built in.|  
|Email profiles|Email that is EFS-enabled is removed, which includes the Mail app for Windows email and attachments.|  

 **Windows 10 Mobile, Windows Phone 8.0, and Windows Phone 8.1**

|Content removed when you're retiring a device|Windows 10 Mobile, Windows Phone 8 and Windows Phone 8.1|  
|-|-|
|Company apps and associated data installed by using Configuration Manager and Intune|Apps are uninstalled. Company app data is removed.|  
|VPN and Wi-Fi profiles|Removed for Windows 10 Mobile and Windows Phone 8.1.|  
|Certificates|Removed for Windows Phone 8.1.|  
|Management agent|Not applicable. Management agent is built in.|  
|Email profiles|Removed (except Windows Phone 8.0).|  

The following settings are also removed from Windows 10 Mobile and Windows Phone 8.1 devices:  

- **Require a password to unlock mobile devices**  
- **Allow simple passwords**  
- **Minimum password length**  
- **Required password type**
- **Password expiration (days)**  
- **Remember password history**  
- **Number of repeated sign-in failures to allow before the device is wiped**  
- **Minutes of inactivity before password is required**  
- **Required password type – minimum number of character sets**  
- **Allow camera**
- **Require encryption on mobile device**  
- **Allow removable storage**  
- **Allow web browser**  
- **Allow application store**  
- **Allow screen capture**  
- **Allow geolocation**  
- **Allow Microsoft Account**  
- **Allow copy and paste**  
- **Allow Wi-Fi tethering**  
- **Allow automatic connection to free Wi-Fi hotspots**  
- **Allow Wi-Fi hotspot reporting**  
- **Allow factory reset**
- **Allow Bluetooth**  
- **Allow NFC**
- **Allow Wi-Fi**

#### To initiate a remote wipe from the Configuration Manager console  

1. In the Configuration Manager console, choose **Assets and Compliance** and choose **Devices**. Alternatively, you can choose **Device Collections** and select a collection.  

2. Select the device that you want to retire/wipe.  

3. Choose **Remote Device Actions** in **Device Group**, and then choose **Retire/Wipe**.  

## Wiping EFS-enabled content  
Windows 8.1 and Windows RT 8.1 support selective wipe of Encrypting File System (EFS)-encrypted content. The following apply to a selective wipe of EFS-enabled content:  

- Only apps and data that are protected by EFS through the same Internet domain as the Intune account are selectively wiped. For more information, see [Windows Selective Wipe for Device Data Management](http://technet.microsoft.com/library/dn486874.aspx).  

- If any changes are made to the domain associated with EFS, the changes can take up to 48 hours before apps and data that use the new domain can be selectively wiped.  

- Each domain that is registered with Intune is the domain that will be wiped.  

The data and apps that EFS selective wipe currently supports are:  

- Mail app for Windows.  

- Work folders.

- Files and folders encrypted by EFS. For more information, see [Best practices for the Encrypting File System](http://support.microsoft.com/kb/223316).  

### Best practices for selective wipe  

- For a successful wipe of email, set up email profiles to iOS and Windows Phone 8.1 devices.  

- For a successful wipe of apps, make sure the apps are distributed through mobile device app management.  

- For iOS, configure the setting **Allow backup to iCloud** to **Disallow** so that users can’t restore content by using iCloud.  

- If an account has been deactivated, then after one year, Intune will retire the account and a selective wipe will be done.  

##  Passcode reset  
If a user forgets their passcode, you can help them by removing the passcode from a device or by forcing a new temporary passcode on a device. The following table lists how passcode reset works on different mobile platforms.  

| Platform                              | Passcode reset                                                                               |
|---------------------------------------|----------------------------------------------------------------------------------------------|
| iOS                                   | Supported for clearing the passcode from a device. Does not create a new temporary passcode. |
| macOS                                 | Not supported.                                                                               |
| Android                               | Supported on versions earlier than Android 7.0. Creates a temporary passcode.                |
| Android for Work                      | Not supported.                                                                               |
| Windows 10 PCs                        | Not supported.                                                                               |
| Windows 10 mobile                     | Supported, excluding Azure AD joined devices.  |
| Windows Phone 8 and Windows Phone 8.1 | Supported.                                                                                   |
| Windows RT 8.1                        | Not supported.                                                                               |
| Windows 8.1 PCs                       | Not supported.                                                                               |

> [!Note]    
> You must perform the passcode reset action from the top-level site in your environment. For example, if you use a central administration site, you can only perform the action on that site. If you’re using a standalone primary site, you can only perform the action on that site.

#### To reset the passcode on a mobile device remotely in Configuration Manager  

1. In the Configuration Manager console, choose **Assets and Compliance** and choose **Devices**. Alternatively, you can choose **Device Collections** and select a collection.  

2. Select the device or devices on which to reset the passcode.  

3. Choose **Remote Device Actions** in **Device Group**, and then choose **Passcode Reset**.  

#### To show the state of the passcode reset  

1. In the Configuration Manager console, choose **Assets and Compliance** and choose **Devices**. Alternatively, you can choose **Device Collections** and select a collection.  

2. Select the device or devices on which to show the state of the passcode reset.  

3. Choose **Remote Device Actions** in **Device Group**, and then choose **Show Passcode State**.  

## Remote lock  
If a user loses their device, you can lock the device remotely. The following table lists how remote lock works on different mobile platforms.  

|Platform|Remote lock|  
|--------------|-----------------|  
|iOS|Supported.|  
|Android|Supported.|  
|Windows 10|Not supported at this time.|  
|Windows Phone 8 and Windows Phone 8.1|Supported.|  
|Windows RT 8.1 |Supported if the current user of the device is the same user who enrolled the device.|  
|Windows 8.1|Supported if the current user of the device is the same user who enrolled the device.|  

> [!Note]    
> You must perform the remote lock action from the top-level site in your environment. For example, if you use a central administration site, you can only perform the action on that site. If you’re using a standalone primary site, you can only perform the action on that site.

#### To lock a mobile device remotely through the Configuration Manager console  

1. In the Configuration Manager console, choose **Assets and Compliance** and choose **Devices**. Alternatively, you can choose **Device Collections** and select a collection.  

2. Select the device or devices to lock.  

3. Choose **Remote Device Actions** in **Device Group**, and then choose **Remote Lock**.  

#### To show the state of the remote lock  

1. In the Configuration Manager console, choose **Assets and Compliance** and choose **Devices**. Alternatively, you can choose **Device Collections** and select a collection.  

2. Select the device on which to show the state of the remote lock.  

3. Choose **Remote Device Actions** in **Device Group**, and then choose **Show Remote Lock State**.  

### See also  
[Windows Selective Wipe for Device Data Management](http://technet.microsoft.com/library/dn486874.aspx)   
