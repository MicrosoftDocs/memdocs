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

# Add the Windows Company Portal app by using Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

To manage devices and install apps, your users can install the Company Portal app themselves from the Microsoft Store or download it from the [Microsoft Intune Company Portal for Windows](../apps/store-apps-company-portal-app.md#download-the-offline-company-portal-app). If your business needs require that you assign the Company Portal app to them, however, you can assign the Windows Company Portal app directly from Intune.

 > [!IMPORTANT]
 > If you download the Company Portal app, the option described in this article requires that you assign manual updates each time an app update is released. To deploy the Company Portal app for Autopilot provisioned Windows devices, see [Add Windows Company Portal app Autopilot devices](store-apps-company-portal-autopilot.md).

> [!NOTE]
> The Company Portal supports Configuration Manager applications. This feature allows end users to see both Configuration Manager and Intune deployed applications in the Company Portal for co-managed customers. This new version of the Company Portal will display Configuration Manager deployed apps for all co-managed customers. This support will help administrators consolidate their different end user portal experiences. For more information, see [Use the Company Portal app on co-managed devices](../../configmgr/comanage/company-portal.md).

## Download the offline Company Portal app

1. Use the Windows Package Manager command-line tool `winget.exe` to download the Windows Company Portal app with dependencies.

2. In Microsoft Intune in the portal, upload the Company Portal app as a new app. You add the application by selecting Line-of-business app as the **App type** in the **Select app type** pane. You then select the app package file (extension .AppxBundle).

8. Under **Select dependency app files** select all the dependencies you downloaded in step 1 by using shift-click, and verify that the **Added** column displays **Yes** for the architectures you need.

     > [!NOTE]
     > If the dependencies are not added, the app might not install on the specified device types.

9. Click **Ok**, enter any desired **App Information**, and click **Add**.

10. Assign the Company Portal app as a required app to your selected set of user or device groups.  

For more information about how Intune handles dependencies for Universal apps, see [Deploying an appxbundle with dependencies via Microsoft Intune MDM](/archive/blogs/configmgrdogs/deploying-an-appxbundle-with-dependencies-via-microsoft-intune-mdm).  

## Next steps

- [Assign apps to groups](apps-deploy.md)
