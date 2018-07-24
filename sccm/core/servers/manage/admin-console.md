---
title: Configuration Manager Console
titleSuffix: Configuration Manager
description: Learn about navigating through the Configuration Manager console.
ms.date: 07/13/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 463ce307-59dd-4abd-87b8-42ca9db178d7
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# System Center Configuration Manager console

*Applies to: System Center Configuration Manager (Current Branch)*

Administrators use the System Center Configuration Manager console to manage the Configuration Manager environment. This article covers the fundamentals of navigating the console. Improvements to the console are listed by version at the bottom of this article. 

## Connect the console to a site server
The console connects to your central administration site server or to your primary site servers. However, you can't connect a Configuration Manager console to a secondary site. If needed, [install the Configuration Manager console](../deploy/install/install-consoles.md). During installation, you specified the fully qualified domain name (FQDN) of the site server to which the Configuration Manager console connects. To connect to a different site server, use the following instructions: 

1. Click on the arrow at the top of the ribbon and select **Connect to a New Site**.
    ![Connect the console to a new site](media/connect-to-a-new-site.png)
2. Type in the FQDN of the site server. If you've previously connected to site server, select the server from the drop-down.  
    ![Type in FQDN of the site server](media/site-server-fqdn.png)
3. Click **Connect**. 

## Navigate the console
Some options under the console may not be visible depending on your assigned security role. For more information about roles, see [Fundamentals of role-based administration](../../understand/fundamentals-of-role-based-administration.md). 

### Workspaces
The Configuration Manager console has four **workspaces**: 
   - **Assets and Compliance**
   - **Software Library**
   - **Monitoring**
   - **Administration**

 ![Configuration Manager workspaces](media/configuration-manager-workspaces.png)

Reorder workspace buttons by clicking the down arrow and selecting **Navigation Pane Options**. Select an item to **Move Up** or **Move Down**. Click **Reset** to restore the default button order. 

 ![Reorder Configuration Manager workspaces](media/navigation-pane-options.png)

You can minimize a workspace button by selecting **Show Fewer Buttons**. The last workspace in the workspace list is minimized first. Clicking on a minimized button and selecting **Show More Buttons** restores the button to its original size.  

![Configuration Manager workspaces](media/workspace-buttons.png)


### Nodes
Workspaces are a collection of **nodes**. One example of a node is the **Software Update Groups** node. Once you are in the node, you can click on the arrow to minimize the navigation pane. 

![Configuration Manager workspaces](media/software-update-groups-node.png)

You can use the **navigation bar** to move around the console when your navigation pane is minimized. 

![Configuration Manager minimized navigation pane](media/minimized-navigation-pane.png)

In the console, nodes are sometimes organized into folders. Clicking directly on the folder usually takes you to a **navigation index** or a **dashboard**.

![Configuration Manager software updates navigation index](media/software-updates-navigation-index.png)

### Ribbon 
The ribbon is at the top of the Configuration Manager console. The ribbon can have more than one tab and can be minimized using the arrow on the right. The buttons on the ribbon change based on the node. Most of the buttons in the ribbon are also available on right click menus. 
 
![Configuration Manager software updates navigation index](media/ribbon.png)

### Details pane
You can get additional information about items by reviewing the details pane. The details pane can have one or more tabs. The tabs will vary depending on the node. 
![Configuration Manager details pane](media/details-pane.png)

### Columns 
You can add, remove, reorder, and resize columns. These actions allow you to display the data you prefer. Available columns will vary depending on the node. Right-click on an existing column heading then click an item to add or remove from your view. Reorder columns by dragging the column heading where you would like it to be. 
![Configuration Managers add column](media/add-columns.png)

At the bottom of the column right click menu, you can sort or group by a column. Additionally, you can sort by a column by clicking on its header. 

![Configuration Manager group by column](media/column-group-by.png)

## Console improvements in version 1810
In Configuration Manager version 1810, the following console improvements are added:

- **Primary user(s)** is available as a column in the device node. <!--1357280-->
- **Currently logged on user** is available as a column in the device node.<!--1358202-->
- Copy information from the **Asset Details** pane for the following monitoring views: <!--1357856-->
    - Content Distribution Status
    - Deployment Status 

    ![Configuration Manager copy asset details](media/1810-deployment-status.PNG)

 - Submit feedback from the console. You can save a copy to submit later if you don't have internet access. 
   
    - **Send a smile**: Send feedback on what you liked.
    - **Send a frown**: Send feedback on what you didn't like. 
    - **Send a suggestion**: Takes you to UserVoice to share your idea. 
 
       ![Send feedback for Configuration Manager](media/1810-send-a-smile.PNG)
![Configuration Manager feedback form](media/1810-feedback-form.PNG)

## Next step
> [!div class="nextstepaction"]
> [Accessibility Features](/sccm/core/understand/accessibility-features.md)

