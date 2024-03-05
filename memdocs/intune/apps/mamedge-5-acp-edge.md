---
# required metadata

title: Use App Configuration Policies for Microsoft Edge for Business
titleSuffix:
description: Use App Configuration Policy for Microsoft Edge for Business.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/04/2024
ms.topic: overview
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology:

# optional metadata

#audience:
#ROBOTS: 
ms.reviewer: samarti
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: 
ms.collection:
- tier1
- highpri
- highseo
- FocusArea_Apps_AppManagement
---

# App Configuration Policies for Microsoft Edge for Business

Microsoft Edge for iOS and Android supports app settings that allow Microsoft Intune administrators to customize the behavior of the app and implement Browser Configuration.

App configuration can be delivered either through the mobile device management (MDM) OS channel on enrolled devices [Managed App Configuration](https://developer.apple.com/library/content/samplecode/sc2279/Introduction/Intro.html) channel for iOS or the [Android in the Enterprise](https://developer.android.com/work/managed-configurations) channel for Android) or through the MAM (Mobile Application Management) channel. Microsoft Edge for iOS and Android supports the following configuration scenarios:

- Only allow work or school accounts
- General app configuration settings
- Data protection settings
- Additional app configuration for managed devices

**Important**

For configuration scenarios that require device enrollment on Android, the devices must be enrolled in Android Enterprise and Microsoft Edge for Android must be deployed via the Managed Google Play store. For more information, see [**Set up enrollment of Android Enterprise personally-owned work profile devices**](/mem/intune/enrollment/android-work-profile-enroll) and [**Add app configuration policies for managed Android Enterprise devices**](/mem/intune/apps/app-configuration-policies-use-android).

We have evaluated the different Microsoft Edge App Configuration and have identified the following key items that need to be configured, we'll then guide you through the process of creating an App Configuration on Microsoft Intune Admin Center.

**Table  Browser App Configurations**

|    Key                                                               	|    Value                                                              	|
|--------------------------------------------------------------------------	|---------------------------------------------------------------------------	|
|    com.microsoft.intune.mam.managedbrowser.PasswordSSO               	|    TRUE                                                               	|
|    com.microsoft.intune.mam.managedbrowser.disableShareUsageData     	|    TRUE                                                               	|
|    com.microsoft.intune.mam.managedbrowser.disabledFeatures          	|    password\|inprivate\|autofill\|translator\|drop\|developer tools    	|
|    com.microsoft.intune.mam.managedbrowser.disableImportPasswords    	|    TRUE                                                               	|
|    com.microsoft.intune.mam.managedbrowser.SmartScreenEnabled        	|    TRUE                                                               	|
|    com.microsoft.intune.mam.managedbrowser.account.syncDisabled      	|    TRUE                                                               	|
|    com.microsoft.intune.IntuneMAMOnly.AdvancedEncryption             	|    enabled                                                            	|

#### To configure the App Configuration, perform the following steps.

1. Go to <https://intune.microsoft.com/>.

Once authenticated select on **Apps** on the left menu.

2. Select on **App configuration policies.**

:::image type="content" alt-text="Apps - App configuration policies - Microsoft Intune Admin Center." source="./media/securing-data-edge-for-business/securing_data_edge_for_business48.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business48.png":::

3. Select **Add** \> **Managed apps.**

4. On the Create app configuration policy,** enter the following information.

> **Name:** Browser ACP
>
> **Description:** Secure Enterprsie Browser ACP Configuration
>
> **Target Policy to:** Selected apps
>
> \+ **Select Public Apps** \> type Edge and select the deseired **Edge
> Configuration**, for this example we will select **iOS/IPadOS**.

:::image type="content" alt-text="Apps - App configuration policies - Microsoft Intune Admin Center." source="./media/securing-data-edge-for-business/securing_data_edge_for_business49.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business49.png":::

5. Select **Select** on the **Microsoft Edge iOS/IPAD OS** and
then select **Next.**

6. Select **Next** on **Settings Catalog** \> **Settings** \>
Expand **General configuration settings.**

7. Enter each of the **names** and **keys** from **The Table**
into each section.

:::image type="content" alt-text="Apps  -  App configuration policies  -  Create app configuration policy- Microsoft Intune Admin Center" source="./media/securing-data-edge-for-business/securing_data_edge_for_business50.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business50.png":::

8. Review each value and select **Next.**

9. Add a **Scope tag** and select **Next.**

10. Review Assignment and select **Next.**

11. **Review + create.**

:::image type="content" alt-text="Apps - App configuration policies - Create app configuration policy - Review + create -Microsoft Intune Admin Center." source="./media/securing-data-edge-for-business/securing_data_edge_for_business51.png" lightbox="./media/securing-data-edge-for-business/securing_data_edge_for_business51.png":::

> [!NOTE]
> Now that the app configuration policy has been created you can repeat steps 1 to 11 and choose a different OS depending on your need.
