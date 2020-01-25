---
title: Manage Application Guard policies
titleSuffix: Configuration Manager
description: Learn how to create and deploy Windows Defender Application Guard policies
ms.date: 07/26/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: 33a6c1d9-4dd8-411c-a748-693a5bd2ea5a
author: mestew
ms.author: mstewart
manager: dougeby


---

# Create and deploy Windows Defender Application Guard policy

*Applies to: Configuration Manager (current branch)*
<!-- 1351960 -->  
You can create and deploy [Windows Defender Application Guard (Application Guard)](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview) policies by using the Configuration Manager endpoint protection. These policies help protect your users by opening untrusted web sites in a secure isolated container that isn't accessible by other parts of the operating system.

## Prerequisites

To create and deploy a Windows Defender Application Guard policy, you must use the Windows 10 Fall Creator’s Update (1709). The Windows 10 devices to which you deploy the policy must be configured with a network isolation policy. For more information, see the [Windows Defender Application Guard overview](https://docs.microsoft.com/windows/threat-protection/windows-defender-application-guard/wd-app-guard-overview).

## Create a policy, and to browse the available settings

1. In the Configuration Manager console, choose **Assets and Compliance**.
2. In the **Assets and Compliance** workspace, choose **Overview** > **Endpoint Protection** > **Windows Defender Application Guard**.
3. In the **Home** tab, in the **Create** group, click **Create Windows Defender Application Guard Policy**.
4. Using the [article](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/configure-wd-app-guard) as a reference, you can browse and configure the available settings. Configuration Manager allows you to set certain policy settings:
   - [Host interaction settings](#bkmk_HIS)
   - [Application behavior](#bkmk_ABS)
   - [File management](#bkmk_FM)
5. On the **Network Definition** page, specify the corporate identity, and define your corporate network boundary.

    > [!NOTE]
    > Windows 10 PCs store only one network isolation list on the client. You can create two different kinds of network isolation lists and deploy them to the client:
    >
    >  - one from Windows Information Protection
    >  - one from Windows Defender Application Guard
    >
    > If you deploy both policies, these network isolation lists must match. If you deploy lists that don’t match to the same client, the deployment will fail. For more information, see the [Windows Information Protection documentation](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/create-wip-policy-using-sccm).

6. When you're finished, complete the wizard, and deploy the policy to one or more Windows 10 1709 devices.

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
  - Retain user-generated browser data
  - Audit security events in the isolated application guard session

### <a name="bkmk_FM"></a> File management
<!--3555858-->
Starting in Configuration Manager version 1906, There's a policy setting that enables users to trust files that normally open in Application Guard. Upon successful completion, the files will open on the host device instead of in Application Guard. For more information about the Application Guard policies, see [Configure Windows Defender Application Guard policy settings](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/configure-wd-app-guard).

- **Allow users to trust files that open in Windows Defender Application Guard** - Enable the user to mark files as trusted. When a file is trusted, it opens on the host rather than in Application Guard. Applies to Windows 10 version 1809 or higher clients.
  - **Prohibited:** Don't allow users to mark files as trusted (default).
  - **File checked by antivirus:** Allow users to mark files as trusted after an antivirus check.
  - **All files:** Allow users to mark any file as trusted.

When you enable file management, you may see errors logged in the client's DCMReporting.log. The errors below typically don't effect functionality: <!--4619457-->

- On compatible devices:
  - FileTrustCriteria_condition not found
- On non-compatible devices:
  - FileTrustCriteria_condition not found
  - FileTrustCriteria_condition could not be located in the map
  - FileTrustCriteria_condition not found in digest

To edit Application Guard settings, expand **Endpoint Protection** in the **Assets and Compliance** workspace, then click on the **Windows Defender Application Guard** node. Right-click on the policy you want to edit, then select **Properties**.

## Next steps

To read more about Windows Defender Application Guard:
 [Windows Defender Application Guard Overview](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/wd-app-guard-overview).
[Windows Defender Application Guard FAQ](https://docs.microsoft.com/windows/security/threat-protection/windows-defender-application-guard/faq-wd-app-guard).
