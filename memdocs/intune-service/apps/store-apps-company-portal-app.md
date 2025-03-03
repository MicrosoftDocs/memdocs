---
# required metadata

title: Manually add the Windows 10 Company Portal app
titleSuffix: Microsoft Intune
description: Learn how your workforce can manually add the Windows 10 Company Portal app to their PC from the Microsoft Store.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 08/27/2024
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

To manage devices and install apps, your users can install the Company Portal app themselves from the Microsoft Store or download it from the [Microsoft Intune Company Portal for Windows](../apps/store-apps-company-portal-app.md#download-the-offline-company-portal-app). If your business needs require that you assign the Company Portal app to them, however, you can assign the Company Portal app for Windows directly from Intune.

 > [!IMPORTANT]
 > To deploy the Company Portal app for Autopilot provisioned devices, see [Add Company Portal app for Autopilot devices](store-apps-company-portal-autopilot.md).

> [!NOTE]
> The Company Portal supports Configuration Manager applications. This feature allows end users to see both Configuration Manager and Intune deployed applications in the Company Portal for co-managed customers. This new version of the Company Portal will display Configuration Manager deployed apps for all co-managed customers. This support will help administrators consolidate their different end user portal experiences. For more information, see [Use the Company Portal app on co-managed devices](../../configmgr/comanage/company-portal.md).

## Download the offline Company Portal app

1. Use the [Windows Package Manager](/windows/package-manager/winget) command-line tool, also known as *Winget.exe*, to download the Company Portal app for Windows with dependencies. Files are downloaded to the Downloads folder on your device by default.  

1. In the Microsoft Intune admin center, upload the Company Portal app as a new app.
    1. Go to **Apps** > **Platforms** and select **Windows**. 
    1. Select  **Add**. 
    1. For **App type**, choose **Other** > **Line-of-business app**.  
    1. Choose **Select** to continue.  
    1. On the **App information** page, choose **Select app package file**. 
    1. In the new pane, select the **File** upload button, and then upload the app package file. The file you want to select has the app package (.appxbundle) extension.   
1. Detected dependencies appear. Under **Select dependency app files**, select all dependencies you downloaded in step 1.
   
   1. **Shift + click** to select all dependencies.
      
   1. Under the **Added** column, verify that **Yes** appears for the architectures you need.  

     > [!NOTE]
     > If you don't add the dependencies, installation could fail for the selected device types.  

1. Select **Ok**.  
1. Under **App information**, enter any information about the app.
1. Select **Add**.  
1. Assign the Company Portal app as a required app to selected users or device groups.   

For more information about how Intune handles dependencies for Universal apps, see [Deploying an appxbundle with dependencies via Microsoft Intune MDM](/archive/blogs/configmgrdogs/deploying-an-appxbundle-with-dependencies-via-microsoft-intune-mdm).  

## Next steps

- [Assign apps to groups](apps-deploy.md)
