---
# required metadata

title: Enable Secure Boot for Windows 10 - Microsoft Intune | Microsoft Docs
description: Learn how to make your device compliant again by enabling Secure Boot.  
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 09/24/2020
ms.topic: end-user-help
ms.prod:
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
---


# Enable Secure Boot on your device  

Your organization requires that you enable Windows Secure Boot, which is a security feature that helps protect your device.  

If you're using a mobile device, contact your IT support person and they'll help enable Secure Boot for you.  

If you're using a PC, you can either:

* Contact your IT support person for help.  
* Try enabling Secure Boot on your own through the PC BIOS menu. For step-by-step instructions, see the **Re-enable Secure Boot** section [in this article](/windows-hardware/manufacture/desktop/disabling-secure-boot#re-enable-secure-boot).  

## More information about Secure Boot  

Secure boot is a security standard developed by members of the PC industry to help make sure that a device boots using only software that is trusted by the Original Equipment Manufacturer (OEM).  

### Check Secure Boot status  
To check the status of Secure Boot on your PC:  

1. Go to Start.
2. In the search bar, type **msinfo32** and press enter. 
3. **System Information** opens. Select **System Summary**. 
4. On the right-side of the screen, look at **BIOS Mode** and **Secure Boot State**. If Bios Mode shows **UEFI**, and Secure Boot State shows **Off**, then Secure Boot is disabled.  

## Next steps  

* For more detailed information about the Secure Boot feature, see the [Windows Developer Hardware docs](/windows-hardware/manufacture/desktop/secure-boot-landing).  

* Still need help? Contact your IT support person. For contact information, check the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980).