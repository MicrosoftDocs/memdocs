---
title: include file
description: include file
author: erikre 
ms.service: microsoft-intune
ms.topic: include
ms.date: 07/31/2024
ms.author: erikre
ms.custom: include file
---
### Level 1 enterprise basic data protection

Level 1 is the minimum data protection configuration for an enterprise mobile device. This configuration replaces the need for basic Exchange Online device access policies by requiring a PIN to access work or school data, encrypting the work or school account data, and providing the capability to selectively wipe the school or work data. However, unlike Exchange Online device access policies, the below App Protection Policy settings apply to all the apps selected in the policy, thereby ensuring data access is protected beyond mobile messaging scenarios.

The policies in level 1 enforce a reasonable data access level while minimizing the impact to users and mirror the default data protection and access requirements settings when creating an App Protection Policy within Microsoft Intune.  

#### Data protection

| Setting | Setting description |             Value  |             Platform        |
|-----------------|--------------------------------------------------------|-----------------------|----------------------------------------|
| Data   Transfer |             Back up org data to…  |             Allow  |             iOS/iPadOS, Android        |
| Data   Transfer |       Send org   data to other apps  |             All apps  |             iOS/iPadOS, Android        |
| Data   Transfer |       Send org data to  |             All destinations  |             Windows       |
| Data   Transfer |       Receive   data from other apps  |             All apps  |             iOS/iPadOS, Android        |
| Data   Transfer |       Receive data from  |             All sources  |             Windows        |
| Data   Transfer |       Restrict   cut, copy, and paste between apps  |             Any app  |             iOS/iPadOS, Android        |
| Data   Transfer |       Allow cut, copy, and paste for  |  Any destination and any source  |             Windows        |
| Data   Transfer |       Third-party keyboards  |             Allow  |             iOS/iPadOS        |
| Data   Transfer |       Approved keyboards  |             Not required  |             Android        |
| Data   Transfer |       Screen   capture and Google Assistant  |             Allow  |             Android        |
| Encryption |             Encrypt org data  |             Require  |             iOS/iPadOS, Android        |
| Encryption |       Encrypt   org data on enrolled devices  |             Require  |             Android        |
| Functionality  |             Sync app with native contacts app  |             Allow  |             iOS/iPadOS, Android        |
| Functionality  |       Printing   org data  |             Allow  |             iOS/iPadOS, Android, Windows        |
| Functionality  |       Restrict   web content transfer with other apps  |             Any app  |             iOS/iPadOS, Android        |
| Functionality  |       Org data notifications  |             Allow  |             iOS/iPadOS, Android        |

#### Access requirements

| Setting  | Value  | Platform  | Notes  |
|----------------------------------------------------------------|---------------|----------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| PIN for access  | Require  | iOS/iPadOS, Android  |   |
| PIN type  | Numeric  | iOS/iPadOS, Android  |   |
| Simple PIN  | Allow  | iOS/iPadOS, Android  |   |
| Select Minimum PIN length  | 4  | iOS/iPadOS, Android  |   |
| Touch ID instead of PIN for access (iOS 8+/iPadOS)  | Allow  | iOS/iPadOS  |   |
| Override biometrics with PIN after timeout  | Require  | iOS/iPadOS, Android  |   |
| Timeout (minutes of activity)  | 1440  | iOS/iPadOS, Android  |   |
| Face ID instead of PIN for access (iOS 11+/iPadOS)  | Allow  | iOS/iPadOS  |   |
| Biometric instead of PIN for access  | Allow  | iOS/iPadOS, Android  |   |
| PIN reset after number of days  | No  | iOS/iPadOS, Android  |   |
| Select number of previous PIN values to maintain  | 0  | Android  |   |
| App PIN when device PIN is set  | Require  | iOS/iPadOS, Android  | If the device is enrolled in Intune, administrators can consider setting this to "Not required" if they're enforcing a strong device PIN via a device compliance policy.  |
| Work or school account credentials for access  | Not required  | iOS/iPadOS, Android  |   |
| Recheck the access requirements after (minutes of inactivity)  | 30  | iOS/iPadOS, Android  |   |

#### Conditional launch

| Setting | Setting description |          Value / Action  |          Platform        | Notes |
|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------|---------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| App conditions |       Max PIN   attempts  |          5 / Reset   PIN  |          iOS/iPadOS,   Android  |                  |
| App conditions |       Offline   grace period  |          10080 /   Block access (minutes)  |          iOS/iPadOS, Android, Windows  |                  |
| App conditions |       Offline   grace period  |          90 / Wipe   data (days)  |          iOS/iPadOS, Android, Windows  |                  |
| Device conditions  |       Jailbroken/rooted   devices  |        N/A / Block   access  |          iOS/iPadOS,   Android  |                  |
| Device conditions  |       SafetyNet   device attestation  |          Basic   integrity and certified devices / Block access  |          Android  |          <p>This   setting configures Google Play’s device integrity check on end-user devices. Basic integrity validates the integrity of the device. Rooted   devices, emulators, virtual devices, and devices with signs of tampering fail   basic integrity. </p><p> Basic  integrity and certified devices validates the compatibility of   the device with Google's services. Only unmodified devices that have been   certified by Google can pass this check.</p>  |
| Device conditions  |       Require   threat scan on apps  |        N/A / Block   access  |          Android  |          This   setting ensures that Google's Verify Apps scan is turned on for end   user devices. If configured, the end-user will be blocked from access until   they turn on Google's app scanning on their Android device.        |
| Device conditions  |       Max allowed device threat level  |        Low / Block   access  |          Windows  |                  |
| Device conditions  |       Require device lock  |        Low/Warn |         Android  |          This setting ensures that Android devices have a device password that meets the minimum password requirements.                |

> [!NOTE]
> Windows conditional launch settings are labeled as **Health Checks**.
