---
# required metadata

title: Send logs to your company support for Windows 10 devices | Microsoft Docs
description: Enroll a Windows 10 1511 device into Intune
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 01/09/2019
ms.topic: article
ms.prod:
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology:
ms.assetid: 038747fb-5b52-47c4-a2b6-f9218da4cfe1
searchScope:
 - User help

# optional metadata

ROBOTS:  
#audience:
#ms.devlang:
ms.reviewer: priyar
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection: 
---

# Send logs to your company support from the Settings app for Windows 10

Use the Settings app to troubleshoot Company Portal for Windows 10. If you run into a problem while using the app on your Windows 10 device, you can email your support team for help. Events and errors that occur in the Company Portal app are saved on your device in a special document called a _diagnostic log_. They can contain additional insights about the error, and when exported are useful to support teams.

1. To open the **Settings** app, go to the **Start** menu > **Settings**. You can also search for *settings* in the search bar.
2. Go to **Accounts** > **Access work or school**.
3. Select **Export your management log files**.

   ![The "Access work or school screen", which presents the Export option underneath the "Related settings" heading.](./media/w10-export-logs.png)

4. The logs will be saved in **C:\Users\Public\Public Documents\MDMDiagnostics**. Two files will be created: one is the log itself, and the other is a special document that allows your admin to review the logs in different programs, like Microsoft Excel. Attach both of these files to an email and send that email to your admin. If you do this more than once, simply choose the files from the day you created the logs. 

You may also need to send [logs from the Company Portal app](send-logs-to-your-it-admin-cp-windows.md) to give your company support more help in trying to troubleshoot any issues they may find. 

Still need help? Contact your company support. For contact information, check the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980).
