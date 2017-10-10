---
title: Planning considerations for automating tasks
description: "Plan before you automate tasks in System Center Configuration Manager."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fc497a8a-3c54-4529-8403-6f6171a21c64
caps.latest.revision: 13
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe

---
# Planning considerations for automating tasks in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

You can create task sequences to automate tasks in your System Center Configuration Manager environment. These tasks range from capturing an operating system on a reference computer to deploying the operating system to one or more destination computers. The actions of the task sequence are defined in the individual steps of the sequence. When the task sequence is run, the actions of each step are performed at the command-line level in the Local System context without requiring user intervention. Use the following sections to help plan  to automate tasks in Configuration Manager.

##  <a name="BKMK_TSStepsActions"></a> Task sequence steps and actions  
 Steps are the basic components of a task sequence. They can contain commands that configure and capture the operating system of a reference computer, or they can contain commands that install the operating system, drivers, the Configuration Manager client, and software on the destination computer. The commands of a task sequence step are defined by the actions of the step. There are two types of actions. An action that you define by using a command-line string is referred to as a custom action. An action that is predefined by Configuration Manager is referred to as a built-in action. A task sequence can perform any combination of custom and built-in actions.  

 Task sequence steps can also include conditions that control how the step behaves, such as stopping the task sequence or continuing the task sequence if an error occurs. Conditions are added to the step by including a task sequence variable to the step. For example, you could use the **SMSTSLastActionRetCode** variable to test the condition of the previous step. Variables can be added to a single step or a group of steps.  

 Task sequence steps are processed sequentially, which includes the action of the step and any conditions that are assigned to the step. When Configuration Manager starts to process a task sequence step, the next step is not started until the previous action has completed. A task sequence is considered complete when all its steps have been completed or when a failed step causes Configuration Manager to stop running the task sequence before all its steps are completed. For example, if the step of a task sequence cannot locate a referenced image or package on a distribution point, the task sequence contains a broken reference and Configuration Manager stops running the task sequence at that point unless the failed step has a condition to continue when an error occurs.  

> [!IMPORTANT]  
>  By default, a task sequence fails after one step or action fails. If you want the task sequence to continue even when a step fails, edit the task sequence, click the **Options** tab, and then select **Continue on error**.  

 For more information about the steps that can be added to a task sequence, see [Task sequence steps](../understand/task-sequence-steps.md).  

##  <a name="BKMK_TSGroups"></a> Task sequence groups  
 **Groups** are multiple steps within a task sequence. A task sequence group consists of a name, an optional description, and any optional conditions that are evaluated as a unit before that task sequence continues with the next step. Groups can be nested within each other, and a group can contain a mixture of steps and subgroups. Groups are useful for combining multiple steps that share a common condition.  

> [!IMPORTANT]  
>  By default, a task sequence group fails when any step or embedded group within the group fails. If you want the task sequence to continue when a step or embedded group fails, edit the task sequence, click the **Options** tab, and then select **Continue on error**.  

 The following table shows how the **Continue on error** option works when you group steps.  

 In this example, there are two groups of task sequences that contain three task sequence steps each.  

|Task sequence group or step|Continue on error setting|  
|---------------------------------|-------------------------------|  
|**Task Sequence Group 1**|**Continue on error** selected.|  
|Task Sequence Step 1|**Continue on error** selected.|  
|Task Sequence Step 2|Not set.|  
|Task Sequence Step 3|Not set.|  
|**Task Sequence Group 2**|Not set.|  
|Task Sequence Step 4|Not set.|  
|Task Sequence Step 5|Not set.|  
|Task Sequence Step 6|Not set.|  

-   If task sequence step 1 fails, the task sequence continues with task sequence step 2.  

-   If task sequence step 2 fails, the task sequence does not run task sequence step 3 but continues to run task sequence steps 4 and 5, which are in a different task sequence group.  

