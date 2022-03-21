---
title: "Use a Custom Action Control"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: b08bf2a3-d433-4024-ab38-824620dacd05
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Use a Configuration Manager Custom Action Control
In Configuration Manager, you use a custom action control by selecting it in the Configuration Manager console Task Sequence Editor. The custom action control is used to configure a custom action that you have defined. The custom action is then becomes a step in the task sequence you are editing. The following procedure assumes that you have completed the tasks in the following topics:  

 [How to Create a Configuration Manager Custom Action Control](../../develop/osd/how-to-create-a-configuration-manager-custom-action-control.md)  

 [How to Create a MOF File for a Configuration Manager Custom Action](../../develop/osd/how-to-create-a-mof-file-for-a-configuration-manager-custom-action.md)  

 The following procedure demonstrates the custom action control saving its properties and reloading them the next time that the action is edited.  

 To use the custom action as part of the sequence that contains it, you will need to advertise it using a Configuration Manager task sequence package. For more information, see [About Configuration Manager Custom Action Client Applications](../../develop/osd/about-configuration-manager-custom-action-client-applications.md)  

> [!NOTE]
>  Step 1 and step 2 are only necessary if the action control Managed Object Format (MOF) file or assembly has been changed.  

### How to use a custom action control in the task sequence editor  

1.  If the Configuration Manager console is open, close it.  

2.  Open the Configuration Manager console.  

3.  In the Configuration Manager console, navigate to **Software Library** / **Operating Systems**.  

4.  Right-click **Task Sequences**, and select **Create Task Sequence**. The New Task Sequence Wizard is displayed.  

5.  Select **Create a new custom task sequence**, and click **Next**.  

6.  In **Task sequence name**, enter `My custom task sequence`.  

7.  Click **Next**, confirm the summary information, and click **Next** again to create the task sequence.  

8.  Click **Close** to close the wizard.  

9. In the results pane, right-click the task sequence that you just created and select **Edit** to display the Task Sequence Editor.  

10. In the Task Sequence Editor, select **Add**, and the categories list is displayed.  

11. Select **CustomActionCategory**, and your custom action appears as one of the possible choices.  

12. Select your custom action (**ConfigMgrTSActionControl**), and the control is displayed.  

13. Add some text to the edit box, and then click **OK**. The Task Sequence Editor should be closed.  

14. Edit the task sequence again and select your custom action.  

15. Note that the text you entered has been retained.  

## See Also  
 [About Configuration Manager Custom Actions](../../develop/osd/about-configuration-manager-custom-actions.md)   
 [About Configuration Manager Custom Action Client Applications](../../develop/osd/about-configuration-manager-custom-action-client-applications.md)   
 [How to Create a Configuration Manager Custom Action Control](../../develop/osd/how-to-create-a-configuration-manager-custom-action-control.md)   
 [How to Create a MOF File for a Configuration ManagerCustom Action](../../develop/osd/how-to-create-a-mof-file-for-a-configuration-manager-custom-action.md)   
 [How to Delete an Operating System Deployment Task Sequence Action](../../develop/osd/how-to-delete-an-operating-system-deployment-task-sequence-action.md)
