---
title: "Accessibility"
titleSuffix: "Configuration Manager"
description: "Learn about the features that make System Center Configuration Manager accessible for people with disabilities."
ms.custom: na
ms.date: 7/31/2017
ms.reviewer: na
ms.suite: na
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1cb96666-98bf-49a9-85ca-dbb53f0655e9
caps.latest.revision: 6
author: aczechowski
ms.author: aaroncz
manager: angrobe
---
# Accessibility features in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*


System Center Configuration Manager includes features to help make it accessible for people with disabilities.


## <a name="bkmk_aconsole"></a> Accessibility features for the Configuration Manager console  

**Shortcuts and improvements with version 1706 and later**

|Keyboard shortcut|  Purpose|
|--------|--------|  
|Ctrl + M|Set the focus on the main (central) pane.|
|Ctrl + T|Set the focus to the top node in the navigation pane. If the focus was already in that pane, the focus is set to the last node you visited.|
|Ctrl + I|Set the focus to the breadcrumb bar, below the ribbon.|
|Ctrl + L|Set the focus to the **Search** field, when available.|
|Ctrl + D|Set the focus to the details pane, when available.|
|Alt     |Change the focus in and out of the ribbon.|


- Improved navigation in the navigation pane when you type the letters of a node name.
- Keyboard navigation through the main view and the ribbon is now circular.
- Keyboard navigation in the details pane is now circular. To return to the previous object or pane, use Ctrl + D, then Shift + TAB.
- After refreshing a Workspace view, the focus is set to the main pane of that workspace.
- Fixed an issue to enable screen readers to announce the names of list items.
- Added accessible names for multiple controls on the page that enables screen readers to announce important information.


**The following shortcuts are available for all versions**

- To access a workspace, use the following keyboard shortcuts:  

|Keyboard shortcut| Workspace|
|--------|--------|  
|Ctrl + 1| Assets and Compliance|
|Ctrl + 2|  Software Library|
|Ctrl + 3|  Monitoring|
|Ctrl + 4|  Administration|


-   To access a workspace menu, select the Tab key until the Expand/Collapse icon is in focus. Then, select the Down arrow key to access the workspace menu.  

-   To navigate through a workspace menu, use the arrow keys.  

-   To access different areas in the workspace, use the Tab key and Shift+Tab keys. To navigate within an area of the workspace, such as the ribbon, use the arrow keys.  

-   To access the address bar when your focus is in the tree node, use Shift+Tab three times.  

-   On a wizard or property page, you can move between the boxes with keyboard shortcuts. Select the Alt key plus the underlined character (Alt+_) to select a specific box.     

-  To navigate to the different nodes of a workspace, enter the first letter of the name of a node. Each key press moves the cursor to the next node that begins with that letter. When you're using a screen reader, the reader reads out the name of that node.

> [!NOTE]  
>  The information in this section might apply only to users who license Microsoft products in the United States. If you obtained this product outside of the United States, you can use the subsidiary information card that came with your software package or visit the [Microsoft Accessibility website](http://go.microsoft.com/fwlink/?LinkId=8431) for contact information for Microsoft support services. You can contact your subsidiary to find out whether the type of products and services that are described in this section are available in your area. Information about accessibility is available in other languages, including Japanese and French.  

##  <a name="bkmk_ahelp"></a> Accessibility features for Configuration Manager Help  
 Configuration Manager Help includes features that make it accessible to a wider range of users, including users who have limited dexterity, low vision, or other disabilities.  

|To do this|Use this keyboard shortcut|  
|----------------|--------------------------------|  
|Display the Help window.|F1|  
|Move the cursor between the Help topic pane and the navigation pane (the **Contents**, **Search**, and **Index** tabs).|F6|  
|Change between tabs (for example, **Contents**, **Search**, and **Index**) in the navigation pane.|Alt + underlined letter of the tab|  
|Select the next hidden text or hyperlink.|Tab|  
|Select the previous hidden text or hyperlink.|Shift+Tab|  
|Perform the action for the selected Show All, Hide All, hidden text, or hyperlink.|Enter|  
|Display the **Options** menu to access any Help toolbar command.|Alt+O|  
|Hide or show the pane that contains the **Contents**, **Search**, and **Index** tabs.|Alt+O, and then select T|  
|Display the previously viewed topic.|Alt+O, and then select B|  
|Display the next topic in a previously displayed sequence of topics.|Alt+O, and then select F|  
|Return to the specified home page.|Alt+O, and then select H|  
|Stop the Help window from opening a Help topic—for example, to stop a webpage from downloading.|Alt+O, and then select S|  
|Open the **Internet Options** dialog box for Windows Internet Explorer, where you can change accessibility settings.|Alt+O, and then select I|  
|Refresh the topic, such as a linked webpage.|Alt+O, and then select R|  
|Print all topics in a book or a selected topic only.|Alt+O, and then select P|  
|Close the Help window.|Alt+F4|  

#### To change the appearance of a Help topic  

1.  To prepare to customize the colors, font styles, and font sizes in Help, open the Help window.  

2.  Choose **Options**, and then choose **Internet Options**.  

3.  On the **General** tab, choose **Accessibility**. Choose **Ignore colors specified on Web pages**, **Ignore font styles specified on Web pages**, and **Ignore font sizes specified on Web pages**. You also can choose to use the settings that are specified in your own style sheet.  

#### To change the color of the background or text in Help  

1.  Open the Help window.  

2.  Choose **Options**, and then choose **Internet Options**.  

3.  On the **General** tab, choose **Accessibility**. Then, choose **Ignore colors specified on Web pages**. You also can choose to use the settings that are specified in your own style sheet.  

4.  To customize the colors that are used in Help, on the **General** tab, choose **Colors**. Uncheck the **Use Windows Colors** box, and then choose the font and background colors that you want to use.  

    > [!NOTE]  
    >  If you change the background color of the Help topics in the Help window, the change also affects the background color for webpages in Windows Internet Explorer.  

#### To change the font in Help  

1.  Open the Help window.  

2.  Choose **Options**, and then choose **Internet Options**.  

3.  On the **General** tab, choose **Accessibility**. To use the same settings as those that are used in your instance of Windows Internet Explorer, choose **Ignore font styles specified on Web pages** and **Ignore font sizes specified on Web pages**. You also can choose to use the settings that are specified in your own style sheet.  

4.  To customize the font style that is used in Help, on the **General** tab, choose **Fonts**, and then choose the font style that you want.  

    > [!NOTE]  
    >  If you change the font of the Help topics in the Help window, the change also affects the font for webpages in Windows Internet Explorer.  
