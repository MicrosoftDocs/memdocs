---
title: "Technical Preview 1707 | Microsoft Docs"
description: "Learn about features available in the Technical Preview version 1707 for System Center Configuration Manager."
ms.custom: na
ms.date: 06/30/2017
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cb405ba0-8792-4ab7-988b-2f835f3a9550
author: Brenduns
ms.author: brenduns
manager: angrobe
---
# Capabilities in Technical Preview 1707 for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*

This article introduces the features that are available in the Technical Preview for System Center Configuration Manager, version 1707. You can install this version to update and add new capabilities to your Configuration Manager technical preview site. Before installing this version of the technical preview, review [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md) to become familiar with general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback about the features in a technical preview.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
-->

**The following are new features you can try out with this version.**  

<!--  Rough Section Template
##  FEATURE

### Procedure 1
### Try it out!  
 Try to complete the following tasks and then send us **Feedback** from the **Home** tab of the Ribbon to let us know how it worked:
 -  Task 1
 -  Task 2              
-->

## Client Peer Cache support for express installation files for Windows 10 and Office 365
<!-- 1352486 -->
Beginning with this release, Peer Cache supports distribution of content express installation files for Windows 10, and of update files for Office 365. No additional configurations are required.

## Configure and deploy Windows Defender Application Guard policies
<!-- 1351960 -->

[Windows Defender Application Guard](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#XLxEbcpkuKcFebrw.97) is a new Windows feature that helps protect your users by opening untrusted web sites in a secure isolated container that is not accessible by other parts of the operating system. In this technical preview, we’ve added support to configure this feature using Configuration Manager compliance settings which you configure, and then deploy to a collection. This feature will be released in preview for the 64-bit version of the Windows 10 Creator’s Update (codename: RS2). To test this feature now, you must be using a preview version of this update. 

### Before you start

To create and deploy Windows Defender Application Guard policies, the Windows 10 devices to which you deploy the policy must be configured with a network isolation policy. For more details, see the blog post referenced later. This capability works only with current Windows 10 Insider builds. To test it, your clients must be running a recent Windows 10 Insider Build.

### Try it out!
Ensure you have read the blog post to understand the basics about Windows Defender Application Guard.

#### To create a policy, and to browse the available settings:

1. In the Configuration Manager console, choose **Assets and Compliance**.
2. In the **Assets and Compliance** workspace, choose **Overview** > **Endpoint Protection** > **Windows Defender Application Guard**.
3. In the **Home** tab, in the **Create** group, click **Create Windows Defender Application Guard Policy**.
4. Using the blog post as a reference, you can browse and configure the available settings to try the feature out.
5. In this release, we’ve added the new **Network Definition** page to the wizard. Here, specify the corporate identity, and define your corporate network boundary.
Windows 10 PCs store only one network isolation list on the client. In this release, you can create two different kinds of network isolation lists (one from Windows Information Protection, and one from Windows Defender Application Guard), and deploy them to the client. If you deploy both policies, these network isolation lists must match. If you deploy lists that don’t match to the same client, the deployment will fail.
You can find more information about how to specify network definitions in the [Windows Information Protection documentation]( https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-sccm). 
6. When you are finished, complete the wizard, and deploy the policy to one or more Windows 10 devices.

### Further reading
To read more about Windows Defender Application Guard, see [this blog post](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Additionally, to learn more about Windows Defender Application Guard Standalone mode, see [this blog post](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).



## Placeholder Section
Remove before publishing.
