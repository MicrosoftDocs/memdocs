---
# required metadata

title: Turn on Windows Defender | Microsoft Docs
description: Learn how to turn on Windows Defender to access company resources.
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 11/08/2017
ms.topic: article
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
#ms.devlang:
ms.reviewer: shburbid
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection: 
---


# Turn on Windows Defender to access company resources

Your work or school wants to ensure that devices accessing their resources are secured. There are a few ways that they can use [Windows Defender](https://www.microsoft.com/safety/pc-security/windows-defender.aspx), Windows' built-in protection for malicious software.

There are a few settings you may need to change on your Windows Defender to fix any access issues. These steps may require you to go to a couple of different places on your computer.

## Turn on Windows Defender

1. In **Start**, open **Control Panel**.
2. Open **Administrative Tools** > **Edit group policy**. This will open the **Local Group Policy Editor** in a new window.
3. Open **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Windows Defender Antivirus**. The setting **Turn off Windows Defender Antivirus** is underneath the folders of other settings. 
4. Open **Turn off Windows Defender Antivirus** and make sure it's set to **Disabled** or **Not configured**.

## Turn on Real-time Protection

Check to make sure that Real-time Protection is turned on by going to **Start** and searching for **Windows Defender Security Center**. Select **Virus and threat protection settings** and confirm that both **Real-time protection** and **Cloud-delivered protection** are switched to **On**. If these options aren't appearing, do the following to enable them:

1. In **Start**, open **Control Panel**.
2. Open **Administrative Tools** > **Edit group policy**. This will open the **Local Group Policy Editor** in a new window.
3. Open **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Windows Defender Security Center** > **Virus and threat protection**.
4. Open the setting **Virus and threat protection area** and set it to **Disabled**.

## Update your antivirus definitions

Check to make sure that your antivirus definitions are up-to-date by going to **Start** and searching for **Windows Defender Security Center**. Select **Protection updates** and **Check for updates** to make sure that your device has current protection against viruses. If this option doesn't appear, follow the steps in [Turn on Real-time Protection](turn-on-defender-windows.md#turn-on-real-time-protection)

Still need help? Contact your company support. For their contact information, check the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980).
