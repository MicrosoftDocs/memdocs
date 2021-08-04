---
title: Supported clients and devices
titleSuffix: Configuration Manager
description: Learn which OS versions Configuration Manager supports for clients and devices.
ms.date: 08/02/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
author: mestew
ms.author: mstewart
manager: dougeby
---

# Supported OS versions for clients and devices for Configuration Manager

*Applies to: Configuration Manager (current branch)*

Configuration Manager supports installing client software on Windows and macOS computers.

## General requirements and limitations

Review the following requirements and limitations for all clients:

- Changing the startup type or **Log on as** settings for any Configuration Manager service isn't supported. This change can prevent key services from running correctly.

## Windows computers

To manage the following Windows OS versions, use the client that's included with Configuration Manager. For more information, see [How to deploy clients to Windows computers](../../clients/deploy/deploy-clients-to-windows-computers.md).

### Supported client OS versions

- **Windows 10**

    For more detailed information, see [Support for Windows 10](support-for-windows-10.md).

- **Windows 8.1** (x86, x64): Professional, Enterprise

#### Azure Virtual Desktop

<!--3556025-->
[Azure Virtual Desktop](/azure/virtual-desktop/) is a desktop and app virtualization service that runs on Microsoft Azure. You can use Configuration Manager to manage these virtual devices running Windows in Azure.

Similar to a terminal server, some of these virtual devices allow multiple concurrent active user sessions. To help with client performance, Configuration Manager now disables user policies on any device that allows these multiple user sessions. Even if you enable user policies, the client disables them by default on these devices, which include Windows 10 Enterprise multi-session and terminal servers.

The client only disables user policy when it detects this type of device during a new installation. For an existing client of this type that you update to this version, the previous behavior persists. On an existing device, it configures the user policy setting even if it detects that the device allows multiple user sessions.

If you require user policy in this scenario, and accept any potential performance impact, use [client settings](../../clients/deploy/configure-client-settings.md) to enable user policy. In the **Client Policy** group, configure the following setting: **Enable user policy for multiple user sessions**.<!-- 4737447 -->

> [!NOTE]
> You can't use co-management with a client running Windows 10 Enterprise multi-session. <!-- SCCMDocs-pr#3950 -->

Starting in version 2006, the **Windows 10 Enterprise multi-session** platform is available in the list of supported OS versions on objects with requirement rules or applicability lists.<!--6527576-->

> [!NOTE]
> If you previously selected the top-level **Windows 10** platform, this action automatically selected all child platforms. This new platform isn't automatically selected. If you want to add **Windows 10 Enterprise multi-session**, manually select it in the list.

For more information, see the following articles:

- [Support for virtualization environments](support-for-virtualization-environments.md)
- [Manage Configuration Manager clients in a virtual desktop infrastructure (VDI)](../../clients/deploy/plan/considerations-for-managing-clients-in-a-vdi.md)

### Supported server OS versions

