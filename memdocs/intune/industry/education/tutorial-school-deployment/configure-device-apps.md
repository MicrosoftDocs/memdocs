---
title: Configure applications with Microsoft Intune
description: Learn how to configure applications with Microsoft Intune in preparation for device deployment.
zone_pivot_groups: platforms-windows-ios
ms.topic: tutorial
author: scottbreenmsft
ms.author: scbree
ms.manager: dougeby
ms.date: 5/2/2024
ms.service: microsoft-intune
ms.subservice: education
---

# Configure applications with Microsoft Intune

With Intune, school IT administrators have access to diverse applications to help students unlock their learning potential. This section discusses tools and resources for adding apps to Intune.

Applications can be assigned to groups:

- If you target apps to a **group of users**, the apps will be installed on any managed devices that the users sign into.
- If you target apps to a **group of devices**, the apps will be installed on those devices and available to any user who signs in.

## Add apps

✅ Add applications to your inventory

::: zone pivot="windows"

### [Intune](#tab/intune)

Intune supports the deployment several application types including desktop apps (msi, exe), Microsoft Store apps, web apps, appxbundle and MSIX.

#### Enterprise Application Management

Enterprise App Management enables you to easily discover and deploy applications and keep them up to date from the Enterprise App Catalog. The Enterprise App Catalog is a collection of prepared Microsoft and non-Microsoft applications. These apps are Win32 apps that are [prepared as Win32 apps](/mem/intune/apps/apps-win32-prepare) and hosted by Microsoft.

> [!IMPORTANT]
> Enterprise App Management is an Intune add-on as part of the Intune suite that is available for trial and purchase. For more information, see [Use Intune Suite add-on capabilities](/mem/intune/fundamentals/intune-add-ons).

For more information, see [Enterprise Application Management](/mem/intune/apps/apps-enterprise-app-management).

#### Win32 apps (MSI, exe)

The addition of desktop applications to Intune should be carried out by repackaging the apps, and defining the commands to silently install them. The process is described in the article [Add, assign, and monitor a Win32 app in Microsoft Intune][MEM-1].

#### Microsoft Store app (new)

To create Microsoft Store apps in Intune:

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), select **Apps** > **All apps** > **Add**.
1. In **Select app type** pane, select **Microsoft Store app (new)** under the **Store app** section.
1. Choose **Select** at the bottom of the page to begin creating an app from the Microsoft Store. The app creation experience has three steps:
    - App information
    - Assignments
    - Review + create
1. Select **Search the Microsoft Store app** to search for and select the app.
1. Review and change settings as required.
    > [!NOTE]
    > Most administrators choose to deploy store apps in the **system** context on education devices for the fastest installation to all users of a device.
1. Select **Save**.

For more information, see [Add Microsoft Store apps](/mem/intune/apps/store-apps-microsoft).

#### Web apps

To create web applications in Intune:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Select **Apps** > **All apps** > **Add**.
1. In the **Select app type** pane, under the **Other** types, select **Windows web link**.
1. Click **Select**. The **Add app** steps are displayed.
1. Provide a URL for the web app, a name, and optionally an icon and description.
1. Select **Save**

For more information, see [Add web apps](/mem/intune/apps/web-app).

### [Intune For Education](#tab/intune-for-education)

Intune for Education supports the deployment of two types of Windows applications: **web apps** and **desktop apps**.

:::image type="content" source="./images/intune-education-apps.png" alt-text="Intune for Education - Apps" lightbox="./images/intune-education-apps.png" border="true":::

#### Desktop apps

Intune for Education supports:

- **Single file MSI** - Single file MSI files can be uploaded directly to Intune for Education. For more information, see [Add desktop apps in Intune for Education](/intune-education/add-desktop-apps-edu).
- **Win32 apps** - The addition of desktop applications to Intune should be carried out by repackaging the apps, and defining the commands to silently install them. The process is described in the article [Add, assign, and monitor a Win32 app in Microsoft Intune][MEM-1].

> [!NOTE]
> For consistency, it is recommended that you choose to use only one of the desktop app installation methods. For example, if you have any applications that require the use of the Win32 app capability, then package and deploy all apps using the Win32 apps capability and don't use the single file MSI (LOB) option.

#### Web apps

To create web applications in Intune for Education:

