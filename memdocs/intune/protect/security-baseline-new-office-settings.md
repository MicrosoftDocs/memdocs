---
# required metadata

title: List of settings for the Microsoft 365 Apps for Enterprise security baseline in Intune
titleSuffix: Microsoft Intune
description: View a list of the settings in the Microsoft Intune security baseline for Microsoft Office apps. This list includes the default values for settings as found in the default configuration of the baseline.
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 05/24/2022
ms.topic: reference
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology:
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

---

<!-- Add when pivots are needed:
 
Metadata:
zone_pivot_groups: dcv2-office-baselines

Pivot yml: 
- id: dcv2-office-baselines
  title: Microsoft 365 Apps for Enterprise baseline versions
  prompt: Choose a version
  pivots:
    id: office-may2023
      title: May 2023
    id: office-future
      title: Future version
-->
# Microsoft  365 Apps for Enterprise security baseline settings reference for Microsoft Intune

This article is a reference for the settings that are available in the Microsoft 365 Apps for Enterprise security baseline for Microsoft Intune and applies to versions of that baseline that released in May 2023 or later.


## About this reference article

Each security baseline is a group of preconfigured Windows settings that help you apply and enforce granular security settings that the relevant security teams recommend. You can also customize each baseline you deploy to enforce only those settings and values you require. When you create a security baseline profile in Intune, you're creating a template that consists of multiple device configuration profiles.

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



## Microsoft 365 Apps for Enterprise

<!-- >::: zone pivot="office-may2023" -->

**Microsoft 365 Apps for Enterprise security baseline for May 2023**  

### Microsoft Access 2016

*Application Settings > Security > Trust Center*

- **Block macros from running in Office files from the Internet (User)**  
  Baseline default: *Enabled*  

- **VBA Macro Notification Settings (User)**  
  Baseline default: *Enabled*  

  - Baseline default: *Disable all with notification*
  
- **Disable Trust Bar Notification for unsigned application add-ins and block them (User)**  
  Baseline default: *Enabled*  

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
- **Block macros from running in Office files from the Internet (User)**  
  Baseline default: *Enabled*

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

- **Don’t allow Dynamic Data Exchange (DDE) server launch in Excel (User)**  
  Baseline default: *Enabled*

- **Don’t allow Dynamic Data Exchange (DDE) server lookup in Excel (User)**  
  Baseline default: *Enabled*

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
  
    Baseline default: *Open in Protected View*

- **Turn off Protected View for attachments opened from Outlook (User)**  
  Baseline default: *Disabled*

*Excel Options > Security > Trust Center > Trusted Locations*

- **Allow Trusted Locations on the network (User)**  
  Baseline default: *Disabled*

### Microsoft Lync Feature Policies

- **Configure SIP security mode**
  Baseline default: *Enabled*

- **Disable HTTP fallback for SIP connection**
  Baseline default: *Enabled*

### Microsoft Office 2016

*Customize*

- **Disable UI extending from documents and templates (User)**  
  Baseline default: *Enabled*

  - **Disallow in PowerPoint (User)**  
    Baseline default: *True*

  - **Disallow in Publisher (User)**  
    Baseline default: *True*

  - **Disallow in Visio (User)**  
    Baseline default: *True*

  - **Disallow in InfoPath (User)**  
    Baseline default: *True*

  - **Disallow in Outlook (User)**  
    Baseline default: *True*

  - **Disallow in Project (User)**  
    Baseline default: *True*

  - **Disallow in Access (User)**  
    Baseline default: *True*

  - **Disallow in Word (User)**  
    Baseline default: *True*

  - **Disallow in Excel (User)**  
    Baseline default: *True*

*Security Settings*

- **ActiveX Control Initialization (User)**  
  Baseline default: *Enabled*

  -**ActiveX Control Initialization: (User)**  
  Baseline default: *6*

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

### Microsoft Office 2016 (Machine)

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

  - **visio.exe (Device)**  
    Baseline default: *True*

  - **outlook.exe (Device)**  
    Baseline default: *True*

  - **pptview.exe (Device)**  
    Baseline default: *True*

  - **winword.exe (Device)**  
    Baseline default: *True*

  - **excel.exe (Device)**  
    Baseline default: *True*

  - **onent.exe (Device)**  
    Baseline default: *True*

  - **winproj.exe (Device)**  
    Baseline default: *True*

  - **exprwd.exe (Device)**  
    Baseline default: *True*

  - **spDesign.exe (Device)**  
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

  - **outlook.exe (Device)**  
    Baseline default: *True*

  - **mspub.exe (Device)**  
    Baseline default: *True*

  - **visio.exe (Device)**  
    Baseline default: *True*

  - **onent.exe (Device)**  
    Baseline default: *True*  

  - **pptview.exe (Device)**  
    Baseline default: *True*

  - **winproj.exe (Device)**  
    Baseline default: *True*

  - **powerpnt.exe (Device)**  
    Baseline default: *True*

  - **mse7.exe (Device)**  
    Baseline default: *True*

  - **msaccess.exe (Device)**  
    Baseline default: *True*

  - **groove.exe (Device)**  
    Baseline default: *True*

  - **winword.exe (Device)**  
    Baseline default: *True*