- **Windows Server 2022**: Standard, Datacenter <sup>[Note 1](#bkmk_note1)</sup> (_starting in version 2107_)<!-- 10200029 -->

- **Windows Server 2019**: Standard, Datacenter <sup>[Note 1](#bkmk_note1)</sup>

- **Windows Server 2016**: Standard, Datacenter <sup>[Note 1](#bkmk_note1)</sup>

- **Windows Storage Server 2016**: Workgroup, Standard

- **Windows Server 2012 R2** (x64): Standard, Datacenter <sup>[Note 1](#bkmk_note1)</sup>

- **Windows Storage Server 2012 R2** (x64)

- **Windows Server 2012** (x64): Standard, Datacenter <sup>[Note 1](#bkmk_note1)</sup>

- **Windows Storage Server 2012** (x64)

#### Server Core

The following versions specifically refer to the Server Core installation of the OS. <sup>[Note 3](#bkmk_note3)</sup>

Windows Server semi-annual channel versions are Server Core installations, such as Windows Server, version 1809. As a Configuration Manager client, they're supported the same as the associated Windows 10 semi-annual channel version. For more information, see [Support for Windows 10](support-for-windows-10.md).

- **Windows Server 2022** (x64) <sup>[Note 2](#bkmk_note2)</sup> (_starting in version 2107_)<!-- 10200029 -->

- **Windows Server 2019** (x64) <sup>[Note 2](#bkmk_note2)</sup>

- **Windows Server 2016** (x64) <sup>[Note 2](#bkmk_note2)</sup>

- **Windows Server 2012 R2** (x64) <sup>[Note 2](#bkmk_note2)</sup>

- **Windows Server 2012** (x64) <sup>[Note 2](#bkmk_note2)</sup>

#### <a name="bkmk_note1"></a> Note 1

Configuration Manager tests and supports Windows Server Datacenter editions, but isn't officially certified for Windows Server. Configuration Manager hotfix support isn't offered for issues that are specific to Windows Server Datacenter Edition. For more information on the Windows Server certification program, see [Windows Server Catalog](https://www.windowsservercatalog.com/).

#### <a name="bkmk_note2"></a> Note 2

To support [client push installation](../../clients/deploy/plan/client-installation-methods.md#client-push-installation), add the File Server service of the File and Storage Services server role. For more information about installing Windows features on Server Core, see [Install roles, role services, and features by using Windows PowerShell cmdlets](/windows-server/administration/server-manager/install-or-uninstall-roles-role-services-or-features#install-roles-role-services-and-features-by-using-windows-powershell-cmdlets).

#### <a name="bkmk_note3"></a> Note 3

The Software Center app isn't supported on any version of Windows Server Core.<!--SCCMDocs issue 683-->

## Windows Embedded computers

Manage Windows Embedded devices by installing the Configuration Manager client on the device. For more information, see [Planning for client deployment to Windows Embedded devices](../../clients/deploy/plan/planning-for-client-deployment-to-windows-embedded-devices.md).

### Requirements and limitations

- All client features are supported on Windows Embedded systems that don't have write filters enabled.

- Clients that use one of the following are supported for all features except power management:

  - Enhanced Write Filters (EWF)

  - RAM File-Based Write Filters (FBWF)

  - Unified Write Filters (UWF)

### Supported OS versions

- **Windows 10 Enterprise** (x86, x64)

- **Windows 10 IoT Enterprise** (x86, x64)
    This version includes the long-term servicing channel (LTSC). For more information, see [Overview of Windows 10 IoT Enterprise](/windows/iot-core/windows-iot-enterprise).<!--SCCMDocs issue 560-->

- **Windows Embedded 8.1 Industry** (x86, x64)

- **Windows Embedded 8 Standard** (x86, x64)

- **Windows Thin PC** (x86, x64)

- **Windows Embedded POSReady 7** (x86, x64)

- **Windows Embedded Standard 7 with SP1** (x86, x64)

## <a name="bkmk_ESU"></a> Extended Security Updates and Configuration Manager

The [Extended Security Updates (ESU)](https://support.microsoft.com/help/4497181/lifecycle-faq-extended-security-updates) program is a last resort option for customers who need to run certain legacy Microsoft products past the end of support. For example, Windows 7. It includes Critical and/or Important security updates (as defined by the [Microsoft Security Response Center (MSRC)](https://www.microsoft.com/msrc)) for a maximum of three years after the product's End of Extended Support date.

Products that are beyond their support lifecycle aren't supported for use with Configuration Manager. This includes any products that are covered under the ESU program. Security updates released under the ESU program will be published to Windows Server Update Services (WSUS). These updates will appear in the Configuration Manager console. While products that are covered under the ESU program are no longer supported for use with Configuration Manager, the [latest released version of Configuration Manager current branch](../../servers/manage/updates.md#version-details) can be used to deploy and install Windows security updates released under the program. The latest released version can also be used to deploy Windows 10 to devices running Windows 7.

Client management features not related to Windows software update management or OS deployment will no longer be tested on the operating systems covered under the ESU program and we don't guarantee that they'll continue to function. It's highly recommended to upgrade or migrate to a current version of the operating systems as soon as possible to receive client management support.

> [!Tip]
> Starting in Configuration Manager 2010, you'll be notified in-console about devices with operating systems that are past the end of support date and that are no longer eligible to receive security updates. For more information, see [Console notifications](../../servers/manage/admin-console-notifications.md#bkmk_2010). This information is provided for your convenience and only for use internally within your company. You should not solely rely on this information to confirm update or license compliance. Be sure to verify the accuracy of the information provided to you.

## Mac computers

Manage Apple Mac computers with the Configuration Manager client for macOS.

The macOS client installation package isn't supplied with the Configuration Manager media. Download it from the Microsoft Download Center, [Microsoft Endpoint Configuration Manager - macOS Client (64-bit)](https://www.microsoft.com/download/details.aspx?id=100850).

For more information, see [How to deploy clients to Macs](../../clients/deploy/deploy-clients-to-macs.md).

### Requirements and limitations for macOS

- Installing or running the Configuration Manager client for macOS on computers under an account other than root isn't supported. Doing so can prevent key services from running correctly.

### Supported versions

- **macOS Big Sur (11)** (requires Configuration Manager client for macOS version 5.0.9000.1002 or later)<!-- 8816608 -->

- **macOS Catalina (10.15)** (requires Configuration Manager client for macOS version 5.0.8742.1000 or later)

- **macOS Mojave (10.14)**

## <a name="bkmk_OnpremOS"></a> On-premises MDM

Configuration Manager has built-in capabilities for managing mobile devices that are on-premises without installing client software. For more information, see [Manage mobile devices with on-premises infrastructure](../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).

### Supported operating systems

- **Windows 10 Pro** (x86, x64)

- **Windows 10 Pro Enterprise** (x86, x64)

- **Windows 10 IoT Enterprise** (x86, x64)
    This version includes the long-term servicing channel (LTSC). For more information, see [Overview of Windows 10 IoT Enterprise](/windows/iot-core/windows-iot-enterprise).<!--SCCMDocs issue 560-->

- **Windows 10 IoT Mobile Enterprise**

- **Windows 10 Team for Surface Hub**

## <a name="bkmk_ExSrvConOS"></a> Exchange Server connector

Configuration Manager supports limited management of devices that connect to your Exchange Server, without installing the Configuration Manager client. For more information, see [Manage mobile devices with Configuration Manager and Exchange](../../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md).

### Supported versions of Exchange Server

- **Exchange Online (Microsoft 365)**: This version includes Business Productivity Online Standard Suite

- **Exchange Server 2016**

- **Exchange Server 2013**

- **Exchange Server 2010 SP1** or **Exchange Server 2010 SP2**
