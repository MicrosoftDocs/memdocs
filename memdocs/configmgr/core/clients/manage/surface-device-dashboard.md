---
title: Surface Device Dashboard
titleSuffix: Configuration Manager
description: Review information about Surface devices using the dashboard.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 07/30/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 7397fc17-3ae8-4525-8386-aea8a9cffa06


---
# Surface device dashboard in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Beginning in version 1802, the Surface device dashboard gives you information about Surface devices found in your environment at a single glance. <!--1355788-->

## Open the Surface device dashboard

To open the Surface device dashboard, use the following steps: 

1. Open the Configuration Manager console. 
2. Click on the **Monitoring** node. 
3. To load the dashboard, click on **Surface Devices**.

**Surface device dashboard**
![Surface device dashboard](media/Surface-device-dashboard.PNG)



## Reviewing information in the Surface device dashboard

The Surface device dashboard shows three graphs for your environment. 

- **Percent of Surface devices** -Gives you the percentage of Surface devices throughout your environment.

    ![Percent of Surface devices graph](media/Percent-Surface-Devices.PNG)
- **Surface Models** -Shows the number of devices per Surface model. 
  - Hovering over a graph section will give you the percentage of Surface devices that are the model selected. 

       ![Surface models graph](media/Surface-Models-Hover.PNG)
  - Clicking on a graph section will take you to a device list for the model. 
      ![Surface model device list](media/Surface-Model-Device-List.PNG)

- **Top five firmware versions**- Displays a chart with the top five firmware models in your environment. 
  - Hovering over a graph section will give you the number of Surface devices that are the firmware version selected. Starting in Configuration Manager version 1806, clicking on a graph section displays a list of relevant devices. <!--1358654-->
     ![Surface model device list](media/Surface-Firmware-Hover.PNG)


## More information

For more information about Surface devices, see:
- The [Surface]( https://go.microsoft.com/fwlink/?linkid=861998) website.

For more information about deploying Surface firmware updates in Configuration Manager, see:
- [How to manage Surface driver updates in Configuration Manager]( https://support.microsoft.com/help/4098906).




