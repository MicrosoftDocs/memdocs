---
title: Manage devices with on-premises MDM
titleSuffix: Configuration Manager
description: Protect device data with full wipe, selective wipe, remote lock, or passcode reset by using Configuration Manager on-premises mobile device management (MDM).
ms.date: 08/14/2018
ms.subservice: mdm
ms.service: configuration-manager
ms.topic: how-to
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Manage devices and protect data with on-premises MDM in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Mobile devices can store sensitive data and provide easy access to many organizational resources. To help protect devices and data, use Configuration Manager for the following device management actions:

- **Full wipe**: Restore the device to its factory settings

- **Selective wipe**: Remove only organizational data

- **Passcode reset**: Remove or reset the passcode when a user forgets it

- **Remote lock**: Help secure a device that might be lost

## Full wipe  

When you need to secure a lost device or when you retire a device from active use, you can start a full wipe on it. This action restores the device to its factory defaults. It removes all organizational and user data and settings.

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, and choose the **Devices** node. You can also choose **Device Collections** and select a collection of which the device is a member.

1. Select the device that you want to wipe.

1. On the ribbon, in the Device group, select **Remote Device Actions**, and then choose **Retire/Wipe**.

1. In the **Retire from Configuration Manager** window, select the option to **Wipe the mobile device and retire it from Configuration Manager**.

## Selective wipe

To remove only organizational data from a device, start a selective wipe.

### Behaviors by OS version

The following tables describe what data is removed and the effect on data that remains on the device after a selective wipe.

#### Windows 10, Windows 8.1, Windows RT 8.1, and Windows RT

|Content|Selective wipe behavior|  
|-------|--------|
|Apps and associated data installed by Configuration Manager|It uninstalls the apps, and removes any sideloading keys. It revokes the encryption key for apps that use Windows Selective Wipe, and the data is no longer accessible.|
|VPN and Wi-Fi profiles|Removes the profiles|
|Certificates|Removes and revokes the certificates|
|Settings|Removes requirements|
|Email profiles|Removes email that's EFS-enabled, which includes the Mail app for Windows email and attachments.|

#### Windows 10 Mobile, Windows Phone 8.0, and Windows Phone 8.1

|Content|Selective wipe behavior|  
|-------|--------|
|Company apps and associated data installed by Configuration Manager|It uninstalls the apps and removes organizational app data.|
|VPN and Wi-Fi profiles|Removes the profiles for Windows 10 Mobile and Windows Phone 8.1|
|Certificates|Removes the certificates for Windows Phone 8.1|
|Email profiles|Removes the profiles (except Windows Phone 8.0)|

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

### Start a selective wipe

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, and choose the **Devices** node. You can also choose **Device Collections** and select a collection of which the device is a member.

1. Select the device that you want to wipe.

1. On the ribbon, in the Device group, select **Remote Device Actions**, and then choose **Retire/Wipe**.

1. In the **Retire from Configuration Manager** window, select the following option: **Wipe company content and retire the mobile device from Configuration Manager**.

### Recommendations for selective wipe

- For a successful wipe of email, set up email profiles to Windows Phone 8.1 devices.

- For a successful wipe of apps, make sure the apps are distributed through mobile device app management.

## Passcode reset

If a user forgets their passcode, use this action to force a new temporary passcode on the device. You can also remove the passcode entirely. The following table lists how passcode reset works on different mobile platforms.

| OS version | Passcode reset |
|------------|----------------|
| Windows 10 | Not supported |
| Windows 10 mobile | Supported, excluding Microsoft Entra joined devices |
| Windows Phone 8 and Windows Phone 8.1 | Supported |
| Windows RT 8.1 | Not supported |
| Windows 8.1 | Not supported |

> [!Note]
> Start the passcode reset action from the top-level site. For example, if you use a central administration site, you can only do the action on that site. If you're using a standalone primary site, you can only do the action from that site.

### Remotely reset the passcode on a mobile device

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, and choose the **Devices** node. You can also choose **Device Collections** and select a collection of which the device is a member.

1. Select the device or devices on which to reset the passcode.

1. On the ribbon, in the Device group, select **Remote Device Actions**, and then choose **Passcode Reset**.  

### Show the state of the passcode reset  

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, and choose the **Devices** node. You can also choose **Device Collections** and select a collection of which the device is a member.

1. Select the device or devices on which to show the state of the passcode reset.

1. On the ribbon, in the Device group, select **Remote Device Actions**, and then choose **Show Passcode State**.  

## Remote lock

If a user loses their device, you can lock the device remotely. The following table lists how remote lock works on different mobile platforms.  

|OS version|Remote lock|
|----------|-----------|
|Windows 10|Not supported|
|Windows Phone 8 and Windows Phone 8.1|Supported|
|Windows RT 8.1|Supported, if the current user of the device is the same user who enrolled the device.|
|Windows 8.1|Supported, if the current user of the device is the same user who enrolled the device.|

> [!Note]
> Start the remote lock action from the top-level site. For example, if you use a central administration site, you can only do the action on that site. If you're using a standalone primary site, do the action from that site.

### Remotely lock a mobile device

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, and choose the **Devices** node. You can also choose **Device Collections** and select a collection of which the device is a member.

1. Select the device or devices to lock.

1. On the ribbon, in the Device group, select **Remote Device Actions**, and then choose **Remote Lock**. Confirm the action.

### Show the state of the remote lock

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, and choose the **Devices** node. You can also choose **Device Collections** and select a collection of which the device is a member.

1. Select the device on which to show the state of the remote lock.

1. On the ribbon, in the Device group, select **Remote Device Actions**, and then choose **Show Remote Lock State**.
