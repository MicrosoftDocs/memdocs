---
title: Install Updates Publisher
titleSuffix: Configuration Manager
description: Install System Center Updates Publisher in your environment
ms.date: 10/20/2021
ms.service: configuration-manager
ms.subservice: software-updates
ms.topic: install-set-up-deploy
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---
# Install Updates Publisher

*Applies to: System Center Updates Publisher*

The information in these articles can help you download, install, and set up Updates Publisher for use with your Configuration Manager environment.

## Prerequisites and limitations
System Center Updates Publisher can only be used with Configuration Manager. It isn't intended for use with stand-alone WSUS hierarchies.

The following sections detail requirements to install and use Updates Publisher, and limitations or known issues for its use.  

### Operating systems
Install and run Updates Publisher on a 64-bit editions of the following operating systems. There are no minimum cumulative update or service pack requirements.

- Windows Server 2016 (Standard, Datacenter)
- Windows Server 2012 R2 (Standard, Datacenter)
- Windows 11
- Windows 10 (Pro, Education, Pro Education, Enterprise)
- Windows 8.1 (Professional, Enterprise)

### Prerequisites
The following are required on the computer that runs Updates Publisher.

-   **64-bit operating system**: The computer where you install Updates Publisher must run a 64-bit operating system.
-   **WSUS 6.2 or later**:
    -   On Windows Server, install the default Administration Console to meet this requirement.
    -   For Windows 8.1 or later operating systems, install the [Remote Server Administration Tools (RSAT) for Windows operating systems](https://support.microsoft.com/help/2693643/remote-server-administration-tools-rsat-for-windows-operating-systems). This installs the necessary support to use Updates Publisher (*API and PowerShell cmdlets*, and *User Interface Management Console*).
-   **Permissions**:
    -   Installation: Local admin
    -   Most operations: local user
    -   Publishing, or operations that involve WSUS: Member of WSUS Administrators group on the WSUS Server.

### Supported languages
Updates Publisher is available only in English but can manage updates for other languages. The language support depends on the task, such as publishing, creating, or editing updates.

When exporting or publishing updates, Updates Publisher displays the title and description of the software update based on the locale of the computer where Updates Publisher is installed.

For example, you create a software update that has an English and Spanish title.

-   If you create the update on a computer whose locale is English, by default, you would see the title and description in English.
-   If you then export or publish that update to a computer whose locale is Spanish, on that computer you would see the title and description in Spanish.

### Publishing
When you publish software updates, you can specify the language of the software update binary file. You can also specify that the binary is language neutral. The following languages are supported:

-   Arabic
-   Chinese (Hong Kong S.A.R.)
-   Chinese (Traditional)
-   Chinese (Simplified)
-   Czech
-   Danish
-   Dutch
-   English
-   Finnish
-   French
-   German
-   Greek
-   Hebrew
-   Hungarian
-   Italian
-   Japanese
-   Korean
-   Norwegian
-   Polish
-   Portuguese
-   Portuguese (Brazil)
-   Russian
-   Spanish
-   Swedish
-   Turkish

### Software update titles and descriptions
The following languages are supported for software update titles and descriptions.

-   Chinese (Traditional)
-   Chinese (Simplified)
-   English
-   French
-   German
-   Italian
-   Japanese
-   Korean
-   Portuguese (Brazil)
-   Russian
-   Spanish

## Install Updates Publisher
Get the **UpdatesPubliser.msi** for installing System Center Updates Publisher from [https://aka.ms/SCUPDownload](https://aka.ms/SCUPDownload).

To install Updates Publisher, run **UpdatesPublisher.msi** on a computer that meets the *prerequisites*. The installer creates the following folder to contain the files necessary to run Updates Publisher: %PROGRAMFILES%\Microsoft\UpdatesPublisher*.

Because this folder contains all the files necessary to use Updates Publisher, you can copy the folder and its contents to a new location or computer and then use Updates Publisher from that location. However, the new location or computer must meet the prerequisites to run Updates Publisher.

After installation completes, run **UpdatesPublisher.exe** from the *UpdatesPublisher* folder to start Updates Publisher.

## Next steps
 After you install Updates Publisher, we recommend you [configuring the options](updates-publisher-options.md) for Updates Publisher. You must configure some options before you can use some features of Updates Publisher.

 However, if you want to use the defaults and don't plan to deploy updates to an update server or to managed devices, you can jump right to [managing software update catalogs](updates-publisher-catalogs.md), or [create software updates](create-updates-with-updates-publisher.md) and create update catalogs of your own.
