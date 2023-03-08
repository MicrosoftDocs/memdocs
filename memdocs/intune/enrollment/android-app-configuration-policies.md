---
# required metadata

title: Android Enterprise security configuration policies
titleSuffix: Microsoft Intune
description: Learn the restrictions and settings for Android Enterprise device basic and high security.
keywords:
author: Lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 06/24/2020
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

# Configure app configuration policies for fully managed devices   

Android Enterprise fully managed devices are intended exclusively for work or school use, so we recommend blocking users from connecting their personal accounts in Microsoft apps.  

## Block personal accounts  

1. Add the apps to Managed Google Play. For more information, see [Add Managed Google Play apps to Android Enterprise devices with Intune](../apps/apps-add-android-for-work.md).
2. Create an app configuration policy for each Managed Google Play app. For more information, see [Add app configuration policies for managed Android Enterprise devices](../apps/app-configuration-policies-use-android.md#create-an-app-configuration-policy).
3. Create the following single key in each policy:  

    | Key | Values |
    | --- | --- |
    | com.microsoft.intune.mam.AllowedAccountUPNs | One or more; delimited UPNs.<br>Only account(s) allowed are the managed user account(s) defined by this key.<br>For Intune enrolled devices, the {{userprincipalname}} token may be used to represent the enrolled user account. |


## Next steps
1. [Configure device enrollment restrictions for personal devices](device-enrollment-restrictions.md)
2. 🡺 **Configure app configuration policies** (*You are here*) 
3. [Configure security settings for personal devices](android-work-profile-security-settings.md)  
4. [Configure security settings for fully managed devices](android-fully-managed-security-settings.md) 