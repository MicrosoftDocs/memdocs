---
title: "Create remote connection profiles"
titleSuffix: "Configuration Manager"
description: "Use System Center Configuration Manager remote connection profiles to enable your users to remotely connect to work computers."
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-compliance
ms.topic: conceptual
ms.assetid: 8c6eabc4-5dda-4682-b03e-3a450e6ef65a
author: aczechowski
manager: dougeby
ms.author: aaroncz
---

# Remote connection profiles in System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
Use System Center Configuration Manager remote connection profiles to allow your users to remotely connect to work computers when they are not connected to the domain or if their personal computers are connected over the Internet.  

 Users can connect to their work PC from the following device types:  

-   Computers that run Microsoft Windows  

-   Devices that run iOS  

-   Devices that run Android  

Remote connection profiles let you deploy Remote Desktop Connection settings to users in your Configuration Manager hierarchy. Users can then use the company portal to access any of their primary work computers through Remote Desktop by using the Remote Desktop Connection settings provided by the company portal.  

Microsoft Intune is required if you want users to connect to their work PCs by using the company portal. If you are not using Intune, users can still use the information from the remote connection profile to connect to their work PCs by using Remote Desktop over a VPN connection.  

> [!IMPORTANT]  
>  When you specify remote connection profile settings by using the Configuration Manager console, the settings are stored in the local policy of the client computer. These settings might override Remote Desktop settings configured by another application. Additionally, if you use Windows Group Policy to configure Remote Desktop settings, the settings specified in the Group Policy will override those configured by using Configuration Manager.  

 When you install Configuration Manager, a new security group, **Remote PC Connect**, is created. This group is populated when you deploy a remote connection profile that includes the primary users of the computer to which you deploy the profile. Although a local administrator can add user names to this group, these users will be removed from the group when deployed remote connection profiles are next evaluated for compliance.  

 If you manually add a user to this group, the user can initiate remote connections, but the connection information will not be published in the company portal.  

 If you manually remove from the group a user that has been added by Configuration Manager, Configuration Manager will automatically remediate this change by adding the user back when the remote connection profile is next evaluated for compliance.  

