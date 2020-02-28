---
# required metadata

title: Bind Android devices by network location in Microsoft Intune - Azure | Microsoft Docs
description: Create or configure network locations in Microsoft Intune for Android devices. You can mark devices as noncompliant based on the device's network location. If the device goes outside the network location, you can block access to company resources.
keywords:
author: Brenduns
ms.author: brenduns
manager: dougeby
ms.date: 11/13/2019
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: ayesham
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Use Locations (network fence) in Intune

You may want to block access to a corporate network if a device leaves a location. The **Locations** feature in Intune provides this functionality. 

You can create a network location-based compliance policy, also known as network fencing. The policy ensures devices must be connected to a work network to be compliant. This policy can be used with Conditional Access policies so devices have access to work resources *only* when the device is connected to the work network. When the device isn't connected to the work network, the device becomes not compliant, and loses access to work resources.

Consider the following scenario:

In your manufacturing facility, some employees use Android devices. An employee takes the Android device outside the facility or plant. To help prevent unauthorized access, you can:

1. Create a location with an IPv4 range called **Manufacturing floor**.
2. Create a compliance policy that requires these devices to be connected to your corporate network, and assign this policy.
3. If the device goes outside the manufacturing plant, then the device is considered not compliant, and doesn't have access to corporate resources.

Additionally, you can add [actions for non-compliance](#configure-the-actions-for-noncompliance). When the device is back on-premises and in the network location, it will regain access to corporate resources.

## Prerequisites

To create a location-based compliance policy:

- Create a network location as IPV4 network ranges for the Gateway Server, DHCP server, and/or DNS server that the devices connect
- Create the compliance policy that uses these locations, and defines the action taken when the device is no longer connected to the network location
- Android devices 6.0 and higher, with the updated Company Portal app

## Create a location

1. In the [Microsoft Endpoint Manager Admin Center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Devices** > **Compliance policies** > **Locations** > **Create**.

2. Enter the following properties:  

   - Required. Enter a **Name** for the location, such as **Manufacturer floor**, or **Building 44-secure**.
   - Optional. Enter an **IPv4 Range** with CIDR (Classless Interdomain Routing) notation, such as `aaa.bbb.ccc.ddd/n`.
   - Optional. Enter the **IPv4 Gateway** address, such as `aaa.bbb.ccc.ddd`.
   - Optional. Enter the **IPv4 DHCP Server** address, such as `aaa.bbb.ccc.ddd`.
   - Optional. Enter a list of **IPv4 DNS Servers** addresses. This setting uses **subset matching**. If the IPv4 DNS Servers on the device are subsets of the values defined, then the device is considered as IN the fence. Be sure to enter one address per line, such as:  
     `aaa.bbb.ccc.ddd`  
     `aaa.bbb.ccc.ddd`
   - Optional. Enter a list of **DNS Suffixes**. This setting uses **subset matching**. If the DNS Suffixes on the device are subsets of the values defined, then the device is considered as IN the fence. Be sure to enter one domain name on each line, such as:  
     `contoso.com`  
     `contoso.org`

3. **Save** your changes.

## Create the location compliance policy

When you [create the compliance policy](create-compliance-policy.md), select **Android** for the **Platform**. In **Locations**, you can choose one or more of the network locations you added. These locations are part of the network fence you're creating for your devices.

## Configure the actions for noncompliance

After the compliance policy is created, the default action for noncompliance applies to the device. You can add more actions. For example, add an action that sends an email to the user when the device is no longer compliant with the locations.

[Add actions for noncompliance](actions-for-noncompliance.md) provides some guidance.

## Company Portal app

When the device is connected to your locations, the device is shown as compliant in the Company Portal app. When the device isn't connected to one of your locations, the device is shown as not-compliant.

## Next steps

[Monitor device compliance policies](compliance-policy-monitor.md)  
[Get started with compliance policies](device-compliance-get-started.md)
