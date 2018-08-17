---
title: How to use task sequence variables
titleSuffix: Configuration Manager
description: Learn about how to use the variables in a Configuration Manager task sequence.
ms.date: 08/17/2018
ms.prod: configuration-manager
ms.technology: configmgr-osd
ms.topic: conceptual
ms.assetid: bc7de742-9e5c-4a70-945c-df4153a61cc3
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# How to use task sequence variables in Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

 The task sequence engine in the OS deployment feature of Configuration Manager uses many variables to control its behaviors. Use these variables to: 
 - Set conditions on steps
 - Change behaviors for specific steps
 - Use in scripts for more complex actions

 For a reference of all available task sequence variables, see [Task sequence variables](/sccm/osd/understand/task-sequence-variables).



## <a name="bkmk_types"></a> Types of variables

 There are several types of variables:  
 - [Built-in](#bkmk_built-in)
 - [Action](#bkmk_action)
 - [Custom](#bkmk_custom)
 - [Read-only](#bkmk_read-only)
 - [Array](#bkmk_array)


### <a name="bkmk_built-in"></a> Built-in variables

 Built-in variables provide information about the environment where the task sequence runs. Their values are available throughout the whole task sequence. Typically, the task sequence engine initializes built-in variables before it runs any steps. 

 For example, **\_SMSTSLogPath** is an environment variable that specifies the path to which Configuration Manager components write log files. Any task sequence step can access this environment variable. 

 The task sequence evaluates some variables before each step. For example, **\_SMSTSCurrentActionName** lists the name of the current step. 

### <a name="bkmk_action"></a> Action variables

 Task sequence action variables specify configuration settings that a single task sequence step uses. By default, the step initializes its settings before it runs. These settings are available only while the associated task sequence step runs. The task sequence adds the action variable value to the environment before it runs the step. It then removes the value from the environment after the step runs.

 For example, you add the **Run Command Line** step to a task sequence. This step includes a **Start In** property. The task sequence stores a default value for this property in the task sequence environment as the **WorkingDirectory** variable. The task sequence initializes this value before it runs the **Run Command Line** step. While this step is running, access the **Start In** property value from the **WorkingDirectory** value. After the step completes, the task sequence removes the value of the **WorkingDirectory** variable from the environment. If the task sequence contains another **Run Command Line** step, it initializes a new **WorkingDirectory** variable. At that time, the task sequence sets the variable to the starting value for the current step.  

 The *default* value for an action variable is present when the step runs. If you set a *new* value, it's available to multiple steps in the task sequence. If you override a default value, the new value remains in the environment and overrides the default value for other steps in the task sequence. For example, you add a **Set Task Sequence Variable** step as the first step of the task sequence. This step sets the **WorkingDirectory** variable to `C:\`. Any **Run Command Line** step in the task sequence uses the new starting directory value.  

 Some task sequence steps mark certain action variables as *output*. Steps later in the task sequence read these output variables.

 > [!Note]  
 > Not all task sequence steps have action variables. For example, although there are variables associated with the **Enable BitLocker** action, there are no variables associated with the **Disable BitLocker** action.  


### <a name="bkmk_custom"></a> Custom variables

 These variables are any that Configuration Manager doesn't create. Initialize your own variables to use as conditions, in command lines, or in scripts. 

 When you specify a name for a new task sequence variable, follow these guidelines:  

 - The task sequence variable name that you specify can contain letters, numbers, the underscore character (`_`), and a hyphen (`-`).  

 - Task sequence variable names have a minimum length of one character and a maximum length of 256 characters.  

 - User-defined variables must begin with a letter (`A-Z` or `a-z`).  

 - User-defined variable names can't begin with the underscore character. Only read-only task sequence variables are preceded by the underscore character.  

 - Task sequence variable names aren't case sensitive. For example, `OSDVAR` and `osdvar` represent the same task sequence variable.  

 - Task sequence variable names can't begin or end with a space. They also can't contain embedded spaces. The task sequence ignores any spaces at the beginning or the end of a variable name.  

 There's no set limit to how many task sequence variables you can create. However, the number of variables is limited by the size of the task sequence environment. The total size limit for the task sequence environment is 32 MB.  


### <a name="bkmk_read-only"></a> Read-only variables

 You can't change the value of some variables, which are read-only. Usually the name begins with an underscore character (\_). The task sequence uses them for its operations, and are visible in the task sequence environment. 

 These variables are useful in scripts or command-lines. For example, running a command line and piping the output to a log file in **\_SMSTSLogPath** with the other log files.

 > [!NOTE]  
 >  Read-only task sequence variables can be read by steps in a task sequence but they can't be set. For example, use a read-only variable as part of the command line for a **Run Command Line** step. You can't set a read-only variable by using the **Set Task Sequence Variable** step.  



### <a name="bkmk_array"></a> Array variables

 The task sequence stores some variables as an array. Each element in the array represents the settings for a single object. Use these variables when a device has more than one object to configure. The following task sequence steps use array variables:

 - [Apply Network Settings](task-sequence-steps.md#BKMK_ApplyNetworkSettings)  

 - [Format and Partition Disk](task-sequence-steps.md#BKMK_FormatandPartitionDisk)  



## <a name="bkmk_set"></a> How to set variables

 For custom variables or those that aren't read-only, there are several methods to initialize and set the value of the variable:  

 - [Set Task Sequence Variable](#bkmk_set-ts-step)
 - [Set Dynamic Variables](#bkmk_set-dyn-step)
 - [Collection and device variables](#bkmk_set-coll-var)
 - [TSEnvironment COM object](#bkmk_set-com)
 - [Prestart command](#bkmk_set-prestart)
 - [Task Sequence Media Wizard](#bkmk_set-media)

 You can delete a variable from the task sequence environment by using the same methods as creating a variable. To delete a variable from the task sequence environment, set the variable value to an empty string.  

 You can combine methods to set a task sequence variable to different values for the same sequence. In an advanced scenario, you might set the default values for steps in a sequence using the Task Sequence Editor and then set a custom variable value using the different creation methods. 

 If you set the same variable on a collection, on a device, and during the task sequence, the task sequence engine uses the following order:  

 1. It evaluates collection variables first.  

 2. Device-specific variables override the same variable set on a collection.  

 3. Variables set by any method during the task sequence take precedence over collection or device variables.  


#### General limitations for task sequence variable values  

 - Task sequence variable values cannot exceed 4,000 characters.  

 - You can't change a read-only task sequence variable. Read-only variables are designated by names that start with an underscore character (`_`).  

 - Task sequence variable values can be case-sensitive depending on the usage of the value. In most cases, task sequence variable values aren't case sensitive. A variable that contains a password is case-sensitive.  


### <a name="bkmk_set-ts-step"></a> Set Task Sequence Variable

 Use this step in the task sequence to set a single variable to a single value. 

 For more information, see [Set Task Sequence Variable](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable). 


### <a name="bkmk_set-dyn-step"></a> Set Dynamic Variables

 Use this step in the task sequence to set one or more task sequence variables. You define rules in this step to determine which variables and values to use. 

 For more information, see [Set Dynamic Variables](/sccm/osd/understand/task-sequence-steps#BKMK_SetDynamicVariables).


### <a name="bkmk_set-coll-var"></a> Collection and device variables

 Set variables on the properties of a collection or a specific device. 

 For more information, see [Create task sequence variables for computers and collections](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#BKMK_CreateTSVariables).


### <a name="bkmk_set-com"></a> TSEnvironment COM object

 To work with variables from a script, use the **TSEnvironment** object. 

 For more information, see [How to use variables in a running task sequence](/sccm/develop/osd/how-to-use-task-sequence-variables-in-a-running-task-sequence) in the Configuration Manager SDK.


### <a name="bkmk_set-prestart"></a> Prestart command

 The prestart command is a script or executable that runs in Windows PE before the user selects the task sequence. The prestart command can query a task sequence variable for information, or prompt a user for information, and then save it in the task sequence environment. Use the [TSEnvironment](#bkmk_set-com) COM object to read and write variables from the prestart command. 

 For more information, see [Prestart commands for task sequence media](/sccm/osd/understand/prestart-commands-for-task-sequence-media).


### <a name="bkmk_set-media"></a> Task Sequence Media Wizard

 Specify variables for task sequences that run from media. When using media to deploy the OS, you add the task sequence variables and specify their values when you create the media. The variables and their values are stored on the media.  

 > [!NOTE]  
 >  Task sequences are stored on stand-alone media. However, all other types of media, such as prestaged media, retrieve the task sequence from a management point.  

 When you run a task sequence from media, you can add a variable on the **Customization** page of the wizard. 

 Use the media variables in place of per-collection or per-computer variables. If the task sequence is running from media, per-computer and per-collection variables don't apply and aren't used.  

 > [!TIP]  
 >  The task sequence writes the package ID and prestart command line to the **CreateTSMedia.log** file on the computer that runs the Configuration Manager console. This log file includes the value for any task sequence variables. Review this log file to verify the value for the task sequence variables.  

 For more information, see [Create task sequence media](/sccm/osd/deploy-use/create-task-sequence-media).



## <a name="bkmk_access"></a> How to access variables

 After you specify the task sequence variable and its value by using one of the methods from the previous section, you can use the environment variable value in your task sequences. You can access default values for built-in task sequence variables, specify a new value for a variable, or use a custom task sequence variable in a command line or script.  

 Use the following methods to access variable values in the task sequence environment:
 - [Use in a step](#bkmk_access-step)
 - [Step condition](#bkmk_access-condition)
 - [Custom script](#bkmk_access-script)


### <a name="bkmk_access-step"></a> Use in a step

 Specify a variable value for a setting in a task sequence step. In the task sequence editor, edit the step, and specify the variable name as the field value. Enclose the variable name in percent signs (`%`) to indicate that it's an environment variable. 

 For example, use the variable name as part of the **Command Line** field of the **Run Command Line** task sequence step. The following command line writes the computer name to a text file. 

 `cmd.exe /c %_SMSTSMachineName% > C:\File.txt`


### <a name="bkmk_access-condition"></a> Step condition

 Use built-in or custom task sequence variables as part of a condition on a step or group. The task sequence evaluates the variable value before it runs the step or group.

 To add a condition that evaluates a variable value, do the following steps:  

 1. In the task sequence editor, select the step or group to which you want to add the condition.  

 2. Switch to the **Options** tab for the step or group. Click **Add Condition**, and select **Task Sequence Variable**.  

 3. In the **Task Sequence Variable** dialog box, specify the following settings:  

    - **Variable**: The name of the variable. For example, `_SMSTSInWinPE`.  

    - **Condition**: The condition to evaluate the variable value. For example, **equals**.  

    - **Value**: The value of the variable to check. For example, `false`.  

 The three examples above together represent a common condition to test whether the task sequence is running from a boot image in Windows PE: 

 **Task Sequence Variable** `_SMSTSInWinPE equals "false"`

 See this condition on the **Capture Files and Settings** group of the default task sequence template to install an existing OS image.


### <a name="bkmk_access-script"></a> Custom script

 Read and write task sequence variables by using the Microsoft.SMS.TSEnvironment COM object while the task sequence is running.

 The following Windows PowerShell example queries the **_SMSTSLogPath** variable to get the current log location. The script also sets a custom variable.

 ```PowerShell
 # Create an object to access the task sequence environment
 $tsenv = New-Object -ComObject Microsoft.SMS.TSEnvironment
 
 # Query the environment to get an existing variable
 # Set a variable for the task sequence log path
 $LogPath = $tsenv.Value("_SMSTSLogPath")

 # Or, convert all of the variables currently in the environment to PowerShell variables
 $tsenv.GetVariables() | % { Set-Variable -Name "$_" -Value "$($tsenv.Value($_))" }

 # Write a message to a log file
 Write-Output "Hello world!" | Out-File -FilePath "$_SMSTSLogPath\mylog.log" -Encoding "Default" -Append
 
 # Set a custom variable "startTime" to the current time
 $tsenv.Value("startTime") = (Get-Date -Format HH:mm:ss) + ".000+000"
 ```



## See also

- [Task sequence steps](/sccm/osd/understand/task-sequence-steps)
- [Task sequence variables](/sccm/osd/understand/task-sequence-variables)
- [Planning considerations for automating tasks](/sccm/osd/plan-design/planning-considerations-for-automating-tasks)
