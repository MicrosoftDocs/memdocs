---
# required metadata

title: Data JAMF Pro sends to Intune
titleSuffix: Microsoft Intune
description: Review the list of data that Jamf Pro sends to Microsoft Intune when you integrate Jamf Pro to manage Macs with Intune.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 01/16/2019
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
ms.reviewer: elocholi
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---



# Data Jamf Pro sends to Intune

When you use [Jamf Pro](https://www.jamf.com) to manage your end-users Macs
with Intune, Jamf Pro captures inventory information about managed macOS devices. 

## Data  
For the list of data that Jamf Pro shares with Intune, see [Appendix: Inventory Information Shared with Microsoft Intune](https://docs.jamf.com/technical-papers/jamf-pro/microsoft-intune/10.9.0/Appendix__Inventory_Information_Shared_with_Microsoft_Intune.html) in the Jamf Pro technical documentation. 

<!--  
Jamf Pro reports the following information to Intune:  

* Device Azure AD ID
* JAMF Inventory State (inventory state of a computer checked in with Jamf Pro within the last 24 hours)
* OS Version
* User Azure AD ID
* Encrypted (FileVault 2)
* Gatekeeper Status
* Password: minimum number of character sets
* Password expiration (days)
* Password Type - simple, alphanumeric, or unknown
* Prevent Auto Login
* Required Passcode Length
* Password: number of previous passwords to prevent reuse
* System Integrity Protection
* Last Check-In Time
* Architecture Type
* Available RAM Slots
* Battery Capacity
* Boot ROM
* Bus Speed
* Cache Size
* Device Name
* Domain Join
* Jamf ID
* MAC address
* Make
* Model
* Model Identifier
* NIC Speed
* Number of Cores
* Number of Processors
* OS
* Platform
* Processor Speed
* Processor Type
* Secondary MAC Address
* Serial Number
* SMC Version
* Total RAM
* UDID
* User Email
--> 

<!-- 
You can remove a Jamf-managed device from the Intune console by selecting **Delete** in the **All devices** view. Bulk device deletion can be enabled by selecting multiple devices and clicking **Delete**.
-->

## Next steps
Get information on how to [remove a Jamf-managed device in the Jamf Pro docs](https://www.jamf.com/jamf-nation/articles/80/unmanaging-computers-while-preserving-their-inventory-information). You can also file a support ticket with [Jamf support](https://www.jamf.com/support/) for additional help. 

