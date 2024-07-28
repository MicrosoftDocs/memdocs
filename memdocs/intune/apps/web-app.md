---
# required metadata

title: Add web apps to Microsoft Intune
titleSuffix: 
description: Learn about adding web apps (client-server applications) to Microsoft Intune.
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 05/10/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: medium
ms.assetid: 5f08752f-0e87-4ad9-a34c-4991b3150775

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
- FocusArea_Apps_Web
---

# Add web apps to Microsoft Intune

[!INCLUDE [azure_portal](../includes/azure_portal.md)]

Intune supports a variety of app types, including web apps. A web app is a client-server application. The server provides the web app, which includes the UI, content, and functionality. Additionally, modern web-hosting platforms commonly offer security, load balancing, and other benefits. A web app is separately maintained on the web. You use Microsoft Intune to point to this app type. You also assign the groups of users that can access this app. 

Before you can manage and assign an app for your users, add the app to Intune. 

Intune creates a shortcut to the web app on the user's device. For iOS/iPadOS devices, a shortcut to the web app is added to the home screen. For macOS devices, end users can pin web apps to the dock on their macOS device. For Android Device Admin devices, a shortcut to the web app is added to the Intune company portal widget and the widget needs to be pinned manually by the user. For Windows devices, a shortcut to the web app is placed on the Start Menu.

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
3. In the **Select app type** pane, under the **Other** types, select **Web link**. Other options include **iOS/iPadOS web clip**, **macOS web clip**, and **Windows web link**.
4. Click **Select**. The **Add app** steps are displayed.
1. On the **App information** page, add the following information:
    - **Name**:  Enter the name of the app as it is to be displayed in the company portal. 

        > [!NOTE]
        > If you change the name of the app through Intune after you have deployed and installed the app, the app will no longer be able to be targeted using commands.

    - **Description**: Enter a description for the app. This description is displayed to users in the company portal.
    - **Publisher**: Enter the name of the publisher of this app.
   - **App URL**: Enter the URL of the website that hosts the app that you want to assign.

        > [!NOTE]
        > Once you deploy a web link app, the App URL cannot be modified, which is by design.

   - **Require a managed browser to open this link**: Select this option to assign to your users a link to a website or web app that they can open in the Intune managed browser. This browser must be installed on their device. 

      > [!NOTE]
      > iOS/iPadOS web clips that require a managed browser will not work with [home screen layout policies.](../configuration/ios-device-features-settings.md)
    - **Full screen**: [iOS/iPadOS only] If configured to **Yes**, launches the web clip as a full-screen web app without a browser. Additionally, there's no URL or search bar, and no bookmarks.
    - **Ignore manifest scope**: [iOS/iPadOS only] If configured to **Yes**, a full screen web clip can navigate to an external web site without showing Safari UI. Otherwise, Safari UI appears when navigating away from the web clip's URL. This setting has no effect when **Full screen** is set to **No**. Available in iOS 14 and later.
    - **Precomposed**: [iOS/iPadOS only] If configured to **Yes**, prevents Apple's application launcher (SpringBoard) from adding "shine" to the icon.
    - **Target application bundle identifier**: [iOS/iPadOS only] Enter the application bundle identifier that specifies the application that opens the URL. Available in iOS 14 and later.
    - **Category**: Optionally, select one or more of the built-in app categories, or a category that you created. Doing so makes it easier for users to find the app when they browse the company portal.
    - **Show this as a featured app in the Company Portal**: Select this option to display the app suite prominently on the main page of the company portal when users browse for apps.
    - **Information URL**: Link people to a website or documentation that has more information about the app. The information URL will be visible to users in Company Portal.
    - **Privacy URL**: Provide a link for people who want to learn more about the app's privacy settings and terms. The privacy URL will be visible to users in Company Portal.
    - **Developer**: The name of the company or Individual that developed the app. This information will be visible to people signed into the admin center.
    - **Owner**: The name of the person in your organization who manages licensing or is the point-of-contact for this app. This name will be visible to people signed in to the admin center.
    - **Notes**: Add additional notes about the app. Notes will be visible to people signed in to the admin center.
    - **Logo**: Upload an icon that will be associated with the app. This icon is displayed with the app when users browse the company portal.
6. Click **Next** to display the **Scope tags** page.
7. Click **Select scope tags** to optionally add scope tags for the app. For more information, see [Use role-based access control (RBAC) and scope tags for distributed IT](../fundamentals/scope-tags.md).
8. Click **Next** to display the **Assignments** page.
1. Select the group assignments for the app. For more information, see [Add groups to organize users and devices](../fundamentals/groups-add.md). 
> [!NOTE]
> iOS/iPadOS and macOS web clips that are assigned as **Required** cannot be installed as removable. To remove these web clips, you must change their assignment to **Uninstall**. If you delete the assignment without first changing it to **Uninstall**, the web clip will remain on the device and cannot be removed by the user. 
10. Click **Next** to display the **Review + create** page. Review the values and settings you entered for the app.
1. When you are done, click **Create** to add the app to Intune.

   The **Overview** blade of the app you've created is displayed.

End-users can launch web apps directly from the Windows Company Portal app by selecting the web app and then choosing the option **Open in browser**. The published web URL is opened directly in the web browser. 

## Next steps

The app that you've created is displayed in the apps list, where you can assign it to the groups that you select. For help, see [Assign apps to groups](apps-deploy.md). 
