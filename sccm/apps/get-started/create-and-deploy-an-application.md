---
title: "Create and deploy an application | System Center Configuration Manager"
ms.custom: na
ms.date: 12/08/2015
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
author: robstackmsft

---
# Create and deploy an application with System Center Configuration Manager
In this topic, you'll jump right in and create an application with System Center Configuration Manager. In this example, you'll create and deploy an application that contains a line of business app for Windows PCs called **Contoso.msi** which must be installed on all PCs running Windows 10 in your company. Along the way, you'll learn about many of the things you can do to help you manage applications effectively.  
  
 This procedure is designed to give you an overview of how to create and deploy Configuration Manager applications. However, it does not cover every option you can configure, or how to create and deploy applications for other platforms.  
  
 For specific details relevant to each platform, see one of the following topics:  
  
-   [Create Windows applications](../../apps/get-started/creating-windows-applications.md)  
  
-   [Create iOS applications](../../apps/get-started/creating-ios-applications.md)  
  
-   [Create Android applications](../../apps/get-started/creating-android-applications.md)  
  
-   [Create Windows Phone applications](../../apps/get-started/creating-windows-phone-applications.md)  
  
-   [Create Mac computer applications](../../apps/get-started/creating-mac-computer-applications.md)  
  
-   [Create Linux and UNIX server applications](../../apps/get-started/creating-linux-and-unix-server-applications.md)  
  
If you are already familiar with Configuration Manager applications, you can skip this topic. However, you might want to review [How to create applications](../../apps/deploy-use/create-applications.md) to learn about all the options available when you create and deploy applications.  
  
## Create and deploy the application  
 Use the information in the following sections to create, deploy, and monitor the **Contoso.msi** application for all Windows 10 PCs in your site.  
  
### Before you start  
 Ensure you have reviewed the information in [Get started with application management in System Center Configuration Manager](../../apps/understand/get-started-with-application-management.md) so that you have prepared your site to install applications and you understand the terminology used in this topic.  
  
 Also, ensure that the installation files for the **Contoso.msi** app are in an accessible location on your network.  
  
### Create the Configuration Manager application  
  
##### How to start the create application wizard and create the application  
  
1.  In the Configuration Manager console, click **Software Library**.  
  
2.  In the **Software Library** workspace, expand **Application Management**, and then click **Applications**.  
  
3.  On the **Home** tab, in the **Create** group, click **Create Application**.  
  
