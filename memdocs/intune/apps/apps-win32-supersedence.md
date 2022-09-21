---
title: Add Win32 app supersedence
titleSuffix: Microsoft Intune
description: Learn how to use Win32 app supersedence with Microsoft Intune. 
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/25/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.technology:
ms.assetid: 

ms.reviewer: manchen
ms.suite: ems
search.appverid: MET150
ms.custom: 
ms.collection: M365-identity-device-management
---

# Add Win32 app supersedence

> [!NOTE]
> Win32 app supersedence is in public preview.

After you've [added a Win32 app to Intune](apps-win32-add.md), you can use Intune to create one or more supersedence relationships between apps. In general, supersedence is where you update or replace something. In Intune, supersedence enables you to update and replace existing Win32 apps with newer versions of the same app or an entirely different Win32 app. This topic provides an overview of the supersedence feature.

> [!IMPORTANT]
> Supersedence, which enables you to update and replace a version of a Win32 app, does not currently allow you to interchange the Win32 app with an app dependency. For more information about app dependencies, see [Dependencies](../apps/apps-win32-add.md#step-5-dependencies).

Supersedence relationships can be created when adding or modifying a Win32 app within Intune. The **Supersedence** steps allow you to specify any supersedence relationships related to the Win32 app.

   ![Screenshot of Win32 app supersedence step](./media/apps-win32-supersedence/apps-win32-supersedence-01.png)

## Prerequisites

App supersedence can only be applied to Win32 apps. For more information, see [Add a Win32 app](apps-win32-add.md) to Intune.

A Microsoft Endpoint Manager permission will be required to create and edit Win32 app supersedence and dependency relationships with other apps. The permission is available under the **Mobile apps** category by selecting **Relate**. Starting in the **2202** service release, MEM admins will need this permission to add supersedence and dependency apps when creating or editing a Win32 app in Microsoft Endpoint Manager admin center. To find this permission in [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431), choose **Tenant administration** > **Roles** > **All roles** > **Create**.

This Win32 app supersedence permission has been added to the following built-in roles:
- Application Manager
- School administrator

## Create a Supersedence relationship in Intune

The following steps help you create a supersedence relationship between apps:

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All apps**, and then select a Win32 app from the list. If you haven't added a Win32 app, you can follow the steps to [add a Win32 app to Intune](apps-win32-add.md).
3. After you have selected the existing Win32 app, click **Properties**. 
3. In the **Supersedence** section, click **Edit** > **Add** to choose apps that should be superseded.

    > [!NOTE]
    > There can be a maximum of 10 nodes in a supersedence relationship in Intune.

4. Find and click the apps to apply the supersedence relationship in the **Add Apps** pane. Click **Select** to add the apps to your supersedence list.
5. In the list of superseded apps, modify the **Uninstall previous version** option for each selected app to specify whether an uninstall command will be sent by Intune to each selected app. If the installer of the current app updates the selected app automatically, then it is not necessary to send an uninstall command. When replacing a selected app with a different app, it may be necessary to turn on the **Uninstall previous version** option to remove and replace the older app.
6. Once this step is finalized, click **Review + save** > **Save**.

    > [!IMPORTANT]
    > Superseding apps do not get automatic targeting. Each app must have explicit targeting to take effect. Superseding apps that are not targeted will be ignored by the agent. If the superseding app is targeted to a device with a superseded app, then the supersedence will take place regardless of whether the superseded app has targeting or not. For more information on Supersedence behavior, please refer to the matrix below. This behavior is in direct contrast to dependencies, which does not require targeting. Additionally, only apps that are targeted will show install statuses in Microsoft Endpoint Manager admin center.

## Supersedence behavior

A *superseding app* is an app that updates or replaces other apps. A *superseded app* is an app that is being updated or replaced. Supersedence behavior can be illustrated based on the following scenarios. 

| Scenarios | Targeting for required intent | Targeting for available intent |
|-|-|-|
| **Scenario   1:**<br> The superseded app exists on the device and **Uninstall previous version** is set to **Yes**. | The superseded app will be uninstalled, and the superseding app will be installed on the device.<p> **NOTE:** Even if the superseded app is not targeted, it will be uninstalled. | Only superseding apps will be shown in the company portal and can be installed. |
| **Scenario   2:**<br>The superseded app exists on the device and **Uninstall previous version** is set to **No**. | The superseding app will be installed on the device. Whether the superseded app will be uninstalled or not is dependent on the superseding app’s installer. | Only superseding apps will be shown in the company portal and can be installed. |
| **Scenario   3:**<br>The superseded app does not exist on the device. | The superseding app will be   installed. | The new app will appear in the   Company Portal. |

### Understand app update versus app replacement within supersedence

Given that an app could have multiple superseded apps, it is possible for an app to update a set of apps while replacing another set of apps at the same time. 

> [!NOTE]
> End-users will not be able to check whether a specific Win32 app supersedence operation is an update or replacement in the Company Portal. In addition, when multiple apps supersede an app with available targeting in the Company Portal, the superseded app's details page will navigate to the app page of the first superseding app that was set up. For example, if app A is superseded by app B and C, and app B is superseded by app A first, then app A's detail page in the Company Portal will navigate to App B.

Understanding how supersedence is applied when updating an app versus replacing an app can be illustrated based on the following scenario.

| Customer   scenario | Description | Expected behavior | Additional information |
|-|-|-|-|
| App   update | IT admin wants to update an app   with a newer version of the same app. | The installer of the newer   version of the app (the superseding app) will automatically update the older   version of the app to the newer version. | Since the installer will   complete the updating, it is not necessary to send down an uninstall command   to the older version. Hence, the Uninstall previous version is toggled off. |
| App   replacement | IT admin wants to replace an app   with an entirely different app. | The superseded app will be   uninstalled and the superseding app will be installed. Both install and   uninstall will be based on IT Pro’s defined install/uninstall command line. | Since the two apps are different,   the admin can turn the Uninstall previous version toggle on to uninstall the   older app from the device. |

### Understand in-place app update versus supersedence app update

In the following scenarios, you should review app detection rules after performing either type of the following updates.

| Update   type | Update description and details |
|-|-|
| In-place   app update | <ul><li>With an   in-place app update, admin can only swap the app content, update the   metadata, and change the detection and install commands.</li>      <li>Admin cannot change any of the fields that are not stored on the   app with an in-place app update.  For   example, the admin cannot modify targeting at the same time as an   update.</li>      <li>Admin can only perform the in-place app update one app at a   time.</li></ul> |
| Supersedence   app update | <ul><li>Admin can   update an app in its entirety with a new set of   configurations.</li>      <li>Admin can elect to send down an uninstall command to uninstall   previous app versions.</li>      <li>Admin can update devices containing multiple app versions to the   newest app version with one Supersedence configuration. The admin also   maintains access to older version of the app.</li></ul> |

## Basic Supersedence Examples

For the purposes of this document, we assume that all apps are targeted (either device or user targeting) and are applicable. 

### Legend for supersedence example scenarios

| Legend | Definition |
|-|-|
| ![Legend supersedence example scenario 1](./media/apps-win32-supersedence/apps-win32-supersedence-02a.png)  | A is superseded by B via app update. |
| ![Legend supersedence example scenario 2](./media/apps-win32-supersedence/apps-win32-supersedence-02b.png)  | A is superseded by B via app   replacement. |
| ![Legend supersedence example scenario 3](./media/apps-win32-supersedence/apps-win32-supersedence-02c.png)  | A is present on the device,   fully installed, and   passes the defined detection rules. |
| ![Legend supersedence example scenario 4](./media/apps-win32-supersedence/apps-win32-supersedence-02d.png)  | A is not present on the device. |

### Case and resolution supersedence examples

| Case | Resolution | Notes |
|-|-|-|
| ![Case supersedence example scenario 1](./media/apps-win32-supersedence/apps-win32-supersedence-03a.png) | **Scenario:** Neither app is   detected  on the device. A is superseded by B via app   update.<p>**Result:** Install B. | App   update means that admin chose not to uninstall the superseded app during the   configuration stage. See above in the Supersedence Step   in App Deployment. |
| ![Case supersedence example scenario 2](./media/apps-win32-supersedence/apps-win32-supersedence-03b.png) | **Scenario:** Only A is detected   on the device. A is superseded by B via app update.<p>**Result:**   Install B. | Since admin   chose not to uninstall the previous version during configuration, A is not   explicitly uninstalled by Intune. A may be uninstalled based on the behavior   of B’s installer. |
| ![Case supersedence example scenario 3](./media/apps-win32-supersedence/apps-win32-supersedence-03c.png) | **Scenario:** Only B is detected   on the device. A is superseded by B via app update.<p>**Result:**   Nothing. | Since B is   already detected on the device, no action is taken. |
| ![Case supersedence example scenario 4](./media/apps-win32-supersedence/apps-win32-supersedence-03d.png) | **Scenario:** Both apps are   detected on the device. A is superseded by B via app   update.<p>**Result:** Nothing. | Since B is   already detected on the device, no action is taken. Admin chose not to   uninstall the previous version when configuring, hence A is not uninstalled. |
| ![Case supersedence example scenario 5](./media/apps-win32-supersedence/apps-win32-supersedence-03e.png) | **Scenario:** Neither apps are   detected on the device. A is superseded by B via app   replacement.<p>**Result:** Install B. | App replacement   means that admin chose to uninstall the superseded app during the   configuration stage. See above in the Supersedence Step   in App Deployment. |
| ![Case supersedence example scenario 6](./media/apps-win32-supersedence/apps-win32-supersedence-03f.png) | **Scenario:** Only A is detected   on the device. A is superseded by B via app replacement.<p>**Result:**   Uninstall A, then install B. | A will be   uninstalled and once the agent detects that A is no longer present on the   device, it will install B. If the detection continues to detect A as present,   then the agent won’t install B. Whether B is installed on the device is   predicated on whether A is detected on the device. |
| ![Case supersedence example scenario 7](./media/apps-win32-supersedence/apps-win32-supersedence-03g.png) | **Scenario:** Only B is detected   on the device. A is superseded by B via app replacement.<p>**Result:**   None | No actions are   taken because B is already installed and A doesn’t exist on the device. |
| ![Case supersedence example scenario 8](./media/apps-win32-supersedence/apps-win32-supersedence-03h.png) | **Scenario:** Both apps are   detected on the device. A is superseded by B via app   replacement.<p>**Result:** Uninstall A. | A is   uninstalled as part of the app replacement process.  Detection of a replaced app after the replacing app is already   installed will incur a remediation enforcement. |

## Behavior for Chained Supersedence Scenarios

Supersedence chains occur when multiple apps are part of a supersedence relationship. For example, an IT admin could configure App A to be superseded by App B, and then later configure App B to be superseded by App C. In this scenario, a supersedence chain is created between App A, B, and C (as shown in the first case below). Supersedence chains can have a maximum of 10 related nodes in the chain. For more information about this maximum, see [Supersedence Limitations](#supersedence-limitations).

>The behavior for supersedence chains can summarized as the following:
- All apps in a supersedence chain will be superseded by the superseding app of the chain. In the example given above, the superseding app of the chain is App C.

To better understand the behavior of a supersedence chain, the following table provides a list of cases and resolutions. When reviewing these supersedence chains, assume all apps are targeted and are applicable to the device.

| Case | Resolution | Notes |
|-|-|-|
| ![Case supersedence scenario 1](./media/apps-win32-supersedence/apps-win32-supersedence-04a.png) | **Scenario:**   None of the apps exist on the device. The relationship between apps is one of   app update.<p>**Result:** Install C. | Since   none of the apps exist on the device, we install the superseding app: App C.   The superseding app refers to the app that supersedes all other apps in the   chain. |
| ![Case supersedence scenario 2](./media/apps-win32-supersedence/apps-win32-supersedence-04b.png) | **Scenario:**   Only Apps A and C exist on the device. The relationship between apps is one   of app update.<p>**Result:** None. | Since App C   already exists on the device and this is an app update scenario, App A is not   uninstalled. |
| ![Case supersedence scenario 3](./media/apps-win32-supersedence/apps-win32-supersedence-04c.png) | **Scenario:**   Only App A exists on the device. The relationship between apps is one of app   update.<p>**Result:** Install C. | Simply install   App C. App A is not uninstalled because it is an app update scenario.  C’s installer may or may not   have behavior to remove A, where "remove" means A is no longer detected via   its detection rules (usually due to version detection). |
| ![Case supersedence scenario 4](./media/apps-win32-supersedence/apps-win32-supersedence-04d.png) | **Scenario:** Only App C exists   on the device. The relationship between apps is one of app   update.<p>**Result:** None. | Since App C,   the superseding app, already exists on the device, and this is an app update   scenario, no action is taken. |
| ![Case supersedence scenario 5](./media/apps-win32-supersedence/apps-win32-supersedence-04e.png) | **Scenario:** None of the apps   exist on the device. The relationship between apps is one of app   replacement.<p>**Result:** Install C. | Since none of   the apps exist on the device, simply install the superseding app, App C. |
| ![Case supersedence scenario 6](./media/apps-win32-supersedence/apps-win32-supersedence-04f.png) | **Scenario:** Apps A and C exist   on the device. The relationship between apps is one of app   replacement.<p>**Result:** Uninstall A. | Since App C   exists on the device and this is an app replacement scenario, simply   uninstall App A. |
| ![Case supersedence scenario 7](./media/apps-win32-supersedence/apps-win32-supersedence-04g.png) | **Scenario:** Only App A exists   on the device. The relationship between apps is one of app   replacement.<p>**Result:** Uninstall A, then install C. | Since this is   an app replacement scenario, App A is uninstalled and App C, the superseding   app, is installed. |
| ![Case supersedence scenario 8](./media/apps-win32-supersedence/apps-win32-supersedence-04h.png) | **Scenario:** Only App C exists   on the device. The relationship between apps is one of app   replacement.<p>**Result:** None. | Since the   superseding app, App C, exists on the device and none of the other superseded   apps exist, no action is taken. |

## Supersedence Limitations

There can only be a maximum of 10 nodes in a single Supersedence graph. The nodes include the superseding app, the superseded apps, and all subsequent related apps. 
In the following Supersedence diagram, there are five nodes in total. Hence, five more nodes could be created until the max node count is reached.

![Supersedence maximum node count example](./media/apps-win32-supersedence/apps-win32-supersedence-05.png)

Additional supersedence limitations:
- Azure Virtual Desktop multi-session only supports supersedence relationships with system-context (device-based) apps.
- The Enrollment Status Page (ESP) is not supported with the supersedence public preview. ESP displays provisioning progress after a new device is enrolled, as well as when new users sign into the device. For the supersedence public preview, if an app has a supersedence relationship, it will not be enforced during ESP even if it is included as a selected app in an ESP policy. Additionally, apps that are involved in supersedence relationships will not be sent to the client device during ESP. However, the apps will be sent to the device after ESP completes, and the supersedence relationship will be respected.
- Only apps that are targeted will show install statuses in Microsoft Endpoint Manager admin center.

## Next steps

- [Troubleshoot Win32 app issues](apps-win32-troubleshoot.md)
- [Monitor app information and assignments with Microsoft Intune](apps-monitor.md)
- [Win32 app management in Microsoft Intune](apps-win32-app-management.md)
