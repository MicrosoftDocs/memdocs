---
# required metadata

title: List of settings for the Microsoft 365 Apps for Enterprise security baseline in Intune
titleSuffix: Microsoft Intune
description: View a list of the settings in the Microsoft Intune security baseline for Microsoft Office apps. This list includes the default values for settings as found in the default configuration of the baseline.
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 09/13/2024
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.assetid:

# optional metadata
#ROBOTS:
#audience:

ms.reviewer: juidaewo
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier2
- M365-identity-device-management
- sub-secure-endpoints
zone_pivot_groups: m365-app-baseline-versions
---

<!-- Add when pivots are needed:
 
Metadata:
zone_pivot_groups: m365-app-baseline-versions

Pivot yml: 
- id: m365-app-baseline-versions
  title: M365 App baseline versions
  prompt: Choose a version
  pivots:
    - id: v2306
      title: Version 2306
    - id: office-may-2023
      title: May 2023
-->

# Microsoft 365 Apps for Enterprise security baseline settings reference for Microsoft Intune

This article is a reference for the settings that are available in the Microsoft 365 Apps for Enterprise security baseline for Microsoft Intune.

## About this reference article

Each security baseline is a group of preconfigured settings that help you apply and enforce granular security settings that the relevant security teams recommend. You can also customize each baseline you deploy to enforce only those settings and values you require. When you create a security baseline profile in Intune, you're creating a template that consists of multiple device configuration profiles.

The details that are displayed in this article are based on baseline version that is selected at the top of the article. For each selection, this article displays:

- A list of each setting in that baseline version.
- The default configuration of each setting in that baseline version.
- When available, a link to the underlying configuration service provider (CSP) documentation, or other related content from the relevant product group that provides context and possibly additional details for the settings use.

When a new version of a baseline becomes available, it replaces the previous version. Profile instances that you’ve created prior to the availability of a new version:

- Become read-only. You can continue to use those profiles but can't edit them to change their configuration.
- Can be updated to the latest version. After you update a profile to the current baseline version, you can edit the profile to modify settings.

To learn more about using security baselines, see:

- [Use security baselines](../protect/security-baselines.md)
- [Manage security baselines](../protect/security-baselines-configure.md).

::: zone pivot="office-may-2023"

**Microsoft 365 Apps for Enterprise security baseline for May 2023**

This baseline version was first made available in May of 2023. It was replaced by the Baseline *Version 2306*