-   If task sequence step 4 fails, no more steps are run, and the task sequence fails because the **Continue on error** setting was not configured for task sequence group 2.  

 You must assign a name to task sequence groups, although the group name does not have to be unique. You can also provide an optional description for the task sequence group.  

##  <a name="BKMK_TSVariables"></a> Task sequence variables  
 Task sequence variables are a set of name and value pairs that supply configuration and operating system deployment settings for computer, operating system, and user state configuration tasks on a Configuration Manager client computer. Task sequence variables provide a mechanism to configure and customize the steps in a task sequence.  

 When you run a task sequence, many of the task sequence settings are stored as environment variables. You can access or change the values of built-in task sequence variables, and you can create new task sequence variables to customize the way a task sequence runs on a destination computer.  

 You can use task sequence variables in the task sequence environment to perform the following actions:  

-   Configure settings for a task sequence action  

-   Supply command-line arguments for a task sequence step  

-   Evaluate a condition that determines whether a task sequence step or group is run  

-   Provide values for custom scripts used in a task sequence  

 For example, you might have a task sequence that includes a **Join Domain or Workgroup** task sequence step. The task sequence might be deployed to different collections, where the membership of the collection is determined by domain membership. In that case, you can specify a per-collection task sequence variable for each collection's domain name and then use that task sequence variable to supply the appropriate domain name in the task sequence.  

###  <a name="BKMK_TSCreateVariables"></a> Create task sequence variables  
 You can add new task sequence variables to customize and control the steps in a task sequence. For example, you can create a task sequence variable to override a setting for a built-in task sequence step. You can also create a custom task sequence variable to use with conditions, command lines, or custom steps in the task sequence. When you create a task sequence variable, the task sequence variable and the associated value is preserved within the task sequence environment, even when the sequence restarts the destination computer. The variable and its value can be used within the task sequence across different operating system environments. For example, it can be used in a full Windows operating system and in the Windows PE environment.  

 The following table describes the methods to create a task sequence variable and additional usage information.  

|Create method|Usage|  
|-------------------|-----------|  
|Setting fields in task sequence steps by using the Task Sequence Editor|Specifies default values for the task sequence step. The variable and value are accessible only when the step runs in the task sequence. They are not part of the overall sequence environment, and they are not accessible by other task sequence steps in the task sequence.<br /><br /> For a list of the built-in variables and their associated actions, see [Task sequence action variables](../understand/task-sequence-action-variables.md).|  
|Adding a set task sequence variable step in a task sequence|Specifies the task sequence variable and value in the task sequence environment when the task sequence step is run as part of a task sequence. All subsequent task sequence steps can access the environment variable and its value.|  
|Defining a per-collection variable|Specifies task sequence variables and values for a collection of computers. All task sequences targeted to the collection can access the task sequence variables and their values.|  
|Defining a per-computer variable|Specifies task sequence variables and values for a particular computer. All task sequences targeted to the computer can access the task sequence variables and their values.|  
|Adding a task sequence variable on the **Customization** page of the Task Sequence Media Wizard|Specifies task sequence variables and values for the task sequence that is run from the media that can access the task sequence variable and its value.|  

 To override the default value for a built-in task sequence variable, you must define a task sequence variable with the same name as the built-in task sequence variable. For a list of built-in task sequence variables with the associated actions and usage, see [Task sequence built-in variables](../understand/task-sequence-built-in-variables.md).  

 You can delete a task sequence variable from the task sequence environment by using the same methods as creating a task sequence variable. In this case, to delete a variable from the task sequence environment, you set the task sequence variable value to an empty string.  

 You can combine methods to set an environment task sequence variable to different values for the same sequence. In an advanced scenario, you might set the default values for steps in a sequence using the Task Sequence Editor and then set a custom variable value using the different creation methods. The following list describes the rules that determine which value is used when a task sequence variable is created by using more than one method.  

1.  The **Set Task Sequence Variable** step overrides all other creation methods.  

