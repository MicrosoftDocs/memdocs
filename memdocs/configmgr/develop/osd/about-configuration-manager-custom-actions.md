---
title: Custom Actions
description: You can create custom actions that can be used with existing Configuration Manager actions.
titleSuffix: Configuration Manager
ms.date: 09/20/2016
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: conceptual
ms.assetid: 894bd31a-0a51-403b-84e9-1cc4958dfa7c
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---
# About Configuration Manager Custom Actions
You can create custom actions that can be used with existing Configuration Manager actions.  

 Custom actions are command-line actions that calls an application. The application can be a process, a script or other commands that you specify in a Managed Object Format (MOF) file description.  

 For more information, see [About Configuration Manager Custom Action Client Applications](../../develop/osd/about-configuration-manager-custom-action-client-applications.md).  

 To allow users to configure your custom action, you can create a custom action control that integrates into the Task Sequence Editor.  

 Creating a custom action control requires the following steps.  

## Creating the Custom Action Control  
 To create a custom action control, you use Visual Studio 2005 to create a Windows control that implements two classes.  

 The control that is displayed in the Task Sequence Editor is the first class, which derives from the **SMSOsdEditorPageControl** class. In this class, you define the user interface and the data transfer to and from the action. When a custom action is created, the control's PropertyManager makes the custom action's properties available for use. These are the properties that are defined in the custom action MOF file.  

 The second class implements the options control, and it derives from the **TaskSequenceOptionControl** class.  

 For more information about creating a custom control in Visual Studio, see [How to Create a Configuration Manager Custom Action Control](../../develop/osd/how-to-create-a-configuration-manager-custom-action-control.md).  

> [!NOTE]
>  The Configuration Manager SDK sample CustomTasksequenceAction shows how to create a custom task sequence action control and MOF.  

### Supporting Help  
 You cannot integrate your control's Help with the Configuration Manager console F1 key Help support. If a user presses F1 in your control, the control does nothing. However, you can implement Help in your control by using a mechanism of your choice to open the Help .chm file. For example, you can add a Help button that opens your Help .chm file.  

## Creating the Custom Action MOF File  
 Each Configuration Manager action is defined in the task sequence provider MOF file, _tasksequenceprovider.mof. A custom action extends this MOF file with a description for the custom action class. You should create the description of your custom action in a separate MOF file.  

 For more information, see [About the Configuration Manager Custom Action MOF File](../../develop/osd/about-configuration-manager-custom-action-mof-files.md) and [How to Create a MOF File for a Configuration Manager Custom Action](../../develop/osd/how-to-create-a-mof-file-for-a-configuration-manager-custom-action.md).  

## Deploying the Custom Action Control Assembly  
 After the custom action control assembly is created, it must be copied to the same directory as the Adminui.tasksequenceeditor.dll. Typically this directory is in %ProgramFiles%\Microsoft Configuration Manager\AdminUI\bin.  

## Using the Custom Action Control  
 To use the custom action, you create and edit a task sequence in the Configuration Manager console. Clicking **Add** displays a list of categories, and you should see the custom action listed in the category that you specified in the custom action MOF file.  

 After you select it, you will see the control that you have created. The action behaves like the default Configuration Manager actions. You can add conditions to the action and you can move the action within the task sequence.  

 For more information, see [How to Use a Configuration Manager Custom Action](../../develop/osd/how-to-use-a-configuration-manager-custom-action-control.md).  
