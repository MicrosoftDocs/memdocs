---
# required metadata
title: What is NXT?
titleSuffix:
description: What is NXT?
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 11/19/2024
ms.topic: overview
ms.service: windows-365
ms.subservice:
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: sajelaci
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started; intro-hub-or-landing
ms.collection:
- M365-identity-device-management
- tier2
---

# What is NXT?

> [!IMPORTANT]
> This is unfinished draft documentation. Not ready for review.

NXT is the first Cloud PC device. It’s a full stack, purpose-built solution by Microsoft, designed to connect you to the Windows 365 service in seconds. When you sign in to your Cloud PC, you can securely connect to a familiar Windows Desktop in the cloud, and access a responsive, high-quality experience. For IT, it brings a more streamlined management experience, where it can be managed alongside other PCs in Microsoft Intune.

The device is secure by design, featuring an adminless user model, no local data storage, and no local apps. You can’t install or execute any arbitrary software on the device, so you are protected from malware. Security baseline policies are enabled by default, and security features cannot be disabled.

## NXT components

...

## In the box

### Power supply details

## Device specifications

### Compute and connectivity

| Memory | ? |
| Storage | ? |
| Wi-Fi | ? |
| Bluetooth | ? |
| USB | ? |

## Device capabilities

### Control + Alt + Delete

Options on the Control + Alt + Delet menu include:

| Control | Description |
| --- | --- |
| Lock | Locks the local device similar to Windows key + L. Connection to Windows 365 lasts 15 minutes, making it easy to quickly reconnect to your Cloud PC after you reauthenticate. |
| Sign out | Closes your Windows 365 connection and signs out of device.  |
| Task Manager | Opens the Task Manager of your Cloud PC. |
| Connection details | Shows information about the current connection to your Cloud PC. |
| Restore and Troubleshoot | Initiates these processes for your Cloud PC. |
| Quick settings | Opens a small set of essential settings. For details on individual Quick settings, see below. |

### Quick settings

In addition to more settings being configured directly from your Cloud PC for GA release (like display configuration, Bluetooth devices, and sound settings) the following local settings can be quickly configured from the sign-in screen: 

| Control | Description |
| --- | --- |
| Wi-Fi | View and manage Wi-Fi connection. |
| Bluetooth (BT) | View and manage BT devices. Note that you can only add BT devices once authenticated. |
| Accessibility Tools | Turn on/off accessibility tools: Magnifier, Narrator, Contrast themes, On-screen keyboard, and Sticky & Filter keys. Voice access coming soon.  |
| Language | Choose preferred display language. |
| Display | Can only change scale and swap multiple monitor arrangement. GA release to support full display configuration. |
| Privacy and Security | View privacy and security settings for camera, mic, and location. |
| Power button | View power management options for the device. |

### MMR and VDI optimization

NXT supports local redirection of web multimedia content, ensuring a smooth, high-quality experience, just like on a local PC. It is also optimized for online meetings with Microsoft Teams (Teams VDI 2.0), providing highly performant video conferencing. Similarly, we’re working to enable high-fidelity Zoom and Webex meetings in the same way.

### Monitor support

NXT supports two 4K displays with 1 HDMI and 1 Display port connection in the back of the device.

### Peripheral support

The device supports USB and Bluetooth peripherals for:

- keyboard
- mouse
- headphones
- camera

### Ports and connections

On the front panel, there’s a USB-A port and a 3.5 mm audio jack. The back panel includes two USB-A ports, a USB-C port, an Ethernet port, and the power connector. It also includes an HDMI port and a Display Port—both the HDMI and Display Port support one monitor each, up to 4k in resolution. On the side, there is a Kensington lock port to help you physically secure the device. For wireless connectivity, the device supports Wi-Fi 6E and Bluetooth 5.3. 

## Preinstalled software

The device comes pre-installed with a build and will auto-update during off hours when a new build is available.  

## Device certifications

- [Product safety](https://support.microsoft.com/en-us/windows/product-safety-warnings-and-instructions-726eab87-f471-4ad8-48e5-9c25f68927ba)
- [Product safety warnings and instructions](https://support.microsoft.com/en-us/windows/product-safety-warnings-and-instructions-726eab87-f471-4ad8-48e5-9c25f68927ba)

## Warranty information


## Package dimensions

| Measurement | Units metric | Units imperial |
| --- | --- | --- |
| Unit length | | |
| Unit width | | |
| Unit depth | | |
| Unit weight | | |
| Exterior shipper length | | |
| Exterior shipper width | | |
| Exterior shipper depth | | |
| Exterior shipper weight | | |

- Unit: The retail-style box NXT is sold in.
- Exterior shipper: The protective shipping packaging around unit.

## Finding the serial number

The serial number for NXT is printed...

The serial number can also be found in the **Properties** app:

1. Sign in to the device.
1. Navigate to **This PC** in file explorer.
1. Right click and select **Properties** of the NXT.

screencap



<!-- ########################## -->
## Next steps

[First time user setup](setup.md).

[Learn more about Windows 365 Enterprise](./enterprise/overview.md).

[Read the Windows 365 service description](/office365/servicedescriptions/windows-365-service-description/windows-365-service-description).
