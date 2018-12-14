---
title: "Custom Action MOF Files"
titleSuffix: "Configuration Manager"
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: conceptual
ms.assetid: aa2b3692-f373-4c66-b22b-d14bfa0c58dd
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# About Configuration Manager Custom Action MOF Files
In System Center Configuration Manager, operating system deployment actions are defined in the Managed Object Format (MOF) file, %*ProgramFiles*%\Microsoft Configuration Manager\bin\i386\\_tasksequenceprovider.mof.  

 When you create a custom action, you must create a MOF file that declares your custom action. You then use Mofcomp.exe to add your changes to the SMS Provider. For more information, see [How to Create a MOF File for a Configuration Manager Custom Action](../../develop/osd/how-to-create-a-mof-file-for-a-configuration-manager-custom-action.md).  

 The administrator configures the custom action, as defined by the MOF file, by using a custom action control. For more information, see [About Configuration Manager Custom Actions](../../develop/osd/about-configuration-manager-custom-actions.md).  

## MOF File Content  
 A custom action derives from [SMS_TaskSequence_Action Server WMI Class](../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md). The MOF file declaration includes a class definition and various qualifiers for the command line, task sequence variables, category, and custom action control assembly location.  

 Properties declared in a class, except those with the `CommandLineArg` qualifier, are available as task sequence variables during client deployment. For more information, see [How to Use Task Sequence Variables in a Running Configuration Manager Task Sequence](../../develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md).  

 The namespace for the custom action is \\\root\SMS_Site_SITECODE. When the MOF file is compiled, the custom action is made a child of [SMS_TaskSequence_Action Server WMI Class](../../develop/reference/osd/sms_tasksequence_action-server-wmi-class.md).  

> [!NOTE]
>  For an example MOF, see the task sequence action MOF that is declared in _tasksequenceprovider.mof.  

 The section of the MOF file for the custom action declaration will look similar to the following example:  

