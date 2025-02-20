---
title: Link users and devices with user device affinity
titleSuffix: Configuration Manager
description: Link users and devices with user device affinity and automatically deploy apps to all devices associated with a user.
ms.date: 04/05/2021
ms.subservice: app-mgt
ms.service: configuration-manager
ms.topic: conceptual
author: baladelli
ms.author: baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# Link users and devices with user device affinity in Configuration Manager

*Applies to: Configuration Manager (current branch)*

User device affinity in Configuration Manager associates a user with one or more devices. This behavior can eliminate the need to know the names of a user's devices to deploy an application to the user. Instead of deploying the application to each of the user's devices, you deploy the application to the user. Then, user device affinity automatically makes sure that the application installs on all devices that are associated with that user.  

Define primary devices that users use every day for their work. When you create an affinity between a user and a device, you gain more app deployment options. For example, if a user requires Microsoft Visio, you can install it on the user's primary device by using a Windows Installer deployment. However, on a device that's not a primary device, you might deploy Visio as a virtual application. You also can use user device affinity to predeploy software on a user's device when the user isn't signed in. Then when the user logs on, the app is already installed and ready to run.  

You only manage user device affinity information for computers. Configuration Manager automatically manages user device affinities for the mobile devices that it enrolls.  

## Manually set up user device affinity  

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, and select the **Devices** node.  

1. Select a device. On the **Home** tab in the ribbon, in the **Device** group, choose **Edit Primary Users**.  

1. In the **Edit Primary Users** dialog box, search for and then select the users to add as primary users for the selected device. Choose **Add**.  

    > [!NOTE]  
    > The **Primary Users** list shows users who are already primary users of this device, and the method by which each user-device relationship was assigned.  

## Set up primary devices for a user  

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, and select the **Users** node.  

1. Select a user. On the **Device** tab in the ribbon, choose **Edit Primary Devices**.  

1. In the **Edit Primary Devices** dialog box, search for and then select the devices to add as primary devices for the selected user. Choose **Add**.  

    > [!NOTE]  
    > The **Primary Devices** list shows devices that are already set up as primary devices for this user, and the method by which each user-device relationship was assigned.  

## Automatically create user device affinities (Windows PCs only)

Configuration Manager reads data about user logon events from the Windows event log. To automatically create user device affinities, turn on these two options in the local security policy on client computers to store logon events in the Windows event log:  

- **Audit account logon events**  
- **Audit logon events**  

To configure these settings, use Windows Group Policy.  

> [!IMPORTANT]  
> If an error causes the Windows event log to generate a high number of entries, it might create a new event log. If this behavior occurs, existing logon events might not be available to Configuration Manager.  

### Set up the site to automatically create user device affinities  

1. In the Configuration Manager console, go to the **Administration** workspace, and select the **Client Settings** node.  

1. To modify the default client settings, select **Default Client Settings**. On the **Home** tab in the ribbon, in the **Properties** group, choose **Properties**. If you modify the default client settings, the site deploys them to all computers in the hierarchy. For more information, see [How to configure client settings](../../core/clients/deploy/configure-client-settings.md).

   - To create custom client agent settings, on the **Home** tab in the ribbon, in the **Create** group, choose **Create Custom Client Device Settings**.

1. In the **User and Device Affinity** group, set the following settings:  

    - **User device affinity threshold (minutes)**: Set the number of minutes of device usage before the site creates a user device affinity.  

    - **User device affinity threshold (days)**: Set the number of days over which the site measures the usage-based affinity threshold.  

    - **Automatically configure user device affinity from usage data**: Select **True** to let the site automatically create user device affinities. If you select **False**, you need to manually approve all user device affinity assignments.  

As an example, if you set **User device affinity threshold (minutes)** to **60** minutes and you set **User device affinity threshold (days)** to **5** days, the user must use the device for at least 60 minutes over a period of 5 days to automatically create a user device affinity.  

After Configuration Manager creates an automatic user device affinity, it continues to monitor the user device affinity thresholds. If the user's activity for the device falls below the thresholds you've set, the site removes the user device affinity. Set **User device affinity threshold (days)** to a value of at least seven days. This configuration avoids situations in which an automatically configured user device affinity might be lost while the user isn't signed in, for example, during the weekend.  

> [!Note]
> Starting in Configuration Manager version 2010, the troubleshooting portal in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) allows you to search for a user and view their associated devices. Tenant attached devices that are assigned user device affinity automatically based on usage are returned when searching for a user. For more information, see [Tenant attach: ConfigMgr client details in the admin center](../../tenant-attach/client-details.md#bkmk_list).

## Import user device affinities from a file

To create many relationships at one time, import a file that has the details for multiple user device affinities. Make sure the target devices are already discovered by the site and exist as resources in the Configuration Manager database.  

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, and select either the **Users** or **Devices** node.  

1. On the **Home** tab in the ribbon, in the **Create** group, choose **Import User Device Affinity**.  

1. In the Import User Device Affinity Wizard, on the **Choose Mapping** page, set this information:  

    - **File name**. Specify a comma-separated values (CSV) file that has a list of users and devices between which you want to create an affinity. In this file, each user-and-device pair must be on its own row, with values separated by a comma. Use this format: `<domain>\<username>,<device NetBIOS name>`  

    - **This file has column headings for reference purposes**. If the .csv file has a top-row header, select this option. The site ignores the header row during the import.  

1. If the file you import has more than two items in each row, use **Column** and **Assign** to specify which columns represent users and devices, and which columns to ignore during import.  

1. Complete the wizard.  


## Let users create their own device affinities

Set up a user to create their own user device affinity in Software Center.

### Set up the site to allow user-created user device affinity requests  

1  In the Configuration Manager console, go to the **Administration** workspace, and select the **Client Settings** node.  

1. To modify the default client settings, select **Default Client Settings**. On the **Home** tab in the ribbon, in the **Properties** group, choose **Properties**.

    To create custom client agent settings, on the **Home** tab in the ribbon, in the **Create** group, choose **Create Custom Client User Settings**.

    > [!NOTE]  
    > If you modify the default client settings, the site deploys them to all computers in the hierarchy. For more information, see [Configure client settings](../../core/clients/deploy/configure-client-settings.md).  

1. In the **User and Device Affinity** group, enable the setting to **Allow user to define their primary devices**.  

### Set up a user device affinity in Software Center

Users can use Software Center to set affinity.

1. In Software Center, go to the **Options** tab.

1. In the **Work information** section, select the option **I regularly use this computer to do my work**.

## Manage user device affinity requests from users

When you disable the client setting to **Automatically configure user device affinity from usage data**, you need to manually approve all user device affinity assignments.  

### Approve or reject a user device affinity request  

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace.  

1. Select the user or device collection for which you want to manage affinity requests.  

1. On the **Home** tab in the ribbon, in the **Collection** group, choose **Manage Affinity Requests**.  

1. In the **Manage User Device Affinity Requests** dialog box, select an affinity request, and then choose **Approve** or **Reject**.  

## Next steps

You can also use Microsoft Intune to find the primary use of an enrolled device. For more information, see [Find the primary user of an Intune device](/mem/intune-service/remote-actions/find-primary-user) in the Intune documentation.
