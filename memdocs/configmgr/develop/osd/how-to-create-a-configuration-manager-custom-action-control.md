---
title: "Create a Custom Action Control"
titleSuffix: "Configuration Manager"
description: "Learn how to create a custom action control in Configuration Manager."
ms.date: "09/20/2016"
ms.prod: "configuration-manager"
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 74d39782-37a9-4358-8e39-7be750a13f98
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: null
ms.collection: openauth


---
# How to Create a Configuration Manager Custom Action Control
In Configuration Manager, to create a custom action control, you create a Windows control by using the following two classes:  

|Class|Description|  
|-----------|-----------------|  
|SmsOsdEditorPageControl|The custom action control. You derive from this class to implement the custom action control that is displayed in the Task Sequence Editor.|  
|TaskSequenceOptionControl|The options control for the custom action. You derive from this class to create the custom action options page that is displayed in the Task Sequence Editor.|  

 These procedures show you how to create a Configuration Manager operating system deployment control assembly by using Visual Studio 2005. When it is loaded into the Task Sequence Editor, the control displays a property page that contains a text box that is used to set a user-name action variable for the custom action.  

 After you have completed these steps, perform the steps in the following topics to create the custom action managed object format (MOF) file and use the custom action control.  

 [How to Create a MOF File for a Configuration Manager Custom Action](../../develop/osd/how-to-create-a-mof-file-for-a-configuration-manager-custom-action.md)  

 [How to Use a Configuration Manager Custom Action](../../develop/osd/how-to-use-a-configuration-manager-custom-action-control.md)  

> [!NOTE]
>  For information about using the custom action as part of a deployment, see [About Configuration Manager Custom Action Client Applications](../../develop/osd/about-configuration-manager-custom-action-client-applications.md)  

## The Control Visual Studio Project  
 The following procedure creates the custom action control project.  

#### Create the control  

1.  In Visual Studio 2010, on the **File** menu, point to **New**, and then click **Project** to open the **New Project** dialog box.  

2.  From the list of **Visual C#**, **Windows** projects, select the **Windows Control Library** project template, and then type `ConfigMgrTSAction` in the **Name** box.  

3.  Click **OK** to create the Visual Studio project.  

4.  In **Solution Explorer**, right-click **UserControl1.cs**, click **Rename**, and then change the name to `ConfigMgrTSActionControl.cs`.  

5.  In **Solution Explorer**, right-click **References**, and then click **Add Reference**.  

6.  In the **Add Reference** dialog box, click the **Browse** tab, navigate to %*ProgramFiles*%\Microsoft Configuration Manager\AdminUI\bin, and then select the following assemblies:  

    -   **Adminui.osdcommon.dll**  

    -   **Adminui.tasksequenceeditor.dll**  

    -   **Adminui.wqlqueryengine.dll**  

    -   **Microsoft.configurationmanagement.exe**  

    -   **Microsoft.configurationmanagement.managementprovider.dll**  

7.  Click **OK** to add the assemblies as project references.  

8.  In **Solution Explorer**, right-click **ConfigMgrTSActionControl.cs**, and then click **View Code**.  

9. Add the following code to include the required namespaces:  

    ```  
    using Microsoft.ConfigurationManagement.AdminConsole;  
    using Microsoft.ConfigurationManagement.AdminConsole.TaskSequenceEditor;  
    ```  

10. Change the class **ConfigMgrTSActionControl** so that it derives from **SmsOsdEditorPageControl**.  

11. In **ConfigMgrTSActionControl.cs**, add the following new constructor to the **ConfigMgrTSActionControl** class:  

    ```  
    public ConfigMgrTSActionControl(SmsPageData data) : base(data)   
    {   
        InitializeComponent();   
    }  
    ```  

12. Add the following method to initialize the control:  

    ```  
    public override void InitializePageControl()  
    {  
       base.InitializePageControl();  
    }  
    ```  

## Create an Options Control  
 The following procedure creates the code that declares the options control for the custom action. This implementation uses the default options control.  

#### To create an options control  

-   At the end of **ConfigMgrTSActionControl.cs** add the following new class in the **ConfigMgrTSAction** namespace:  

    ```  
    public class ConfigureTSActionOptions : TaskSequenceOptionControl  
    {  
        public ConfigureTSActionOptions() : base()   
        {  
        }  
        public ConfigureTSActionOptions(SmsPageData data) : base(data)   
        {  
        }  
    }  

    ```  

