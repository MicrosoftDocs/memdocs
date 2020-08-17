---
title: Configuration Manager console changes and tips
titleSuffix: Configuration Manager
description: Learn about changes to the Configuration Manager console and tips for using it.
ms.date: 08/11/2020
ms.prod: configuration-manager
ms.technology: configmgr-core
ms.topic: reference
ms.assetid: 2162d67d-31a9-45b2-bb9e-835f3ac6e6fe
author: mestew
ms.author: mstewart
manager: dougeby
---

# Configuration Manager console changes and tips

*Applies to: Configuration Manager (current branch)*

Use the information below to find out about changes to the Configuration Manager console and tips for using the console:

## General tips

### <a name="bkmk_search"></a> Improvements to console search
<!--4640570-->
*(Introduced in version 1910)*

- You can use the **All Subfolders** search option from the **Driver Packages** and **Queries** nodes.<!--2841181,5424892--> Starting in version 2002, also use this option from the **Configuration Items** and **Configuration Baselines** nodes.<!--5891241-->

- When a search returns more than 1,000 results, select the **OK** button on the notice bar to view more results.<!--4640570-->

    ![Screenshot of notice bar for too many search results](./media/4640570-search-too-many-results.png)

    > [!TIP]
    > The default limit on search results is 1,000. You can change this default value. In the Configuration Manager console, go to the **Search** tab of the ribbon. In the **Options** group, select **Search Settings**. Change the **Search Results** value. A larger number of search results might take longer to display.
    >
    > By default, the upper maximum limit is 100,000. To change this limit, set the DWORD value **QueryResultCountMaximum** in the following registry key:
    >
    > `HKEY_CURRENT_USER\Software\Microsoft\ConfigMgr10\AdminUI`
    >
    > The in-console setting corresponds to the **QueryResultCountLimit** value in the same key. An administrator can configure these values in the HKLM hive for all users of the device. The HKCU value overrides the HKLM setting.

### Role based administration for folders
<!--3600867-->
*(Introduced in version 1906)*

You can set security scopes on folders. If you have access to an object in the folder but don't have access to the folder, you'll be unable to see the object. Similarly, if you have access to a folder but not an object within it, you won't see that object. Right-click a folder, choose **Set Security Scopes**, then choose the security scopes you want to apply.

### Views sort by integer values

*(Introduced in version 1902)*

We've made improvements to how various views sort data. For example, in the **Deployments** node of the **Monitoring** workspace, the following columns now sort as numbers instead of string values:  

- Number Errors​
- Number In Progress​
- Number Other​
- Number Success​
- Number Unknown​  

### Move the warning for a large number of results

*(Introduced in version 1902)*

When you select a node in the console that returns more than 1,000 results, Configuration Manager displays the following warning:

> Configuration Manager returned a large number of results. You can narrow your results by using search. Or, click here to view a maximum of 100000 results.

There's now additional blank space in between this warning and the search field. This move helps to prevent inadvertently selecting the warning to display more results.

### Send feedback

*(Introduced in version 1806)*
<!--1357542-->

Submit product feedback from the console.  

- **Send a smile**: Send feedback on what you liked  

- **Send a frown**: Send feedback on what you didn't like  

- **Send a suggestion**: Takes you to UserVoice to share your idea  

