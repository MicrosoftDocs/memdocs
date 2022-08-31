---
# required metadata
title: Connectivity health checks in Windows 365
titleSuffix:
description: Learn about the health checks that are automatically run on Azure network connections.
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

Connectivity errors can occur even when all connectivity health checks have successfully passed.

## View connectivity checks

1. Sign in to [windows365.microsoft.com](https://windows365.microsoft.com) > **Devices** > **Windows 365** > **Azure network connections**.
2. Select a connection in the list > **Overview** > **Connectivity and usage (preview)**.


An admin is also able to look at the connectivity history of a user to see if user might have experience failed connectivity check, or connectivity error in the last 14 days.

, while connectivity errors are unexpected network failures that might cause a user to drop connection to their Cloud PC e.g. interruption in your internet service by your Internet Service Vendor (ISV). 



## Connectivity checks

| Check | Failure description | Troubleshooting |
| --- | --- | --- |
| Azure Resource Availability Check | Azure resources are not up and running. | If this persists, contact Microsoft support. |
| DomainJoin | This Cloud PC isn't joined to a domain. | Try reprovisioning the Cloud PC or join it to a domain. |
| DomainReachable | This Cloud PC can't connect to the domain. | Check for an issue with your virtual network configuration by reviewing your [Azure network connection checks](troubleshoot-azure-network-connection). |
| DomainTrust | The domain doesn't trust this Cloud PC. | Make sure that the local device password matches the device password in the domain. |
| SxSStackListener | The side-by-side stack installed on the Cloud PC is malfunctioning or blocked. | Run the troubleshooting tool to fix this issue. |
| Unknown | This Cloud PC might not be running or the network isn't connected to the public Internet. | Run the troubleshooting tool to get more information. |
| UrlsAccesible | This Cloud PC is blocking traffic to [these URLs](requirements.md). | Unblock the URLs this Cloud PC uses to connect to Windows 365. |
| VM Power Status Check | This Cloud PC is powered off and an issue is preventing it from turning back on. |  If this persists, contact Microsoft support. |

If any of these issues persist, contact Microsoft support.

## User connectivity history report

The user connectivity history report shows when a user started a connection and when the connection finished. There are different ways a connection can start/finish and these are logged as activities in the report. The report shows of the following activities:

| Activity | Description |
| --- | --- | --- |
| Connection started | The user successfully connected to their Cloud PC. |
| Connection finished | The user signs out of their Cloud PC or finishes their work session. If the connection fails because of an unexpected network connectivity error, it's listed as a **Connection finished** with a **Failure** status.|
| Connectivity check | If the connection fails because of a failed connectivity check, the failed check is listed. |

Select any activity to get more information about the event.





<!-- ########################## -->
## Next steps

[Learn more about Azure network connections](azure-network-connections.md).
