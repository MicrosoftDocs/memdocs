---
title: Support Center quickstart
titleSuffix: Configuration Manager
description: Quickly capture the state of a Configuration Manager client for troubleshooting.
ms.date: 04/05/2021
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: quickstart
author: banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Support Center quickstart guide

*Applies to: Configuration Manager (current branch)*

Support Center has powerful capabilities including troubleshooting and real-time log viewing. It can also be used in just a few minutes to capture the state of a Configuration Manager client computer. This ability includes accessing remote clients.

Create a complete *troubleshooting bundle* file (.zip) that captures the client state. The bundle doesn't only contain log files. It can include other types of data such as registry settings and client configurations. Provide the bundle to a support technician who uses Support Center Viewer.

## Prerequisites

- Local administrative rights to a Configuration Manager client

- The Support Center installer. This file is on the site server at `cd.latest\SMSSETUP\Tools\SupportCenter\SupportCenterInstaller.msi`. For more information, see [Support Center - Install](support-center.md#install).

## Step 1: Create a data bundle on a local client

1. Install Support Center on the Configuration Manager client.

1. Go to the **Start** menu, in the **Microsoft Endpoint Manager** group, select the option based on your site version:

    - For version 2103 and later: Select **Support Center Client Data Collector**.

    - For version 2010 and earlier: Select **Support Center**.

1. On the Home tab of the ribbon, select **Collect selected data**.

    By default, Support Center only collects the minimum data set:

      - **Client log files**: All log files from the Configuration Manager clients, by default in `C:\Windows\CCM\logs`. It also includes log files for client setup, by default in `C:\Windows\ccmsetup\Logs`.

      - **Client configuration**: Information from the Configuration Manager client. For example, the version, the assigned site and management point, and if it's internet facing. This option is always enabled.

      - **Operating system**: Information about the computer. For example, Windows install, network adapters, and system services. This option is always enabled.

    :::image type="content" source="media/support-center-client-data-collector.png" alt-text="Collect selected data option in Support Center Client Data Collector":::

1. Save the troubleshooting bundle file (.zip) to a folder on the computer. By default, the file name is similar to the following example: `Support_c885cdfed3c7482bba4f9e662978ec07.zip`.

## Step 2: View the data bundle using Support Center Viewer

1. Start **Support Center Viewer**. This action can happen on any computer with Support Center.

1. Select **Open bundle**, browse to the bundle file, and select **Open**.

    :::image type="content" source="media/support-center-viewer.png" alt-text="Support Center Viewer with an open bundle":::

1. After Support Center Viewer processes the file, switch to each available tab. View the types of data that Support Center collects by default:

    - **Configuration** tab

        - Configuration Manager client configuration

        - Operating system

        - Computer

        - Services

        - Network adapters

    - **Logs** tab: Choose one or more entries in the list, and select **Open**. This action opens the selected log files in Log Viewer. Use this feature to look up error codes, and use advanced filters to help you more quickly analyze log files.

## Collect more data

Beyond these basic capabilities, Support Center can also collect a wide variety of other client state information. Open **Support Center Client Data Collector** and select **Collect all data**. This process typically lasts several minutes, even on newer computers. Support Center collects the following data:

:::image type="content" source="media/support-center-client-data-collector-all-data.png" alt-text="Collect all data option in Support Center Client Data Collector":::

- **Policy**: Configuration Manager policy settings, including both the requested policy configuration and the actual policy configuration.

- **Client WMI**: Client configuration information from WMI. Support Center doesn't collect client policy.

- **Certificates**: Public key information for client certificates. Support Center doesn't collect certificate private keys.

- **Debug dumps**: Collect a debug dump of client and related processes. Debug dumps can be large. Only enable this option when troubleshooting issues with client performance.

    > [!WARNING]
    > Collecting debug dumps will cause data bundles to become very large. In some cases, the size can be several hundred MB.
    >
    > Debug dumps may contain sensitive information, including passwords, cryptographic secrets, or user data. Only collect debug dumps on the recommendation of Microsoft Support personnel. Carefully handle data bundles that contain debug dumps to protect them from unauthorized access.
    >
    > This data type isn't supported when you make a remote connection to another client.

- **Client registry**: Collects client configuration information from the registry. Support Center only collects Configuration Manager registry information.

- **Troubleshooting**: Real-time troubleshooting data to help diagnose common client problems with Active Directory, management points, networking, policy assignments, and registration.

    > [!NOTE]
    > This data type isn't supported when you make a remote connection to another client.

- **Windows Update log files**: Collects log files for Windows Updates, which are necessary when troubleshooting issues with software updates.

## Next steps

[User interface reference](support-center-ui-reference.md)
