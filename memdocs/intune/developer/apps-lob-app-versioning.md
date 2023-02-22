---
# required metadata

title: Line-of-business app versioning in Intune
description: Introduces how app versions are used in Intune when an app is added or updated.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/16/2021
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: developer
ms.localizationpriority: medium
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: jamiesil
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection:
- tier3
- M365-identity-device-management
---

# Line-of-business app versioning

When you add or update a line-of-business (LOB) app in Microsoft Intune, the version property of the app is extracted to detect and install the app on devices. The version value is stored in the **identityVersion** property of the LOB app entity. When the LOB app is updated, the Intune service compares the versions of the existing and updated app packages. If the versions are the same, the Intune service rejects the update.

The following items are considered as the version property of the app:

- App package-specific versions. Some app types contain more than one of these properties.
- The **InternalVersion** property that's specified in the app's metadata. This value refers to the internal tracking version for the content of the app, specifically when the app is updated.
- The **MetadataVersion** property that's specified in the app's metadata. This value refers to the internal tracking version for the metadata changes that have been applied to the app. The property is reset for each revision of the **InternalVersion** property.

## Locations where you can view the app version

In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), you can view the app version in the following locations:

- When you add the app to Intune, the version is displayed in the **App package file** pane. The version value will be used for the **identityVersion** property.

  :::image type="content" source="media/apps-lob-app-versioning/apps-lob-app-versioning-01.png" alt-text="Select app package file":::
- When you select an existing LOB app, the version is displayed in the details pane. The version value is the value of the **identityVersion** property.

  :::image type="content" source="media/apps-lob-app-versioning/apps-lob-app-versioning-02.png" alt-text="View an existing app":::
- You can select to view the version in the list of apps. The version value is the value of the **identityVersion** property.
  
  :::image type="content" source="media/apps-lob-app-versioning/apps-lob-app-versioning-03.png" alt-text="View app versions":::

You can see the version when you install the app from the Company Portal app.

:::image type="content" source="media/apps-lob-app-versioning/apps-lob-app-versioning-03.png" alt-text="View app version during installation":::

- For .appx and .apk files, the version value is the value of the **identityVersion** property.
- For other types of files, the version value is the value of the **InternalVersion** property in the app's metadata.

## iOS app packages

The iOS app package (.ipa) files contain two version-related keys:

- CFBundleShortVersionString: This key stores the version number.
- CFBundleVersion: This key stores the build number.

For more information about these keys, see [Apple Technical Note TN2420: Version Numbers and Build Numbers](https://developer.apple.com/library/content/technotes/tn2420/_index.html).

Currently, Intune uses the **CFBundleVersion** value for the **identityVersion** property of the [iosLobApp](/graph/api/resources/intune-apps-ioslobapp?view=graph-rest-beta&preserve-view=true) entity.

### Extract the version number and build number of the iOS app

To manually extract the version number and build number of an .ipa file in Windows, follow these steps:

1. Rename the *\<AppName>.ipa* file to *\<AppName>.zip*.
1. Extract the *\<AppName>.zip* file to a folder.
1. Go to the folder that contains the extracted files, open the `Payload\<AppName>.app` folder, and locate the Info.plist file.
1. Open the Info.plist file in a supported editor.
1. Check the values of the CFBundleShortVersionString and CFBundleVersion keys.

## Android app packages

The Android app package (.apk) files contain two version-related attributes:

- `android:versionCode`: An internal version number. This number is used only to determine whether one version is more recent than another (higher numbers indicate more recent versions). This value isn't the version number that's shown to users.
- `android:versionName`: The version number that's shown to users. This attribute can be set as a raw string, or as a reference to a string resource. The string has no other purpose than to be displayed to users. The **versionCode** attribute holds the significant version number used internally.

These attributes are stored in the app manifest file AndroidManifest.xml. For more information, see [Android developer guide: \<manifest>](https://developer.android.com/guide/topics/manifest/manifest-element#vcode).

Currently, Intune uses the **versionCode** value for the **identityVersion** property of the [androidLobApp](/graph/api/resources/intune-apps-androidlobapp?view=graph-rest-beta&preserve-view=true) entity.

### Extract the versionCode and versionName attributes of the Android app

To manually extract the attributes of an .apk file in Windows, follow these steps:

1. [Install the Apktool](https://ibotpeaches.github.io/Apktool/install/).
1. Run the Apktool to decode the .apk file to a folder. For example, run the following command:

   ```console
   apktool d <AppName>.apk -o <OutputFolder>
   ```

1. Go to the \<OutputFolder> folder, and open the AndroidManifest.xml file in an editor.
1. Check the values of the `android:versionCode` and `android:versionName` attributes. Here's an example:

   ```xml
   <manifest xmlns:android="http://schemas.android.com/apk/res/android"
          package="com.realtechvr.nogravity"
          android:versionCode="17"
          android:versionName="1.1.7"
          android:installLocation="preferExternal" >
    ...
   </manifest>
   ```

> [!NOTE]
> The third-party products that this article discusses are manufactured by companies that are independent of Microsoft. Microsoft makes no warranty, implied or otherwise, about the performance or reliability of these products.

## Next steps

To learn more about LOB apps, see the following topics:

- [Add apps to Microsoft Intune](../apps/apps-add.md)<br>
- [Prepare line-of-business apps for app protection policies](../developer/apps-prepare-mobile-application-management.md)<br>

