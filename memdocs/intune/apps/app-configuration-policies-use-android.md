---
# required metadata

title: Add app configuration policies for managed Android Enterprise devices
titleSuffix: Microsoft Intune
description: Use app configuration policies in Microsoft Intune to supply settings when users run a Managed Google Play app.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/08/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.assetid: d0b6f3fe-2bd4-4518-a6fe-b9fd115ed5e0


# optional metadata

#ROBOTS:
#audience:

ms.reviewer: esalter
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.collection:
- tier1
- M365-identity-device-management
- Android
- FocusArea_Apps_Configure
ms.custom: intune-azure
---

# Add app configuration policies for managed Android Enterprise devices

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

App configuration policies in Microsoft Intune supply settings to Managed Google Play apps on managed Android Enterprise devices. The app developer exposes Android-managed app configuration settings. Intune uses these exposed setting to let the admin configure features for the app. The app configuration policy is assigned to your user groups. The policy settings are used when the app checks for them, typically the first time the app runs.

Not every app supports app configuration. Check with the app developer to see if their app supports app configuration policies.

[!INCLUDE [android-supported-os](../includes/android-supported-os.md)]

## Email apps

Android Enterprise has several enrollment methods. The enrollment type depends on how email is configured on the device:

- On Android Enterprise Fully Managed, Dedicated, and Corporate-owned Work Profiles, use an app configuration policy and the steps in this article. App configuration policies support Gmail and Nine Work email apps.
- On Android Enterprise personally owned devices with a work profile, create an [Android Enterprise email device configuration profile](../configuration/email-settings-android-enterprise.md). When you create the profile, you can configure settings for email clients that support app configuration policies. When using the configuration designer, Intune includes email settings specific to Gmail and Nine Work apps.
<!-- commenting this bullet out for workitem: device admin end of support, 13891824
- On Android device administrator, create an [Android device administrator email device configuration profile](../configuration/email-settings-android.md) for Samsung Knox devices. When you create the profile, you can configure Exchange email settings, such as `outlook.office365.com`.-->

## Create an app configuration policy

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
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

    > [!NOTE]
    > As of Android 12, configuring **Auto grant** for the following permissions is not supported for coporate-owned work profile or corporate-owned dedicated devices.
    > * SMS (read)
    > * Location access (coarse)
    > * Location access (fine)
    > * Camera
    > * Record audio
    > * Allow body sensor data

