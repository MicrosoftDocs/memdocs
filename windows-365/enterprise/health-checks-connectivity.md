---
# required metadata
title: Connectivity health checks in Windows 365
titleSuffix:
description: Learn about connectivity health checks.
keywords:
author: ErikjeMS
ms.author: erikje
manager: dougeby
ms.date: 08/31/2022
ms.topic: how-to
ms.service: cloudpc
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: abpineda
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# Connectivity health checks

Connectivity health checks are run on individual Cloud PCs and give information on the state of the Cloud PC's connection. These checks are constantly run by the Windows 365 service in the backend. When any of these checks fail, the end user won’t be able to connect to their Cloud PC.

You can review any connectivity errors and use the **Troubleshoot this connection** button to troubleshoot.

## View Cloud PC connectivity status

1. Sign in to [windows365.microsoft.com](https://windows365.microsoft.com) > **Devices** > **Windows 365** > **All Cloud PCs**.
2. Select a connection in the list > **Overview** > **Connectivity and usage (preview)**.

If the Cloud PC is connected, the status will show as **Available**.

If there is a problem with the Cloud PC's connection, the status will show as **Unavailable**. Details appear on the right. Select **Troubleshoot this connection** to troubleshoot the issue.

## Connectivity errors

When a connectivity checks fails, you'll see one of the following errors. Review the status pane to see more details. You can use the **Troubleshoot this connection** button to troubleshoot.

- **Azure Resource Availability Check**: Azure resources are not up and running.
- **DomainJoin**: This Cloud PC isn't joined to a domain.
- **omainReachable**: This Cloud PC can't connect to the domain.
- **DomainTrust**: The domain doesn't trust this Cloud PC.
- **SxSStackListener**: The side-by-side stack installed on the Cloud PC is malfunctioning or blocked. 
- **Unknown**: This Cloud PC might not be running or the network isn't connected to the public Internet.
- **UrlsAccesible**: This Cloud PC is blocking traffic to [these URLs](requirements.md).
- **VM Power Status Check**: This Cloud PC is powered off and an issue is preventing it from turning back on.

If any of these issues persist, contact Microsoft support.

Connectivity errors can occur even when all connectivity health checks have successfully passed.

## User connectivity history report

The user connectivity history report shows when a user started a connection and when the connection finished. There are different ways a connection can start/finish and these are logged as activities in the report.

### View Connectivity history report

1. Sign in to [windows365.microsoft.com](https://windows365.microsoft.com) > **Devices** > **Windows 365** > **All Cloud PCs**.
2. Select a connection in the list > **Overview** > **Connectivity and usage (preview)** > **View connectivity history**.

### Activities

The report shows of the following activities:

| Activity | Description |
| --- | --- | --- |
| Connection started | The user successfully connected to their Cloud PC. |
| Connection finished | The user signs out of their Cloud PC or finishes their work session. If the connection fails because of an unexpected network connectivity error, it's listed as a **Connection finished** with a **Failure** status.|
| Connectivity check | If the connection fails because of a failed connectivity check, the failed check is listed. |

Select any activity to get more information about the event.

<!-- ########################## -->
## Next steps

[Learn more about Azure network connections](azure-network-connections.md).
