---
# required metadata

title: Manually add the Windows 10 Company Portal app
titleSuffix: Microsoft Intune
description: Learn how your workforce can manually add the Windows 10 Company Portal app to their PC from the Microsoft Store.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/27/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.assetid: bfe1a2d3-f611-4dbb-adef-c0dff4d7b810

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: bryanke
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- Windows
- highpri
---

# Add the Windows 10 Company Portal app by using Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

To manage devices and install apps, your users can install the Company Portal app themselves from the Microsoft Store or download it from the [Microsoft Intune Company Portal for Windows](../apps/store-apps-company-portal-app.md#download-the-offline-company-portal-app). If your business needs require that you assign the Company Portal app to them, however, you can assign the Windows 10 Company Portal app directly from Intune.

 > [!IMPORTANT]
 > If you download the Company Portal app, the option described in this article requires that you assign manual updates each time an app update is released. To deploy the Company Portal app for Windows 10 Autopilot provisioned devices, see [Add Windows 10 Company Portal app Autopilot devices](store-apps-company-portal-autopilot.md).

> [!NOTE]
> The Company Portal supports Configuration Manager applications. This feature allows end users to see both Configuration Manager and Intune deployed applications in the Company Portal for co-managed customers. This new version of the Company Portal will display Configuration Manager deployed apps for all co-managed customers. This support will help administrators consolidate their different end user portal experiences. For more information, see [Use the Company Portal app on co-managed devices](../../configmgr/comanage/company-portal.md).

## Download the offline Company Portal app

1. Search for and then select the **Company Portal** app.
2. Set the **License type** to **Offline**. Offline apps are managed by Intune, whereas online apps are managed by the store. Use offline apps when you need to install and maintain a specific app version.
3. Select **Get the app** to acquire and add the offline Company Portal app to your inventory. If you already have the offline app, you can select the **Manage** option.
4. For **Platform**, select **Windows 10 all devices**, and then select the appropriate **Minimum version**, **Architecture**, and **Download app metadata** values.
5. Select **Download** to save the file to your local machine.

    ![Windows 10 devices, where architecture equals X86, is selected](./media/app-sideload-windows/Win10CP-all-devices.png)

6. Download all the packages under "Required Frameworks" by selecting **Download**.  

    This action must be completed for x86, x64, and ARM architectures:<br> 
    *There are 9 Required Framework Packages when selecting 1507 as the minimum OS Version, 12 packages when selecting 1511, and 15 packages when selecting 1607.*

7. In Microsoft Intune in the portal, upload the Company Portal app as a new app. You add the application by selecting Line-of-business app as the **App type** in the **Select app type** pane. You then select the app package file (extension .AppxBundle).

8. Under **Select dependency app files** select all the dependencies you downloaded in step 7 by using shift-click, and verify that the **Added** column displays **Yes** for the architectures you need.

     > [!NOTE]
     > If the dependencies are not added, the app might not install on the specified device types.

9. Click **Ok**, enter any desired **App Information**, and click **Add**.

10. Assign the Company Portal app as a required app to your selected set of user or device groups.  

For more information about how Intune handles dependencies for Universal apps, see [Deploying an appxbundle with dependencies via Microsoft Intune MDM](/archive/blogs/configmgrdogs/deploying-an-appxbundle-with-dependencies-via-microsoft-intune-mdm).  

## Frequently asked questions

 > [!NOTE]
 > Microsoft Intune will be ending support on October 21, 2022 for devices running Windows 8.1. Intune will no longer support Windows 8.1 sideloading.

### How do I update the Company Portal app on my users' devices if they have already installed the older apps from the store?

If your users have already installed the Windows 8.1 Company Portal apps from the Microsoft Store, their apps should be automatically updated to the latest version with no action required from you or your users. If the update does not happen, ask your users to confirm that they have enabled auto-updates for Store apps on their devices.

### How do I upgrade my sideloaded Windows 8.1 Company Portal app to the Windows 10 Company Portal app?

Our recommended migration path is to delete the assignment for the Windows 8.1 Company Portal app by setting the assignment action to **Uninstall**. After you select this setting, you can assign the Windows 10 Company Portal app by using any of the previously discussed options.  

If you need to sideload the app and you assigned the Windows 8.1 Company Portal without signing it with the Symantec Certificate, complete the upgrade by completing the steps in the preceding sections of this article.

If you need to sideload the app and you signed and assigned the Windows 8.1 Company Portal app with the Symantec code-signing certificate, follow the steps in the next section.

## Next steps

- [Assign apps to groups](apps-deploy.md)