4.  On the **General** page of the **Create Application wizard**, choose to **Automatically detect information about this application from installation files**. This will pre-populate some of the information in the wizard with information extracted from the installation .msi file, then specify the following information:  
  
    -   **Type** - Choose **Windows Installer (\*.msi file)**  
  
    -   **Location** - Enter the location (or click **Browse** to select the location) of the installation file **Contoso.msi**. Note that the location must be specified in the form *\\\Server\Share\File* in order for Configuration Manager to locate the installation files.  
  
         You'll end up with something looking like the following screenshot:  
  
         ![App management wizard general page](../../apps/get-started/media/App-management-wizard-general-page.png "App)  
  
5.  Click **Next**. On the **Import Information** page of the wizard, you'll see some information about the app and any associated files that were imported to Configuration Manager. Once you are done, click **Next** again.  
  
6.  On the **General Information** page of the wizard, you can supply further information about the application to help you sort and locate it in the Configuration Manager console.  
  
     Additionally, the Installation program field lets you specify the full command line that will be used to install the application on PCs. You can edit this to add your own properties (for example **/q** for an unattended install).  
  
    > [!TIP]  
    >  Some of the fields on this page of the wizard might have been filled in automatically when you imported the application installation files.  
  
     You'll end up with a screen that looks similar to the screenshot below:  
  
     ![App management wizard general information page](../../apps/get-started/media/App-management-wizard-general-information-page.png "App)  
  
7.  Click **Next**. On the Summary page of the wizard, you can confirm your application settings, then complete the wizard.  
  
 You've finished creating the app. To find it, in the **Software Library** workspace, expand **Application Management**, and then click **Applications**. For this example, you'll see:  
  
 ![Final app graphic](../../apps/get-started/media/Final-app-graphic.png "Final)  
  
### Examine the properties of the application and its deployment type  
 Now that you've created an application, you can refine the application settings if required. To look at the application properties, select the app, and then, in the **Home** tab, in the **Properties** group, click **Properties**.  
  
 In the **<Contoso\> Application Properties** dialog box, you'll see many items that you can configure to fine-tune the behavior of the application. For details about all the settings you can configure, see [How to create applications with System Center Configuration Manager](../../apps/deploy-use/create-applications.md). For the purposes of this example, you'll just be changing some properties of the application's deployment type.  
  
 Click the **Deployment Types** tab, select the **Contoso Application** deployment type, and then click **Edit**. You'll see a dialog box like this one:  
  
 ![App management app properties page](../../apps/get-started/media/App-management-app-properties-page.png "App)  
  
### Add a requirement to the deployment type  
 Requirements specify conditions that must be met before an application is installed on a device.  You can choose from built-in requirements, or create your own. In this example, you will add a requirement that the application will only install on PCs running Windows 10.  
  
##### To add the requirement  
  
1.  From the deployment type properties page you just opened, click the **Requirements** tab.  
  
2.  Click **Add** to open the **Create Requirement** dialog box.  
  
3.  In the **Create Requirement** dialog box, specify the following information:  
  
    -   **Category** - **Device**  
  
    -   **Condition** - **Operating system**  
  
    -   **Rule type** - **Value**  
  
    -   **Operator** - **One of**  
  
    -   From the operating systems list, select **Windows 10**.  
  
     You'll end up with a dialog box that looks like this:  
  
     ![App management requirements page](/sccm/apps/get-started/media/App-management-requirements-page.png)  
  
4.  Click **OK** to close each property page you opened, and return to the **Applications** list in the Configuration Manager console.  
  
> [!TIP]  
>  Requirements can help reduce the number of Configuration Manager collections you need. Because you just specified that the application can only install on PCs running Windows 10, you can later deploy this to a collection that contains PCs that run many different operating systems, and the application will only install on Windows 10 PCs.  
  
### Add the application content to a distribution point  
 To successfully deploy the application to PCs, you must next ensure that the application content is copied to a distribution point. PCs will access the distribution point to install the application.  
  
> [!TIP]  
>  To find out more about distribution points and content management in Configuration Manager, see [Manage content and content infrastructure for System Center Configuration Manager](../../core/servers/deploy/configure/manage-content-and-content-infrastructure.md).  
  
##### To copy the application content to a distribution point  
  
1.  In the Configuration Manager console, click **Software Library**.  
  
2.  In the **Software Library** workspace, expand **Applications** and then, in the list of applications, select the **Contoso Application** that you created.  
  
3.  On the **Home** tab, in the **Deployment** group, click **Distribute Content**.  
  
4.  On the **General** page of the **Distribute Content Wizard**, check that the application name is correct, and then click **Next**.  
  
5.  On the **Content** page, review the information that will be copied to the distribution point, and then click **Next**.  
  
6.  On the **Content Destination** page, click add to select one or more distribution points, or distribution point groups on which to install the application content.  
  
7.  Complete the wizard.  
  
 You can check that the application content copied successfully to the distribution point from the **Monitoring** workspace under **Distribution Status** > **Content Status**.  
  
### Deploy the application  
 Next, deploy the application to a device collection in your hierarchy. For this example, you'll deploy the application to the **All Systems** device collection.  
  
> [!TIP]  
>  Remember that only Windows 10 computers will install the application because of the requirements you selected earlier.  
  
##### To deploy the application  
  
1.  In the Configuration Manager console, click **Software Library**.  
  
2.  In the **Software Library** workspace, expand **Application Management**, and then click Applications.  
  
3.  From the list of applications, select the application you created earlier, **Contoso Application**, and then, on the **Home** tab, in the **Deployment** group, click **Deploy**.  
  
4.  On the **General** page of the **Deploy Software Wizard**, click **Browse** to select the **All Systems** device collection.  
  
5.  On the **Content** page of the wizard, check that the distribution point from which you want PCs to install the application is selected.  
  
6.  On the **Deployment Settings** page of the wizard, ensure that the deployment action is set to **Install**, and the deployment purpose is set to **Required**.  
  
    > [!TIP]  
    >  By setting the deployment purpose to **Required**, you ensure that the application is installed on PCs that meet the requirements you set. If you set this value to **Available**, then users can install the application on demand from Software Center.  
  
7.  On the **Scheduling** page, you can configure when the application will be installed. For this example, select **As soon as possible after the available time**.  
  
8.  On the **User Experience** page of the wizard, click **Next** to accept the default values.  
  
9. Complete the wizard.  
  
 Use the information in the **Monitor the application** section below to see the status of your application deployment.  
  
### Monitor the application  
 In this section, you'll take a quick look at the deployment status of the application you just deployed.  
  
##### To review the deployment status  
  
1.  In the Configuration Manager console, click **Monitoring**.  
  
2.  In the **Monitoring** workspace, click **Deployments**.  
  
3.  From the list of deployments, select **Contoso Application**.  
  
4.  On the **Home** tab, in the **Deployment** group, click **View Status**.  
  
5.  Select one of the following tabs to see more status about the application deployment:  
  
    -   **Success** - The application installed successfully on the indicated PCs.  
  
    -   **In Progress** - The application has not yet finished installing.  
  
    -   **Error** - An error occurred installing the application on the indicated PCs. Further information about the error is also displayed.  
  
    -   **Requirements Not Met** - The application did not attempt to install on the indicated devices because they did not meet the requirements you configured (in this example, because they do not run Windows 10).  
  
    -   **Unknown** - Configuration Manager was unable to report the status of the deployment. Check back again later.  
  
> [!TIP]  
>  There are a few ways you can monitor application deployments. For full details, see [Monitor applications with System Center Configuration Manager](../Topic/Monitor%20applications%20with%20System%20Center%20Configuration%20Manager.md).  
  
### End user experience  
 Users who have PCs running Windows 10 managed by Configuration Manager will shortly see a message telling them that they must install the Contoso application. Once they accept the installation, the application will be installed.  
  
## See Also  
 [Deploy and manage applications with System Center Configuration Manager](../Topic/Deploy%20and%20manage%20applications%20with%20System%20Center%20Configuration%20Manager.md)

