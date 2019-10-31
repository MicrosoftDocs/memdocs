---
title: Office 365 Client Management dashboard
titleSuffix: "Configuration Manager"
description: "Review Office 365 client information from the Office 365 Client Management dashboard"
author: mestew
ms.author: mstewart
manager: dougeby
ms.date: 11/01/2019
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-sum
ms.assetid: 69f234a2-b04b-445a-b81f-6b4acfc00eaf
ms.collection: M365-identity-device-management
---

# Office 365 Client Management dashboard

Beginning in Configuration Manager version 1802, you can review Office 365 client information from the Office 365 Client Management dashboard. The Office 365 client management dashboard displays a list of relevant devices when graph sections are selected. <!--1357281 -->

## Prerequisites

### Enable hardware inventory

The data that is displayed in the Office 365 Client Management dashboard comes from hardware inventory. Enable hardware inventory and select the **Office 365 ProPlus Configurations** hardware inventory class for data to display in the dashboard.
 
1. Enable hardware inventory, if it isn't yet enabled. For details, see [Configure hardware inventory](/sccm/core/clients/manage/inventory/configure-hardware-inventory).
2. In the Configuration Manager console, navigate to **Administration** > **Client Settings** > **Default Client Settings**.  
3. On the **Home** tab, in the **Properties** group, click **Properties**.  
4. In the **Default Client Settings** dialog box, click **Hardware Inventory**.  
5. In the **Device Settings** list, click **Set Classes**.  
6. In the **Hardware Inventory Classes** dialog box, select **Office 365 ProPlus Configurations**.  
7. Click **OK** to save your changes and close the **Hardware Inventory Classes** dialog box.

The Office 365 Client Management dashboard starts displaying data as hardware inventory is reported.

### Internet connectivity for clients

*(Introduced in version 1906 as a prerequisite)*

