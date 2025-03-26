---
# required metadata

title: Company Portal device setting requirements for Windows | Microsoft Intune
description: Learn more about Intune Company Portal device setting requirements for Windows OS.     
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/05/2024
ms.topic: end-user-help
ms.service: microsoft-intune
ms.subservice: end-user
ms.assetid: 
searchScope:
 - User help

# optional metadata

ROBOTS:  
#audience:

ms.reviewer: madakeva 
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection:
- tier3
---

# Company Portal device setting requirements for Windows              

This article describes the Windows device setting requirements in Intune Company Portal. Company Portal enforces these requirements on behalf of your workplace or school to ensure your device is secure while accessing their network. Requirements are specific to each organization. You only need to update the device settings that Company Portal flags. 

## Update operating system   

To get the latest updates for Windows, see [Microsoft Support: Get the latest Windows update](https://support.microsoft.com/windows/get-the-latest-windows-update-7d20e88c-0568-483a-37bc-c3885390d212).  

We recommend keeping the operating system (OS) on work and school devices up-to-date. Before updating a device, back up all of the information on it. Keep a backup so that you can recover your data if something interrupts the update, or transfer your information to a replacement device. 

## Operating system isn't supported  

The operating system (OS) version running on your device isn't supported. The current version of Windows might not work with your organization's apps, tools, or other internal infrastructure. To resolve this issue, either upgrade or downgrade to an OS version supported by your organization. OS requirements vary by organization. Contact your IT support person to find out what requirements you need to meet.   

For information about how to upgrade to Windows 11, see:  

* [Upgrade to Windows 11: FAQ](https://support.microsoft.com/windows/upgrade-to-windows-11-faq-fb6206a2-1a0f-448a-80f1-8668ee5b2bf9)  
* [Getting ready for the Windows 11 upgrade](https://support.microsoft.com/windows/getting-ready-for-the-windows-11-upgrade-eb50813f-c7da-4cf8-89a3-6ba0d33b2773)  

## Enable anti-malware protection  

Anti-malware is an important factor in making sure your device is protected. To meet this compliance requirement, enable the anti-malware software and features required by your organization. On devices running Windows 10 and later, the built-in anti-malware software is Microsoft Defender Antivirus. 

Remember to only download apps from verified sources, such as the Company Portal app and the Microsoft Store. For more information about anti-malware for Windows, see [Microsoft Support: Getting started with anti-malware in Microsoft Defender](https://support.microsoft.com/topic/getting-started-with-anti-malware-in-microsoft-defender-f5219ae5-abb7-4985-a149-1ec1bb304eda). 

## Enable Window Code Integrity  

Contact your IT support person to enable code integrity on your work or school device. Code integrity is a threat protection feature that checks the drivers and system files on your device for signs of corruption or malicious software. For it to work on your device, another security feature called *Secure Boot* must be enabled. Your IT support person can also help you enable Secure Boot, which will in turn trigger code integrity the next time you start up your device.  

<!-- Admin info commented out 
If you're a Microsoft Intune administrator and want to learn more about Intune's device health compliance settings, see [Add Windows 10/11 device compliance policy](../protect/compliance-policy-create-windows.md). For a detailed look at the compliance actions you can take in Intune, see the [HealthAttestation CSP](/windows/client-management/mdm/healthattestation-csp#step-8-take-appropriate-policy-action-based-on-evaluation-results). -->  

## Turn on Windows Defender Firewall  

Windows Defender Firewall helps prevent hackers and malicious software from gaining access to your work or school device through the internet or a network. Your organization might require you to turn it on before you can access their network resources.  

For more information and how-to instructions, see [Microsoft Support: Turn Microsoft Defender Firewall on or off](https://support.microsoft.com/windows/turn-microsoft-defender-firewall-on-or-off-ec0844f7-aebd-0583-67fe-601ecf5d774f) on Microsoft Support.  

<!-- removing steps 8/1/24
1. Go to **Start** and open **Control Panel**.
2. Select **System and Security** > **Windows Defender Firewall**.  
3. Choose **Turn Windows Defender Firewall on or off**. 
4. Select **Turn on Windows Defender Firewall** for domain, private, and public network settings.    -->

## Access point restrictions not set up  
Your company applied access point restrictions on your device. This setting requires the Company Portal app to verify a few network settings on your device. Tap **Resolve** and wait while the Company Portal app checks for an approved network connection.  

## Not connected to an approved network  

Your device is connected to a network that isn't approved for work access. While connected to this network, you can't access work email, apps, and other protected resources. To meet this compliance requirement, connect to a company-approved network. Then tap **Resolve** in Company Portal to retry.  

## Restrictions couldn't be enforced  

Company Portal can't determine if your device is connected to an approved network. This error could be a result of poor network connectivity, low battery, battery saver mode, or a Company Portal error. To resolve, verify that you have a strong network reception. Turn off battery saver mode and make sure your battery life has at least 30% remaining. Then tap **Resolve** in Company Portal to retry. 

## Enable Secure Boot  

[Secure Boot](/windows/security/operating-system-security/system-security/secure-the-windows-10-boot-process#secure-boot) is a security standard developed by members of the PC industry to help ensure that a device boots using only software that's trusted by the original equipment manufacturer (OEM). Your organization might require you to enable it. We recommend reaching out to your IT support person for help with enabling Secure Boot on a work or school device. 
 
Secure Boot settings are available in  Windows Security and UEFI BIOS settings. For information about accessing the UEFI menu on a Surface device, see [Manage Surface UEFI settings](/surface/manage-surface-uefi-settings#open-surface-uefi-menu). For information about how to boot other devices into UEFI BIOS mode, see the manufacturer's documentation. 
 
## Turn on virus and threat protection     

Microsoft Defender Antivirus is an antivirus software included in Windows that protects against viruses, malware, and other threats. Your organization might require you to turn on specific antivirus features on your device before you can access their network.   

* Turn on real-time protection: Real-time protection enables Microsoft Defender Antivirus to scan for threats on your device. To turn on real-time protection, go to **Start** > **Windows Security** > **Virus & threat protection**.   

<!-- Removing steps 8/1/24
1. Select the **Start** menu.
2. In the search bar, type **group policy**. Then select **Edit group policy** from the listed results. The Local Group Policy Editor opens.
4. Select **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Microsoft Defender Antivirus**. 
5. Scroll to the bottom of the list and select **Turn off Microsoft Defender Antivirus**.  
6. Select **Disabled** or **Not configured**. It might feel counter-intuitive to select these options because the names suggest that you're turning off Microsoft Defender Antivirus. Don't worry, these options actually ensure that it's turned on. 
7. Select **Apply** > **OK**.  -->  

* Turn on cloud-delivered protection: On your device, go to **Start** > **Windows Security** > **Virus & threat protection**. Turn on cloud-delivered protection.  

<!--removing steps 8/1/24 
1. Open the **Windows Security** app. 
2. Select **Virus & threat protection**.
3. Under **Virus & threat protection settings**, select **Manage settings**.
4. Flip each switch under **Real-time protection** and **Cloud-delivered protection** to turn them on. 

If you don't see these options on your screen, they may be hidden. Complete the following steps to make them visible.  

1. Select the **Start** menu.  
2. In the search bar, type **group policy**. Then select **Edit group policy** from the listed results. The Local Group Policy Editor opens.
3. Select **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Windows Security** > **Virus and threat protection**.
4. Select **Hide the Virus and threat protection area**.
5. Select **Disabled** > **Apply** > **OK**.   -->  

* Update antivirus definitions: On your device, go to **Start** > **Windows Security** > **Virus & threat protection**. Then check for new protection updates. If you don't see the option to check for updates, turn on real-time protection and cloud-delivered protection, and then try again. 

For more information, see [Microsoft Support: Virus & threat protection in Windows Security](https://support.microsoft.com/windows/virus-threat-protection-in-windows-security-1362f4cd-d71a-b52a-0b66-c2820032b65e).  

<!-- 
Complete the following steps to update your antivirus definitions.  
1. Open the **Windows Security** app.   
2. Select **Virus & threat protection**.
3. Under **Virus & threat protection updates**, select **Protection updates**.  
4. Select **Check for updates**. If you don't see this option on your screen, turn on real-time protection and cloud-delivered protection. Then try checking for updates again. --> 

## Change User Access Control setting  

The User Access Control settings prevent potentially harmful programs and software from making changes to your device. To meet this compliance requirement, adjust User Access Control so that your device has more protection. User Access Control settings are in Control Panel under **System and Security**. For more information, see [Microsoft Support: User Account Control settings](https://support.microsoft.com/windows/user-account-control-settings-d5b2046b-dcb8-54eb-f732-059f321afe18).  

<!-- Removing steps 8/1/24
You can adjust User Account Control settings in the Control Panel.  

1. Go to **Start** and open **Control Panel**.
2. Select **System and Security**.
3. Under **Security and Maintenance**, select **Change User Account Control settings**.
3. Move the slider to one of the following levels: 
   * **Notify me only when apps try to make changes to my computer (default)**
   * **Always notify**  
4. Select **OK** to save your changes. 
5. Select **Yes** when prompted to confirm the changes.   --> 

## Next steps 
If you're having trouble resolving a compliance requirement, contact your IT support person or IT administrator for help. They can help you quickly identify the problem and solution so that you can use your device for work or school again. To find your organization's contact information, sign in to the Company Portal app or [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980).  
