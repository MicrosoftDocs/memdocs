---
# required metadata

title: Turn on Microsoft Defender Antivirus on enrolled device | Microsoft Docs
description: Learn how to turn on Microsoft Defender Antivirus to access company resources on an Intune-enrolled device. 
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 06/06/2023
ms.topic: end-user-help
ms.prod:
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology:
ms.assetid: d16dd2de-3ed5-474f-a04b-36dcd350162c
searchScope:
 - User help

# optional metadata

ROBOTS:  
#audience:

ms.reviewer: shburbid
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection:
- tier2
---


# Turn on Microsoft Defender Antivirus to access company resources  

Organizations want to ensure that devices accessing their resources are secured, so they may require you to use Microsoft Defender Antivirus and additional Windows Security features. Microsoft Defender Antivirus is an antivirus software that's included in Windows and can help protect your device from viruses, malware, and other threats. 

This article describe how to update your device settings to meet your organization's antivirus requirements and resolve access problems. 

## Turn on Microsoft Defender Antivirus
Complete the following steps to turn on Microsoft Defender Antivirus on your device. 

1. Select the **Start** menu.
2. In the search bar, type **group policy**. Then select **Edit group policy** from the listed results. The Local Group Policy Editor will open.
4. Select **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Microsoft Defender Antivirus**. 
5. Scroll to the bottom of the list and select **Turn off Microsoft Defender Antivirus**.  
6. Select **Disabled** or **Not configured**. It might feel counter-intuitive to select these options because the names suggest that you're turning Microsoft Defender Antivirus off. Don't worry, these options actually ensure that it's turned on. 
7. Select **Apply** > **OK**.  


## Turn on real-time and cloud-delivered protection

Complete the following steps to turn on real-time and cloud-delivered protection. Together, these antivirus features protect you against spyware and can deliver fixes for malware issues via the cloud. 

1. Select the **Start** menu.
2. In the search bar, type **Windows Security**. Select the matching result. 
3. Select **Virus & threat protection**.
4. Under **Virus & threat protection settings**, select **Manage settings**.
5. Flip each switch under **Real-time protection** and **Cloud-delivered protection** to turn them on. 

If you don't see these options on your screen, they may be hidden. Complete the following steps to make them visible.  

1. Select the **Start** menu.  
2. In the search bar, type **group policy**. Then select **Edit group policy** from the listed results. The Local Group Policy Editor will open.
3. Select **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Windows Security** > **Virus and threat protection**.
4. Select **Hide the Virus and threat protection area**.
5. Select **Disabled** > **Apply** > **OK**.  

## Update your antivirus definitions
Complete the following steps to update your antivirus definitions.  
1. Select the **Start** menu.
2. In the search bar, type **Windows Security**. Select the matching result. 
3. Select **Virus & threat protection**.
4. Under **Virus & threat protection updates**, select **Protection updates**.  
5. Select **Check for updates**. If you don't see this option on your screen, complete the first set of steps under [Turn on real-time and cloud-delivered protection](turn-on-defender-windows.md#turn-on-real-time-and-cloud-delivered-protection). Then try checking for updates again. 

## Next steps  

Still need help? Contact your support person. To find your organization's contact information, sign in to the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980). 
