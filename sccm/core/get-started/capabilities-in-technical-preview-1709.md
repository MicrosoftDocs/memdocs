---
title: "Technical Preview 1709 | Microsoft Docs"
description: "Learn about features available in the Technical Preview version 1709 for System Center Configuration Manager."
ms.custom: na
ms.date: 09/25/2017
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a3ef6bdc-a204-4c4c-a02f-2bd03f35183e
author: Brenduns
ms.author: brenduns
manager: angrobe
---
# Capabilities in Technical Preview 1709 for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*

This article introduces the features that are available in the Technical Preview for System Center Configuration Manager, version 1709. You can install this version to update and add new capabilities to your Configuration Manager technical preview site. Before installing this version of the technical preview, review [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md) to become familiar with general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback about the features in a technical preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Known Issues in this Technical Preview:**
-   **Update to preview version 1709 fails when you have a site server in passive mode**. When you run the preview version 1706, 1707, or 1708 and have a [primary site server in passive mode](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability), you must uninstall the passive mode site server before you can successfully update your preview site to version 1709. You can reinstall the passive mode site server after your site runs version 1709.

  To uninstall the passive mode site server:
  1. In the console go to **Administration** > **Overview** > **Site Configuration** > **Servers and Site System Roles**, and then select the passive mode site server.
  2. In the **Site System Roles** pane, right click on the **Site server** role, and then choose **Remove Role**.
  3. Right-click on the passive mode site server, and then choose **Delete**.
  4. After the site server uninstalls, on the active primary site server restart the service **CONFIGURATION_MANAGER_UPDATE**.




**The following are new features you can try out with this version.**  

## Improved VPN Profile Experience in Configuration Manager Console <!-- 1313282 -->

We’ve updated the VPN profile wizard and properties pages to display settings appropriate for the selected platform.  Specifically:

- Each platform has its own workflow, meaning that new VPN profiles contain only the setting supported by the platform.
- The **Supported Platforms** pages now appears after the **General** page.  You now choose the platform before setting property values.
- When the platform is set to **Android**, **Android for Work**, or **Windows 8.1**, the **Supported platforms** page is not needed and is not displayed.
- The Configuration Manager client-based workflow has been combined with the hybrid mobile device (MDM) client-based Windows 10 workflows; they support the same settings.
- Each platform workflow includes just the settings appropriate for that workflow.  For example, the Android workflow contains settings appropriate for Android; settings appropriate for iOS or Windows 10 Mobile no longer appear in the Android workflow.
- For Windows 8.1 devices, settings managed by Configuration Manager ar clearly marked.
- The Automatic VPN page is obsolete and has been removed.

These changes apply to new VPN profiles.  

To minimize compatibility risk, existing VPN profiles are unchanged.  When you edit an existing profile, the settings appear as they did when the profile was created.  

### Try it out!

Create a new VPN profile using the usual process. Notice that the first page in the VPN profile wizard’s options have changed.

1.	Go to **Assets and Compliance** > **Overview** > **Compliance Settings** > **Company Resource Access** > **VPN Profiles** and then choose **Create VPN Profile**.
2.	Enter a name on the **General** page and choose one of the following options under **Specify the type of VPN profile you want to create**:

    - Windows 10  
    - Windows 8.1  
    - Windows Phone 8.1  
    - iOS and macOS  
    - Android  
    - Android for Work  

3.	If you choose **Windows 8.1**, you also have the option to **Create new profile** or **Import from file**.
4.	Complete the wizard to finish creating the profile.

As you select different platforms, notice that only the settings relevant to the selected platform display.



<!--  Rough Section Template
##  FEATURE    [Commented TFS #]

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->
