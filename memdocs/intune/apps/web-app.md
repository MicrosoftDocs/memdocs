---
# required metadata

title: Add web apps to Microsoft Intune
titleSuffix: 
description: Learn about adding web apps (client-server applications) to Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 12/16/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.technology:
ms.assetid: 5f08752f-0e87-4ad9-a34c-4991b3150775

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: manchen
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
---

# Add web apps to Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune supports a variety of app types, including web apps. A web app is a client-server application. The server provides the web app, which includes the UI, content, and functionality. Additionally, modern web-hosting platforms commonly offer security, load balancing, and other benefits. A web app is separately maintained on the web. You use Microsoft Intune to point to this app type. You also assign the groups of users that can access this app. 

Before you can manage and assign an app for your users, add the app to Intune. 

Intune creates a shortcut to the web app on the user's device. For iOS/iPadOS devices, a shortcut to the web app is added to the home screen. For Android Device Admin devices, a shortcut to the web app is added to the Intune company portal widget and the widget needs to be pinned manually by the user. For Windows devices, a shortcut to the web app is placed on the Start Menu.

> [!Note]
> A browser must be installed on the user's device to launch web apps. 
> 
> For Android Enterprise devices, see [Managed Google Play web links](apps-add-android-for-work.md#managed-google-play-web-links).
> 
> For iOS devices, new web clips (pinned web apps) will open in Microsoft Edge instead of the Intune Managed Browser when required to open in a protected browser. For older iOS web clips, you must retarget these web clips to ensure they open in Microsoft Edge rather then the Managed Browser.
>
> For legacy device admin Android devices, web links pinned through the Company Portal widget can only open with the Intune Managed Browser if users' Company Portal version is older than 5.0.4737.0. 

## Add a web app to Intune
To add an app to Intune as a shortcut to an app on the web, do the following:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Apps** > **All apps** > **Add**.
3. In the **Select app type** pane, under the available **Other** types, select **Web link**.
4. Click **Select**. The **Add app** steps are displayed.
5. On the **App information** page, add the following information:
    - **Name**:  Enter the name of the app as it is to be displayed in the company portal. 

        > [!NOTE]
        > If you change the name of the app through Intune after you have deployed and installed the app, the app will no longer be able to be targeted using commands.

    - **Description**: Enter a description for the app. This description is displayed to users in the company portal.
    - **Publisher**: Enter the name of the publisher of this app.
    - **App URL**: Enter the URL of the website that hosts the app that you want to assign.
    - **Category**: Optionally, select one or more of the built-in app categories, or a category that you created. Doing so makes it easier for users to find the app when they browse the company portal.
    - **Show this as a featured app in the Company Portal**: Select this option to display the app suite prominently on the main page of the company portal when users browse for apps.
    - **Require a managed browser to open this link**: Select this option to assign to your users a link to a website or web app that they can open in the Intune managed browser. This browser must be installed on their device.
    - **Logo**: Upload an icon that will be associated with the app. This icon is displayed with the app when users browse the company portal.
6. Click **Next** to display the **Scope tags** page.
7. Click **Select scope tags** to optionally add scope tags for the app. For more information, see [Use role-based access control (RBAC) and scope tags for distributed IT](../fundamentals/scope-tags.md).
8. Click **Next** to display the **Assignments** page.
9. Select the group assignments for the app. For more information, see [Add groups to organize users and devices](../fundamentals/groups-add.md). 
10. Click **Next** to display the **Review + create** page. Review the values and settings you entered for the app.
11. When you are done, click **Create** to add the app to Intune.

    The **Overview** blade of the app you've created is displayed.

End-users can launch web apps directly from the Windows Company Portal app by selecting the web app and then choosing the option **Open in browser**. The published web URL is opened directly in the web browser. 

## Next steps

The app that you've created is displayed in the apps list, where you can assign it to the groups that you select. For help, see [Assign apps to groups](apps-deploy.md). 
