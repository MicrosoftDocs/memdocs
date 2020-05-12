---
# required metadata

title: Use OEMConfig on Android Enterprise devices in Microsoft Intune - Azure | Microsoft Docs
description: Use Microsoft Intune to manage and use devices running Android Enterprise with OEMConfig. See all the steps, including an overview, see the prerequisites, create the configuration profile in Intune, and see a list of supported OEMConfig apps.
keywords:
author: MandiOhlinger
ms.author: mandia
manager: dougeby
ms.date: 03/02/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: configuration
ms.localizationpriority:
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Use and manage Android Enterprise devices with OEMConfig in Microsoft Intune

In Microsoft Intune, you can use OEMConfig to add, create, and customize OEM-specific settings for Android Enterprise devices. OEMConfig is typically used to configure settings that aren't built in to Intune. Different original equipment manufacturers (OEM) include different settings. The available settings depend on what the OEM includes in their OEMConfig app.

This feature applies to:  

- Android Enterprise

This article describes OEMConfig, lists the prerequisites, shows how to create a configuration profile, and lists the supported OEMConfig apps in Intune.

## Overview

OEMConfig policies are a special type of device configuration policy similar to [app configuration policy](../apps/app-configuration-policies-overview.md). OEMConfig is a standard defined by Google that uses app configuration in Android to send device settings to apps written by OEMs (original equipment manufacturers). This standard allows OEMs and EMMs (enterprise mobility management) to build and support OEM-specific features in a standardized way. [Learn more about OEMConfig](https://blog.google/products/android-enterprise/oemconfig-supports-enterprise-device-features/).

Historically, EMMs, such as Intune, manually build support for OEM-specific features after they're introduced by the OEM. This approach leads to duplicated efforts and slow adoption.

With OEMConfig, an OEM creates a schema that defines OEM-specific management features. The OEM embeds the schema into an app, and then puts this app on Google Play. The EMM reads the schema from the app, and exposes the schema in the EMM administrator console. The console allows Intune administrators to configure the settings in the schema.

When the OEMConfig app installs on a device, it uses the settings configured in the EMM administrator to manage the device. Device settings are executed by the OEMConfig app, instead of an MDM agent built by the EMM.

When the OEM adds and improves management features, the OEM also updates the app in Google Play. As an administrator, you get these new features and updates (including fixes) without waiting for EMMs to include these updates.

> [!TIP]
> You can only use OEMConfig with devices that support this feature and have a corresponding OEMConfig app. Consult your OEM for specific details.

## Before you begin

When using OEMConfig, be aware of the following information:

- Intune exposes the OEMConfig app's schema so you can configure it. Intune doesn't validate or change the schema provided by the app. So if the schema is incorrect, or has inaccurate data, then this data is still sent to devices. If you find a problem that originates in the schema, contact the OEM for guidance.
- Intune doesn't influence or control the content of the app schema. For example, Intune doesn't have any control over strings, language, the actions allowed, and so on. We recommend contacting the OEM for more information on managing their devices with OEMConfig.
- At any time, OEMs can update their supported features and schemas, and upload a new app to Google Play. Intune always syncs the latest version of the OEMConfig app from Google Play. Intune doesn't maintain older versions of the schema or the app. If you run into version conflicts, we recommend contacting the OEM for more information.
- Assign one OEMConfig profile to a device. If multiple profiles are assigned to the same device, you may see inconsistent behavior. The OEMConfig model only supports a single policy per device.

## Prerequisites

To use OEMConfig on your devices, be sure you have the following requirements:

- An Android Enterprise device enrolled in Intune.
- An OEMConfig app built by the OEM, and uploaded to Google Play. If it's not on Google Play, contact the OEM for more information.
- The Intune administrator has role-based access control (RBAC) permissions for **Mobile apps**, **Device Configurations**, and the "read" permission under **Android for Work**. These permissions are required because OEMConfig profiles use managed app configurations to manage device configurations.

## Prepare the OEMConfig app

Be sure the device supports OEMConfig, the correct OEMConfig app is added to Intune, and the app is installed on the device. Contact the OEM for this information.

> [!TIP] 
> OEMConfig apps are specific to the OEM. For example, a Sony OEMConfig app installed on a Zebra Technologies device doesn't do anything.

1. Get the OEMConfig app from the Managed Google Play Store. [Add Managed Google Play apps to Android enterprise devices](../apps/apps-add-android-for-work.md) lists the steps.
2. Some OEMs may ship devices with the OEMConfig app pre-installed. If the app isn't preinstalled, use Intune to [add and deploy the app to devices](../apps/apps-deploy.md).

## Create an OEMConfig profile

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Devices** > **Configuration profiles** > **Create profile**.
3. Enter the following properties:

    - **Platform**: Select **Android enterprise**.
    - **Profile type**: Select **OEMConfig**.

4. Select **Create**.
5. In **Basics**, enter the following properties:

    - **Name**: Enter a descriptive name for the new profile.
    - **Description**: Enter a description for the profile. This setting is optional, but recommended.
    - **OEMConfig app**: Choose **Select an OEMConfig app**.

6. In **Associated app**, select an existing OEMConfig app you previously added > **Select**. Be sure to choose the correct OEMConfig app for the devices you're assigning the policy to.

    If you don't see any apps listed, then set up Managed Google Play, and get apps from the Managed Google Play store. [Add Managed Google Play apps to Android Enterprise devices](../apps/apps-add-android-for-work.md) lists the steps.

    > [!IMPORTANT]
    > If you added an OEMConfig app and synced it to Google Play, but it's not listed as an **Associated app**, you may have to contact Intune to onboard the app. See [adding a new app](#supported-oemconfig-apps) (in this article).

7. Select **Next**.
8. In **Configure settings**, select the **Configuration designer** or **JSON editor**:

    > [!TIP]
    > Read the OEM documentation to make sure you're configuring the properties correctly. These app properties are included by the OEM, not Intune. Intune does minimal validation of the properties, or what you enter. For example, if you enter `abcd` for a port number, the profile saves as-is, and is deployed to your devices with the values you configure. Be sure you enter the correct information.

    - **Configuration designer**: When you select this option, the properties available within the app schema are shown for you to configure.

      - Context menus in the configuration designer indicate that more options are available. For example, the context menu might let you add, delete, and reorder settings. These options are included by the OEM. Be sure to read the OEM app documentation to learn how these options should be used to create profiles.

      - Many settings have default values supplied by the OEM. To see if there's a default value, hover over the info icon next to the setting. A tooltip shows the default values for that setting (if applicable), and more details provided by the OEM.

      - Clicking **Clear** deletes a setting from the profile. If a setting isn't in the profile, its value on the device won't change when the profile is applied.

      - If you create an empty (unconfigured) bundle in the configuration designer, it's deleted when switching to the JSON editor.

    - **JSON editor**: When you select this option, a JSON editor opens with a template for the full configuration schema embedded in the app. In the editor, customize the template with values for the different settings. If you use the **Configuration designer** to change your values, the JSON editor overwrites the template with values from the configuration designer.

      - If you're updating an existing profile, the JSON editor shows the settings that were last saved with the profile.

      - OEMConfig schemas can be large and complex. If you prefer to update these settings using a different editor, select the **Download JSON template** button. Use an editor of your choice to add your configuration values to the template. Then, copy and paste your updated JSON in to the **JSON editor** property.

      - You can use the JSON editor to create a backup of your configuration. After you configure your settings, use this feature to get the JSON settings with your values. Copy and paste the JSON to a file, and save it. Now you have a backup file.

    Any changes made in the configuration designer are also made automatically in the JSON editor. Likewise, any changes made in the JSON editor are automatically made in the configuration designer. If your input contains invalid values, you can't switch between the configuration designer and JSON editor until you fix the issues.

9. Select **Next**.
10. In **Scope tags** (optional), assign a tag to filter the profile to specific IT groups, such as `US-NC IT Team` or `JohnGlenn_ITDepartment`. For more information about scope tags, see [Use RBAC and scope tags for distributed IT](../fundamentals/scope-tags.md).

    Select **Next**.

11. In **Assignments**, select the users or groups that will receive your profile. Assign one profile to each device. The OEMConfig model only supports one policy per device.

    For more information on assigning profiles, see [Assign user and device profiles](device-profile-assign.md).

    Select **Next**.

12. In **Review + create**, review your settings. When you select **Create**, your changes are saved, and the profile is assigned. The policy is also shown in the profiles list.

The next time the device checks for configuration updates, the OEM-specific settings you configured are applied to the OEMConfig app.

> [!NOTE]
> The OEMConfig standard doesn't currently include status reporting. So, by default, profiles show a **Pending** status.

## Supported OEMConfig apps

Compared to standard apps, OEMConfig apps expand the managed configurations privileges granted by Google to support more complex schemas. Intune currently supports the following OEMConfig apps:

-----------------

| OEM | Bundle ID | OEM Documentation (if available) |
| --- | --- | ---|
| Ascom | com.ascom.myco.oemconfig | |
| Cipherlab | com.cipherlab.oemconfig | |
| Honeywell | com.honeywell.oemconfig |  |
| HMDGlobal - 7.2 | com.hmdglobal.app.oemconfig.n7_2 | 
| HMDGlobal - 4.2 | com.hmdglobal.app.oemconfig.n4_2 | 
| Kyocera | jp.kyocera.enterprisedeviceconfig |  |
| Samsung | com.samsung.android.knox.kpu | [Knox Service Plugin Admin Guide](https://docs.samsungknox.com/knox-service-plugin/admin-guide/index.htm) |
| Seuic | com.seuic.seuicoemconfig | |
| Spectralink - Barcodes | com.spectralink.barcode.service |  |
| Spectralink - Buttons | com.spectralink.buttons |  |
| Spectralink - Device | com.spectralink.slnkdevicesettings  |  |
| Spectralink - Logging | com.spectralink.slnklogger |  |
| Spectralink - VQO | com.spectralink.slnkvqo |  |
| Unitech Electronics | com.unitech.oemconfig | |
| Zebra Technologies | com.zebra.oemconfig.common | [Zebra OEMConfig overview](http://techdocs.zebra.com/oemconfig ) |

-----------------

If an OEMConfig application exists for your device, but it isn't in the table above, or isn't showing up in the Intune console, email `IntuneOEMConfig@microsoft.com`.

> [!NOTE]
> OEMConfig apps must on-boarded by Intune before they can be configured with OEMConfig profiles. Once an app is supported, you don't need to contact Microsoft about setting it up in your tenant. Just follow the instructions on this page.
>
> If you experience an OEMConfig app behaving incorrectly, then contact the developers of the OEMConfig app. Intune isn't responsible for technical issues with the individual OEMConfig apps.

## Next steps

[Monitor the profile status](device-profile-monitor.md).