2.  Per-computer variables take precedence over per-collection variables. If you specify the same task sequence variable name for a per-computer variable and a per-collection variable, the per-computer variable value is used when the destination computer runs the deployed task sequence.  

3.  Task sequences can be run from media. Use the media variables in place of per-collection or per-computer variables. If the task sequence is running from media, per-computer and per-collection variables do not apply and are not used. Instead, task sequence variables defined on the **Customization** page of the Task Sequence Media wizard are used to set values specific to a task sequence that runs from media  

4.  If a task sequence variable value is not set in the overall sequence environment, built-in actions use the default value for the step, as set in the Task Sequence Editor.  

 In addition to overriding values for built-in task sequence step settings, you can also create a new environment variable for use in a task sequence step, script, command line, or condition. When you specify a name for a new task sequence variable, follow these guidelines:  

-   The task sequence variable name that you specify can contain letters, numbers, the underscore character (_), and a hyphen (-).  

-   Task sequence variable names have a minimum length of 1 character and a maximum length of 256 characters.  

-   User defined variables must begin with a letter (A-Z or a-z).  

-   User-defined variable names cannot begin with the underscore character. Only read-only task sequence variables are preceded by the underscore character  

    > [!NOTE]  
    >  Read-only task sequence variables can be read by task sequence steps in a task sequence but they cannot be set. For example, you can use a read-only task sequence variable as part of the command line for a **Run Command Line** task sequence action variable, but you cannot set a read-only variable by using the **Set Task Sequence Variable** action variable.  

-   Task sequence variable names are not case sensitive. For example, OSDVAR and osdvar represent the same task sequence variable.  

-   Task sequence variable names cannot begin or end with a space or contain embedded spaces. Spaces that are left at the beginning or the end of a task sequence variable name are ignored.  

 The following table displays examples of valid and non-valid user-specified task sequence variables.  

|Examples of valid user-specified variable nNames|Examples of non valid user-specified variable names|  
|-------------------------------------------------------|----------------------------------------------------------|  
|MyVariable|1Variable<br /><br /> User-specified task sequence variables cannot begin with a number.|  
|My_Variable|MyV@riable<br /><br /> User-specified task sequence variables cannot contain the @ symbol.|  
|My_Variable_2|_MyVariable<br /><br /> User-specified task sequence variables cannot begin with an underscore.|  

 General limitations for task sequence variables:  

-   Task sequence variable values cannot exceed 4,000 characters.  

-   You cannot create or override a read-only task sequence variable. Read-only variables are designated by names that start with an underscore character (_). You can access the value of read-only task sequence variables in your task sequence; however, you cannot change their associated values.  

-   Task sequence variable values can be case sensitive depending on the usage of the value. In most cases, task sequence variable values are not case sensitive. However, some values can be case sensitive such as a variable that contains a password.  

-   There is no limit to how many task sequence variables can be created. However, the number of variables is limited by the size of the task sequence environment. The total size limit for the task sequence environment is 32 MB.  

###  <a name="BKMK_TSEnvironmentVariables"></a> Access environment variables  
 After you specify the task sequence variable and its value by using one of the methods from the previous section, you can use the environment variable value in your task sequences. You can access default values for built-in task sequence variables, specify a new value for a built-in variable, or use a custom task sequence variable in a command line or script.  

 The following table outlines task sequence operations that can be performed by accessing the task sequence environment variables.  

