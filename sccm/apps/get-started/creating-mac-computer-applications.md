---
title: "Create Mac computer applications"
titleSuffix: "Configuration Manager"
description: "See which considerations you must take into account when you create and deploy applications for Mac computers."
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-app
ms.topic: conceptual
ms.assetid: ab1aecdd-d943-44f5-b0a9-e8fe7439e5d6
author: aczechowski
manager: dougeby
ms.author: aaroncz
---
# Create Mac computer applications with System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
Keep the following considerations in mind when you create and deploy applications for Mac computers.  

> [!IMPORTANT]  
>  The procedures in this topic cover information about deploying applications to Mac computers on which you installed the Configuration Manager client. Mac computers that you enrolled with Microsoft Intune do not support application deployment.  

## General considerations  
 You can use System Center Configuration Manager to deploy applications to Mac computers that run the Configuration Manager Mac client. The steps to deploy software to Mac computers are similar to the steps to deploy software to Windows computers. However, before you create and deploy applications for Mac computers that are managed by Configuration Manager, consider the following:  

-   Before you can deploy Mac application packages to Mac computers, you must use the **CMAppUtil** tool on a Mac computer to convert these applications into a format that can be read by Configuration Manager.  

-   Configuration Manager does not support the deployment of Mac applications to users. Instead, these deployments must be made to a device. Similarly, for Mac application deployments, Configuration Manager does not support the **Pre-deploy software to the user’s primary device** option on the **Deployment Settings** page of the **Deploy Software Wizard**.  

-   Mac applications support simulated deployments.  

-   You cannot deploy applications to Mac computers that have a purpose of **Available**.  

-   The option to send wake-up packets when you deploy software is not supported for Mac computers.  

-   Mac computers do not support Background Intelligent Transfer Service (BITS) for downloading application content. If an application download fails, it is restarted from the beginning.  

-   Configuration Manager does not support global conditions when you create deployment types for Mac computers.  

## Steps to create and deploy an application  
 The following table provides the steps, details, and information for creating and deploying applications for Mac computers.  

|Step|Details|  
|----------|-------------|  
|**Step 1**: Prepare Mac applications for Configuration Manager|Before you can create Configuration Manager applications from Mac software packages, you must use the **CMAppUtil** tool on a Mac computer to convert the Mac software into a Configuration Manager**.cmmac** file.|  
|**Step 2**: Create a Configuration Manager application that contains the Mac software|Use the **Create Application Wizard** to create an application for the Mac software.|  
|**Step 3**: Create a deployment type for the Mac application|This step is required only if you did not automatically import this information from the application.|  
|**Step 4**: Deploy the Mac application|Use the **Deploy Software Wizard** to deploy the application to Mac computers.|  
|**Step 5**: Monitor the deployment of the Mac application|Monitor the success of application deployments to Mac computers.|  

## Supplemental procedures to create and deploy applications for Mac computers  
 Use the following procedures to create and deploy applications for Mac computers that are managed by Configuration Manager.  

###  Step 1: Prepare Mac applications for Configuration Manager  
 The process for creating and deploying Configuration Manager applications to Mac computers is similar to the deployment process for Windows computers. However, before you create Configuration Manager applications that contain Mac deployment types, you must prepare the applications by using the **CMAppUtil** tool. This tool is downloaded with the Mac client installation files. The **CMAppUtil** tool can gather information about the application, which includes detection data from the following Mac packages:  

-   Apple Disk Image (.dmg)  

-   Meta Package File (.mpkg)  

-   Mac OS X Installer Package (.pkg)  

-   Mac OS X Application (.app)  

After it gathers application information, the **CMAppUtil** then creates a file with the extension **.cmmac**. This file contains the installation files for the Mac software and information about detection methods that can be used to evaluate whether the application is already installed. **CMAppUtil** can also process **.dmg** files that contain multiple Mac applications and create different deployment types for each application.  

