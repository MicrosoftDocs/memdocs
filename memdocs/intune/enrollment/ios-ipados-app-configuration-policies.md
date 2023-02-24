---
# required metadata

title: iOS/iPadOS security app configuration policies
titleSuffix: Microsoft Intune
description: Learn the app configuration policies for iOS/iPadOS devices.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 04/15/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: enrollment
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: rosssmi
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure;seodec18
ms.collection:
- tier2
- M365-identity-device-management
---

# iOS/iPadOS security configuration framework app configuration policies

As part of the [iOS/iPadOS security configuration framework](ios-ipados-configuration-framework.md), you must properly set app configuration policies for iOS/iPadOS devices.

iOS/iPadOS supervised devices are designed to be used for work or school data only. So, Microsoft apps deployed on these devices must be configured to disallow personal accounts.

## Disallow personal accounts for Microsoft apps on iOS/iPadOS devices

1. Add the iOS apps so that they can be deployed to the device. For more information, see [Add iOS store apps to Microsoft Intune](../apps/store-apps-ios.md).
2. Create a policy for each Microsoft app as described in [Add app configuration policies for managed iOS/iPadOS devices](../apps/app-configuration-policies-use-ios.md).
3. Create the following single key in each policy: 

    | Key | Values |
    | --- | --- |
    | IntuneMAMAllowedAccountsOnly | **Enabled**: The only account allowed is the managed user account defined by the IntuneMAMUPN key.<br>**Disabled** (or any value that is not a case insensitive match to **Enabled**): Any account is allowed. |
    | IntuneMAMUPN | UPN of the account allowed to sign into the app. For Intune enrolled devices, the {{userprincipalname}} token may be used to represent the enrolled user account. |

## Next steps
Apply [iOS/iPadOS device compliance security configuration settings](ios-ipados-device-compliance-security-configurations.md).
