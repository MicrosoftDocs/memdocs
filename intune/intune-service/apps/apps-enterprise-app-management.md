---
title: Microsoft Intune Enterprise Application Management
description: Learn about Enterprise App Management and the Enterprise App Catalog in Microsoft Intune.
ms.date: 01/07/2026
ms.topic: how-to
ms.reviewer: dguilory
ms.subservice: suite
ms.collection:
- M365-identity-device-management
- highpri
- FocusArea_Apps_EAC
---

# Microsoft Intune Enterprise Application Management

Microsoft Intune Enterprise App Management enables you to easily discover and deploy applications and keep them up to date from the Enterprise App Catalog. The Enterprise App Catalog is a collection of prepared Microsoft and non-Microsoft applications. These apps are Win32 apps that are [prepared as Win32 apps](../apps/apps-win32-prepare.md) and hosted by Microsoft.

> [!IMPORTANT]
> Enterprise App Management is an Intune add-on as part of the Intune suite that's available for trial and purchase. For more information, see [Use Intune Suite add-on capabilities](../fundamentals/intune-add-ons.md).

[!INCLUDE [windows-10-support](../includes/windows-10-support.md)]

## Benefits of Enterprise App Management

The Enterprise App Management provides the following benefits:

- **Streamlined app management**: You can save time and reduce complexity by streamlining the app management process. Discover and add apps directly from the Intune console.
- **Stay current with updates**: You're able to keep apps up-to-date by easily creating apps for the new versions of products as they're available in the catalog. Use the **Enterprise App Catalog apps with updates** report.
- **Windows Autopilot integration**: Enterprise App Catalog apps are supported with Windows Autopilot. Microsoft Intune Enterprise App Management enables IT admins to easily manage applications from the Enterprise App Catalog. Using Windows Autopilot, you can select blocking apps from the Enterprise App Catalog in the Enrollment Status Page (ESP) and the Device Preparation Page (DPP) profiles. This feature allows you to update apps more easily without needing to update those profiles with the latest versions.

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
> Self-updating apps might require that your tenant has network rules configured to allow an update from the app vendor.

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
> Microsoft makes no guarantee, express or implied, with respect to adding a requested app to the Enterprise App Catalog. After Microsoft reviews the submission form, the app might be added. Microsoft doesn't offer or assume any Service Level Agreement (SLA) or timeline regarding adding an app to the Enterprise App Catalog.

### Where are the devices downloading the app content from?

Microsoft hosts the applications in Microsoft storage accessible through `*.manage.microsoft.com`. For the full list of network requirements, see [Network endpoints for Microsoft Intune](../fundamentals/intune-endpoints.md?tabs=north-america).

### Is Microsoft providing security around any of the content provided in the Enterprise App Catalog?

Microsoft doesn't assert compliance, authorization, authenticity, or integrity for apps distributed via Intune. Customers are responsible for ensuring that apps meet their requirements.

### What app installer types are in the Enterprise App Catalog?

The apps currently provided in the Enterprise application catalog are Windows Win32 applications (exe and msi).

### How can Microsoft detect if an application from the Enterprise App Catalog is in use?

At this time, Intune provides no running application detection.

### What are the Service Level Objectives for when an app update is available in the catalog?

Service Level Objectives (SLOs) define target timelines for making app updates available in the Enterprise App Catalog between when Microsoft receives them to when they're made available in the Enterprise App Catalog. Unlike Service Level Agreements (SLAs), SLOs are guidelines, not guarantees that allow customers to plan typical app update processing timelines.

The SLO measurement window starts at ingestion, the point when the app update is first received from the data source and logged in the EAM system.

#### App Update Process Flow

1. **Ingestion** – App update is received by Microsoft
2. **Automated Validation** – Compatibility and compliance checks
3. **Manual Validation** - More testing if needed
4. **Catalog Availability** – App update published to Enterprise App Catalog

#### Automated Validation

Most apps undergo automated validation checks.

- Target: 80–90% of app updates are processed and available in the Intune portal within 24 hours of ingestion.

#### Manual Validation Apps

If an app fails automated checks, it moves to manual validation and requires more testing. Updates requiring manual testing and approval are completed within seven days.

#### Exception Handling

- High-usage or critical apps that fail automated validation are prioritized for expedited processing (goal of 48 hours.)
- Apps that fail both automated and manual validation don't meet SLO and are flagged as unsupported.

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

Enterprise App Management is only provided by Microsoft Intune. Configuration Manager doesn't directly support Enterprise App Management apps. However, co-managed clients can get Enterprise App Catalog apps when targeted from Microsoft Intune.

### What happens if an app is removed from the Enterprise App Catalog?

Occasionally, app vendors might request removal of their applications from the Enterprise App Catalog. When this happens:

- **Existing deployments remain unaffected**: Apps that are already deployed to your tenant and user devices continue to function normally.
- **No new deployments**: You can't deploy new instances of the removed app from the Enterprise App Catalog.
- **Alternative solutions**: For future deployments, work directly with the app vendor or use traditional Win32 app deployment methods.

### Does Enterprise App Management use **Winget**?

No. Enterprise App Catalog apps are directly installed by the Intune management extension (IME).

### How do I update my Enterprise App Catalog app?

For applications that don't update themselves, you can view the upgrades that are available for the Enterprise App Management (EAM) app via supersedence.

### After several hours, what can I do if my app continues to show that it isn't ready and that the requested content is still being prepared?

If the app content isn't synced after several hours, delete the app and try again.

### Is there an Intune report available to view details about the Enterprise App Catalog apps for a specific device?

