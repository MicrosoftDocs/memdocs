---
title: "Monitor Mobile Threat Defense compliance"
description: "Monitor the Mobile Threat Defense partner compliance status from the Configuration Manager manager console"
ms.custom: na
ms.date: 03/21/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 408190da-bea6-4122-9dd6-f90155040e88
caps.latest.revision:
author: andredm7
ms.author: andredm
manager: angrobe

---

# **Monitor Mobile Threat Defense compliance**

*Applies to: System Center Configuration Manager (Current Branch)*

## To monitor the overall compliance status

To monitor the mobile threat defense status:

1.  In the Configuration Manager console, click on **Monitoring** workspace.

2.  In the **Monitoring** workspace, click on the **Security** node.

You can see a summary of the compliance status with different threat levels, which is displayed in a visual chart format. You can click on the individual sections of the charts to see more information like: 

- The number of devices reporting as non-compliant by platform
- Any errors related to the device compliance status

![](http://i.imgur.com/bmPsiWk.png)

## To monitor the individual compliance status

You can also see the individual device status:

1.  In the Configuration Manager console, click on **Assets and compliance** workspace.

2.  Click on **Devices**.

> [!TIP] 
> You can add the **Device threat compliance** and the **Device threat level** columns to see the status. These columns are not displayed by default.

## Device Threat Protection tab

Additionally, on the **Devices** screen, you can select specific devices, then click on the **Device Threat Protection** tab that provides more details about the device compliance status. Find below the column descriptions and their expected values to help you analyze the device compliance status.

> [!IMPORTANT] 
> The Device Threat Protection tab only shows up if the selected device is a mobile device.

|Column name|Visible by default|Description| 
|-|-|-|
|**Description**| Yes | Details about the threat provided by the Mobile Threat Defense partner. |
|**Last update time**| Yes | The last time the Mobile Threat Defense partner sent updated detail about the threat to Intune. |
|**Threat severity**| Yes | Threat severity is the definition for an individual threat based on the configuration of the admin in the Mobile Threat Defense partner console. It has one of the three values: **Low**, **Medium** or **High** |
|**Threat status**| Yes | The current state of the threat on the device. Possible states: **Active**, **Resolved** or **Ignored:** Indicates that the user ignored the threat on their device, but the threat is still present. |
|**Threat type**| Yes | Mobile Threat Defense partner type of threat. Possible values: **App**, **File** or **OS** |
|**AAD Account ID**| No | The Azure Active Directory unique identifier. |
|**Classification**| Yes | Mobile Threat Defense partner provided classification of threat. Possible values: **Root Enabler, Riskware, Adware, Chargeware, DataLeak, Trojan, Worm, Virus, Exploit, Backdoor, Bot, AppDropper, ClickFraud, Spam, Spyware, SurveillanceWare, Vulnerability, Unknown, Root Jailbrake, Connectivity, TollFraud, SideloadedApp** |
|**Device ID**| No | The Azure Active Directory object ID representing the Workplace Joined Device with threat information. |
|**Threat ID**| No | Mobile Threat Defense partner generated unique identifier for the threat. The Threat ID is used for tracking resolution. |
|**Threat URL**| No | When present, the Threat URL links back to the Mobile Threat Defense partner’s management console view of this specific threat. |

> [!TIP] 
> Make sure to enable the columns that are not **visible by default** to see more details about the Mobile Threat Defense compliance status for your devices.