|Task sequence operation|Usage|  
|-----------------------------|-----------|  
|Configure action settings|You can specify that a task sequence step setting is provided by a variable value when the sequence runs.<br /><br /> To supply a task sequence step setting by using a task sequence environment variable, use the Task Sequence Editor to edit the step and specify the variable name as the field value. The variable name must be enclosed in percent signs (%) to indicate that it is an environment variable.|  
|Supply command-line arguments|You can specify part or all of a custom command line by using an environment variable value.<br /><br /> To supply a command-line setting by using an environment variable, use the variable name as part of the **Command Line** field of the **Run Command Line** task sequence step. The variable name must be enclosed in percent signs (%).<br /><br /> For example, the following command line uses a built-in environment variable to write the computer name to C:\File.txt.<br /><br /> <br /><br /> **Cmd /C %_SMSTSMachineName% > C:\File.txt**|  
|Evaluate a step condition|You can use built-in or custom task sequence environment variables as part of a task sequence step or group condition. The environment variable value will be evaluated before the task sequence step or group runs.<br /><br /> To add a condition that evaluates a variable value, do the following:<br /><br /> 1.  Select the step or group that you want to add the condition to.<br />2.  On the **Options** tab for the step or group, select **Task Sequence Variable** from the **Add Condition** drop down.<br />3.  In the **Task Sequence Variable** dialog box, specify the name of the variable, the condition that is tested, and the value of the variable.|  
|Provide information for a custom script|Task Sequence variables can be read and written by using the Microsoft.SMS.TSEnvironment COM object while the task sequence is running.<br /><br /> The following example illustrates a Visual Basic script file that queries the **_SMSTSLogPath** task sequence variable to get the current log location. The script also sets a custom variable.<br /><br /> <br /><br /> **dim osd: set env = CreateObject("Microsoft.SMS.TSEnvironment")**<br /><br /> <br /><br /> **dim logPath**<br /><br /> <br /><br /> **' You can query the environment to get an existing variable.**<br /><br /> **logPath = env("_SMSTSLogPath")**<br /><br /> <br /><br /> **' You can also set a variable in the OSD environment.**<br /><br /> **env("MyCustomVariable") = "varname"**<br /><br /> <br /><br /> For more information about how to use task sequence variables in scripts, refer to the SDK documentation|  

###  <a name="BKMK_ComputerCollectionVariables"></a> Computer and collection variables  
 You can configure task sequences to run on multiple computers or collections simultaneously. You can specify unique per-computer or per-collection information, such as specify a unique operating system product key or join all the members of a collection to a specified domain.  

 You can assign task sequence variables to a single computer or a collection. When the task sequence starts to run on the target computer or collection, the values specified are applied to the target computer or collection.  

 You can specify task sequence variables for a single computer or a collection. When the task sequence starts to run on the target computer or collection, the variables specified are added to the environment and the values are available to all task sequence steps in the task sequence.  

> [!WARNING]  
>  If you use the same variable name for both a per-collection and per-computer variable, the computer variable value takes precedence over the collection variable. Task sequence variables that you assign to collections take precedence over built-in task sequence variables.  

 For more information about how to create task sequence variables for computers and collections, see [Create task sequence variables for computers and collections](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_CreateTSVariables).  

###  <a name="BKMK_TSMediaVariables"></a> Task sequence media variables  
 You can specify task sequence variables for task sequences that are run from media. When using media to deploy the operating system you add the task sequence variables and specify their values when you create the media; the variables and their values are stored on the media.  

> [!NOTE]  
>  Task sequences are stored on stand-alone media. However, all other types of media, such as prestaged media, retrieve the task sequence from a management point.  

 You can specify task sequence variables on the **Customization** page of the Task Sequence Media Wizard. For information about how to create media, see [Create task sequence media](../deploy-use/create-task-sequence-media.md).  

> [!TIP]  
>  The task sequence writes the package ID and prestart command-line, including the value for any task sequence variables, to the CreateTSMedia.log log file on the computer that runs the Configuration Manager console. You can review this log file to verify the value for the task sequence variables.  

##  <a name="BKMK_TSCreate"></a> Create a  task sequence  
 You create task sequences by using the Create Task Sequence Wizard. The wizard can create built-in task sequences that perform specific tasks or custom task sequences that can perform many different tasks.  

 For example, you can create task sequences that build and capture an operating system image of a reference computer, install an existing operating system image on a destination computer, or create a custom task sequence that performs a customized task. You can use custom task sequences to perform specialized operating system deployments.  

 For more information about how to create task sequences, see [Create task sequences](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_CreateTaskSequence).  

