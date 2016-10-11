---
title: "Use the LTSB client with the Current Branch  | System Center Configuration Manager"
description: "Learn about using the client from the Long-Term Servicing Branch of Configuration Manager with a Current Branch site."
ms.custom: na
ms.date: 10/12/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 600086d5-bd9e-4ac1-8ace-c7a62de80dc2
caps.latest.revision: 0
author: Brendunsms.author: brendunsmanager: angrobe
Robots: NOINDEX,NOFOLLOW
---
# Use the client software from the version 1606 baseline media with a Current Branch site



You can use the System Center Configuration Manager client software from the version 1606 baseline media DVD that you get with System Center 2016 (the LTSB client), to manage devices that belong to a Current Branch site.   

## How this scenario works:
Typically, when you install a new in-console update for the Current Branch, clients automatically update their client software so they can use those new features.

With this scenario, you use the Current Branch and receive the new features and updates. Most clients run the client software from the Current Branch and can update that client software with each version update you install. However, on a subset of critical systems that you do not want to receive client software updates, you install the Configuration Manager LTSB client (from the media you get with System Cener 2016). These clients will not install new client software until you explicitly deploy a new version off the client software to them.

More information on how to prevent Current Branch clients from automatically updating when you install a new version of Configuration Manager will be available with Current Branch version 1610.

The Current Branch site must run version 1606 or later.

## The LTSB client software
The client software (client.msi) for Windows computers that is included with the LTSB media is supported for the full lifecycle of the LTSB release when used with the LTSB release.

When you use a LTSB client with the Current Branch, the client is supported for two years after the general availability of the LTSB, which is October 12th, 2016.  

Plan to update the LTSB client on devices that you manage with the Current Branch before support for the client expires. To do so you download a new LTSB client version from Microsoft and then deploy that updated client software to your devices that use the current LTSB client.

**Limitations of the LTSB client:**
- 	Updates for the LTSB client software are not available by using in-console updates. Additional details for deploying an updated client will be provided when an updated client is released.

## Identify the client version you use
Following are the major client versions available for both Current Branch and LTSB:

|Client version|Branch and version |  
|----------------|---------------------|
|5.00.8325.xxxx |	- Current Branch 1511|
|5.00.8355.xxxx	|- Current Branch 1602|
|5.00.8412.1307	|- Current Branch 1606 </br> - Current Branch 1606 with the 1606 hotfix rollup (KB3186654)</br>- Long-Term Servicing Branch|  

On the client you can view the client Version on the **General** tab of the Configuration Manager control panel applet.

On the **Components** tab of the applet, some components show different values. For example, for a client version 8412.1307, some components might be listed as 5.00.8412.**1000** or 5.00.8412.**1006**.  This different in the last four digits for some components is normal and does not indicate a failure of the component to update to the current client version.
