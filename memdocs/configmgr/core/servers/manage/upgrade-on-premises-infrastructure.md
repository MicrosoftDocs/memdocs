---
title: Upgrade on-premises infrastructure
titleSuffix: Configuration Manager
description: Learn how to upgrade infrastructure, such as SQL Server and the OS of site systems.
ms.date: 04/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: conceptual
ms.assetid: 8ca970dd-e71c-404f-9435-d36e773a0db2
author: mestew
ms.author: mstewart
manager: dougeby
---

# Upgrade on-premises infrastructure that supports Configuration Manager

*Applies to: Configuration Manager (current branch)*

Use the information in this article to help you upgrade the server infrastructure that runs Configuration Manager.  

- If you want to *upgrade* from an earlier version to Configuration Manager, current branch, see [Upgrade to Configuration Manager](../deploy/install/upgrade-to-configuration-manager.md).  

- If you want to *update* your Configuration Manager, current branch, infrastructure to a new version, see [Updates for Configuration Manager](updates.md).  

## <a name="BKMK_SupConfigUpgradeSiteSrv"></a> Upgrade the OS of site systems  

Configuration Manager supports the in-place upgrade of the server OS that hosts a site server and any site system role, in the following situations:  

- If Configuration Manager still supports the resulting service pack level of Windows, it supports in-place upgrade to a later Windows Server service pack.  

- In-place upgrade from:  

    - Windows Server 2016 to Windows Server 2019  

    - Windows Server 2012 R2 to Windows Server 2019  

    - Windows Server 2012 R2 to Windows Server 2016  

    - Windows Server 2012 to Windows Server 2016  

    - Windows Server 2012 to Windows Server 2012 R2  

    - Windows Server 2008 R2 to Windows Server 2012 R2  

To upgrade a server, use the upgrade procedures provided by the OS you're upgrading to. See the following articles:  

- [Windows Server Upgrade Center](/windows-server/upgrade/upgrade-overview)  

- [Upgrade and conversion options for Windows Server 2016](/windows-server/get-started/supported-upgrade-paths)  

- [Upgrade Options for Windows Server 2012 R2](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn303416(v=ws.11))  

### <a name="bkmk_2016-2019"></a> Upgrade to Windows Server 2016 or 2019

Use the steps in this section for any of the following upgrade scenarios:  

- Upgrade either Windows Server 2012 R2 or Windows Server 2016 to Windows Server 2019  

- Upgrade either Windows Server 2012 or Windows Server 2012 R2 to Windows Server 2016  

#### Before upgrade

- (Windows Server 2012 or Windows Server 2012 R2): Remove the System Center Endpoint Protection (SCEP) client. Windows Server now has Windows Defender built in, which replaces the SCEP client. The presence of the SCEP client can prevent an upgrade to Windows Server.  

- Remove the WSUS role from the server if it's installed. You may keep the SUSDB and reattach it once WSUS is reinstalled.  

- If you're upgrading the OS of the site server, make sure [file-based replication](../../plan-design/hierarchy/file-based-replication.md) is healthy for the site. Check all inboxes for a backlog on both sending and receiving sites. If there are lots of stuck or pending replication jobs, wait until they clear out.<!-- SCCMDocs#1792 -->
    - On the sending site, review **sender.log**.
    - On the receiving site, review **despooler log**.

#### After upgrade

- Make sure Windows Defender is enabled, set for automatic start, and running.  

- Make sure the following Configuration Manager services are running:  

    - SMS_EXECUTIVE  

    - SMS_SITE_COMPONENT_MANAGER  

- Make sure the **Windows Process Activation** and **WWW/W3svc** services are enabled and set for automatic start. The upgrade process disables these services, so make sure they're running for the following site system roles:  

    - Site server  

    - Management point  

- Make sure each server that hosts a site system role continues to meet all [prerequisites](../../plan-design/configs/site-and-site-system-prerequisites.md). For example, you might need to reinstall BITS, WSUS, or configure specific settings for IIS.  

- After restoring any missing prerequisites, restart the server one more time to make sure services are started and operational.  

- If you're upgrading the primary site server, then [run a site reset](modify-your-infrastructure.md#bkmk_reset).  

#### Known issue for remote Configuration Manager consoles

After you upgrade the site server, or an instance of the SMS Provider, you can't connect with the Configuration Manager console. To work around this problem, manually restore permissions for the **SMS Admins** group in WMI. Permissions must be set on the site server, and on each remote server that hosts an instance of the SMS Provider:

1. On the applicable servers, open the Microsoft Management Console (MMC) and add the snap-in for  **WMI Control**, and then select **Local computer**.  

2. In the MMC, open the **Properties** of **WMI Control (Local)** and select the **Security** tab.  

3. Expand the tree below Root, select the **SMS** node, and then choose **Security**.  Make sure the **SMS Admins** group has the following permissions:  

    - Enable Account  

    - Remote Enable  

4. On the **Security tab** below the **SMS** node, select the **site_&lt;sitecode**> node, and then choose **Security**. Make sure the **SMS Admins** group has the following permissions:  

    - Execute Methods  

    - Provider Write  

    - Enable Account  

    - Remote Enable  

5. Save the permissions to restore access for the Configuration Manager console.  

#### Known issue for remote site systems

After you upgrade a server that hosts a site system role, the value `Software\Microsoft\SMS` may be missing from the following registry key: `HKLM\SYSTEM\CurrentControlSet\Control\SecurePipeServers\Winreg\AllowedPaths`

