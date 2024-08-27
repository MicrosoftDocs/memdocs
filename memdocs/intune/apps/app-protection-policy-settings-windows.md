---
# required metadata

title: App protection policy settings for Windows
titleSuffix: Microsoft Intune
description: This topic describes the app protection policy (APP) settings for MAM on Windows.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 06/24/2024
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.assetid: 0f8b08f2-504c-4b38-bea2-b8a4ef0526b8

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: demerson
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# App protection policy settings for Windows

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

This article describes app protection policy (APP) settings for Windows. The policy settings that are described can be [configured](app-protection-policies.md) for an app protection policy on the **Settings** pane in the Intune admin center when you make a new policy. 

You can enable protected MAM access to org data via Microsoft Edge on personal Windows devices. This capability is known as [Windows MAM](../apps/protect-mam-windows.md) and provides functionality using Intune Application Configuration Policies (ACP), Intune Application Protection Policies (APP), Windows Security Center client threat defense, and Application Protection Conditional Access. For more information about Windows MAM, see [Data protection for Windows MAM](../apps/protect-mam-windows.md), [Create an MTD app protection policy for Windows](../protect/mtd-app-protection-policy.md#to-create-an-mtd-app-protection-policy-for-windows), and [Configure Microsoft Edge for Windows with Intune](../apps/manage-microsoft-edge-windows.md).

There are two categories of app protection policy settings for Windows:
- [Data protection](../apps/app-protection-policy-settings-windows.md#data-protection)
- [Health Checks](../apps/app-protection-policy-settings-windows.md#health-checks)

> [!IMPORTANT]
> Intune MAM on Windows supports unmanaged devices.  If a device is already managed, then Intune MAM enrollment will be blocked and APP settings will not be applied.  If a device becomes managed after MAM enrollment, APP settings will no longer be applied.

## Data protection

The **Data protection** settings impact the org data and context. As the admin, you can control the movement of data into and out of the context of org protection. The org context is defined by documents, services, and sites accessed by the specified org account. The following policy settings help control external data received into the org context and org data sent out of the org context.  

### Data Transfer
| Setting | How to use | Default value |
|------|----------|-------|
| **Receive data from** | Select one of the following options to specify the sources org users can receive data from:<br><ul><li>**All sources**: Org users can open data from any account, document, location, or application into the org context.</li><li>**No sources**: Org users can't open data from external accounts, documents, locations, or applications into the org context. **NOTE**: For Microsoft Edge, **No sources** controls file upload behavior either via drag and drop or the file open dialog. Local file viewing and sharing files between sites/tabs will be blocked.</li></ul><br><br> | **All sources** |
| **Send org data to** | Select one of the following options to specify the destinations org users can send data to:<br><ul><li>**All destinations**: Org users can send org data to any account, document, location, or application.</li><li>**No destinations**: Org users can't send org data to external accounts, documents, locations, or applications from the org context. **NOTE**: For Microsoft Edge, **No destinations** blocks file download. This means sharing files between sites/tabs will be blocked.</li></ul><br><br> | **All destinations** |
| **Allow cut, copy, and paste for** | Select one of the following options to specify the sources and destinations org users can cut or copy or paste org data:<br><ul><li>**Any destination and any source**: Org users can paste data from and cut/copy data to any account, document, location, or application.</li><li>**No destination or source**: Org users can't cut, copy, or paste data to or from external accounts, documents, locations or applications from or into the org context. **NOTE**: For Microsoft Edge, **No destination or source** blocks cut, copy, and paste behavior within the web content only. Cut, copy, and paste are disabled from all web content, but not application controls, including the address bar.</li></ul><br><br> | **Any destination and any source** |

### Functionality
| Setting | How to use | Default value |
|------|----------|-------|
| **Printing Org data** | Select **Block** to prevent printing of org data. Select **Allow** to permit printing of org data. Personal or unmanaged data isn't affected.  | **Allow**  |

## Health Checks

Set the health check conditions for your app protection policy. Select a **Setting** and enter the **Value** that users must meet to access your org data. Then select the **Action** you want to take if users do not meet your conditionals. In some cases, multiple actions can be configured for a single setting. For more information, see [Health Check Actions]().

### App conditions

Configure the following health check settings to verify the application configuration before allowing access to org accounts and data.

> [!NOTE]
> The term ***policy-managed app*** refers to apps that are configured with app protection policies.

| Setting | How to use | Default value |
|------|----------|-------|
| **Offline grace period** | The number of minutes that policy-managed app can run offline. Specify the time (in minutes) before the access requirements for the app are rechecked.<p>*Actions* include: <br><ul><li>**Block access (minutes)**: The number of minutes that policy-managed apps can run offline. Specify the time (in minutes) before the access requirements for the app are rechecked. After the configured period expires, the app blocks access to work or school data until network access is available. The Offline grace period timer for blocking data access is calculated based on last check-in with the Intune service.  This policy-setting format supports a positive whole number.</li><li>**Wipe data (days)**: After this many days (defined by the admin) of running offline, the app will require the user to connect to the network and reauthenticate. If the user successfully authenticates, they can continue to access their data and the offline interval will reset.  If the user fails to authenticate, the app will perform a selective wipe of the users' account and data.  See [How to wipe only corporate data from Intune-managed apps](apps-selective-wipe.md) for more information on what data is removed with a selective wipe. The Offline grace period timer for wiping data is calculated by the app based on last check-in with the Intune service. This policy setting format supports a positive whole number.</li></ul>This entry can appear multiple times, with each instance supporting a different action.<br><br> | Block access (minutes): **720** minutes (12 hours)<p>Wipe data (days): **90** days  |
| **Min app version** | Specify a value for the minimum application version value.<p>*Actions* include: <br><ul><li>**Warn** - The user sees a notification if the app version on the device doesn't meet the requirement. This notification can be dismissed.</li><li>**Block access** - The user is blocked from access if the app version on the device doesn't meet the requirement. </li><li>**Wipe data** - The user account that is associated with the application is wiped from the device. </li></ul> </li></ul>   As apps often have distinct versioning schemes between them, create a policy with one minimum app version targeting one app.<br><br> This entry can appear multiple times, with each instance supporting a different action.<br><br> This policy setting supports matching Windows app bundle version formats (major.minor or major.minor.patch).  | *No default value* |
| **Min SDK version** | Specify a minimum value for the Intune SDK version.<p>*Actions* include: <br><ul><li>**Block access** - The user is blocked from access if the app's Intune app protection policy SDK version doesn't meet the requirement. </li><li>**Wipe data** - The user account that is associated with the application is wiped from the device. </li></ul></li></ul>This entry can appear multiple times, with each instance supporting a different action.|  *No default value*   |
| **Disabled account** | Specify an automated action if the Microsoft Entra account for the user is disabled.  Admin may specify only one Action.  There is no value to set for this setting.   *Actions* include: <br><ul><li>**Block access** - When we have confirmed the user has been disabled in Microsoft Entra ID, the app blocks access to work or school data.</li><li>**Wipe data**  - When we have confirmed the user has been disabled in Microsoft Entra ID, the app will perform a selective wipe of the users' account and data. </li></ul> **NOTE:** If user status can't be confirmed due to connectivity, authentication or any other reason, these actions (**Block access** and **Wipe data**) will not be enforced.  | *No default value* |

### Device conditions

Configure the following health check settings to verify the device configuration before allowing access to org accounts and data.
Similar device based settings can be configured for enrolled devices. Learn more about configuring device compliance settings for enrolled devices.

| Setting | How to use | Default value |
|------|----------|-------|
| **Min OS version** | Specify a minimum Windows operating system to use this app.<p>*Actions* include: <br><ul><li>**Warn** - The user will see a notification if the Windows version on the device doesn't meet the requirement. This notification can be dismissed. </li><li>**Block access** - The user will be blocked from access if the Windows version on the device doesn't meet this requirement.</li><li>**Wipe data** - The user account that is associated with the application is wiped from the device.  </li></ul> </li></ul>This entry can appear multiple times, with each instance supporting a different action.<br><br> This policy setting format supports either major.minor, major.minor.build, major.minor.build.revision. <br><br> To find the Windows version, open a Command Prompt. The version is displayed at the top of the Command Prompt window. An example of the version format to use is **10.0.22631.3155**. Note, if you use the `winver` command, you will only see the OS Build (such as 22631.3155), which isn't the correct format to use. | |
| **Max OS version** | Specify a maximum Windows operating system to use this app.<p>*Actions* include: <br><ul><li>**Warn** - The user will see a notification if the Windows version on the device doesn't meet the requirement. This notification can be dismissed. </li><li>**Block access** - The user will be blocked from access if the Windows version on the device doesn't meet this requirement.</li><li>**Wipe data** - The user account that is associated with the application is wiped from the device.  </li></ul><br>This entry can appear multiple times, with each instance supporting a different action.<br><br> This policy setting format supports either major.minor, major.minor.build, major.minor.build.revision.  | |
| **Max allowed device threat level** | App protection policies can take advantage of the Intune-MTD connector. Specify a maximum threat level acceptable to use this app. Threats are determined by your chosen Mobile Threat Defense (MTD) vendor app on the end user device. Specify either *Secured*, *Low*, *Medium*, or *High*. *Secured* requires no threats on the device and is the most restrictive configurable value, while *High* essentially requires an active Intune-to-MTD connection.<p>*Actions* include: <br><ul><li>**Block access** - The user will be blocked from access if the threat level determined by your chosen Mobile Threat Defense (MTD) vendor app on the end user device doesn't meet this requirement.</li><li>**Wipe data** - The user account that is associated with the application is wiped from the device.</li></ul><br>For more information on using this setting, see [Enable MTD for unenrolled devices](../protect/mtd-enable-unenrolled-devices.md). | |

## Additional information

For more information about APP for Windows devices, see the following resources: 
- [App protection policies overview](../apps/app-protection-policy.md)
- [Data protection for Windows MAM](../apps/protect-mam-windows.md) 
- [Create an MTD app protection policy for Windows](../protect/mtd-app-protection-policy.md#to-create-an-mtd-app-protection-policy-for-windows)
- [Add an app configuration policy for managed apps on Windows devices](../apps/app-configuration-policies-managed-app.md#add-an-app-configuration-policy-for-managed-apps-on-windows-devices)
- [Configure Microsoft Edge for Windows with Intune](../apps/manage-microsoft-edge-windows.md)
- [Require an app protection policy on Windows devices](/entra/identity/conditional-access/how-to-app-protection-policy-windows)
