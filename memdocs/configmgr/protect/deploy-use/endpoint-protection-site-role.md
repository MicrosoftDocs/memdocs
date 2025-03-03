---
title: Create Endpoint Protection point site system role
titleSuffix: Configuration Manager
description: Learn how to configure Endpoint Protection to manage security and malware on Configuration Manager client computers.
ms.date: 02/14/2017
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

# Create an Endpoint Protection point site system role

*Applies to: Configuration Manager (current branch)*

The Endpoint Protection point site system role must be installed before you can use Endpoint Protection. It must be installed on one site system server only, and it must be installed at the top of the hierarchy on a central administration site or a stand-alone primary site.

Use one of the following procedures depending on whether you want to install a new site system server for Endpoint Protection or use an existing site system server:
- [Install on a new site system server](#new-site-system-server)
- [Install on an existing site system server](#existing-site-system-server)

> [!IMPORTANT]
>  When you install an Endpoint Protection point, an Endpoint Protection client is installed on the server hosting the Endpoint Protection point. Services and scans are disabled on this client to enable it to co-exist with any existing antimalware solution that is installed on the server. If you later enable this server for management by Endpoint Protection and select the option to remove any third-party antimalware solution, the third-party product will not be removed. You must uninstall this product manually.

## Prerequisites

The endpoint protection point requires the following Windows Server features:

- .NET Framework 3.5

- Windows Defender feature (Windows Server 2016)<!-- SCCMDocs#2120 -->
- Windows Defender Antivirus feature (Windows Server 2019)
- Microsoft Defender Antivirus feature (Windows Server 2022 or later)

For more information, see [Site and site system prerequisites](../../core/plan-design/configs/site-and-site-system-prerequisites.md).

## New site system server

1.  In the Configuration Manager console, click **Administration**.

2.  In the **Administration** workspace, expand **Site Configuration**, and then click **Servers and Site System Roles**.

3.  On the **Home** tab, in the **Create** group, click **Create Site System Server**.

4.  On the **General** page, specify the general settings for the site system, and then click **Next**.

5.  On the **System Role Selection** page, select **Endpoint Protection point** in the list of available roles, and then click **Next**.

6.  On the **Endpoint Protection** page, select the **I accept the Endpoint Protection license terms** check box, and then click **Next**.

    > [!IMPORTANT]
    >  You cannot use Endpoint Protection in Configuration Manager unless you accept the license terms.

7.  On the **Cloud Protection Service** page, select the level of information that you want to send to Microsoft to help develop new definitions, and then click **Next**.

    > [!NOTE]
    >  This option configures the Cloud Protection Service (formerly known as Microsoft Active Protection Service or MAPS) settings that are used by default. You can then configure custom settings for each antimalware policy you create. Join Cloud Protection Service, to help to keep your computers more secure by supplying Microsoft with malware samples that can help Microsoft to keep antimalware definitions more up-to-date. Additionally, when you join Cloud Protection Service, the Endpoint Protection client can use the dynamic signature service to download new definitions before they are published to Windows Update. For more information, see [How to create and deploy antimalware policies for Endpoint Protection](endpoint-antimalware-policies.md).

8.  Complete the wizard.


## Existing site system server

1.  In the Configuration Manager console, click **Administration**.

2.  In the **Administration** workspace, expand **Site Configuration**, click **Servers and Site System Roles**, and then select the server that you want to use for Endpoint Protection.

3.  On the **Home** tab, in the **Server** group, click **Add Site System Roles**.

4.  On the **General** page, specify the general settings for the site system, and then click **Next**.

5.  On the **System Role Selection** page, select **Endpoint Protection point** in the list of available roles, and then click **Next**.

6.  On the **Endpoint Protection** page, select the **I accept the Endpoint Protection license terms** check box, and then click **Next**.

    > [!IMPORTANT]
    >  You cannot use Endpoint Protection in Configuration Manager unless you accept the license terms.

7.  On the **Cloud Protection Service** page, select the level of information that you want to send to Microsoft to help develop new definitions, and then click **Next**.

    > [!NOTE]
    >  This option configures the Cloud Protection Service settings (formerly known as MAPS) that are used by default. You can configure custom settings for each antimalware policy you configure. For more information, see [How to create and deploy antimalware policies for Endpoint Protection](endpoint-antimalware-policies.md).

8.  Complete the wizard.