For more information about the following settings that are included in this baseline, download the [Microsoft Security Compliance Toolkit 1.0](https://www.microsoft.com/download/details.aspx?id=55319) from the Microsoft Download Center, and review the *Microsoft 365 Apps for Enterprise-2206-FINAL.zip* file.

::: zone-end
::: zone pivot="v2306"

**Microsoft 365 Apps for Enterprise for security baseline version 2306**

This baseline version was first made available in November 2023, and replaces the *May 2023* version.

For more information about the following settings that are included in this baseline, download the [Security Compliance Toolkit and Baselines](https://www.microsoft.com/download/details.aspx?id=55319) from the Microsoft Download Center, and then review the *Microsoft 365 Apps for Enterprise 2306.zip* file.

::: zone-end
::: zone pivot="office-may-2023,v2306"

## Administrative Templates

*MS Security Guide*

- **Block Flash activation in Office documents**  
  Baseline default: *Enabled*  
  - **Block Flash player in Office (Device)**  
    Baseline default: Block all activation*

- **Restrict legacy JScript execution for Office**  
  Baseline default: *Enabled*

  - **Excel: (Device)**  
    Baseline default: *69632*

  - **PowerPoint: (Device)**  
    Baseline default: *69632*

  - **OneNote: (Device)**  
    Baseline default: *69632*

  - **Publisher: (Device)**  
    Baseline default: *69632*

  - **Access: (Device)**  
    Baseline default: *69632*

  - **Project: (Device)**  
    Baseline default: *69632*
  
  - **Visio: (Device)**  
    Baseline default: *69632*

  - **Outlook: (Device)**  
    Baseline default: *69632*


  - **Word: (Device)**  
    Baseline default: *69632*



## Microsoft Access 2016

*Application Settings > Security > Trust Center*

- **Block macros from running in Office files from the Internet (User)**  
  Baseline default: *Enabled*

- **Disable Trust Bar Notification for unsigned application add-ins and block them (User)**  
  Baseline default: *Enabled*

::: zone-end
::: zone pivot="v2306"
<!-- v.2306 only -->

- **Require that application add-ins are signed by Trusted Publisher (User)**  
  Baseline default: *Enabled*

::: zone-end
::: zone pivot="office-may-2023,v2306"

- **VBA Macro Notification Settings (User)**  
  Baseline default: *Enabled*  
  - Baseline default: *Disable all with notification*

*Application Settings > Security > Trust Center > Trusted Locations*

- **Allow Trusted Locations on the network (User)**  
  Baseline default: *Disabled*

### Microsoft Excel 2016

*Data Recovery*

- **Do not show data extraction options when opening corrupt workbooks (User)**  
  Baseline default: *Enabled*

*Excel Options > Advanced*

- **Ask to update automatic links (User)**  
  Baseline default: *Enabled*

*Excel Options > Advanced > General*

- **Load pictures from Web pages not created in Excel (User)**  
  Baseline default: *Disabled*

*Excel Options > Save*

- **Disable AutoRepublish (User)**  
  Baseline default: *Enabled*

- **Do not show AutoRepublish warning alert (User)**  
  Baseline default: *Disabled*

*Excel Options > Security*

- **Force file extension to match file type (User)**  
  Baseline default: *Enabled*  
  - Baseline default: *Always match file type*

- **Scan encrypted macros in Excel Open XML workbooks (User)**  
  Baseline default: *Enabled*  
  - Baseline default: *Scan encrypted macros (default)*

- **Turn off file validation (User)**  
  Baseline default: *Disabled*

- **WEBSERVICE Function Notification Settings (User)**  
  Baseline default: *Enabled*  
  - Baseline default: *Disable all with notification*

*Excel Options > Security > Trust Center*

::: zone-end
::: zone pivot="v2306"
<!-- v.2306 only -->

- **Block Excel XLL Add-ins that come from an untrusted source (User)**  
  Baseline default: *Enabled*
  - Baseline default: *Block*

::: zone-end
::: zone pivot="office-may-2023,v2306"

- **Block macros from running in Office files from the Internet (User)**  
  Baseline default: *Enabled*

::: zone-end
::: zone pivot="v2306"
- **Disable Trust Bar Notification for unsigned application add-ins and block them (User) (Deprecated)**  
  Baseline default: *Enabled*

::: zone-end
::: zone pivot="office-may-2023,v2306"

- **Prevent Excel from running XLM macros (User)**  
  Baseline default: *Enabled*

- **Require that application add-ins are signed by Trusted Publisher (User)**  
  Baseline default: *Enabled*  
  - **Disable Trust Bar Notification for unsigned application add-ins and block them (User)**  
  Baseline default: *Enabled*

- **VBA Macro Notification Settings (User)**  
  Baseline default: *Enabled*  
  - Baseline default: *Disable all except digitally signed macros*

*Excel Options > Security > Trust Center > External Content*

- **Always prevent untrusted Microsoft Query files from opening (User)**  
  Baseline default: *Enabled*

::: zone-end
::: zone pivot="office-may-2023"
<!-- May 2023: only -->

- **Don’t allow Dynamic Data Exchange (DDE) server launch in Excel (User)**  
  Baseline default: *Enabled*

- **Don’t allow Dynamic Data Exchange (DDE) server lookup in Excel (User)**  
  Baseline default: *Enabled*

::: zone-end
::: zone pivot="office-may-2023,v2306"

*Excel Options > Security > Trust Center > File Block Settings*

- **dBase III / IV files (User)**  
  Baseline default: *Enabled*  
  - **File block setting: (User)**  
    Baseline default: *Open/Save blocked, use open policy*

- **Dif and Sylk files (User)**  
  Baseline default: *Enabled*  
  - **File block setting: (User)**  
    Baseline default: *Open/Save blocked, use open policy*

- **Excel 2 macrosheets and add-in files (User)**  
  Baseline default: *Enabled*  
  - **File block setting: (User)**  
    Baseline default: *Open/Save blocked, use open policy*

- **Excel 2 worksheets (User)**  
  Baseline default: *Enabled*  
  - **File block setting: (User)**  
    Baseline default: *Open/Save blocked, use open policy*

- **Excel 3 macrosheets and add-in files (User)**  
  Baseline default: *Enabled*  
  - **File block setting: (User)**  
    Baseline default: *Open/Save blocked, use open policy*

- **Excel 3 worksheets (User)**  
  Baseline default: *Enabled*  
  - **File block setting: (User)**  
    Baseline default: *Open/Save blocked, use open policy*

- **Excel 4 macrosheets and add-in files (User)**  
  Baseline default: *Enabled*  
  - **File block setting: (User)**  
    Baseline default: *Open/Save blocked, use open policy*

- **Excel 4 workbooks (User)**  
  Baseline default: *Enabled*  
  - **File block setting: (User)**  
    Baseline default: *Open/Save blocked, use open policy*

- **Excel 4 worksheets (User)**  
  Baseline default: *Enabled*  
  - **File block setting: (User)**  
    Baseline default: *Open/Save blocked, use open policy*

- **Excel 95 workbooks (User)**  
  Baseline default: *Enabled*  
  - **File block setting: (User)**  
    Baseline default: *Open/Save blocked, use open policy*

- **Excel 95-97 workbooks and templates (User)**  
  Baseline default: *Enabled*  
  - **File block setting: (User)**  
    Baseline default: *Open/Save blocked, use open policy*

- **Excel 97-2003 workbooks and templates (User)**  
  Baseline default: *Enabled*  
  - **File block setting: (User)**  
    Baseline default: *Open/Save blocked, use open policy*

- **Set default file block behavior (User)**  
  Baseline default: *Enabled*  
  - Baseline default: *Blocked files are not opened*

- **Web pages and Excel 2003 XML spreadsheets (User)**  
  Baseline default: *Enabled*  
  - **File block setting: (User)**  
    Baseline default: *Open/Save blocked, use open policy*

*Excel Options > Security > Trust Center > Protected View*

- **Always open untrusted database files in Protected View (User)**  
  Baseline default: *Enabled*

- **Do not open files from the Internet zone in Protected View (User)**  
  Baseline default: *Disabled*

- **Do not open files in unsafe locations in Protected View (User)**  
  Baseline default: *Disabled*

- **Set document behavior if file validation fails (User)**  
  Baseline default: *Enabled*  
  - **Checked: Allow edit. Unchecked: Do not allow edit. (User)**  
    Baseline default: *False*  
    - Baseline default: *Open in Protected View*

- **Turn off Protected View for attachments opened from Outlook (User)**  
  Baseline default: *Disabled*

*Excel Options > Security > Trust Center > Trusted Locations*

- **Allow Trusted Locations on the network (User)**  
  Baseline default: *Disabled*

## Microsoft Lync Feature Policies

- **Configure SIP security mode**  
  Baseline default: *Enabled*

- **Disable HTTP fallback for SIP connection**  
  Baseline default: *Enabled*

## Microsoft Office 2016

*Customize*

- **Disable UI extending from documents and templates (User)**  
  Baseline default: *Enabled*

  - **Disallow in PowerPoint (User)**  
    Baseline default: *True*

  - **Disallow in Publisher (User)**  
    Baseline default: *True*

  - **Disallow in Outlook (User)**  
    Baseline default: *True*

  - **Disallow in Project (User)**  
    Baseline default: *True*

  - **Disallow in Access (User)**  
    Baseline default: *True*

  - **Disallow in InfoPath (User)**  
    Baseline default: *True*

  - **Disallow in Word (User)**  
    Baseline default: *True*

  - **Disallow in Excel (User)**  
    Baseline default: *True*

  - **Disallow in Visio (User)**  
    Baseline default: *True*

*Security Settings*

- **ActiveX Control Initialization (User)**  
  Baseline default: *Enabled*  
  -**ActiveX Control Initialization: (User)**  
  Baseline default: *6*

::: zone-end
::: zone pivot="v2306"
<!-- v.2306 only -->

- **Allow Basic Authentication prompts from network proxies (User)**  
  Baseline default: *Disabled*

::: zone-end
::: zone pivot="office-may-2023,v2306"

- **Allow VBA to load typelib references by path from untrusted intranet locations (User)**  
  Baseline default: *Disabled*

- **Automation Security (User)**  
  Baseline default: *Enabled*  
  - **Set the Automation Security level (User)**  
  Baseline default: *Use application macro security level*

- **Control how Office handles form-based sign-in prompts (User)**  
  Baseline default: *Enabled*  
  - **Specify hosts allowed to show form-based sign-in prompts to users: (User)**  
    Baseline default: *;*  
  - **Behavior: (User)**  
    Baseline default: *Block all prompts*

- **Disable additional security checks on VBA library references that may refer to unsafe locations on the local machine (User)**  
  Baseline default: *Disabled*

- **Disable all Trust Bar notifications for security issues (User)**  
  Baseline default: *Disabled*

::: zone-end
::: zone pivot="v2306"
<!-- V.2306: only  -->

- **Encryption mode for Information Rights Management (IRM) (User)**  
  Baseline default: *Enabled*  
  - **IRM Encryption Mode: (User)**  
    Baseline default: *Cipher Block Chaining (CBC)*

::: zone-end
::: zone pivot="office-may-2023,v2306"

- **Encryption type for password protected Office 97-2003 files (User)**  
  Baseline default: *Enabled*  
  - **Encryption type: (User)**  
    Baseline default: *Microsoft Enhanced RSA and AES Cryptographic Provider,AES 256,256*

- **Encryption type for password protected Office Open XML files (User)**  
  Baseline default: *Enabled*  
  - **Encryption type: (User)**  
    Baseline default: *Microsoft Enhanced RSA and AES Cryptographic Provider,AES 256,256*

- **Load Controls in Forms3 (User)**  
  Baseline default: *Enabled*  
  - **Load Controls in Forms3: (User)**  
    Baseline default: *1*

- **Macro Runtime Scan Scope (User)**  
  Baseline default: *Enabled*  
  - Baseline default: *Enable for all documents*

- **Protect document metadata for rights managed Office Open XML Files (User)**  
  Baseline default: *Enabled*

*Security Settings > Trust Center*

- **Allow mix of policy and user locations (User)**  
  Baseline default: *Disabled*

*Server Settings*

- **Disable the Office client from polling the SharePoint Server for published links (User)**  
  Baseline default: *Enabled*

*Smart Documents (Word, Excel)*

- **Disable Smart Document's use of manifests (User)**  
  Baseline default: *Enabled*

## Microsoft Office 2016 (Machine)

*Security Settings > IE Security*

- **Add-on Management**  
  Baseline default: *Enabled*

  - **mspub.exe (Device)**  
    Baseline default: *True*

  - **mse7.exe (Device)**  
    Baseline default: *True*

  - **msaccess.exe (Device)**  
    Baseline default: *True*

  - **powerpnt.exe (Device)**  
    Baseline default: *True*

  - **excel.exe (Device)**  
    Baseline default: *True*

  - **visio.exe (Device)**  
    Baseline default: *True*

  - **onent.exe (Device)**  
    Baseline default: *True*

  - **outlook.exe (Device)**  
    Baseline default: *True*

  - **pptview.exe (Device)**  
    Baseline default: *True*

  - **winword.exe (Device)**  
    Baseline default: *True*

  - **exprwd.exe (Device)**  
    Baseline default: *True*

  - **spDesign.exe (Device)**  
    Baseline default: *True*

  - **winproj.exe (Device)**  
    Baseline default: *True*

  - **groove.exe (Device)**  
    Baseline default: *True*

- **Consistent Mime Handling**  
  Baseline default: *Enabled*

  - **exprwd.exe (Device)**  
    Baseline default: *True*

  - **excel.exe (Device)**  
    Baseline default: *True*

  - **spDesign.exe (Device)**  
    Baseline default: *True*

  - **onent.exe (Device)**  
    Baseline default: *True*  

  - **outlook.exe (Device)**  
    Baseline default: *True*

  - **pptview.exe (Device)**  
    Baseline default: *True*

  - **mspub.exe (Device)**  
    Baseline default: *True*

  - **visio.exe (Device)**  
    Baseline default: *True*

  - **winproj.exe (Device)**  
    Baseline default: *True*

  - **msaccess.exe (Device)**  
    Baseline default: *True*

  - **powerpnt.exe (Device)**  
    Baseline default: *True*
  
  - **groove.exe (Device)**  
    Baseline default: *True*

  - **mse7.exe (Device)**  
    Baseline default: *True*

  - **winword.exe (Device)**  
    Baseline default: *True*

- **Disable user name and password**  
  Baseline default: *Enabled*

  - **excel.exe (Device)**  
    Baseline default: *True*
 
  - **groove.exe (Device)**  
    Baseline default: *True*

  - **onent.exe (Device)**  
    Baseline default: *True*

  - **mse7.exe (Device)**  
    Baseline default: *True*

  - **mspub.exe (Device)**  
    Baseline default: *True*

  - **visio.exe (Device)**  
    Baseline default: *True*

  - **exprwd.exe (Device)**  
    Baseline default: *True*

  - **msaccess.exe (Device)**  
    Baseline default: *True*

  - **spDesign.exe (Device)**  
    Baseline default: *True*

  - **winword.exe (Device)**  
    Baseline default: *True*

  - **powerpnt.exe (Device)**  
    Baseline default: *True*

  - **outlook.exe (Device)**  
    Baseline default: *True*

  - **winproj.exe (Device)**  
    Baseline default: *True*

  - **pptview.exe (Device)**  
    Baseline default: *True*

- **Information Bar**  
  Baseline default: *Enabled*

  - **pptview.exe (Device)**  
    Baseline default: *True*

  - **excel.exe (Device)**  
    Baseline default: *True*

  - **mspub.exe (Device)**  
    Baseline default: *True*

  - **msaccess.exe (Device)**  
    Baseline default: *True*

  - **onent.exe (Device)**  
    Baseline default: *True*

  - **outlook.exe (Device)**  
    Baseline default: *True*

  - **winproj.exe (Device)**  
    Baseline default: *True*

  - **powerpnt.exe (Device)**  
    Baseline default: *True*

  - **spDesign.exe (Device)**  
    Baseline default: *True*

  - **groove.exe (Device)**  
    Baseline default: *True*

  - **visio.exe (Device)**  
    Baseline default: *True*

  - **mse7.exe (Device)**  
    Baseline default: *True*

  - **winword.exe (Device)**  
    Baseline default: *True*

  - **exprwd.exe (Device)**  
    Baseline default: *True*

- **Local Machine Zone Lockdown Security**  
  Baseline default: *Enabled*

  - **mse7.exe (Device)**  
    Baseline default: *True*

  - **powerpnt.exe (Device)**  
    Baseline default: *True*

  - **mspub.exe (Device)**  
    Baseline default: *True*

  - **outlook.exe (Device)**  
    Baseline default: *True*

  - **pptview.exe (Device)**  
    Baseline default: *True*

  - **excel.exe (Device)**  
    Baseline default: *True*

  - **exprwd.exe (Device)**  
    Baseline default: *True*

  - **groove.exe (Device)**  
    Baseline default: *True*

  - **winword.exe (Device)**  
    Baseline default: *True*

  - **msaccess.exe (Device)**  
    Baseline default: *True*

  - **spDesign.exe (Device)**  
    Baseline default: *True*

  - **visio.exe (Device)**  
    Baseline default: *True*

  - **onent.exe (Device)**  
    Baseline default: *True*

  - **winproj.exe (Device)**  
    Baseline default: *True*

- **Mime Sniffing Safety Feature**  
  Baseline default: *Enabled*

  - **onent.exe (Device)**  
    Baseline default: *True*

  - **winword.exe (Device)**  
    Baseline default: *True*

  - **excel.exe (Device)**  
    Baseline default: *True*

  - **powerpnt.exe (Device)**  
    Baseline default: *True*

  - **exprwd.exe (Device)**  
    Baseline default: *True*

  - **groove.exe (Device)**  
    Baseline default: *True*

  - **visio.exe (Device)**  
    Baseline default: *True*

  - **outlook.exe (Device)**  
    Baseline default: *True*

  - **mspub.exe (Device)**  
    Baseline default: *True*

  - **mse7.exe (Device)**  
    Baseline default: *True*

  - **msaccess.exe (Device)**  
    Baseline default: *True*

  - **pptview.exe (Device)**  
    Baseline default: *True*

  - **winproj.exe (Device)**  
    Baseline default: *True*

  - **spDesign.exe (Device)**  
    Baseline default: *True*

- **Navigate URL**  
  Baseline default: *Enabled*

  - **groove.exe (Device)**  
    Baseline default: *True*

  - **spDesign.exe (Device)**  
    Baseline default: *True*

  - **onent.exe (Device)**  
    Baseline default: *True*

  - **pptview.exe (Device)**  
    Baseline default: *True*

  - **outlook.exe (Device)**  
    Baseline default: *True*

  - **winproj.exe (Device)**  
    Baseline default: *True*

  - **msaccess.exe (Device)**  
    Baseline default: *True*

  - **winword.exe (Device)**  
    Baseline default: *True*

  - **excel.exe (Device)**  
    Baseline default: *True*

  - **mspub.exe (Device)**  
    Baseline default: *True*

  - **exprwd.exe (Device)**  
    Baseline default: *True*

  - **powerpnt.exe (Device)**  
    Baseline default: *True*

  - **visio.exe (Device)**  
    Baseline default: *True*

  - **mse7.exe (Device)**  
    Baseline default: *True*

- **Object Caching Protection**  
  Baseline default: *Enabled*

  - **winword.exe (Device)**  
    Baseline default: *True*

  - **powerpnt.exe (Device)**  
    Baseline default: *True*

  - **spDesign.exe (Device)**  
    Baseline default: *True*
 
  - **mse7.exe (Device)**  
    Baseline default: *True*

  - **mspub.exe (Device)**  
    Baseline default: *True*

  - **msaccess.exe (Device)**  
    Baseline default: *True*

  - **onent.exe (Device)**  
    Baseline default: *True*

  - **outlook.exe (Device)**  
    Baseline default: *True*

  - **groove.exe (Device)**  
    Baseline default: *True*

 - **excel.exe (Device)**  
    Baseline default: *True*

  - **visio.exe (Device)**  
    Baseline default: *True*

  - **pptview.exe (Device)**  
    Baseline default: *True*

  - **winproj.exe (Device)**  
    Baseline default: *True*

  - **exprwd.exe (Device)**  
    Baseline default: *True*

- **Protection From Zone Elevation**  
  Baseline default: *Enabled*

  - **winproj.exe (Device)**  
    Baseline default: *True*

  - **groove.exe (Device)**  
    Baseline default: *True*

  - **outlook.exe (Device)**  
    Baseline default: *True*

  - **mspub.exe (Device)**  
    Baseline default: *True*

  - **visio.exe (Device)**  
    Baseline default: *True*

  - **powerpnt.exe (Device)**  
    Baseline default: *True*

  - **excel.exe (Device)**  
    Baseline default: *True*

  - **mse7.exe (Device)**  
    Baseline default: *True*

  - **winword.exe (Device)**  
    Baseline default: *True*

  - **exprwd.exe (Device)**  
    Baseline default: *True*

  - **msaccess.exe (Device)**  
    Baseline default: *True*

  - **spDesign.exe (Device)**  
    Baseline default: *True*

  - **onent.exe (Device)**  
    Baseline default: *True*

  - **pptview.exe (Device)**  
    Baseline default: *True*

- **Restrict ActiveX Install**  
  Baseline default: *Enabled*

  - **mse7.exe (Device)**  
    Baseline default: *True*

  - **powerpnt.exe (Device)**  
    Baseline default: *True*

  - **spDesign.exe (Device)**  
    Baseline default: *True*

  - **onent.exe (Device)**  
    Baseline default: *True*

  - **excel.exe (Device)**  
    Baseline default: *True*

  - **mspub.exe (Device)**  
    Baseline default: *True*

  - **visio.exe (Device)**  
    Baseline default: *True*

  - **exprwd.exe (Device)**  
    Baseline default: *True*

  - **outlook.exe (Device)**  
    Baseline default: *True*

  - **pptview.exe (Device)**  
    Baseline default: *True*

  - **winproj.exe (Device)**  
    Baseline default: *True*

  - **winword.exe (Device)**  
    Baseline default: *True*

  - **groove.exe (Device)**  
    Baseline default: *True*

  - **msaccess.exe (Device)**  
    Baseline default: *True*

- **Restrict File Download**  
  Baseline default: *Enabled*
  
  - **onent.exe (Device)**  
    Baseline default: *True*

  - **mse7.exe (Device)**  
    Baseline default: *True*

  - **groove.exe (Device)**  
    Baseline default: *True*

  - **visio.exe (Device)**  
    Baseline default: *True*

  - **winproj.exe (Device)**  
    Baseline default: *True*

  - **msaccess.exe (Device)**  
    Baseline default: *True*

  - **spDesign.exe (Device)**  
    Baseline default: *True*

  - **excel.exe (Device)**  
    Baseline default: *True*

  - **powerpnt.exe (Device)**  
    Baseline default: *True*

  - **mspub.exe (Device)**  
    Baseline default: *True*

  - **exprwd.exe (Device)**  
    Baseline default: *True*

  - **outlook.exe (Device)**  
    Baseline default: *True*

  - **pptview.exe (Device)**  
    Baseline default: *True*

  - **winword.exe (Device)**  
    Baseline default: *True*

- **Saved from URL**  
  Baseline default: *Enabled*

  - **mspub.exe (Device)**  
    Baseline default: *True*

  - **visio.exe (Device)**  
    Baseline default: *True*

  - **winword.exe (Device)**  
    Baseline default: *True*

  - **msaccess.exe (Device)**  
    Baseline default: *True*

  - **onent.exe (Device)**  
    Baseline default: *True*

  - **outlook.exe (Device)**  
    Baseline default: *True*

  - **groove.exe (Device)**  
    Baseline default: *True*

  - **excel.exe (Device)**  
    Baseline default: *True*

  - **powerpnt.exe (Device)**  
    Baseline default: *True*

  - **pptview.exe (Device)**  
    Baseline default: *True*

  - **exprwd.exe (Device)**  
    Baseline default: *True*

  - **mse7.exe (Device)**  
    Baseline default: *True*

  - **spDesign.exe (Device)**  
    Baseline default: *True*

  - **winproj.exe (Device)**  
    Baseline default: *True*

- **Scripted Window Security Restrictions**  
  Baseline default: *Enabled*

  - **visio.exe (Device)**  
    Baseline default: *True*

  - **onent.exe (Device)**  
    Baseline default: *True*

  - **winproj.exe (Device)**  
    Baseline default: *True*

  - **winword.exe (Device)**  
    Baseline default: *True*

  - **exprwd.exe (Device)**  
    Baseline default: *True*

  - **mse7.exe (Device)**  
    Baseline default: *True*

  - **mspub.exe (Device)**  
    Baseline default: *True*

  - **outlook.exe (Device)**  
    Baseline default: *True*

  - **msaccess.exe (Device)**  
    Baseline default: *True*

  - **powerpnt.exe (Device)**  
    Baseline default: *True*

  - **groove.exe (Device)**  
    Baseline default: *True*

  - **excel.exe (Device)**  
    Baseline default: *True*

  - **pptview.exe (Device)**  
    Baseline default: *True*

  - **spDesign.exe (Device)**  
    Baseline default: *True*

## Microsoft Outlook 2016

*Security > Security Form Settings*

The "Outlook Security Mode" policy controls how security settings in Outlook are enforced. To manage any of the dependent Outlook security policies using Microsoft Intune, Office cloud policy service, or Group policy this policy must be enabled and the Outlook Security Policy dropdown set to "Use Outlook Security Group Policy".

- **Outlook Security Mode (User)**  
  Baseline default: *Enabled*  
  - **Outlook Security Policy: (User)**  
    Baseline default: *Use Outlook Security Group Policy*  
    - **Guard behavior: (User)**  
      Baseline default: *Automatically Deny*

  - **Prevent users from customizing attachment security settings (User)**  
    Baseline default: *Enabled*

  - **Retrieving CRLs (Certificate Revocation Lists) (User)**  
    Baseline default: *Enabled*  
    - Baseline default: *When online always retrieve the CRL*

::: zone-end
::: zone pivot="office-may-2023"
<!-- May 2023: only  -->

  - **Junk E-mail protection level (User)**  
    Baseline default: *Disabled*

::: zone-end
::: zone pivot="office-may-2023,v2306"

  - **Configure Outlook object model prompt When accessing the Formula property of a UserProperty object (User)**  
    Baseline default: *Enabled*  
    - **Guard behavior: (User)**  
      Baseline default: *Automatically Deny*

  - **Authentication with Exchange Server (User)**  
    Baseline default: *Enabled*  
    - **Select the authentication with Exchange server. (User)**  
      Baseline default: *Kerberos Password Authentication*

 - **Enable RPC encryption (User)**  
    Baseline default: *Enabled*

  - **Allow hyperlinks in suspected phishing e-mail messages (User)**  
    Baseline default: *Disabled*

  - **Configure Outlook object model prompt when reading address information (User)**  
    Baseline default: *Enabled*  
    - **Guard behavior: (User)**  
      Baseline default: *Automatically Deny*

  - **Configure Outlook object model prompt when sending mail (User)**  
    Baseline default: *Enabled*

  - **Allow users to demote attachments to Level 2 (User)**  
    Baseline default: *Disabled*

  - **Allow Active X One Off Forms (User)**  
    Baseline default: *Enabled*  
    - **Sets which ActiveX controls to allow.**  
      Baseline default: *Load only Outlook Controls*

  - **Allow scripts in one-off Outlook forms (User)**  
    Baseline default: *Disabled*

  - **Remove file extensions blocked as Level 2 (User)**  
    Baseline default: *Enabled*  
    - **Removed Extensions: (User)**  
      Baseline default: *;*

  - **Use Unicode format when dragging e-mail message to file system (User)**  
    Baseline default: *Disabled*  

  - **Set Outlook object model custom actions execution prompt (User)**  
    Baseline default: *Enabled*  
    - **When executing a custom action: (User)**  
      Baseline default: *Automatically Deny*

  - **Do not allow Outlook object model scripts to run for public folders (User)**  
    Baseline default: *Enabled*

  - **Include Internet in Safe Zones for Automatic Picture Download (User)**  
    Baseline default: *Disabled*

  - **Security setting for macros (User)**  
    Baseline default: *Enabled*  
    - **Security Level (User)**  
      Baseline default: *Warn for signed, disable unsigned*

  - **Remove file extensions blocked as Level 1 (User)**  
    Baseline default: *Enabled*  
    - **Removed Extensions: (User)**  
      Baseline default: *;*

  - **Signature Warning (User)**  
    Baseline default: *Enabled*  
    - **Signature Warning (User)**  
      Baseline default: *Always warn about invalid signatures*

- **Display Level 1 attachments (User)**  
  Baseline default: *Disabled*

- **Minimum encryption settings (User)**  
  Baseline default: *Enabled*
  - **Minimum key size (in bits): (User)**  
    Baseline default: *168*

- **Do not allow Outlook object model scripts to run for shared folders (User)**  
  Baseline default: *Enabled*

- **Configure Outlook object model prompt when executing Save As (User)**  
  Baseline default: *Enabled*
  - **Guard behavior: (User)**  
    Baseline default: *Automatically Deny*
  - **Configure Outlook object model prompt when reading address information (User)**  
    Baseline default: *Enabled*  
    - **Guard behavior: (User)**  
      Baseline default: *Automatically Deny*

- **Configure Outlook object model prompt when responding to meeting and task requests (User)**  
  Baseline default: *Enabled*
  - **Guard behavior: (User)  
    Baseline default: *Automatically Deny*

## Microsoft PowerPoint 2016

*PowerPoint Options > Security*

::: zone-end
::: zone pivot="v2306"
<!-- V.2306: only -->

- **Run Programs (User)**  
  Baseline default: *Disabled*  

::: zone-end
::: zone pivot="office-may-2023"
<!-- May 2023: only -->

- **Run Programs (User)**  
  Baseline default: *Enabled*  
  - *disable (don't run any programs)*

::: zone-end
::: zone pivot="office-may-2023,v2306"

- **Scan encrypted macros in PowerPoint Open XML presentations (User)**  
  Baseline default: *Enabled*  
  - Baseline default: *Scan encrypted macros (default)*

- **Turn off file validation (User)**  
  Baseline default: *Disabled*

*PowerPoint Options > Security > Trust Center*

- **Block macros from running in Office files from the Internet (User**)  
  Baseline default: *Enabled*

::: zone-end
::: zone pivot="v2306"
<!-- V.2306: only  -->

- **Disable Trust Bar Notification for unsigned application add-ins and block them (User) (Deprecated)**  
  Baseline default: *Enabled*

::: zone-end
::: zone pivot="office-may-2023,v2306"

- **Require that application add-ins are signed by Trusted Publisher (User)**  
  Baseline default: *Enabled*  
  - **Disable Trust Bar Notification for unsigned application add-ins and block them (User)**  
  Baseline default: *Enabled*

- **VBA Macro Notification Settings (User)**  
  Baseline default: *Enabled*  
  - Baseline default: *Disable all except digitally signed macros*

*PowerPoint Options > Security > Trust Center > File Block Settings*

- **PowerPoint 97-2003 presentations, shows, templates and add-in files (User)**  
  Baseline default: *Enabled*  
  - **File block setting: (User)**  
    Baseline default: *Open/Save blocked, use open policy*

- **Set default file block behavior (User)**  
  Baseline default: *Enabled*  
  - Baseline default: *Blocked files are not opened*

*PowerPoint Options > Security > Trust Center > Protected View*

- **Do not open files from the Internet zone in Protected View (User)**  
  Baseline default: *Disabled*

- **Do not open files in unsafe locations in Protected View (User)**  
  Baseline default: *Disabled*

- **Set document behavior if file validation fails (User)**  
  Baseline default: *Enabled* 
 
  - **Checked: Allow edit. Unchecked: Do not allow edit. (User)**  
    Baseline default: *False*
  - Baseline default: *Open in Protected View*  

- **Turn off Protected View for attachments opened from Outlook (User)**  
  Baseline default: *Disabled*

*PowerPoint Options > Security > Trust Center > Trusted Locations*

- **Allow Trusted Locations on the network (User)**  
  Baseline default: *Disabled*

## Microsoft Project 2016

*Project Options > Security > Trust Center*

- **Allow Trusted Locations on the network (User)**  
  Baseline default: *Disabled*

::: zone-end
::: zone pivot="v2306"
<!-- V.2306: only  -->

- **Disable Trust Bar Notification for unsigned application add-ins and block them (User) (Deprecated)**  
  Baseline default: *Enabled*

::: zone-end
::: zone pivot="office-may-2023,v2306"

- **Require that application add-ins are signed by Trusted Publisher (User)**  
  Baseline default: *Enabled*  
  - **Disable Trust Bar Notification for unsigned application add-ins and block them (User)**  
    Baseline default: *Enabled*

- **VBA Macro Notification Settings (User)**  
  Baseline default: *Enabled*  
  - Baseline default: *Disable all except digitally signed macros*

## Microsoft Publisher 2016

*Security*

- **Publisher Automation Security Level (User)**  
  Baseline default: *Enabled*  
  - Baseline default: *By UI (prompted)*

*Security > Trust Center*

::: zone-end
::: zone pivot="v2306"
<!-- V.2306: only  -->

- **Block macros from running in Office files from the internet (User)**
  Baseline default: *Enabled*

- **Disable Trust Bar Notification for unsigned application add-ins (User) (Deprecated)**  
  Baseline default: *Enabled*

::: zone-end
::: zone pivot="office-may-2023,v2306"

- **Require that application add-ins are signed by Trusted Publisher (User)**  
  Baseline default: *Enabled*

  - **Disable Trust Bar Notification for unsigned application add-ins (User)**  
  Baseline default: Enabled*

- **VBA Macro Notification Settings (User)**  
  Baseline default: *Enabled*  
  - Baseline default: *Disable all except digitally signed macros*

## Microsoft Visio 2016

*Visio Options > Security > Trust Center*

- **Allow Trusted Locations on the network (User)**  
  Baseline default: *Disabled*

- **Block macros from running in Office files from the Internet (User)**  
  Baseline default: *Enabled*


::: zone-end
::: zone pivot="v2306"
<!-- V.2306: only -->
- **Disable Trust Bar Notification for unsigned application add-ins and block them (User) (Deprecated)**  
  Baseline default: *Enabled*

::: zone-end
::: zone pivot="office-may-2023,v2306"

- **Require that application add-ins are signed by Trusted Publisher (User)**  
  Baseline default: *Enabled*  
  - **Disable Trust Bar Notification for unsigned application add-ins and block them (User)**  
    Baseline default: *Enabled*

- **VBA Macro Notification Settings (User)**  
  Baseline default: *Enabled*  
  - Baseline default: *Disable all except digitally signed macros*

*Visio Options > Security > Trust Center > File Block Settings*

- **Visio 2000-2002 Binary Drawings, Templates and Stencils (User)**  
  Baseline default: *Enabled*  
  - **File block setting: (User)**  
    Baseline default: *Open/Save blocked*

- **Visio 2003-2010 Binary Drawings, Templates and Stencils (User)**  
  Baseline default: *Enabled*  
  - **File block setting: (User)**  
    Baseline default: *Open/Save blocked*

- **Visio 5.0 or earlier Binary Drawings, Templates and Stencils (User)**  
  Baseline default: *Enabled*  
  - **File block setting: (User)**  
    Baseline default: *Open/Save blocked*

## Microsoft Word 2016

*Word Options > Security > Trust Center*

- **Block macros from running in Office files from the Internet (User)**  
  Baseline default: *Enabled*

::: zone-end
::: zone pivot="v2306"
<!-- V.2306: only  -->
- **Disable Trust Bar Notification for unsigned application add-ins and block them (User) (Deprecated)**  
  Baseline default: *Enabled*

::: zone-end
::: zone pivot="office-may-2023,v2306"

- **Dynamic Data Exchange (User)**  
  Baseline default: *Disabled*

- **Require that application add-ins are signed by Trusted Publisher (User)**  
  Baseline default: *Enabled*

  - **Disable Trust Bar Notification for unsigned application add-ins and block them (User)**  
  Baseline default: *Enabled*

- **Scan encrypted macros in Word Open XML documents (User)**  
  Baseline default: *Enabled*
  - Baseline default: *Scan encrypted macros (default)*

- **VBA Macro Notification Settings (User)**  
  Baseline default: *Enabled*
  - Baseline default: *Disable all except digitally signed macros*

*Word Options > Security > Trust Center > File Block Settings*

- **Set default file block behavior (User)**  
  Baseline default: *Enabled*
  - Baseline default: *Blocked files are not opened*

- **Word 2 and earlier binary documents and templates (User)**  
  Baseline default: *Enabled*
  - **File block setting: (User)**  
    Baseline default: *Open/Save blocked, use open policy*

- **Word 2000 binary documents and templates (User)**  
  Baseline default: *Enabled*
  - **File block setting: (User)**  
    Baseline default: *Open/Save blocked, use open policy*

- **Word 2003 binary documents and templates (User)**  
  Baseline default: *Enabled*
  - **File block setting: (User)**  
    Baseline default: *Open/Save blocked, use open policy*

- **Word 2007 and later binary documents and templates (User)**  
  Baseline default: *Enabled*
  - **File block setting: (User)**  
    Baseline default: *Open/Save blocked, use open policy*

- **Word 6.0 binary documents and templates (User)**  
  Baseline default: *Enabled*
  - **File block setting: (User)**  
    Baseline default: *Open/Save blocked, use open policy*

- **Word 95 binary documents and templates (User)**  
  Baseline default: *Enabled*
  - **File block setting: (User)**  
    Baseline default: *Open/Save blocked, use open policy*

- **Word 97 binary documents and templates (User)**  
  Baseline default: *Enabled*
  - **File block setting: (User)**  
    Baseline default: *Open/Save blocked, use open policy*

- **Word XP binary documents and templates (User)**  
  Baseline default: *Enabled*
  - **File block setting: (User)**  
    Baseline default: *Open/Save blocked, use open policy*

*Word Options > Security > Trust Center > Protected View*

- **Do not open files from the Internet zone in Protected View (User)**  
  Baseline default: *Disabled*

- **Do not open files in unsafe locations in Protected View (User)**  
  Baseline default: *Disabled*

- **Set document behavior if file validation fails (User)**  
  Baseline default: *Enabled*

  - Baseline default: *Open in Protected View*

  - **Checked: Allow edit. Unchecked: Do not allow edit. (User)**  
    Baseline default: *False*

- **Turn off Protected View for attachments opened from Outlook (User)**  
  Baseline default: *Disabled*

*Word Options > Security*

- **Turn off file validation (User)**  
  Baseline default: *Disabled*

*Word Options > Security > Trust Center > Trusted Locations*

- **Allow Trusted Locations on the network (User)**  
  Baseline default: *Disabled*

::: zone-end

## Next steps

- [Learn about security baselines](../protect/security-baselines.md)
- [Avoid conflicts](../protect/security-baselines.md#avoid-conflicts)
- [Troubleshoot policies and profiles in Intune](/troubleshoot/mem/intune/troubleshoot-policies-in-microsoft-intune)