- **Disable user name and password**  
  Baseline default: *Enabled*

  - **pptview.exe (Device)**  
    Baseline default: *True*

  - **groove.exe (Device)**  
    Baseline default: *True*

  - **onent.exe (Device)**  
    Baseline default: *True*

  - **mse7.exe (Device)**  
    Baseline default: *True*

  - **excel.exe (Device)**  
    Baseline default: *True*

  - **visio.exe (Device)**  
    Baseline default: *True*

  - **exprwd.exe (Device)**  
    Baseline default: *True*

  - **spDesign.exe (Device)**  
    Baseline default: *True*

  - **winword.exe (Device)**  
    Baseline default: *True*

  - **mspub.exe (Device)**  
    Baseline default: *True*

  - **msaccess.exe (Device)**  
    Baseline default: *True*

  - **powerpnt.exe (Device)**  
    Baseline default: *True*

  - **outlook.exe (Device)**  
    Baseline default: *True*

  - **winproj.exe (Device)**  
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

  - **outlook.exe (Device)**  
    Baseline default: *True*

  - **winproj.exe (Device)**  
    Baseline default: *True*

  - **spDesign.exe (Device)**  
    Baseline default: *True*

  - **onent.exe (Device)**  
    Baseline default: *True*

  - **powerpnt.exe (Device)**  
    Baseline default: *True*

  - **winword.exe (Device)**  
    Baseline default: *True*

  - **exprwd.exe (Device)**  
    Baseline default: *True*

  - **groove.exe (Device)**  
    Baseline default: *True*

  - **visio.exe (Device)**  
    Baseline default: *True*

  - **mse7.exe (Device)**  
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

  - **visio.exe (Device)**  
    Baseline default: *True*

  - **winword.exe (Device)**  
    Baseline default: *True*

  - **msaccess.exe (Device)**  
    Baseline default: *True*

  - **spDesign.exe (Device)**  
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

  - **pptview.exe (Device)**  
    Baseline default: *True*

  - **mspub.exe (Device)**  
    Baseline default: *True*

  - **mse7.exe (Device)**  
    Baseline default: *True*

  - **msaccess.exe (Device)**  
    Baseline default: *True*

  - **spDesign.exe (Device)**  
    Baseline default: *True*

  - **winproj.exe (Device)**  
    Baseline default: *True*

- **Navigate URL**  
  Baseline default: *Enabled*

  - **powerpnt.exe (Device)**  
    Baseline default: *True*

  - **visio.exe (Device)**  
    Baseline default: *True*

  - **mse7.exe (Device)**  
    Baseline default: *True*

  - **groove.exe (Device)**  
    Baseline default: *True*

  - **onent.exe (Device)**  
    Baseline default: *True*

  - **pptview.exe (Device)**  
    Baseline default: *True*

  - **spDesign.exe (Device)**  
    Baseline default: *True*

  - **outlook.exe (Device)**  
    Baseline default: *True*

  - **winproj.exe (Device)**  
    Baseline default: *True*

  - **excel.exe (Device)**  
    Baseline default: *True*

  - **exprwd.exe (Device)**  
    Baseline default: *True*

  - **msaccess.exe (Device)**  
    Baseline default: *True*

  - **winword.exe (Device)**  
    Baseline default: *True*

  - **mspub.exe (Device)**  
    Baseline default: *True*

- **Object Caching Protection**  
  Baseline default: *Enabled*

  - **excel.exe (Device)**  
    Baseline default: *True*

  - **pptview.exe (Device)**  
    Baseline default: *True*

  - **winproj.exe (Device)**  
    Baseline default: *True*

  - **exprwd.exe (Device)**  
    Baseline default: *True*

  - **winword.exe (Device)**  
    Baseline default: *True*

  - **spDesign.exe (Device)**  
    Baseline default: *True*

  - **mse7.exe (Device)**  
    Baseline default: *True*

  - **mspub.exe (Device)**  
    Baseline default: *True*

  - **powerpnt.exe (Device)**  
    Baseline default: *True*

  - **onent.exe (Device)**  
    Baseline default: *True*

  - **outlook.exe (Device)**  
    Baseline default: *True*

  - **msaccess.exe (Device)**  
    Baseline default: *True*

  - **visio.exe (Device)**  
    Baseline default: *True*

  - **groove.exe (Device)**  
    Baseline default: *True*

