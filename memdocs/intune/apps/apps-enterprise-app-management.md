---
title: Microsoft Intune Enterprise Application Management
titleSuffix:
description: Learn about Enterprise App Management and the Enterprise App Catalog in Microsoft Intune. 
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 02/08/2024
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

The benefits of using Enterprise App Management are the following:

- **Streamlined app management**: You can save time and reduce complexity by streamlining the app management process. Discover and add apps directly from the Intune console.
- **Stay current with updates**: You're able to keep apps up-to-date by easily creating apps for the new versions of products as they're available in the catalog.

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

You can also configure app specific rules used to detect the presence of the Enterprise App Catalog app where you can choose to either manually configure the detection rules or use a custom script to detect the presence of the app before installing the app.

## Self-updating apps

The Enterprise App Catalog includes apps that self update. Intune will ensure the app is at least at a target minimum version, and will consider the app installed if the detected version of the app is at or above the minimum version. Self-updating apps update on client devices based on the vendor's process. Intune will report the version of the app detected on the device.

> [!IMPORTANT]
> Self-updating apps may require that your tenant has network rules configured to allow an update from the app vendor.

## Frequently asked questions (FAQ)

### How can I request to add an application the Enterprise App Catalog?

If you aren't already working with a Microsoft contact, fill out the [Enterprise app management app catalog request](https://aka.ms/EAM/AppRequest) form.

> [!IMPORTANT]
> Microsoft makes no guarantee, express or implied, with respect to adding a requested app to the Enterprise App Catalog. Once the submission is reviewed using the form provided above, the app may or may not be added to the Enterprise App Catalog. Microsoft does not offer or assume any Service Level Agreement (SLA) or timeline with regard to adding an app to the Enterprise App Catalog.

### Where are the devices downloading the app content from?

Microsoft hosts the applications in Microsoft storage.

### Is Microsoft providing security around any of the content provided in the Enterprise App Catalog?

No. Microsoft makes no guarantee, express or implied, with respect to the security and compliance of the applications provided in the Enterprise App Catalog.

### What app installer types are in the Enterprise App Catalog?

The apps currently provided in the Enterprise application catalog are Windows Win32 applications (exe and msi).

### How will Microsoft detect if an application from the Enterprise App Catalog is in use?

At this time, Intune provides no running application detection.

### What is the Service Level Agreement (SLA) for when an app update is available in the catalog?

No SLA is currently available.

### How many applications are in the catalog?

At the time of general availability (GA), Microsoft expects to have 100 applications available in the Enterprise App Catalog. Additional apps will be available on an on-going basis.

### How can working with the applications in Enterprise App Catalog be automated?

Graph API will be available soon after general availability.

### Will Enterprise catalog apps automatically update to a new version when a new version is available in the Enterprise app catalog?

No, the created app will remain at the version it was created at so the IT Pro can have full control over the experience.

### Can you get licensed applications from this catalog?

Yes. You can get licensed applications from the Enterprise App Catalog, although you're responsible for purchasing the license from the vendor and distributing it to your organization. Intune doesn't perform a license check on Enterprise App Catalog apps.

### Can Enterprise App Management be purchased standalone?

Yes. Enterprise App Management can be purchased as a standalone SKU or as part of the Microsoft Intune Suite.

### Can Enterprise App Management be leveraged with Microsoft Configuration Manager?

Enterprise App Management is only provided by Microsoft Intune. Configuration Manager doesn't directly support Enterprise App Management apps, however co-managed clients can get Enterprise App Catalog apps when targeted from Microsoft Intune.

### Does Enterprise App Management use **Winget**?

No. Enterprise App Catalog apps are directly installed by the Intune management extension (IME).

### How do I update my Enterprise App Catalog app?

You can configure what experience you want related to uninstalling the previous version, however the behavior of the application upgrade is controlled by the vendor. 

### After several hours, what can I do if my app continues to show that it isn't ready and that the requested content is still being prepared?

If the app content hasn't synced after several hours, delete the app and try again.

## Apps available in the Enterprise App Catalog

