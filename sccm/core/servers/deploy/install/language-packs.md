---
title: "Language packs"
description: "Learn about the language support available in System Center Configuration Manager."
ms.custom: na
ms.date: 1/3/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cd74e5f5-33f6-4566-8c9d-d6a93bfe71ed
caps.latest.revision: 10
author: Brenduns
ms.author: brenduns
manager: angrobe

---
# Language packs in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

This topic provides technical details about language support in System Center Configuration Manager.  

## <a name="BKMK_SupLanguagePacks"></a> Supported operating system languages  
 You can install support for the display languages in the following tables by installing **server language packs** or **client language packs** at a central administration site and at primary sites. You select the server and client languages to support at a site from the available language pack files during the site installation process.

 Language pack files are downloaded when you run Setup as part of the prerequisites and redistributable file download. You also can use [Setup Downloader](setup-downloader.md) to download these files before you run Setup.   

 Use the following table to map a locale ID to a language that you want to support on servers or client computers. For more information about locale IDs, see [Locale IDs assigned by Microsoft](http://go.microsoft.com/fwlink/p/?LinkId=252609).  

### Server languages  

|Server language|Locale ID (LCID)|Three-letter code|  
|---------------------|------------------------|-----------------------|  
|English (default)|0409|ENU|  
|Chinese (Traditional, Hong Kong SAR)|0c04|ZHH|  
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

### Client languages  

|Client language|Locale ID (LCID)|Three-letter code|  
|---------------------|------------------------|-----------------------|  
|English (default)|0409|ENG|  
|Chinese (Traditional, Hong Kong SAR)|0c04|ZHH|  
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
 When you add support for mobile device languages, all supported mobile device client languages are included. You cannot select individual language packs for mobile device support.  

### Identify installed language packs  
To identify the language packs that are installed on a computer that runs the Configuration Manager client, look for the locale ID (LCID) of the installed language packs in the computer's registry. This information is available at:

 **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCMSetup\InstalledLangs**  

You can use hardware inventory to collect this information, and then build a custom report to view the language details. For information about collecting custom hardware inventory, see [How to configure hardware inventory in System Center Configuration Manager](../../../../core/clients/manage/inventory/configure-hardware-inventory.md). For information about creating reports, see the [Manage Configuration Manager reports](../../../../core/servers/manage/operations-and-maintenance-for-reporting.md#BKMK_ManageReports) section in the [Operations and maintenance for reporting in System Center Configuration Manager](../../../../core/servers/manage/operations-and-maintenance-for-reporting.md) topic.  