```  
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

 The complete MOF also specifies the namespace and other information,  

 For the complete MOF for this sample, see [How to Create a MOF File for a Configuration Manager Custom Action](../../develop/osd/how-to-create-a-mof-file-for-a-configuration-manager-custom-action.md).  

### Command Line  
 The command line for the action is described in the `CommandLine` class qualifier. It defines the application that is called and the various arguments that can be supplied. For each command-line argument, there is a `CommandLineArg` class qualifier for the argument on the corresponding class property.  

 `CommandLine` typically takes the form:  

 `CommandLine("smsswd.exe /run:%1 Application.exe %2 %3")`  

 Smsswd.exe is used to run a program within a package. It requires the following arguments:  

|Argument|Description|  
|--------------|-----------------|  
|/run:%1|Identifies the package that the application is in. %1 is the package identifier ([SMS_Package Server WMI Class](../../develop/reference/core/servers/configure/sms_package-server-wmi-class.md)`PackageID` property).|  
|Application.exe|The custom action application that is performed.|  
|%2 - %n|One or more command-line arguments for Application.exe.|  

 The command-line substitution strings, %1, %2 and so forth, are defined by the `CommandLineArg` class qualifier. For example, the following declares %1.  

```  
[TaskSequencePackage, CommandLineArg(1)]  
string          PackageIDForApplicationExe;  
```  

 With the custom action control, you use the `PackageIDForApplicationExe` property to configure the package identifier.  

> [!NOTE]
>  Properties declared with the `CommandLineArg` qualifier are not available as task sequence variables during client deployment.  

### Action Category  
 An action can be associated with a specific category, in the task sequence editor drop down menu, by using the `ActionCategory` class qualifier.  

> [!NOTE]
>  Do not use a category that is already in use by another action.  

 The syntax is:  

 `ActionCategory{CategoryName,ActionOrder,CategoryOrder}`  

 `CategoryName`  
 The category name.  

 `ActionOrder`  
 The action order within the category.  

 `CategoryOrder`  
 The category order within all categories.  

 The default Configuration Manager categories that you can add an action to are:  

- General  

- Disks  

- User State  

- Images  

- Drivers  

- Settings  

  You can also create a new category by specifying a new category in the `ActionCategory` class qualifier. For example, the following MOF file creates a new category called My Custom Category. The action is placed second within the category and the category is placed fifth overall.  

  `ActionCategory{"My Custom Category",2,5"},`  

### ActionName  
 The `ActionName` class qualifier defines the custom action control name. The qualifier has the following syntax:  

 `ActionName{"Assembly", "Namespace.Properties.Resources", "Control"}`  

 `Assembly`  
 The assembly that contains the action control.  

 `Namespace.Properties.Resources`  
 The namespace for the resource that contains the displayed action name strings. For more information, see [How to Create a Configuration Manager Custom Action Control](../../develop/osd/how-to-create-a-configuration-manager-custom-action-control.md).  

 `Control`  
 The control that contains the string resources.  

### Action User Interface  
 The `ActionUI` class qualifier defines the location of the assembly and classes that are used by an action. The qualifier has the following syntax:  

 `ActionUI{"Assembly","Namespace", "Control", "Option control"}`  

 `Assembly`  
 The assembly that contains the action control.  

 `Namespace`  
 The namespace that the action control resides in.  

 `Control`  
 The action control displayed in the task sequence editor. It hosts the option control page.  

 `Option control`  
 The page used to manage action options, in the task sequence editor.  

 Multiple control tabs can be implemented by including more control class names separated by commas. For example:  

 ActionUI{"Assembly","Namespace", "Control1", "Control2", "Control3", "Option control"}  

### Action Variables  
 The `VariableName` qualifier is used to override the default variable name for a property.  

 A class property can be defined as a task sequence variable by adding the `VariableName` class qualifier. In the example above, the property `MessageTimeout` is an action variable with the name `RebootTimeout`.  

 If the `VariablePrefix` class qualifier is used, the variables are prefixed with the class qualifier value.  

 For more information about variable usage, see [How to Use Task Sequence Variables in a Running Configuration Manager Task Sequence](../../develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md)  

### Properties  

#### Qualifiers  
 There are several qualifiers that can be applied to the MOF properties. The following are commonly used:  

|Qualifier|Description|  
|---------------|-----------------|  
|CommandLineArg|A property that should be inserted on the command line|  
|Not_Null|A value is required for this property.|  
|ValueMap|Specifies a list of allowed string values.|  
|ValueRange|Specifies a range of allowed values (int fields).|  
|RequiredIfNull|A value is required for this property if another property is null.|  
|TaskSequencePackage|Identifies a property as a package identifier.|  
|VariableName|Specifies a different name for the property in the task sequence environment.|  
|AllowedLen|Specifies the minimum and maximum number of characters in a string.|  
|SuccessCodes|Specifies one or more return code from the executable that indicates success.|  

#### Restrictions  

-   Regular qualifier constraints can be applied to class properties. For example, in the example above, the command-line arguments cannot be `null`. For more information, see the [Windows Management Instrumentation (WMI) SDK](http://go.microsoft.com/fwlink/?LinkId=43950).  

-   Ensure that property names and qualifiers are synchronized between the MOF file, custom action control and client application. The property names must match as well as any limitations. For example, if an `int` property is required, and it must be in the range 1 - 512, then the MOF file should have a `Not_Null` and `ValueRange` qualifier, the custom control should ensure that the property is set and within range, and the client application should verify the value before using it.  

## See Also  
 [About Configuration Manager Custom Actions](../../develop/osd/about-configuration-manager-custom-actions.md)   
 [Extending Operating System Deployment](../../develop/osd/extending-operating-system-deployment.md)   
 [How to Create a Configuration Manager Custom Action Control](../../develop/osd/how-to-create-a-configuration-manager-custom-action-control.md)   
 [How to Create a MOF File for a Configuration Manager Custom Action](../../develop/osd/how-to-create-a-mof-file-for-a-configuration-manager-custom-action.md)   
 [How to Use Task Sequence Variables in a Running Configuration Manager Task Sequence](../../develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence.md)   
 [About Configuration Manager Custom Action Client Applications](../../develop/osd/about-configuration-manager-custom-action-client-applications.md)
