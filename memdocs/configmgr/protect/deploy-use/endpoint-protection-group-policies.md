---
title: Manage Endpoint Protection using Group Policies
titleSuffix: Configuration Manager
description: Learn how to manage Endpoint Protection using Group Policies.
ms.date: 03/22/2018
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.assetid: e63f2394-6eb1-4a33-bec5-8377fc62a34e
author: mestew
ms.author: mstewart
manager: dougeby


---

# Use Group Policy settings to configure and manage Endpoint Protection

**Applies to:**

- Systems with Microsoft Defender ATP and Endpoint Protection for the following operating systems:
    - Windows Server 2012 R2
    - Windows 8.1
    - Windows Server 2012
    - Windows 8
    - Windows Server 2008 R2 SP1
    - Windows 7 SP1
    - Windows Server 2008 SP2
    - Windows Vista

**Does not apply to:**
- Systems with Microsoft Defender Advanced Threat Protection (Microsoft Defender ATP) and using Microsoft Endpoint Configuration Manager, Current Branch (CB)
- Microsoft Defender Antivirus (formerly known as Windows Defender Antivirus) for the following operating systems:
    - Windows Server 2019
    - Windows Server 2016
    - Windows 10

You can use Group Policies to manage down-level (legacy) Windows and Windows Servers operating systems that are not managed by Configuration Manager. For example, devices in a perimeter network (also known as a DMZ, demilitarized zone, and screened subnet) or devices integrated during a merger and acquisition.

This topic describes how to use Group Policies to manage Endpoint Protection in down-level systems.

## Use Group Policy settings to manage Microsoft Defender Antivirus in Windows 10, Windows Server 2016, and Windows Server 2019

Microsoft Defender Antivirus is the antimalware protection component built into Windows 10, Windows Server 2016, and Windows Server 2019. You can [configure and manage Microsoft Defender Antivirus](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-antivirus/configuration-management-reference-microsoft-defender-antivirus) with a number of tools, including Group Policy. 

To manage Microsoft Defender Antivirus with Group Policy settings:

1. On your Group Policy management device, open the Group Policy Management Console, right-click the Group Policy Object (GPO) you want to configure and click Edit.
2. In the Group Policy Management Editor, go to **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Microsoft Defender Antivirus**.
3. Under **Microsoft Defender Antivirus**, expand the section that contains the setting you want to configure, double-click the setting to open it, and make configuration changes.

For a complete list of Group Policy settings for Microsoft Defender Antivirus, see [Use Group Policy settings to configure and manage Microsoft Defender Antivirus](https://docs.microsoft.com/windows/security/threat-protection/microsoft-defender-antivirus/use-group-policy-microsoft-defender-antivirus).

> [!NOTE]
> The registry keys to configure Microsoft Defender Antivirus policy settings are located in Hkey_Local_Machine > Software > Policies > Microsoft > Windows Defender.

## Use Group Policies to manage Endpoint Protection in previous versions of Windows

You can use Group Policies to manage Endpoint Protection in down-level (legacy) Windows and Windows Servers operating systems that are not managed by Configuration Manager. For example, devices in a perimeter network (also known as a DMZ, demilitarized zone, and screened subnet) or devices integrated during a merger and acquisition.

This section describes how to use Group Policies to manage Endpoint Protection in the following down-level systems:
- Windows Server 2012 R2
- Windows 8.1
- Windows Server 2012
- Windows 8
- Windows Server 2008 R2 SP1
- Windows 7 SP1
- Windows Server 2008 SP2
- Windows Vista

The Group Policies to manage Endpoint Protection are located in 
Computer Configuration > Administrative Templates > Windows Components > Endpoint Protection

> [!NOTE]
> The registry keys to configure Endpoint Protection in previous Windows versions are located in Hkey_Local_Machine > Software > Policies > Microsoft > Microsoft Antimalware.

## How to import Endpoint Protection GPO

On a Windows 7 SP1 system that is managed by Configuration Manager client:

1. Go to c:\Program Files\Microsoft Security Client\Admx. 

2. In ADMX folder, compress the following into a zip file, for example SCEP_admx.zip:
    - en-us
    - EndPointProtection.adml
    - EndPointProtection.admx
3. Copy the zip file.
4. Download the compressed (.zip) file in your local computer or domain controller.
4. Extract the contents of the zip file.

## Load Endpoint Protection GPO on a Central Store on a Domain Controller
This is the recommended method. 
If you are using a [Central Store for Group Policy Administrative Templates](https://support.microsoft.com/help/3087759/how-to-create-and-manage-the-central-store-for-group-policy-administra), copy the following files from the extracted zip file:
- Copy **EndPointProtection.admx** into \\<forest.root>\SysVol\<forest.root>\Policies\PolicyDefinitions
- Copy **EndPointProtection.adml** into \\<forest.root>\SysVol\<forest.root>\Policies\PolicyDefinitions\en-
US
2. Open the [Group Policy Management Console](https://docs.microsoft.com/internet-explorer/ie11-deploy-guide/group-policy-and-group-policy-mgmt-console-ie11)
3. Navigate to **Computer Configuration** > **Policies** > **Administrative Templates: Policy definitions** > **Windows Components** > **Endpoint Protection**.
The list of Endpoint Protection GPOs is displayed.
4. Right-click the GPO you want to configure and click **Edit**.

## Load Endpoint Protection GPO on a local system
As an alternative, you can load the Group Policy settings for Endpoint Protection directly to your local or standalone system.

To load Endpoint Protection Group Policy settings on your local system:
1. Copy the following files from the configuration package:
    - Copy **EndPointProtection.admx** into C:\Windows\PolicyDefinitions
    - Copy **EndPointProtection.adml** into C:\Windows\PolicyDefinitions\en-US
2. Open Local Group Policy Editor.
3. Navigate to **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Endpoint Protection**. 
The list of Endpoint Protection GPOs is displayed.
4. Right-click the GPO you want to configure and click **Edit**.