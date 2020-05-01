---
# required metadata

title: Manually add the Windows 10 Company Portal app
titleSuffix: Microsoft Intune
description: Learn how your workforce can manually add the Windows 10 Company Portal app to their PC from the Microsoft Store.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/21/2020
ms.topic: conceptual
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology:
ms.assetid: bfe1a2d3-f611-4dbb-adef-c0dff4d7b810

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: mghadial
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Add the Windows 10 Company Portal app by using Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

To manage devices and install apps, your users can install the Company Portal app themselves from the Microsoft Store. If your business needs require that you assign the Company Portal app to them, however, you can assign the Windows 10 Company Portal app directly from Intune. You can do so even if you haven't integrated Intune with the Microsoft Store for Business.

 > [!IMPORTANT]
 > If you download the Company Portal app, the option described in this article requires that you assign manual updates each time an app update is released. To deploy the Company Portal app for Windows 10 Autopilot provisioned devices, see [Add Windows 10 Company Portal app Autopilot devices](store-apps-company-portal-autopilot.md).

## Configure settings to show offline apps
1. Sign in to the [Microsoft Store for Business](https://www.microsoft.com/business-store) with your admin account.
2. Select the **Manage** tab near the top of the window.
3. In the left pane, select **Settings**.
4. Under **Shopping experience**, set **Show offline apps** to **On**.  
    The offline licensed apps are displayed.

## Download the offline Company Portal app
1. Search for and then select the **Company Portal** app.
2. Set the **License type** to **Offline**.
3. Select **Get the app** to acquire and add the offline Company Portal app to your inventory.
4. On the **Company portal** app page, select **Manage**.
5. For **Platform**, select **Windows 10 all devices**, and then select the appropriate **Minimum version**, **Architecture**, and **Download app metadata** values. 
6. Select **Download** under **Package details** to save the file to your local machine.

    ![Windows 10 devices, where architecture equals X86, is selected](./media/app-sideload-windows/Win10CP-all-devices.png)

7. Download all the packages under "Required Frameworks" by selecting **Download**.  

    This action must be completed for x86, x64, and ARM architectures:<br> 
    *There are 9 Required Framework Packages when selecting 1507 as the minimum OS Version, 12 packages when selecting 1511, and 15 packages when selecting 1607.*

8. In Microsoft Intune in the Azure portal, upload the Company Portal app as a new app. You add the application by selecting Line-of-business app as the **App type** in the **Select app type** pane. You then select the app package file (extension .AppxBundle).

9. Under **Select dependency app files** select all the dependencies you downloaded in step 7 by using shift-click, and verify that the **Added** column displays **Yes** for the architectures you need.

     > [!NOTE]
     > If the dependencies are not added, the app might not install on the specified device types.

10. Click **Ok**, enter any desired **App Information**, and click **Add**.

11. Assign the Company Portal app as a required app to your selected set of user or device groups.  

For more information about how Intune handles dependencies for Universal apps, see [Deploying an appxbundle with dependencies via Microsoft Intune MDM](https://blogs.technet.microsoft.com/configmgrdogs/2016/11/30/deploying-an-appxbundle-with-dependencies-via-microsoft-intune-mdm/).  

## Frequently asked questions 
### How do I update the Company Portal app on my users' devices if they have already installed the older apps from the store?
If your users have already installed the Windows 8.1 or Windows Phone 8.1 Company Portal apps from the Microsoft Store, their apps should be automatically updated to the latest version with no action required from you or your users. If the update does not happen, ask your users to confirm that they have enabled auto-updates for Store apps on their devices.   

### How do I upgrade my sideloaded Windows 8.1 Company Portal app to the Windows 10 Company Portal app?
Our recommended migration path is to delete the assignment for the Windows 8.1 Company Portal app by setting the assignment action to **Uninstall**. After you select this setting, you can assign the Windows 10 Company Portal app by using any of the previously discussed options.  

If you need to sideload the app and you assigned the Windows 8.1 Company Portal without signing it with the Symantec Certificate, complete the upgrade by completing the steps in the preceding sections of this article.

If you need to sideload the app and you signed and assigned the Windows 8.1 Company Portal app with the Symantec code-signing certificate, follow the steps in the next section.

### How do I upgrade my signed and sideloaded Windows Phone 8.1 Company Portal app or Windows 8.1 Company Portal app to the Windows 10 Company Portal app?
Our recommended migration path is to delete the existing assignment for the Windows Phone 8.1 Company Portal app or the Windows 8.1 Company Portal app by setting the assignment action to **Uninstall**. After you select this setting, you can assign the Windows 10 Company Portal app normally.  

Otherwise, the Windows 10 Company Portal app must be appropriately updated and signed to ensure that the upgrade path is respected.  

If you sign and assign the Windows 10 Company Portal app in this way, you will need to repeat this process for each new app update when it is available in the store. The app is not automatically updated when the store is updated.  

Here's how you sign and assign the app in this way:

1. Download the [Microsoft Intune Windows 10 Company Portal App Signing Script](https://aka.ms/win10cpscript).  
    This script requires the Windows SDK for Windows 10 to be installed on the host computer. [Download the Windows SDK for Windows 10](https://go.microsoft.com/fwlink/?LinkId=619296).
2. Download the Windows 10 Company Portal app from the Microsoft Store for Business, as discussed previously.  
3. To sign the Windows 10 Company Portal app, run the script with the input parameters detailed in the script header, as shown in the following table.  
    Dependencies do not need to be passed into the script. They are required only when the app is being uploaded to the Intune Admin Console.

| Parameter |  Description  |
|---|---|
| InputWin10AppxBundle  |  The path to the source appxbundle file. |
| OutputWin10AppxBundle | The output path for the signed appxbundle file. 
| Win81Appx  | The path to the Windows 8.1 or Windows Phone 8.1 Company Portal (.APPX) file. |
| PfxFilePath  |  The path to the Symantec Enterprise Mobile Code Signing Certificate (.PFX) file.  |
| PfxPassword  | The password of the Symantec Enterprise Mobile Code Signing Certificate. |
| PublisherId | The Publisher ID of the enterprise. If it is absent, the Subject field of the Symantec Enterprise Mobile Code Signing Certificate is used. |
| SdkPath | The path to the root folder of the Windows SDK for Windows 10. This argument is optional and defaults to ${env:ProgramFiles(x86)}\Windows Kits\10.  |

When the script has finished running, it outputs the signed version of the Windows 10 Company Portal app. You can then assign the signed version of the app as a line-of-business (LOB) app via Intune, which upgrades the currently assigned versions to this new app.  

## Next steps

- [Assign apps to groups](apps-deploy.md)