- **Protection From Zone Elevation**  
  Baseline default: *Enabled*

  - **msaccess.exe (Device)**  
    Baseline default: *True*

  - **spDesign.exe (Device)**  
    Baseline default: *True*

  - **groove.exe (Device)**  
    Baseline default: *True*

  - **winproj.exe (Device)**  
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

  - **onent.exe (Device)**  
    Baseline default: *True*

  - **pptview.exe (Device)**  
    Baseline default: *True*

  - **exprwd.exe (Device)**  
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

  - **pptview.exe (Device)**  
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

  - **visio.exe (Device)**  
    Baseline default: *True*

  - **mspub.exe (Device)**  
    Baseline default: *True*

  - **outlook.exe (Device)**  
    Baseline default: *True*

  - **winword.exe (Device)**  
    Baseline default: *True*

  - **excel.exe (Device)**  
    Baseline default: *True*

  - **msaccess.exe (Device)**  
    Baseline default: *True*

  - **powerpnt.exe (Device)**  
    Baseline default: *True*

  - **onent.exe (Device)**  
    Baseline default: *True*

  - **groove.exe (Device)**  
    Baseline default: *True*

  - **exprwd.exe (Device)**  
    Baseline default: *True*

  - **mse7.exe (Device)**  
    Baseline default: *True*

  - **spDesign.exe (Device)**  
    Baseline default: *True*

  - **pptview.exe (Device)**  
    Baseline default: *True*

  - **winproj.exe (Device)**  
    Baseline default: *True*

- **Scripted Window Security Restrictions**  
  Baseline default: *Enabled*

  - **visio.exe (Device)**  
    Baseline default: *True*

  - **onent.exe (Device)**  
    Baseline default: *True*

  - **winword.exe (Device)**  
    Baseline default: *True*

  - **exprwd.exe (Device)**  
    Baseline default: *True*

  - **mspub.exe (Device)**  
    Baseline default: *True*

  - **outlook.exe (Device)**  
    Baseline default: *True*

  - **powerpnt.exe (Device)**  
    Baseline default: *True*

  - **groove.exe (Device)**  
    Baseline default: *True*

  - **mse7.exe (Device)**  
    Baseline default: *True*

  - **msaccess.exe (Device)**  
    Baseline default: *True*

  - **excel.exe (Device)**  
    Baseline default: *True*

  - **spDesign.exe (Device)**  
    Baseline default: *True*

  - **pptview.exe (Device)**  
    Baseline default: *True*

  - **winproj.exe (Device)**  
    Baseline default: *True*

 


### Microsoft Outlook 2016

*Security > Security Form Settings*

The "Outlook Security Mode" policy controls how security settings in Outlook are enforced. To manage any of the dependent Outlook security policies using Microsoft Endpoint Manager, Office cloud policy service, or Group policy this policy must be enabled and the Outlook Security Policy dropdown set to "Use Outlook Security Group Policy".

- **Outlook Security Mode (User)**
    *Enabled*
  - **Outlook Security Policy: (User)**
     *Use Outlook Security Group Policy*
    - **Guard behavior: (User)**
Automatically Deny
Configure Outlook object model prompt When accessing the Formula property of a UserProperty object (User)
Enabled
Guard behavior: (User)
Automatically Deny
Authentication with Exchange Server (User)
Enabled
Select the authentication with Exchange server. (User)
Kerberos Password Authentication
Configure Outlook object model prompt when reading address information (User)
Enabled
Guard behavior: (User)
Automatically Deny
Enable RPC encryption (User)
Enabled
Allow hyperlinks in suspected phishing e-mail messages (User)
Disabled
Configure Outlook object model prompt when sending mail (User)
Enabled
Allow users to demote attachments to Level 2 (User)
Disabled
Allow Active X One Off Forms (User)
Enabled
Sets which ActiveX controls to allow. 
Load only Outlook Controls
Allow scripts in one-off Outlook forms (User)
Disabled
Prevent users from customizing attachment security settings (User)
Enabled
Remove file extensions blocked as Level 2 (User)
Enabled
Removed Extensions: (User)
 
Retrieving CRLs (Certificate Revocation Lists) (User)
Enabled
When online always retreive the CRL
Configure Outlook object model prompt when accessing an address book (User)
Enabled
Guard behavior: (User)
Automatically Deny
Do not allow Outlook object model scripts to run for public folders (User)
Enabled
Include Internet in Safe Zones for Automatic Picture Download (User)
Disabled
Signature Warning (User)
Enabled
Signature Warning (User)
Always warn about invalid signatures
Use Unicode format when dragging e-mail message to file system (User)
Disabled
Set Outlook object model custom actions execution prompt (User)
Enabled
When executing a custom action: (User)
Automatically Deny
Security setting for macros (User)
Enabled
Security Level (User)
Warn for signed, disable unsigned
Remove file extensions blocked as Level 1 (User)
Enabled
Removed Extensions: (User)
 
Junk E-mail protection level (User)
Disabled
Display Level 1 attachments (User)
Disabled
Minimum encryption settings (User)
Enabled
Minimum key size (in bits): (User)
 
Do not allow Outlook object model scripts to run for shared folders (User)
Enabled
Configure Outlook object model prompt when executing Save As (User)
Enabled
Guard behavior: (User)
Automatically Deny
Configure Outlook object model prompt when responding to meeting and task requests (User)
Enabled
Guard behavior: (User)
Automatically Deny