11. If the managed app supports configuration settings, the **Configuration settings format** dropdown box is visible. Select one of the following methods to add configuration information:
    - **Use configuration designer**
    - **Enter JSON data**

    For details about using the configuration designer, see [Use configuration designer](#use-the-configuration-designer). For details about entering XML data, see [Enter JSON data](#enter-json-data).

12. If you need to enable users to connect the targeted app across both the work and personal profiles, select **Enabled** next to **Connected apps**.

    :::image type="content" source="./media/app-configuration-policies-use-android/app-configuration-policies-use-android-01.png" alt-text="Screenshot of configuration policy - Settings":::

    > [!NOTE]
    > This setting only works for personally owned work profile and corporate-owned work profile devices.
    > 
    > Changing the **Connected apps** setting to **Not Configured** will not remove the configuration policy from the device. To remove the **Connected apps** functionality from a device, you must unassign the related configuration policy.

13. Click **Next** to display the **Scope tags** page.
14. [Optional] You can configure scope tags for your app configuration policy. For more information about scope tags, see [Use role-based access control (RBAC) and scope tags for distributed IT](../fundamentals/scope-tags.md).
15. Click **Next** to display the **Assignments** page. 
16. In the dropdown box next to **Assign to**, select either **Add groups**, **Add all users**, or **Add all devices** to assign the app configuration policy. Once you've selected an assignment group, you can select a [filter](../fundamentals/filters.md) to refine the assignment scope when deploying app configuration policies for managed devices.

    :::image type="content" alt-text="Screenshot of policy assignments - Assignments" source="./media/app-configuration-policies-use-android/app-configuration-policies-use-android-02.png" ::: 

17. Select **All users** in the dropdown box.

    :::image type="content" alt-text="Screenshot of policy assignments - All Users dropdown option" source="./media/app-configuration-policies-use-android/app-configuration-policies-use-android-03.png" :::

18. [Optional] Click **Edit filter** to add a [filter](../fundamentals/filters.md) and refine the assignment scope.

    :::image type="content" alt-text="Screenshot of policy assignments - Edit filter" source="./media/app-configuration-policies-use-android/app-configuration-policies-use-android-04.png" :::

16. Click **Select groups to exclude** to display the related pane.

17. Choose the groups you want to exclude and then click **Select**.

    >[!NOTE]
    >When adding a group, if any other group has already been included for a given assignment type, it is pre-selected and unchangeable for other include assignment types. Therefore, that group that has been used, cannot be used as an excluded group.

18. Click **Next** to display the **Review + create** page.
19. Click **Create** to add the app configuration policy to Intune.

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
| Microsoft Entra Device ID | dc0dc142-11d8-4b12-bfea-cae2a8514c82 |
| Account ID | fc0dc142-71d8-4b12-bbea-bae2a8514c81 |
| Intune Device ID | b9841cd9-9843-405f-be28-b2265c59ef97 |
| Domain | contoso.com |
| Mail | john@contoso.com |
| Partial UPN | john |
| User ID | 3ec2c00f-b125-4519-acf0-302ac3761822 |
| User name | John Doe |
| User Principal Name | john@contoso.com |

### Allow only configured organization accounts in apps 

As the Microsoft Intune administrator, you can control which work or school accounts are added to Microsoft apps on managed devices. You can limit access to only allowed organization user accounts and block personal accounts on enrolled devices. For Android devices, use the following key/value pairs in a Managed Devices app configuration policy:

| Key | com.microsoft.intune.mam.AllowedAccountUPNs |
|---|---|
| **Values** | <ul><li>One or more <code>;</code> delimited UPNs.</li><li>Only account(s) allowed are the managed user account(s) defined by this key.</li><li> For Intune enrolled devices, the <code>{{userprincipalname}}</code> token may be used to represent the enrolled user account.</li></ul> |

   > [!NOTE]
   > The following apps process the above app configuration and only allow organization accounts:
   > - Copilot for Android (28.1.420328045 and later)
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

## Enable connected apps

Applies to:<br>
Android 11+

Personally owned work profile users must have Company Portal version 5.0.5291.0 or newer. Corporate-owned work profile users do not need a specific version of the Microsoft Intune app for support.

You can allow users using Android personally owned and corporate-owned work profiles to turn on connected apps experiences for supported apps. This app configuration setting enables apps to connect and integrate app data across the work and personal app instances.

For an app to provide this experience, the app needs to integrate with Google's connected apps SDK, so only limited apps support it. You can turn on the connected apps setting proactively, and when apps add support, users will be able to enable the connected apps experience.

Changing the **Connected apps** setting to **Not Configured** will not remove the configuration policy from the device. To remove the **Connected apps** functionality from a device, you must unassign the related configuration policy.

> [!WARNING]
> If you enable the connected apps functionality for an app, work data in personal apps will not be protected by an app protection policy.
> 
> Additionally, regardless of your connected apps configuration, some OEMs may automatically connect certain apps or may be able to request user approval to connect apps that you did not configure. An example of an app in this case could be the OEM's keyboard app.

There are two ways users may be able to connect work and personal apps after you've enabled the connected apps setting:
1. A supported app may choose to prompt a user to approve connecting it across profiles.
2. Users can open the Settings app and go to the Connected work & personal apps section, where they will see all supported apps listed.

> [!IMPORTANT]
> If multiple app configuration policies are assigned for the same app targeting the same device, and one policy sets **Connected Apps** to `Enabled` while the other policy does not, the app configuration will report a conflict and the resulting behavior applied on the device will be to disallow the connected apps.

## Preconfigure the permissions grant state for apps

You can also preconfigure app permissions to access Android device features. By default, Android apps that require device permissions, such as access to location or the device camera, prompt users to accept or deny permissions.

For example, an app uses the device's microphone. The user is prompted to grant the app permission to use the microphone.

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **App configuration policies** >  **Add** > **Managed devices**.
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

- [Assign a Managed Google Play app to Android Enterprise personally owned and corporate-owned work profile devices](apps-add-android-for-work.md#assign-a-managed-google-play-app-to-android-enterprise-personally-owned-and-corporate-owned-work-profile-devices)
- [Deploying Outlook for iOS/iPadOS and Android app configuration settings](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/outlook-for-ios-and-android-configuration-with-microsoft-intune)

## Next steps

Continue to [assign](apps-deploy.md) and [monitor](apps-monitor.md) the app.
