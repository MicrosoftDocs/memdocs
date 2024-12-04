---
title: Configuration Manager console
titleSuffix: Configuration Manager
description: Learn about navigating through the Configuration Manager console.
ms.date: 12/04/2024
ms.subservice: core-infra
ms.service: configuration-manager
ms.topic: conceptual
author: Baladelli    
ms.author: Baladell
manager: apoorvseth
ms.localizationpriority: medium
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# How to use the Configuration Manager console

*Applies to: Configuration Manager (current branch)*

Administrators use the Configuration Manager console to manage the Configuration Manager environment. This article covers the fundamentals of navigating the console.  

## <a name="bkmk_open"></a> Open the console

The Configuration Manager console is always installed on every site server. You can also install it on other computers. For more information, see [Install the Configuration Manager console](../deploy/install/install-consoles.md).

The simplest method to open the console on a Windows computer is to go to **Start** and start typing `Configuration Manager console`. You may not need to type the entire string for Windows to find the best match.

If you browse the Start menu, look for the **Configuration Manager console** icon in the **Microsoft Endpoint Manager** group.

:::image type="content" source="media/microsoft-endpoint-manager-start-menu.png" alt-text="Microsoft Endpoint Manager start menu icons.":::

## Connect to a site server

The console connects to your central administration site server or to your primary site servers. You can't connect a Configuration Manager console to a secondary site. During installation, you specified the fully qualified domain name (FQDN) of the site server to which the console connects.

To connect to a different site server, use the following steps:

