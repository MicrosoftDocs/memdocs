---
# required metadata

title: Wipe a macOS device
titleSuffix: Microsoft Intune
description: Learn how to wipe all data, including the operating system, from a macOS device.
keywords:
author: Smritib17
ms.author: smbhardwaj
manager: dougeby
ms.date: 05/19/2020
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: remote-actions
ms.localizationpriority: high
ms.technology:
ms.assetid: ab396092-907a-44b7-a157-aabee62176a9

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: Beflamm
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Wipe all data from a macOS device

Intune gives you the ability to use the **Wipe** remote device action to wipe data from macOS devices, including the operating system. It's important to note that the device is also  removed from Intune management and no warning is given to the end user once a wipe is initiated.

## Before you start

- For devices running macOS 12.0.1 and later, review the requirements for erasing devices available on the [Apple Support site](https://support.apple.com/en-ph/guide/deployment/dep0a819891e/web).

- For devices running a version of macOS below 12.0.1, macOS will need to be reinstalled. Steps covering how to reinstall macOS are available on the [Apple Support site](https://support.apple.com/en-us/HT204904).

## How to use Wipe

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Devices** > **All devices** > and select the device you want to wipe. Select **Wipe**. 

    :::image type="content" source="./media/device-wipe-mac-os/wipeaction-mac-os.png" alt-text="Screen shot that shows where in the Intune admin center you select Wipe." lightbox="./media/device-wipe-mac-os/wipeaction-mac-os.png":::

2. Provide a 6-digit number for the **Recovery PIN**. The six-digit PIN is required to reinstall the operating system on the device if the device is not equipped with T2 security chip enabled (i.e. the model year of the device is 2018 and earlier, or the device is running macOS 10.14 or earlier). Be sure to make a note of this PIN and give it to the device owner as it won't be visible after the wipe action completes.

    :::image type="content" source="./media/device-wipe-mac-os/obliteration-behavior.png" alt-text="Screen shot that shows where in the Intune admin center you select Wipe." lightbox="./media/device-wipe-mac-os/obliteration-behavior.png":::

3. Select an option from **Obliteration Behavior**, which is used to define the fallback for devices when Erase All Contents and Settings (EACS) fails. The following options can be configured:

    - **Default**: If Erase All Content and Settings (EACS) preflight fails, the device responds to Intune with an Error status and then attempts to erase itself. If EACS preflight succeeds but EACS fails, then the device attempts to erase itself.  

    - **Do not obliterate**: If Erase All Content and Settings (EACS) preflight fails, the device responds to Intune with an Error status and doesn't attempt to erase itself. If EACS preflight succeeds but EACS fails, then the device doesn't attempt to erase itself.

    - **Obliterate with warning**: If Erase All Content and Settings (EACS) preflight fails, the device responds with a Success status and then attempts to erase itself. If EACS preflight succeeds but EACS fails, then the device attempts to erase itself.

    - **Always obliterate**: The system doesn't attempt Erase All Content and Settings (EACS). T2 and later devices always obliterate.  

4. Select **Wipe** to erase the device.
