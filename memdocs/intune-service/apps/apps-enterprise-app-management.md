---
title: Microsoft Intune Enterprise Application Management
titleSuffix:
description: Learn about Enterprise App Management and the Enterprise App Catalog in Microsoft Intune. 
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 03/17/2025
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
> Microsoft recommends using the pre-populated fields containing specific commands and rules, however you can modify the pre-populated fields if needed.

You can also configure app specific rules used to detect the presence of the Enterprise App Catalog app. You can choose to either manually configure the detection rules or use a custom script to detect the presence of the app before installing the app.

## Self-updating apps

The Enterprise App Catalog includes apps that self update. Intune ensures the app is at least at a target minimum version, and considers the app installed if the detected version of the app is at or above the minimum version. Self-updating apps update on client devices based on the vendor's process. Intune reports the version of the app detected on the device.

> [!IMPORTANT]
> Self-updating apps may require that your tenant has network rules configured to allow an update from the app vendor.

## Frequently asked questions (FAQ)

### How can I request to add an application to the Enterprise App Catalog?

We have added a new category to the [Microsoft Feedback Portal](https://feedbackportal.microsoft.com/feedback/forum/ef1d6d38-fd1b-ec11-b6e7-0022481f8472) that allows you to submit application requests, suggest changes, and share any other feedback about Enterprise application management. We recommend you filter the feedback portal under **Categories** by selecting **Enterprise App Management (Intune add-on)** to successfully route your requests and feedback.

To request adding an application to the Enterprise app catalog use the [Microsoft Feedback Portal](https://feedbackportal.microsoft.com/feedback/forum/ef1d6d38-fd1b-ec11-b6e7-0022481f8472). The feedback portal will also give Microsoft the ability to communicate with you on the status of your request and other communication about your request.

Include the following details when requesting to add an application:
- Application publisher
- Application name
- Download URL

> [!IMPORTANT]
> Enterprise application management does not support the addition of applications that are behind a paywall or login screen.

You can also upvote an application previously submitted by someone else. Applications with large numbers of votes receive the most consideration and effort to be added to the catalog. However, priority depends on complexity of the applications mechanics.

> [!IMPORTANT]
> Microsoft makes no guarantee, express or implied, with respect to adding a requested app to the Enterprise App Catalog. Once the submission is reviewed using the form provided above, the app may or may not be added to the Enterprise App Catalog. Microsoft does not offer or assume any Service Level Agreement (SLA) or timeline with regard to adding an app to the Enterprise App Catalog.

### Where are the devices downloading the app content from?

Microsoft hosts the applications in Microsoft storage accessible through `*.manage.microsoft.com`. For the full list of network requirements, see [Network endpoints for Microsoft Intune](../fundamentals/intune-endpoints.md?tabs=north-america).  

### Is Microsoft providing security around any of the content provided in the Enterprise App Catalog?

Microsoft does not assert compliance or authorizations for apps distributed via Intune. Customers are responsible for ensuring that apps meet their requirements.

### What app installer types are in the Enterprise App Catalog?

The apps currently provided in the Enterprise application catalog are Windows Win32 applications (exe and msi).

### How will Microsoft detect if an application from the Enterprise App Catalog is in use?

At this time, Intune provides no running application detection.

### What is the Service Level Agreement (SLA) for when an app update is available in the catalog?

No SLA is currently available.

### How many applications are in the catalog?

The catalog has over 400+ available applications in the Enterprise App Catalog. More apps are available on an ongoing basis.

### How can working with the applications in Enterprise App Catalog be automated?

Graph API is planned to be available soon.

### Will Enterprise catalog apps automatically update to a new version when a new version is available in the Enterprise app catalog?

Updates are shown in Monitor report under Enterprise App Catalog apps with updates. The updates won't be applied automatically. You still need to go in and create a new app with supersedence relationship.

### Can you get licensed applications from this catalog?

Yes. You can get licensed applications from the Enterprise App Catalog, although you're responsible for purchasing the license from the vendor and distributing it to your organization. Intune doesn't perform a license check on Enterprise App Catalog apps.

### Can Enterprise App Management be purchased standalone?

Yes. Enterprise App Management can be purchased as a standalone SKU or as part of the Microsoft Intune Suite.

### Can Enterprise App Management be leveraged with Microsoft Configuration Manager?

Enterprise App Management is only provided by Microsoft Intune. Configuration Manager doesn't directly support Enterprise App Management apps, however co-managed clients can get Enterprise App Catalog apps when targeted from Microsoft Intune.

### Does Enterprise App Management use **Winget**?

No. Enterprise App Catalog apps are directly installed by the Intune management extension (IME).

### How do I update my Enterprise App Catalog app?

For applications that don’t update themselves, you can view the upgrades that are available for the EAM app via supersedence.

### After several hours, what can I do if my app continues to show that it isn't ready and that the requested content is still being prepared?

If the app content hasn't synced after several hours, delete the app and try again.

### Is there an Intune report available to view details about the Enterprise App Catalog apps for a specific device?

Yes, the Managed Apps report provides a report of apps on a specific device that are currently installed, not installed, or available for install. For the device, the report provides details about the application, version, resolved intent, and installation status. For more information about this report, see [Managed Apps report](../fundamentals/reports.md#managed-apps-report-operational).


## Apps available in the Enterprise App Catalog

There are various applications available in the Enterprise App Catalog. To view the current application list in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), see [Add a Windows catalog app (Win32) to Intune](../apps/apps-add-enterprise-app.md#add-a-windows-catalog-app-win32-to-intune).

> [!NOTE]
> Additional apps will be available on an on-going basis in the Enterprise App Catalog.

The following table of Enterprise Apps is available within Intune:

| Apps |
|---|
| 3CXPhone for Windows |
| 3DF Zephyr Free |
| 4K Video Downloader |
| 4K Video Downloader+ |
| 7-Zip |
| 8x8 Work |
| Able2Extract Professional |
| ActiveState Software Komodo Edit |
| Adobe AIR |
| AIMP |
| Air Explorer |
| Aircall for desktop |
| Akiflow |
| Allway Sync |
| Amazon AWS Command Line Interface |
| Amazon AWS Tools for Windows |
| Amazon AWS VPN Client |
| Amazon Corretto JDK 11 |
| Amazon Corretto JDK 15 |
| Amazon Corretto JDK 16 |
| Amazon Corretto JDK 17 |
| Amazon Corretto JDK 19 |
| Amazon Corretto JDK 8 |
| Amazon Kindle |
| Amazon Redshift ODBC driver |
| Amazon WorkSpaces |
| Android Studio 2022 |
| Android Studio 3 |
| Android Studio 4 |
| App Dynamic AirServer Universal |
| Apple iTunes |
| Aptakube |
| Araxis Merge |
| ArcticLine Software Jet Screenshot |
| Arduino IDE |
| Articulate 360 |
| Artweaver Free |
| ASAP Utilities |
| ASUS Remote Drive |
| Atlassian Companion |
| Audacity |
| Autodesk Single Signon Component |
| AVer Information A+ Suite |
| AVS Media Player |
| AWS SAM command line interface |
| AWS Session Manager Plugin |
| Azure Functions Core Tools |
| Bambu Studio |
| BandiView |
| BCF Manager for Tekla |
| Beam Studio |
| Beats Winlogbeat |
| Belgium e-ID viewer |
| Beyond Compare |
| Beyond Identity |
| Blender |
| BlueJeans 2 |
| Box CLI |
| Box Drive |
| Brady Workstation |
| Bria Enterprise |
| BrightAuthor connected |
| Bulk Crap Uninstaller |
| Bullzip PDF to Word |
| BurnAware Free |
| Burp Suite Community Edition |
| Burp Suite Professional Edition |
| Calibre |
| Calibrite Profiler |
| Caphyon Advanced Installer |
| Capture One 20 |
| Capture One 22 |
| Causasoft ExhibitManager |
| Chef Workstation for Windows |
| Cisco Jabber 14 |
| Cisco JVDI Agent 12 |
| Cisco JVDI Agent 14 |
| Cisco Webex Meetings |
| Cisco WebEx Recorder and Player |
| Cisco WebEx Recording Editor |
| Cisco Webex Teams |
| Citrix Receiver |
| Citrix Workspace app |
| Citrix Workspace app LTSR |
| Class |
| ClassPoint |
| Clevershare |
| ClipboardFusion |
| ClockAssist |
| Clockify |
| Cloud Drive Mapper |
| CloudCompare |
| Cloudflare WARP |
| CMake |
| Colour Contrast Analyser |
| CPU-Z |
| Creative Force Kelvin |
| Cryptomator |
| Cube Browser |
| CutePDF Writer |
| Dane Prairie Systems Win2PDF |
| Datadog Agent |
| DAX Studio |
| DB Browser for SQLite |
| DBeaver Community |
| DBeaver Enterprise |
| DBeaver Lite |
| DBeaver Ultimate |
| DbVisualizer |
| Defraggler |
| Delinea Connection Manager |
| Dell Command Update |
| Dell Command Update (Windows Universal Application) |
| Dell Display Manager |
| Dell Peripheral Manager |
| Devolutions Launcher |
| Devolutions Remote Desktop Manager |
| Devolutions Remote Desktop Manager Agent |
| Devolutions Workspace |
| DevPod |
| Directory Opus |
| dnGrep |
| Docker Desktop |
| draw.io Desktop |
| dRofus |
| Druva inSync |
| Duo Desktop |
| Eclipse Temurin JDK with Hotspot 11 (LTS) |
| Eclipse Temurin JDK with Hotspot 12 |
| Eclipse Temurin JDK with Hotspot 15 |
| Eclipse Temurin JDK with Hotspot 16 |
| Eclipse Temurin JDK with Hotspot 17 (LTS) |
| Eclipse Temurin JDK with Hotspot 18 |
| Eclipse Temurin JDK with Hotspot 19 |
| Eclipse Temurin JDK with Hotspot 20 |
| Eclipse Temurin JDK with Hotspot 21 |
| Eclipse Temurin JDK with Hotspot 22 |
| Eclipse Temurin JDK with Hotspot 8 (LTS) |
| Eclipse Temurin JRE with Hotspot 11 (LTS) |
| Eclipse Temurin JRE with Hotspot 12 |
| Eclipse Temurin JRE with Hotspot 15 |
| Eclipse Temurin JRE with Hotspot 16 |
| Eclipse Temurin JRE with Hotspot 17 (LTS) |
| Eclipse Temurin JRE with Hotspot 18 |
| Eclipse Temurin JRE with Hotspot 19 |
| Eclipse Temurin JRE with Hotspot 20 |
| Eclipse Temurin JRE with Hotspot 22 |
| Eclipse Temurin JRE with Hotspot 8 (LTS) |
| Egnyte Connect Desktop App |
| Egnyte WebEdit |
| Elevate UC |
| Endnote 20 |
| Endnote X8 |
| Endnote X9 |
| ESET Endpoint Antivirus V10 |
| ESET Endpoint Antivirus V12 |
| ESET Endpoint Security V12 |
| Evernote |
| FactSet Workstation |
| FastPictureViewer Professional |
| FastStone Soft Capture |
| FastStone Soft Image Viewer |
| FastStone Soft Photo Resizer |
| FileZilla |
| FlashFXP |
| FlexWhere for Desktop |
| Forté Agent |
| Fortify |
| Foxit PDF Editor 11 |
| Foxit PDF Editor 12 |
| Foxit PDF Editor Pro 11 |
| Foxit PDF Reader |
| Foxit PhantomPDF 10 |
| Foxit PhantomPDF Pro 10 |
| Frame App |
| Free Countdown Timer |
| Front Desktop |
| FXHOME HitFilm Express |
| Gadwin PrintScreen |
| Gadwin PrintScreenPro |
| Garden Gnome Package Viewer |
| Genesys Cloud |
| GeoGebra 5 |
| GeoGebra 6 |
| GIMP |
| Git |
| GitHub CLI |
| GoLand 2021.1 |
| GoLand 2022.2 |
| GoodSync 12 |
| GoodSync Personal |
| Google Ads Editor |
| Google Backup and Sync |
| Google Chrome for Business |
| Google Chrome Remote Desktop Host |
| Google Drive |
| Google Drive File Stream |
| Google Go Programming Language 1.16 |
| Google Go Programming Language 1.19 |
| Google Go Programming Language 1.20 |
| Google Go Programming Language 1.21 |
| Google Go Programming Language 1.22 |
| GoTo Connect |
| Gpg4win |
| GraphDB Desktop |
| grepWin |
| gsudo |
| HeidiSQL |
| HP Client Management Script Library |
| HP Prime Virtual Calculator |
| Huddle Desktop |
| HWMonitor |
| IAP Desktop |
| IBM Aspera Connect |
| IBM Semeru Runtime Open Edition JDK 11 (LTS) |
| IBM Semeru Runtime Open Edition JDK 16 |
| IBM Semeru Runtime Open Edition JDK 17 (LTS) |
| IBM Semeru Runtime Open Edition JDK 18 |
| IBM Semeru Runtime Open Edition JDK 22 |
| IBM Semeru Runtime Open Edition JDK 8 (LTS) |
| IBM Semeru Runtime Open Edition JRE 11 (LTS) |
| IBM Semeru Runtime Open Edition JRE 17 (LTS) |
| IBM Semeru Runtime Open Edition JRE 18 |
| IBM Semeru Runtime Open Edition JRE 22 |
| IBM Semeru Runtime Open Edition JRE 8 (LTS) |
| IcedTea-Web |
| ImageGlass |
| Inkscape |
| Intermedia Unite |
| IrfanView |
| IronPython |
| IsoBuster |
| Jabra Direct |
| JAM Software TreeSize Free |
| Joplin |
| KeePass Password Safe (Classic Edition) |
| KeePassXC |
| Keeper |
| Kerio Connect |
| Kobo |
| Konnekt |
| Kotobee Author |
| Krisp |
| Krita |
| Lansweeper |
| Laserbox basic |
| LastPass |
| LEGO Education SPIKE |
| Lenovo Quick Clean |
| Lens Desktop |
| Liberica JDK |
| Liquit Workspace Agent 3 |
| Local Administrator Password Solution |
| Logi Tune |
| Logitech Options |
| Logitech Presentation |
| Logitech SetPoint |
| LogMeIn Client |
| LogMeIn GoToMeeting IT Installer |
| LogMeIn GoToMeeting multi-build Installer |
| LogMeIn Hamachi |
| LogMeIn Host |
| LogMeIn RemotelyAnywhere |
| Luna Modeler |
| Mail Viewer |
| Malwarebytes |
| MariaDB Server 10.2 |
| MariaDB Server 10.3 |
| MariaDB Server 10.4 |
| MariaDB Server 10.5 |
| MariaDB Server 10.6 |
| MariaDB Server 10.7 |
| MariaDB Server 10.9 |
| Mattermost Desktop |
| Maxcut |
| MAXQDA 2020 Reader |
| Memento Desktop Edition |
| Mendeley Desktop |
| Mendeley Reference Manager |
| Mersive Solstice Client |
| Meta Quest Developer Hub |
| Microsoft .NET Runtime 6.0 |
| Microsoft .NET Runtime 7.0 |
| Microsoft Active Directory Rights Management Service Client |
| Microsoft Analysis Management Objects |
| Microsoft Analysis Services ADOMD.NET |
| Microsoft Analysis Services OLE DB Provider |
| Microsoft ASP.NET Core Runtime 6.0 |
| Microsoft ASP.NET Core Runtime 7.0 |
| Microsoft Azure CLI |
| Microsoft Azure Connected Machine Agent |
| Microsoft Azure Data Studio |
| Microsoft Azure PowerShell |
| Microsoft Azure Storage Explorer |
| Microsoft Defender for Endpoint plug-in for WSL |
| Microsoft Deployment Toolkit (8456) |
| Microsoft ODBC Driver 13 for SQL Server |
| Microsoft OLE DB Driver 18 for SQL Server |
| Microsoft Power BI Desktop |
| Microsoft PowerShell Core |
| Microsoft PowerToys |
| Microsoft Remote Help |
| Microsoft Skype for Desktop |
| Microsoft Skype TX |
| Microsoft SQL Server 2012 Native Client |
| Microsoft SQL Server 2014 Express LocalDB |
| Microsoft SQL Server 2016 Report Builder |
| Microsoft SQL Server 2017 Express Advanced Edition |
| Microsoft SQL Server 2017 for Microsoft Windows Latest Cumulative Update |
| Microsoft Surface Data Eraser |
| Microsoft Surface Diagnostic Toolkit for Business |
| Microsoft System CLR Types for SQL Server 2014 |
| Microsoft Universal Print Connector |
| Microsoft Visual C++ 2005 Redistributable |
| Microsoft Visual C++ 2015-2022 Redistributable |
| Microsoft Visual Studio 2022 Enterprise |
| Microsoft Visual Studio 2022 Professional |
| Microsoft Visual Studio Code |
| Microsoft Visual Studio Team Explorer 2022 |
| Microsoft Windows Admin Center |
| Microsoft Windows Assessment and Deployment Kit (ADK) for Windows 10 update 1607 |
| Microsoft Windows Assessment and Deployment Kit (ADK) for Windows 10 update 1803 |
| Microsoft Windows Assessment and Deployment Kit (ADK) for Windows 10 update 2004 |
| Microsoft Windows Assessment and Deployment Kit (ADK) for Windows 11 |
| Microsoft Windows Desktop Runtime 6.0 |
| Microsoft Windows Desktop Runtime 7.0 |
| Microsoft Windows PE add-on for ADK for Windows 11 |
| MongoDB Compass |
| MongoDB Compass Isolated Edition |
| MongoDB Compass Readonly Edition |
| MOOS Project Viewer |
| Mozilla Firefox |
| Mozilla Firefox ESR 102 |
| Mozilla Firefox ESR 115 |
| Mozilla FrontMotion Firefox Community Edition ESR |
| Mozilla SeaMonkey |
| Mozilla Thunderbird |
| MSEndpointMgr Intune Debug Toolkit |
| MSIX Core |
| MuseScore 3 |
| MuseScore Studio 4 |
| Nessus Agent 10 |
| NetBird |
| NetLogo |
| NetSetMan |
| NETworkManager |
| New Relic Infrastructure Agent |
| Nextcloud |
| NextivaONE |
| Nitro Pro 13 (Retail) |
| Node.js 15 |
| Node.js 17 |
| Node.js 18 LTS |
| Node.js 19 |
| Node.js 20 LTS |
| Node.js 21 |
| Node.js 22 LTS |
| NoMachine |
| NoMachine Enterprise Client |
| NoMachine Fonts Others |
| NordLayer |
| NVIDIA GeForce Experience |
| Obsidian |
| OnSIP |
| OpenAudible |
| OpenDNS Umbrella Roaming Client |
| OpenJDK 11 |
| OpenJDK 16 |
| OpenJDK 17 |
| OpenLens |
| OpenShot Video Editor |
| OpenVPN |
| OpenVPN Connect |
| OpenWebStart |
| Oracle Java Runtime Environment Version 8 |
| Oracle Java SE Development Kit 17 |
| Oracle MySQL Installer 8 |
| ownCloud Desktop Client |
| Pandoc |
| PaperCut MF |
| PaperCut Mobility Print |
| PaperCut NG |
| Parallels Client 18 |
| Parallels Client 19 |
| Parallels Toolbox |
| Password Safe 3 |
| PDF Studio |
| PDF Studio Viewer |
| PDF24 Creator |
| PDFCreator |
| PDFgear |
| PDFsam Basic |
| PDFsam Visual |
| PDF-Tools |
| PDF-XChange PRO |
| PeaZip |
| PerformanceTest |
| Pexip Infinity Connect |
| PicPick |
| Piriform CCleaner |
| Piriform CCleaner Slim |
| PlanGrid |
| PLEdit 7 |
| Plex Media Server |
| Poll Everywhere |
| Poly Lens Desktop App |
| Power BI ALM Toolkit |
| PrinterLogic Printer Installer Client |
| Private Internet Access |
| Project Plan 365 |
| Project Viewer 365 |
| Proton VPN |
| PRTG Desktop |
| PSPad |
| Publish or Perish |
| Putty |
| PuTTY CAC |
| Python 3.10 |
| Python 3.11 |
| Python 3.12 |
| Python 3.9 |
| QNAP Qsync |
| Qurentis |
| R for Windows |
| Rancher Desktop |
| Rarlab WinRAR |
| RBTools |
| REAPER |
| Red Hat OpenJDK |
| Red Hat OpenJDK JRE |
| RenderDoc |
| REV Hardware Client |
| RingCentral App |
| RingCentral Phone |
| Rocket.Chat |
| Royal TS 5 |
| Royal TS 6 |
| Royal TS 7 |
| RStudio 1.4 |
| RustDesk |
| RVTools |
| ScaleFT |
| Screen InStyle |
| ScreenCloud Player |
| ScreenToGif |
| Sejda PDF Desktop |
| SelfGuide Recorder |
| SharePoint Online Management Shell |
| Shotcut |
| SideQuest |
| Simplenote |
| Skillbrains LightShot |
| Slido |
| Smartsheet desktop app |
| Snagit 2019 |
| Snagit 2020 |
| Snagit 2021 |
| Snagit 2023 |
| Snagit 2024 |
| Snapform Viewer |
| SnapGene Viewer |
| Snapmaker Luban |
| SoapUI |
| Softerra LDAP Administrator |
| Softland doPDF |
| SolarWinds Orion SDK |
| SonicWall NetExtender |
| South River Technologies WebDrive |
| Spectrometry |
| Squirrels Reflector 3 |
| Squirrels Reflector 4 |
| SRWare Iron |
| Stellarium |
| Storyboarder |
| SURF eduVPN Client |
| SURFdrive |
| Symphony Desktop Application |
| SyncBackFree |
| Synology Drive Client |
| Synology Evidence Integrity Authenticator |
| Sysprogs SmarTTY |
| TablePlus |
| Tabular Editor 2 |
| Tailscale |
| TDP SecureAnyBox Launcher |
| TeamDrive |
| TeamSpeak client |
| TeamViewer Host |
| Teracopy for Windows |
| TextExpander |
| TGRMN Software Bulk Rename Utility |
| The Document Foundation LibreOffice 24 |
| The Document Foundation LibreOffice 24 Help Pack |
| The Document Foundation LibreOffice 6.3 |
| The Document Foundation LibreOffice 7.4 Help Pack |
| The Document Foundation LibreOffice 7.5 SDK |
| Thycotic Application Control Agent |
| Thycotic Directory Services Agent |
| Tidio |
| TightVNC |
| TI-SmartView CE-T |
| TortoiseGit |
| TortoiseHg |
| TortoiseSVN |
| TortoiseSVN ipv6 |
| Trimble Connect |
| TSPrint Client |
| Turbo Studio |
| Turbo.net Desktop |
| TurboVNC |
| Typora |
| UEStudio |
| UltraCompare |
| UltraViewer |
| UltraVNC |
| Unity Hub |
| UNIVERGE BLUE CONNECT |
| Vagrant |
| VariCAD |
| VariCAD Viewer |
| VeraCrypt |
| Visual Paradigm Project Viewer |
| VMware Horizon View Client 3.5 |
| VMware Horizon View Client 5.4 |
| voidtools Everything |
| voidtools Everything Lite |
| VSCodium |
| Waterfox |
| Waterfox Classic |
| Western Digital Dashboard |
| Win10Pcap |
| WinDirStat |
| Windows 10 Codec Pack |
| WinMerge |
| WinSCP |
| WireGuard |
| WizTree |
| Wrike |
| Xamarin Mono |
| XMind 2020 |
| XMind 2021 |
| XnSoft XnConvert |
| XnSoft XnView Extended |
| XnSoft XnView Minimal |
| XnSoft XnView MP |
| XnSoft XnView Standard |
| Yubico Authenticator |
| YubiKey Manager CLI |
| Zeal |
| Zello |
| Zivver Office Plugin |
| Zoom Player Max |
| Zoom Plugin for Microsoft Outlook |
| Zoom Plugin for Skype for Business |
| Zoom Plugin for Windows Virtual Desktop Client |
| Zoom Rooms |
| Zoom VDI Universal Plugin |
| Zoom Workplace |
| Zorus Archon Agent |
| Zotero |
| Zscaler Client Connector 3.6 |
| Zscaler Client Connector 3.9 |
| Zscaler Client Connector 4.0 |
| Zscaler Client Connector 4.3 |
| Zscaler Client Connector for VDI |
| Zulip |
| Zulu JDK 11 (LTS) |
| Zulu JDK 13 (MTS) |
| Zulu JDK 15 (MTS) |
| Zulu JDK 16 (STS) |
| Zulu JDK 17 (LTS) |
| Zulu JDK 18 (STS) |
| Zulu JDK 20 (STS) |
| Zulu JRE 11 (LTS) |
| Zulu JRE 13 (MTS) |
| Zulu JRE 15 (MTS) |
| Zulu JRE 17 (LTS) |

## Next steps

- [Add an Enterprise App Catalog app to Microsoft Intune](../apps/apps-add-enterprise-app.md)
- [Monitor app information and assignments with Microsoft Intune](apps-monitor.md)
- [Troubleshoot Win32 app issues](apps-win32-troubleshoot.md)
