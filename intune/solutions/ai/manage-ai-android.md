---
title: Control AI features on Android Enterprise devices
description: Using Microsoft Intune, you can manage and restrict AI usage on Android devices enrolled in Intune. This guide provides lists the steps in Intune to block AI apps, websites, screen-driven experiences, on-device AI services, and OEM-specific AI features. You can manage Microsoft Copilot, Google Gemini, Samsung Galaxy AI, claude.ai, ChatGPT, and more.
ms.date: 11/11/2025
ms.topic: how-to
ms.reviewer: cchristenson
ms.collection:
  - M365-identity-device-management
  - intune-scenario
---

# Manage AI on Android with Intune - A Guide for IT Admins

In Microsoft Intune, you can manage and restrict generative AI usage on Android devices enrolled in Intune. You can block (or allow) AI apps, websites, screen-driven experiences, on-device AI services, and OEM-specific AI features.

This article lists different ways that AI experiences can be available on Android devices, and how you can use Intune to block these experiences.

When you use the steps in this guide, you can manage and restrict AI experiences on your Android devices.

Applies to:

- Android Enterprise

??Add link to Android SC article, SC common tasks??

## Prerequisites

:::row:::
:::column span="1":::
[!INCLUDE [platform](../../includes/requirements/platform.md)]

:::column-end:::
:::column span="3":::
> IT admins and security engineers can allow/block generative AI on the following Android enrollment types:
>
> - Android Enterprise corporate owned fully managed devices (COBO)
> - Android Enterprise corporate owned dedicated devices (COSU)
> - Android Enterprise corporate owned devices with a work profile (COPE)
> - Android Enterprise personally owned devices with a work profile (BYOD)
>
> To learn more about the different Android enrollment options, see the [Android Enrollment guide](../../intune-service/fundamentals/deployment-guide-enrollment-android.md).
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [device-configuration](../../includes/requirements/device-configuration.md)]

:::column-end:::
:::column span="3":::
> - Devices enrolled in Intune, including co-managed devices
> - Managed Google Play account linked in the Intune admin center (**Devices > Android > Enrollment > Managed Google Play**)
:::column-end:::
:::row-end:::

:::row:::
:::column span="1":::
[!INCLUDE [rbac](../../includes/requirements/rbac.md)]

:::column-end:::
:::column span="3":::
> To configure the policies, use an account with the following role:
>
> - [!INCLUDE [minimum-rbac-role-policy-profile-manager](../../intune-service/includes/minimum-rbac-role-policy-profile-manager.md)]
:::column-end:::
:::row-end:::

## Before you begin

- When you create the AI policies, you can assign them to the **All Users** and **All Devices** groups. Even though this assignment is the simplest approach, you can target your policies to specific users and devices.

  To learn more, see:

  - [Inclusion and exclusion groups](../../intune-service/apps/apps-inc-exl-assignments.md) to assign apps that target specific users and devices.
  - [Assign policies in Intune](../../intune-service/configuration/device-profile-assign.md) that target specific users and devices.

