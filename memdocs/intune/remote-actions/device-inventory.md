---
# required metadata

title: View device details with Microsoft Intune
description: View your device details, including operating systems, storage space, manufacturer, and model. Get a list of installed apps, check compliance policies, and set up TeamViewer with Microsoft Intune in Azure. Similar to viewing inventory of the devices you manage.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 04/29/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

#ms.reviewer: dougeby
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: 
  - M365-identity-device-management
  - highpri
---

# See device details in Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

The **Devices** feature provides additional details into the devices you manage, including their hardware and the apps installed.

This article shows you how to view all your devices, and their properties in the Azure portal.

## View the device details

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **All devices** > select one of your listed devices to open its details:

   - **Overview** shows the device name, and lists some key properties of the device, like whether it's a personal or corporate device, serial number, primary user, and more. You can do the following on the device (depending on the device platform):
      - [Retire](devices-wipe.md#retire)
      - [Wipe](devices-wipe.md#wipe)
      - [Delete](devices-wipe.md#delete-devices-from-the-intune-portal)
      - [Remote lock](device-remote-lock.md)
      - [Sync](device-sync.md)
      - [Reset passcode](device-passcode-reset.md)
      - [Restart](device-restart.md) 
      - [Fresh Start](device-fresh-start.md) (Windows only)
      - [Autopilot reset](/windows/deployment/windows-autopilot/windows-autopilot-reset#reset-devices-with-remote-windows-autopilot-reset) (Windows only)
      - [Quick scan](../configuration/device-restrictions-windows-10.md) (Windows 10 only)
      - [Full scan](../configuration/device-restrictions-windows-10.md) (Windows 10 only)
      - [Update Windows Defender security intelligence](/windows/security/threat-protection/microsoft-defender-antivirus/manage-protection-updates-microsoft-defender-antivirus)
      - [BitLocker key rotation](../protect/encrypt-devices.md#to-rotate-the-bitlocker-recovery-key)
      - [Rename device](device-rename.md)
      - [New Remote Assistance Session](./teamviewer-support.md)
   - Use **Properties** to assign a [device category you create](../enrollment/device-group-mapping.md), and change ownership of the device to a personal device, or a corporate device.
   - **Hardware** includes many details about the device, like the device ID, operating system and version, storage space, and more details.
   - **Discovered apps** lists all the apps that Intune found installed on the device, and the app versions. For more information, see [Intune discovered apps](../apps/app-discovered-apps.md).
   - **Device compliance** lists all assigned compliance policies, and if the device is compliant or not compliant.
   - **Device configuration** shows all device configuration policies assigned to the device, and if the policy succeeded or failed.
   - **App configuration**
   - **Recovery keys** shows available BitLocker keys found for the device
   - **Managed apps** lists all the managed apps that Intune configured and has deployed to the device.

## Hardware device details

Depending on the carrier used by the devices, not all details might be collected.

> [!Note]  
>Hardware and Software inventory is refreshed in the Intune service every 7 days, starting from the date of enrolment. 

|Detail|Description|Platform|
|--------------|----------------------|----|  
|Name|The name of the device.|Windows, iOS, Android|
|Management name|The device name used only in the console. Changing this name won't change the name on the device.|Windows, iOS, Android <br/><br/> NOTE: Management names will not automatically populate for Android Enterprise dedicated, fully managed, and corporate-owned with work profile devices that were enrolled before November 2021. However, the admin may still edit the management name.|
|UDID|The device's Unique Device identifier.|Windows, iOS|
|Intune Device ID|A GUID that uniquely identifies the device.|Windows, iOS, Android|
|Serial number|The device's serial number from the manufacturer.|Windows, iOS, iPadOS, Android <br/><br/> Intune doesn't display serial number for Android personally-owned work profile devices running Android 12 and newer.|
|Shared device|If **Yes**, the device is shared by more than one user.|Windows, iOS|
|User approved enrollment|If **Yes**, then the device has user approved enrollment that lets admins manage certain security settings on the device.|Windows, iOS|
|Operating system|The operating system used on the device.|Windows, iOS, Android|
|Operating system version|The version of the operating system on the device.|Windows, iOS, iPadOS, Android|
|Operating system language|The language set for the operating system on the device.|Windows, iOS, Android|
|Build number|The operating system's build number.|Android|
|Security patch level|The security patch level for the device.|Android|
|Total storage space|The total storage space on the device (in gigabytes).|Windows, iOS|
|Free storage space|The unused storage space on the device (in gigabytes).|Windows, iOS|
| PowerPrecision+ Battery Health | State-of-Health rating as determined by Zebra (PowerPrecision+ batteries only). | Android |
| PowerPrecision Battery Charge Cycles Consumed | Number of full charge cycles consumed as determined by Zebra (PowerPrecision batteries only). | Android |
| Last Battery Check-in | Date of last check-in for battery last found in the device as determined by Zebra (PowerPrecision and PowerPrecision+ batteries only). | Android |
| Battery Serial Number | Serial number of the battery pack last found in the device as determined by Zebra (PowerPrecision and PowerPrecision+ batteries only). | Android |
|IMEI|The device's International Mobile Equipment Identity.|Windows, iOS/iPadOS, Android <br/><br/> NOTE: Intune doesn't display IMEI for Android personally-owned work profile devices running Android 12 and newer|
|MEID|The device's mobile equipment identifier.|Windows, iOS/iPadOS, Android <br/><br/> NOTE: Intune doesn't display MEID for Android personally-owned work profile devices running Android 12 and newer|
|Manufacturer|The manufacturer of the device.|Windows, iOS/iPadOS, Android|
|Model|The model of the device.|Windows, iOS/iPadOS, Android|
|Phone number|The phone number assigned to the device.|Windows, iOS/iPadOS, Android <br/><br/> NOTE: Reporting for phone number is not supported for Android Enterprise corporate-owned work profile devices. For Android Enterprise fully managed and dedicated devices, reporting for phone number is supported; however, certain SIM cards will not write the data and therefore the phone number won't get reported in those cases.|
|Subscribe carrier|The device's wireless carrier.|Windows, iOS/iPadOS, Android|
|Cellular technology|The radio system used by the device.|Windows, iOS/iPadOS, Android|
|Wi-Fi MAC|The device's Media Access Control address.|Windows, iOS/iPadOS, Android<br><br>**NOTE**: As of October 2021, Intune doesn't display Wi-Fi MAC addresses for newly enrolled personally-owned work profile devices and devices managed with device administrator running Android 9 and above. |
|Ethernet MAC|The primary Ethernet MAC address for the device. For macOS devices with no ethernet, the device will report the Wi-Fi MAC address.|macOS|
|ICCID|The Integrated Circuit Card Identifier, which is a SIM card's unique identification number.|Windows, iOS/iPadOS, Android<br/><br/>ICCID isn't inventoried on Android Enterprise Dedicated, Fully Managed, or Corporate-Owned Work Profile devices.|
|EID|The eSIM identifier, which is a unique identifier for the embedded SIM (eSIM) for cellular devices that have an eSIM.|iOS/iPadOS|
|Wi-Fi IPv4 address|The device's IPv4 address.|Android Enterprise fully managed, dedicated and corp-owned work profiles.<br/><br/>**NOTE**: Any change to IPv4 or subnet ID may take up to 8 hours to reflect in MEM portal from the time that network changes on device.|
|Wi-Fi subnet ID|The device's subnet ID.|Android Enterprise fully managed, dedicated and corp-owned work profiles.<br/><br/>**NOTE**: Any change to IPv4 or subnet ID may take up to 8 hours to reflect in MEM portal from the time that network changes on device.|
|Enrolled date|The date and time that the device was enrolled in Intune.|Windows, iOS/iPadOS, Android|
|Last contact|The date and time that the device last connected to Intune.|Windows, iOS/iPadOS, Android|
|Activation lock bypass code|The code that can be used to disable the activation lock.|iOS|
|Azure AD registered|If **Yes**, the device is registered with Azure Directory.|Windows, iOS/iPadOS, Android|
|Intune registered|If **Yes**, the device is registered with Intune|Windows, iOS/iPadOS, Android|
|Compliance|The device's compliance state.|Windows, iOS/iPadOS, Android|
|EAS activated|If **Yes**, then the device is synchronized with an Exchange mailbox.|Windows, iOS/iPadOS, Android|
|EAS activation ID|The device's Exchange ActiveSync identifier.|Windows, iOS/iPadOS, Android|
|Supervised|If **Yes**, administrators have enhanced control over the device.|iOS/iPadOS|
|Encrypted|If **Yes**, the data stored on the device is encrypted.|Windows, iOS/iPadOS, Android|

> [!Note]  
> For Windows 10 devices that are registered with [Windows Autopilot service](../../autopilot/add-devices.md), Enrolled date might display the time when devices were registered with Autopilot instead of the time when they were enrolled.
> For Android Enterprise corporate-owned work profile devices, reporting for phone number is not supported. For Android Enterprise fully managed and dedicated devices, reporting for phone number is supported; however, certain SIM cards will not write the data and therefore the phone number won't get reported in those cases.

## Next steps

See what else you can do to [manage your devices](device-management.md) with Intune.