1. Sign in to the [Intune for Education portal](https://intuneeducation.portal.azure.com).
1. Select **Apps**.
1. Select **New app** > **New web app**.
1. Provide a URL for the web app, app name, and optionally an icon and description.
1. Select **Save**.

For more information, see [Add web apps][INT-2].

#### Microsoft Store app (new)

To create Microsoft Store apps in Intune for Education:

1. Sign in to the [Intune for Education portal](https://intuneeducation.portal.azure.com).
1. Select **Apps**.
1. Select **New app** > **New Microsoft Store app (new)**.
1. Search for and select the app.
1. Review and change settings as required.
    > [!NOTE]
    > Most customers choose to deploy store apps in the **system** context on education devices for the fastest installation to all users of a device.
1. Select **Save**.

For more information, see [Add Microsoft Store apps](/mem/intune/apps/store-apps-microsoft).

::: zone-end

::: zone pivot="ios"

> [!TIP]
> The best user experience for receiving apps on a device is for apps to be assigned using Apple School Manager and the Volume Purchase Program (VPP) with device licensing. When device-licensed VPP apps are assigned to devices or users, the app can be installed without user interaction. For iOS apps without VPP, the user is prompted to sign in to the App Store with an Apple ID.

### [Intune](#tab/intune)

#### Volume purchase program (VPP) apps

To add apps from VPP, set up a connection to Apple School Manager and add your apps in Apple School Manager.

For more information, see [Configure VPP tokens](/mem/intune/apps/vpp-apps-ios).

#### iOS App

To add apps to iOS devices without using VPP in Intune for Education:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Select **Apps** > **All apps** > **Add**.
1. In the **Select app type** pane, select **iOS store app**.
1. Click **Select**. The **Add app** steps are displayed.
1. Select **Search the App Store**.
1. In the **Search the App Store** pane, select the App Store country/region locale.
1. In the **Search** box, type the name (or part of the name) of the app. Intune searches the store and returns a list of relevant results.
1. In the results list, select the app you want, and then select **Select**.
1. Follow the steps remaining steps and select **Create**.

> [!NOTE]
> Apps installed with this method will require the user of the device to sign in using an Apple ID to install the application. To avoid prompting the user for an Apple ID, use VPP apps.

#### Web apps

To create web applications:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Select **Apps** > **All apps** > **Add**.
1. In the **Select app type** pane, under the **Other** types, select **iOS/iPadOS web clip**.
1. Click **Select**. The **Add app** steps are displayed.
1. Follow the steps remaining steps and select **Create**.

For more information, see [Add web apps](/mem/intune/apps/web-app).

### [Intune For Education](#tab/intune-for-education)

#### Volume purchase program (VPP) apps

To add apps from VPP, set up a connection to Apple School Manager and add your apps in Apple School Manager.

For more information, see [Configure VPP tokens](/intune-education/setup-ios-device-management#configure-vpp-tokens).

#### iOS App

To add apps to iOS devices without using VPP in Intune:

1. Sign in to the [Intune for Education portal](https://intuneeducation.portal.azure.com).
1. Select **Apps**.
1. Select **New app** > **New iOS app**.
1. Search the app store by entering the app name and selecting the country.
1. Select the app in the list.
1. Click **Add to Intune**.

> [!NOTE]
> Apps installed with this method will require the user of the device to sign in using an Apple ID to install the application. To avoid prompting the user for an Apple ID, use VPP apps.

#### Web apps

To create web applications in Intune for Education:

1. Sign in to the [Intune for Education portal](https://intuneeducation.portal.azure.com).
1. Select **Apps**.
1. Select **New app** > **New web app**.
1. Provide a URL for the web app, a name, and optionally an icon and description.
1. Select **Save**.

For more information, see [Add web apps][INT-2].

---

### Other apps

Intune also supports deploying **[iOS/iPadOS LOB apps](/mem/intune/apps/lob-apps-ios)** from the Intune admin center. A line-of-business (LOB) app is an app that you add to Intune from an IPA app installation file.

::: zone-end

## Assign apps

✅ Assign apps from your inventory to groups

::: zone pivot="windows"

### [Intune](#tab/intune)

To assign applications to a group of users or devices:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Select **Apps** > **All apps**.
1. In the **Apps** pane, select the app you want to assign.
1. In the **Manage** section of the menu, select **Properties**.
1. Next to assignments, select **Edit**.
1. Select one or more groups to for the app assignment and select **Select**.
1. Review your selections and select **Save**.

### [Intune For Education](#tab/intune-for-education)

To assign applications to a group of users or devices:

1. Sign in to the [Intune for Education portal](https://intuneeducation.portal.azure.com).
1. Select **Groups** > Pick a group to manage.
1. Select **Apps**.
1. Select either **Web apps** or **Windows apps**.
1. Select the apps you want to assign to the group > **Save**.

::: zone-end

::: zone pivot="ios"

### [Intune](#tab/intune)

To assign applications to a group of users or devices:

1. 1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
1. Select **Apps** > **All apps**.
1. In the **Apps** pane, select the app you want to assign.
1. In the **Manage** section of the menu, select **Properties**.
1. Next to assignments, select **Edit**.
1. Select one or more groups to for the app assignment and select **Select**.
1. Review your selections and select **Save**.

### [Intune For Education](#tab/intune-for-education)

1. Sign in to the [Intune for Education portal](https://intuneeducation.portal.azure.com).
1. Select **Groups** > Pick a group to manage.
1. Select **Apps**.
1. Select either **Web apps** or **iOS apps**.
1. Select the apps you want to assign to the group > **Save**.

::: zone-end

## Next steps

With the applications configured, you can now deploy students' and teachers' devices.

> [!div class="nextstepaction"]
> [Next: Deploy devices >](enroll-overview.md)

<!-- Reference links in article -->

[EDU-1]: /education/windows/tutorial-deploy-apps-winse

[MEM-1]: /mem/intune/apps/apps-win32-add

[INT-1]: /intune-education/express-configuration-intune-edu
[INT-2]: /intune-education/add-web-apps-edu