1.  Copy the Mac software installation package to the folder on the Mac computer where you extracted the contents of the **macclient.dmg** file that you downloaded from the Microsoft Download Center.  

2.  On the same Mac computer, open a terminal window and navigate to the folder where you extracted the contents of the **macclient.dmg** file.  

3.  Navigate to the **Tools** folder and type the following command-line command:  

     **./CMAppUtil** *<properties\>*  

     For example, say you want to convert the contents of an Apple disk image file named **MySoftware.dmg** that's stored in the user's desktop folder into a **cmmac** file in the same folder. You also want to create **cmmac** files for all applications that are found in the disk image file. To do this, use the following command line:  

     **./CMApputil –c /Users/** *<User Name\>* **/Desktop/MySoftware.dmg -o /Users/** *<User Name\>* **/Desktop -a**  

    > [!NOTE]  
    >  The application name can't be more than 128 characters.  

     To configure options for **CMAppUtil**, use the command-line properties in the following table:  

    |Property|More information|  
    |--------------|----------------------|  
    |**-h**|Displays the available command-line properties.|  
    |**-r**|Outputs the **detection.xml** of the provided **.cmmac** file to **stdout**. The output contains the detection parameters and the version of **CMAppUtil** that was used to create the **.cmmac** file.|  
    |**-c**|Specifies the source file to be converted.|  
    |**-o**|Specifies the output path in conjunction with the –c property.|  
    |**-a**|Automatically creates .cmmac files in conjunction with the –c property for all applications and packages in the disk image file.|  
    |**-s**|Skips generating the **detection.xml** if no detection parameters are found and forces the creation of the **.cmmac** file without the **detection.xml** file.|  
    |**-v**|Displays more detailed output from the **CMAppUtil** tool together with diagnostic information.|  

4.  Ensure that the **.cmmac** file has been created in the output folder that you specified.  

###  Create a Configuration Manager application that contains the Mac software  

Use the following procedure to help you create an application for Mac computers that are managed by Configuration Manager.  

1.  In the Configuration Manager console, choose **Software Library** > **Application Management** > **Applications**.  

3.  On the **Home** tab, in the **Create** group, choose **Create Application**.  

4.  On the **General** page of the **Create Application Wizard**, select **Automatically detect information about this application from installation files**.  

    > [!NOTE]  
    >  If you want to specify information about the application yourself, select **Manually specify the application information**. For more information about how to manually specify the information, see [How to create applications with System Center Configuration Manager](../../apps/deploy-use/create-applications.md).  

5.  In the **Type** drop-down list, select **Mac OS X**.  

6.  In the **Location** field, specify the UNC path in the form *\\\\<server\>\\<share\>\\<filename\>* to the Mac application installation file (**.cmmac** file) that will detect application information. Alternatively, choose **Browse** to browse to and specify the installation file location.  

    > [!NOTE]  
    >  You must have access to the UNC path that contains the application.  

7.  Choose **Next**.  

8.  On the **Import Information** page of the **Create Application Wizard**, review the information that was imported. If necessary, you can choose **Previous** to go back and correct any errors. Choose **Next** to proceed.  

9. On the **General Information** page of the **Create Application Wizard**, specify information about the application such as the application name, comments, version, and an optional reference to help you reference the application in the Configuration Manager console.  

    > [!NOTE]  
    >  Some of the application information might already be on this page if it was previously obtained from the application installation files.  

10. Choose **Next**, review the application information on the **Summary** page, and then complete the **Create Application Wizard**.  

11. The new application is displayed in the **Applications** node of the Configuration Manager console.  

###  Step 3: Create a deployment type for the Mac application  
 Use the following procedure to help you create a deployment type for Mac computers that are managed by Configuration Manager.  

> [!NOTE]  
>  If you automatically imported information about the application in the **Create Application Wizard**, a deployment type for the application might already have been created.  

1.  In the Configuration Manager console, choose **Software Library** > **Application Management** > **Applications**.  

