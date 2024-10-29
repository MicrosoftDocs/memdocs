---
# required metadata

title: Understand app protection policy delivery and timing
titleSuffix: Microsoft Intune
description: Learn the different deployment windows for app protection policies to understand when changes should appear on your end user devices.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/20/2024
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.assetid: ec111319-7e02-434f-946b-88647726bf1a

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: scottduf
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection:
- tier2
- M365-identity-device-management
---

# Understand App Protection Policy delivery timing

Learn about the different delivery timing for app protection policies to understand when changes should appear on your end-user devices.

## Delivery timing summary

App protection policy (APP) delivery depends on the license state and Intune service registration for your users.  

|    User State    |    App Protection behavior     |    Retry Interval  (see note)    |    Why does this happen?    |
|-----------------------------------------------------|-------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------|
|    Tenant Not   Onboarded    |    Wait for   next retry interval. App Protection isn't active for the user.    |    24   hours    |    Occurs   when you have not setup your tenant for Intune.    |
|    User Not   Licensed     |    Wait for next   retry interval. App Protection isn't active   for the user.     |    12 hours - However, on Android devices this interval requires Intune APP SDK version 5.6.0 or later. Otherwise for Android devices, the interval is 24 hours.   |    Occurs when you   haven't licensed the user for Intune.    |
|    User Not   Assigned App Protection Policies    |    Wait for   next retry interval. App Protection isn't active for the user.    |    12 hours        |    Occurs when you   haven't assigned APP settings to the user.    |
|    User Assigned App Protection Policies but app isn't defined in the App Protection Policies   |    Wait for   next retry interval. App Protection isn't active for the user.    |    12 hours        |    Occurs when you   haven't added the app to APP.    |
|    User   Successfully Registered for Intune MAM    |    App   Protection is applied per policy settings.    Updates occur based on retry interval    |    Intune   Service defined based on user load.    Typically 30 mins.     |    Occurs when   the user has successfully registered with the Intune service for APP   configuration.    |

> [!NOTE]
> Retry intervals may require active app use to occur, meaning the app is launched and in use.  If the retry interval is 24 hours and the user waits 48 hours to launch the app, the Intune APP SDK will retry at 48 hours.

> [!NOTE]
> Applications that have not checked-in with the Intune MAM Service within the last 90 days may be automatically deregistered from the Intune MAM Service.  When the user next launches the application, the Intune APP SDK will automatically attempt to register the application.  The user may be prompted to connect to the internet and enter credentials to complete the registration.

## Handling network connectivity issues

When user registration fails due to network connectivity issues an accelerated retry interval is used. The Intune APP SDK retries at increasingly longer intervals until the interval reaches 60 minutes or a successful connection is made. The Intune APP SDK will then continue to retry at 60-minute intervals until a successful connection is made. Then, the Intune APP SDK returns to the standard retry interval based on the user state.

## Next steps

[Assign licenses to users so they can enroll devices in Intune](../fundamentals/licenses-assign.md)

