---
title: "Capabilities in Technical Preview 1608"
titleSuffix: "Configuration Manager"
description: "Learn about features available in the Technical Preview for System Center Configuration Manager, version 1608."
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 63e1df5e-637c-4b07-b7ec-95340f43a805
author: aczechowski
manager: dougeby
ms.author: aaroncz
ROBOTS: NOINDEX
---
# Capabilities in Technical Preview 1608 for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*

This article introduces the features that are available in the Technical Preview for System Center Configuration Manager, version 1608. You can install this version to update and add new capabilities to your Configuration Manager technical preview site.      Before installing this version of the technical preview, review the introductory topic, [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md), to become familiar with general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback about the features in a technical preview.    


**The following are new features you can try out with this version.**  




##  Improvements to the Prepare ConfigMgr Client for Capture task sequence step  
The Prepare ConfigMgr Client step will now completely remove the Configuration Manager client, instead of only removing key information. When the task sequence deploys the captured operating system image it will install a new Configuration Manager client each time.  


## Improvements to Software Center
* The Software Center **Applications**, **Updates**, and **Operating Systems** tabs now show what software was recently added. Numbers in the navigation pane show how many new pieces of software are in each tab.
* Users can now request approval for applications, and then view the request history in the **Application Details** view in Software Center. The **Request** button in **Application Details** no longer redirects to the web-based Application Catalog.

## Improvements to Asset Intelligence
We have added a field to the properties for inventoried software that lets you set a parent and child relationship with other software. In the Inventoried Software list, you can then view the parent of any software and also hide all child software.

### Configure a parent to child relationship
  1. To set parent software, in the Inventoried Software node, right-click on a software item in the **Inventoried Software** list, and choose **Properties**.
  2. In the dialog box that opens, select the software that you want to set as the parent software for your initial selection.

### Filter the software display
After you have defined parent to child relationships, you can filter your view to only show software that is a parent or that has no defined relationship. This hides all software that is set as a child of another inventoried software. To do so:
   1.	For the Search bar, choose to **Add Criteria**
   2. Select **Parent Software** and then change the criteria value to **is empty**, and then click **Search**.

The display now shows only the parent software items, or software that has no defined relationships. Software that is only a child of another title does not display.

## Remote control keyboard translation
In the past, Configuration Manager transmitted the key position from the viewer’s location to the sharer’s location. This was problematic for keyboard configurations that differed from viewer to sharer. For example, a viewer with an English keyboard would type an “A”, but the sharer’s French keyboard would provide a “Q”. We are changing the default behavior so that the character itself is transmitted from the viewer’s keyboard to the sharer, and what the viewer intends to type arrives at the sharer.

This behavior can be turned off by the viewer if they prefer to type according to the sharer’s keyboard arrangement. To change the behavior, in **Configuration Manager Remote Control**, choose **Action**,and choose **Enable keyboard translation** to transmit key position.

> [!NOTE]
>
> Special keys, such as ~!#@$%, will not be translated correctly.
