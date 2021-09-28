---
title: Language packs
titleSuffix: Configuration Manager
description: Learn about the language support available in Configuration Manager.
ms.date: 04/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: mestew
ms.author: mstewart
manager: dougeby
ms.localizationpriority: medium
---

# Language packs in Configuration Manager

*Applies to: Configuration Manager (current branch)*

This article provides technical details about language support in Configuration Manager. Configuration Manager site servers and clients are considered language-neutral. Add support for display languages by installing **server language packs** or **client language packs** at a central administration site and at primary sites. You select the server and client languages to support at a site from the available language pack files during the site installation process.

Install multiple languages at each site. You only need to install the languages that you use.

- Each site supports multiple languages for Configuration Manager consoles.

- Add support for only the client languages that you want to support by installing individual client language packs at each site.

When you install support for a language that matches the following components:

- The display language of a computer: Both the Configuration Manager console and the client user interface that runs on that computer display information in that language.

- The language preference that's in use by the web browser of a computer: Connections to web-based information display in that language. For example, SQL Server Reporting Services.

When you run Configuration Manager setup, it downloads language pack files as part of the prerequisites and redistributable files. You can also use the [setup downloader](setup-downloader.md) to download these files before you run setup.

## Server languages  

Use the following table to map a locale ID to a language that you want to support on servers. For more information about locale IDs, see [Locale IDs assigned by Microsoft](/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c).  

|Server language|Locale ID (LCID)|Three-letter code|  
|---------------------|------------------------|-----------------------|  
|English (default)|0409|ENU|  
|Chinese (Simplified)|0804|CHS|  
|Chinese (Traditional, Taiwan)|0404|CHT|  
|Czech|0405|CSY|  
|Dutch - Netherlands|0413|NLD|  
|French|040c|FRA|  
|German|0407|DEU|  
|Hungarian|040e|HUN|  
|Italian - Italy|0410|ITA|  
|Japanese|0411|JPN|  
|Korean|0412|KOR|  
|Polish|0415|PLK|  
|Portuguese - Brazil|0416|PTB|  
|Portuguese - Portugal|0816|PTG|  
|Russian|0419|RUS|  
|Spanish - Spain|0c0a|ESN|  
|Swedish|041d|SVE|  
|Turkish|041f|TRK|  

## Client languages

Use the following table to map a locale ID to a language that you want to support on client computers. For more information about locale IDs, see [Locale IDs assigned by Microsoft](/openspecs/windows_protocols/ms-lcid/a9eac961-e77d-41a6-90a5-ce1a8b0cdb9c).

|Client language|Locale ID (LCID)|Three-letter code|  
|---------------------|------------------------|-----------------------|  
|English (default)|0409|ENG|  
|Chinese -Simplified|0804|CHS|  
|Chinese (Traditional, Taiwan)|0404|CHT|  
|Czech|0405|CSY|  
|Danish|0406|DAN|  
|Dutch - Netherlands|0413|NLD|  
|Finnish|040b|FIN|  
|French|040c|FRA|  
|German|0407|DEU|  
|Greek|0408|ELL|  
|Hungarian|040e|HUN|  
|Italian - Italy|0410|ITA|  
|Japanese|0411|JPN|  
|Korean|0412|KOR|  
|Norwegian|0414|NOR|  
|Polish|0415|PLK|  
|Portuguese (Brazil)|0416|PTB|  
|Portuguese (Portugal)|0816|PTG|  
|Russian|0419|RUS|  
|Spanish - Spain|0c0a|ESN|  
|Swedish|041d|SVE|  
|Turkish|041f|TRK|  

### Mobile device client languages

When you add support for mobile device languages, all supported mobile device client languages are included. You can't select individual language packs for mobile device support.

## Identify installed language packs

To identify the language packs that are installed on a computer that runs the Configuration Manager client, look for the locale ID (LCID) of the installed language packs in the computer's registry. This information is available at the following registry path:  

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCMSetup\InstalledLangs`  

Customize hardware inventory to collect this information. Then build a custom report to view the language details. For more information about collecting custom hardware inventory, see [How to configure hardware inventory](../../../clients/manage/inventory/configure-hardware-inventory.md). For more information, see [Create reports](../../manage/operations-and-maintenance-for-reporting.md#create-reports).