For more information, see [Product Feedback](../../understand/find-help.md#BKMK_1806Feedback).


## Assets and Compliance workspace

### Real-time actions from device lists
<!--4616810-->
*(Introduced in version 1906)*

There are various ways to display a list of devices under the **Devices** node in the **Assets and Compliance** workspace.

- In the **Assets and Compliance** workspace, select the **Device Collections** node. Select a device collection, and choose the action to **Show members**. This action opens a subnode of the **Devices** node with a device list for that collection.  

  - When you select the collection subnode, you can now start **CMPivot** from the Collection group of the ribbon.  

- In the **Monitoring** workspace, select the **Deployments** node. Select a deployment, and choose the **View Status** action in the ribbon. In the deployment status pane, double-click the total assets to drill-through to a device list.  

  - When you select a device in this list, you can now start **CMPivot** and **Run Scripts** from the Device group of the ribbon.  


### Collections tab in devices node
<!--4616810-->
*(Introduced in version 1906)*

In the **Assets and Compliance** workspace, go to the **Devices** node, and select a device. In the details pane, switch to the new **Collections** tab. This tab lists the collections that include this device. 

> [!Note]  
> - This tab currently isn't available from a devices subnode under the **Device Collections** node. For example, when you select the option to **Show Members** on a collection.
> - This tab may not populate as expected for some users. To see the complete list of collections a device belongs to, you must have the **Full Administrator** security role. This is a known issue. <!--5107309--> <!--5107309-->


### Add SMBIOS GUID column to device and device collection nodes

*(Introduced in version 1906)*

<!--4526580-->
In both the **Devices** and **Device Collections** nodes, you can now add a new column for **SMBIOS GUID**. This value is the same as the **BIOS GUID** property of the System Resource class. It's a unique identifier for the device hardware.

### Search device views using MAC address

<!--3600878-->
*(Introduced in version 1902)*

You can search for a MAC address in a device view of the Configuration Manager console. This property is useful for OS deployment administrators while troubleshooting PXE-based deployments. When you view a list of devices, add the **MAC Address** column to the view. Use the search field to add the **MAC Address** search criteria.

### View users for a device

Starting in version 1806, the following columns are available in the **Devices** node:  

- **Primary user(s)** <!--1357280-->  

- **Currently logged on user** <!--1358202-->  

    > [!NOTE]  
    > Viewing the currently logged on user requires [user discovery](../deploy/configure/configure-discovery-methods.md#bkmk_config-adud) and [user device affinity](../../../apps/deploy-use/link-users-and-devices-with-user-device-affinity.md).  

For more information on how to show a non-default column, see [How to use the admin console](admin-console.md#columns).

### Improvement to device search performance

<!-- 3614690 -->
Starting in version 1806, when searching in a device collection, it doesn't search the keyword against all object properties. When you're not specific about what to search, it searches across the following four properties:

- Name
- Primary user(s)
- Currently logged on user
- Last logon user name

This behavior significantly improves the time it takes to search by name, especially in a large environment. Custom searches by specific criteria are unaffected by this change.


## Software Library workspace

### Order by program name in task sequence
<!--4616810-->
*(Introduced in version 1906)*

In the **Software Library** workspace, expand **Operating Systems**, and select the **Task Sequences** node. Edit a task sequence, and select or add the [Install Package](../../../osd/understand/task-sequence-steps.md#BKMK_InstallPackage) step. If a package has more than one program, the drop-down list now sorts the programs alphabetically.

### Task sequences tab in applications node
<!--4616810-->
*(Introduced in version 1906)*

In the **Software Library** workspace, expand **Application Management**, go to the **Applications** node, and select an application. In the details pane, switch to the new **Task sequences** tab. This tab lists the task sequences that reference this application.

### Drill through required updates
<!--4224414-->
*(Introduced in version 1906)*

1. Go to one of the following places in the Configuration Manager console:

   - **Software Library** > **Software Updates** > **All Software Updates**
   - **Software Library** > **Windows 10 Servicing** > **All Windows 10 Updates**
   - **Software Library** > **Office 365 Client Management** > **Office 365 Updates**

1. Select any update that is required by at least one device.
1. Look at the **Summary** tab and find the pie chart under  **Statistics**.
1. Select the **View Required** hyperlink next to the pie chart to drill down into the device list.
1. This action takes you to a temporary node under **Devices** where you can see the devices requiring the update. You can also take actions for the node such as creating a new collection from the list.

> [!NOTE]
> Starting on April 21, 2020, Office 365 ProPlus is being renamed to **Microsoft 365 Apps for enterprise**. For more information, see [Name change for Office 365 ProPlus](https://docs.microsoft.com/deployoffice/name-change). You may still see references to the old name in the Configuration Manager console and supporting documentation while the console is being updated.

### Maximize the browse registry window

<!--3594151 includes all MMS 1902 console changes-->
*(Introduced in version 1902)*

1. In the **Software Library** workspace, expand **Application Management**, and select the **Applications** node.
1. Select an application that has a deployment type with a detection method. For example, a Windows Installer detection method.
1. In the details pane, switch to the **Deployment Types** tab.
1. Open the properties of a deployment type, and switch to the **Detection Method** tab. Select **Add Clause**.
1. Change the **Setting Type** to **Registry** and select **Browse** to open the **Browse Registry** window. You can now maximize this window.  

### Edit a task sequence by default

*(Introduced in version 1902)*

In the **Software Library** workspace, expand **Operating Systems**, and select the **Task Sequences** node. **Edit** is now the default action when opening a task sequence. Previously the default action was **Properties**.  

### Go to the collection from an application deployment

*(Introduced in version 1902)*

1. In the **Software Library** workspace, expand **Application Management**, and select the **Applications** node.
1. Select an application. In the details pane, switch to the **Deployments** tab.
1. Select a deployment, and then choose the new **Collection** option in the ribbon on the Deployment tab. This action switches the view to the collection that's the target of the deployment.
   - This action is also available from the right-click context menu on the deployment in this view.


## Monitoring workspace

### Correct names for client operations
<!--4616810-->
*(Introduced in version 1906)*

In the **Monitoring** workspace, select **Client Operations**. The operation to **Switch to next Software Update Point** is now properly named.

### Show collection name for scripts
<!--4616810-->
*(Introduced in version 1906)*

In the **Monitoring** workspace, select the **Script Status** node. It now lists the **Collection Name** in addition to the ID.

### Remove content from monitoring status

*(Introduced in version 1902)*

1. In the **Monitoring** workspace, expand **Distribution Status**, and select **Content Status**.
1. Select an item in the list, and choose the **View Status** option in the ribbon.
1. In the Asset Details pane, right-click a distribution point, and select the new option **Remove**. This action removes this content from the selected distribution point.

### Copy details in monitoring views

*(Introduced in version 1806)*
<!--1357856-->
Copy information from the **Asset Details** pane for the following monitoring nodes:  

- **Content Distribution Status**  

- **Deployment Status**  

![Deployment Status view, copy asset details](media/1810-deployment-status.PNG)

## Administration workspace

<!--4223683-->
Starting in version 1906, you can enable some nodes under the **Security** node to use the administration service. This change allows the console to communicate with the SMS Provider over HTTPS instead of via WMI. For more information, see [Set up the administration service](../../../develop/adminservice/set-up.md#bkmk_console).

## Next steps

- [Use the console](admin-console.md)
- [Console notifications](admin-console-notifications.md)
- [Accessibility features](../../understand/accessibility-features.md)