---
# required metadata

title: Resolve access point restrictions set in Intune
description: Review the three common messages for Intune's access point restriction policies and learn how to resolve them
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 05/28/2018
ms.topic: end-user-help
ms.service: microsoft-intune
ms.subservice: end-user
ms.assetid: 
searchScope:
 - User help


# optional metadata

ROBOTS:  
#audience:

ms.reviewer: arnab
#ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection:
- tier2
---

# Resolve access point restrictions

Organizations may restrict the locations from which devices access corporate data.
To configure these *access point restrictions*, they specify and set approved
network locations.  

When you try to connect to an unrecognized or unapproved network, you may receive one or more of the following messages:

* Access point restrictions aren't set up.
* You aren't connected to an approved network.
* An error occurred and the access point restrictions couldn't be enforced.

 The following tables list each message, what it means, and how to access your work resources again.

## Access point restrictions not set up  
| Company Portal message | What this message means | What you should do                                                               
|------------------------|--------------------------|--------------------------|
| **Access point restrictions are not set up – Access point restrictions are active and must be set up.** | Your company applied access point restrictions on your device. This setting requires the Company Portal app to verify a few network settings on your device. | Tap **Resolve.** The Company Portal app will check to ensure that you're connected to a company-approved network. |

## Not connected to an approved network  

| Company Portal message | What this message means | What you should do                                                                   
|------------------------|-----------------------------------|--------------------------|
| **Device is not connected to an approved network – Connect to an approved wireless network.** | You're connected to a network that isn't approved for work access. As long as you're connected to this network, you'll be unable to access work email, apps, and other protected corporate resources. | Connect to a company-approved network. Then tap **Resolve** to retry. |

## Restrictions couldn't be enforced  

| Company Portal message | What this message means | What you should do                                                                      
|------------------------|-----------------------------------|--------------------------|
| **Access point restrictions could not be enforced – Company Portal encountered an error.** | Intune can't determine if you're connected to an approved network. This error could be a result of poor network connectivity, low battery, battery saver mode, or a Company Portal error. | Verify that you have a strong network reception. Turn off battery saver mode and make sure your battery life has at least 30% remaining. Then tap **Resolve** to retry. 

Still need help? We recommend that you contact your company support. For specific contact information, go to the [Company Portal website](https://portal.manage.microsoft.com/#HelpDeskDialog).
