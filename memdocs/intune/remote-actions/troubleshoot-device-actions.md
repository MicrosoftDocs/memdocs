---
# required metadata

title: Troubleshoot device actions in Microsoft Intune - Azure | Microsoft Docs
description: Get help troubleshooting device action issues.
keywords:
author: erikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/02/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: medium
ms.technology:
ms.assetid: 
ROBOTS:

# optional metadata

#audience:

ms.reviewer: coferro
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-classic
ms.collection: M365-identity-device-management
---

# Troubleshoot device actions in Intune

Microsoft Intune has many actions that help you managed devices. This article provides answers for some common questions that can help you troubleshoot device actions.

## Disable Activation Lock action

### I clicked the "Disable Activation Lock" action in the portal but nothing happened on the device.
This is expected. After starting the Disable Activation Lock action, Intune is requested an updated code from Apple. You'll manually enter the code in the passcode field after your device is on the Activation Lock screen. This code is only valid for 15 days, so be sure to click the action and copy the code before you issue the Wipe.

### Why don't I see the Disable Activation Lock code in the Hardware overview blade of my iOS/iPadOS device?
The most likely reasons include:
- The code has expired and been cleared from the service.
- The device isn't Supervised with the Device Restriction Policy to allow Activation Lock.

You can check on the code in Graph Explorer with the following query:

```GET - https://graph.microsoft.com/beta/deviceManagement/manageddevices('deviceId')?$select=activationLockBypassCode.```

### Why is the Disable Activation Lock action greyed out for my iOS/iPadOS device?
The most likely reasons include: 
- The code has expired and been cleared from the service.
- The device isn't Supervised with the Device Restriction Policy to allow Activation Lock.

### Is the Disable Activation Lock code case sensitive?
No. And you don't need to enter the dashes.

## Remove devices action

### How do I tell who started a Retire/Wipe?
In the the [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Tenant administration** > **Audit logs** > check the **Initiated By** column.
If you don't see an entry, the most likely person to have initiated the action is the user of the device. They probably used the Company Portal app or portal.manage.microsoft.com.

### Why wasn't my application uninstalled after using Retire?
Because it wasn't considered a managed application. In this context, a managed application is an application that was installed by using the Intune service. This includes:
- The app was deployed as Required
- The app was deployed as Available and then installed by the end user from within the Company Portal App.

### Why is Wipe grayed out for Android Enterprise Work Profile devices?
This is expected behavior. Google doesn't allow Factory Resetting of Work Profile devices from the MDM Provider.

### Why can I sign back into my Office apps after my device was retired?
Because retiring a device doesn't revoke access tokens. You can use Conditional Access policies to mitigate this condition.

### How can I monitor a Retire/Wipe action after it was issued?
In the the [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Tenant administration** > **Audit logs**.

### Why do wipes sometimes show as Pending indefinitely?
Devices don't always report their status back to the Intune service before the reset was started. So, the action shows as Pending. If you've confirmed the action was successful, delete the device from the service.

### What happens if I start a retire/wipe on an offline device or a device that hasn't communicated with the service in a while?
The device will remain in **Retire/Wipe Pending** state until the MDM certificate expires. The MDM certificate lasts for one year from enrollment, and automatically renews every year. If the device checks in before the MDM certificate expires, it will be retired/wiped. If the device doesn't check in before the MDM certificate expires, it won't be able to check in to the service. 180 days after the MDM certificate expires, the device will be automatically removed from the Azure portal.


## Reset Passcode action

### Why is the Reset Passcode action greyed out on my Android Device Admin enrolled device?
To combat Ransom ware, Google removed the  passcode reset feature on the Device Admin API (applies to Android version 7.0 or higher devices).

### Why do I get a "Not Supported" message when I issue a passcode reset to my Android 8.0 or later Work Profile enrolled device?
Because the Reset Token hasn't been activated on the device. To activate the Reset Token:
1. You must require a Work Profile passcode in your Configuration Policy.
2. The end user must set an appropriate Work Profile passcode.
3. The end user must accept the secondary prompt to allow passcode reset.
After these steps are complete, you should no longer receive this response.

### Why am I prompted to set a new passcode on my iOS/iPadOS device when I issue the Remove Passcode action?
Because one of your compliance policies requires a passcode.


## Wipe action

### I can’t restart a Windows 10 device after using the wipe action
This can be caused if you use the choose the **Wipe device, and continue to wipe even if devices loses power. If you select this option, please be aware that it might prevent some Windows 10 devices from starting up again.** on a Windows 10 device.

This may be caused when the installation of Windows has major corruption that is preventing the operating system from reinstalling. In such a case, the process fails and leaves the system in the [Windows Recovery Environment]( https://docs.microsoft.com/windows-hardware/manufacture/desktop/windows-recovery-environment--windows-re--technical-reference).

### I can’t restart a BitLocker encrypted device after using the wipe action
This can be caused if you use the choose the **Wipe device, and continue to wipe even if devices loses power. If you select this option, please be aware that it might prevent some Windows 10 devices from starting up again.** option on a BitLocker encrypted device.

To resolve this issue, use bootable media to re-install Windows 10 on the device.


## Next steps

Get [support help from Microsoft](../fundamentals/get-support.md), or use the [community forums](https://social.technet.microsoft.com/Forums/en-US/home?category=microsoftintune).
