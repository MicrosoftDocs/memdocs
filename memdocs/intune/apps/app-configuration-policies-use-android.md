---
# required metadata

title: Add app configuration policies for managed Android Enterprise devices
titleSuffix: Microsoft Intune
description: Use app configuration policies in Microsoft Intune to supply settings when users run a Managed Google Play app.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/25/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology:
ms.assetid: d0b6f3fe-2bd4-4518-a6fe-b9fd115ed5e0


# optional metadata

#ROBOTS:
#audience:

ms.reviewer: chrisbal
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Add app configuration policies for managed Android Enterprise devices

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

App configuration policies in Microsoft Intune supply settings to Managed Google Play apps on managed Android Enterprise devices. The app developer exposes Android-managed app configuration settings. Intune uses these exposed setting to let the admin configure features for the app. The app configuration policy is assigned to your user groups. The policy settings are used when the app checks for them, typically the first time the app runs.

> [!NOTE]  
> Not every app supports app configuration. Check with the app developer to see if their app supports app configuration policies.

## Email apps

Android Enterprise has several enrollment methods. The enrollment type depends on how email is configured on the device:

- On Android Enterprise Fully Managed, Dedicated, and Corporate-owned Work Profiles, use an app configuration policy and the steps in this article. App configuration policies support Gmail and Nine Work email apps.
- On Android Enterprise personally owned devices with a work profile, create an [Android Enterprise email device configuration profile](../configuration/email-settings-android-enterprise.md). When you create the profile, you can configure settings for email clients that support app configuration policies. When using the configuration designer, Intune includes email settings specific to Gmail and Nine Work apps.
- On Android device administrator, create an [Android device administrator email device configuration profile](../configuration/email-settings-android.md) for Samsung Knox devices. When you create the profile, you can configure Exchange email settings, such as `outlook.office365.com`.

