---
# required metadata
title: Accessing Cloud PCs
titleSuffix:
description: Learn how end-users can access their Cloud PC.
keywords:
author: ErikjeMS  
ms.author: erikje
manager: dougeby
ms.date: 09/03/2021
ms.topic: how-to
ms.service: cloudpc
ms.subservice:
ms.localizationpriority: high
ms.technology:
ms.assetid: 

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: ivivano
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure; get-started
ms.collection: M365-identity-device-management
---

# Access a Cloud PC

End users can access their Cloud PCs in two different ways:

- [windows365.microsoft.com](https://Windows365.microsoft.com)
- Microsoft Remote Desktop

For information on hardware requirements, see [End user hardware requirements](end-user-hardware-requirements.md).

## Windows365 web site

End users can navigate to [windows365.microsoft.com](https://windows365.microsoft.com) to access their Cloud PCs.  

### Software requirements

To access their Cloud PC from this website, the end user's device must meet the following requirements:

- Supported operating systems: Windows, macOS, ChromeOS, Linux
- A modern browser like Microsoft Edge, Google Chrome, Safari, or Mozilla Firefox (v55.0 and later).

### End-user actions

While on windows365.microsoft.com, end users can perform actions on their Cloud PCs by selecting the gear icon on a Cloud PC card.

- **Rename**: Changes the name of the Cloud PC shown to the user on the web site. This action won’t affect any name in Microsoft Endpoint Manager, Azure Active Directory, on the device, or in the Remote Desktop Apps.  
- **Restart**: Restarts the Cloud PC.
- **Troubleshoot**: Troubleshoot and attempt to resolve any issues that may be preventing a user from connecting to their Cloud PC. The checks run include:
    - Check whether any files or agents required for connectivity are correctly installed.
    - Make sure that the Azure resources are available.

  | Return state | Description |
  | ------------- | ------------- |
  | No issues detected | None of the checks discovered an issue with the Cloud PC. |
  | Issues resolved  | An issue was detected and fixed. |
  | Can’t connect to Cloud PC. We’re working to fix it, try again later. | A Microsoft service required for connectivity is unavailable. Try connecting again later. |
  | We couldn’t fix issues with your Cloud PC. Contact your administrator. | An issue was detected but it couldn't be fixed. This issue exists because of an ongoing Windows update or another issue. If this error persists for an extended period of time, the Cloud PC may need to be reprovisioned. |

## Remote Desktop

The Microsoft Remote Desktop app lets users access and control a remote PC, including a Cloud PC.

For a list of clients by operating system, see [Remote Desktop clients](/windows-server/remote/remote-desktop-services/clients/remote-desktop-clients). For a comparison of features by client, see [Compare the clients: features](/windows-server/remote/remote-desktop-services/clients/remote-desktop-features#client-features).

### Install the Microsoft Remote Desktop app

To set up their Remote Desktop client, users follow these steps:

1. Download the Remote Desktop app from the [Remote Desktop clients page](/windows-server/remote/remote-desktop-services/clients/remote-desktop-clients).
2. Select **Subscribe**.
3. Enter their Azure Active Directory credentials.
4. The Cloud PC appears in the list, and they can double-click it to launch.

<!-- ########################## -->
## Next steps

For information about the different protocol network requirements per scenario, see [Network requirements](./enterprise/requirements-network.md).