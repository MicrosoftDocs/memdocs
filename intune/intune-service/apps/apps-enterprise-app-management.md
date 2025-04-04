---
title: Microsoft Intune Enterprise Application Management
titleSuffix:
description: Learn about Enterprise App Management and the Enterprise App Catalog in Microsoft Intune. 
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 04/03/2025
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.assetid: 
ms.reviewer: dguilory
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
- FocusArea_Apps_EAC
---

# Microsoft Intune Enterprise Application Management

Microsoft Intune Enterprise App Management enables you to easily discover and deploy applications and keep them up to date from the Enterprise App Catalog. The Enterprise App Catalog is a collection of prepared Microsoft and non-Microsoft applications. These apps are Win32 apps that are [prepared as Win32 apps](../apps/apps-win32-prepare.md) and hosted by Microsoft.

> [!IMPORTANT]
> Enterprise App Management is an Intune add-on as part of the Intune suite that is available for trial and purchase. For more information, see [Use Intune Suite add-on capabilities](../fundamentals/intune-add-ons.md).

## Benefits of Enterprise App Management

The Enterprise App Management provides the following benefits:

- **Streamlined app management**: You can save time and reduce complexity by streamlining the app management process. Discover and add apps directly from the Intune console.
- **Stay current with updates**: You're able to keep apps up-to-date by easily creating apps for the new versions of products as they're available in the catalog. Use the **Enterprise App Catalog apps with updates** report.

When you add an Enterprise App Catalog app, Intune prefills the following installation details:

- Commands to install and uninstall the app
- Time required to install the app
- Option to allow app uninstallation by the end user
- Installation and device restart behavior
- Return codes to indicate post-installation behavior
- Whether to install the app for system or user
  
Microsoft Intune prefills the detection rules that devices must meet before the app is installed:

- File size
- File version
- Registry

Also, Intune prefills the requirements that devices must meet before the app is installed:

- Windows OS architecture required
- Minimum OS required

> [!IMPORTANT]
> Microsoft recommends using the prepopulated fields containing specific commands and rules, however you can modify the prepopulated fields if needed.

You can also configure app specific rules used to detect the presence of the Enterprise App Catalog app. You can choose to either manually configure the detection rules or use a custom script to detect the presence of the app before installing the app.

## Self-updating apps

The Enterprise App Catalog includes apps that self update. Intune ensures the app is at least at a target minimum version, and considers the app installed if the detected version of the app is at or above the minimum version. Self-updating apps update on client devices based on the vendor's process. Intune reports the version of the app detected on the device.

> [!IMPORTANT]
> Self-updating apps may require that your tenant has network rules configured to allow an update from the app vendor.

## Frequently asked questions (FAQ)

### How can I request to add an application to the Enterprise App Catalog?

