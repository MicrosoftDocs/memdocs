---
title: Install the Exchange connector
titleSuffix: Configuration Manager
description: Install and configure the Exchange connector for Configuration Manager to manage mobile devices via ActiveSync.
ms.date: 12/31/2019
ms.prod: configuration-manager
ms.technology: configmgr-mdm
ms.topic: conceptual
ms.collection: tier3
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.localizationpriority: medium
ms.reviewer: mstewart,aaroncz 
---

# Install and configure the Exchange connector

*Applies to: Configuration Manager (current branch)*

Use this procedure to install and configure an Exchange Server connector to manage mobile devices. Configuration Manager supports only one connector in an Exchange organization.

Before you install the Exchange Server connector for Configuration Manager, make sure you have the required permissions and versions. For more information, see [Device management with Exchange and Configuration Manager](manage-mobile-devices-with-exchange-activesync.md#prerequisites).

## Exchange connection account

Decide which account will connect to the Exchange Client Access server to manage the mobile devices. The account can be the computer account of the site server or a Windows user account.

Then, configure this account in an Exchange role group to run the following Exchange Server cmdlets:

- **Clear-ActiveSyncDevice**  

- **Get-ActiveSyncDevice**  

- **Get-ActiveSyncDeviceAccessRule**  

- **Get-ActiveSyncDeviceStatistics**  

- **Get-ActiveSyncMailboxPolicy**  

- **Get-ActiveSyncOrganizationSettings**  

- **Get-ExchangeServer**  

- **Get-Mailbox**

- **Get-Recipient**  

- **Set-ADServerSettings**  

- **Set-ActiveSyncDeviceAccessRule**  

- **Set-ActiveSyncMailboxPolicy**  

- **Set-CASMailbox**  

- **New-ActiveSyncDeviceAccessRule**  

- **New-ActiveSyncMailboxPolicy**  

- **Remove-ActiveSyncDevice**  

- **Get-CasMailbox**  

- **Get-User**  

- **Set-ActiveSyncOrganizationSettings**  

The following Exchange Server management roles include these cmdlets:

- Recipient Management
- View-Only Organization Management
- Server Management

For more information, see [Understanding management role groups](/exchange/understanding-management-role-groups-exchange-2013-help) in the Exchange Server 2013 documentation.

> [!TIP]  
> If you try to install or use the Exchange Server connector without the required cmdlets, you'll see the following error in the EasDisc.log file on the site server computer: `Invoking cmdlet <cmdlet> failed`.

## Install the connector

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Hierarchy Configuration**, and then select **Exchange Server Connectors**.

1. On the **Home** tab of the ribbon, in the **Create** group, select **Add Exchange Server**.

1. On the **General** page of the Add Exchange Server wizard, select one of the Exchange Server environments:

    - **On-premises Exchange Server**: Specify a single server or a Client Access Server array for each Active Directory site.

        If the server or the array is offline, Configuration Manager tries to discover a Client Access Server to use. If that fails, Configuration Manager falls back to using a mailbox server to make a connection to a Client Access Server. When it retries the connection, it logs the following warnings in the EasDisc.log file on the site server computer: `Failed to open runspace for site <site_name>`.

    - **Hosted Exchange Server**: Specify the server address of your Exchange Online environment.

    Then select the primary site to run the Exchange Server connector.

1. On the **Account** page, specify the account to connect to the Exchange Server. For more information, see [Exchange connection account](#exchange-connection-account).

1. On the **Discovery** page, configure the synchronization schedule and rules for finding devices.

1. On the **Settings** page, configure the mobile device settings in the following groups:

    - **General**
    - **Password**
    - **Email Management**
    - **Security**
    - **Application**

    For more information, see [Exchange connector settings](manage-mobile-devices-with-exchange-activesync.md#policies).

    If you also enroll mobile devices by using Configuration Manager [on-premises MDM](../understand/manage-mobile-devices-with-on-premises-infrastructure.md), enable the option to **Allow external mobile device management**. This setting allows these mobile devices to continue receiving email from Exchange after Configuration Manager enrolls them.

1. Complete the wizard.

## Verify and monitor

Verify the installation of the Exchange Server connector with status messages and log files:

- Confirm that Site Component Manager successfully installed the Exchange Server connector. Look for message status ID **1015** from the **SMS_EXCHANGE_CONNECTOR** component.

    The installation can fail if the specified Client Access Server is offline. If Configuration Manager can't successfully install the connector, Configuration Manager retries the installation every 60 minutes. It continues to retry until the installation succeeds or you remove the Exchange Server connector.

- On the site server computer, review **SiteComp.log** for the following entry: `Component SMS_EXCHANGE_CONNECTOR flagged for installation`. It then logs the successful installation with the following text: `STATMSG: ID=1015`.

After you complete the installation, monitor the mobile devices that are found and managed by the connector. View the collections of mobile devices, and use the reports for mobile devices.

> [!NOTE]  
> Configuration Manager generates names for the mobile devices that it finds. It uses the format *user name*_*device type*. For example, **jdoe_WindowsPhone**. If a user has more than one mobile device that has the same device type, Configuration Manager displays the same name for these mobile devices in the console and in reports.  

## See also

- [Ports used by Configuration clients and site systems](../../core/plan-design/hierarchy/ports.md#BKMK_PortsExchangeConnectorHosted)
- [Proxy server support](../../core/plan-design/network/proxy-server-support.md#site-system-roles-that-use-a-proxy)
- [Security recommendations for mobile devices](../../core/clients/deploy/plan/security-and-privacy-for-clients.md#security-guidance-for-mobile-devices)
- [Privacy information for mobile devices that are managed with the Exchange Server connector](../../core/clients/deploy/plan/security-and-privacy-for-clients.md#privacy-information-for-the-exchange-server-connector)