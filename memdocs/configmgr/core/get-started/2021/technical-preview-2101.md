---
title: Technical preview 2101
titleSuffix: Configuration Manager
description: Learn about new features available in the Configuration Manager technical preview branch version 2101.
ms.date: 01/29/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ROBOTS: NOINDEX
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Features in Configuration Manager technical preview version 2101

*Applies to: Configuration Manager (technical preview branch)*

This article introduces the features that are available in the technical preview for Configuration Manager, version 2101. Install this version to update and add new features to your technical preview site.

Review the [technical preview](../technical-preview.md) article before installing this update. That article familiarizes you with the general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback.

The following sections describe the new features to try out in this version:

<!-- [!INCLUDE [Example feature name](includes/2101/1234567.md)] -->

[!INCLUDE [Console extension installation](includes/2101/3555909.md)]
[!INCLUDE [Deploy a feature update with a task sequence](includes/2101/3555906.md)]
[!INCLUDE [Tenant Attach: Required application deployments display in Microsoft Intune admin center](includes/2101/8795301.md)]      
[!INCLUDE [Client setting for displaying Software Center custom tabs](includes/2101/9142301.md)]
[!INCLUDE [Simplified CMPivot permissions requirements](includes/2101/7898885.md)]
[!INCLUDE [Allow exclusion of organizational units (OU) from Active Directory User Discovery](includes/2101/5193509.md)]
[!INCLUDE [Changes to Support Center](includes/2101/8693068.md)]
[!INCLUDE [Prerequisite rule for deprecated Azure Monitor connector](includes/2101/8269855.md)]
[!INCLUDE [Manage aged distribution point messages](includes/2101/8561493.md)]
[!INCLUDE [Encryption algorithm to capture and restore user state](includes/2101/9171505.md)]
[!INCLUDE [PowerShell release notes preview](includes/2101/8905809.md)]


## Known issues
### Unable to upload files when sending a frown through the console
<!--9238008-->
When filing a frown from the Configuration Manager console, files won't be uploaded.  

**Mitigation:** To work around this issue, you'll need to edit the `microsoft.configurationmanagement.exe.config` file located in the admin console installation directory. Use the instruction below to work around the issue:

1. Open **Notepad** as administrator.
1. From Notepad, choose **File** then **Open**.
1. Browse to the Configuration Manager console installation directory and open the file named `Microsoft.ConfigurationManagement.exe.config`. 
   - The default location is `C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`

1. In the `<runtime>` section, add the following text:

   ```text
       <assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">
         <dependentAssembly>
           <assemblyIdentity name="Microsoft.WindowsAzure.Storage" publicKeyToken="31bf3856ad364e35" culture="neutral" />
           <bindingRedirect oldVersion="0.0.0.0-8.7.0.0" newVersion="6.2.0.0" />
         </dependentAssembly>
       </assemblyBinding>
   ```
      :::image type="content" source="media/9238008-config-file.png" alt-text="Notepad with line added to the runtime section highlighted. The next non-highlighted line starts with &lt;AppContextSwitchOverrides" lightbox="media/9238008-config-file.png":::

1. Save the config file then reopen the Configuration Manager console and file your feedback. 
 



<!--
## General known issues

[!INCLUDE [Azure AD authentication doesn't work](includes/2101/known-issue-7569264.md)]
-->

## Next steps

For more information about installing or updating the technical preview branch, see [Technical preview](../technical-preview.md).

For more information about the different branches of Configuration Manager, see [Which branch of Configuration Manager should I use?](../../understand/which-branch-should-i-use.md).