We added a category to the [Microsoft Feedback Portal](https://feedbackportal.microsoft.com/feedback/forum/ef1d6d38-fd1b-ec11-b6e7-0022481f8472) that allows you to submit application requests, suggest changes, and share any other feedback about Enterprise application management. We recommend you filter the feedback portal under **Categories** by selecting **Enterprise App Management (Intune add-on)** to successfully route your requests and feedback.

To request adding an application to the Enterprise app catalog use the [Microsoft Feedback Portal](https://feedbackportal.microsoft.com/feedback/forum/ef1d6d38-fd1b-ec11-b6e7-0022481f8472). The feedback portal gives Microsoft the ability to communicate with you on the status of your request and other communication about your request.

Include the following details when requesting to add an application:
- Application publisher
- Application name
- Download URL

> [!IMPORTANT]
> Enterprise application management doesn't support the addition of applications that are behind a paywall or sign in screen.

You can also upvote an application previously submitted by someone else. Applications with large numbers of votes receive the most consideration and effort to be added to the catalog. However, priority depends on complexity of the applications mechanics.

> [!IMPORTANT]
> Microsoft makes no guarantee, express or implied, with respect to adding a requested app to the Enterprise App Catalog. Once the submission is reviewed using the form provided above, the app may or may not be added to the Enterprise App Catalog. Microsoft doesn't offer or assume any Service Level Agreement (SLA) or timeline regarding adding an app to the Enterprise App Catalog.

### Where are the devices downloading the app content from?

Microsoft hosts the applications in Microsoft storage accessible through `*.manage.microsoft.com`. For the full list of network requirements, see [Network endpoints for Microsoft Intune](../fundamentals/intune-endpoints.md?tabs=north-america).  

### Is Microsoft providing security around any of the content provided in the Enterprise App Catalog?

Microsoft doesn't assert compliance or authorizations for apps distributed via Intune. Customers are responsible for ensuring that apps meet their requirements.

### What app installer types are in the Enterprise App Catalog?

The apps currently provided in the Enterprise application catalog are Windows Win32 applications (exe and msi).

### How will Microsoft detect if an application from the Enterprise App Catalog is in use?

At this time, Intune provides no running application detection.

### What is the Service Level Agreement (SLA) for when an app update is available in the catalog?

No SLA is currently available.

### How many applications are in the catalog?

For a complete list of applications, see [Apps available in the Enterprise App Catalog](../apps/apps-enterprise-app-management.md#apps-available-in-the-enterprise-app-catalog).

### How can working with the applications in Enterprise App Catalog be automated?

You can use Microsoft's Graph API to work with applications in Enterprise App Catalog. For more information, see [Working with Intune in Microsoft Graph](/graph/api/resources/intune-graph-overview).

### Will Enterprise catalog apps automatically update to a new version when a new version is available in the Enterprise app catalog?

Updates are shown in Intune by selecting **Apps** > **Enterprise App Catalog apps with updates**. The updates aren't applied automatically. You still need to go in and create a new app with supersedence relationship.

### Can you get licensed applications from this catalog?

Yes. You can get licensed applications from the Enterprise App Catalog, although you're responsible for purchasing the license from the vendor and distributing it to your organization. Intune doesn't perform a license check on Enterprise App Catalog apps.

### Can Enterprise App Management be purchased standalone?

Yes. Enterprise App Management can be purchased as a standalone SKU or as part of the Microsoft Intune Suite.

### Can Enterprise App Management be used with Microsoft Configuration Manager?

Enterprise App Management is only provided by Microsoft Intune. Configuration Manager doesn't directly support Enterprise App Management apps, however co-managed clients can get Enterprise App Catalog apps when targeted from Microsoft Intune.

### Does Enterprise App Management use **Winget**?

No. Enterprise App Catalog apps are directly installed by the Intune management extension (IME).

### How do I update my Enterprise App Catalog app?

For applications that don’t update themselves, you can view the upgrades that are available for the Enterprise App Management (EAM) app via supersedence.

### After several hours, what can I do if my app continues to show that it isn't ready and that the requested content is still being prepared?

If the app content hasn't synced after several hours, delete the app and try again.

### Is there an Intune report available to view details about the Enterprise App Catalog apps for a specific device?

Yes, the Managed Apps report provides a report of apps on a specific device that are currently installed, not installed, or available for install. For the device, the report provides details about the application, version, resolved intent, and installation status. For more information about this report, see [Managed Apps report](../fundamentals/reports.md#managed-apps-report-operational).


## Apps available in the Enterprise App Catalog

There are various applications available in the Enterprise App Catalog. To view the current application list in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), see [Add a Windows catalog app (Win32) to Intune](../apps/apps-add-enterprise-app.md#add-a-windows-catalog-app-win32-to-intune).

> [!NOTE]
> Additional apps will be available on an ongoing basis in the Enterprise App Catalog.

The following table of Enterprise Apps is available within Intune:

| Apps |
|---|
| :::no-loc text="3CX Desktop App":::|
| :::no-loc text="3CXPhone for Windows":::|
| :::no-loc text="3DxWare 10":::|
| :::no-loc text="4K Video Downloader":::|
| :::no-loc text="4K Video Downloader+":::|
| :::no-loc text="7-Zip":::|
| :::no-loc text="Able2Extract Professional":::|
| :::no-loc text="ActiveState Software Komodo Edit":::|
| :::no-loc text="Adobe AIR":::|
| :::no-loc text="AIMP":::|
| :::no-loc text="Air Explorer":::|
| :::no-loc text="Aircall for desktop":::|
| :::no-loc text="AirParrot 2":::|
| :::no-loc text="Akiflow":::|
| :::no-loc text="Allway Sync":::|
| :::no-loc text="Altova XMLSpy Enterprise 2023":::|
| :::no-loc text="Amazon AWS Command Line Interface":::|
| :::no-loc text="Amazon AWS Tools for Windows":::|
| :::no-loc text="Amazon AWS VPN Client":::|
| :::no-loc text="Amazon Corretto JDK 11":::|
| :::no-loc text="Amazon Corretto JDK 15":::|
| :::no-loc text="Amazon Corretto JDK 16":::|
| :::no-loc text="Amazon Corretto JDK 17":::|
| :::no-loc text="Amazon Corretto JDK 18":::|
| :::no-loc text="Amazon Corretto JDK 19":::|
| :::no-loc text="Amazon Kindle":::|
| :::no-loc text="Amazon Redshift ODBC driver":::|
| :::no-loc text="Amazon WorkSpaces":::|
| :::no-loc text="Android Studio 2022":::|
| :::no-loc text="Android Studio 3":::|
| :::no-loc text="Android Studio 4":::|
| :::no-loc text="App Dynamic AirServer Universal":::|
| :::no-loc text="Apple iTunes":::|
| :::no-loc text="Aptakube":::|
| :::no-loc text="Araxis Merge":::|
| :::no-loc text="ArcticLine Software Jet Screenshot":::|
| :::no-loc text="Arduino IDE":::|
| :::no-loc text="Articulate 360":::|
| :::no-loc text="ASUS Remote Drive":::|
| :::no-loc text="Atlassian Companion":::|
| :::no-loc text="Audacity":::|
| :::no-loc text="Autodesk Access":::|
| :::no-loc text="Autodesk Identity Manager":::|
| :::no-loc text="Autodesk Single Signon Component":::|
| :::no-loc text="AVer Information A+ Suite":::|
| :::no-loc text="AWS SAM command line interface":::|
| :::no-loc text="AWS Session Manager Plugin":::|
| :::no-loc text="AxCrypt":::|
| :::no-loc text="Azure Functions Core Tools":::|
| :::no-loc text="Bambu Studio":::|
| :::no-loc text="Beam Studio":::|
| :::no-loc text="Belgium e-ID viewer":::|
| :::no-loc text="Beyond Compare":::|
| :::no-loc text="Beyond Identity":::|
| :::no-loc text="Blender":::|
| :::no-loc text="BlueJeans 2":::|
| :::no-loc text="Box CLI":::|
| :::no-loc text="Box Drive":::|
| :::no-loc text="Brady Workstation":::|
| :::no-loc text="Bridge Designer 2016":::|
| :::no-loc text="BrightAuthor connected":::|
| :::no-loc text="Bulk Crap Uninstaller":::|
| :::no-loc text="Bullzip PDF to Word":::|
| :::no-loc text="BurnAware Free":::|
| :::no-loc text="Burp Suite Community Edition":::|
| :::no-loc text="Burp Suite Professional Edition":::|
| :::no-loc text="Bytello Share":::|
| :::no-loc text="Calibrite Profiler":::|
| :::no-loc text="Camtasia Studio 2018":::|
| :::no-loc text="Camtasia Studio 2019":::|
| :::no-loc text="Caphyon Advanced Installer":::|
| :::no-loc text="Capture One 20":::|
| :::no-loc text="Capture One 22":::|
| :::no-loc text="Causasoft ExhibitManager":::|
| :::no-loc text="Charles":::|
| :::no-loc text="Chatbox":::|
| :::no-loc text="Chef Workstation for Windows":::|
| :::no-loc text="Cisco Jabber 14":::|
| :::no-loc text="Cisco JVDI Agent 12":::|
| :::no-loc text="Cisco JVDI Agent 14":::|
| :::no-loc text="Cisco Webex Meetings":::|
| :::no-loc text="Cisco WebEx Recorder and Player":::|
| :::no-loc text="Cisco WebEx Recording Editor":::|
| :::no-loc text="Cisco Webex Teams":::|
| :::no-loc text="Citrix Receiver":::|
| :::no-loc text="Citrix Workspace app":::|
| :::no-loc text="Citrix Workspace app LTSR":::|
| :::no-loc text="Class":::|
| :::no-loc text="Classic Shell":::|
| :::no-loc text="ClassPoint":::|
| :::no-loc text="Clevershare":::|
| :::no-loc text="ClockAssist":::|
| :::no-loc text="Clockify":::|
| :::no-loc text="Cloud Drive Mapper":::|
| :::no-loc text="CloudCompare":::|
| :::no-loc text="Cloudflare WARP":::|
| :::no-loc text="CMake":::|
| :::no-loc text="Colour Contrast Analyser":::|
| :::no-loc text="CPU-Z":::|
| :::no-loc text="Creative Force Kelvin":::|
| :::no-loc text="Creative Force Triad":::|
| :::no-loc text="Cryptomator":::|
| :::no-loc text="Cube Browser":::|
| :::no-loc text="CutePDF Writer":::|
| :::no-loc text="Dane Prairie Systems Win2PDF":::|
| :::no-loc text="DataGrip 1.0":::|
| :::no-loc text="DAX Studio":::|
| :::no-loc text="DB Browser for SQLite":::|
| :::no-loc text="DBeaver Community":::|
| :::no-loc text="DBeaver Enterprise":::|
| :::no-loc text="DBeaver Lite":::|
| :::no-loc text="DBeaver Ultimate":::|
| :::no-loc text="DbVisualizer":::|
| :::no-loc text="Defraggler":::|
| :::no-loc text="Delinea Connection Manager":::|
| :::no-loc text="Dell Command Update":::|
| :::no-loc text="Dell Command Update (Windows Universal Application)":::|
| :::no-loc text="Dell Display Manager":::|
| :::no-loc text="Dell EMC System Update":::|
| :::no-loc text="Dell Peripheral Manager":::|
| :::no-loc text="Devolutions Launcher":::|
| :::no-loc text="Devolutions Remote Desktop Manager":::|
| :::no-loc text="Devolutions Remote Desktop Manager Agent":::|
| :::no-loc text="Devolutions Workspace":::|
| :::no-loc text="DevPod":::|
| :::no-loc text="Directory Opus":::|
| :::no-loc text="DisplayLink Dock Driver":::|
| :::no-loc text="Ditto Connect":::|
| :::no-loc text="dnGrep":::|
| :::no-loc text="Docker Desktop":::|
| :::no-loc text="draw.io Desktop":::|
| :::no-loc text="dRofus":::|
| :::no-loc text="Eclipse Temurin JDK with Hotspot 11 (LTS)":::|
| :::no-loc text="Eclipse Temurin JDK with Hotspot 12":::|
| :::no-loc text="Eclipse Temurin JDK with Hotspot 15":::|
| :::no-loc text="Eclipse Temurin JDK with Hotspot 16":::|
| :::no-loc text="Eclipse Temurin JDK with Hotspot 17 (LTS)":::|
| :::no-loc text="Eclipse Temurin JDK with Hotspot 18":::|
| :::no-loc text="Eclipse Temurin JDK with Hotspot 19":::|
| :::no-loc text="Eclipse Temurin JDK with Hotspot 20":::|
| :::no-loc text="Eclipse Temurin JDK with Hotspot 21":::|
| :::no-loc text="Eclipse Temurin JDK with Hotspot 22":::|
| :::no-loc text="Eclipse Temurin JDK with Hotspot 23":::|
| :::no-loc text="Eclipse Temurin JRE with Hotspot 11 (LTS)":::|
| :::no-loc text="Eclipse Temurin JRE with Hotspot 12":::|
| :::no-loc text="Eclipse Temurin JRE with Hotspot 15":::|
| :::no-loc text="Eclipse Temurin JRE with Hotspot 16":::|
| :::no-loc text="Eclipse Temurin JRE with Hotspot 17 (LTS)":::|
| :::no-loc text="Eclipse Temurin JRE with Hotspot 18":::|
| :::no-loc text="Eclipse Temurin JRE with Hotspot 19":::|
| :::no-loc text="Eclipse Temurin JRE with Hotspot 20":::|
| :::no-loc text="Eclipse Temurin JRE with Hotspot 22":::|
| :::no-loc text="Eclipse Temurin JRE with Hotspot 23":::|
| :::no-loc text="Egnyte Connect Desktop App":::|
| :::no-loc text="Egnyte WebEdit":::|
| :::no-loc text="Elevate UC":::|
| :::no-loc text="Endnote 20":::|
| :::no-loc text="Endnote X8":::|
| :::no-loc text="Endnote X9":::|
| :::no-loc text="ESET Endpoint Antivirus V10":::|
| :::no-loc text="ESET Endpoint Antivirus V12":::|
| :::no-loc text="ESET Endpoint Security V12":::|
| :::no-loc text="Evernote":::|
| :::no-loc text="FactSet Workstation":::|
| :::no-loc text="FastPictureViewer Professional":::|
| :::no-loc text="FastStone Soft Capture":::|
| :::no-loc text="FastStone Soft Photo Resizer":::|
| :::no-loc text="FileZilla":::|
| :::no-loc text="FlashFXP":::|
| :::no-loc text="FlexWhere for Desktop":::|
| :::no-loc text="Fortify":::|
| :::no-loc text="Foxit PDF Editor 11":::|
| :::no-loc text="Foxit PDF Editor 12":::|
| :::no-loc text="Foxit PDF Editor Pro 11":::|
| :::no-loc text="Foxit PDF Reader":::|
| :::no-loc text="Foxit PhantomPDF 10":::|
| :::no-loc text="Foxit PhantomPDF Pro 10":::|
| :::no-loc text="Free Countdown Timer":::|
| :::no-loc text="Front Desktop":::|
| :::no-loc text="Fuzzy Lookup Add-In For Excel":::|
| :::no-loc text="FXHOME HitFilm Express":::|
| :::no-loc text="Gadwin ScreenRecorder":::|
| :::no-loc text="Garden Gnome Package Viewer":::|
| :::no-loc text="General Workings Streamlabs OBS":::|
| :::no-loc text="Genesys Cloud":::|
| :::no-loc text="GeoGebra 5":::|
| :::no-loc text="Geomilieu":::|
| :::no-loc text="Gephi":::|
| :::no-loc text="GIMP":::|
| :::no-loc text="Git":::|
| :::no-loc text="GitHub CLI":::|
| :::no-loc text="GnuPG VS-Desktop":::|
| :::no-loc text="GoAnywhere OpenPGP Studio":::|
| :::no-loc text="GoLand 2021.1":::|
| :::no-loc text="GoLand 2022.2":::|
| :::no-loc text="GoodSync 12":::|
| :::no-loc text="GoodSync Personal":::|
| :::no-loc text="Google Ads Editor":::|
| :::no-loc text="Google Backup and Sync":::|
| :::no-loc text="Google Chrome for Business":::|
| :::no-loc text="Google Chrome Remote Desktop Host":::|
| :::no-loc text="Google Drive":::|
| :::no-loc text="Google Drive File Stream":::|
| :::no-loc text="Google Go Programming Language 1.16":::|
| :::no-loc text="Google Go Programming Language 1.17":::|
| :::no-loc text="Google Go Programming Language 1.18":::|
| :::no-loc text="Google Go Programming Language 1.19":::|
| :::no-loc text="Google Go Programming Language 1.20":::|
| :::no-loc text="Google Go Programming Language 1.21":::|
| :::no-loc text="Google Go Programming Language 1.22":::|
| :::no-loc text="GoTo Connect":::|
| :::no-loc text="Gpg4win":::|
| :::no-loc text="GraphDB Desktop":::|
| :::no-loc text="grepWin":::|
| :::no-loc text="gsudo":::|
| :::no-loc text="Hanword HWP document converter for Microsoft Word 2016":::|
| :::no-loc text="HashTools":::|
| :::no-loc text="HeidiSQL":::|
| :::no-loc text="Horizon Collaborate":::|
| :::no-loc text="HP Client Management Script Library":::|
| :::no-loc text="HP Prime Virtual Calculator":::|
| :::no-loc text="Huddle Desktop":::|
| :::no-loc text="HWMonitor":::|
| :::no-loc text="IAP Desktop":::|
| :::no-loc text="Ibis Calculeren voor Bouw":::|
| :::no-loc text="IBM Aspera Connect":::|
| :::no-loc text="IBM Semeru Runtime Open Edition JDK 11 (LTS)":::|
| :::no-loc text="IBM Semeru Runtime Open Edition JDK 16":::|
| :::no-loc text="IBM Semeru Runtime Open Edition JDK 17 (LTS)":::|
| :::no-loc text="IBM Semeru Runtime Open Edition JDK 18":::|
| :::no-loc text="IBM Semeru Runtime Open Edition JDK 20":::|
| :::no-loc text="IBM Semeru Runtime Open Edition JDK 22":::|
| :::no-loc text="IBM Semeru Runtime Open Edition JRE 11 (LTS)":::|
| :::no-loc text="IBM Semeru Runtime Open Edition JRE 17 (LTS)":::|
| :::no-loc text="IBM Semeru Runtime Open Edition JRE 18":::|
| :::no-loc text="IBM Semeru Runtime Open Edition JRE 19":::|
| :::no-loc text="IBM Semeru Runtime Open Edition JRE 20":::|
| :::no-loc text="IBM Semeru Runtime Open Edition JRE 22":::|
| :::no-loc text="IcedTea-Web":::|
| :::no-loc text="iMazing Converter":::|
| :::no-loc text="ImpExpPro":::|
| :::no-loc text="Inkscape":::|
| :::no-loc text="Install4j":::|
| :::no-loc text="Intermedia Unite":::|
| :::no-loc text="IrfanView":::|
| :::no-loc text="IronPython":::|
| :::no-loc text="IsoBuster":::|
| :::no-loc text="JAM Software TreeSize Free":::|
| :::no-loc text="Joplin":::|
| :::no-loc text="JProfiler":::|
| :::no-loc text="KeePass Password Safe (Classic Edition)":::|
| :::no-loc text="KeePassXC":::|
| :::no-loc text="Keeper":::|
| :::no-loc text="KeeWeb":::|
| :::no-loc text="Kerio Connect":::|
| :::no-loc text="KeyShot Studio":::|
| :::no-loc text="KeyStore Explorer":::|
| :::no-loc text="Kobo":::|
| :::no-loc text="Konnekt":::|
| :::no-loc text="Kotobee Author":::|
| :::no-loc text="Kreya":::|
| :::no-loc text="Krisp":::|
| :::no-loc text="Krita":::|
| :::no-loc text="Lansweeper":::|
| :::no-loc text="Laserbox basic":::|
| :::no-loc text="LastPass":::|
| :::no-loc text="LEGO Education SPIKE":::|
| :::no-loc text="Lenovo Quick Clean":::|
| :::no-loc text="Lens Desktop":::|
| :::no-loc text="Liquit Workspace Agent 3":::|
| :::no-loc text="Logi Tune":::|
| :::no-loc text="Logitech Bolt":::|
| :::no-loc text="Logitech Options":::|
| :::no-loc text="Logitech Presentation":::|
| :::no-loc text="LogMeIn Client":::|
| :::no-loc text="LogMeIn GoToMeeting IT Installer":::|
| :::no-loc text="LogMeIn GoToMeeting multi-build Installer":::|
| :::no-loc text="LogMeIn Hamachi":::|
| :::no-loc text="LogMeIn Host":::|
| :::no-loc text="LogMeIn RemotelyAnywhere":::|
| :::no-loc text="LucaNet.Excel-Add-In":::|
| :::no-loc text="LucidLink Classic":::|
| :::no-loc text="Luna Modeler":::|
| :::no-loc text="Macrobond":::|
| :::no-loc text="Macrobond Viewer":::|
| :::no-loc text="Mail Viewer":::|
| :::no-loc text="Malwarebytes":::|
| :::no-loc text="MariaDB Server 10.2":::|
| :::no-loc text="MariaDB Server 10.3":::|
| :::no-loc text="MariaDB Server 10.4":::|
| :::no-loc text="MariaDB Server 10.5":::|
| :::no-loc text="MariaDB Server 10.6":::|
| :::no-loc text="MariaDB Server 10.7":::|
| :::no-loc text="MariaDB Server 10.9":::|
| :::no-loc text="Mattermost Desktop":::|
| :::no-loc text="Maxcut":::|
| :::no-loc text="MAXQDA 2020 Reader":::|
| :::no-loc text="Memento Desktop Edition":::|
| :::no-loc text="Mendeley Desktop":::|
| :::no-loc text="Mendeley Reference Manager":::|
| :::no-loc text="Meta Quest Developer Hub":::|
| :::no-loc text="Meta Spark Player":::|
| :::no-loc text="Microsoft Access Database Engine 2016":::|
| :::no-loc text="Microsoft Active Directory Rights Management Service Client":::|
| :::no-loc text="Microsoft Analysis Management Objects":::|
| :::no-loc text="Microsoft Analysis Services ADOMD.NET":::|
| :::no-loc text="Microsoft Analysis Services OLE DB Provider":::|
| :::no-loc text="Microsoft Azure CLI":::|
| :::no-loc text="Microsoft Azure Connected Machine Agent":::|
| :::no-loc text="Microsoft Azure Data Studio":::|
| :::no-loc text="Microsoft Azure PowerShell":::|
| :::no-loc text="Microsoft Azure Storage Explorer":::|
| :::no-loc text="Microsoft Bot Framework Composer":::|
| :::no-loc text="Microsoft Defender for Endpoint plug-in for WSL":::|
| :::no-loc text="Microsoft ODBC Driver 13 for SQL Server":::|
| :::no-loc text="Microsoft ODBC Driver 17 for SQL Server":::|
| :::no-loc text="Microsoft OLE DB Driver 18 for SQL Server":::|
| :::no-loc text="Microsoft Power BI Desktop":::|
| :::no-loc text="Microsoft PowerToys":::|
| :::no-loc text="Microsoft Remote Desktop WebRTC Redirector":::|
| :::no-loc text="Microsoft Remote Help":::|
| :::no-loc text="Microsoft Skype TX":::|
| :::no-loc text="Microsoft SQL Server 2012 Native Client":::|
| :::no-loc text="Microsoft SQL Server 2014 Express LocalDB":::|
| :::no-loc text="Microsoft SQL Server 2016 Report Builder":::|
| :::no-loc text="Microsoft SQL Server 2017 Express Advanced Edition":::|
| :::no-loc text="Microsoft SQL Server 2017 for Microsoft Windows Latest Cumulative Update":::|
| :::no-loc text="Microsoft Surface Data Eraser":::|
| :::no-loc text="Microsoft Surface Diagnostic Toolkit for Business":::|
| :::no-loc text="Microsoft System CLR Types for SQL Server 2014":::|
| :::no-loc text="Microsoft Universal Print Connector":::|
| :::no-loc text="Microsoft Visio 2016 Viewer":::|
| :::no-loc text="Microsoft Visual C++ 2012 Redistributable":::|
| :::no-loc text="Microsoft Visual C++ 2015-2022 Redistributable":::|
| :::no-loc text="Microsoft Visual Studio 2010 Tools for Office Runtime":::|
| :::no-loc text="Microsoft Visual Studio 2022 Enterprise":::|
| :::no-loc text="Microsoft Visual Studio 2022 Professional":::|
| :::no-loc text="Microsoft Visual Studio Code":::|
| :::no-loc text="Microsoft Visual Studio Team Explorer 2022":::|
| :::no-loc text="Microsoft Windows Admin Center":::|
| :::no-loc text="Microsoft Windows Assessment and Deployment Kit (ADK) for Windows 10 update 1607":::|
| :::no-loc text="Microsoft Windows Assessment and Deployment Kit (ADK) for Windows 10 update 1803":::|
| :::no-loc text="Microsoft Windows Assessment and Deployment Kit (ADK) for Windows 10 update 2004":::|
| :::no-loc text="Microsoft Windows Assessment and Deployment Kit (ADK) for Windows 11":::|
| :::no-loc text="Microsoft Windows PE add-on for ADK for Windows 11":::|
| :::no-loc text="monday":::|
| :::no-loc text="MongoDB Compass":::|
| :::no-loc text="MongoDB Compass Isolated Edition":::|
| :::no-loc text="MongoDB Compass Readonly Edition":::|
| :::no-loc text="MOOS Project Viewer":::|
| :::no-loc text="Morphic":::|
| :::no-loc text="Mozilla Firefox":::|
| :::no-loc text="Mozilla Firefox ESR 102":::|
| :::no-loc text="Mozilla Firefox ESR 115":::|
| :::no-loc text="Mozilla FrontMotion Firefox Community Edition ESR":::|
| :::no-loc text="Mozilla SeaMonkey":::|
| :::no-loc text="Mozilla Thunderbird":::|
| :::no-loc text="mPollux DigiSign Client":::|
| :::no-loc text="MSEndpointMgr Intune Debug Toolkit":::|
| :::no-loc text="MSIX Core":::|
| :::no-loc text="MuseScore 3":::|
| :::no-loc text="MuseScore Studio 4":::|
| :::no-loc text="Nagstamon":::|
| :::no-loc text="Nessus Agent 10":::|
| :::no-loc text="NetBird":::|
| :::no-loc text="NetSetMan":::|
| :::no-loc text="NETworkManager":::|
| :::no-loc text="New Relic Infrastructure Agent":::|
| :::no-loc text="Nextcloud":::|
| :::no-loc text="NextivaONE":::|
| :::no-loc text="Nitro Pro 11":::|
| :::no-loc text="Nitro Pro 13 (Retail)":::|
| :::no-loc text="Node.js 15":::|
| :::no-loc text="Node.js 17":::|
| :::no-loc text="Node.js 18 LTS":::|
| :::no-loc text="Node.js 19":::|
| :::no-loc text="Node.js 20 LTS":::|
| :::no-loc text="Node.js 21":::|
| :::no-loc text="Node.js 22 LTS":::|
| :::no-loc text="NordLayer":::|
| :::no-loc text="NVIDIA GeForce Experience":::|
| :::no-loc text="NVivo 12":::|
| :::no-loc text="NVivo 13":::|
| :::no-loc text="Obsidian":::|
| :::no-loc text="OnSIP":::|
| :::no-loc text="OpenAudible":::|
| :::no-loc text="OpenDNS Umbrella Roaming Client":::|
| :::no-loc text="OpenJDK 11":::|
| :::no-loc text="OpenJDK 16":::|
| :::no-loc text="OpenJDK 17":::|
| :::no-loc text="OpenJDK 21":::|
| :::no-loc text="OpenShot Video Editor":::|
| :::no-loc text="OpenVPN":::|
| :::no-loc text="OpenVPN Connect":::|
| :::no-loc text="OpenWebStart":::|
| :::no-loc text="Oracle Java SE Development Kit 17":::|
| :::no-loc text="Oracle Java SE Development Kit 23":::|
| :::no-loc text="ownCloud Desktop Client":::|
| :::no-loc text="Pandoc":::|
| :::no-loc text="PaperCut MF":::|
| :::no-loc text="PaperCut Mobility Print":::|
| :::no-loc text="PaperCut NG":::|
| :::no-loc text="Paperpile":::|
| :::no-loc text="Parallels Client 18":::|
| :::no-loc text="Parallels Client 19":::|
| :::no-loc text="Password Safe 3":::|
| :::no-loc text="Path Copy Copy":::|
| :::no-loc text="PDF Studio":::|
| :::no-loc text="PDF Studio Viewer":::|
| :::no-loc text="PDF24 Creator":::|
| :::no-loc text="PDFCreator":::|
| :::no-loc text="PDFgear":::|
| :::no-loc text="PDFsam Basic":::|
| :::no-loc text="PDFsam Visual":::|
| :::no-loc text="PDF-Tools":::|
| :::no-loc text="PDF-XChange PRO":::|
| :::no-loc text="PeaZip":::|
| :::no-loc text="PerformanceTest":::|
| :::no-loc text="Pexip Infinity Connect":::|
| :::no-loc text="PL SQL Developer 15":::|
| :::no-loc text="PlanGrid":::|
| :::no-loc text="Plex Media Player":::|
| :::no-loc text="Plex Media Server":::|
| :::no-loc text="Poll Everywhere":::|
| :::no-loc text="Poly Lens Desktop App":::|
| :::no-loc text="Power BI ALM Toolkit":::|
| :::no-loc text="Preform":::|
| :::no-loc text="PrinterLogic Printer Installer Client":::|
| :::no-loc text="Private Internet Access":::|
| :::no-loc text="Project Plan 365":::|
| :::no-loc text="Project Viewer 365":::|
| :::no-loc text="Proton VPN":::|
| :::no-loc text="PRTG Desktop":::|
| :::no-loc text="PSPad":::|
| :::no-loc text="Putty":::|
| :::no-loc text="PuTTY CAC":::|
| :::no-loc text="Python 3.10":::|
| :::no-loc text="Python 3.11":::|
| :::no-loc text="Python 3.12":::|
| :::no-loc text="Python 3.13":::|
| :::no-loc text="Python 3.7":::|
| :::no-loc text="Python 3.8":::|
| :::no-loc text="Python 3.9":::|
| :::no-loc text="QNAP Qsync":::|
| :::no-loc text="R for Windows":::|
| :::no-loc text="Rancher Desktop":::|
| :::no-loc text="Raspberry Pi Imager":::|
| :::no-loc text="RBTools":::|
| :::no-loc text="Red Hat OpenJDK":::|
| :::no-loc text="Red Hat OpenJDK JRE":::|
| :::no-loc text="Remote Ripple":::|
| :::no-loc text="RenderDoc":::|
| :::no-loc text="REV Hardware Client":::|
| :::no-loc text="RingCentral App":::|
| :::no-loc text="RingCentral Phone":::|
| :::no-loc text="Rocket.Chat":::|
| :::no-loc text="Royal TS 5":::|
| :::no-loc text="RStudio 1.4":::|
| :::no-loc text="RustDesk":::|
| :::no-loc text="RVTools":::|
| :::no-loc text="Saola Animate":::|
| :::no-loc text="ScaleFT":::|
| :::no-loc text="Screen InStyle":::|
| :::no-loc text="ScreenBeam Conference":::|
| :::no-loc text="ScreenCloud Player":::|
| :::no-loc text="ScreenToGif":::|
| :::no-loc text="SelfGuide Recorder":::|
| :::no-loc text="SharePoint Online Management Shell":::|
| :::no-loc text="Shotcut":::|
| :::no-loc text="SideQuest":::|
| :::no-loc text="Signiant App":::|
| :::no-loc text="Simplenote":::|
| :::no-loc text="Skillbrains LightShot":::|
| :::no-loc text="Slido":::|
| :::no-loc text="SmartFTP Client":::|
| :::no-loc text="Smartsheet desktop app":::|
| :::no-loc text="Snagit 2018":::|
| :::no-loc text="Snagit 2019":::|
| :::no-loc text="Snagit 2020":::|
| :::no-loc text="Snagit 2021":::|
| :::no-loc text="Snagit 2023":::|
| :::no-loc text="Snagit 2024":::|
| :::no-loc text="Snapform Viewer":::|
| :::no-loc text="Snapmaker Luban":::|
| :::no-loc text="SoapUI":::|
| :::no-loc text="Softerra LDAP Administrator":::|
| :::no-loc text="Softerra LDAP Browser":::|
| :::no-loc text="Softland doPDF":::|
| :::no-loc text="SolarWinds Orion SDK":::|
| :::no-loc text="SonicWall Connect Tunnel":::|
| :::no-loc text="SonicWall NetExtender":::|
| :::no-loc text="South River Technologies WebDrive":::|
| :::no-loc text="Spectrometry":::|
| :::no-loc text="Squirrels Reflector 3":::|
| :::no-loc text="Squirrels Reflector 4":::|
| :::no-loc text="SRWare Iron":::|
| :::no-loc text="Stellarium":::|
| :::no-loc text="Storyboarder":::|
| :::no-loc text="Striata Reader":::|
| :::no-loc text="SURF eduVPN Client":::|
| :::no-loc text="SURFdrive":::|
| :::no-loc text="Symphony Desktop Application":::|
| :::no-loc text="SyncBackFree":::|
| :::no-loc text="Synology Cloud Station Backup":::|
| :::no-loc text="Synology Drive Client":::|
| :::no-loc text="Synology Evidence Integrity Authenticator":::|
| :::no-loc text="Sysprogs SmarTTY":::|
| :::no-loc text="Tabular Editor 2":::|
| :::no-loc text="Tailscale":::|
| :::no-loc text="TDP SecureAnyBox Launcher":::|
| :::no-loc text="TeamDrive":::|
| :::no-loc text="TeamSpeak client":::|
| :::no-loc text="TeamViewer Host":::|
| :::no-loc text="Teracopy for Windows":::|
| :::no-loc text="TGRMN Software Bulk Rename Utility":::|
| :::no-loc text="The Document Foundation LibreOffice 24":::|
| :::no-loc text="The Document Foundation LibreOffice 24 Help Pack":::|
| :::no-loc text="Thycotic Application Control Agent":::|
| :::no-loc text="Thycotic Directory Services Agent":::|
| :::no-loc text="Tidio":::|
| :::no-loc text="TightVNC":::|
| :::no-loc text="TI-SmartView CE-T":::|
| :::no-loc text="TortoiseGit":::|
| :::no-loc text="TortoiseSVN":::|
| :::no-loc text="TortoiseSVN ipv6":::|
| :::no-loc text="Trimble Connect":::|
| :::no-loc text="TSPrint Client":::|
| :::no-loc text="Turbo Studio":::|
| :::no-loc text="Turbo.net Desktop":::|
| :::no-loc text="TurboVNC":::|
| :::no-loc text="Typora":::|
| :::no-loc text="UEStudio":::|
| :::no-loc text="UltraCompare":::|
| :::no-loc text="UltraFinder":::|
| :::no-loc text="UltraFTP":::|
| :::no-loc text="UltraMon":::|
| :::no-loc text="UltraVNC":::|
| :::no-loc text="Unity Hub":::|
| :::no-loc text="UNIVERGE BLUE CONNECT":::|
| :::no-loc text="UrBackup Client":::|
| :::no-loc text="Vagrant":::|
| :::no-loc text="VariCAD":::|
| :::no-loc text="VariCAD Viewer":::|
| :::no-loc text="VeraCrypt":::|
| :::no-loc text="VideoScribe":::|
| :::no-loc text="Visual Paradigm Project Viewer":::|
| :::no-loc text="VMware Horizon View Client 3.5":::|
| :::no-loc text="VMware Horizon View Client 5.4":::|
| :::no-loc text="voidtools Everything":::|
| :::no-loc text="voidtools Everything Lite":::|
| :::no-loc text="VSCodium":::|
| :::no-loc text="Waterfox Classic":::|
| :::no-loc text="Western Digital Dashboard":::|
| :::no-loc text="Wildix Collaboration":::|
| :::no-loc text="Win10Pcap":::|
| :::no-loc text="WinDirStat":::|
| :::no-loc text="Windows 10 Codec Pack":::|
| :::no-loc text="WinMerge":::|
| :::no-loc text="WireGuard":::|
| :::no-loc text="WizTree":::|
| :::no-loc text="Wrike":::|
| :::no-loc text="XMind 2020":::|
| :::no-loc text="XMind 2021":::|
| :::no-loc text="XMind 2022":::|
| :::no-loc text="XnSoft XnConvert":::|
| :::no-loc text="XnSoft XnShell":::|
| :::no-loc text="XnSoft XnView Extended":::|
| :::no-loc text="XnSoft XnView Minimal":::|
| :::no-loc text="XnSoft XnView MP":::|
| :::no-loc text="XnSoft XnView Standard":::|
| :::no-loc text="Yubico PIV Tool":::|
| :::no-loc text="YubiKey Manager CLI":::|
| :::no-loc text="Zeal":::|
| :::no-loc text="Zello":::|
| :::no-loc text="Zivver Office Plugin":::|
| :::no-loc text="Zoom Player Max":::|
| :::no-loc text="Zoom Plugin for Skype for Business":::|
| :::no-loc text="Zoom Plugin for Windows Virtual Desktop Client":::|
| :::no-loc text="Zorus Archon Agent":::|
| :::no-loc text="Zscaler Client Connector 3.6":::|
| :::no-loc text="Zscaler Client Connector 3.9":::|
| :::no-loc text="Zscaler Client Connector 4.0":::|
| :::no-loc text="Zscaler Client Connector 4.1":::|
| :::no-loc text="Zscaler Client Connector 4.3":::|
| :::no-loc text="Zscaler Client Connector for VDI":::|
| :::no-loc text="Zulip":::|
| :::no-loc text="Zulu JDK 10 (STS)":::|
| :::no-loc text="Zulu JDK 11 (LTS)":::|
| :::no-loc text="Zulu JDK 12 (STS)":::|
| :::no-loc text="Zulu JDK 13 (MTS)":::|
| :::no-loc text="Zulu JDK 15 (MTS)":::|
| :::no-loc text="Zulu JDK 16 (STS)":::|
| :::no-loc text="Zulu JDK 17 (LTS)":::|
| :::no-loc text="Zulu JDK 18 (STS)":::|
| :::no-loc text="Zulu JDK 20 (STS)":::|
| :::no-loc text="Zulu JRE 11 (LTS)":::|
| :::no-loc text="Zulu JRE 12 (STS)":::|
| :::no-loc text="Zulu JRE 13 (MTS)":::|
| :::no-loc text="Zulu JRE 15 (MTS)":::|
| :::no-loc text="Zulu JRE 17 (LTS)":::|

## Next steps

- [Add an Enterprise App Catalog app to Microsoft Intune](../apps/apps-add-enterprise-app.md)
- [Monitor app information and assignments with Microsoft Intune](apps-monitor.md)
- [Troubleshoot Win32 app issues](apps-win32-troubleshoot.md)
