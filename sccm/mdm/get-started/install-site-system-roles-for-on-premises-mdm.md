---
title: "Install roles for On-premises MDM "
titleSuffix: "Configuration Manager"
description: "Install site system roles for On-premises Mobile Device Management in System Center Configuration Manager."
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: c3cf9f64-c2b9-4ace-9527-2aba6d4eef04
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Install site system roles for On-premises Mobile Device Management in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

System Center Configuration Manager On\-premises Mobile Device Management requires the following site system roles in your Configuration Manager site infrastructure:  

- Enrollment point  

- Enrollment proxy point  

- Distribution point  

- Device management point  

- Service connection point  

  If you are adding On\-premises Mobile Device Management to your organization that has most PCs and devices managed using the Configuration Manager client software, you might have most of the site system roles installed already as part of your existing infrastructure. If not, see [Add site system roles for System Center Configuration Manager](../../core/servers/deploy/configure/add-site-system-roles.md) for complete information on how to add them to your site.  

> [!NOTE]  
>  If you use database replicas with   your device management point site system role, newly enrolled devices will initially fail to connect to the device management point until the database replica  synchronizes with it. This connection failure occurs because the database replica does not have the information about the newly enrolled device necessary for a successful connection. Replicas synchronize every 5 minutes, so devices will fail to connect for the first 5 minutes after enrollment (usually 2 connection attempts), after which the device will connect successfully.  

 Whether you are using existing site system roles or adding new ones, you must configure them to be used to manage modern devices. Follow the steps below to configure the distribution point and device management point to function correctly for On\-premises Mobile Device Management:  

> [!NOTE]  
>  The current branch of Configuration Manager only supports intranet connections from devices to the distribution points and device management points  for On\-premises Mobile Device Management. However, if you are also managing Mac OS X computers, those clients require internet connections to those site system roles. In that case, when you configure the properties of the distribution point and the device management point,  you should use the **Allow intranet and internet connections** setting instead.  

### To configure site system roles to manage modern devices:  

1. In the Configuration Manager console, click **Administration** > **Overview** > **Site Configuration** > **Servers and Site System Roles**.  

2. Select site system server with distribution point or device management point you want to configure, open properties for **Site System** and make sure it has a FQDN specified. Click **OK**.  

3. Open properties for the distribution point site system role. On the General tab, make sure **HTTPS** is selected and select **Allow intranet-only connections**.  

    If you're also separately managing Mac computers with the Configuration Manager client, use **Allow intranet and internet connections** instead.  

   > [!NOTE]  
   >  Distribution points configured for intranet connections require site boundaries to be configured for them. The current branch of Configuration Manager only supports IPv4 range boundaries for On\-premises Mobile Device Management. For more information on configuring site boundaries, see [Define site boundaries and boundary groups for System Center Configuration Manager](../../core/servers/deploy/configure/define-site-boundaries-and-boundary-groups.md).  

4. Click the check box next to **Allow mobile devices to connect to this distribution point**, and then click **OK**.  

5. Open properties for the management point site system role. On the General tab, make sure **HTTPS** is selected, and select **Allow intranet-only connections**.  

    If you're also separately managing Mac computers with the Configuration Manager client, use **Allow intranet and internet connections** instead.  

6. Click the check box next to **Allow mobile devices and Mac Computer to use this management point**. Click **OK**.  

    This effectively turns the management point into  a device management point.  

   Once the site system roles have been added and configured for managing modern devices, you then need to configure the servers hosting the roles as trusted endpoints for enrolling and communicating with managed devices. See [Set up certificates for trusted communications for On-premises Mobile Device Management in System Center Configuration Manager](../../mdm/get-started/set-up-certificates-on-premises-mdm.md) for more information.  