- For corporate owned devices with a work profile (COPE) and personally owned devices with a work profile (BYOD), most controls are available only in the work profile. They're not available in the personal profile.
- The steps in this guide show you how to block AI experiences. If you want to allow specific AI experiences, you can use the same steps but configure them to allow instead of block.
- When you create a policy and assign it, the devices receive the policy the next time they check in with Intune. To learn more, see [Intune policy refresh intervals](../../intune-service/configuration/device-profile-troubleshoot.md#policy-refresh-intervals).

## How AI shows up on Android

On Android devices, AI is available in several ways:

- **AI apps** - Standalone apps like ChatGPT, Microsoft Copilot, and Perplexity can be downloaded and used on the devices.
- **AI websites** - Users can access AI websites through browser apps, like Microsoft Edge and Chrome.
- **Screen-driven and Assistant experiences** - OS-integrated features that read on-screen content (like Circle to Search) or provide assistant help are typically installed and available by default.
- **On-device AI services** - Android can run the on-device **Gemini Nano** foundational model locally using **AICore**. Apps like Messages, Recorder, or GBoard use Gemini Nano to respond to messages, generate summaries, and suggest smart replies.
- **OEM-specific AI services** - OEMs might implement their own AI capabilities, like Galaxy AI by Samsung.

## Block AI apps

✅ **Goal - End users can't install AI apps from the Google Play Store**

AI apps like ChatGPT, Copilot, Perplexity, and Claude can be installed from the Google Play Store. You can use Intune to block these apps from being installed on your devices.

# [Corporate owned devices](#tab/ai-apps-corp)

**Supported enrollment types**:

- Corporate owned fully managed devices (COBO)
- Corporate owned dedicated devices (COSU)
- Corporate owned devices with a work profile (COPE)

### Step 1 - Determine your app strategy

Determine your organization's app strategy - **Block or Allow**:

- **Block strategy** - No apps in the Google Play Store can be downloaded unless assigned by admins. Only apps that are assigned are available on the device.

  This strategy is the default for corporate owned devices.

- **Allow strategy** - All apps can be downloaded unless specifically blocked by admins.

  If the following setting is set to **Allow** in a device restrictions configuration profile, then your organization is probably using an Allow strategy. This setting allows non-admin specified apps to be downloaded:

  - **Devices** > **Android Enterprise** > **Configuration** > **Create** > **New Policy** > **Templates** > **Device Restrictions** > **Applications** > **Allow access to all apps in Google Play store**

### Step 2 - Implement your app strategy

In this step, implement your app strategy to block or allow AI apps.

#### Block strategy (default)

With a Block strategy, no apps in the Google Play Store can be downloaded unless explicitly allowed. Use the following steps to make sure the app you want to block isn't already deployed to your devices.

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Apps > Android > Android apps**.
2. Select the app name > **Properties**.
3. Make sure **Assignments** is not set to **Required**, not set to **Available for enrolled devices**, or not set to **Available with or without enrollment**.

If all these options aren't set, then the app hasn't been deployed by an Intune policy. If any of these options are set, then the app is deployed. In this scenario, you can change the assignment to **Uninstall** to remove it from the devices.

#### Allow strategy

With an Allow strategy, all apps in the Google Play Store can be downloaded.

1. Determine if the **Allow access to all apps in Google Play store** setting is set to allow.

    If you use [Copilot](../../intune-service/copilot/copilot-intune-overview.md), you can ask Copilot to check this setting for you. You can also create a new device restrictions profile to configure this setting.

    1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices** > **Configuration** > **Create** > **New Policy**

    2. Configure the following properties and select **Create**:

        - **Platform**: Select **Android Enterprise**.
        - **Profile type**: Select **Templates** > **Fully Managed, Dedicated, and Corporate-Owned Work Profile** > **Device restrictions**.

    3. Expand the **Applications** category and set the **Allow access to all apps in Google Play store** setting to **Allow**.

    4. Select **Next** and continue creating the profile. For step-by-step instructions, see [Create device profiles](../../intune-service/configuration/device-profile-create.md).

2. Add the apps you want to block.

    When they're added to Intune, you can block the apps. Then they're considered managed apps.

    1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Apps > Android > Create > Managed Google Play app**.
    2. Select the AI app you want to block > **Sync**.
    3. In **Apps > Android > Android apps**, make sure the app is shown in the list. The sync might take a few minutes.

3. Blocks specific apps by assigning them for **Uninstall**:

    If the apps are already installed on devices, assigning them for **Uninstall** removes them from the devices.

    1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Apps > Android > Android apps**.
    2. Select the AI app you want to uninstall > **Properties**.
    3. Select **Assignments** > **Edit**.
    4. In **Uninstall**, add a group, users, or devices.

# [Personally owned devices](#tab/ai-apps-personal)

**Supported enrollment types**:

- Personally owned devices with a work profile (BYOD)

By default, no apps in the Google Play Store can be downloaded unless explicitly allowed. Use the following steps to make sure the app you want to block isn't already deployed to your devices.

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Apps > Android > Android apps**.
2. Select the AI app > **Properties**.
3. Make sure **Assignments** is not set to **Required**, not set to **Available for enrolled devices**, or not set to **Available with or without enrollment**.

If all these options aren't set, then the app hasn't been deployed by an Intune policy.

It's possible the app was installed manually by the user or through another MDM solution. In this situation, set the assignment to **Uninstall** to remove it from the devices.

---

## Block AI Websites

✅ **Goal - Block AI websites in web browser apps**

You can use Intune app configuration policies to block access to AI websites in web browser apps, like Microsoft Edge and Chrome. Only the websites you enter are blocked. So, you can also use this approach to only allow specific AI websites. If you use multiple browsers, you need to create a separate policy for each web browser app.

**Supported enrollment types**:

- Corporate owned fully managed devices (COBO)
- Corporate owned dedicated devices (COSU)
- Corporate owned devices with a work profile (COPE)
- Personally owned devices with a work profile (BYOD)

### Step 1 - Add your web browser as a managed app

To configure the browser settings, you first need to add the browser app to Intune so it becomes a managed app.

For the steps, see:

- It's possible the browser app is [built-in](../../intune-service/apps/apps-add-built-in.md).
- If the app isn't built in, then you can [add your browser app from the Play Store](../../intune-service/apps/store-apps-android.md).

### Step 2 - Create an app configuration policy

Use the following steps to create an app configuration policy that configures your web browser app to block access to the AI websites you enter.

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Apps > Configuration > Create > Managed devices**.
2. In **Basics**, configure the following properties:

    - **Name**: Enter a name for the policy, like **Block AI Websites in Edge**.
    - **Platform**: Select **Android Enterprise**.
    - **Profile type**: Select your enrollment type:

      - Fully Managed, Dedicated, and Corporate-Owned Work Profile Only
      - Personally Owned Work Profile devices

    - **Targeted app**: Select the browser app you added, like Edge or Chrome.

3. Select **Next**.
4. In **Settings** > **Configuration settings format**, select **Enter JSON data**. Enter the list of URLs to block. For example, enter:

    ```json
    {
      "key": "URLBlocklist",
      "valueStringArray": [ "https://chatgpt.com", "https://claude.ai", "https://copilot.microsoft.com", "https://perplexity.ai", "https://gemini.google.com" ]
    }
    ```

5. Select **Next** and continue creating the policy. For step-by-step instructions, see [Add App Configuration Policies for Managed Android Enterprise Devices](../../intune-service/apps/app-configuration-policies-use-android.md).

## Block Screen-Driven AI Experiences

✅ **Goal - Block features that can read on-screen content**

AI features can read on-screen content, and can provide insights & recommendations from screenshots and content displayed on the screen. Some of these features are built into the OS, like Circle to Search, and some are provided by assistant apps.

To block these features, you can use Intune to restrict screenshot abilities and block content sharing with privileged apps.

# [Fully managed<br/>Dedicated](#tab/screen-fully-managed)

**Supported enrollment types**:

- Corporate owned fully managed devices (COBO)
- Corporate owned dedicated devices (COSU)

### Step 1 - Implement Basic Coverage

[!INCLUDE [ai-android-block-assist-settings-catalog](../../includes/ai-android-block-assist-settings-catalog.md)]

### Step 2 - Implement Comprehensive Coverage (Optional)

For more comprehensive protection, you can also restrict screenshot abilities and other functionalities by blocking screen captures.

This setting blocks AI features from accessing on-screen content, but also disables screenshots device-wide.

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices > Configuration > Create > New policy**.
2. Enter the following properties:

    - **Platform**: Select **Android Enterprise**.
    - **Profile type**: Select **Settings catalog**.

3. Select **Create**.
4. In **Basics**, enter a **Name** for the profile, and select **Next**.
5. Select **Add settings**.
6. Select the **General** category > **Block Screen capture** setting. Set its value to **True**.

    This setting blocks AI features from accessing on-screen content. End users can't take screenshots on the device.

7. Select **Next** and continue creating the profile. For step-by-step instructions, see [Create device profiles](../../intune-service/configuration/device-profile-create.md).

# [Corporate owned with work profile](#tab/screen-corporate-owned)

**Supported enrollment types**:

- Corporate owned devices with a work profile (COPE)

### Step 1 - Implement Basic Coverage

[!INCLUDE [ai-android-block-assist-settings-catalog](../../includes/ai-android-block-assist-settings-catalog.md)]

### Step 2 - Implement Comprehensive Coverage (Optional)

For more comprehensive protection, you can also restrict screenshot abilities and other functionalities using the following settings:

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices > Configuration > Create > New policy**.
2. Enter the following properties:

    - **Platform**: Select **Android Enterprise**.
    - **Profile type**: Select **Settings catalog**.

3. Select **Next**.
4. In **Basics**, enter a **Name** for the profile, and select **Next**.
5. Select **Add settings**.
6. Select the **General** category and configure the following settings:

    - **Allow copy and paste between work and personal profiles**: Set to **False**. This setting blocks copy and paste functionality between work and personal profiles. This helps ensure that no data from the work profile leaks into AI apps in the personal profile.

    - **Block screen capture**: Set to **True**. This setting blocks AI features from accessing on-screen content. End users can't take screenshots in the work profile.

    - **Data sharing between work and personal profiles**: Set to **Block all sharing between profiles**. This setting blocks data sharing between work and personal profiles. It helps ensure that no data from the work profile leaks into AI apps in the personal profile.

7. Select the **Personal profile** category and configure the following setting:

    - **Block screen capture**: Set to **True**. This setting blocks AI features from accessing on-screen content. End users can't take screenshots in the personal profile.

8. Select **Next** and continue creating the profile. For step-by-step instructions, see [Create device profiles](../../intune-service/configuration/device-profile-create.md).

9. Create a device restrictions profile to block specific AI apps. This setting isn't available in the settings catalog. So, that's why you create a separate device restrictions profile.

    1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices > Configuration > Create > New policy**.
    2. Enter the following properties:

        - **Platform**: Select **Android Enterprise**.
        - **Profile type**: Select **Templates** > **Fully managed, dedicated, and Corporate-owned work profile** > **Device restrictions**.

    3. Select **Create**.
    4. In **Basics**, enter a **Name** for the profile, and select **Next**.
    5. In **Configuration settings**, expand the **Personal profile** category and configure the following settings:

        - **Type of restricted apps list**: Set to **Blocked Apps** and add the AI apps you want to block.

    6. Continue creating the profile and assign the profile. For step-by-step instructions, see [Create device profiles](../../intune-service/configuration/device-profile-create.md).

# [Personally owned with work profile](#tab/screen-personal)

**Supported enrollment types**:

- Personally owned devices with a work profile (BYOD)

To prevent sensitive data from being used by AI apps in the personal profile, you can configure the following settings. These settings help you manage data flow from the work profile to the personal profile.

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices > Configuration > Create > New policy**.
2. Enter the following properties:

    - **Platform**: Select **Android Enterprise**.
    - **Profile type**: Select **Templates > Personally-Owned work profile > Device restrictions**.

3. Select **Create**.
4. In **Basics**, enter a **Name** for the profile, and select **Next**.
5. In **Configuration settings**, expand **Work profile settings** category. The following settings and their default values help limit AI data leakage. If any of these settings are changed from their default values, you should change them back to the defaults.

    - **Copy and paste between work and personal profiles**: Set to **Block** (default).
    - **Data sharing between work and personal profiles**: Set to **Device Default**. Device Default restricts sharing between work and personal profiles.

6. Select **Next** and continue creating the profile. For step-by-step instructions, see [Create device profiles](../../intune-service/configuration/device-profile-create.md).

---

## Disable On-Device AI System App

✅ **Goal - Block Google's local AI processing**

Gemini Nano is Google's on-device foundation model and processes AI interactions on the device. It enables AI summary and message reply capabilities in Messages, Recorder, GBoard, and other services. You can use Intune to disable the AICore system app.

**Supported enrollment types**:

- Corporate owned fully managed devices (COBO)
- Corporate owned dedicated devices (COSU)
- Corporate owned devices with a work profile (COPE)
- Personally owned devices with a work profile (BYOD)

Use the following steps to disable the AICore system app.

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps > Android > Create**.
2. In **Select app type**, select **Other > Android Enterprise system app**, and then choose **Select**.
3. In **App information**, configure the following properties, and then select **Next**:

   - **Name**: Enter `AICore`.
   - **Publisher**: Enter `Google Android`.
   - **Package Name**: Enter `com.google.android.aicore`.

4. In **Scope tags**, select **Next**.
5. In **Assignments > Uninstall**, select the group assignments for the app. When you select **Uninstall**, the app is disabled.

    Select **Next**.

6. In **Review + create**, review the values and settings you entered for the app. When you're done, select **Create**.

## Disable OEM-Specific AI Capabilities

✅ **Goal - Turn off OEM‑provided AI features**

OEMs can include their own AI features and capabilities on the device, like the Samsung Galaxy AI experiences through the Knox Service Plugin. These features are typically managed through the OEM's OEMConfig app. Using Intune, you can configure the OEMConfig app to manage these AI features.

To configure the OEMConfig app, you need to know the AI settings available in the app. Contact your OEMs to get a list of available AI controls in their OEMConfig apps.

For a list of supported OEMConfig apps, see [OEMConfig in Intune - Supported OEMConfig apps](../../intune-service/configuration/android-oem-configuration-overview.md#supported-oemconfig-apps).

**Supported enrollment types**:

- Corporate owned fully managed devices (COBO)
- Corporate owned dedicated devices (COSU)
- Corporate owned devices with a work profile (COPE)
- Personally owned devices with a work profile (BYOD)

Use the following steps to add, deploy, and configure the OEMConfig app and its AI capabilities.

### Step 1 - Add the OEMConfig app

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Apps > Android > Create > Managed Google Play app > Select**.
2. Select the OEMConfig app you want to configure.
3. Choose **Select** > **Sync**.

Make sure the app is shown in the list (**Apps > Android > Android apps**). The sync can take a few minutes.

### Step 2 - Deploy the OEMConfig app

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Apps > Android > Android apps**.
2. Select the OEMConfig app you added.
3. Select **Properties** > **Assignments** > **Edit**.
4. Add your group and/or users to the following **Assignments**:

    - Required
    - Available for enrolled devices
    - Available with or without enrollment

5. Review and save your changes.

### Step 3 - Configure the OEMConfig app

1. In the [Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), go to **Devices > Manage devices > Configuration > Create > New policy**.
2. Enter the following properties:

   - **Platform**: Select **Android Enterprise**.
   - **Profile type**: Select **Templates > OEMConfig**.

3. Select **Create**.
4. In **Basics**, configure the following properties, and then select **Next**:

    - **Name**: Enter a name for the profile.
    - **OEMConfig app**: Select the OEMConfig app you added and assigned.

5. In **Configuration settings**, select **Configuration designer** or **JSON editor** to configure the settings available in the OEMConfig app. If you select **Configuration designer**, you might be able to use the **Locate** search box to find AI-related settings.

    The available settings depend on the OEMConfig app you select. Contact your OEM to get a list of available AI controls in their OEMConfig apps.

6. Select **Next** and continue creating the profile. For step-by-step instructions, see [Use and manage Android Enterprise devices with OEMConfig](../../intune-service/configuration/android-oem-configuration-overview.md).

    Make sure you assign the profile to the same groups and/or users you assigned the OEMConfig app to.

## Related content

- [Android enrollment guide](../../intune-service/fundamentals/deployment-guide-enrollment-android.md)
- [Include and exclude app assignments in Microsoft Intune](../../intune-service/apps/apps-inc-exl-assignments.md)
- [Assign apps to groups in Microsoft Intune](../../intune-service/apps/apps-deploy.md)
- [Use OEMConfig on Android Enterprise devices in Microsoft Intune](../../intune-service/configuration/android-oem-configuration-overview.md)
- [Microsoft Intune support for Apple Intelligence](https://techcommunity.microsoft.com/blog/intunecustomersuccess/microsoft-intune-support-for-apple-intelligence/4254037)