##  <a name="BKMK_TSEdit"></a> Edit a task sequence  
 You edit the task sequence by using the **Task Sequence Editor**. The editor can make the following changes to the task sequence:  

-   You can add or remove steps from the task sequence.  

-   You can change the order of the steps of the task sequence.  

-   You can add or remove groups of steps.  

-   You can specify whether the task sequence continues when an error occurs.  

-   You can add conditions to the steps and groups of a task sequence.  

> [!IMPORTANT]  
>  If the task sequence has any unassociated references to a package or a program as a result of the edit, you must correct the reference, delete the unreferenced program from the task sequence, or temporarily disable the failed task sequence step until the broken reference is corrected or removed.  

 For more information about how to edit task sequences, see [Edit a task sequence](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_ModifyTaskSequence).  

##  <a name="BKMK_TSDeploy"></a> Deploy a task sequence  
 You can deploy a task sequence to destination computers that are in any Configuration Manager collection. This includes the **All Unknown Computers** collection that is used to deploy operating systems to unknown computers. However, you cannot deploy a task sequence to user collections.  

> [!IMPORTANT]  
>  Do not deploy task sequences that install operating systems to inappropriate collections, such as the **All Systems** collection. Be sure that the collection that you deploy the task sequence to contains only those computers where you want the operating system to be installed. To help prevent unwanted operating system deployment, you can manage deployment settings. For more information, see [Settings to manage high-risk deployments](../../protect/understand/settings-to-manage-high-risk-deployments.md).  

 Each destination computer that receives the task sequence runs the task sequence according to the settings specified in the deployment. The task sequences itself does not contain associated files or programs. Any files that are referenced by a task sequence must already be present on the destination computer or reside on a distribution point that clients can access. In addition, the task sequence installs the packages that are referenced by programs, even if the program or package is already installed on the destination computer.  

