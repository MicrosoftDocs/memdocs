---
# required metadata

title: Retrieve iOS app logs - Microsoft Intune | Microsoft Docs
description: Learn how to retrieve Intune Company Portal app logs off your device for troubleshooting purposes. 
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/05/2025
ms.topic: end-user-help
ms.service: microsoft-intune
ms.subservice: end-user
ms.assetid: 
searchScope:
 - User help

# optional metadata

ROBOTS:  
#audience:

ms.reviewer: annovich
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection:
- tier2
---


# Retrieve iOS app logs from device  

 Whenever you experience a problem in Company Portal, the details of that problem are recorded and stored on your device in a _diagnostic log_. This article describes how to upload those logs from your device to your computer. This process is useful for when you need troubleshooting help, because you can save the logs in a file and email it to your IT support person.   

## Retrieve logs via Console app  

To retrieve logs via the native Console app, you'll need your iOS device, a USB cable, and a Mac running macOS 10.12 or later.   

1. Connect your iOS device to your Mac with the USB cable. 
1. On your Mac, press **command + Space** and search for Console. You can also find it in **Applications** > **Utilities** > **Console**.  
1. On your iOS device, you'll be prompted to trust the computer. Select **Trust**. 
1. In Console, select your iOS device from the **Devices** list > **Start**. Console begins to gather your logs. 
1. In the Console menu, select **Action** > **Include Info Messages** and **Include Debug Messages**.  
1. Select **Clear** and remove any search queries you may have in Console.  
1. Open Company Portal on your iOS device and try to reproduce the problem by repeating the steps or actions you took leading up to the problem.              
1. In the Console menu, select **Edit** > **Select All**, and then select **Edit** > **Copy**. 
1. Paste the log contents in TextEdit.  
1. From the menu, select **Format** > **Make Plain Text**. 
1. Save the file as a .log file. Example: Contosologs.log   

## Next steps

After you save your file, you can send it to your IT support person as an email attachment. For contact information, check for helpdesk information on the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980) or app.  