1. Select the arrow at the top of the [ribbon](#ribbon), and choose **Connect to a New Site**.

    :::image type="content" source="media/connect-to-a-new-site.png" alt-text="Connect the console to a new site.":::

1. Type in the FQDN of the site server. If you've previous session to site server, select the server from the drop-down list.

    :::image type="content" source="media/site-server-fqdn.PNG" alt-text="Site Connection window, enter the FQDN of the site server.":::

1. Select **Connect**.

> [!TIP]
> You can specify the minimum authentication level for administrators to access Configuration Manager sites. This feature enforces administrators to sign in to Windows with the required level. For more information, see [Plan for the SMS Provider](../../plan-design/hierarchy/plan-for-the-sms-provider.md#authentication). <!--1357013-->

## Navigation

Some areas of the console may not be visible depending on your assigned security role. For more information about roles, see [Fundamentals of role-based administration](../../understand/fundamentals-of-role-based-administration.md).

### Workspaces

The Configuration Manager console has four **workspaces**:

- **Assets and Compliance**

- **Software Library**

- **Monitoring**

- **Administration**

:::image type="content" source="media/configuration-manager-workspaces.png" alt-text="Configuration Manager workspaces with context menu.":::

Reorder workspace buttons by selecting the down arrow and choosing **Navigation Pane Options**. Select an item to **Move Up** or **Move Down**. Select **Reset** to restore the default button order.

:::image type="content" source="media/navigation-pane-options.png" alt-text="Navigation Pane Options window to reorder workspaces.":::

Minimize a workspace button by selecting **Show Fewer Buttons**. The last workspace in the list is minimized first. Select a minimized button and choose **Show More Buttons** to restore the button to its original size.

:::image type="content" source="media/workspace-buttons.png" alt-text="Minimized workspaces in the Configuration Manager console.":::

### Nodes

Workspaces are a collection of **nodes**. One example of a node is the **Software Update Groups** node in the **Software Library** workspace.

Once you are in the node, you can select the arrow to minimize the navigation pane.

:::image type="content" source="media/software-update-groups-node.png" alt-text="Example node and highlight minimize arrow.":::

Use the **navigation bar** to move around the console when you minimize the navigation pane.

:::image type="content" source="media/minimized-navigation-pane.png" alt-text="Configuration Manager minimized navigation pane.":::

In the console, nodes are sometimes organized into folders. When you select the folder, it usually displays a **navigation index** or a **dashboard**.

:::image type="content" source="media/software-updates-navigation-index.png" alt-text="Configuration Manager software updates navigation index.":::

> [!NOTE]
> You can use PowerShell to manage console folders with the following cmdlets:
>
> - [Get-CMFolder](/powershell/module/configurationmanager/get-cmfolder)
> - [New-CMFolder](/powershell/module/configurationmanager/new-cmfolder)
> - [Remove-CMFolder](/powershell/module/configurationmanager/remove-cmfolder)
> - [Set-CMFolder](/powershell/module/configurationmanager/set-cmfolder)

### Ribbon

The ribbon is at the top of the Configuration Manager console. The ribbon can have more than one tab and can be minimized using the arrow on the right. The buttons on the ribbon change based on the node. Most of the buttons in the ribbon are also available on context menus.

:::image type="content" source="media/ribbon.png" alt-text="Example ribbon, highlighting multiple tabs and minimize arrow.":::

### Details pane

You can get additional information about items by reviewing the details pane. The details pane can have one or more tabs. The tabs vary depending on the node.

:::image type="content" source="media/details-pane.png" alt-text="Configuration Manager example details pane.":::

### Columns

You can add, remove, reorder, and resize columns. These actions allow you to display the data you prefer. Available columns vary depending on the node. To add or remove a column from your view, right-click on an existing column heading and select an item. Reorder columns by dragging the column heading where you would like it to be.

:::image type="content" source="media/add-columns.png" alt-text="Configuration Managers add column.":::

At the bottom of the column context menu, you can sort or group by a column. Additionally, you can sort by a column by selecting its header.

:::image type="content" source="media/column-group-by.png" alt-text="Configuration Manager group by column.":::

## <a name="bkmk_sedo"></a> Reclaim lock for editing objects

<!--4786915-->

If the Configuration Manager console stops responding, you can be locked out of making further changes until the lock expires after 30 minutes. This lock is part of the Configuration Manager SEDO (Serialized Editing of Distributed Objects) system. For more information, see [Configuration Manager SEDO](../../../develop/core/understand/sedo.md).

You can clear your lock on any object in the Configuration Manager console. This action only applies to your user account that has the lock, and on the same device from which the site granted the lock. When you attempt to access a locked object, you can now **Discard Changes**, and continue editing the object. These changes would be lost anyway when the lock expired.

## <a name="bkmk_viewconnected"></a> View recently connected consoles

<!--3699367-->
You can view the most recent connections for the Configuration Manager console. The view includes active connections and those connections that recently connected. You'll always see your current console connection in the list and you only see connections from the Configuration Manager console. You won't see PowerShell or other SDK-based connections to the SMS Provider. The site removes instances from the list that are older than 30 days.

### <a name="bkmk_connections-prereq"></a> Prerequisites to view connected consoles

- Your account needs the **Read** permission on the **SMS_Site** object.

- Configure the administration service REST API. For more information, see [What is the administration service?](../../../develop/adminservice/overview.md).

### View connected consoles

1. In the Configuration Manager console, go to the **Administration** workspace.

1. Expand **Security** and select the **Console Connections** node.

1. View the recent connections, with the following properties:

    - User name
    - Machine name
    - Connected site code
    - Console version
    - Last connected time: When the user last *opened* the console
    - An open console in the foreground sends a heartbeat every 10 minutes, which shows in the **Last Console Heartbeat** column. <!--4923997-->

:::image type="content" source="media/console-connections.png" alt-text="View Configuration Manager console connections.":::

## <a name="bkmk_message"></a> Start Microsoft Teams Chat from Console Connections
<!--4923997-->

You can message other Configuration Manager administrators from the **Console Connections** node using Microsoft Teams. When you choose to **Start Microsoft Teams Chat** with an administrator, Microsoft Teams is launched and a chat is opened with the user.

### Prerequisites

- For starting a chat with an administrator, the account you want to chat with needs to have been discovered with [Microsoft Entra ID or AD User Discovery](../deploy/configure/about-discovery-methods.md#bkmk_aboutUser).
- Microsoft Teams installed on the device from which you run the console.
note
- All [prerequisites to view connected consoles](#bkmk_connections-prereq)

### Start Microsoft Teams Chat

1. Go to **Administration** > **Security** > **Console Connections**.
1. Right-click on a user's console connection and select **Start Microsoft Teams Chat**.
    - If the User Principal Name isn't found for the selected administrator, **Start Microsoft Teams Chat** is grayed out.
    - An error message, including a download link, appears if Microsoft Teams isn't installed on the device from which you run the console.
    - If Microsoft Teams is installed on the device from which you run the console, it will open a chat with the user.

### Known issues

The error message notifying you that Microsoft Teams isn't installed won't be displayed if the following Registry key doesn't exist:

Computer\HKEY_CURRENT_USER\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall

To work around the issue, manually create the Registry key.

## <a name="bkmk_doc-dashboard"></a> In-console documentation dashboard

<!--3556019 FKA 1357546-->
The **Documentation** node in the **Community** workspace includes information about Configuration Manager documentation and support articles. It includes the following sections:

- **Recommended**: a manually curated list of important articles.
- **Troubleshooting articles**: guided walkthroughs to assist with troubleshooting Configuration Manager components and features.
- **New and updated support articles**: articles that are recently new or updated.

### Troubleshooting connection errors

The **Documentation** node has no explicit proxy configuration. It uses any OS-defined proxy in the **Internet Options** control panel applet. To retry after a connection error, refresh the **Documentation** node.

## <a name="bkmk_dark"></a> Dark theme for the console
<!--9070525-->
*(Introduced in version 2203)*

Starting in version 2203, the Configuration Manager console offers a dark theme. To use the theme, select the arrow from the top left of the ribbon, then choose **Switch console theme**. Select **Switch console theme** again to return to the light theme. As of version 2303, the main screen of the console and delete secondary site wizards adhere to the dark theme.  

:::image type="content" source="./media/9070525-console-dark-theme.png" alt-text="Screenshot of the Configuration Manager using the dark theme for the console. The 'Switch console theme' option is displayed in the upper right corner of the image.":::

### Known issue

- Console restart is required on doing the theme switch, as the node navigation pane might not properly render when you move to a new workspace.
- Currently, there are locations in the console that may not display the dark theme correctly. We are continuously working to improve the dark theme. 


## Connect via Windows PowerShell

The Configuration Manager console includes a PowerShell module with over a thousand cmdlets to interact programmatically from the command line. Select the arrow at the top of the [ribbon](#ribbon), and choose **Connect via Windows PowerShell**.

For more information, see [Get started with Configuration Manager cmdlets](/powershell/sccm/overview).

## Command-line options

The Configuration Manager console has the following command-line options:

|Option|Description|  
|------------|-----------------|  
|`/sms:debugview=1`|A DebugView is included in all ResultViews that specify a view. DebugView shows raw properties (names and values).|  
|`/sms:NamespaceView=1`|Shows namespace view in the console.|  
|`/sms:ResetSettings`|The console ignores user-persisted connection and view states. The window size isn't reset.|  
|`/sms:IgnoreExtensions`|Disables any Configuration Manager extensions.|  
|`/sms:NoRestore`|The console ignores previous persisted node navigation.|  
|`/server=[ServerName]`|Connect to a CAS or Primary site server by specifying the fully qualified domain name (FQDN) or server name for that site.|  

## Next steps

- [Console notifications](admin-console-notifications.md)
- [Console tips](admin-console-tips.md)
- [Accessibility features](../../understand/accessibility-features.md)
- [Task sequence editor](../../../osd/understand/task-sequence-editor.md#bkmk_conditions)
