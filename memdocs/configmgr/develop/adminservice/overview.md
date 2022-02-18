---
title: What is the administration service
titleSuffix: Configuration Manager
description: Use the Configuration Manager administration service REST API to interact with the site over an HTTPS OData connection.
ms.date: 12/21/2021
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: overview
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth
---

# What is the administration service in Configuration Manager?

*Applies to: Configuration Manager (current branch)*

The [SMS Provider](../../core/plan-design/hierarchy/plan-for-the-sms-provider.md) provides API interoperability access over HTTPS, called the **administration service**. The administration service is a representational state transfer (REST) API based on the Open Data (OData) v4 protocol.

The administration service currently has two layers or routes:

- Administration service > WMI > SQL: `https://<SMSProviderFQDN>/AdminService/wmi/<ClassName>`

    The **WMI** route supports both GET and POST commands to over 700 classes.

- Administration service > OData/SQL: `https://<SMSProviderFQDN>/AdminService/v1.0/<ClassName>`

    This versioned route (**v1.0**) supports new Configuration Manager functionality.

The `<ClassName>` value is a valid Configuration Manager class name. The administration service class names are case-sensitive. Make sure to use the proper capitalization. For example, `SMS_Site`.

## Scenarios

Configuration Manager natively uses the administration service for the following features:

- [Email approval of apps](../../apps/deploy-use/app-approval.md#bkmk_email-approve)

- [View recently connected consoles](../../core/servers/manage/admin-console.md#bkmk_viewconnected)

- The **Security** [node of the console](set-up.md#enable-console-usage)

- Microsoft Endpoint Manager [tenant attach](../../tenant-attach/device-sync-actions.md)

- [Community hub](../../core/servers/manage/community-hub.md)

- [Managing console extensions](../../core/servers/manage/admin-console-extensions.md)<!--1104776-->

In addition, you can develop custom solutions with the administration service, for example:

- Replace a custom web service to access information from the site.

- In PowerShell scripts that you run directly from the Configuration Manager console. For more information, see [Create and run PowerShell scripts from the Configuration Manager console](../../apps/deploy-use/create-deploy-scripts.md).

- A PowerShell script in a task sequence. This action lets you access information from the site without requiring a custom web service to interface with the WMI provider. For more information, see [Task sequence steps - Run PowerShell Script](../../osd/understand/task-sequence-steps.md#BKMK_RunPowerShellScript).

- Access site data from Power BI using the OData connector option.

## Prerequisites

Configure the following prerequisites on the server that hosts the SMS Provider role:

- In version 2006 and earlier, enable the Windows server role **Web Server (IIS)**. Starting in version 2010, this role is no longer required.

- Starting in version 2107, the SMS Provider requires .NET version 4.6.2, and version 4.8 is recommended.<!--10402814--> In version 2103 and earlier, this role requires .NET 4.5 or later. For more information, [Site and site system prerequisites](../../core/plan-design/configs/site-and-site-system-prerequisites.md#net-version-requirements).

- You may need to enable secure HTTPS communication with a trusted certificate. For more information, see [Enable secure HTTPS communication](set-up.md#enable-secure-https-communication).

To access the administration service, your user account needs to be an administrative user in Configuration Manager. If you access the administration service via a cloud management gateway, you need to have an account in Azure Active Directory (Azure AD).

For more information on scalability of the SMS Provider and administration service, see [Size and scale numbers](../../core/plan-design/configs/size-and-scale-numbers.md#sms-provider).

> [!NOTE]
> For any machine with the Configuration Manager console, if it's using a proxy server, the console fails to connect to the administration service. For example, when trying to access the **Security** nodes, you may see errors that the administration service isn't enabled or available. The **SmsAdminUI.log** file shows errors such as, `Failed to get a response for OData query.`<!-- known issue 12468490 -->
>
> To work around this issue, either remove the proxy configuration from the machine, or make the following configuration change:<!-- 12468037 -->
>
> 1. Manually edit the following XML file: `C:\Program Files (x86)\Microsoft Endpoint Manager\AdminConsole\bin\Microsoft.ConfigurationManagement.exe.config`
> 1. Configure the `<defaultproxy>` behavior with one of the following options:
>     1. Set `enabled="false"`
>     1. Add the FQDN of the SMS Provider to the `<bypasslist>`.
>
>    For more information, see [`<defaultProxy>` Element (Network Settings)](/dotnet/framework/configure-apps/file-schema/network/defaultproxy-element-network-settings).

## Next steps

> [!div class="nextstepaction"]
> [How to set up the administration service](set-up.md)
