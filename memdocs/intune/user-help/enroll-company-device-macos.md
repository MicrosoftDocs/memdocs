---
# required metadata

title: Enroll your organization-provided macOS device in management | Microsoft Docs
description: Describes how to enroll an macOS device in Intune that was purchased and provided by your organization.
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 08/29/2018
ms.topic: end-user-help
ms.service: microsoft-intune
ms.subservice: end-user
ms.assetid: 
searchScope:
 - User help

# optional metadata

ROBOTS:  
#audience:

ms.reviewer: 
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection:
- tier1
---

# Enroll your organization-provided macOS device in management

Learn how to get your new macOS device managed in Intune.  

Devices that are provided by your work or school are often preconfigured before you receive them. Your organization will send these preconfigured settings to your device after you turn it on and sign in for the first time. After your device completes setup, you'll receive access to your work or school resources.

To begin management setup, power on your device and sign in with your work or school credentials. The rest of this article describes the steps and screens you'll see as you walk through Setup Assistant.

## What is Apple's Automated Device Enrollment?

Your organization might have purchased their devices through an Apple program called *Automated Device Enrollment* (formerly referred to as their device enrollment program or *DEP*). Automated Device Enrollment lets organizations buy large amounts of iOS, iPadOS or macOS devices. Organizations can then configure and manage those devices within their preferred mobile device management provider, such as Intune. If you're an administrator and want more information about Apple ADE, see [Automatically enroll macOS devices with Apple's Automated Device Enrollment with ABM/ASM](/mem/intune/enrollment/device-enrollment-program-enroll-macos).  

## Get your device managed

Complete the following steps to enroll your macOS device in management. If you're using your own device, rather than an org-provided device, follow the steps for [personal and bring-your-own devices](enroll-your-device-in-intune-macos-cp.md).  

1. Power on your macOS device.
2. Choose your country/region. Then select **Continue**.  

   ![Screenshot of macOS device Setup Assistant Welcome screen, showing a list of languages to select from.](./media/enroll-company-device-macos/macos-dep-welcome-1808.png)  

3. Choose a keyboard layout. The list shows one or more options based off your selected country/region. To see all layout options, regardless of your selected country/region, select **Show All**. When you're done, select **Continue.**  

   ![Screenshot of macOS device Setup Assistant Keyboard Layout screen, showing a list of keyboard languages to select from, an unchecked Show All option, and a Back and Continue button.](./media/enroll-company-device-macos/macos-dep-keyboard-1808.png)  

4. Select your Wi-Fi network. You must have an internet connection to continue setup. If you do not see your network, or if you need to connect over a wired network, select **Other Network Options**. When you're done, select **Continue**.  

   ![Screenshot of macOS device Setup Assistant Select Your Wi-Fi Network screen, showing a list of available networks to choose from. Also shows an Other Network Options button, Back button, and Continue button.](./media/enroll-company-device-macos/macos-dep-wifi-1808.png)  

5. After you're connected to Wi-Fi, the **Remote Management** screen appears. Remote management enables your organization's administrator to remotely configure your device with company-required accounts, settings, apps, and networks. Read through the remote management explanation to help you understand how your device is managed. Then select **Continue**.  

   ![Screenshot of macOS device Setup Assistant Remote Management screen, with text explaining remote management and a link to documentation for more information. Also shows a Back button and Continue button.](./media/enroll-company-device-macos/macos-dep-remote-management-1-1808.png)  

6. When prompted, sign in with your work or school account. After you're authenticated, your device will install a management profile. The profile configures and enables your access to your organization's resources.  

7. Read about the Apple data & privacy icon so that you can later identify when personal information is being collected. Then select **Continue**.  

   ![Screenshot of macOS device Setup Assistant Data & Privacy screen, showing an illustration of two people shaking hands, and describing Apple's use of personal information. Also shows a Back and Continue button.](./media/enroll-company-device-macos/macos-dep-apple-data-privacy-1808.png)  
   
8. After your device is enrolled, you might have additional steps to complete. The steps you see depend on how your organization customized the setup experience. It could require you to:
    * Sign in to an Apple account
    * Agree to the Terms and conditions
    * Create a computer account
    * Walk through an express setup
    * Set up your Mac

## Get the Company Portal app

Download the Intune Company Portal app for macOS on your device. The app lets you monitor, sync, add, and remove your device from management, and install apps. 

1. On your Mac, go to [https://portal.manage.microsoft.com/EnrollmentRedirect.aspx](https://portal.manage.microsoft.com/EnrollmentRedirect.aspx).  
2. Sign in to the Company Portal website with your work or school account. 
3. Select **Get the App** to download the Company Portal installer for macOS.  
4. When prompted, open the .pkg file. Follow the on-screen prompts to install the app. 

Then register your device with Company Portal.    
   
1. Open the Company Portal app and sign in with your work or school account.
1. Find your device and select**Register**.  
1. Select **Continue** > **Done**. 

After registration, your device appears in the Company Portal app, alongside any other work or school devices you've registered.  Required work or school apps automatically install on your device, while optional apps are available in Company Portal.  

For help and support, contact your organization's support person. For contact information, check the helpdesk details in the Company Portal app or [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980).  
