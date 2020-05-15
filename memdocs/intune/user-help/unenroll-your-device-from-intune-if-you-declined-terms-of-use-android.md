---
# required metadata

title: Remove your device from management if you declined Terms of Use | Microsoft Docs
description:
keywords:
author: lenewsad
ms.author: lanewsad
manager: dougeby
ms.date: 03/23/2018
ms.topic: article
ms.prod:
ms.service: microsoft-intune
ms.subservice: end-user
ms.technology:
ms.assetid: 4278f000-0258-4de5-93a1-195b48e5061e
searchScope:
 - User help

# optional metadata

ROBOTS:
#audience:

ms.reviewer: chrisbal
ms.suite: ems
#ms.tgt_pltfrm:
ms.custom: intune-enduser
ms.collection: 
---


# Remove your device from management if you declined "Terms of Use"

If you declined the terms of use while trying to sign in to the Company Portal app, you are prevented from signing in to the Company Portal app on future tries, so you need to use these "workaround" instructions to remove your device from Intune.

When you uninstall the Company Portal app, you are also removing your device from Intune. Your device will no longer be able to access company resources. For more about what happens when you remove your device from management, see [What happens if you unenroll your device from Intune?](what-happens-if-you-unenroll-your-device-from-intune-android.md).

Before you can uninstall the Company Portal app, you have to go to the **Device administrators** setting, and turn off **Company Portal**. The steps may differ a little, depending on which Android device you have.

## Removing the device from the Company Portal app

To remove your device from Intune and uninstall the Company Portal app:

1. Go to **Settings** &gt; **Security &amp; Screen Lock** &gt; **Device administrators**.

    Completing this step immediately unenrolls your device.

2. Uncheck the box next to, or turn off, **Company Portal**.

    You can now uninstall the Company Portal app.

## Removing data collected by the Company Portal app

To remove all data that the Company Portal app for Android stores on your device:

- Clear app data in Applications -> Click on app -> button "Clear data"
- Delete the folder '\storage\internal storage\Android\data\com.microsoft.windowsintune.companyportal'


Still need help? Contact your company support (check the [Company Portal website](https://go.microsoft.com/fwlink/?linkid=2010980) for contact information), or write the <a href="mailto:wintunedroidfbk@microsoft.com?subject=I'm having unenrolling my Android device&body=Describe the issue you're experiencing here.">Microsoft Android team</a>.
