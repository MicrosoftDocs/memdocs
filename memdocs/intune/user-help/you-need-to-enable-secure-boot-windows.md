---
# required metadata

title: Enable Secure Boot on Windows devices - Microsoft Intune | Microsoft Docs
description: Learn how to make your enrolled device compliant again by enabling Secure Boot.
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/29/2024
ms.topic: end-user-help
ms.localizationpriority: high
ms.service: microsoft-intune
ms.subservice: end-user
ms.assetid: de881f1b-7622-4ec2-8bf8-025f71ca9887
searchScope:
 - User help

# optional metadata

ROBOTS:
#audience:

ms.reviewer: madholdaa
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection:
- tier2
---


# Enable Secure Boot on work or school device  

Secure Boot is a security standard developed by members of the PC industry to help ensure that a device boots using only software that's trusted by the original equipment manufacturer (OEM). Your organization's device management policies may require you to enable it on your enrolled Windows device. Devices that don't meet this requirement may be unable to access work or school resources.     

## Enable Secure Boot  
You can manage Secure Boot in the UEFI BIOS settings (PC firmware) on your device. To learn how to boot your device into UEFI or BIOS mode, see the manufacturer's documentation. For example, on tablets it's common to press the **Volume up** or **Volume down** button while powering on your device. Other common keys used include Esc, Delete, F1, F2, F10, F11, or F12. 

The following steps describe how to change the Secure Boot configuration on a Surface device. For more information about Secure Boot for Surface, see [Manage Surface UEFI settings](/surface/manage-surface-uefi-settings#open-surface-uefi-menu). 

1. Save any open work.  
2. Open **Settings** and go to **System** > **Recovery**.  
3. Under **Recovery options**, find **Advanced setup** and select **Restart now**.  
4. Select **Restart now** to confirm. 
5. After your device restarts, select **Troubleshoot**.
6. Select **Advanced options** > **UEFI Firmware Settings**.  
7. Select **Restart**.
8. In the **Security** tab, go to **Secure Boot** and select **Change configuration**. 

## Check Secure Boot status  
To check the status of Secure Boot on your PC:  

1. Go to Start.
2. In the search bar, type **msinfo32** and press enter. 
3. **System Information** opens. Select **System Summary**. 
4. On the right-side of the screen, look at **BIOS Mode** and **Secure Boot State**. If Bios Mode shows **UEFI**, and Secure Boot State shows **Off**, then Secure Boot is disabled. 

## Next steps  

* For more information about Secure Boot, see [What is Secure Boot?](https://www.microsoft.com/en-us/surface/do-more-with-surface/what-is-secure-boot).  
* Still need help? Contact your support person if you're having trouble enabling Secure Boot or if it appears enabled already. Sign in to the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980) to check for your support person's contact information.  