> [!NOTE]  
>  In comparison to packages and programs, if the task sequence installs an application, the application installs only if the requirement rules for the application are met and the application is not already installed, based on the detection method that is specified for the application.  

 The Configuration Manager client runs a task sequence deployment when it downloads client policy. To initiate this action rather than wait until the next polling cycle, see [Initiate Policy Retrieval for a Configuration Manager Client](../../core/clients/manage/manage-clients.md#BKMK_PolicyRetrieval).  

 When you deploy task sequences to Windows Embedded devices that are write filter enabled, you can specify whether to disable the write filter on the device during the deployment and then restart the device after the deployment. If the write filter is not disabled, the task sequence is deployed to a temporary overlay and it will not be available when the device restarts.  

> [!NOTE]  
>  When you deploy a task sequence to a Windows Embedded device, ensure that the device is a member of a collection that has a configured maintenance window. This allows you to manage when the write filter is disabled and enabled, and when the device restarts.  
>   
>  If clients download task sequences outside of a maintenance window, the task sequence is downloaded twice. In this scenario clients will download the task sequence, disable the write filters, restart the computer, and then download the task sequence again because the task sequence was downloaded to the temporary overlay which is cleared when the device restarts.  

 For more information about how to deploy task sequences, see the [Deploy a task sequence](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_DeployTS).  

##  <a name="BKMK_TSExportImport"></a> Export and import a task sequences  
 Configuration Manager lets you export and import task sequences. When you export a task sequence, you can include the objects that are referenced by the task sequence. These include an operating system image, a boot image, a client agent package, a driver package, and applications that have dependencies.  

> [!NOTE]  
>  The export and import process for task sequences is very similar to the export and import process for applications in Configuration Manager.  

 For more information about how to export and import task sequences, see [Export and import task sequences](../deploy-use/manage-task-sequences-to-automate-tasks.md#BKMK_ExportImport).  

##  <a name="BKMK_TSRun"></a> Run a task sequence  
 By default, task sequences always run by using the Local System account. The task sequence command-line step provides the ability to run the task sequence as a different account. When the task sequence is run, the Configuration Manager client first checks for any referenced packages before it starts the steps of the task sequence. If a referenced package is not validated or is not available on a distribution point, the task sequence returns an error for the associated task sequence step.  

 If a distributed task sequence is configured to download and run, all dependent packages and applications are downloaded to the Configuration Manager client cache. The required packages and applications are obtained from distribution points, and if the Configuration Manager client cache size is too small or the package or application cannot be found, the task sequence fails and a status message is generated. You can also specify that the client downloads the content only when it is required when you select **Download content locally when needed by running task sequence**, or you can use the **Run program from distribution point** option to specify that the client installs the files directly from the distribution point without downloading them into the cache first. The **Run program from distribution point** option is available only if the referenced packages have the setting **Copy the content in this package to a package share on distribution points** enabled on the **Data Access** tab of the **Package** properties.  

 If a dependent package or application cannot be located by the client running the task sequence, the client immediately sends an error when the deployment is configured as **Available**. However, if the deployment is configured as **Required**, the Configuration Manager client waits and retries to download the content until the deadline, in case the content is not yet replicated to a distribution point that the client can access.  

 When a task sequence completes successfully or fails, Configuration Manager records this in the Configuration Manager client history. You cannot cancel or stop a task sequence after it is initiated on a computer.  

> [!IMPORTANT]  
>  If a task sequence step requires the client computer to restart, the client must be able to boot to a formatted disk partition. Otherwise, the task sequence fails regardless of any error handling that is specified by the task sequence.  

 When a dependent object of a task sequence, such as a software distribution package, is updated to a newer version, any task sequence that references the package is automatically updated and it references the newest version, regardless of how many updates have been deployed.  

> [!NOTE]  
>  Before a Configuration Manager client runs a task sequence, the client checks all task sequences for possible dependencies and the availability of those dependencies on a distribution point. If the client finds a deleted object that the task sequence depends on, the client generates an error and does not run the task sequence.  

###  <a name="BKMK_RunProgram"></a> Run a program before the task sequence is run  
 You can select a program that runs before the task sequence is run. To specify a program to run first, open the **Properties** dialog box for the task sequence and select the **Advanced** tab to set the following options:  

> [!IMPORTANT]  
>  To run a program before the task sequence is run, all content for the task sequence and program must be available on a package share for the package. You configure the package share on the **Data Access** tab in the properties for the package.  

-   **Run another program first**: Specify that you want another program to run before the task sequence is run.  

    > [!IMPORTANT]  
    >  This setting applies only to task sequences that run in the full operating system. Configuration Manager ignores this setting if the task sequence is started by using PXE or boot media.  

-   **Package**: Specify the package that contains the program.  

-   **Program**: Specify the program to run.  

-   **Always run this program first**: Specify that you want Configuration Manager to run this program every time it runs the task sequence on the same client. By default, after a program is run successfully, the program is not run again if the task sequence is rerun on the same client.  

 If the selected program fails to run on a client, the task sequence is not run.  

##  <a name="BKMK_TSMaintenanceWindow"></a> Use a maintenance window to specify when a task sequence can run  
 You can specify when the task sequence can run by defining a maintenance window for the collection that contains your destination computers. Maintenance windows are configured with a start date, a start and finish time, and a recurrence pattern. In addition, when you set the schedule for the maintenance window you can specify that the maintenance window applies only to task sequences. For more information, see [How to use maintenance windows](../../core/clients/manage/collections/use-maintenance-windows.md).  

> [!IMPORTANT]  
>  When you configure a maintenance window to run a task sequence, once the task sequences starts it continues to run even if the maintenance window closes. The task sequence will either complete successfully or fail.  

##  <a name="BKMK_TSNetworkAccessAccount"></a> Task sequences and the Network Access Account  
 Although task sequences run only in the context of the Local System account, you might need to configure the Network Access Account in the following circumstances:  

-   You must configure the Network Access Account correctly or the task sequence will fail if it tries to access Configuration Manager packages on distribution points to complete its task. For more information about the Network Access account, see [Network Access Account](../../core/plan-design/hierarchy/manage-accounts-to-access-content.md#bkmk_NAA).  

    > [!NOTE]  
    >  The Network Access Account is never used as the security context for running programs, installing applications, installing updates, or running task sequences; however, the Network Access account is used to access the associated resources on the network.  

-   When you use a boot image to initiate an operating system deployment, Configuration Manager uses the Windows PE environment, which is not a full operating system. The Windows PE environment uses an automatically generated, random name that is not a member of any domain. If you do not configure the Network Access Account correctly, the computer might not have the necessary permissions to access the required Configuration Manager packages to complete the task sequence.  

##  <a name="BKMK_TSCreateMedia"></a> Create media for task sequences  
 You can write task sequences and their related files and dependencies to several types of media. This includes writing to removable media such as a DVD or CD set or a USB flash drive for capture, stand-alone, and bootable media, or writing to a Windows Imaging Format (WIM) file for prestaged media.  

 You can create the following types of media:  

-   **Capture media**. Capture media captures an operating system image that is configured and created outside the Configuration Manager infrastructure. Capture media can contain custom programs that can run before a task sequence runs. The custom program can interact with the desktop, prompt the user for input values, or create variables to be used by the task sequence.  

     For more information, see [Create capture media](../deploy-use/create-capture-media.md).  

-   **Stand-alone media**. Stand-alone media contains the task sequence and all associated objects that are necessary for the task sequence to run. Stand-alone media task sequences can run when Configuration Manager has limited or no connectivity to the network. Stand-alone media can be run in the following ways:  

    -   If the destination computer is not booted, the Windows PE image that is associated with the task sequence is used from the stand-alone media and the task sequence begins.  

    -   The stand-alone media can be manually started if a user is logged on to the network and initiates the installation.  

    > [!IMPORTANT]  
    >  The steps of a stand-alone media task sequence must be able to run without any retrieving any data from the network; otherwise, the task sequence step that tries to retrieve the data fails. For example, a task sequence step that requires a distribution point to obtain a package fails; however if the necessary package is contained on the stand-alone media, the task sequence step succeeds.  

     For more information, see [Create stand-alone media](../deploy-use/create-stand-alone-media.md).  

-   **Bootable media**. Bootable media contains the required files to start a destination computer so that it can connect to the Configuration Manager infrastructure to determine which task sequences to run based on its membership to a collection. The task sequence and dependent objects are not contained on the media; instead, they are obtained over the network from the Configuration Manager client. This method is useful for new computers or bare-metal deployments, or when no Configuration Manager client or operating system is on the destination computer.  

     For more information, see [Create bootable media](../deploy-use/create-bootable-media.md).  

-   **Prestaged media**. Prestaged media deploys an operating system image to a destination computer that is not provisioned. The prestaged media is stored as a Windows Imaging Format (WIM) file that can be installed on a bare-metal computer by the manufacturer or at an enterprise staging center that is not connected to the Configuration Manager environment.  

     For more information, see [Create prestaged media](../deploy-use/create-prestaged-media.md).  

 When you create media, specify a password for the media to control access to the files that are contained on the media. If you specify a password, a user must be present to enter the password at the target computer when the task sequence is run.  

 When you run a task sequence by using media, the specified computer chip architecture contained on the media will not be recognized and the task sequence attempts to run even if the architecture specified does not match what is actually installed on the target computer. If the chip architecture contained on the media does not match the chip architecture installed on the target computer, the installation fails.  

 For more information about how to deploy operating systems by using media, see [Create task sequence media](../deploy-use/create-task-sequence-media.md).  
