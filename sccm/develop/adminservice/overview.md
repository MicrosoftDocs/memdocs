---
title: What is the administration service
titleSuffix: Configuration Manager
description: Use the Configuration Manager administration service REST API to interact with the site over an HTTPS OData connection.
ms.date: 03/20/2020
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: 30139ba6-e288-4ddb-9d78-0eb76ff62d1a
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# What is the administration service in Configuration Manager?

*Applies to: Configuration Manager (current branch)*

> [!Tip]  
> This feature was first introduced in version 1810 as a [pre-release feature](/sccm/core/servers/manage/pre-release-features). Beginning with version 1906, it's no longer a pre-release feature.  

The SMS Provider also provides API interoperability access over HTTPS, called the **administration service**. This REST API can be used in place of a custom web service to access information from the site. For more information, see [What is the administration service?](/configmgr/develop/adminservice/overview).

The **administration service** URL format is `https://<servername>/AdminService/wmi/<ClassName>` where `<servername>` is the server where the SMS Provider is installed and `<ClassName>` is a valid Configuration Manager WMI class name. In version 1810, this class name doesn't include the `SMS_` prefix. In version 1902 and later, this class name is the same as the WMI class name.

For example:

- 1810: `https://servername/AdminService/wmi/Site`
- 1902 and later: `https://servername/AdminService/wmi/SMS_Site`

> [!Note]  
> The administration service class names are case-sensitive. Make sure to use the proper capitalization, for example SMS_Site.

Make direct calls to this service with the Windows PowerShell cmdlet [Invoke-RestMethod](https://docs.microsoft.com/powershell/module/microsoft.powershell.utility/invoke-restmethod).

> [!Tip]  
> You can use this cmdlet in a task sequence. This action lets you access information from the site without requiring a custom web service to interface with the WMI provider.

You can also use it to access site data from Power BI using the OData connector option.

The administration service logs its activity to the **adminservice.log** file.

### Enable the administration service through the CMG

The **SMS Provider** appears as a role with an option to allow communication over the cloud management gateway (CMG). The current use for this setting is to enable application approvals via email from a remote device. For more information, see [Approve applications](/sccm/apps/deploy-use/app-approval).

#### Prerequisites

- The server that hosts the SMS Provider requires .NET 4.5.2 or later.  

    - Starting in version 1902, this prerequisite is version .NET 4.5 or later.  

- Enable the SMS Provider to use a certificate. Use one of the following options:  

    - Enable [Enhanced HTTP](/sccm/core/plan-design/hierarchy/enhanced-http) (recommended)  

        > [!Note]  
        > When the site creates a certificate for the SMS Provider, it won't be trusted by the web browser on the client. Based on your security settings, accessing the REST provider, you may see a security warning.  

    - Manually bind a PKI-based certificate to port 443 in IIS on the server that hosts the SMS Provider role  

#### Process to enable the API through the CMG

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Servers and Site System Roles** node.  

2. Select the server with the **SMS Provider** role.  

3. In the details pane, select the **SMS Provider** role, and select **Properties** in the ribbon on the **Site Role** tab.  

4. Select the option to **Allow Configuration Manager cloud management gateway traffic for administration service**.  


### Enable the Configuration Manager console to use the administration service

<!--4223683-->
Starting in version 1906, enable some nodes of the Configuration Manager console to use the administration service. This change allows the console to communicate with the SMS Provider over HTTPS instead of via WMI.

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node. In the ribbon, select **Hierarchy Settings**.

1. On the **General** page, select the option to **Enable the Configuration Manager console to use the administration service**.

In version 1906, it only affects the following nodes under the **Security** node in the **Administration** workspace:

- Administrative Users
- Security Roles
- Security Scopes
- Console Connections

When you select one of these nodes, if the following error message displays:

*Configuration Manager can't connect to the administration service*

Review the information below the error. Then verify that the administration service is enabled, configured, and functional.
