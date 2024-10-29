---
title: Technical preview 2405
titleSuffix: Configuration Manager
description: Learn about new features available in the Configuration Manager technical preview branch version 2405.
ms.date: 06/07/2024
ms.service: configuration-manager
ms.topic: conceptual
author: PalikaSingh
ms.author: palsi
manager: apoorvseth
ROBOTS: NOINDEX, NOFOLLOW
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Features in Configuration Manager technical preview version 2405

*Applies to: Configuration Manager (technical preview branch)*

This article introduces the features that are available in the technical preview for Configuration Manager, version 2405. Install this version to update and add new features to your technical preview site. When you install a new technical preview site, this release is also available as a baseline version.

Review the [technical preview](../technical-preview.md) article before installing this update. That article familiarizes you with the general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback.

The following sections describe the new features to try out in this version:

[!INCLUDE [Introducing Centralized Search  - Desired Workspace Selection](includes/2405/27927529.md)]
[!INCLUDE [BitLocker support in Arm devices](includes/2405/27825049.md)]
[!INCLUDE [Configuration Manager now support SQL Extended Protection for Authentication](includes/2405/28106757.md)]
[!INCLUDE [Performance Enhancement of policy processing and collection evaluation](includes/2405/27679763.md)]

## Known issues

### Unable to import or connect to Powershell Configuration Manager module via console

While importing or connecting to Configuration manager Powershell module via CM console users get the following error message :
`PS C:\Build\AdminConsole\bin> Import-Module .\ConfigurationManager.psd1
Import-Module : The module manifest 'C:\Build\AdminConsole\bin\ConfigurationManager.psd1' could not be
processed because it is not a valid Windows PowerShell restricted language file. Remove the elements that are not permitted by the
restricted language`


### Configuration Manager console won't automatically update

If you update a technical preview site from version 2401 to a later version, the Configuration Manager console fails to update. This problem is because of a known issue in the extension installer.

**Mitigation:** To work around this issue, after you update the site from version 2401 to a later version, manually uninstall the previous console and run **ConsoleSetup.exe**.

For more information, see [Install the Configuration Manager console](../../servers/deploy/install/install-consoles.md)


## Next steps

For more information about installing or updating the technical preview branch, see [Technical preview](../technical-preview.md).

For more information about the different branches of Configuration Manager, see [Which branch of Configuration Manager should I use?](../../understand/which-branch-should-i-use.md).