Starting in version 1906, devices that have Office installed need internet connectivity to populate add-in information for the [Office 365 ProPlus upgrade readiness dashboard](bkmk_readiness-dash). Devices download an add-in readiness file from the [Office Content Delivery Network](https://docs.microsoft.com/office365/enterprise/content-delivery-networks#the-office-365-cdn). This file contains the full list of add-ins that are known to Microsoft and details of their expected performance on Office 365 ProPlus. Each device uses the information from the file to determine add-in compatibility. If a device can't download the file, it will have an add-in readiness status of **Needs Review**.

## Viewing the Office 365 Client Management dashboard

To view the Office 365 Client Management dashboard in the Configuration Manager console, go to **Software Library** > **Overview** > **Office 365 Client Management**. At the top of the dashboard, use the **Collection** drop-down setting to filter the dashboard data by members of a specific collection. Beginning in Configuration Manager version 1802, the Office 365 client management dashboard displays a list of relevant devices when graph sections are selected.

The Office 365 Client Management dashboard provides charts for the following information:

- Number of Office 365 clients
- Office 365 client versions
- Office 365 client languages
- Office 365 client channels
  For more information, see [Overview of update channels for Office 365 ProPlus](/DeployOffice/overview-of-update-channels-for-office-365-proplus).


## <a name="bkmk_o365_readiness"></a> Integration for Office 365 ProPlus readiness
<!--3735402-->
Starting in Configuration Manager version 1902, you can use the dashboard to identify devices with high confidence that are ready to upgrade to Office 365 ProPlus. This integration provides insights into potential compatibility issues with Office add-ins and macros in your environment. Then use Configuration Manager to deploy Office to ready devices.

The Office 365 client management dashboard includes a new tile, **Office 365 ProPlus Upgrade Readiness**. This tile is a bar chart of devices in the following states:
- Not assessed
- Ready to upgrade
- Needs review

Select a state to drill-through to a device list. This readiness report shows more detail about devices. It includes columns for the compatibility state of both Office add-ins and macros.

### Prerequisites for Office 365 ProPlus readiness integration

- Enable hardware inventory in client settings. For more information, see the [Prerequisites](#prerequisites) section.  

- The device needs connectivity to the Office content delivery network (CDN) to download an add-in readiness file. For more information, see [Content delivery networks](https://docs.microsoft.com/office365/enterprise/content-delivery-networks). If the device can't download this file, the add-ins state is *Needs review*.  

    > [!Note]  
    > No data is sent to Microsoft for this feature.  

### <a name="bkmk_ort"></a> Detailed macro readiness

By default, the scanning agent looks at the most recently used (MRU) files list on each device. It counts the files in this list that support macros. These files include the following types:
- Macro-enabled Office file formats, such as Excel macro-enabled workbooks (.xlsm) or Word macro-enabled document (.docm)  
- Older Office formats that don't indicate whether there's macro content. For example, an Excel 97-2003 workbook (.xls).

If you need a more detailed evaluation, deploy the **Office Readiness Toolkit**. This tool analyzes the code within a macro file. It checks if there are any potential compatibility concerns. For example, the file uses a function that changed in a more recent version of Office. After you run the Office Readiness Toolkit, Configuration Manager can use its results. This additional data enhances the device readiness calculation. For more information, see [Use the Readiness Toolkit to assess application compatibility for Office 365 ProPlus](https://aka.ms/readinesstoolkit).

## <a name="bkmk_readiness-dash"></a> Office 365 ProPlus upgrade readiness dashboard

*(Introduced in version 1906)*

<!--4021125-->
To help you determine which devices are ready to upgrade to Office 365 ProPlus, there's a readiness dashboard starting in version 1906. It includes the **Office 365 ProPlus upgrade readiness** tile that released in Configuration Manager current branch version 1902. The following new tiles on this dashboard help you evaluate Office add-in and macro readiness:

- Deployment
- Device readiness
- Add-in readiness
- Add-in support statements
- Top add-ins by count of version
- Number of devices that have macros
- Macro readiness
- Macro advisories

### Using the Office 365 ProPlus upgrade readiness dashboard

After verifying you have the [prerequisites](#prerequisites), use the following instructions to use the dashboard:
 
1. In the Configuration Manager console, go to the **Software Library** workspace, expand **Office 365 Client Management**.
1. Select the **Office 365 ProPlus Upgrade Readiness** node.
1. Change the **Collection** and **Target Office Architecture** to change the information relayed in the dashboard.

![Office 365 ProPlus upgrade readiness dashboard](./media/4021125-office-365-upgrade-readiness-dashboard.png)

![Office 365 ProPlus upgrade readiness dashboard](./media/4021125-office-365-to-add-ins.png)

![Office 365 ProPlus upgrade readiness dashboard](./media/4021125-office-365-macro-advisories.png)

### Device Readiness information

Once the add-in and macro inventory on each device is evaluated, the devices are then grouped according to the information. Devices whose status are listed as **Ready to upgrade** aren't likely to have any compatibility issues.

Selecting the **Ready to upgrade** category on the graph shows more details about the devices in the limiting collection. You can review the device list, make selections according to your business requirements, and create a new device collection from your selection. Use your new collection to deploy Office 365 ProPlus with Configuration Manager.

Devices that might be at risk for compatibility issues are marked as **Needs review**. These devices may need action to be taken before upgrading them to Office 365 ProPlus. For example, you might update critical add-ins to a more recent version.

### Add-in information

 On each device, an inventory of all installed add-ins is collected. The inventory is then compared with the information Microsoft has about the add-in performance on Office 365 ProPlus. If an add-in is found which is likely to cause issues after upgrading, then all devices with the add-in are flagged for review.

### Macro information

Configuration Manager looks at the most recently used files on each device. It counts the files in this list that support macros, including the following types:

- Macro-enabled Office file formats.
- Older Office formats, which don't indicate if there's macro content.

If you need a more detailed evaluation for macros, use the **Office Readiness Toolkit** since it analyzes the code within the macro file. The results can be picked up by Configuration Manager's hardware inventory agent when you select the option for **Most recently used Office documents and installed add-ins on this computer**. The additional data can enhance the device readiness calculation. For more information, see [Use the Readiness Toolkit to assess application compatibility for Office 365 ProPlus](https://aka.ms/readinesstoolkit).


## Next steps

[Manage Office 365 ProPlus with Configuration Manager](/sccm/sum/deploy-use/manage-office-365-proplus-updates)
