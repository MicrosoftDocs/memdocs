---
# required metadata

title: Troubleshoot Exchange connectors
titleSuffix: Microsoft Intune
description: Troubleshoot issues related to the Intune on-premises Exchange connector.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 10/02/2019
ms.topic: troubleshooting
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: medium
ms.technology:
ms.assetid: a7e3c742-295b-40bb-9afa-17f243062500

# optional metadata

#audience:

ms.reviewer:
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Troubleshoot the Intune Exchange Connector

This article describes how to troubleshoot issues related to the Intune Exchange Connector.

## Before you start

Before you start troubleshooting an Exchange Connector issue in Intune, collect some basic information so that you’re working on a solid foundation. This approach can help you better understand the nature of the problem and resolve it more quickly.

- Verify that your process meets the installation requirements. See [Set up the on-premises Intune Exchange Connector](exchange-connector-install.md).
- Verify that your account has both Exchange and Intune administrator permissions.
- Note the complete and exact error message text, details, and where the message is displayed.
- Determine when the problem started: 
  - Are you setting up the connector for the first time? 
  - Did the connector work correctly and then fail?
  - If it was working, what changes occurred in the Intune environment, Exchange environment, or on the computer that runs the connector software?
- What is the MDM authority?
- What version of Exchange do you use?

### Use PowerShell to get more data on Exchange Connector issues

- To get a list of all mobile devices for a mailbox, use `Get-ActiveSyncDeviceStatistics -mailbox mbx`
- To get a list of SMTP addresses for a mailbox, use `Get-Mailbox -Identity user | select emailaddresses | fl`
- To get detailed information about a device's access state, use `Get-CASMailbox <upn> | fl`

## Review the connector configuration

Review the [on-premises Exchange connector requirements](exchange-connector-install.md#intune-exchange-connector-requirements) to make sure your environment and the connector is configured correctly. 

### General considerations for the connector

- Make sure your firewall and proxy servers allow communication between the server that hosts the Intune Exchange Connector and the Intune service.

- The computer that hosts the Intune Exchange Connector and the Exchange Client Access Server (CAS) should be domain-joined and on same LAN. Make sure that the required permissions are added for the account that’s used by the Intune Exchange connector.

- The notification account is used to retrieve *Autodiscover* settings. For more information about Autodisover in Exchange, see [Autodiscover service in Exchange Server](https://docs.microsoft.com/exchange/architecture/client-access/autodiscover?view=exchserver-2016).

- The Intune Exchange Connector sends a request to the EWS URL by using the notification account credentials to send notification email messages together with the *Get Started* link (to enroll in Intune). Use of the *Get Started* link to enroll is a requirement for Android non-Knox devices. Otherwise, these devices will be blocked by Conditional Access.

### Common issues for connector configurations

- **Account permissions**: In the Microsoft Intune Exchange Connector dialog box, make sure you've specified a user account that has the appropriate permissions to execute the [required Windows PowerShell Exchange cmdlets](exchange-connector-install.md#exchange-cmdlet-requirements).
- **Notification email messages**: Enable notifications and specify a notification account.
- **Client Access Server synchronization**: When configuring the Exchange Connector, specify a CAS that has the lowest network latency possible to the server hosting the Exchange connector. Communication latency between the CAS and the Exchange connector can delay device discovery, particularly when using Exchange Online Dedicated.
- **Synchronization schedule**: A user with a newly enrolled device could be delayed in getting access until the Exchange connector synchronizes with the Exchange CAS. A full sync takes place once a day, and a delta (quick) sync occurs several times a day. You can [manually force a quick sync or full sync](exchange-connector-install.md#manually-force-a-quick-sync-or-full-sync) to minimize delays.

## Next steps
The following articles can help resolve common problems and specific errors:

- [Resolve common problems for the Intune Exchange Connector](troubleshoot-exchange-connector-common-problems.md).
- [Resolve common Errors for the Intune Exchange Connector](troubleshoot-exchange-connector-common-errors.md).

Seek assistance from support or the Intune community:

- See [Get Support](../fundamentals/get-support.md) to use the Intune Console to help troubleshoot the issue, or to open a support case with Microsoft. 
- Post your issue in the [Microsoft Intune forums](https://social.technet.microsoft.com/Forums/en-US/home?forum=microsoftintuneprod).  
