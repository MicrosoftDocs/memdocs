---
title: "Create and deploy a Windows Defender Application Guard policy"
titleSuffix: "System Center Configuration Manager"
description: "Create and deploy Windows Defender Application Guard policy."
ms.custom: na
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 
caps.latest.revision: 5
author: mestew
ms.author: mstewart
manager: angrobe
---


# Create and deploy Windows Defender Application Guard policy 
*Applies to: System Center Configuration Manager (Current Branch)*
<!-- 1351960 -->
You can create and deploy [Windows Defender Application Guard](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview) policies by using the Configuration Manager endpoint protection. These policies help protect your users by opening untrusted web sites in a secure isolated container that is not accessible by other parts of the operating system.

## Prerequisites

To create and deploy a Windows Defender Application Guard policy, you must use the Windows 10 Fall Creator’s Update (1709). Also, the Windows 10 devices to which you deploy the policy must be configured with a network isolation policy. For more information, see the [Windows Defender Application Guard overview](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview). 


## Create a policy, and to browse the available settings:

1. In the Configuration Manager console, choose **Assets and Compliance**.
2. In the **Assets and Compliance** workspace, choose **Overview** > **Endpoint Protection** > **Windows Defender Application Guard**.
3. In the **Home** tab, in the **Create** group, click **Create Windows Defender Application Guard Policy**.
4. Using the [article](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/configure-wd-app-guard) as a reference, you can browse and configure the available settings. Configuration Manager allows you to set certain policy settings see [host interaction settings](#BKMK_HIS) and [application behavior](#BKMK_AppB).
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

6. When you are finished, complete the wizard, and deploy the policy to one or more Windows 10 1709 devices.

### <a name="bkmk_HIS"></a> Host interaction settings
Configures interactions between host devices and the Application Guard container. Before Configuration Manager version 1802, both application behavior and host interaction were under the **Settings** tab.

- **Clipboard** - Under settings prior to Configuration Manager 1802
    - Permitted content type
        - Text
        - Images
- **Printing:**
    - Enable printing to XPS
    - Enable printing to PDF
    - Enable printing to local printers
    - Enable printing to network printers
- **Graphics:** (starting with Configuration Manager version 1802)
    - Virtual graphics processor access
- **Files:** (starting with Configuration Manager version 1802)
    - Save downloaded files to host

### <a name="bkmk_ABS"></a> Application behavior settings
Configures application behavior inside the Application Guard session. Before Configuration Manager version 1802, both application behavior and host interaction were under the **Settings** tab.

- **Content:**
   - Enterprise sites can load non-enterprise content, such as third-party plug-ins.
- **Other:**
    - Retain user generated browser data
    - Audit security events in the isolated application guard session



## Next steps
To read more about Windows Defender Application Guard:
 [Windows Defender Application Guard Overview](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/wd-app-guard-overview).
[Windows Defender Application Guard FAQ](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/faq-wd-app-guard).
