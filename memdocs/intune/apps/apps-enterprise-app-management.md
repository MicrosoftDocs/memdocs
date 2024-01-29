---
title: Microsoft Intune Enterprise Application Management
titleSuffix:
description: Learn about Enterprise App Management and the Enterprise App Catalog in Microsoft Intune. 
keywords:
author: Erikre
ms.author: erikre
manager: dougeby
ms.date: 01/08/2024
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: apps
ms.localizationpriority: high
ms.technology:
ms.assetid: 
ms.reviewer: dguilory
ms.suite: ems
search.appverid: MET150
ms.custom: intune-azure
ms.collection:
- tier1
- M365-identity-device-management
- highpri
---

# Microsoft Intune Enterprise Application Management

Microsoft Intune Enterprise App Management enables you to easily discover and deploy pre-packaged applications and keep them up to date from the Enterprise App Catalog. The Enterprise App Catalog is a collection of pre-packaged Microsoft and non-Microsoft applications. These applications are Win32 apps that are hosted by Microsoft so you can provision these applications in your tenant.

> [!IMPORTANT]
> Enterprise App Management is an Intune add-on as part of the Intune suite that is available for trial and purchase. For more information, see [Use Intune Suite add-on capabilities](../fundamentals/intune-add-ons.md).

Enterprise App Management (EAM) encompasses the aspects of working with Win32 apps from the Enterprise App Catalog. The catalog offers a variety of Win32 apps that have been wrapped using the [Intune App Wrapping Tool](../developer/apps-prepare-mobile-application-management.md#intune-app-wrapping-tool). In addition, these apps have been [prepared as Win32 apps](../apps/apps-win32-prepare.md).

## Benefits of Enterprise App Management

The benefits of using Enterprise App Management are the following:

- **Streamlined app management**: You can save time and reduce complexity by streamlining the app management process. Discover and package apps directly from the Intune console.
- **Reduce security risks and vulnerabilities**: Mitigate risk and deploy app fixes immediately when security vulnerabilities are discovered.
- **Stay current with updates**: You'll be able to keep apps up-to-date and secure by identifying and updating outdated applications using guided updating.

When you add an Enterprise App Catalog app, Intune pre-populates the following installation details:

- Commands to install and uninstall the app silently
- Option to allow the app to be uninstalled by the enduser
- Device restart behavioir after installation or uninstallation
- Return codes to indicate post-installation behavior
- Whether to install the app for system or user
- Time required to install the app
  
Microsoft Intune pre-populates the detection rules that devices must meet before the app is installed:

- File sive
- File version
- Registry

Also, Intune pre-populates the requirements that devices must meet before the app is installed:

- Windows OS architecture required
- Minimum OS required

> [!IMPORTANT]
> Microsoft recommends using the pre-populated fields containing specific commands and rules, however you can modify the pre-populated fields if needed.

You can also configure app specific rules used to detect the presence of the Enterprise App Catalog app where you can choose to either manually configure the detection rules or use a custom script to detect the presence of the app before installing the app.

## Self-updating apps

The Enterprise App Catalog includes apps that self update. Intune will ensure the app is at least at a target minimum version, but will consider the app installed if the detected version of the app is at or above the minimum version. Self-updating apps will update based on the vendors process. Intune will report the version of the app detected on the device.

## Frequently asked questions (FAQ)

### How can I request to add an application the Enterprise App Catalog?

If you aren't already working with a Microsoft contact, fill out the [Enterprise app management app catalog request](https://aka.ms/EAM/AppRequest) form.

> [!IMPORTANT]
> Microsoft makes no guarantee, express or implied, with respect to adding a requested app to the Enterprie App Catalog. Once the submission is reviewed using the form provided above, the app may or may not be added to the Enterprise App Catalog. Microsoft does not offer or assume any Service Level Agreement (SLA) or timeline with regard to adding an application to the Enterprise App Catalog.

### Where are the devices downloading the app content from?

Microsoft hosts the applications in Microsoft storage. When requested via the customer, the content is copied over to customer tenant, making it available in seconds or minutes.

### Is Microsoft providing security around any of the content provided in the Enterprise App Catalog?

No. Microsoft makes no guarantee, express or implied, with respect to the security and compliance of the applications provided in the Enterprise App Catalog.

### What app installer types are in the Enterprise App Catalog?

The apps currently provided in the Enterprise application catalog are Windows Win32 applications (exe and msi).

### How will Microsoft detect if an application from the Enterprise App Catalog is in use?

At this time, Intune provides no running application detection.

### What is the Service Level Agreement (SLA) for when an app update is avaiable in the catalog?

No SLA is currently available.

### How many applications are in the catalog?

At the time of general availability (GA), Microsoft expects to have approximatly 100 applications available in the Enterprise App Catalog.

### How can working with the applications in Enterprise App Catalog be automated?

Graph API support will be avaiable soon after general avaiablility. 

### When will Enterprise App Catalog apps have the capability to automatically update to the latest version when its added to the catalog.

No. There's no automated processes available as of General Avaliability.

### Can you get licensed applications from this catalog?

Yes. You can get licensed applications from the Enterprise App Catalog, although you're responsible for purchasing the license from the vendor. Intune doesn't perform a license check.

### How are licensed applications installed?

If you install a licensed application where a license isn't provided, the application will provide the end-user with the application's first run experience.

### Are updates available for unmanaged applications?

No. At the time of General Avaliability, unmanaged applications aren't supported. Support for unmanaged applications may be available in a future iteration.

### When will automated updates be available?

Automated updates are planned for a future iteration.

### Can this be purchased standalone

Yes. Enterprise App Management can be purchased as a standalone SKU or as part of the Microsoft Intune Suite.

### Does using this app type require Microsoft Intune? Can Enterprise applications be leveraged with Configuration Manager?

Using an Enterprise App Management is only provided by Microsoft Intune. Configuration Manager isn't supported, however Enterprise App Management will work for co-managed clients.

### Does Enterprise App Management use **Winget**?

No. Enterprise App Management leverages Win32.

### For the application updating, will the app be upgraded, installed side-by-side, or will the previous version be uninstalled?

You can configure what experience you want related to uninstalling the previous version, however the behavior of the application upgrade is controlled by the vendor. 

### Is Enterprise App Management available for GCC, GCC High, or DoD tenants?

Support for GCC is planned to be available later in 2024.

### Is Autopatch leveraged with Enterprise App Management?

Autopatch isn't leveraged with Enterprise App Management. We plan to evaluate Autopatch and other integrations in future iterations.

### Is Enterprise App Management available for co-managed devices?

Yes. Enterprise App Management is available for co-managed devices.

## Next steps

- [Add an Enterprise App Catalog app (Win32) to Microsoft Intune](../apps/apps-add-enterprise-app.md)
- [Monitor app information and assignments with Microsoft Intune](apps-monitor.md)
- [Troubleshoot Win32 app issues](apps-win32-troubleshoot.md)