3.  Select an application. Then, on the **Home** tab, in the **Application** group, choose **Create Deployment Type** to create a new deployment type for this application.  

    > [!NOTE]  
    >  You can also start the **Create Deployment Type Wizard** from the **Create Application Wizard** and from the **Deployment Types** tab of the *<application name\>* **Properties** dialog box.  

4.  On the **General** page of the **Create Deployment Type Wizard**, in the **Type** drop-down list, select **Mac OS X**.  

5.  In the **Location** field, specify the UNC path in the form \\\\<server\>\\<share\>\\<filename\> to the application installation file (**.cmmac** file). Alternatively, choose **Browse** to browse to and specify the installation file location.  

    > [!NOTE]  
    >  You must have access to the UNC path that contains the application.  

6.  Choose **Next**.  

7.  On the **Import Information** page of the **Create Deployment Type Wizard**, review the information that was imported. If necessary, choose **Previous** to go back and correct any errors. Choose **Next** to continue.  

8.  On the **General Information** page of the **Create Deployment Type Wizard**, specify information about the application such as the application name, comments, and the languages in which the deployment type is available.  

    > [!NOTE]  
    >  Some of the deployment type information might already be on this page if it was previously obtained from the application installation files.  

9. Choose **Next**.  

10. On the **Requirements** page of the **Create Deployment Type Wizard**, you can specify the conditions that must be met before the deployment type can be installed on Mac computers.  

11. Choose **Add** to open the **Create Requirement** dialog box and add a new requirement.  

    > [!NOTE]  
    >  You can also add new requirements on the **Requirements** tab of the *<deployment type name\>* **Properties** dialog box.  

12. From the **Category** drop-down list, select that this requirement is for a device.  

13. From the **Condition** drop-down list, select the condition that you want to use to assess whether the Mac computer meets the installation requirements. The contents of this list varies depending on the category that you select.  

14. From the **Operator** drop-down list, choose the operator to use to compare the selected condition to the specified value to assess whether the user or device meets the installation requirements. The available operators vary depending on the selected condition.  

15. In the **Value** field, specify the values to use with the selected condition and operator to assess whether the user or device meets in the installation requirement. The available values vary depending on the condition and operator that you select.

16. Choose **OK** to save the requirement rule and exit the **Create Requirement** dialog box.  

17. On the **Requirements** page of the **Create Deployment Type Wizard**, choose **Next**.  

18. On the **Summary** page of the **Create Deployment Type Wizard**, review the actions for the wizard to take.  If necessary, choose **Previous** to go back and change deployment type settings. Choose **Next** to create the deployment type.  

19. After the **Progress** page finishes, review the actions that have been taken, and then choose **Close** to complete the **Create Deployment Type Wizard**.  

20. If you started this wizard from the **Create Application Wizard**, you will return to the **Deployment Types** page.  

###  Deploy the Mac application  
 The steps to deploy an application to Mac computers are the same as the steps to deploy an application to Windows computers, except for the following differences:  

-   The deployment of applications to users is not supported.  

-   Deployments that have a purpose of **Available** are not supported.  

-   The **Pre-deploy software to the user’s primary device** option on the **Deployment Settings** page of the **Deploy Software Wizard** is not supported.  

-   Because Mac computers do not support Software Center, the setting **User notifications** on the **User Experience** page of the **Deploy Software Wizard** is ignored.  

-   The option to send wake-up packets when you deploy software is not supported for Mac computers.  

> [!NOTE]  
>  You can build a collection that contains only Mac computers. To do so, create a collection that uses a query rule and use the example WQL query in the [How to create queries](../../core/servers/manage/create-queries.md) topic.  

 For more information, see [Deploy applications](../../apps/deploy-use/deploy-applications.md).  

###  Step 5: Monitor the deployment of the Mac application  
 You can use the same process to monitor application deployments to Mac computers as you would to monitor application deployments to Windows computers.  

 For more information, see [Monitor applications](/sccm/apps/deploy-use/monitor-applications-from-the-console).  
