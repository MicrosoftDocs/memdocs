---
# required metadata

title: Retrieve iOS app logs - Microsoft Intune | Microsoft Docs
description: Learn how to retrieve Intune Company Portal app logs off your device for troubleshooting purposes. 
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 12/01/2020
ms.topic: end-user-help
ms.prod:
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology:
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
2. On your Mac, press **command + Space** and search for Console. You can also find it in **Applications** > **Utilities** > **Console**.  
3. On your iOS device, you'll be prompted to trust the computer. Select **Trust**. 
3. In Console, select your iOS device from the **Devices** list. Console begins to gather your logs. 
4. From the menu, select **Action** > **Include Info Messages** and **Include Debug Messages**.  
6. Select **Clear** and remove any search queries you may have in Console.  
7. Open Company Portal on your iOS device and try to reproduce the problem by repeating the steps or actions you took leading up to the problem.              
8. In the Console toolbar, select **Edit** > **Select All**, and then select **Edit** > **Copy**. 
9. Paste the log contents in a text editor. 
10. From the menu, select **Format** > **Make Plain Text**. 
11. Save the file as a .log file (Example: Contosologs.log) 

## Next steps

After you save your file, you can send it to your IT support person as an email attachment. For contact information, check the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980).  
