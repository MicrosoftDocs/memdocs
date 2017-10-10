---
title: "Create and deploy an application"
titleSuffix: "Configuration Manager"
description: "Create and deploy an application containing a line-of-business app and learn how to manage apps effectively."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-app
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3bd1e487-ea18-43c1-b7c3-acbd9b86d429
caps.latest.revision: 15
caps.handback.revision: 0
author: mattbriggsms.author: mabrigg
manager: angrobe

---
# Create and deploy an application with System Center Configuration Manager*Applies to: System Center Configuration Manager (Current Branch)*
In this topic, you'll jump right in and create an application with System Center Configuration Manager. In this example, you'll create and deploy an application that contains a line-of-business app for Windows PCs called **Contoso.msi**, which must be installed on all PCs that are running Windows 10 in your company. Along the way, you'll learn about many of the things you can do to manage applications effectively.  

 This procedure is designed to give you an overview of how to create and deploy Configuration Manager applications. However, it does not cover all the configuration options, or how to create and deploy applications for other platforms.  

 For specific details that are relevant to each platform, see one of the following topics:  

-   [Create Windows applications](../../apps/get-started/creating-windows-applications.md)  
-   [Create iOS applications](../../apps/get-started/creating-ios-applications.md)  
-   [Create Android applications](../../apps/get-started/creating-android-applications.md)  
-   [Create Windows Phone applications](../../apps/get-started/creating-windows-phone-applications.md)  
-   [Create Mac computer applications](../../apps/get-started/creating-mac-computer-applications.md)  
-   [Create Linux and UNIX server applications](../../apps/get-started/creating-linux-and-unix-server-applications.md)
-   [Create Windows Embedded applications](../../apps/get-started/creating-windows-embedded-applications.md)


If you are already familiar with Configuration Manager applications, you can skip this topic. However, you might want to review [Create applications](../../apps/deploy-use/create-applications.md) to learn about all the options that are available when you create and deploy applications.  

## Before you start  

Make sure that you've reviewed the information in [Introduction to application management](/sccm/apps/understand/introduction-to-application-management) so that you have prepared your site to install applications and you understand the terminology that's used in this topic.  

 Also, make sure that the installation files for the **Contoso.msi** app are in an accessible location on your network.  

## Create the Configuration Manager application  

### To start the Create Application Wizard and create the application  

1.  In the Configuration Manager console, choose **Software Library** > **Application Management** > **Applications**.  

3.  On the **Home** tab, in the **Create** group, choose **Create Application**.  

4.  On the **General** page of the **Create Application Wizard**, choose **Automatically detect information about this application from installation files**. This pre-populates some of the information in the wizard with information that's extracted from the installation .msi file. Then specify the following information:  

    -   **Type**: Choose **Windows Installer (\*.msi file)**.  

    -   **Location**: Type the location (or choose **Browse** to select the location) of the installation file **Contoso.msi**. Note that the location must be specified in the form *\\\Server\Share\File* for Configuration Manager to locate the installation files.  

	You'll end up with something that looks like the following screenshot:  

	![App management wizard general page](/sccm/apps/get-started/media/App-management-wizard-general-page.png)  

5.  Choose **Next**. On the **Import Information** page, you'll see some information about the app and any associated files that were imported to Configuration Manager. Once you are done, choose **Next** again.  

6.  On the **General Information** page, you can supply further information about the application to help you sort and locate it in the Configuration Manager console.  

     Additionally, the **Installation program** field lets you specify the full command line that will be used to install the application on PCs. You can edit this to add your own properties (for example **/q** for an unattended installation).  

    > [!TIP]  
    >  Some of the fields on this page of the wizard might have been filled in automatically when you imported the application installation files.  

     You'll end up with a screen that looks similar to the following screenshot:  

     ![App management wizard general information page](/sccm/apps/get-started/media/App-management-wizard-general-information-page.png)  

7.  Choose **Next**. On the Summary page, you can confirm your application settings and then complete the wizard.  

 You've finished creating the app. To find it, in the **Software Library** workspace, expand **Application Management**, and then choose **Applications**. For this example, you'll see:  

 ![Final app graphic](/sccm/apps/get-started/media/Final-app-graphic.png)  

## Examine the properties of the application and its deployment type  

Now that you've created an application, you can refine the application settings if you need to. To look at the application properties, select the app, and then, in the **Home** tab in the **Properties** group, choose **Properties**.  

 In the **<Contoso\> Application Properties** dialog box, you'll see many items that you can configure to refine the behavior of the application. For details about all the settings you can configure, see [Create applications](../../apps/deploy-use/create-applications.md). For the purposes of this example, you'll just be changing some properties of the application's deployment type.  

 Choose the **Deployment Types** tab > **Contoso Application** deployment type > **Edit**. 	

You'll see a dialog box like this one:  

