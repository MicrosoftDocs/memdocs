---
title: Configure definition updates
titleSuffix: Configuration Manager
description: Learn how to select and configure methods with Endpoint Protection in Configuration Manager to keep antimalware definitions up to date on client computers.
ms.date: 10/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
author: BalaDelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
ms.collection: tier3
---

# Configure definition updates for Endpoint Protection  

*Applies to: Configuration Manager (current branch)*

 With Endpoint Protection in Configuration Manager, you can use any of several available methods to keep antimalware definitions up to date on client computers in your hierarchy. The information in this topic can help you to select and configure these methods.

 To update antimalware definitions, you can use one or more of the following methods:

- [Updates distributed from Configuration Manager](endpoint-definitions-configmgr.md) - This method uses Configuration Manager software updates to deliver definition and engine updates to computers in your hierarchy.

- [Updates distributed from Windows Server Update Services (WSUS)](endpoint-definitions-wsus.md) - This method uses your WSUS infrastructure to deliver definition and engine updates to computers.

- [Updates distributed from Microsoft Update](endpoint-definitions-microsoft-updates.md) - This method allows computers to connect directly to Microsoft Update in order to download definition and engine updates. This method can be useful for computers that are not often connected to the business network.

- [Updates distributed from Microsoft Malware Protection Center](endpoint-definitions-protection-center.md) - This method will download definition updates from the Microsoft Malware Protection Center.

- [Updates from UNC file shares](endpoint-definitions-network.md) - With this method, you can save the latest definition and engine updates to a share on the network. Clients can then access the network to install the updates.

  You can configure multiple definition update sources and control the order in which they are assessed and applied. This is done in the **Configure Definition Update Sources** dialog box when you create an antimalware policy.

> [!IMPORTANT]
>  For Windows 10 or later PCs, you must configure Endpoint Protection to update malware definitions for Windows Defender.

## How to Configure Definition Update Sources
 Use the following procedure to configure the definition update sources to use for each antimalware policy.

1.  In the Configuration Manager console, click **Assets and Compliance**.

2.  In the **Assets and Compliance** workspace, expand **Endpoint Protection**, and then click **Antimalware Policies**.

3.  Open the properties page of the **Default Antimalware Policy** or create a new antimalware policy. For more information about how to create antimalware policies, see [How to create and deploy antimalware policies for Endpoint Protection](endpoint-antimalware-policies.md).

4.  In the **Security Intelligence updates** section of the antimalware properties dialog box, click **Set Source**.
    - The **Definition updates** section was renamed to **Security Intelligence updates** starting in Configuration Manager version 1902.

5.  In the **Configure Definition Update Sources** dialog box, select the sources to use for definition updates. You can click **Up** or **Down** to modify the order in which these sources are used.

6.  Click **OK** to close the **Configure Definition Update Sources** dialog box.

## Configure Endpoint Protection definitions

-   [Updates distributed from Configuration Manager](endpoint-definitions-configmgr.md) - This method uses Configuration Manager software updates to deliver definition and engine updates to computers in your hierarchy.

-   [Updates distributed from Windows Server Update Services (WSUS)](endpoint-definitions-wsus.md) - This method uses your WSUS infrastructure to deliver definition and engine updates to computers.

-   [Updates distributed from Microsoft Update](endpoint-definitions-microsoft-updates.md) - This method allows computers to connect directly to Microsoft Update in order to download definition and engine updates. This method can be useful for computers that are not often connected to the business network.

-   Updates distributed from Microsoft Malware Protection Center - This method will download definition updates from the Microsoft Malware Protection Center.

-   [Updates from UNC file shares](endpoint-definitions-network.md) - With this method, you can save the latest definition and engine updates to a share on the network. Clients can then access the network to install the updates.
