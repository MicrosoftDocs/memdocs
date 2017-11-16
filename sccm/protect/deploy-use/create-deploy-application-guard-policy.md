---
title: "Create and deploy a Windows Defender Application Guard policy"
titleSuffix: "Configuration Manager"
description: "Create and deploy Windows Defender Application Guard policy."
ms.custom: na
ms.date: 11/21/2017
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 
caps.latest.revision: 5
author: ErikjeMS
ms.author: erikje
manager: angrobe
---
# Create and deploy Windows Defender Application Guard policy <!-- 1351960 -->

You can create and deploy [Windows Defender Application Guard](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview) policies by using the Configuration Manager endpoint protection. These policies help protect your users by opening untrusted web sites in a secure isolated container that is not accessible by other parts of the operating system.

## Prerequisites

To create and deploy a Windows Defender Application Guard policy, you must use the Windows 10 Fall Creator’s Update. Also, the Windows 10 devices to which you deploy the policy must be configured with a network isolation policy. For more information, see [this blog post](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). This capability works only with current Windows 10 Insider builds. To test it, your clients must be running a recent Windows 10 Insider Build.


## Create a policy, and to browse the available settings:

1. In the Configuration Manager console, choose **Assets and Compliance**.
2. In the **Assets and Compliance** workspace, choose **Overview** > **Endpoint Protection** > **Windows Defender Application Guard**.
3. In the **Home** tab, in the **Create** group, click **Create Windows Defender Application Guard Policy**.
4. Using the [blog post](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97) as a reference, you can browse and configure the available settings.
5. On the **Network Definition** page, specify the corporate identity, and define your corporate network boundary.

    > [!NOTE]
    > Windows 10 PCs store only one network isolation list on the client. You can create two different kinds of network isolation lists and deploy them to the client:
    >
    >  - one from Windows Information Protection
    >  - one from Windows Defender Application Guard
    >
    > If you deploy both policies, these network isolation lists must match. If you deploy lists that don’t match to the same client, the deployment will fail. For more information, see the [Windows Information Protection documentation](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-sccm).
    > 
    > 

6. When you are finished, complete the wizard, and deploy the policy to one or more Windows 10 devices.

## Next steps
To read more about Windows Defender Application Guard, see [this blog post](https://blogs.windows.com/msedgedev/2016/09/27/application-guard-microsoft-edge/#BmJGKPfSjHHzsMmI.97). Additionally, to learn more about Windows Defender Application Guard Standalone mode, see [this blog post](https://techcommunity.microsoft.com/t5/Windows-Insider-Program/Windows-Defender-Application-Guard-Standalone-mode/td-p/66903).