## Create an app configuration policy

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Choose the **Apps** > **App configuration policies** > **Add** > **Managed devices**. Note that you can choose between **Managed devices** and **Managed apps**. For more information see [Apps that support app configuration](app-configuration-policies-overview.md#apps-that-support-app-configuration).
3. On the **Basics** page, set the following details:
    - **Name** - The name of the profile that appears in the portal.
    - **Description** - The description of the profile that appears in the portal.
    - **Device enrollment type** - This setting is set to **Managed devices**.
4. Select **Android Enterprise** as the **Platform**.
5. Click **Select app** next to **Targeted app**. The **Associated app** pane is displayed. 
6. On the **Associated app** pane, choose the managed app to associate with the configuration policy and click **OK**.
7. Click **Next** to display the **Settings** page.
8. Click **Add** to display the **Add permissions** pane.
9. Click the permissions that you want to override. Permissions granted will override the "Default app permissions" policy for the selected apps.
10. Set the **Permission state** for each permission. You can choose from **Prompt**, **Auto grant**, or **Auto deny**.  
11. If the managed app supports configuration settings, the **Configuration settings format** dropdown box is visible. Select one of the following methods to add configuration information:
    - **Use configuration designer**
    - **Enter JSON data**

    For details about using the configuration designer, see [Use configuration designer](#use-the-configuration-designer). For details about entering XML data, see [Enter JSON data](#enter-json-data).

12. Click **Next** to display the **Assignments** page.
13. In the dropdown box next to **Assign to**, select either **Selected groups**, **All users**, **All devices**, or **All users and all devies** to assign the app configuration policy to.

    ![Screenshot of Policy assignments Include tab](./media/app-configuration-policies-use-ios/app-config-policy01.png)

14. Select **All users** in the dropdown box.

    ![Screenshot of Policy assignments - All Users dropdown option](./media/app-configuration-policies-use-ios/app-config-policy02.png)

15. Click **Select groups to exclude** to display the related pane.

    ![Screenshot of Policy assignments - Select groups to exclude pane](./media/app-configuration-policies-use-ios/app-config-policy03.png)

16. Choose the groups you want to exclude and then click **Select**.

    >[!NOTE]
    >When adding a group, if any other group has already been included for a given assignment type, it is pre-selected and unchangeable for other include assignment types. Therefore, that group that has been used, cannot be used as an excluded group.

17. Click **Next** to display the **Review + create** page.
18. Click **Create** to add the app configuration policy to Intune.

## Use the configuration designer

You can use the configuration designer for Managed Google Play apps when the app is designed to support configuration settings. Configuration applies to devices enrolled in Intune. The designer lets you configure specific configuration values for the settings exposed by the app.

1. Select **Add**. Choose the list of configuration settings that you want to enter for the app.

    If you're using Gmail or Nine Work email apps, [Android Enterprise device settings to configure email](../configuration/email-settings-android-enterprise.md) has more information on these specific settings.

2. For each key and value in the configuration, set:

    - **Value type**: The data type of the configuration value. For String value types, you can optionally choose a variable or certificate profile as the value type.
    - **Configuration value**: The value for the configuration. If you select variable or certificate for the **Value type**, choose from a list of variables or certificate profiles. If you choose a certificate, then the certificate alias of the certificate deployed to the device is populated at runtime.

### Supported variables for configuration values

You can choose the following options if you choose variable as the value type:

| Option | Example |
|----|----|
| Azure AD Device ID | dc0dc142-11d8-4b12-bfea-cae2a8514c82 |
| Account ID | fc0dc142-71d8-4b12-bbea-bae2a8514c81 |
| Intune Device ID | b9841cd9-9843-405f-be28-b2265c59ef97 |
| Domain | contoso.com |
| Mail | john@contoso.com |
| Partial UPN | john |
| User ID | 3ec2c00f-b125-4519-acf0-302ac3761822 |
| User name | John Doe |
| User Principal Name | john@contoso.com |

### Allow only configured organization accounts in multi-identity apps 

As the Microsoft Intune administrator, you can control which work or school accounts are added to Microsoft apps on managed devices. You can limit access to only allowed organization user accounts and block personal accounts on enrolled devices. For Android devices, use the following key/value pairs in a Managed Devices app configuration policy:

| **Key** | com.microsoft.intune.mam.AllowedAccountUPNs |
|---|---|
| **Values** | <ul><li>One or more <code>;</code> delimited UPNs.</li><li>Only account(s) allowed are the managed user account(s) defined by this key.</li><li> For Intune enrolled devices, the <code>{{userprincipalname}}</code> token may be used to represent the enrolled user account.</li></ul> |

   > [!NOTE]
   > The following apps process the above app configuration and only allow organization accounts:
   > - Edge for Android (42.0.4.4048 and later)
   > - Office, Word, Excel, PowerPoint for Android (16.0.9327.1000 and later)
   > - OneDrive for Android (5.28 and later)
   > - OneNote for Android (16.0.13231.20222 or later)
   > - Outlook for Android (2.2.222 and later)
   > - Teams for Android (1416/1.0.0.2020073101 and later)

## Enter JSON data

Some configuration settings on apps (such as apps with Bundle types) can't be configured with the configuration designer. Use the JSON editor for those values. Settings are supplied to apps automatically when the app is installed.

1. For **Configuration settings format**, select **Enter JSON editor**.
2. In the editor, you can define JSON values for configuration settings. You can choose **Download JSON template** to download a sample file that you can then configure.
3. Choose **OK**, and then choose **Add**.

The policy is created and shown in the list.

When the assigned app is run on a device, it runs with the settings that you configured in the app configuration policy.

## Preconfigure the permissions grant state for apps

You can also preconfigure app permissions to access Android device features. By default, Android apps that require device permissions, such as access to location or the device camera, prompt users to accept or deny permissions.

For example, an app uses the device's microphone. The user is prompted to grant the app permission to use the microphone.

1. In the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **App configuration policies** >  **Add** > **Managed devices**.
2. Add the following properties:
    - **Name**: Enter a descriptive name for the policy. Name your policies so you can easily identify them later. For example, a good policy name is **Android Enterprise prompt permissions app policy for entire company**.
    - **Description**. Enter a description for the profile. This setting is optional, but recommended.
    - **Device enrollment type**: This setting is set to **Managed devices**.
    - **Platform**: Select **Android Enterprise**.
3. Select **Profile Type**:
3. Select **Targeted App**. Choose the app that you want to associate a configuration policy with. Select from the list of Android Enterprise fully managed work profile apps that you've approved and synchronized with Intune.
4. Select **Permissions** > **Add**. From the list, select the available app permissions > **OK**.
5. Select an option for each permission to grant with this policy:
    - **Prompt**. Prompt the user to accept or deny.
    - **Auto grant**. Automatically approve without notifying the user.
    - **Auto deny**. Automatically deny without notifying the user.
6. To assign the app configuration policy, select the app configuration policy > **Assignment** > **Select groups**. Choose the user groups to assign > **Select**.
7. Choose **Save** to assign the policy.

## Additional information

- [Assign a Managed Google Play app to Android Enterprise personally-owned and corporate-owned work profile devices](apps-add-android-for-work.md#assign-a-managed-google-play-app-to-android-enterprise-personally-owned-and-corporate-owned-work-profile-devices)
- [Deploying Outlook for iOS/iPadOS and Android app configuration settings](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune)

## Next steps

Continue to [assign](apps-deploy.md) and [monitor](apps-monitor.md) the app.
