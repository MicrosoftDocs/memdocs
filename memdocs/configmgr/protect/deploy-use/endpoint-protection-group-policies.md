---
title: Manage Endpoint Protection using Group Policies
titleSuffix: Configuration Manager
description: Learn how to manage Endpoint Protection using Group Policies.
ms.date: 10/05/2021
ms.service: configuration-manager
ms.subservice: protect
ms.topic: how-to
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---
# Use Group Policy settings to manage Endpoint Protection in previous versions of Windows

**Applies to:**

- [Microsoft Defender for Endpoint](/windows/security/threat-protection/microsoft-defender-atp/microsoft-defender-advanced-threat-protection)
- System Center Endpoint Protection on the following down-level devices:
    - Windows Server 2012 R2
    - Windows 8.1
    - Windows Server 2012
    - Windows 8
    - Windows Server 2008 R2 SP1
    - Windows 7 SP1
    - Windows Server 2008 SP2
    - Windows Vista

You may have a number of down-level or legacy Windows devices that are enabled with Endpoint Protection—but are outside of your Configuration Manager hierarchy. For example, devices in a demilitarized zone or devices that are integrated through mergers and acquisitions. 

You can manage Endpoint Protection in such devices using Group Policy settings, described as follows:

- [Copy Endpoint Protection policy definitions](#copy-endpoint-protection-policy-definitions)
- Load Endpoint Protection policy definitions into any of the following locations:
    - [Central Store on a Domain Controller (Recommended)](#load-endpoint-protection-group-policy-settings-into-a-central-store-on-a-domain-controller)
    - [Local device](#load-endpoint-protection-group-policy-settings-into-your-local-device)

> [!NOTE]
> For information on how to use Group Policy settings to manage Microsoft Defender Antivirus in Windows 10, Windows Server 2019, Windows Server 2016, or later as well as [on Windows Server 2012 R2 after installing Microsoft Defender for Endpoint using the modern, unified solution](/microsoft-365/security/defender-endpoint/configure-server-endpoints#windows-server-2012-r2-and-windows-server-2016) see [Use Group Policy settings to configure and manage Microsoft Defender Antivirus](/windows/security/threat-protection/microsoft-defender-antivirus/use-group-policy-microsoft-defender-antivirus).

## Copy Endpoint Protection policy definitions

On a down-level Windows device that is managed by Endpoint Protection, copy the Endpoint Protection policy definition files.

1. Go to **C:\Program Files\Microsoft Security Client\Admx**. 

2. Compress the following files into a zip file, for example **SCEP_admx.zip**:
    - **EndPointProtection.adml**
    - **EndPointProtection.admx**
3. Copy the zip file into a temporary folder. For example, **C:\temp_SCEP_GPO_admx**.
4. Extract the file. 

> [!NOTE]
> The registry keys to configure Endpoint Protection policy settings are located in **Hkey_Local_Machine\Software\Policies\Microsoft\Microsoft Antimalware**.

## Load Endpoint Protection Group Policy settings into a Central Store on a domain controller

If you are using a [Central Store for Group Policy Administrative Templates](https://support.microsoft.com/help/3087759/how-to-create-and-manage-the-central-store-for-group-policy-administra), perform the following steps to load and configure Endpoint Protection Group policy settings. This is the recommended method.

1. Go to the folder where you extracted the Endpoint Protection policy definition files.
2. Copy the .admx and .adml files into the **PolicyDefinitions** folder on the domain controller:
    1. Copy **EndPointProtection.admx** into **\\\\\<forest.root\>\\SYSVOL\\\<domain\>\\Policies\\PolicyDefinitions**. 
    2. Copy **EndPointProtection.adml** into **\\\\\<forest.root\>\\SYSVOL\\\<domain\>\\Policies\\PolicyDefinitions\\en-US**.  

    For example:
    
    - Copy **EndPointProtection.admx** into **\\DC\SYSVOL\contoso.com\Policies\PolicyDefinitions**.
    - Copy **EndPointProtection.adml** into **\\DC\SYSVOL\contoso.com\Policies\PolicyDefinitions\en-US**.
    
    where **DC** is the name of your Domain Controller and **contoso.com** is your domain.

3. Open the [Group Policy Management Console](/internet-explorer/ie11-deploy-guide/group-policy-and-group-policy-mgmt-console-ie11) and create a new Group Policy Object (GPO) in your domain, for example **Endpoint Protection**.
4. Right-click the GPO for Endpoint Protection and click **Edit**.
5. In the Group Policy Management Editor, go to **Computer Configuration** > **Policies** > **Administrative Templates: Policy definitions** > **Windows Components** > **Endpoint Protection**.

   The list of Endpoint Protection Group Policies is displayed.

6. Expand the section that contains the setting you want to configure, double-click the setting to open it, and make configuration changes.

## Load Endpoint Protection Group Policy settings into your local device

Instead of using Central Store for loading Endpoint Protection policy definitions, you can store them locally into your device.

1. Go to the folder where you extracted the Endpoint Protection policy definition files.
2. Copy the .admx and .adml files into your local PolicyDefinitions folder.
    1. Copy **EndPointProtection.admx** into **%SystemRoot%/PolicyDefinitions**. 
    2. Copy **EndPointProtection.adml** into **%SystemRoot%/PolicyDefinitions/en-US**.
    
    For example:

    - Copy **EndPointProtection.admx** into **C:\Windows\PolicyDefinitions**.
    - Copy **EndPointProtection.adml** into **C:\Windows\PolicyDefinitions\en-US**.
    
3. Open Local Group Policy Editor.
4. Go to **Computer Configuration** > **Administrative Templates** > **Windows Components** > **Endpoint Protection**.

    The list of Endpoint Protection Group Policies is displayed.

5. Expand the section that contains the setting you want to configure, double-click the setting to open it, and make configuration changes.

## Next steps
- For an overview on Endpoint Protection, see [Endpoint Protection](endpoint-protection.md).
- For information on configuring Endpoint Protection on a standalone client manually, see [Configure Endpoint Protection on a standalone client](endpoint-protection-configure-standalone-client.md).
