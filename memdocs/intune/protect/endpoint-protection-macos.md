---
# required metadata

title: Add endpoint protection on macOS in Microsoft Intune - Azure | Microsoft Docs
description: On macOS devices, use the gatekeeper to determine where apps can be installed, including the mac app store. Also enable or configure a firewall allow specific apps, blocks specifics apps, use stealth mode, and even block certain types of incoming connections using Microsoft Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/24/2020
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology:

# optional metadata

#ROBOTS:
#audience:

ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# macOS endpoint protection settings in Intune  

This article shows you the endpoint protection settings that you can configure for devices that run macOS. You configure these settings by using a macOS device configuration profile for [endpoint protection](endpoint-protection-configure.md) in Intune.  

## Before you begin

[Create a macOS endpoint protection profile](endpoint-protection-configure.md).

## Gatekeeper  

- **Allow apps downloaded from these locations**  
  Limit the apps a device can launch, depending on where the apps were downloaded from. The intent is to protect devices from malware, and allow apps from only the sources you trust.  

  - **Not configured**  
  - **Mac App Store**  
  - **Mac App Store and identified developers**  
  - **Anywhere**  

  **Default**: Not configured  

- **User can override Gatekeeper**  
  Prevents users from overriding the Gatekeeper setting, and prevents users from Control clicking to install an app. When enabled, users can Control-click any app, and install it.  
 
  - **Not configured** - Users can Control-click to install apps.  
  - **Block** - Prevents users from using Control-click to install apps.  

  **Default**: Not configured  

## Firewall  

Use the firewall to control connections per-application, rather than per-port. Using per-application settings makes it easier to get the benefits of firewall protection. It also helps prevent undesirable apps from taking control of network ports that are open for legitimate apps.  

**General**
- **Firewall**  
  Enable Firewall to configure how incoming connections are handled in your environment.  
  - **Not configured**  
  - **Enable**  

  **Default**: Not configured  

- **Incoming connections**  
  Block all incoming connections except the connections required for basic Internet services, such as DHCP, Bonjour, and IPSec. This feature also blocks all sharing services, such as File Sharing and Screen Sharing. If you're using sharing services, then keep this setting as *Not configured*.  
  - **Not configured**  
  - **Block**  

  **Default**: Not configured  

**Allow or block incoming connections for specific apps.**  

  - **Apps allowed**  
    Select the apps that are explicitly allowed to receive incoming connections.  

  - **Apps blocked**  
    Select the apps that should block incoming connections.  

  - **Stealth mode**  
    To prevent the computer from responding to probing requests, enable stealth mode. The device continues to answer incoming requests for authorized apps. Unexpected requests, such as ICMP (ping), are ignored.  
    - **Not configured**  
    - **Enable**  

    **Default**: Not configured  

## FileVault  
For more information about Apple FileVault settings, see [FDEFileVault](https://developer.apple.com/documentation/devicemanagement/fdefilevault) in the Apple developer content. 

> [!IMPORTANT]  
> As of macOS 10.15, FileVault configuration requires user approved MDM enrollment. 

- **FileVault**  
  You can *enable* Full Disk Encryption using XTS-AES 128 with FileVault on devices that run macOS 10.13 and later.  
  - **Not configured**  
  - **Enable**  

  **Default**: Not configured  

  - **Recovery key type**  
    *Personal key* recovery keys are created for devices. Configure the following settings for the personal key.  

    - **Location of personal recovery key** - Specify a short message to the user that explains how and where they can retrieve their personal recovery key. This text is inserted into the message the user sees on their log in screen when prompted to enter their personal recovery key if a password is forgotten.  

    - **Personal recovery key rotation** - Specify how frequently the personal recovery key for a device will rotate. You can select the default of **Not configured**, or a value of **1** to **12** months.  

  - **Disable prompt at sign out**  
    Prevent the prompt to the user that requests they enable FileVault when they sign out.  When set to Disable, the prompt at sign-out is disabled and instead, the user is prompted when they sign in.  
    - **Not configured**  
    - **Disable** - Disable the prompt at sign-out.

    **Default**: Not configured  

  - **Number of times allowed to bypass**  
  Set the number of times a user can ignore prompts to enable FileVault before FileVault is required for the user to sign in. 

    - **Not configured** - Encryption on the device is required before the next sign-in is allowed.  
    - **1** to **10** - Allow a user to ignore the prompt from 1 to 10 times before requiring encryption on the device.  
    - **No limit, always prompt** - The user is prompted to enable FileVault but encryption is never required.  
 
    **Default**: *Varies* - When the setting *Disable prompt at sign out* is set to **Not configured**, this setting defaults to **Not configured**. When *Disable prompt at sign out* is set to **Disable**, this setting defaults to **1** and a value of **Not configured** isn't an option.

For more information about FileVault with Intune, see [FileVault recovery keys](encryption-monitor.md#filevault-recovery-keys).

## Next steps

[Assign the profile](../configuration/device-profile-assign.md) and [monitor its status](../configuration/device-profile-monitor.md).

You can also configure endpoint protection on [Windows 10 and newer devices](endpoint-protection-windows-10.md).
