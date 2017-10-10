---
title: "Create a MOF File for a Custom Action"
titleSuffix: "Configuration Manager"
ms.custom: ""
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.reviewer: ""
ms.suite: ""
ms.technology:
  - "configmgr-other"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to:
  - "System Center Configuration Manager (current branch)"
ms.assetid: c0e8adb8-58e6-4954-abeb-ba7d2344de06searchScope: - ConfigMgr SDK
caps.latest.revision: 5
author: "shill-ms"
ms.author: "v-suhill"
manager: "mbaldwin"
---
# How to Create a MOF File for a Configuration Manager Custom Action
You define a custom task sequence action, its properties and its user interface controls by creating a managed object format (MOF) file to describe the class. The MOF file is then compiled by using Mofcomp.exe.  

 For more information about custom action MOF files, see [About the Configuration Manager Custom Action MOF File](../../develop/osd/about-configuration-manager-custom-action-mof-files.md).  

 The following procedure adds a class declaration for the custom action that you created in [How to Create a Configuration Manager Custom Action Control](../../develop/osd/how-to-create-a-configuration-manager-custom-action-control.md).  

 For information about using the custom action, see [About Configuration Manager Custom Action Client Applications](../../develop/osd/about-configuration-manager-custom-action-client-applications.md).  

### To create a MOF file for a custom action  

1.  In Notepad, create a new file.  

2.  Add the following MOF code to the file.  

    ```  

    #pragma autorecover  

    #pragma namespace("\\\\.\\root")  

    // SMS Root Storage  
    instance of __Namespace  
    {  
        Name = "SMS";  
    };  

    #pragma namespace("\\\\.\\root\\SMS")  

    // Configuration Manager database name for this computer.  
    instance of __Namespace  
    {  
        Name = "site_REPLACESITECODE";  
    };  

    #pragma namespace("\\\\.\\root\\SMS\\site_REPLACESITECODE")  

    #pragma classflags("forceupdate")  

    [   CommandLine("smsswd.exe /run:%1 Application.exe /user:%2"),  
        VariablePrefix("MyCustomActionPrefix"),  
        ActionCategory("My Custom Action Category,7,1"),  
        ActionName{"ConfigMgrTSAction.dll", "ConfigMgrTSAction.Properties.Resources", "ConfigMgrTSAction"},  
        ActionUI{"ConfigMgrTSAction.dll", "ConfigMgrTSAction","ConfigMgrTSActionControl",   
    "ConfigureTSActionOptions"}  
        ]  
    class ConfigMgrTSActionControl : SMS_TaskSequence_Action  
    {  
        [TaskSequencePackage, CommandLineArg(1)]  
        string          PackageIDForApplicationExe;  

        [Not_Null, CommandLineArg(2)]  
        string          User;  

        [VariableName("CustomLocation")]  
        string          Location;  

    };  
    ```  

3.  Replace `REPLACESITECODE` with the site code for your Configuration Manager site.  

4.  Choose a folder, and save the file as type `All Files` with the name CustomAction.mof.  

5.  Open a Command Prompt window, navigate to the folder that you saved CustomAction.mof in, and enter the following:  

    ```  
    mofcomp CustomAction.mof  
    ```  

6.  Press ENTER to compile the CustomAction.mof.  

7.  Confirm that the class has been added in CIM Studio. The class should be listed as a child class of [SMS_TaskSequence_Action](../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

8.  Complete [How to Use a Configuration Manager Custom Action Control](../../develop/osd/how-to-use-a-configuration-manager-custom-action-control.md).  

## See Also  
 [About Configuration Manager Custom Actions](../../develop/osd/about-configuration-manager-custom-actions.md)   
 [About the Configuration Manager Custom Action MOF File](../../develop/osd/about-configuration-manager-custom-action-mof-files.md)   
 [Extending Operating System Deployment](../../develop/osd/extending-operating-system-deployment.md)   
 [How to Create a Configuration Manager Custom Action Control](../../develop/osd/how-to-create-a-configuration-manager-custom-action-control.md)   
 [About Configuration Manager Custom Action Client Applications](../../develop/osd/about-configuration-manager-custom-action-client-applications.md)
