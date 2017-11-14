---
title: "Technical Preview 1711 | Microsoft Docs"
titleSuffix: "Configuration Manager"
description: "Learn about features available in the Technical Preview version 1711 for System Center Configuration Manager."
ms.custom: na
ms.date: 11/16/2017
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2e68dc12-6776-437a-9138-45cd7d4bf9cf
author: Brenduns
ms.author: brenduns
manager: angrobe
---
# Capabilities in Technical Preview 1711 for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*

This article introduces the features that are available in the Technical Preview for System Center Configuration Manager, version 1711. You can install this version to update and add new capabilities to your Configuration Manager technical preview site. Before installing this version of the technical preview, review [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md) to become familiar with general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback about the features in a technical preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->
**Known Issues in this Technical Preview:**
-   **Support for Windows 10, version 1709 (also known as the Fall Creators Update)**.  Beginning with this Windows release, Windows media includes multiple editions. When configuring a task sequence to use an operating system upgrade package or operating system image, be sure to select an [edition that is supported for use by Configuration Manager](/sccm/core/plan-design/configs/support-for-windows-10#windows-10-as-a-client).
-   **Update to a new preview version fails when you have a site server in passive mode**. When you run a preview version that has a [primary site server in passive mode](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability), you must uninstall the passive mode site server before you can successfully update your preview site to this new preview version. You can reinstall the passive mode site server after your site completes the update.

  To uninstall the passive mode site server:
  1. In the console go to **Administration** > **Overview** > **Site Configuration** > **Servers and Site System Roles**, and then select the passive mode site server.
  2. In the **Site System Roles** pane, right click on the **Site server** role, and then choose **Remove Role**.
  3. Right-click on the passive mode site server, and then choose **Delete**.
  4. After the site server uninstalls, on the active primary site server restart the service **CONFIGURATION_MANAGER_UPDATE**.

**The following are new features you can try out with this version.**  

<!--  Section Template
##  FEATURE
### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## Improvements to Run Task Sequence
<!-- 1261338 -->

This technical preview will improve the Run Task Sequence step. Improvements include the following items:

 - Support for all operating system deployment scenarios from Software Center, PXE, and media.
 - Improvements to console actions such as copy, import, export, and warning during object deletion. 
 - Support for the **Create Prestage Content** wizard.
 - Integration with deployment verification.
 - The Run Task Sequence step can now be used across multiple levels of task sequences, not just a single parent-child relationship. Multi-level relationships increase the complexity, so use with caution. These relationships are still checked for circular references.

### Try it out!  

Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:

1. In the task sequence editor, click **Add**, select **General**, and click **Run Task Sequence**.
2. Click **Browse** to select the child task sequence.

## Allow user interaction when installing an application <!-- 1356976 -->

With this preview, you can allow an end user to interact with an application installation during the running of the task sequence. For example, run a setup process that prompts the end user for various options. Some application installers cannot have user prompts silenced, or the installation process may require specific configuration values only known to the user. This feature allows you to handle these installation scenarios.

### Try it out!

Try to complete the following tasks and then send **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:

1.  Create or edit an application. For more information, see [Create applications with System Center Configuration Manager](/sccm/apps/deploy-use/create-applications).

2.  Create or edit a task sequence to install the application using the **Install Application** step. For more information, see [Install Application](/sccm/osd/understand/task-sequence-steps#BKMK_InstallApplication) in the [Task sequence steps in System Center Configuration Manager](/sccm/osd/understand/task-sequence-steps).

    a. Choose the **User Experience** tab in the **Windows Installer (\*msi file) Properties**.

    b. Select **Install for system** for **Install behavior**.

    c. Select **Whether or not a user is logged on** for **Log on requirement**.

    d. Select **Normal** for **Installation program visibility.

    e. Do not check the **Allow users to interact with the program installation** box.

3. You can add specific steps in your application installation, such as:

    a. Imaging task sequence after the Setup Windows and Configuration Manager step.

    b. In-place upgrade task sequence in the Post-Processing group.

4.  Deploy the task sequence to a client.
5.  Install the task sequence from Software Center.

During task sequence progress, the application installation interface appears on the target end-user device. The task sequence progress pauses until the end user completes the application installation workflow.

<!-- When we have another H2 in this topic, Add this Next Steps section back in.  -->

## Next Steps
For information about installing or updating the technical preview branch, see [Technical Preview for System Center Configuration Manager](/sccm/core/get-started/technical-preview).    