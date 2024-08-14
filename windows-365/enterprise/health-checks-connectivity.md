---
# required metadata
title: Connectivity health checks in Windows 365
titleSuffix:
description: Learn about connectivity health checks.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 01/31/2024
ms.topic: how-to
ms.service: windows-365
ms.subservice: windows-365-enterprise
ms.localizationpriority: high
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: abpineda
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection:
- M365-identity-device-management
- tier2
---

# Connectivity health checks

Connectivity health checks are run on individual Cloud PCs and give information on the state of the Cloud PC's connection. These checks are constantly run by the Windows 365 service in the backend. When any of these checks fail, the end user won’t be able to connect to their Cloud PC.

You can review any failed connectivity checks and use the **Troubleshoot this connection** button to troubleshoot.

## View Cloud PC connectivity status

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Windows 365** > **All Cloud PCs**.
2. Select a connection in the list > **Overview** > **Performance (preview)**.

If the Cloud PC is connected, the status will show as **Available**.

If there is a problem with the Cloud PC's connection due to malfunctioning components, the status will show as **Unavailable**. Details appear on the right. Select **Troubleshoot this connection** to troubleshoot the issue.

## Connectivity errors

When a connectivity check fails, you'll see one of the following messages. Review the status pane to see more details. You can use the **Troubleshoot this connection** button to troubleshoot.

- **DomainJoin**: This Cloud PC isn't joined to a domain.
- **DomainReachable**: This Cloud PC can't connect to the domain. Review your Azure Virtual Network checks. 
- **DomainTrust**: The domain doesn't trust this Cloud PC. Make sure the local device password matches the device password in the domain. 
- **SxSStackListener**: The side-by-side stack installed on the Cloud PC is malfunctioning or blocked. 
- **Unknown**: This Cloud PC might not be running or the network isn't connected to the public Internet.
- **UrlsAccesibleCheck**: This Cloud PC is blocking traffic to [these URLs](requirements.md).

<!--
Possible different view of this data:

| Check | Failure description | Troubleshooting |
| --- | --- | --- |
| DomainJoin | This Cloud PC isn't joined to a domain. | Try reprovisioning the Cloud PC or join it to a domain. |
| DomainReachable | This Cloud PC can't connect to the domain. | Check for an issue with your virtual network configuration by reviewing your [Azure network connection checks](troubleshoot-azure-network-connection.md). |
| DomainTrust | The domain doesn't trust this Cloud PC. | Make sure that the local device password matches the device password in the domain. |
| SxSStackListener | The side-by-side stack installed on the Cloud PC is malfunctioning or blocked. | Run the troubleshooting tool to fix this issue. |
| Unknown | This Cloud PC might not be running or the network isn't connected to the public Internet. | Run the troubleshooting tool to get more information. |
| UrlsAccesible | This Cloud PC is blocking traffic to [these URLs](requirements.md). | Unblock the URLs this Cloud PC uses to connect to Windows 365. |

-->
If any of these issues persist, contact Microsoft support.

Connectivity errors can occur even when all connectivity health checks have successfully passed.

## User connectivity history report

The user connectivity history report shows when a user started a connection and when the connection finished. There are different ways a connection can start/finish and these are logged as activities in the report.

### View Connectivity history report

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) > **Devices** > **Windows 365** > **All Cloud PCs**.
2. Select a Cloud PC in the list > **Overview** > **Performance (preview)** > **View report** under **Connectivity status**.

### Activities

The report shows of the following activities:

| Activity | Description |
| --- | --- | --- |
| Connection started | The user successfully connected to their Cloud PC. |
| Connection finished | The user signs out of their Cloud PC or finishes their work session. If the connection fails because of an unexpected network connectivity error, it's listed as a **Connection finished** with a **Failure** status.|
| Connectivity check | If the connection fails because of a failed connectivity check, the failed check is listed. |

Select any activity to get more information about the event.

The connectivity history report will provide visibility to other activities within a 1-hour period of a connectivity error or failed check.  As an example, if a user attempts to connect to their Cloud PC, and is not able to, the health checks and successful sign-in activity within 1 hour prior/after of the error will show as well.  This allows an admin to evaluate an error, possible cause, and if/when the system became healthy again.

<!-- ########################## -->
## Next steps

[Learn more about Azure network connections](azure-network-connections.md).
