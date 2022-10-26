---
title: Create remote connection profiles
titleSuffix: Configuration Manager
description: Use Configuration Manager remote connection profiles to enable your users to remotely connect to work computers.
ms.date: 01/06/2020
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.author: banreetkaur
author: banreet
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Remote connection profiles in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Use Configuration Manager remote connection profiles to allow your users to remotely connect to work computers. These profiles let you deploy Remote Desktop Connection settings to users in your hierarchy. Users can access any of their primary work computers through Remote Desktop over a VPN connection.  

> [!IMPORTANT]  
> When you specify remote connection profile settings with Configuration Manager, the client stores the settings in Windows local policy. These settings might override Remote Desktop settings that you configure with another application. Additionally, if you use Windows Group Policy to configure Remote Desktop settings, the settings specified in the Group Policy will override Configuration Manager settings.

Configuration Manager creates a security group on clients, **Remote PC Connect**. When you deploy a remote connection profile, the client adds the primary users of the computer to this group. A local administrator can manually add or remove users to this group, but Configuration Manager updates the membership when it next evaluates compliance of the profile.

> [!IMPORTANT]  
> If the user device affinity relationship between a user and a device changes, Configuration Manager disables the remote connection profile and Windows Firewall settings to prevent connections to the computer.

## Prerequisites  

### External dependencies  

- If you want to enable users to connect from the internet, install and configure a Remote Desktop Gateway server. For more information about how to install and configure a Remote Desktop Gateway server, see [Remote Desktop Services - Access from anywhere](/windows-server/remote/remote-desktop-services/rds-plan-access-from-anywhere).

- If clients run a host-based firewall, it must enable the mstsc.exe program. When you configure a remote connection profile, enable the setting to **Allow Windows Firewall exception for connections on Windows domains and on private networks**. This setting allows Configuration Manager to automatically configure Windows Firewall.

    > [!TIP]
    > Group Policy settings to configure Windows Firewall can override the configuration that you set in Configuration Manager. If you use Group Policy to configure Windows Firewall, make sure that Group Policy settings don't block mstsc.exe.

    If clients run a different host-based firewall, manually configure this firewall dependency.  

### Configuration Manager dependencies  

- In order for a user to connect to a work computer, that computer must be a primary device of the user. For more information, see [Link users and devices with user device affinity](../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).

- To manage remote connection profiles, your user account needs specific permissions in Configuration Manager. The **Compliance Settings Manager** built-in role includes the permissions required to manage these profiles. For more information, see [Configure role-based administration](../../core/servers/deploy/configure/configure-role-based-administration.md).

## Security and privacy considerations

### Security considerations  

- Manually specify user device affinity instead of allowing users to identify their primary device. Don't enable usage-based configuration.

  - Before you can deploy a remote connection profile, you need to enable the option to **Allow all primary users of the work computer to remotely connect**. With this configuration, you should always manually specify user device affinity. Don't consider the information that Configuration Manager collects from users or from the device to be authoritative. If you deploy a profile, and a trusted administrative user doesn't specify user device affinity, unauthorized users might receive elevated privileges and can remotely connect to computers.

  - Configuration Manager collects usage-based information through state messages, which is a fast but insecure communication channel. To help mitigate this threat, use Server Message Block (SMB) signing or Internet Protocol security (IPsec) between client computers and the management point.

- Restrict local administrative rights on the site server computer. A local administrator on the site server can manually add members to the **Remote PC Connect** security group that Configuration Manager automatically creates and maintains. This action might cause an elevation of privileges because members receive Remote Desktop permissions.

### Privacy considerations  

When a user remotely connects to a work computer, they download a .wsrdp file. This file contains the device name and the Remote Desktop Gateway Server name. These values are required to create the Remote Desktop session. The .wsrdp file is downloaded and automatically saved locally. This file is overwritten the next time that the user runs a Remote Desktop session.  

## Create a profile

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, expand **Compliance Settings**, and select **Remote Connection Profiles**.  

1. On the **Home** tab of the ribbon, in the **Create** group, select **Create Remote Connection Profile**.  

1. On the **General** page of the **Create Remote Connection Profile Wizard**, specify a name and optional description for the profile. Both values have a maximum limit of 256 characters.  

