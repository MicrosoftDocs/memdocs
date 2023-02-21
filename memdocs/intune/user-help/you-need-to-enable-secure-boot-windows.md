---
# required metadata

title: Enable Secure Boot on Windows devices - Microsoft Intune | Microsoft Docs
description: Learn how to make your enrolled device compliant again by enabling Secure Boot.  
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/23/2022
ms.topic: end-user-help
ms.prod:
ms.localizationpriority: high
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology:
ms.assetid: de881f1b-7622-4ec2-8bf8-025f71ca9887
searchScope:
 - User help

# optional metadata

ROBOTS:  
#audience:

ms.reviewer: chrisbal
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser; seodec18
ms.collection:
- tier2
---


# Enable Secure Boot on enrolled Windows device  

Secure Boot is a security standard developed by members of the PC industry to help ensure that a device boots using only software that's trusted by the original equipment manufacturer (OEM). Your organization's device management policies may require you to enable it on your enrolled Windows device. Devices that don't meet this requirement may be unable to access work or school resources.     

## Enable Secure Boot  
If your enrolled device is a mobile device, contact your support person and they'll help enable Secure Boot for you.  

If your enrolled device is a PC, you can either:  

* Contact your support person for help.  
* Enable Secure Boot from the PC BIOS menu. For step-by-step instructions, see [Re-enable Secure Boot](/windows-hardware/manufacture/desktop/disabling-secure-boot#re-enable-secure-boot).  

## Check Secure Boot status  
To check the status of Secure Boot on your PC:  

1. Go to Start.
2. In the search bar, type **msinfo32** and press enter. 
3. **System Information** opens. Select **System Summary**. 
4. On the right-side of the screen, look at **BIOS Mode** and **Secure Boot State**. If Bios Mode shows **UEFI**, and Secure Boot State shows **Off**, then Secure Boot is disabled.  

## Next steps  

* For more detailed information about the Secure Boot feature, see the [Windows Developer Hardware docs](/windows-hardware/manufacture/desktop/secure-boot-landing).  
* Still need help? Contact your support person if you're having trouble enabling Secure Boot or if it appears enabled already. Sign in to the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980) to check for your support person's contact information.  