## Customize the User Interface  
 The following procedure adds a text box and code to manage action data.  

#### To add the user interface  

1.  In **Solution Explorer**, right-click **ConfigMgrTSActionControl.cs**, and then click **View Designer**.  

2.  In the **Toolbox**, click the **Common Controls** tab, and then double-click **TextBox**. A button named `textBox1` is added to your control on the User Control Designer.  

3.  Double-click the text box. An event handler named `textBox1_TextChanged` is added to the class ConfigMgrTSActionControl. Add the following code to ensure that changes are saved to the action's property manager:  

    ```  
    SetDirtyFlag(true);  
    ```  

4.  In the class ConfigMgrTSActionControl, add the following method to write the text box value to the `User` property defined in the custom action MOF. This is called when the **OK** or **Apply** button is clicked.  

    ```  
    protected override bool ApplyChanges(out Control errorControl, out bool showError)  
    {  
        // You can check the error here and return false.  
        if (this.HasError(out errorControl) == true)  
        {  
            this.ShowMessageBox(  
                this.GetErrorString(),  
                "Error",  
                MessageBoxButtons.OK,  
                MessageBoxIcon.Warning);  
            errorControl = null;  
            showError = true;  
            return false;  
        }  
        this.PropertyManager["User"].StringValue = textBox1.Text;  

        return base.ApplyChanges(out errorControl, out showError);  
    }  
    ```  

5.  In the design view for the control, double-click the control to create the method **ConfigMgrTSActionControl_Load**.  

6.  Add the following code to the method. This code loads the text box with an existing User value. This happens when the task sequence action is edited after it is created.  

    ```  
    textBox1.Text = this.PropertyManager["User"].StringValue;  
    ```  

## Resource Strings  
 The following procedure adds the resource strings that are used to display the custom action name in the Task Sequence Editor.  

#### To add resource strings  

1.  In **Solution Explorer**, on the **Project** menu, click **Properties**.  

2.  Click the **Resources** tab. If the resources file does not exist, create it by selecting the message that is displayed on the **Resources** tab.  

3.  On the Resource Designer toolbar, point to the resource view drop-down, click the arrow, and make sure it is set to **Strings** (which is the default). A settings grid appears, displaying the strings that are maintained by that instance of the Resource Designer.  

4.  Click the **Name** column of the last row in the grid, which is marked with an asterisk (*).  

5.  In the **Name** column, enter `DefaultDisplay_ConfigMgrTSAction` as the string name.  

6.  In the **Value** column, enter the string **Custom Action**. This is the string displayed in the list of task sequence actions.  

7.  Click the **Name** column of the last row in the grid, which is marked with an asterisk (*).  

8.  In the **Name** column, enter `ConfigMgrTSAction` as the string name.  

9. In the **Value** column, enter `Custom Action`. This is the string that is displayed when you add the custom action.  

## Deploy the Assembly  
 This procedure builds and copies the assembly that you have created to the Configuration Manager console assemblies folder. For important information about deploying Configuration Manager console extensions, see [About Configuration Manager Administrator Console Extension Deployment](../../develop/core/servers/console/console-extension-deployment.md).  

#### To deploy the assembly  

1.  Build the project. Visual Studio creates the assembly as \Visual Studio 2005\Projects\ConfigMgrControl\ConfigMgrTSAction\bin\Debug\ConfigMgrTSActionControl.dll.  

2.  Copy the assembly to the folder %*ProgramFiles*%\Microsoft Configuration Manager\AdminUI\bin.  

## See Also  
 [About Configuration Manager Console Extension](../../develop/core/servers/console/about-configuration-manager-console-extension.md)   
 [Configuration Manager Console Extension Deployment](../../develop/core/servers/console/console-extension-deployment.md)   
 [How to Create a MOF File for a Configuration Manager Custom Action](../../develop/osd/how-to-create-a-mof-file-for-a-configuration-manager-custom-action.md)   
 [How to Use a Configuration Manager Custom Action](../../develop/osd/how-to-use-a-configuration-manager-custom-action-control.md)
