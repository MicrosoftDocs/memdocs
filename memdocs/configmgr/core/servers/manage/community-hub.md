---
title: Community hub and GitHub
titleSuffix: Configuration Manager
description: Enable and use Community hub in Configuration Manager
ms.date: 06/20/2022
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Community hub and GitHub
<!--3555935, 3555936-->
*Applies to: Configuration Manager (current branch)*

> [!IMPORTANT]
> Starting in March 2023, this feature of Configuration Manager is being removed. 
All future versions, starting with 2303 will not have the Community hub node in the admin console. The Community hub node in older versions will be redirected to [deprecated features](../../plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md).  

The IT Admin community has developed a wealth of knowledge over the years. Rather than reinventing items like Scripts and Reports from scratch, we've built a **Community hub** in Configuration Manager where IT Admins can share with each other. By leveraging the work of others, you can save hours of work. The Community hub fosters creativity by building on others work and having other people build on yours. GitHub already has industry-wide processes and tools built for sharing. Now, the Community hub can leverage those tools directly in the Configuration Manager console as foundational pieces for driving this new community.

## About Community hub

Community hub supports the following objects:

[!INCLUDE [Community hub object type information](includes/community-hub-object-types.md)]

## <a name="bkmk_new"></a> What's new

- Support for downloading signed console extensions and limited contribution, added in July 2021 <!--3555909, 8116426-->
- [Filter content](#bkmk_search) when using search, added in June 2021 <!--8516139-->
- Support for configuration baselines including child configuration items, added in March 2021 <!--7983121-->
- Support for Power BI reports, added in February 2021 <!--5679831-->

## Prerequisites

- The device running the Configuration Manager console used to access the Community hub needs the following items:
   - .NET Framework version 4.6 or later
     - .NET Framework version 4.6.2 or later is required starting in Configuration Manager 2010
     - Starting in version 2107, the console requires .NET version 4.6.2, and version 4.8 is recommended.<!--10402814--> For more information, see [Install the Configuration Manager console](../deploy/install/install-consoles.md#net-version-requirements).
   - A supported version of Windows 10 or later
      - Windows Server isn't supported before version 2010, so the Configuration Manager console needs to be installed on a supported Windows client device separate from the site server.
      - Starting in version 2010, [install the Microsoft Edge WebView2 console extension](#bkmk_webview2) to support Windows Server. <!--3555940, 8625943, 8717639 -->


- The [administration service](../../../develop/adminservice/set-up.md) in Configuration Manager needs to be set up and functional.

- If your organization restricts network communication with the internet using a firewall or proxy device, you need to allow the Configuration Manager console to access internet endpoints. For more information, see [Internet access requirements](../../plan-design/network/internet-endpoints.md#community-hub).

- A GitHub account is only required to contribute and share content from the **Your hub** page. If you don't wish to share, you can use contributions from others without having a GitHub account, For more information, see [Contribute to Community hub](community-hub-contribute.md).
   > [!IMPORTANT]
   > Configuration Manager versions 2006 and earlier won't be able to sign in to GitHub. Configuration Manager version 2010 or later with the [WebView2 console extension installed](#bkmk_webview2) is required for sign in. <!--9598183-->

## Permissions

- To import a script: **Create** permission for **SMS_Scripts** class.
- To import a report: Full Administrator security role.
- Starting in version 2010, Full Administrators can opt in the hierarchy for unreviewed content via hierarchy settings. Lower hierarchy administrators can't opt in the hierarchy for unreviewed hub items. For more information, see the [Categorize Community hub content](#bkmk_category) section.

[!INCLUDE [Community hub security role information](includes/community-hub-security-roles.md)]

## Use the Community hub

1. Go to the **Community hub** node in the **Community** workspace.
1. Select an item to download.
1. You'll need appropriate permissions in your Configuration Manager site to download objects from the hub and import them into the site.
    - To import a script: **Create** permission for SMS_Scripts class.
    - To import a report: Full Administrator security role.
1. Downloaded reports are deployed to a report folder called **hub** on the reporting services point. Downloaded scripts can be seen in the **Run Scripts** node. Typically, downloaded items are placed in the console node for which they're used.
1. View all items downloaded from the hub by your organization by selecting **Your downloads** from the **Community hub** node.

[![All items downloaded from the Community hub](./media/3555935-community-hub-downloads.png)](./media/3555935-community-hub-downloads.png#lightbox)

## <a name="bkmk_search"></a> Filter Community hub content when searching
<!--8516139-->
You can filter content in the Community hub when using search. The following filters are available to use when searching:

[!INCLUDE [Community hub search filters](includes/community-hub-search-filter.md)]

## <a name="bkmk_deeplink"></a> Direct links to Community hub items
<!--4224406-->
[!INCLUDE [Community hub direct link information](includes/community-hub-links.md)]

## <a name="bkmk_category"></a> Categorize Community hub content
<!--8052494-->
*(Introduced in version 2010)*

Starting in Configuration Manager version 2010, Community hub content is grouped into a Microsoft, curated, or unreviewed category to allow admins to choose the types of content their environment displays. Admins can choose from the different categories of content that are provided in the **Community hub** to match their risk profile and their willingness to share and use content from those outside Microsoft and outside their own company. Only **Full Administrators** can opt in the hierarchy for unreviewed content via hierarchy settings.

Community hub content has three categories for content sources:
- **Microsoft curated**: Content provided by Microsoft
- **Community curated**: Content provided by the community that gets reviewed by Microsoft
- **Community unreviewed**: General content from the community that doesn't get reviewed by Microsoft

:::image type="content" source="./media/8052494-community-hub-content-sources.png" alt-text="The three categories for content sources in Community hub":::

Admins can choose the types of content their environment displays from the following options:

- **Display Microsoft content**: Selecting this option means that only content created by Microsoft will be shown in the Community hub. This content has had some basic testing and scanning validation to confirm no malware and inappropriate text.
- **Display Microsoft and curated community content**: Show curated content from both Microsoft and community partners with basic level of review. Selecting this option means that only content that has been curated will be shown. The curation process includes basic review to confirm that the content doesn’t have malware and inappropriate text, but hasn’t necessarily been tested. It will include content from the community, not just from Microsoft.
- **Display all content including unreviewed content**:  Selecting this option means that all content is shown. This option includes unreviewed open-source type samples from the community, meaning that the content hasn’t necessarily been reviewed at all. It's provided as-is as open-source type sample content. Doing your own inspection and testing before using is highly encouraged, which is good practice on any content, but especially this class of content.

:::image type="content" source="./media/8052494-community-hub-content-hierarchy-settings.png" alt-text="Hierarchy settings for allowed content sources for the Community hub":::

Since the content is *open-source* style content, admins should always review what is provided before consuming it. The new curation process is intended to vet the material to make sure there aren't obvious quality or compliance issues, but it will be somewhat of a cursory review. All content stored within GitHub and accessed from the Community hub isn’t supported by Microsoft. Microsoft doesn’t validate content collected from or shared by the general community. For more information, see [GitHub Terms of Service](https://help.github.com/terms) and [GitHub Privacy Statement](https://help.github.com/privacy).

### Select the content categories to display in Community hub for the environment

1. In the Configuration Manager console, go to **Administration** > **Overview** > **Site Configuration** > **Sites**.
1. Select the top-level site in your hierarchy and select **Hierarchy Settings** from the ribbon.
1. On the **General** tab, change the **Community hub** setting to **Display Microsoft content**.
1. Select **Ok** when you're finished changing the hierarchy setting.
1. Open the **Community hub** node in the **Community** workspace.
1. Ensure that only Microsoft content is displayed and available for download.
1. Go back to **Hierarchy Settings** and select another option such as **Display all content, including unreviewed content**.
1. Confirm that only the type of content is displayed and able to be downloaded from the Community hub, that matches the corresponding hierarchy setting category.

## <a name="bkmk_webview2"></a> Install the WebView2 console extension
<!--3555940, 8625943, 8717639 -->
*(Introduced in version 2010)*

The Microsoft Edge WebView2 console extension enables the full functionality for Community hub. If WebView2 isn't installed, a banner is shown when you navigate to the **Community hub** node.<!--9598183--> The WebView2 console extension:

- Displays the **Community hub** on Windows Server operating systems
- Enables sign in for GitHub
   - GitHub sign-in is needed for [contributing to Community hub](community-hub-contribute.md) but not for downloading items.

> [!IMPORTANT]
> - When you upgrade to Configuration Manager 2107, you will be prompted to install the WebView2 console extension again. <!--0247811, 10005418-->
> - Configuration Manager versions 2006 and earlier can’t sign into GitHub but can still download items. Using Community hub on Windows Server requires the WebView2 console extension and Configuration Manager version 2010 or later. <!--9082812-->

Follow the instructions below to enable the full functionality of Community hub:

1. In the upper-right corner of the console, select the bell icon to display Configuration Manager console notifications.

   :::image type="content" source="./media/3555909-notification.png" alt-text="Notifications in the Configuration Manager console":::

1. The notification will say **New custom console extensions are available**.

   :::image type="content" source="./media/3555909-extension-notification.png" alt-text="New custom console extensions are available notification":::

1. Select the link **Install custom console extensions** to launch the install.
1. When the install completes, select **Close** to restart the console.

    :::image type="content" source="./media/3555909-extension-installed.png" alt-text="Console extension completed install":::

1. Confirm that you can view the **Community hub** node from the machine running the Windows Server operating system.
   - You may also notice that a new folder `AdminConsole\bin\Microsoft.WebView2.FixedVersionRuntime.<version>.x86` was created.
   - The files are automatically downloaded from https://developer.microsoft.com/en-us/microsoft-edge/webview2/#download-section with the other redistributable files.

> [!Tip]
> Starting in Configuration Manager version 2103, you can also install the WebView2 extension from the **Console Extensions** node. For more information, see [Install an extension on a local console](admin-console-extensions.md#bkmk_local_install).

## <a name="bkmk_known"></a> Known issues

### Community hub doesn't load
<!--9561090-->
The Community hub may not load, or load after a long delay if the WebView2 console extension hasn't been installed. For more information about installing console extensions, see the [Install the WebView2 console extension](#bkmk_webview2) and [Managing console extensions (starting in version 2103)](admin-console-extensions.md).

### Unhandled exception occurs when loading Community hub
<!--12109686-->
In certain circumstances, you may encounter the following exception when loading Community hub:

`Could not load type 'System.Runtime.InteropServices.Architecture' from assembly 'mscorlib, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089'.`

**Workaround**: To work around this issue, update the .NET Framework to version 4.7.1 or later for the machine running the Configuration Manager console.

### Unable to access Community hub node when running console as a different user
<!--7826897-->
If you're signed in as a user with lower rights and choose **Run as** a different user to open the Configuration Manager console, you may not be able to access the **Community hub** node.

### Downloaded reports don't get removed from your downloads page
<!--7851305-->
If you delete a downloaded report from the **Monitoring** > **Reports** node, the report isn't deleted from the **Community hub** > **Your downloads** page and you're unable to download the report again.

### Unable to download baseline that contains a previously downloaded configuration item
<!--9528524-->
 If you previously downloaded a configuration item from Community hub using Configuration Manager 2010, you may receive an error when downloading a baseline after upgrading to Configuration Manager version 2103. A download error can occur when the baseline contains an updated version of the configuration item you previously downloaded with Configuration Manager 2010.

**Workaround**: To work around this issue, delete the configuration item you previously downloaded, then download the baseline with the new version of the configuration item.

### Unable to sign in when single sign on with multifactor authentication is used
<!--10436429-->

When single sign on with multifactor authentication is used, you may not be able to sign in for the following features when using Configuration Manager 2103 and earlier:
- Community hub
- Community hub from CMPivot
- Custom tabs in Software Center that load a website that's subject to conditional access policies

## Next steps

[Contribute to the Configuration Manager Community hub](community-hub-contribute.md)
