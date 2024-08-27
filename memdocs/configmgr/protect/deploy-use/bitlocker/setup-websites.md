---
title: Set up BitLocker portals
titleSuffix: Configuration Manager
description: Install the BitLocker management components for the self-service portal, and the administration and monitoring website
ms.date: 09/15/2020
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

# Set up BitLocker portals

*Applies to: Configuration Manager (current branch)*

<!--3601034-->

To use the following BitLocker management components in Configuration Manager, you first need to install them:

- User self-service portal
- Administration and monitoring website (helpdesk portal)

You can install the portals on an existing site server or site system server with IIS installed, or use a standalone web server to host them.

> [!NOTE]
> Starting in version 2006, you can install the BitLocker self-service portal and the administration and monitoring website at the central administration site.<!-- 5925693 -->
>
> In version 2002 and earlier, only install the self-service portal and the administration and monitoring website with a primary site database. In a hierarchy, install these websites for each primary site.

Before you start, confirm the [prerequisites](../../plan-design/bitlocker-management.md#prerequisites) for these components.

## Run the script

On the target web server, do the following actions:

> [!NOTE]
> Depending upon your site design, you may need to run the script multiple times. For example, run the script on the management point to install the administration and monitoring website. Then run it again on a standalone web server to install the self-service portal.

1. Copy the following files from `SMSSETUP\BIN\X64` in the Configuration Manager installation folder on the site server to a local folder on the target server:

    - `MBAMWebSite.cab`
    - `MBAMWebSiteInstaller.ps1`

1. Run PowerShell as an administrator, and then run the script similar to the following command line:

    ``` PowerShell
    .\MBAMWebSiteInstaller.ps1 -SqlServerName <ServerName> -SqlInstanceName <InstanceName> -SqlDatabaseName <DatabaseName> -ReportWebServiceUrl <ReportWebServiceUrl> -HelpdeskUsersGroupName <DomainUserGroup> -HelpdeskAdminsGroupName <DomainUserGroup> -MbamReportUsersGroupName <DomainUserGroup> -SiteInstall Both
    ```

    For example,

    ``` PowerShell
    .\MBAMWebSiteInstaller.ps1 -SqlServerName sql.contoso.com -SqlInstanceName instance1 -SqlDatabaseName CM_ABC -ReportWebServiceUrl https://rsp.contoso.com/ReportServer -HelpdeskUsersGroupName "contoso\BitLocker help desk users" -HelpdeskAdminsGroupName "contoso\BitLocker help desk admins" -MbamReportUsersGroupName "contoso\BitLocker report users" -SiteInstall Both
    ```

    > [!IMPORTANT]
    > This example command line uses all of the possible parameters to show their usage. Adjust your use according to your requirements in your environment.

After installation, access the portals via the following URLs:

- Self-service portal: `https://webserver.contoso.com/SelfService`
- Administration and monitoring website: `https://webserver.contoso.com/HelpDesk`

> [!NOTE]
> Microsoft recommends but doesn't require the use of HTTPS. For more information, see [How to set up SSL on IIS](/iis/manage/configuring-security/how-to-set-up-ssl-on-iis).

## Script usage

This process uses a PowerShell script, MBAMWebSiteInstaller.ps1, to install these components on the web server. It accepts the following parameters:

- `-SqlServerName <ServerName>` (required): The fully qualified domain name of the primary site database server.

- `-SqlInstanceName <InstanceName>`: The SQL Server instance name for the primary site database. If SQL Server uses the default instance, don't include this parameter.

- `-SqlDatabaseName <DatabaseName>` (required): The name of the primary site database, for example `CM_ABC`.

- `-ReportWebServiceUrl <ReportWebServiceUrl>`: The web service URL of the primary site's reporting service point. It's the **Web Service URL** value in **Reporting Services Configuration Manager**.

    > [!NOTE]
    > This parameter is to install the **Recovery Audit Report** that's linked from the administration and monitoring website. By default Configuration Manager includes the other BitLocker management reports.

- `-HelpdeskUsersGroupName <DomainUserGroup>`: For example, `contoso\BitLocker help desk users`. A domain user group whose members have access to the **Manage TPM** and **Drive Recovery** areas of the administration and monitoring website. When using these options, this role needs to fill in all fields, including the user's domain and account name.

- `-HelpdeskAdminsGroupName <DomainUserGroup>`: For example, `contoso\BitLocker help desk admins`. A domain user group whose members have access to all recovery areas of the administration and monitoring website. When helping users recover their drives, this role only has to enter the recovery key.

- `-MbamReportUsersGroupName <DomainUserGroup>`: For example, `contoso\BitLocker report users`. A domain user group whose members have read-only access to the **Reports** area of the administration and monitoring website.

    > [!NOTE]
    > The installer script doesn't create the domain user groups that you specify in the **-HelpdeskUsersGroupName**, **-HelpdeskAdminsGroupName**, and **-MbamReportUsersGroupName** parameters. Before you run the script, make sure to create these groups.
    >
    > When you specify the **-HelpdeskUsersGroupName**, **-HelpdeskAdminsGroupName**, and **-MbamReportUsersGroupName** parameters, make sure to specify both the domain name and the group name. Use the format `"domain\user_group"`. Don't exclude the domain name. If the domain name or group name contains spaces or special characters, enclose the parameter in quotation marks (`"`).

- `-SiteInstall Both`: Specify which of the components to install. Valid options include:
  - `Both`: Install both components
  - `HelpDesk`: Install only the administration and monitoring website
  - `SSP`: Install only the self-service portal

- `-IISWebSite`: The website where the script installs the MBAM web applications. By default, it uses the IIS default website. Create the custom website before using this parameter.

- `-InstallDirectory`: The path where the script installs the web application files. By default, this path is `C:\inetpub`. Create the custom directory before using this parameter.

- `-DomainName` *applies to version 2002 and later*: Specify the NetBIOS domain name of the server with the help desk or self-service web portal role. Only necessary if the NetBIOS domain name doesn't match the DNS domain name. This configuration is also known as a disjointed domain namespace. For example, `-DomainName fabrikham` where the DNS domain name is `contoso.com`.<!-- MEMDocs #759 -->

- -IncludePortInSPN information about this parameter should be specified which will help admins to use them when they use http based SPNs. Also reference for this article should be mentioned to help them out. https://learn.microsoft.com/en-us/troubleshoot/windows-server/system-management-components/error-0x80090322-when-connecting-powershell-to-remote-server-via-winrm

- `-Uninstall`: Uninstalls the BitLocker Management Help Desk/Self-Service web portal sites on a web server where they have been previously installed.

## Verify

Monitor and troubleshoot using the following logs:

- Windows Event logs under **Microsoft-Windows-MBAM-Web**. For more information, see [About BitLocker event logs](../../tech-ref/bitlocker/about-event-logs.md) and [Server event logs](../../tech-ref/bitlocker/server-event-logs.md).

- Trace logs for each component are in the following default locations:

  - Self-service portal: `C:\inetpub\Microsoft BitLocker Management Solution\Logs\Self Service Website`

  - Administration and monitoring website: `C:\inetpub\Microsoft BitLocker Management Solution\Logs\Help Desk Website`

For more troubleshooting information, see [Troubleshoot BitLocker](../../tech-ref/bitlocker/troubleshoot.md).

## Next steps

[Customize the self-service portal](customize-self-service-portal.md)

For more information on using the components that you installed, see the following articles:

- [BitLocker administration and monitoring website](helpdesk-portal.md)
- [BitLocker self-service portal](self-service-portal.md)
