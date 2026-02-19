---
title: iOS/iPadOS bundle IDs for built-in apps in Microsoft Intune
description: See a list of the bundle IDs for the built-in iOS and iPadOS apps. Use these bundle IDs to explicitly allow apps in device configuration profiles and policies in Microsoft Intune.
ms.date: 09/22/2025
ms.topic: reference
ms.collection:
- M365-identity-device-management
---

# Bundle IDs for built-in iOS and iPadOS apps you can use in Intune

When you configure features on iOS/iPadOS devices, you can also add the built-in apps on these devices. This article lists the bundle IDs of some common built-in iOS/iPadOS apps.

To get the bundle ID of other apps, you can:

- [Get the app bundle ID using the Intune admin center](../apps/get-app-bundle-id-intune-admin-center.md).
- Go to Apple's list of [iOS/iPadOS bundle IDs](https://support.apple.com/guide/deployment/bundle-ids-for-native-ios-and-ipados-apps-depece748c41/1/web/1.0) (opens Apple's web site).

> [!TIP]
> On macOS devices, you can get the bundle ID using the Terminal app and AppleScript: `osascript -e 'id of app "AppName"'`.

This feature applies to:

- iOS/iPadOS

## Bundle IDs

| Bundle ID                   | App Name     | Publisher |
|-----------------------------|--------------|-----------|
| com.apple.AppStore          | App Store    | Apple     |
| com.apple.store.Jolly       | Apple Store  | Apple     |
| com.apple.calculator        | Calculator   | Apple     |
| com.apple.mobilecal         | Calendar     | Apple     |
| com.apple.camera            | Camera       | Apple     |
| com.apple.mobiletimer       | Clock        | Apple     |
| com.apple.clips             | Clips        | Apple     |
| com.apple.compass           | Compass      | Apple     |
| com.apple.MobileAddressBook | Contacts     | Apple     |
| com.apple.facetime          | FaceTime     | Apple     |
| com.apple.DocumentsApp      | Files        | Apple     |
| com.apple.mobileme.fmf1     | Find Friends | Apple     |
| com.apple.mobileme.fmip1    | Find iPhone  | Apple     |
| com.apple.games             | Games        | Apple     |
| com.apple.gamecenter        | Game Center  | Apple     |
| com.apple.mobilegarageband  | GarageBand   | Apple     |
| com.apple.Health            | Health       | Apple     |
| com.apple.Home              | Home         | Apple     |
| com.apple.iBooks            | iBooks       | Apple     |
| com.apple.iMovie            | iMovie       | Apple     |
| com.apple.itunesconnect.mobile | iTunes Connect | Apple |
| com.apple.MobileStore       | iTunes Store | Apple     |
| com.apple.itunesu           | iTunes U     | Apple     |
| com.apple.Keynote           | Keynote      | Apple     |
| com.apple.mobilemail        | Mail         | Apple     |
| com.apple.Maps              | Maps         | Apple     |
| com.apple.measure           | Measure      | Apple     |
| com.apple.MobileSMS         | Messages     | Apple     |
| com.apple.Music             | Music        | Apple     |
| com.apple.news              | News         | Apple     |
| com.apple.mobilenotes       | Notes        | Apple     |
| com.apple.Numbers           | Numbers      | Apple     |
| com.apple.Pages             | Pages        | Apple     |
| com.apple.Passwords         | Passwords    | Apple     |
| com.apple.mobilephone       | Phone        | Apple     |
| com.apple.Photo-Booth       | Photo Booth  | Apple     |
| com.apple.mobileslideshow   | Photos       | Apple     |
| com.apple.podcasts          | Podcasts     | Apple     |
| com.apple.preview           | Preview      | Apple     |
| com.apple.reminders         | Reminders    | Apple     |
| com.apple.mobilesafari      | Safari       | Apple     |
| com.apple.Preferences       | Settings     | Apple     |
| com.apple.shortcuts         | Shortcuts    | Apple     |
| com.apple.SiriViewService   | Siri         | Apple     |
| com.apple.stocks            | Stocks       | Apple     |
| com.apple.tips              | Tips         | Apple     |
| com.apple.tv                | TV           | Apple     |
| com.apple.videos            | Videos       | Apple     |
| com.apple.VoiceMemos        | VoiceMemos   | Apple     |
| com.apple.Passbook          | Wallet       | Apple     |
| com.apple.Bridge            | Watch        | Apple     |
| com.apple.weather           | Weather      | Apple     |
| com.apple.barcodesupport.qrcode| QR Code Reader | Apple |


## Next steps

Use these bundle IDs to configure [device features](device-features-apple.md) and to [allow or restrict some settings](device-restrictions-apple.md) on iOS/iPadOS devices.