There are various applications available in the Enterprise App Catalog. To view the current application list in [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), see [Add a Windows catalog app (Win32) to Intune](../apps/apps-add-enterprise-app.md#add-a-windows-catalog-app-win32-to-intune).

> [!NOTE]
> Additional apps will be available on an on-going basis in the Enterprise App Catalog.

The following table of Enterprise Apps is available within Intune:

| App |
|---|
| 7-Zip |
| Amazon AWS Tools for Windows |
| Amazon Corretto 16 |
| Amazon Kindle |
| Android Studio 2022 |
| Android Studio 3 |
| Android Studio 4 |
| Araxis Merge |
| Artweaver Free |
| Atomi Systems ActivePresenter |
| Audacity |
| Beyond Compare |
| Blender |
| BlueJeans 2 |
| Brady Workstation |
| Burp Suite Community Edition |
| Burp Suite Professional Edition |
| Calibre |
| Cisco Jabber 14 |
| Cisco Webex Meetings |
| Cisco WebEx Recorder and Player |
| Cisco WebEx Recording Editor |
| Cisco Webex Teams |
| Citrix Receiver |
| Citrix Workspace app |
| Citrix Workspace app LTSR |
| CMake |
| Dell Command Update (Windows Universal   Application) |
| Docker Desktop |
| draw.io Desktop |
| Duo Desktop |
| Eclipse Temurin JDK with Hotspot 11 (LTS) |
| Eclipse Temurin JDK with Hotspot 19 |
| Eclipse Temurin JRE with Hotspot 11 (LTS) |
| Eclipse Temurin JRE with Hotspot 19 |
| Egnyte Connect Desktop App |
| Egnyte WebEdit |
| Evernote |
| Foxit PDF Editor 11 |
| Foxit PDF Editor 12 |
| Foxit PDF Reader |
| Frame App |
| Free Countdown Timer |
| Google Chrome for Business |
| Google Drive |
| Inkscape |
| JAM Software TreeSize Free |
| KeePass Password Safe (Classic Edition) |
| KeePassXC |
| Lansweeper |
| Lenovo Quick Clean |
| LogMeIn GoToMeeting IT Installer |
| Microsoft .NET Runtime 6.0 |
| Microsoft Azure CLI |
| Microsoft Azure Storage Explorer |
| Microsoft Power BI Desktop |
| Microsoft PowerShell Core |
| Microsoft PowerToys |
| Microsoft Skype for Desktop |
| Microsoft Surface Diagnostic Toolkit for   Business |
| Microsoft Visual C++ 2008 Redistributable |
| Microsoft Visual C++ 2015-2022  Redistributable |
| Microsoft Visual Studio Code |
| Mozilla Firefox |
| Mozilla Thunderbird |
| Nessus Agent 10 |
| Notepad++ |
| NVIDIA GeForce Experience |
| OpenShot Video Editor |
| OpenVPN |
| Oracle Java Runtime Environment Version 8 |
| Parallels Client 18 |
| Piriform CCleaner |
| Poll Everywhere |
| Poly Lens Desktop App |
| Python 3.10 |
| Python 3.11 |
| QNAP Qsync |
| R for Windows |
| Rarlab WinRAR |
| Remote Help |
| Royal TS 5 |
| Royal TS 6 |
| Royal TS 7 |
| ScreenToGif |
| Simon Tatham Putty |
| SyncBackFree |
| TeamSpeak client |
| TechSmith Snagit 2019 |
| TechSmith Snagit 2020 |
| TechSmith Snagit 2021 |
| TechSmith Snagit 2023 |
| TechSmith Snagit 2024 |
| TightVNC |
| TortoiseSVN |
| TortoiseSVN ipv6 |
| UltraViewer |
| voidtools Everything |
| voidtools Everything Lite |
| WinSCP |
| WireGuard |
| Zoom Client for Meetings |

## Next steps

- [Add an Enterprise App Catalog app to Microsoft Intune](../apps/apps-add-enterprise-app.md)
- [Monitor app information and assignments with Microsoft Intune](apps-monitor.md)
- [Troubleshoot Win32 app issues](apps-win32-troubleshoot.md)
