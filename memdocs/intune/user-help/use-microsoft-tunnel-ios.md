---
# required metadata

title: Use the Microsoft Tunnel app for iOS - Microsoft Intune  | Microsoft Docs
description: Learn how to connect over VPN using Microsoft Tunnel for iOS.
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/29/2022  
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

ms.reviewer: shthilla
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection: 
---


# Using Microsoft Tunnel for iOS  

Microsoft Tunnel uses Microsoft Defender for Endpoint as The Microsoft Tunnel client app on iOS. Microsoft Defender for Endpoint replaces Microsoft Tunnel as the client app beginning on April 29, 2022. Use of the standalone Microsoft Tunnel client app remains in support until the end of June 2022.

The Microsoft Tunnel client app helps you securely and privately connect to your corporate network over a VPN. If your organization requires you to use the app, they already configured a VPN connection for your work account. To connect to the VPN, simply install the app and sign in with your work account. 


## Connect and disconnect VPN      

1. Open Microsoft Tunnel. 
2. Sign in with your work account if prompted.
3. On the **Connect** screen, turn the **Status** toggle on or off to connect or disconnect from the VPN. 
 
An absent **Status** toggle means that Tunnel is configured to connect automatically when certain apps are in use. To turn this functionality off, go to **Details** and turn off **Connect on demand**.    

If the toggle is stuck in the off position, select **Help** > **Send logs** and report the problem to your IT support person. For more details, see the [Send logs](use-microsoft-tunnel-ios.md#send-logs) section in this article. 


## Connection details    

The following information appears on the **Connect** screen when Tunnel is connected.  

* **Uptime**: How long the VPN connection has been running. 

* **Data received**: How much data has been received through the VPN connection. 

* **Data sent**: How much data has been sent through the VPN connection.  

Tap **Details** to see the following information:  

* **Address**: The server address for your VPN connection. 

* **Script/Address/Port**: These details will help IT support troubleshoot your proxy server connection, should you ever need help. 

* **Device-wide connection**: When turned on, all network traffic to and from your device goes through the VPN connection.  

* **Connect on demand**: When turned on, Microsoft Tunnel automatically connects when certain apps (listed under **Apps that use Tunnel**) are in use.   

* **Apps that use Tunnel**: If apps are listed, only network traffic to and from these apps go through the VPN connection.  

## App settings  

To configure how Tunnel collects and logs data, open the **Settings** app on your device. Select **Microsoft Tunnel** to:  

* Allow/block Microsoft from collecting usage and performance data. 
* Turn verbose logging on/off.   


## Get help in the app  
Select **Help** from the menu at the bottom of the screen to:  

* Access documentation (directs you to this article). 
* Send logs to IT support to report a problem.  

### Send logs  

Send app logs to IT support to get help with an app or connection problem.

1. Select **Help** > **Send logs**.
2. Select **Send logs** again. Your logs will be sent to a Microsoft database, from which your organization can access. 
3. Select **Email administrator**. 
5. In the body of the email, describe the problem you experienced so that the support team has an idea of what to look for. 
6. Send the email.  

## About Microsoft Tunnel  
Select **About** to view the Microsoft Tunnel privacy policy, terms of use, and third-party notices.  



## Next steps  
Need additional help? Contact your IT support person. For contact information, check the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980).  
