---
title: Common Education Windows Update configuration
description: Learn about common Windows Update configuration used by Eduation organizations in Intune
ms.date: 11/09/2023
ms.topic: overview
author: scottbreenmsft
ms.author: scbree
---

# Common Education Windows Update configuration

Create update rings that specify how and when Windows as a Service updates your Windows 10/11 devices with feature and quality updates.

In this article you will find Windows Update ring configuration that is commonly used for 1:1 student and teacher devices.

## Update rings for Windows 10 and later

Additional information:
- [Update rings for Windows 10 and later policy in Intune](/mem/intune/protect/windows-10-update-rings)
- [The Windows Update policies you should set and why](https://techcommunity.microsoft.com/t5/windows-it-pro-blog/the-windows-update-policies-you-should-set-and-why/ba-p/3270914)
- [教育機関向け Microsoft Intune を使った Windows Update 管理](https://youtu.be/o6_eGOyv-_g)
- [YouTube: Windows Update for Business Fundamentals](https://www.youtube.com/watch?v=TXwp-jLDcg0&list=PLMuDtq95SdKvpS9zPyFt9fc9HgepQxaw9&index=1)

### Update settings

|Update settings|Value|Notes|CSP|
|---|---|----|
|Microsoft product updates|Allow|Do not set to Block. In order to revert the configuration, a PowerShell commands will have to be run on each device.|AllowMUUpdateService|
|Windows drivers|Allow||ExcludeWUDriversInQualityUpdate|
|Quality update deferral period (days)|7||DeferQualityUpdatesPeriodInDays|
|Feature update deferral period (days)|30|Select 0 if using a Feature update policy otherwise select 30 days.|DeferFeatureUpdatesPeriodInDays|
|Upgrade Windows 10 devices to Latest Windows 11 release|No||ProductVersion|
|Set feature update uninstall period (2 - 60 days)|14||ConfigureFeatureUpdateUninstallPeriod|
|Enable pre-release builds|Not configured||ManagePreviewBuilds|