![App management app properties page](/sccm/apps/get-started/media/App-management-app-properties-page.png)  

## Add a requirement to the deployment type  
 Requirements specify conditions that must be met before an application is installed on a device.  You can choose from built-in requirements or you can create your own. In this example, you add a requirement that the application will only get installed on PCs that are running Windows 10.  

1.  From the deployment type properties page you just opened, choose the **Requirements** tab.  

2.  Choose **Add** to open the **Create Requirement** dialog box.  

3.  In the **Create Requirement** dialog box, specify the following information:  

    -   **Category**: **Device**  

    -   **Condition**: **Operating system**  

    -   **Rule type**: **Value**  

    -   **Operator**: **One of**  

    -   From the operating systems list, select **Windows 10**.  

    You'll end up with a dialog box that looks like this:  

    ![App management requirements page](/sccm/apps/get-started/media/App-management-requirements-page.png)  

4.  Choose **OK** to close each property page that you opened. Then return to the **Applications** list in the Configuration Manager console.  

> [!TIP]  
>  Requirements can help reduce the number of Configuration Manager collections you need. Because you just specified that the application can only get installed on PCs that are running Windows 10, you can later deploy this to a collection that contains PCs that run many different operating systems. But the application will only get installed on Windows 10 PCs.  

## Add the application content to a distribution point  

Next, to deploy the application to PCs, make sure that the application content is copied to a distribution point. PCs access the distribution point to install the application.  

> [!TIP]  
>  To find out more about distribution points and content management in Configuration Manager, see [Manage content and content infrastructure](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  

1.  In the Configuration Manager console, choose **Software Library**.  

2.  In the **Software Library** workspace, expand **Applications**. Then, in the list of applications, select the **Contoso Application** that you created.  

3.  On the **Home** tab, in the **Deployment** group, choose **Distribute Content**.  

4.  On the **General** page of the **Distribute Content Wizard**, check that the application name is correct, and then choose **Next**.  

5.  On the **Content** page, review the information that will be copied to the distribution point, and then choose **Next**.  

6.  On the **Content Destination** page, choose **Add** to select one or more distribution points, or distribution point groups on which to install the application content.  

7.  Complete the wizard.  

You can check that the application content was copied successfully to the distribution point from the **Monitoring** workspace, under **Distribution Status** > **Content Status**.  

## Deploy the application  

Next, deploy the application to a device collection in your hierarchy. In this example, you deploy the application to the **All Systems** device collection.  

> [!TIP]  
>  Remember that only Windows 10 computers will install the application because of the requirements that you selected earlier.  

1.  In the Configuration Manager console, choose **Software Library** > **Application Management** > **Applications**.  

3.  From the list of applications, select the application that you created earlier (**Contoso Application**), and then, on the **Home** tab in the **Deployment** group, choose **Deploy**.  

4.  On the **General** page of the **Deploy Software Wizard**, choose **Browse** to select the **All Systems** device collection.  

5.  On the **Content** page, check that the distribution point from which you want PCs to install the application is selected.  

6.  On the **Deployment Settings** page, make sure that the deployment action is set to **Install**, and the deployment purpose is set to **Required**.  

    > [!TIP]  
    >  By setting the deployment purpose to **Required**, you make sure that the application is installed on PCs that meet the requirements that you set. If you set this value to **Available**, then users can install the application on demand from Software Center.  

7.  On the **Scheduling** page, you can configure when the application will be installed. For this example, select **As soon as possible after the available time**.  

8.  On the **User Experience** page, choose **Next** to accept the default values.  

9. Complete the wizard.  

Use the information in the following **Monitor the application** section to see the status of your application deployment.  

## Monitor the application  
 In this section, you'll take a quick look at the deployment status of the application that you just deployed.  

### To review the deployment status  

1.  In the Configuration Manager console, choose **Monitoring** > **Deployments**.  

3.  From the list of deployments, select **Contoso Application**.  

4.  On the **Home** tab, in the **Deployment** group, choose **View Status**.  

5.  Select one of the following tabs to see more status updates about the application deployment:  

    -   **Success**: The application installed successfully on the indicated PCs.  

    -   **In Progress**: The application has not yet finished installing.  

    -   **Error**: An error occurred installing the application on the indicated PCs. Further information about the error is also displayed.  

    -   **Requirements Not Met**: No installation attempt was made on the indicated devices because they did not meet the requirements you configured (in this example, because they do not run on Windows 10).  

    -   **Unknown**: Configuration Manager was unable to report the status of the deployment. Check back again later.  

> [!TIP]  
>  There are a few ways you can monitor application deployments. For full details, see [Monitor applications](/sccm/apps/deploy-use/monitor-applications-from-the-console).  

## End-user experience  

Users who have PCs that are managed by Configuration Manager and running Windows 10 see a message telling them that they must install the Contoso application. Once they accept the installation, the application gets installed.  