1. On the **Profile Settings** page, specify the following settings:  

    - **Full name and port of the Remote Desktop Gateway server (optional)**: Specify the name of the Remote Desktop Gateway Server to use for connections. This value has the following requirements:

        - The server name can't be longer than 256 characters.
        - It can contain uppercase, lowercase, and numeric characters.
        - Aside from periods (`.`) between segments, and a colon (`:`) before the port, the only special characters are dash (`–`) and underscore (`_`).
        - Configuration Manager doesn't support the use of an internationalized domain name for this value.

    - **Allow connections only from computers that run Remote Desktop with Network Level Authentication**: Enabled by default, this setting adds an additional level of security for the connection. For more information, see [Grant Remote Desktop access](/windows-server/remote/remote-desktop-services/clients/remote-desktop-allow-access#why-allow-connections-only-with-network-level-authentication).

    - Enable the following connection settings:

        - **Allow remote connections to work computers**

        - **Allow all primary users of the work computer to remotely connect**

        - **Allow Windows Firewall exception for connections on Windows domains and on private networks**

        > [!IMPORTANT]  
        > All three settings must be the same before you can continue.

        Only disable these settings when you deploy a profile to turn off remote connections.

1. Complete the wizard.

The new profile is displayed in the **Remote Connection Profiles** node in the **Assets and Compliance** workspace.  

## Deploy

1. In the Configuration Manager console, go to the **Assets and Compliance** workspace, expand **Compliance Settings**, and select **Remote Connection Profiles**.

1. In the **Remote Connection Profiles** list, select the profile that you want to deploy. In the **Home** tab of the ribbon, in the **Deployment** group, select **Deploy**.  

1. In the **Deploy Remote Connection Profile** window, specify the following information:

    - **Collection**: Browse to select the device collection where you want to deploy the profile.

    - **Remediate noncompliant rules when supported**: Enable this setting to automatically remediate the profile settings when they're noncompliant on a device. The profile can be non-compliant when it doesn't exist.

    - **Allow remediation outside the maintenance window**: If you configure a maintenance window for the collection to which you deploy the profile, enable this option to let Configuration Manager remediate it outside the maintenance window. For more information, see [How to use maintenance windows](../../core/clients/manage/collections/use-maintenance-windows.md).

    - **Generate an alert**: Enable this option to configure a compliance alert.

    - **Specify the compliance evaluation schedule for this configuration baseline**: Specify a simple or custom schedule by which the client evaluates the profile.

1. Select **OK** to close the window and create the deployment.

### Client evaluation

The client evaluates the profile when a user signs in.

If a device leaves a collection to which you deploy a remote connection profile, Configuration Manager disables the settings on the device. However, for this process to occur correctly, you must have already deployed at least one configuration item or configuration baseline that contains a configuration item from your site.

### Conflict resolution

Don't deploy more than one remote connection profile with conflicting settings to the same device. For example, you deploy two profiles with different settings to the same collection. You only configure one profile deployment to **Remediate noncompliant rules when supported**. This deployment might override the settings in the other profile. Configuration Manager doesn't support this type of remote connection profile deployment.

## Monitor

In the Configuration Manager console, go to the **Monitoring** workspace, and select **Deployments**. In the **Deployments** list, select the remote connection profile deployment.

You can review summary information about the compliance of the remote connection profile deployment on the main page. To view more detailed information, select the profile deployment. Then on the **Home** tab of the ribbon, in the **Deployment** group, select **View Status**. This action opens the **Deployment Status** page.  

The **Deployment Status** page contains the following tabs:  

- **Compliant**: Displays the compliance of the remote connection profile based on the number of assets that are affected.

    > [!IMPORTANT]  
    > The client doesn't evaluate a remote connection profile if it's not applicable. However, it still reports compliant.

- **Error**: Displays a list of all errors for the selected remote connection profile deployment based on the number of assets that are affected.

- **Non-Compliant**: Displays a list of all noncompliant rules within the remote connection profile based on the number of assets that are affected.

- **Unknown**: Displays a list of all devices that didn't report compliance for the selected remote connection profile deployment, together with the current client status of the devices.

On any tab, open a rule to create a temporary subnode under the **Users** node in the **Assets and Compliance** workspace. This subnode contains all devices with the compliance state of the selected tab.

The **Asset Details** pane displays the devices with the selected compliance state for this profile. Open a device in the list to display additional information.

## Reports

Configuration Manager includes built-in reports that you can use to monitor information about remote connection profiles. These reports have the report category of **Compliance and Settings Management**.  

> [!IMPORTANT]  
> Use the wildcard character (`%`) when you use the parameters **Device filter** and **User filter** in the reports for compliance settings.  

For more information about how to configure reporting in Configuration Manager, see [Introduction to reporting](../../core/servers/manage/introduction-to-reporting.md).