> [!IMPORTANT]  
>  If the user device affinity relationship between a user and a device changes (for example, the computer a user connects to, stops being a primary device of the user, Configuration Manager disables the remote connection profile and Windows Firewall settings to prevent connections to the computer.  

## Prerequisites  

### External dependencies  

|Dependency|More information|  
|----------------|----------------------|  
|Remote Desktop Gateway server.|If you want to enable users to connect on the Internet from outside the company domain, you must install and configure a Remote Desktop Gateway server.<br /><br /> If Remote Desktop or Terminal Services settings are managed by another application or Group Policy settings, remote connection profiles might not work correctly. When you deploy remote connection profiles from the Configuration Manager console, its settings are stored in the local policy of the client computer. These settings might override Remote Desktop settings that are configured by another application. Additionally, if you use Group Policy settings to configure Remote Desktop settings, the settings that are specified in the Group Policy settings override the settings that are configured by Configuration Manager.<br /><br /> For more information about how to install and configure a Remote Desktop Gateway server, see the Windows Server documentation.|  
|If client computers run a host-based firewall, it must enable the Mstsc.exe program.|When you configure a remote connection profile, you must enable the **Allow Windows Firewall exception for connections on Windows domains and on private networks** setting. When this setting is enabled, Configuration Manager automatically configures Windows Firewall to enable the Mstsc.exe program. However, if client computers run a different host-based firewall, you must manually configure this firewall dependency.<br /><br /> Group Policy settings to configure Windows Firewall can override the configuration that you set in Configuration Manager. If you use Group Policy to configure Windows Firewall, ensure that Group Policy settings do not block the Mstsc.exe program.|  

### Configuration Manager dependencies  

|Dependency|More information|  
|----------------|----------------------|  
|Configuration Manager must be connected to Microsoft Intune (known as a hybrid configuration).|For more information about connecting Configuration Manager to Microsoft Intune, see Manage Mobile Devices with Configuration Manager and Microsoft Intune.|  
|In order for a user to connect to a work computer on the company network, that computer must be a primary device of the user.|For more information about user device affinity, see [Link users and devices with user device affinity](/sccm/apps/deploy-use/link-users-and-devices-with-user-device-affinity).|  
|Specific security permissions must have been granted to manage remote connection profiles.|The **Compliance Settings Manager** security role includes the permissions required to manage remote connection profiles. For more information, see <br />[Configure role-based administration](/sccm/core/servers/deploy/configure/configure-role-based-administration).|  

## Security and privacy considerations for remote connection profiles  

### Security considerations  

|Security best practice|More information|  
|----------------------------|----------------------|  
|Manually specify user device affinity instead of allowing users to identify their primary device. In addition, do not enable usage-based configuration.|Because you must enable **Allow all primary users of the work computer to remotely connect** before you can deploy a remote connection profile, always manually specify user device affinity. Do not consider the information that is collected from users or from the device to be authoritative. If you deploy remote connection profiles and a trusted administrative user does not specify user device affinity, unauthorized users might receive elevated privileges and then be able to remotely connect to computers.<br /><br /> If you do enable usage-based configuration, this information is collected through state messages for which Configuration Manager does not provide security. To help mitigate this threat, use Server Message Block (SMB) signing or Internet Protocol security (IPsec) between client computers and the management point.|  
|Restrict local administrative rights on the site server computer.|A user who has local administrative rights on the site server can manually add members to the Remote PC Connect security group that Configuration Manager automatically creates and maintains. This might cause an elevation of privileges because members who are added to this group receive Remote Desktop permissions.|  

### Privacy considerations  

-   If a user initiates a connection to a work computer from the company portal, a file with a .rdp or .wsrdp extension is downloaded that contains the device name and the Remote Desktop Gateway Server name that is required to initiate the Remote Desktop session. The file extension depends on the operating system of the device. For example, the Windows 7 and Windows 8 operating systems use an .rdp file, and Windows 8.1 uses a .wsrdp file.  

-   The user can choose to open or save the .rdp file. If the user chooses to open the .rdp file, the file might be stored in the cache for the web browser, depending on the retention settings that are configured for the browser. If the user chooses to save the file, the file is not stored in the browser cache. The file is saved until the user manually deletes it.  

-   The .wsrdp file is downloaded and automatically saved locally. This file is overwritten the next time that the user runs a Remote Desktop session.  

-   Before you configure remote connection profiles, consider your privacy requirements.  


## Create a remote connection profile

1. In the Configuration Manager console, click **Assets and Compliance** > **Compliance Settings** > **Remote Connection Profiles**.  

2. On the **Home** tab, in the **Create** group, click **Create Remote Connection Profile**.  

3. On the **General** page of the **Create Remote Connection Profile Wizard**, specify a name and optional description for the profile using a maximum of 256 characters for each.  

4. On the **Profile** settings page, specify the following settings for the remote connection profile:  

   -   **Full name and port of the Remote Desktop Gateway server (optional)** - Specify the name of the Remote Desktop Gateway Server to be used for connections.  

       > [!NOTE]  
       >  Configuration Manager does not support an internationalized domain name to be used to specify a server in this box.  
       >   
       >  The server name must be no longer than 256 characters and can contain uppercase characters, lowercase characters, numeric characters, and the **–** and **_** characters, which are separated by periods.  

   -   **Allow connections only from computers that run Remote Desktop with Network Level Authentication**  

5. Select **Enabled** or **Disabled** for each of the following connection settings:  

   -   **Allow remote connections to work computers**  

   -   **Allow all primary users of the work computer to remotely connect**  

   -   **Allow Windows Firewall exception for connections on Windows domains and on private networks**  

   > [!IMPORTANT]  
   >  All three settings must be the same before you can proceed past this page of the wizard.  

6. On the **Summary** page, review the actions to be taken, and then complete the wizard.  

   The new remote connection profile is displayed in the **Remote Connection Profiles** node in the **Assets and Compliance** workspace.  

Deploy a remote connection profile  

1.  In the Configuration Manager console, click **Assets and Compliance** > **Compliance Settings** > **Remote Connection Profiles**.  

3.  In the **Remote Connection Profiles** list, select the remote connection profile that you want to deploy, and then, in the **Home** tab, in the **Deployment** group, click **Deploy**.  

4.  In the **Deploy Remote Connection Profile** dialog box, specify the following information:  

    -   **Collection** - Click **Browse** to select the device collection where you want to deploy the remote connection profile.  

    -   **Remediate noncompliant rules when supported** - Enable this to automatically remediate the remote connection profile when it is found to be noncompliant on a device, for example, when it is not present.  

    -   **Allow remediation outside the maintenance window** - If a maintenance window has been configured for the collection to which you deploy the remote connection profile, enable this option to let Configuration Manager remediate the remote connection profile outside the maintenance window. For more information about maintenance windows, see [How to use maintenance windows](/sccm/core/clients/manage/collections/use-maintenance-windows).  

    -   **Generate an alert** - Enable this option to configure an alert that is generated if the remote connection profile compliance is less than a specified percentage by a specified date and time. You can also specify whether you want an alert to be sent to System Center Operations Manager.  

    -   **Specify the compliance evaluation schedule for this configuration baseline** - Specify the schedule by which the deployed remote connection profile is evaluated on devices. You can specify either a simple or a custom schedule.  

    > [!TIP]  
    >  If a device leaves a collection to which a remote connection profile has been deployed, the remote connection profile settings are disabled on the device. However, for this process to occur correctly, you must have already deployed at least one configuration item or configuration baseline that contains a configuration item from your site.  
    >   
    >  The profile is evaluated by devices when the user logs on.  
    >   
    >  If two remote connection profiles are deployed to the same device collection, where in one profile **Remediate noncompliant rules when supported** is checked and in the other profile, the same option is not checked, and the two remote connection profiles contain different connection settings, then the profile in which the option is not checked might override the settings in the other profile. This type of remote connection profile deployment is not supported by Configuration Manager.  

5.  Click **OK** to close the **Deploy Remote Connection Profile** dialog box and to create the deployment.  

## Monitor a remote connection profile  

### View compliance results in the Configuration Manager console  

1.  In the Configuration Manager console, click **Monitoring** > **Deployments**.  

3.  In the **Deployments** list, select the remote connection profile deployment for which you want to review compliance information.  

4.  You can review summary information about the compliance of the remote connection profile deployment on the main page. To view more detailed information, select the remote connection profile deployment, and then on the **Home** tab, in the **Deployment** group, click **View Status** to open the **Deployment Status** page.  

     The **Deployment Status** page contains the following tabs:  

    -   **Compliant:** Displays the compliance of the remote connection profile based on the number of assets that are affected. You can double-click a rule to create a temporary node under the **Users** node in the **Assets and Compliance** workspace. This node contains all devices that are compliant with the remote connection profile. The **Asset Details** pane also displays the devices that are compliant with this profile. Double-click a device in the list to display additional information.  

        > [!IMPORTANT]  
        >  A remote connection profile is not evaluated if it is not applicable on a client device. However, it is returned as compliant.  

    -   **Error:** Displays a list of all errors for the selected remote connection profile deployment based on the number of assets that are affected. You can double-click a rule to create a temporary node under the **Users** node of the **Assets and Compliance** workspace. This node contains all devices that generated errors with this profile. When you select a device, the **Asset Details** pane displays the devices that the selected issue affects. Double-click a device in the list to display additional information about the issue.  

    -   **Non-Compliant:** Displays a list of all noncompliant rules within the remote connection profile based on the number of assets that are affected. You can double-click a rule to create a temporary node under the **Users** node of the **Assets and Compliance** workspace. This node contains all devices that are not compliant with this profile. When you select a device, the **Asset Details** pane displays the devices that the selected issue affects. Double-click a device in the list to display additional information about the issue.  

    -   **Unknown:** Displays a list of all devices that did not report compliance for the selected remote connection profile deployment, together with the current client status of the devices.  

5.  On the **Deployment Status** page, you can review detailed information about the compliance of the deployed remote connection profile. A temporary node is created under the **Deployments** node that helps you find this information again quickly.  

### View compliance results with reports  
 Configuration Manager includes built-in reports that you can use to monitor information about remote connection profiles. These reports have the report category of **Compliance and Settings Management**.  

> [!IMPORTANT]  
>  You must use a wildcard (%) character when you use the parameters **Device filter** and **User filter** in the reports for compliance settings.  

 For more information about how to configure reporting in Configuration Manager, see [Reporting in System Center Configuration Manager](/sccm/core/servers/manage/reporting).  