If this value is missing after you upgrade Windows on the server, manually add it. Otherwise site system roles can have issues uploading files to the site server inboxes.

### <a name="bkmk_2012r2"></a> Upgrade to Windows Server 2012 R2

When you upgrade from either Windows Server 2008 R2 or Windows Server 2012 to Windows Server 2012 R2, the following conditions apply:

#### Before upgrade

- On Windows Server 2012: Remove the WSUS role from the server if it's installed. You may keep the SUSDB and reattach it once WSUS is reinstalled.  

- On Windows Server 2008 R2: Before you upgrade to Windows Server 2012 R2, you must uninstall WSUS 3.2 from the server. You may keep the SUSDB and reattach it once WSUS is reinstalled. For more information, see [Windows Server Update Services Overview](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh852345(v=ws.11)#new-and-changed-functionality).  

- If you're upgrading the OS of the site server, make sure [file-based replication](../../plan-design/hierarchy/file-based-replication.md) is healthy for the site. Check all inboxes for a backlog on both sending and receiving sites. If there are lots of stuck or pending replication jobs, wait until they clear out.<!-- SCCMDocs#1792 -->
    - On the sending site, review **sender.log**.
    - On the receiving site, review **despooler log**.

#### After upgrade

- The upgrade process disables the Windows Deployment Services. Make sure this service is started and running for the following site system roles:  

    - Site server  

    - Management point  

- Make sure the **Windows Process Activation** and **WWW/W3svc** services are enabled and set for automatic start. The upgrade process disables these services, so make sure they're running for the following site system roles:  

    - Site server  

    - Management point  

- Make sure each server that hosts a site system role continues to meet all [prerequisites](../../plan-design/configs/site-and-site-system-prerequisites.md). For example, you might need to reinstall BITS, WSUS, or configure specific settings for IIS.  

    After restoring any missing prerequisites, restart the server one more time to make sure services are started and operational.  

### Unsupported upgrade scenarios

The following Windows Server upgrade scenarios are commonly asked about, but not supported by Configuration Manager:  

- Windows Server 2008 to Windows Server 2012 or later  

- Windows Server 2008 R2 to Windows Server 2012  


## <a name="BKMK_SupConfigUpgradeClient"></a> Upgrade the OS of clients  

Configuration Manager supports an in-place upgrade of the OS for Configuration Manager clients in the following situations:  

- If Configuration Manager supports the resulting service pack level, it supports in-place upgrade to a later Windows service pack.  

- In-place upgrade of Windows from a supported version to Windows 10. For more information, see [Upgrade Windows to the latest version](../../../osd/deploy-use/upgrade-windows-to-the-latest-version.md).  

- Build-to-build servicing upgrades of Windows 10. For more information, see [Manage Windows as a service](../../../osd/deploy-use/manage-windows-as-a-service.md).  


## <a name="BKMK_SupConfigUpgradeDBSrv"></a> Upgrade SQL Server  

Configuration Manager supports an in-place upgrade of SQL Server on the site database server.

For information about the versions of SQL Server that Configuration Manager supports, see [Support for SQL Server versions](../../plan-design/configs/support-for-sql-server-versions.md).  

### Upgrade the service pack version of SQL Server

If Configuration Manager still supports the resulting SQL Server service pack level, it supports the in-place upgrade of SQL Server to a later service pack.

When you have more than one Configuration Manager site in a hierarchy, each site can run a different service pack version of SQL Server. There's no limitation to the order in which sites upgrade the service pack version of SQL Server.

### Upgrade to a new version of SQL Server

Configuration Manager supports the in-place upgrade of SQL Server to the following versions:

- SQL Server 2019

- SQL Server 2017

- SQL Server 2016

- SQL Server 2014

This includes the upgrade of SQL Server Express to a newer version of SQL Server Express at secondary sites.

When you upgrade the version of SQL Server that hosts the site database, you must upgrade the SQL Server version that's used at sites in the following order:

1. Upgrade SQL Server at the central administration site first  

2. Upgrade secondary sites before you upgrade a secondary site's parent primary site  

3. Upgrade parent primary sites last. These sites include both child primary sites that report to a central administration site, and stand-alone primary sites that are the top-level site of a hierarchy.  

When you upgrade a site database from an earlier version of SQL Server, the database keeps its existing cardinality estimation level, if it's at the minimum allowed for that instance of SQL Server. If you upgrade SQL Server with a database at a compatibility level lower than the allowed level, it automatically sets the database to the lowest compatibility level allowed by SQL Server. For more information, see [Supported SQL Server versions: Database compatibility level](../../plan-design/configs/support-for-sql-server-versions.md#database-compatibility-level).

For more information about upgrading SQL Server, see the following SQL Server articles:  

- [Upgrade to SQL Server 2019](/sql/database-engine/install-windows/supported-version-and-edition-upgrades-version-15)  

- [Upgrade to SQL Server 2017](/sql/database-engine/install-windows/supported-version-and-edition-upgrades-2017)  

- [Upgrade to SQL Server 2016](/sql/database-engine/install-windows/supported-version-and-edition-upgrades)  

### To upgrade SQL Server on the site database server  

1. Stop all Configuration Manager services at the site  

2. Upgrade SQL Server to a supported version  

3. Restart the Configuration Manager services  

> [!NOTE]  
> When you change the SQL Server edition in use at the central administration site from Standard to either a Datacenter or Enterprise, the database partition doesn't change. This database partition limits the number of clients the hierarchy supports.