Yes, the Managed Apps report provides a report of apps on a specific device that are currently installed, not installed, or available for install. For the device, the report provides details about the application, version, resolved intent, and installation status. For more information about this report, see [Managed Apps report](../fundamentals/reports.md#managed-apps-report-operational).


## Apps available in the Enterprise App Catalog

There are various applications available in the Enterprise App Catalog. To view the current application list in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), see [Add a Windows catalog app (Win32) to Intune](../apps/apps-add-enterprise-app.md#add-a-windows-catalog-app-win32-to-intune).

More apps are available on an ongoing basis in the Enterprise App Catalog.

> [!NOTE]
> **think-cell apps removed from Enterprise App Catalog**: At the request of think-cell, their applications are removed from the Enterprise App Catalog. This removal **does not affect** existing think-cell installations in your tenant or on user devices. Customers who currently have think-cell apps deployed through the Enterprise App Catalog can continue to manage these installations normally.

The following table of Enterprise Apps is available within Intune:

| Apps |
|---|
| :::no-loc text="3CX Desktop App":::|
| :::no-loc text="3CXPhone for Windows":::|
| :::no-loc text="3DF Zephyr Free":::|
| :::no-loc text="3DxWare 10":::|
| :::no-loc text="4K Video Downloader":::|
| :::no-loc text="4K Video Downloader+":::|
| :::no-loc text="7-Zip":::|
| :::no-loc text="8x8 Work":::|
| :::no-loc text="AbaClient":::|
| :::no-loc text="Able2Extract Professional":::|
| :::no-loc text="Acro Software CutePDF Writer":::|
| :::no-loc text="ActiveState Software Komodo Edit":::|
| :::no-loc text="ActiveState Software Komodo IDE":::|
| :::no-loc text="Adobe AIR":::|
| :::no-loc text="Agent Ransack":::|
| :::no-loc text="AIMP":::|
| :::no-loc text="Air Explorer":::|
| :::no-loc text="Aircall for desktop":::|
| :::no-loc text="AirParrot 2":::|
| :::no-loc text="Akiflow":::|
| :::no-loc text="alfaview":::|
| :::no-loc text="Allway Sync":::|
| :::no-loc text="ALLPlayer":::|
| :::no-loc text="Altova XMLSpy Enterprise 2023":::|
| :::no-loc text="Amazon AWS Command Line Interface":::|
| :::no-loc text="Amazon AWS Tools for Windows":::|
| :::no-loc text="Amazon AWS VPN Client":::|
| :::no-loc text="Amazon Corretto 18":::|
| :::no-loc text="Amazon Corretto JDK 8":::|
| :::no-loc text="Amazon Corretto JDK 11":::|
| :::no-loc text="Amazon Corretto JDK 15":::|
| :::no-loc text="Amazon Corretto JDK 16":::|
| :::no-loc text="Amazon Corretto JDK 17":::|
| :::no-loc text="Amazon Corretto JDK 19":::|
| :::no-loc text="Amazon DCV Client":::|
| :::no-loc text="Amazon Kindle":::|
| :::no-loc text="Amazon Redshift ODBC driver":::|
| :::no-loc text="Amazon WorkSpaces":::|
| :::no-loc text="Android Studio 2022":::|
| :::no-loc text="Android Studio 3":::|
| :::no-loc text="Android Studio 4":::|
| :::no-loc text="AnyBurn":::|
| :::no-loc text="AnyDesk":::|
| :::no-loc text="AnyLogic Professional":::|
| :::no-loc text="AnyLogic University":::|
| :::no-loc text="Anywhere365 Integrator":::|
| :::no-loc text="App Dynamic AirServer Universal":::|
| :::no-loc text="Appgate SDP Client":::|
| :::no-loc text="Apple iTunes":::|
| :::no-loc text="Aptakube":::|
| :::no-loc text="Araxis Merge":::|
| :::no-loc text="ArcticLine Software Jet Screenshot":::|
| :::no-loc text="Arduino IDE":::|
| :::no-loc text="Articulate 360":::|
| :::no-loc text="Articulate Replay 360":::|
| :::no-loc text="Articulate Studio 360":::|
| :::no-loc text="Artweaver Free":::|
| :::no-loc text="ASAP Utilities":::|
| :::no-loc text="ASUS Remote Drive":::|
| :::no-loc text="Astute Manager":::|
| :::no-loc text="Atlassian Companion":::|
| :::no-loc text="Atlassian Confluence":::|
| :::no-loc text="Atomi Systems ActivePresenter":::|
| :::no-loc text="Atostek ID":::|
| :::no-loc text="Audacity":::|
| :::no-loc text="Autodesk Access":::|
| :::no-loc text="Autodesk Design Review 2018":::|
| :::no-loc text="Autodesk Identity Manager":::|
| :::no-loc text="Autodesk Interoperability Tools":::|
| :::no-loc text="Autodesk Single Signon Component":::|
| :::no-loc text="AVer Information A+ Suite":::|
| :::no-loc text="AVS Image Converter":::|
| :::no-loc text="AVS Media Player":::|
| :::no-loc text="AWS SAM command line interface":::|
| :::no-loc text="AWS Session Manager Plugin":::|
| :::no-loc text="AxCrypt":::|
| :::no-loc text="Axel Rietschin Software Developments FastPictureViewer Professional":::|
| :::no-loc text="Axure RP":::|
| :::no-loc text="Azure Functions Core Tools":::|
| :::no-loc text="Bambu Studio":::|
| :::no-loc text="BandiView":::|
| :::no-loc text="Beam Studio":::|
| :::no-loc text="Beats Winlogbeat":::|
| :::no-loc text="Belgium e-ID viewer":::|
| :::no-loc text="Beyond Compare":::|
| :::no-loc text="Beyond Identity":::|
| :::no-loc text="BleachBit":::|
| :::no-loc text="Blender":::|
| :::no-loc text="Blender Foundation Blender":::|
| :::no-loc text="BlueJeans 2":::|
| :::no-loc text="Box CLI":::|
| :::no-loc text="Box Drive":::|
| :::no-loc text="Brady Workstation":::|
| :::no-loc text="BREAK PRO":::|
| :::no-loc text="Bria Enterprise":::|
| :::no-loc text="Bridge Designer 2016":::|
| :::no-loc text="BrightAuthor connected":::|
| :::no-loc text="BrowserStackLocal":::|
| :::no-loc text="Bulk Crap Uninstaller":::|
| :::no-loc text="Bullzip PDF to Word":::|
| :::no-loc text="BurnAware Free":::|
| :::no-loc text="Burp Suite Community Edition":::|
| :::no-loc text="Burp Suite Professional Edition":::|
| :::no-loc text="Business Tax Software BLR":::|
| :::no-loc text="Bytello Share":::|
| :::no-loc text="Calibrite Profiler":::|
| :::no-loc text="Camtasia Studio 2018":::|
| :::no-loc text="Camtasia Studio 2019":::|
| :::no-loc text="Caphyon Advanced Installer":::|
| :::no-loc text="Capture One 20":::|
| :::no-loc text="Capture One 22":::|
| :::no-loc text="Cato Client":::|
| :::no-loc text="Causasoft ExhibitManager":::|
| :::no-loc text="Certify The Web":::|
| :::no-loc text="Charles":::|
| :::no-loc text="Chatbox":::|
| :::no-loc text="Chef Workstation for Windows":::|
| :::no-loc text="Cisco Jabber 14":::|
| :::no-loc text="Cisco Jabber 15":::|
| :::no-loc text="Cisco JVDI Agent 12":::|
| :::no-loc text="Cisco JVDI Agent 14":::|
| :::no-loc text="Cisco JVDI Agent 15":::|
| :::no-loc text="Cisco Webex Meetings":::|
| :::no-loc text="Cisco Webex Productivity Tools":::|
| :::no-loc text="Cisco WebEx Recorder and Player":::|
| :::no-loc text="Cisco WebEx Recording Editor":::|
| :::no-loc text="Cisco Webex Teams":::|
| :::no-loc text="Citrix Receiver":::|
| :::no-loc text="Citrix Workspace app":::|
| :::no-loc text="Citrix Workspace app LTSR":::|
| :::no-loc text="Class":::|
| :::no-loc text="Classic Shell":::|
| :::no-loc text="ClassPoint":::|
| :::no-loc text="ClipboardFusion":::|
| :::no-loc text="ClockAssist":::|
| :::no-loc text="Clockify":::|
| :::no-loc text="Cloud Drive Mapper":::|
| :::no-loc text="CloudCompare":::|
| :::no-loc text="Cloudflare WARP":::|
| :::no-loc text="CloudShow":::|
| :::no-loc text="CMake":::|
| :::no-loc text="CodeMeter Runtime Kit":::|
| :::no-loc text="Colour Contrast Analyser":::|
| :::no-loc text="ComponentAgro CHECK PC2Web":::|
| :::no-loc text="CPU-Z":::|
| :::no-loc text="Creative Force Kelvin":::|
| :::no-loc text="Creative Force Triad":::|
| :::no-loc text="Crestron AirMedia app":::|
| :::no-loc text="Crestron AirMedia Peripheral Installer":::|
| :::no-loc text="CrisisGo App":::|
| :::no-loc text="Cryptomator":::|
| :::no-loc text="Cube Browser":::|
| :::no-loc text="CutePDF Writer":::|
| :::no-loc text="Cyberduck CLI":::|
| :::no-loc text="Dane Prairie Systems Win2PDF":::|
| :::no-loc text="Datadog Agent":::|
| :::no-loc text="DataGrip 1.0":::|
| :::no-loc text="DataGrip 2016.3":::|
| :::no-loc text="DataGrip 2020.3":::|
| :::no-loc text="DataGrip 2021.1":::|
| :::no-loc text="DataGrip 2021.2":::|
| :::no-loc text="DataGrip 2021.3":::|
| :::no-loc text="DataGrip 2022.1":::|
| :::no-loc text="DataGrip 2022.2":::|
| :::no-loc text="DataGrip 2024":::|
| :::no-loc text="DataGrip 2024.1":::|
| :::no-loc text="DataSpell":::|
| :::no-loc text="David Kocher Cyberduck":::|
| :::no-loc text="DAX Studio":::|
| :::no-loc text="DB Browser for SQLite":::|
| :::no-loc text="DBeaver Community":::|
| :::no-loc text="DBeaver Enterprise":::|
| :::no-loc text="DBeaver Lite":::|
| :::no-loc text="DBeaver Ultimate":::|
| :::no-loc text="DbVisualizer":::|
| :::no-loc text="Dedoose Desktop App":::|
| :::no-loc text="Defraggler":::|
| :::no-loc text="Delinea Connection Manager":::|
| :::no-loc text="Dell Command Update":::|
| :::no-loc text="Dell Command Update (Windows Universal Application)":::|
| :::no-loc text="Dell Display Manager":::|
| :::no-loc text="Dell EMC System Update":::|
| :::no-loc text="Dell Peripheral Manager":::|
| :::no-loc text="Dell SupportAssist":::|
| :::no-loc text="Devolutions Launcher":::|
| :::no-loc text="Devolutions Remote Desktop Manager":::|
| :::no-loc text="Devolutions Remote Desktop Manager Agent":::|
| :::no-loc text="Devolutions Workspace":::|
| :::no-loc text="DevPod":::|
| :::no-loc text="digiSeal Reader":::|
| :::no-loc text="DiRoots ProSheets":::|
| :::no-loc text="Directory Opus":::|
| :::no-loc text="DisplayLink Dock Driver":::|
| :::no-loc text="Ditto Connect":::|
| :::no-loc text="dnGrep":::|
| :::no-loc text="Docker Desktop":::|
| :::no-loc text="docuPrinter LT":::|
| :::no-loc text="docuPrinter PRO":::|
| :::no-loc text="docuPrinter TSE":::|
| :::no-loc text="Draftable Desktop":::|
| :::no-loc text="draw.io Desktop":::|
| :::no-loc text="DroidCam Client":::|
| :::no-loc text="dRofus":::|
| :::no-loc text="Druva inSync":::|
| :::no-loc text="Duo Desktop":::|
| :::no-loc text="DYMO ID":::|
| :::no-loc text="Eclipse Temurin JDK with Hotspot 8 (LTS)":::|
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
| :::no-loc text="Eclipse Temurin JRE with Hotspot 8 (LTS)":::|
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
| :::no-loc text="Elgato Stream Deck":::|
| :::no-loc text="Elevate UC":::|
| :::no-loc text="Encrypt.me":::|
| :::no-loc text="Endnote 20":::|
| :::no-loc text="Endnote X8":::|
| :::no-loc text="Endnote X9":::|
| :::no-loc text="Enpass":::|
| :::no-loc text="EnterpriseDB Corporation PostgreSQL 12":::|
| :::no-loc text="ESET Endpoint Antivirus V9":::|
| :::no-loc text="ESET Endpoint Antivirus V10":::|
| :::no-loc text="ESET Endpoint Antivirus V12":::|
| :::no-loc text="ESET Endpoint Encryption":::|
| :::no-loc text="ESET Endpoint Security V9":::|
| :::no-loc text="ESET Endpoint Security V12":::|
| :::no-loc text="Evernote":::|
| :::no-loc text="exacqVision Client":::|
| :::no-loc text="EZB Systems UltraISO":::|
| :::no-loc text="FactSet Workstation":::|
| :::no-loc text="FastPictureViewer Professional":::|
| :::no-loc text="FastStone Soft Capture":::|
| :::no-loc text="FastStone Soft Image Viewer":::|
| :::no-loc text="FastStone Soft Photo Resizer":::|
| :::no-loc text="FileZilla":::|
| :::no-loc text="Filius":::|
| :::no-loc text="FlashFXP":::|
| :::no-loc text="FlexWhere for Desktop":::|
| :::no-loc text="Forté Agent":::|
| :::no-loc text="Fortify":::|
| :::no-loc text="Foxit PDF Editor 11":::|
| :::no-loc text="Foxit PDF Editor 12":::|
| :::no-loc text="Foxit PDF Editor 13":::|
| :::no-loc text="Foxit PDF Editor 2024":::|
| :::no-loc text="Foxit PDF Editor Pro 11":::|
| :::no-loc text="Foxit PDF Editor Pro 11 (Multi-Language)":::|
| :::no-loc text="Foxit PDF Editor Pro 13":::|
| :::no-loc text="Foxit PDF Reader":::|
| :::no-loc text="Foxit PhantomPDF 10":::|
| :::no-loc text="Foxit PhantomPDF Pro 10":::|
| :::no-loc text="Foxit PhantomPDF Pro 10 (Multi-Language)":::|
| :::no-loc text="Frame App":::|
| :::no-loc text="Free Countdown Timer":::|
| :::no-loc text="FreeCAD":::|
| :::no-loc text="Front Desktop":::|
| :::no-loc text="FTP Rush v3":::|
| :::no-loc text="Fusion 2025":::|
| :::no-loc text="Fuzzy Lookup Add-In For Excel":::|
| :::no-loc text="FXHOME HitFilm Express":::|
| :::no-loc text="Gadwin PrintScreen":::|
| :::no-loc text="Gadwin PrintScreenPro":::|
| :::no-loc text="Gadwin ScreenRecorder":::|
| :::no-loc text="Galaxy Modeler":::|
| :::no-loc text="Garden Gnome Package Viewer":::|
| :::no-loc text="Garmin BaseCamp":::|
| :::no-loc text="Garmin Express":::|
| :::no-loc text="General Workings Streamlabs OBS":::|
| :::no-loc text="Genesys Cloud":::|
| :::no-loc text="Genesys Cloud Background Assistant":::|
| :::no-loc text="GeoGebra 5":::|
| :::no-loc text="GeoGebra 6":::|
| :::no-loc text="Geomilieu":::|
| :::no-loc text="Gephi":::|
| :::no-loc text="GIMP":::|
| :::no-loc text="Git":::|
| :::no-loc text="GitHub CLI":::|
| :::no-loc text="GnuPG VS-Desktop":::|
| :::no-loc text="GoAnywhere OpenPGP Studio":::|
| :::no-loc text="Golden 6":::|
| :::no-loc text="Golden 7":::|
| :::no-loc text="Golden 8":::|
| :::no-loc text="GoLand 2017.3":::|
| :::no-loc text="GoLand 2021.1":::|
| :::no-loc text="GoLand 2022.2":::|
| :::no-loc text="GoLand 2024":::|
| :::no-loc text="GoodSync 12":::|
| :::no-loc text="GoodSync Personal":::|
| :::no-loc text="Google Ads Editor":::|
| :::no-loc text="Google Backup and Sync":::|
| :::no-loc text="Google Chrome for Business":::|
| :::no-loc text="Google Chrome Remote Desktop Host":::|
| :::no-loc text="Google Credential Provider for Windows":::|
| :::no-loc text="Google Drive":::|
| :::no-loc text="Google Drive File Stream":::|
| :::no-loc text="Google Go Programming Language 1.16":::|
| :::no-loc text="Google Go Programming Language 1.17":::|
| :::no-loc text="Google Go Programming Language 1.18":::|
| :::no-loc text="Google Go Programming Language 1.19":::|
| :::no-loc text="Google Go Programming Language 1.20":::|
| :::no-loc text="Google Go Programming Language 1.21":::|
| :::no-loc text="Google Go Programming Language 1.22":::|
| :::no-loc text="Google Web Designer":::|
| :::no-loc text="GoTo Connect":::|
| :::no-loc text="Gpg4win":::|
| :::no-loc text="GraphDB Desktop":::|
| :::no-loc text="Graphviz":::|
| :::no-loc text="grepWin":::|
| :::no-loc text="gsudo":::|
| :::no-loc text="HandBrake":::|
| :::no-loc text="Hanword HWP document converter for Microsoft Word 2016":::|
| :::no-loc text="HashTools":::|
| :::no-loc text="HeidiSQL":::|
| :::no-loc text="HIPIN v4":::|
| :::no-loc text="Horizon Collaborate":::|
| :::no-loc text="HP Client Management Script Library":::|
| :::no-loc text="HP Prime Virtual Calculator":::|
| :::no-loc text="Huddle Desktop":::|
| :::no-loc text="HWMonitor":::|
| :::no-loc text="IAP Desktop":::|
| :::no-loc text="Ibis Calculeren voor Bouw":::|
| :::no-loc text="Ibis Calculeren voor Infra":::|
| :::no-loc text="IBM Aspera Connect":::|
| :::no-loc text="IBM Semeru Runtime Open Edition JDK 8 (LTS)":::|
| :::no-loc text="IBM Semeru Runtime Open Edition JDK 11 (LTS)":::|
| :::no-loc text="IBM Semeru Runtime Open Edition JDK 16":::|
| :::no-loc text="IBM Semeru Runtime Open Edition JDK 17 (LTS)":::|
| :::no-loc text="IBM Semeru Runtime Open Edition JDK 18":::|
| :::no-loc text="IBM Semeru Runtime Open Edition JDK 19":::|
| :::no-loc text="IBM Semeru Runtime Open Edition JDK 20":::|
| :::no-loc text="IBM Semeru Runtime Open Edition JDK 22":::|
| :::no-loc text="IBM Semeru Runtime Open Edition JRE 8 (LTS)":::|
| :::no-loc text="IBM Semeru Runtime Open Edition JRE 11 (LTS)":::|
| :::no-loc text="IBM Semeru Runtime Open Edition JRE 17 (LTS)":::|
| :::no-loc text="IBM Semeru Runtime Open Edition JRE 18":::|
| :::no-loc text="IBM Semeru Runtime Open Edition JRE 19":::|
| :::no-loc text="IBM Semeru Runtime Open Edition JRE 20":::|
| :::no-loc text="IBM Semeru Runtime Open Edition JRE 22":::|
| :::no-loc text="IcedTea-Web":::|
| :::no-loc text="ImageGlass":::|
| :::no-loc text="iMazing Converter":::|
| :::no-loc text="Image-Line Software FL Studio":::|
| :::no-loc text="ImpExpPro":::|
| :::no-loc text="Infix PDF Editor":::|
| :::no-loc text="Inkscape":::|
| :::no-loc text="Inmatrix Zoom Player Max":::|
| :::no-loc text="Install4j":::|
| :::no-loc text="Intermedia Unite":::|
| :::no-loc text="IrfanView":::|
| :::no-loc text="IronPython":::|
| :::no-loc text="IronPython 2.7":::|
| :::no-loc text="IsoBuster":::|
| :::no-loc text="iZotope RX Advanced 10":::|
| :::no-loc text="Jabra Direct":::|
| :::no-loc text="JAM Software TreeSize Free":::|
| :::no-loc text="JAWS 2025":::|
| :::no-loc text="JetBrains dotUltimate 2022":::|
| :::no-loc text="JetBrains dotUltimate 2023":::|
| :::no-loc text="JetBrains dotUltimate 2024":::|
| :::no-loc text="JetBrains ReSharper 2023.1":::|
| :::no-loc text="Joplin":::|
| :::no-loc text="JProfiler":::|
| :::no-loc text="BCF Manager for Tekla":::|
| :::no-loc text="KDiff3":::|
| :::no-loc text="KeePass Password Safe (Classic Edition)":::|
| :::no-loc text="KeePassXC":::|
| :::no-loc text="Keeper":::|
| :::no-loc text="KeeWeb":::|
| :::no-loc text="Kerio Connect":::|
| :::no-loc text="KeyShot Studio":::|
| :::no-loc text="KeyStore Explorer":::|
| :::no-loc text="KNIME Analytics Platform":::|
| :::no-loc text="Kobo":::|
| :::no-loc text="Kodu Game Lab":::|
| :::no-loc text="Konnekt":::|
| :::no-loc text="Kotobee Author":::|
| :::no-loc text="Kotobee Reader":::|
| :::no-loc text="Kovid Goyal Calibre":::|
| :::no-loc text="KPN Desktop Integratie":::|
| :::no-loc text="Kreya":::|
| :::no-loc text="Krisp":::|
| :::no-loc text="Krita":::|
| :::no-loc text="Lansweeper":::|
| :::no-loc text="Lark Deployment Tool":::|
| :::no-loc text="Laserbox basic":::|
| :::no-loc text="LastPass":::|
| :::no-loc text="LEGO Education SPIKE":::|
| :::no-loc text="Lenovo Accessories and Display Manager":::|
| :::no-loc text="Lenovo Quick Clean":::|
| :::no-loc text="Lens Desktop":::|
| :::no-loc text="Liberica JDK":::|
| :::no-loc text="Lifelong Kindergarten Group Scratch":::|
| :::no-loc text="LINQPad 5":::|
| :::no-loc text="LiquidFiles Outlook Plugin":::|
| :::no-loc text="Liquit Workspace Agent 3":::|
| :::no-loc text="Local Administrator Password Solution":::|
| :::no-loc text="Logi Tune":::|
| :::no-loc text="Logitech Bolt":::|
| :::no-loc text="Logitech Camera Settings":::|
| :::no-loc text="Logitech Options":::|
| :::no-loc text="Logitech Presentation":::|
| :::no-loc text="Logitech SetPoint":::|
| :::no-loc text="Logitech Sync App":::|
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
| :::no-loc text="MatterControl":::|
| :::no-loc text="Mattermost Desktop":::|
| :::no-loc text="Maxcut":::|
| :::no-loc text="MAXQDA 2020 Reader":::|
| :::no-loc text="Memento Desktop Edition":::|
| :::no-loc text="Mendeley Desktop":::|
| :::no-loc text="Mendeley Reference Manager":::|
| :::no-loc text="Mendix 9":::|
| :::no-loc text="Mersive Solstice Client":::|
| :::no-loc text="Meta Quest Developer Hub":::|
| :::no-loc text="Meta Spark Player":::|
| :::no-loc text="Meteor Modeler":::|
| :::no-loc text="Microsoft .NET Core 2.2":::|
| :::no-loc text="Microsoft .NET Desktop Runtime 6.0":::|
| :::no-loc text="Microsoft .NET Desktop Runtime 7.0":::|
| :::no-loc text="Microsoft .NET Runtime 6.0":::|
| :::no-loc text="Microsoft .NET Runtime 7.0":::|
| :::no-loc text="Microsoft .NET SDK 9.0":::|
| :::no-loc text="Microsoft Access Database Engine 2016":::|
| :::no-loc text="Microsoft Active Directory Rights Management Service Client":::|
| :::no-loc text="Microsoft Analysis Management Objects":::|
| :::no-loc text="Microsoft Analysis Services ADOMD.NET":::|
| :::no-loc text="Microsoft Analysis Services OLE DB Provider":::|
| :::no-loc text="Microsoft ASP.NET Core Runtime 5.0":::|
| :::no-loc text="Microsoft ASP.NET Core Runtime 6.0":::|
| :::no-loc text="Microsoft ASP.NET Core Runtime 7.0":::|
| :::no-loc text="Microsoft Azure CLI":::|
| :::no-loc text="Microsoft Azure Connected Machine Agent":::|
| :::no-loc text="Microsoft Azure Data CLI":::|
| :::no-loc text="Microsoft Azure Data Studio":::|
| :::no-loc text="Microsoft Azure Information Protection client":::|
| :::no-loc text="Microsoft Azure PowerShell":::|
| :::no-loc text="Microsoft Azure Storage Explorer":::|
| :::no-loc text="Microsoft Bot Framework Composer":::|
| :::no-loc text="Microsoft Bot Framework Emulator":::|
| :::no-loc text="Microsoft Defender for Endpoint plug-in for WSL":::|
| :::no-loc text="Microsoft Deployment Toolkit (8456)":::|
| :::no-loc text="Microsoft Enterprise Mode Site List Manager":::|
| :::no-loc text="Microsoft ODBC Driver 13 for SQL Server":::|
| :::no-loc text="Microsoft ODBC Driver 17 for SQL Server":::|
| :::no-loc text="Microsoft OLE DB Driver 18 for SQL Server":::|
| :::no-loc text="Microsoft On-premises data gateway":::|
| :::no-loc text="Microsoft OneNote":::|
| :::no-loc text="Microsoft Power BI Desktop":::|
| :::no-loc text="Microsoft PowerShell Core":::|
| :::no-loc text="Microsoft PowerToys":::|
| :::no-loc text="Microsoft Purview Information Protection client":::|
| :::no-loc text="Microsoft Remote Desktop WebRTC Redirector":::|
| :::no-loc text="Microsoft Remote Help":::|
| :::no-loc text="Microsoft Skype for Desktop":::|
| :::no-loc text="Microsoft Skype TX":::|
| :::no-loc text="Microsoft SQL Server 2012 Express with Advanced Services":::|
| :::no-loc text="Microsoft SQL Server 2012 Native Client":::|
| :::no-loc text="Microsoft SQL Server 2014 Express LocalDB":::|
| :::no-loc text="Microsoft SQL Server 2016 Report Builder":::|
| :::no-loc text="Microsoft SQL Server 2017 Express Advanced Edition":::|
| :::no-loc text="Microsoft SQL Server 2017 for Microsoft Windows Latest Cumulative Update":::|
| :::no-loc text="Microsoft SQL Server 2017 Reporting Services":::|
| :::no-loc text="Microsoft SQL Server 2022 Express Edition":::|
| :::no-loc text="Microsoft SQL Server Management Studio 20":::|
| :::no-loc text="Microsoft Surface Data Eraser":::|
| :::no-loc text="Microsoft Surface Diagnostic Toolkit for Business":::|
| :::no-loc text="Microsoft System CLR Types for SQL Server 2014":::|
| :::no-loc text="Microsoft Universal Print Connector":::|
| :::no-loc text="Microsoft Visio 2016 Viewer":::|
| :::no-loc text="Microsoft Visual C++ 2005 Redistributable":::|
| :::no-loc text="Microsoft Visual C++ 2008 Redistributable":::|
| :::no-loc text="Microsoft Visual C++ 2012 Redistributable":::|
| :::no-loc text="Microsoft Visual C++ 2015-2022 Redistributable":::|
| :::no-loc text="Microsoft Visual Studio 2010 Tools for Office Runtime":::|
| :::no-loc text="Microsoft Visual Studio 2022 Community":::|
| :::no-loc text="Microsoft Visual Studio 2022 Enterprise":::|
| :::no-loc text="Microsoft Visual Studio 2022 Professional":::|
| :::no-loc text="Microsoft Visual Studio Code":::|
| :::no-loc text="Microsoft Visual Studio Team Explorer 2022":::|
| :::no-loc text="Microsoft Windows Admin Center":::|
| :::no-loc text="Microsoft Windows Assessment and Deployment Kit (ADK) for Windows 10 update 1607":::|
| :::no-loc text="Microsoft Windows Assessment and Deployment Kit (ADK) for Windows 10 update 1803":::|
| :::no-loc text="Microsoft Windows Assessment and Deployment Kit (ADK) for Windows 10 update 1809":::|
| :::no-loc text="Microsoft Windows Assessment and Deployment Kit (ADK) for Windows 10 update 1903":::|
| :::no-loc text="Microsoft Windows Assessment and Deployment Kit (ADK) for Windows 10 update 2004":::|
| :::no-loc text="Microsoft Windows Assessment and Deployment Kit (ADK) for Windows 11":::|
| :::no-loc text="Microsoft Windows PE add-on for ADK for Windows 10 update 1809":::|
| :::no-loc text="Microsoft Windows PE add-on for ADK for Windows 11":::|
| :::no-loc text="Mitel miCollab":::|
| :::no-loc text="Mobirise":::|
| :::no-loc text="Mocha TN3270":::|
| :::no-loc text="Mocha TN3812":::|
| :::no-loc text="Mocha TN5250":::|
| :::no-loc text="monday":::|
| :::no-loc text="MongoDB Compass":::|
| :::no-loc text="MongoDB Compass Isolated Edition":::|
| :::no-loc text="MongoDB Compass Readonly Edition":::|
| :::no-loc text="Moon Modeler":::|
| :::no-loc text="MOOS Project Viewer":::|
| :::no-loc text="Morphic":::|
| :::no-loc text="Mozilla Firefox":::|
| :::no-loc text="Mozilla Firefox ESR 102":::|
| :::no-loc text="Mozilla Firefox ESR 115":::|
| :::no-loc text="Mozilla FrontMotion Firefox Community Edition":::|
| :::no-loc text="Mozilla FrontMotion Firefox Community Edition ESR":::|
| :::no-loc text="Mozilla SeaMonkey":::|
| :::no-loc text="Mozilla Thunderbird":::|
| :::no-loc text="mPollux DigiSign Client":::|
| :::no-loc text="MSEndpointMgr Intune Debug Toolkit":::|
| :::no-loc text="MSIX Core":::|
| :::no-loc text="Multilogin":::|
| :::no-loc text="MuseScore 3":::|
| :::no-loc text="MuseScore Studio 4":::|
| :::no-loc text="Nagstamon":::|
| :::no-loc text="NAPS2":::|
| :::no-loc text="NCPA":::|
| :::no-loc text="Nessus Agent 10":::|
| :::no-loc text="NetBird":::|
| :::no-loc text="NetLogo":::|
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
| :::no-loc text="NoMachine":::|
| :::no-loc text="NoMachine Enterprise Client":::|
| :::no-loc text="NoMachine Enterprise Desktop":::|
| :::no-loc text="NoMachine Fonts Others":::|
| :::no-loc text="NordLayer":::|
| :::no-loc text="Notepad++":::|
| :::no-loc text="NV Access NVDA":::|
| :::no-loc text="NVIDIA GeForce Experience":::|
| :::no-loc text="NVivo 12":::|
| :::no-loc text="NVivo 13":::|
| :::no-loc text="NWEA Secure Testing Browser":::|
| :::no-loc text="Obsidian":::|
| :::no-loc text="ocenaudio":::|
| :::no-loc text="Oh My Posh":::|
| :::no-loc text="OnSIP":::|
| :::no-loc text="OpenAudible":::|
| :::no-loc text="OpenDNS Umbrella Roaming Client":::|
| :::no-loc text="OpenJDK 11":::|
| :::no-loc text="OpenJDK 16":::|
| :::no-loc text="OpenJDK 17":::|
| :::no-loc text="OpenJDK 21":::|
| :::no-loc text="OpenLens":::|
| :::no-loc text="OpenShot Video Editor":::|
| :::no-loc text="OpenVPN":::|
| :::no-loc text="OpenVPN Connect":::|
| :::no-loc text="OpenWebStart":::|
| :::no-loc text="Oracle Java Runtime Environment Version 8":::|
| :::no-loc text="Oracle Java SE Development Kit 17":::|
| :::no-loc text="Oracle Java SE Development Kit 23":::|
| :::no-loc text="Oracle MySQL Connector Net 8.0":::|
| :::no-loc text="Oracle MySQL Connector NET 9":::|
| :::no-loc text="Oracle MySQL Installer 8 for Windows":::|
| :::no-loc text="OrcaSlicer":::|
| :::no-loc text="ownCloud Desktop Client":::|
| :::no-loc text="Pandoc":::|
| :::no-loc text="PaperCut MF":::|
| :::no-loc text="PaperCut Mobility Print":::|
| :::no-loc text="PaperCut NG":::|
| :::no-loc text="Paperpile":::|
| :::no-loc text="Parallels Client 18":::|
| :::no-loc text="Parallels Client 19":::|
| :::no-loc text="Parallels Toolbox":::|
| :::no-loc text="Password Safe 3":::|
| :::no-loc text="Path Copy Copy":::|
| :::no-loc text="Pausit Launcher":::|
| :::no-loc text="PDF Studio":::|
| :::no-loc text="PDF Studio Viewer":::|
| :::no-loc text="PDF24 Creator":::|
| :::no-loc text="PDFCreator":::|
| :::no-loc text="pdfFiller":::|
| :::no-loc text="PDFgear":::|
| :::no-loc text="PDFsam Basic":::|
| :::no-loc text="PDFsam Visual":::|
| :::no-loc text="PDF-Tools":::|
| :::no-loc text="PDF-XChange PRO":::|
| :::no-loc text="PeaZip":::|
| :::no-loc text="PerformanceTest":::|
| :::no-loc text="Perky Duck":::|
| :::no-loc text="Pexip":::|
| :::no-loc text="Pexip Infinity Connect":::|
| :::no-loc text="pgAdmin 4":::|
| :::no-loc text="PicPick":::|
| :::no-loc text="Pidgin":::|
| :::no-loc text="Piriform CCleaner":::|
| :::no-loc text="Piriform CCleaner Slim":::|
| :::no-loc text="PL SQL Developer 15":::|
| :::no-loc text="PLEdit 7":::|
| :::no-loc text="PlanGrid":::|
| :::no-loc text="Plex Media Player":::|
| :::no-loc text="Plex Media Server":::|
| :::no-loc text="Poll Everywhere":::|
| :::no-loc text="Poly Lens Desktop App":::|
| :::no-loc text="Power BI ALM Toolkit":::|
| :::no-loc text="Preform":::|
| :::no-loc text="PrinterLogic Printer Installer Client":::|
| :::no-loc text="Private Internet Access":::|
| :::no-loc text="PrivadoVPN":::|
| :::no-loc text="proCertum SmartSign SimplySign Desktop":::|
| :::no-loc text="Project Plan 365":::|
| :::no-loc text="Project Viewer 365":::|
| :::no-loc text="Proton VPN":::|
| :::no-loc text="PRTG Desktop":::|
| :::no-loc text="PSPad":::|
| :::no-loc text="Publish or Perish":::|
| :::no-loc text="Puppet Development Kit":::|
| :::no-loc text="Publisher Select 3":::|
| :::no-loc text="Putty":::|
| :::no-loc text="PuTTY CAC":::|
| :::no-loc text="Python 3.7":::|
| :::no-loc text="Python 3.8":::|
| :::no-loc text="Python 3.9":::|
| :::no-loc text="Python 3.10":::|
| :::no-loc text="Python 3.11":::|
| :::no-loc text="Python 3.12":::|
| :::no-loc text="Python 3.13":::|
| :::no-loc text="QGIS":::|
| :::no-loc text="QGIS LTR":::|
| :::no-loc text="QNAP Qsync":::|
| :::no-loc text="Qurentis":::|
| :::no-loc text="R for Windows":::|
| :::no-loc text="RadiAnt DICOM viewer":::|
| :::no-loc text="Rainmeter":::|
| :::no-loc text="Rancher Desktop":::|
| :::no-loc text="Rarlab WinRAR":::|
| :::no-loc text="Raspberry Pi Imager":::|
| :::no-loc text="RBTools":::|
| :::no-loc text="Red Hat OpenJDK":::|
| :::no-loc text="Red Hat OpenJDK JRE":::|
| :::no-loc text="ReluxDesktop":::|
| :::no-loc text="Remote Ripple":::|
| :::no-loc text="RenderDoc":::|
| :::no-loc text="REAPER":::|
| :::no-loc text="REV Hardware Client":::|
| :::no-loc text="RingCentral App":::|
| :::no-loc text="RingCentral Phone":::|
| :::no-loc text="Robo 3T":::|
| :::no-loc text="RoboForm":::|
| :::no-loc text="Rocket.Chat":::|
| :::no-loc text="Royal TS 5":::|
| :::no-loc text="Royal TS 6":::|
| :::no-loc text="Royal TS 7":::|
| :::no-loc text="RStudio 1.4":::|
| :::no-loc text="RStudio 2022":::|
| :::no-loc text="RStudio 2023":::|
| :::no-loc text="Rstudio 2024":::|
| :::no-loc text="RustDesk":::|
| :::no-loc text="RVTools":::|
| :::no-loc text="Salesforce CLI sf v2":::|
| :::no-loc text="Samsung Smart Switch":::|
| :::no-loc text="Samsung Smart View":::|
| :::no-loc text="Saola Animate":::|
| :::no-loc text="ScaleFT":::|
| :::no-loc text="Screen InStyle":::|
| :::no-loc text="ScreenBeam Conference":::|
| :::no-loc text="ScreenCloud Player":::|
| :::no-loc text="ScreenToGif":::|
| :::no-loc text="Sejda PDF Desktop":::|
| :::no-loc text="SelfGuide Recorder":::|
| :::no-loc text="SharePoint Online Management Shell":::|
| :::no-loc text="Shotcut":::|
| :::no-loc text="SHOTPlus 6":::|
| :::no-loc text="SHOTPlus Tunnel":::|
| :::no-loc text="SHOTPlus Underground":::|
| :::no-loc text="SideQuest":::|
| :::no-loc text="Signiant App":::|
| :::no-loc text="Simon Tatham Putty":::|
| :::no-loc text="Simple Sticky Notes":::|
| :::no-loc text="Simplenote":::|
| :::no-loc text="Sketchup Pro 2024":::|
| :::no-loc text="Sketchup Pro 2025":::|
| :::no-loc text="Skillbrains LightShot":::|
| :::no-loc text="Slido":::|
| :::no-loc text="SMath Studio":::|
| :::no-loc text="SmartFTP Client":::|
| :::no-loc text="Smartsheet desktop app":::|
| :::no-loc text="SnapCAD":::|
| :::no-loc text="SnapGene Viewer":::|
| :::no-loc text="Snagit 2018":::|
| :::no-loc text="Snagit 2019":::|
| :::no-loc text="Snagit 2020":::|
| :::no-loc text="Snagit 2021":::|
| :::no-loc text="Snagit 2023":::|
| :::no-loc text="Snagit 2024":::|
| :::no-loc text="Snapform Viewer":::|
| :::no-loc text="Snapmaker Luban":::|
| :::no-loc text="SnelStart":::|
| :::no-loc text="SoapUI":::|
| :::no-loc text="Softerra LDAP Administrator":::|
| :::no-loc text="Softerra LDAP Browser":::|
| :::no-loc text="Softland doPDF":::|
| :::no-loc text="SolarWinds Orion SDK":::|
| :::no-loc text="SonicWall Connect Tunnel":::|
| :::no-loc text="SonicWall NetExtender":::|
| :::no-loc text="Sophos Connect":::|
| :::no-loc text="South River Technologies WebDrive":::|
| :::no-loc text="Spark AR Player for Desktop":::|
| :::no-loc text="Splashtop Business":::|
| :::no-loc text="Squirrels Reflector 3":::|
| :::no-loc text="Squirrels Reflector 4":::|
| :::no-loc text="SRWare Iron":::|
| :::no-loc text="Steam":::|
| :::no-loc text="Stellarium":::|
| :::no-loc text="Storyboarder":::|
| :::no-loc text="Striata Reader":::|
| :::no-loc text="SuperOffice WebTools":::|
| :::no-loc text="SURF eduVPN Client":::|
| :::no-loc text="SURFdrive":::|
| :::no-loc text="Symphony Desktop Application":::|
| :::no-loc text="SyncBackFree":::|
| :::no-loc text="SyncBackPro":::|
| :::no-loc text="Synology Cloud Station Backup":::|
| :::no-loc text="Synology Cloud Station Drive":::|
| :::no-loc text="Synology Drive Client":::|
| :::no-loc text="Synology Evidence Integrity Authenticator":::|
| :::no-loc text="Sysprogs SmarTTY":::|
| :::no-loc text="Tabular Editor 2":::|
| :::no-loc text="TablePlus":::|
| :::no-loc text="Tableau Desktop 2022":::|
| :::no-loc text="Tableau Prep Builder 2022":::|
| :::no-loc text="Tableau Prep Builder 2023":::|
| :::no-loc text="Tailscale":::|
| :::no-loc text="Talkdesk":::|
| :::no-loc text="TDP SecureAnyBox Agent":::|
| :::no-loc text="TDP SecureAnyBox Launcher":::|
| :::no-loc text="TeamCity":::|
| :::no-loc text="TeamDrive":::|
| :::no-loc text="TeamSpeak client":::|
| :::no-loc text="TeamViewer Host":::|
| :::no-loc text="TED Notepad":::|
| :::no-loc text="TELUS Business Connect Phone":::|
| :::no-loc text="Temperature Technology T-TEC":::|
| :::no-loc text="Teracopy for Windows":::|
| :::no-loc text="TextExpander":::|
| :::no-loc text="TGRMN Software Bulk Rename Utility":::|
| :::no-loc text="The Document Foundation LibreOffice 6.2":::|
| :::no-loc text="The Document Foundation LibreOffice 6.3":::|
| :::no-loc text="The Document Foundation LibreOffice 6.4":::|
| :::no-loc text="The Document Foundation LibreOffice 7.4":::|
| :::no-loc text="The Document Foundation LibreOffice 7.4 Help Pack":::|
| :::no-loc text="The Document Foundation LibreOffice 7.5":::|
| :::no-loc text="The Document Foundation LibreOffice 7.5 Help Pack":::|
| :::no-loc text="The Document Foundation LibreOffice 7.5 SDK":::|
| :::no-loc text="The Document Foundation LibreOffice 24":::|
| :::no-loc text="The Document Foundation LibreOffice 24 Help Pack":::|
| :::no-loc text="ThinkPad TrackPoint Keyboard II Software":::|
| :::no-loc text="Thonny":::|
| :::no-loc text="Thycotic Application Control Agent":::|
| :::no-loc text="Thycotic Directory Services Agent":::|
| :::no-loc text="Thycotic Local Security Agent":::|
| :::no-loc text="Tidio":::|
| :::no-loc text="TightVNC":::|
| :::no-loc text="TI-Nspire CX CAS Student Software":::|
| :::no-loc text="TI-Nspire CX Premium Teacher Software":::|
| :::no-loc text="TI-SmartView CE-T":::|
| :::no-loc text="Topaz SigPlusExtLite":::|
| :::no-loc text="TortoiseGit":::|
| :::no-loc text="TortoiseSVN":::|
| :::no-loc text="TortoiseSVN ipv6":::|
| :::no-loc text="TortoiseHg":::|
| :::no-loc text="TransIP STACK":::|
| :::no-loc text="Tribler":::|
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
| :::no-loc text="Ultimaker Cura":::|
| :::no-loc text="UltraMon":::|
| :::no-loc text="UltraVNC":::|
| :::no-loc text="UltraViewer":::|
| :::no-loc text="UNIVERGE BLUE CONNECT":::|
| :::no-loc text="Unity Hub":::|
| :::no-loc text="UrBackup Client":::|
| :::no-loc text="Vagrant":::|
| :::no-loc text="VariCAD":::|
| :::no-loc text="VariCAD Viewer":::|
| :::no-loc text="VeraCrypt":::|
| :::no-loc text="VEXcode IQ 3":::|
| :::no-loc text="VEXcode V5":::|
| :::no-loc text="VideoScribe":::|
| :::no-loc text="Vim":::|
| :::no-loc text="Visual Paradigm Project Viewer":::|
| :::no-loc text="VMware Horizon Client 4.5":::|
| :::no-loc text="VMware Horizon Client 4.6":::|
| :::no-loc text="VMware Horizon Client 4.7":::|
| :::no-loc text="VMware Horizon Client 4.8.1":::|
| :::no-loc text="VMware Horizon Client 5.0":::|
| :::no-loc text="VMware Horizon Client 5.2":::|
| :::no-loc text="VMware Horizon Client 5.3":::|
| :::no-loc text="VMware Horizon Client 5.4.2":::|
| :::no-loc text="VMware Horizon Client 5.4.3":::|
| :::no-loc text="VMware Horizon Client 5.5":::|
| :::no-loc text="VMware Horizon Client 2006":::|
| :::no-loc text="VMware Horizon Client 2012":::|
| :::no-loc text="VMware Horizon Client 2103":::|
| :::no-loc text="VMware Horizon Client 2209":::|
| :::no-loc text="VMware Horizon View Client 3.5":::|
| :::no-loc text="VMware Horizon View Client 5.4":::|
| :::no-loc text="voidtools Everything":::|
| :::no-loc text="voidtools Everything Lite":::|
| :::no-loc text="VSCodium":::|
| :::no-loc text="Waterfox":::|
| :::no-loc text="Waterfox Classic":::|
| :::no-loc text="Wazuh Agent":::|
| :::no-loc text="Webstorm 2022.2":::|
| :::no-loc text="WebStorm 2024":::|
| :::no-loc text="Western Digital Dashboard":::|
| :::no-loc text="Wildix Collaboration":::|
| :::no-loc text="Win10Pcap":::|
| :::no-loc text="Wind Financial Terminal":::|
| :::no-loc text="WinDirStat":::|
| :::no-loc text="Windows 10 Codec Pack":::|
| :::no-loc text="WinMerge":::|
| :::no-loc text="WinSCP":::|
| :::no-loc text="WireGuard":::|
| :::no-loc text="Wireshark 4.4":::|
| :::no-loc text="WiX Toolset 3":::|
| :::no-loc text="WizTree":::|
| :::no-loc text="Wrike":::|
| :::no-loc text="Xamarin Mono for Windows":::|
| :::no-loc text="Xink Client AD":::|
| :::no-loc text="XMind 2020":::|
| :::no-loc text="XMind 2021":::|
| :::no-loc text="XMind 2022":::|
| :::no-loc text="XMind Ltd XMind 2020":::|
| :::no-loc text="XMind Ltd XMind 2021":::|
| :::no-loc text="XnSoft XnConvert":::|
| :::no-loc text="XnSoft XnShell":::|
| :::no-loc text="XnSoft XnView Extended":::|
| :::no-loc text="XnSoft XnView Minimal":::|
| :::no-loc text="XnSoft XnView MP":::|
| :::no-loc text="XnSoft XnView Standard":::|
| :::no-loc text="Yubico Authenticator":::|
| :::no-loc text="Yubico PIV Tool":::|
| :::no-loc text="YubiKey Manager CLI":::|
| :::no-loc text="ZAC":::|
| :::no-loc text="ZBrush":::|
| :::no-loc text="Zeal":::|
| :::no-loc text="Zello":::|
| :::no-loc text="Zivver Office Plugin":::|
| :::no-loc text="Zoho WorkDrive":::|
| :::no-loc text="Zoom Client for Meetings":::|
| :::no-loc text="Zoom Player":::|
| :::no-loc text="Zoom Player Max":::|
| :::no-loc text="Zoom Plugin for Microsoft Outlook":::|
| :::no-loc text="Zoom Plugin for Skype for Business":::|
| :::no-loc text="Zoom Plugin for Windows Virtual Desktop Client":::|
| :::no-loc text="Zoom Rooms":::|
| :::no-loc text="Zoom VDI Universal Plugin":::|
| :::no-loc text="Zorus Archon Agent":::|
| :::no-loc text="Zotero":::|
| :::no-loc text="Zscaler Client Connector 3.6":::|
| :::no-loc text="Zscaler Client Connector 3.9":::|
| :::no-loc text="Zscaler Client Connector 4.0":::|
| :::no-loc text="Zscaler Client Connector 4.1":::|
| :::no-loc text="Zscaler Client Connector 4.3":::|
| :::no-loc text="Zscaler Client Connector for VDI":::|
| :::no-loc text="Zulip":::|
| :::no-loc text="Zulu JDK 6 (LTS)":::|
| :::no-loc text="Zulu JDK 7 (LTS)":::|
| :::no-loc text="Zulu JDK 8 (LTS)":::|
| :::no-loc text="Zulu JDK 9 (STS)":::|
| :::no-loc text="Zulu JDK 10 (STS)":::|
| :::no-loc text="Zulu JDK 11 (LTS)":::|
| :::no-loc text="Zulu JDK 12 (STS)":::|
| :::no-loc text="Zulu JDK 13 (MTS)":::|
| :::no-loc text="Zulu JDK 15 (MTS)":::|
| :::no-loc text="Zulu JDK 16 (STS)":::|
| :::no-loc text="Zulu JDK 17 (LTS)":::|
| :::no-loc text="Zulu JDK 18 (STS)":::|
| :::no-loc text="Zulu JDK 20 (STS)":::|
| :::no-loc text="Zulu JRE 7 (LTS)":::|
| :::no-loc text="Zulu JRE 8 (LTS)":::|
| :::no-loc text="Zulu JRE 11 (LTS)":::|
| :::no-loc text="Zulu JRE 12 (STS)":::|
| :::no-loc text="Zulu JRE 13 (MTS)":::|
| :::no-loc text="Zulu JRE 15 (MTS)":::|
| :::no-loc text="Zulu JRE 17 (LTS)":::|

## Next steps

- [Add an Enterprise App Catalog app to Microsoft Intune](../apps/apps-add-enterprise-app.md)
- [Monitor app information and assignments with Microsoft Intune](apps-monitor.md)
- [Troubleshoot Win32 app issues](apps-win32-troubleshoot.md)
