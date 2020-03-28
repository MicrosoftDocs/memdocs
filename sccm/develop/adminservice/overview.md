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

The [SMS Provider](/configmgr/core/plan-design/hierarchy/plan-for-the-sms-provider) provides API interoperability access over HTTPS, called the **administration service**. The administration service is a representational state transfer (REST) API based on the Open Data (OData) v4 protocol.

> [!Tip]  
> This feature was first introduced in version 1810 as a [pre-release feature](/sccm/core/servers/manage/pre-release-features). Beginning with version 1906, it's no longer a pre-release feature.  

The administration service currently has two layers or routes:

- Administration service > WMI > SQL: `https://<SMSProviderFQDN>/AdminService/wmi/<ClassName>`

    The WMI route supports both GET and POST commands to over 700 classes.

- Administration service > OData/SQL: `https://<SMSProviderFQDN>/AdminService/v1/<ClassName>`

    This versioned route supports new Configuration Manager functionality.

The `<ClassName>` value is a valid Configuration Manager class name. The administration service class names are case-sensitive. Make sure to use the proper capitalization. For example, `SMS_Site`.

> [!NOTE]
> In Configuration Manager version 1810, this class name didn't include the `SMS_` prefix. In version 1902 and later, for better consistency, the administration service class names are the same as the WMI class names.

## Scenarios

Configuration Manager natively uses the administration service for the following features:

- [Email approval of apps](/configmgr/apps/deploy-use/app-approval#bkmk_email-approve)

- [View recently connected consoles](/configmgr/core/servers/manage/admin-console#bkmk_viewconnected)

- The **Security** [node of the console](/configmgr/develop/adminservice/set-up#bkmk_console) (version 1906 and later)

- Microsoft Endpoint Manager [tenant attach](/configmgr/tenant-attach/device-sync-actions) (version 2002 and later)

<!-- - Community Hub -->

In addition, you can develop custom solutions with the administration service, for example:

- Replace a custom web service to access information from the site.

- In PowerShell scripts that you run directly from the Configuration Manager console. For more information, see [Create and run PowerShell scripts from the Configuration Manager console](/configmgr/apps/deploy-use/create-deploy-scripts).

- A PowerShell script in a task sequence. This action lets you access information from the site without requiring a custom web service to interface with the WMI provider. For more information, see [Task sequence steps - Run PowerShell Script](/configmgr/osd/understand/task-sequence-steps#BKMK_RunPowerShellScript).

- Access site data from Power BI using the OData connector option.

## Prerequisites

Configure the following prerequisites on the server that hosts the SMS Provider role:

- Install the .NET Framework version 4.5 or later.

    > [!NOTE]
    > Configuration Manager version 1810 requires .NET 4.5.2 or later.

- Enable secure HTTPS communication with a trusted certificate. For more information, see [Enable secure HTTPS communication](/configmgr/develop/adminservice/set-up#bkmk_https).

## Next steps

> [!div class="nextstepaction"]
> [How to set up the administration service](/configmgr/develop/adminservice/set-up)
