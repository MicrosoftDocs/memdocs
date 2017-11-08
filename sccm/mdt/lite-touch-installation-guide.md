---

title: "Quick Start - Lite Touch Installation"
titleSuffix: "Microsoft Deployment Toolkit"
description: "A Quick Start guiide for Microsoft Deployment Toolkit lite touch installation."
ms.date:  09/09/2016
ms.prod: configuration-manager
ms.technology:
  - mdt
ms.topic: article
ms.assetid:  21bedd68-e925-46e0-a540-df8c0aba2d6c

author: brenduns  
ms.author: angrobe  
manager: angrobe

---



## Quick Start Guide for Lite Touch Installation  
 Microsoft Deployment Toolkit (MDT) 2013 provides technology for deploying Windows operating systems, and Microsoft Office. This guide helps you quickly evaluate MDT 2013 by providing condensed, step-by-step instructions for using it to install the Windows 8.1 operating system through Lite Touch Installation (LTI) using bootable media (DVD or USB flash drive). This guide demonstrates how to perform the New Computer deployment scenario using an MDT 2013 deployment share. The New Computer deployment scenario covers the deployment of Windows 8.1 to a new computer. This scenario assumes that there is no user data or profile to preserve.  

> [!NOTE]
>  In this document, *Windows* applies to the Windows 8.1, Windows 8, Windows 7, Windows Server® 2012 R2, Windows Server 2012, and Windows Server 2008 R2 operating systems unless otherwise noted. MDT does not support ARM processor–based versions of Windows. Similarly, *MDT* refers to MDT 2013 unless otherwise stated.  

 After using this guide to evaluate MDT, review the rest of the MDT guidance to learn more about the technology’s advanced features.  

## Prerequisites  
 To deploy operating systems and applications using MDT, the environment must meet the following software and computer configuration prerequisites.  

### Required Software  
 To complete this guide, the following software is required:  

-   Windows 8.1  

     If you decide to complete this guide on an operating system other than Windows 8.1, MDT requires the following elements:  

    -   Microsoft .NET Framework version 3.5 with Service Pack 1  

    -   Windows PowerShell™ version 2.0  

     Windows 8.1 includes these features.  

-   Windows Assessment and Deployment Kit (Windows ADK) for Windows 8.1  

-   Networking services, including Domain Name System and Dynamic Host Configuration Protocol  

> [!NOTE]
>  The Task Sequencer used in MDT deployments requires that the Create Global Object right be assigned to credentials used to access and run the Deployment Workbench and the deployment process. This right is normally available to accounts with Administrator-level permissions (unless explicitly removed). Also, the Specialized Security – Limited Functionality (SSLF) security profile removes the Create Global Object right and should not be applied to computers being deployed using MDT until the MDT process is complete.  

### Computer Configuration  
 To complete this guide, set up the computers listed in the following table. These computers can be either physical computers or virtual machines (VMs) with the system resources designated.  


|**Computer name**|**Description**|  
|-|-|  
|WDG-MDT-01|This computer runs MDT and Windows 8.1 and is installed in a domain named *mdt2013.corp.woodgrovebank.com* with a network basic input/output system (NetBIOS) name of *MDT2013*. The system resources of the computer are:<br /><br /> -   Processor running at 1.4 gigahertz (GHz) or faster.<br />-   1 gigabyte (GB) or greater physical memory.<br />-   One disk partition that has 16 GB or more available disk space that will become the drive C partition.<br />-   One CD-ROM or DVD-ROM drive that will be assigned the drive letter D.|  
|WDG-REF-01|This is the reference computer and runs no current operating system. The system resources of the computer are:<br /><br /> -   Processor running at 1.4 GHz or faster.<br />-   1 GB or more of physical memory.<br />-   16 GB or more of available disk space.|  
|WDG-CLI-01|This is the target computer and runs no current operating system. The system resources of the computer are:<br /><br /> -   Processor running at 1.4 GHz or faster.<br />-   1 GB or more of physical memory.<br />-   16 GB or more of available disk space.|  

> [!NOTE]
>  This guide assumes that you are evaluating MDT on 64-bit (x64) physical or virtual computers. If evaluating MDT on 32-bit (x86) platforms, download and install the x86 editions of MDT and the components that this guide describes.  

## Step 1: Obtain the Required Software  
 This guide assumes that the 64-bit version of Windows 8.1 is installed on a computer named *WDG-MDT-01*. If the computer you are using has a different name, substitute the name of that computer for *WDG-MDT-01*.  

> [!NOTE]
>  This section assumes that you are creating a new infrastructure for MDT.  

 The following software is required to perform LTI deployments:  

-   MDT 2013  

-   Windows ADK for Windows 8.1  

-   Windows 8.1 distribution files  

-   Device drivers required for the target computer, WDG-CLI-01  

-   Device drivers required for the reference computer, WDG-REF-01  

## Step 2: Prepare the MDT Environment  
 In this step, you prepare the MDT environment prior to creating the reference computer and deploying a captured image of the reference computer to the target computer (WDG-CLI-01).  

 Prepare the MDT environment by:  

-   Installing MDT as described in [Step 2-1: Install MDT](#InstallMDT)  

-   Installing Windows ADK as described in [Step 2-2: Install Windows ADK](#InstallWindowsADK)  

###  <a name="InstallMDT"></a> Step 2-1: Install MDT  
 To install MDT, complete the following steps:  

1.  Double-click **MicrosoftDeploymentToolkit2013_x64.msi** (for 64-bit operating systems) or **MicrosoftDeploymentToolkit2013_x86.msi** (for 32-bit operating systems), and then click **Install**.  

     The Microsoft Deployment Toolkit 2013 Setup Wizard starts.  

2.  Complete the Microsoft Deployment Toolkit 2013 Setup Wizard using the following information. Accept the default values unless otherwise specified.  

    |**On this wizard page**|**Do this**|  
    |-|-|  
    |**Welcome to the Microsoft Deployment Toolkit 2013 Setup Wizard**|Click **Next**.|  
    |**End-User License Agreement**|Click **I accept the terms in the License Agreement**, and then click **Next**.|  
    |**Custom Setup**|Click **Next**.|  
    |**Ready to install Microsoft Deployment Toolkit 2013**|Click **Install**.|  
    |**Installing Microsoft Deployment Toolkit 2013**|The progress for installing MDT is displayed.|  
    |**Completing the Microsoft Deployment Toolkit 2013 Setup Wizard**|Click **Finish**.|  

 The Microsoft Deployment Toolkit 2013 Setup Wizard finishes, and MDT is installed on WDG-MDT-01.  

###  <a name="InstallWindowsADK"></a> Step 2-2: Install Windows ADK  
 To install Windows ADK, perform the following steps:  

1.  Mount the Windows ADK distribution files on a physical or virtual CD-ROM drive.  

2.  In Windows Explorer, go to the root of the CD-ROM drive, and then double-click **adksetup.exe**.  

     The Assessment and Deployment Kit Setup Wizard starts.  

3.  Complete the Assessment and Deployment Kit Setup Wizard using the following information.

    |**On this wizard page**|**Do this**|  
    |-|-|  
    |**Specify Location**|Click **Next**.|  
    |**Join the Customer Experience Improvement Program (CEIP)**|Click **Yes** if you want to participate or **No** if not. Then, click **Next**.|  
    |**License Agreement**|Click **Accept**.|  
    |**Select the features you want to install**|Ensure that only the check boxes for the following features are selected, and then click **Next**:<br /><br /> -   Deployment Tools<br />-   Windows Preinstallation Environment (Windows PE)<br />-   Windows User State Migration Tool **Note:**  MDT does not require the other features, but they can be installed, if desired.|  
    |**Installing features**|The progress for installing the features is displayed.|  
    |**Welcome to the Assessment and Deployment Kit**|Click **Close**.|  

4.  Click **Start**, and then point to **All Programs**. Point to **Microsoft Deployment Toolkit**, and then click **Deployment Workbench**.  

5.  Close all open windows.  

> [!NOTE]
>  After installing Windows ADK, log off, and then log on again to the computer so that the PATH environment variable is updated to include the %Program Files%\Windows Imaging folder.  

## Step 3: Configure MDT to Create the Reference Computer  
 When you have prepared the MDT environment, create the reference computer. The reference computer is the template for deploying new images to the target computers. Configure this computer exactly as the target computers will be configured. You will deploy Windows 8.1 to the reference computer (WDG-REF-01), capture an image of the reference computer, and then deploy the captured image to the target computer (WDG-CLI-01).  

 Configure MDT to create a reference computer by:  

-   Creating an MDT deployment share as described in [Step 3-1: Create an MDT Deployment Share](#CreateMDTDeployShare)  

-   Adding operating system files to the deployment share as described in [Step 3-2: Add Operating System Files to the Deployment Share](#AddOSFilestoDeployShare)  

-   Adding device drivers to the deployment share as described in [Step 3-3: Add Device Drivers to the Deployment Share](#AddDriverstoDeployShare)  

-   Creating a task sequence for the reference computer as described in [Step 3-4: Create a Task Sequence for the Reference Computer](#CreateTaskSequence)  

-   Enabling monitoring of the LTI deployment process as described in [Step 3-5: Enable LTI Deployment Process Monitoring](#EnableLTIDeployMonitor)  

-   Updating the deployment share as described in [Step 3-6: Update the Deployment Share](#UpdateDeployShare)  

###  <a name="CreateMDTDeployShare"></a> Step 3-1: Create an MDT Deployment Share  
 Before deployment can begin, create an MDT deployment share in the Deployment Workbench. This deployment share is the repository for the operating system images, language packs, applications, device drivers, and other software deployed to the target computers.  

 **To create a deployment share in the Deployment Workbench**  

1.  Click **Start**, and then point to **All Programs**. Point to **Microsoft Deployment Toolkit**, and then click **Deployment Workbench**.  

2.  In the Deployment Workbench console tree, go to Deployment Workbench/Deployment Shares.  

3.  In the Actions pane, click **New Deployment Shares**.  

     The New Deployment Share Wizard starts.  

4.  Complete the New Deployment Share Wizard using the following information.

    |**On this wizard page**|**Do this**|  
    |-|-|  
    |**Path**|In **Deployment share path**, type **C:\DeploymentShare$**, and then click **Next**.|  
    |**Share**|Click **Next**.|  
    |**Descriptive Name**|Click **Next**.|  
    |**Options**|Click **Next**.|  
    |**Summary**|Click **Next**.|  
    |**Progress**|The progress for creating the deployment share is displayed.|  
    |**Confirmation**|Click **Finish**.|  

 The New Deployment Share Wizard finishes, and the new deployment share—MDT Deployment Share (C:\DeploymentShare$)—appears in the details pane.  

###  <a name="AddOSFilestoDeployShare"></a> Step 3-2: Add Operating System Files to the Deployment Share  
 MDT acts as a repository for the operating system files deployed to the reference computer (WDG-REF-01) and target computer (WDG-CLI-01). Add the operating system in the Operating Systems node in the Deployment Workbench using the Import Operating System Wizard.  

 **To add the Windows 8.1 operating system files to the deployment share**  

1.  Click **Start**, and then point to **All Programs**. Point to **Microsoft Deployment Toolkit**, and then click **Deployment Workbench**.  

2.  In the Deployment Workbench console tree, go to Deployment Workbench/Deployment Shares/MDT Deployment Share (C:\DeploymentShare$)/Operating Systems.  

3.  In the Actions pane, click **Import Operating System**.  

     The Import Operating System Wizard starts.  

4.  Complete the Import Operating System Wizard using the following information.    

    |**On this wizard page**|**Do this**|  
    |-|-|  
    |**On this wizard page**|**Do this**|  
    |**OS Type**|Click **Full set of source files**, and then click **Next**.|  
    |**Source**|In **Source directory**, type ***source_path*** (where *source_path* is the fully qualified path to the Windows 8.1 distribution files), and then click **Next**.|  
    |**Destination**|Click **Next**.|  
    |**Summary**|Click **Next**.|  
    |**Progress**|The progress for importing the operating system is displayed.|  
    |**Confirmation**|Click **Finish**.|  

 The Import Operating System Wizard finishes. Windows 8.1 is added to the list of operating systems in the details pane and copied to the *deployment_share*\Operating Systems\\*operating_system* folder (where *deployment_share* is the shared network folder you created earlier in the process and *operating_system* is the name of the operating system you added to the deployment share).  

###  <a name="AddDriverstoDeployShare"></a> Step 3-3: Add Device Drivers to the Deployment Share  
 After you have added Windows 8.1 to the Deployment Workbench, add any device drivers required for the reference computer (WDG-REF-01) and the target computer (WDG-CLI-01). These device drivers will be added to Windows PE and deployed with Windows 8.1. Add the device drivers in the Out-of-box Drivers node in the Deployment Workbench by using the New Driver Wizard, which copies the device driver files to the deployment share in Out-of-Box Drivers\\*device_driver* (where *device_driver* is the name of the device driver you added to the deployment share).  

> [!NOTE]
>  If the device drivers for the reference computer (WDG-REF-01) and the target computer (WDG-CLI-01) are included with Windows 8.1, skip this step and proceed with the following step.  

 **To add the device drivers for the reference and target computers to the distribution share**  

1.  Click **Start**, and then point to **All Programs**. Point to **Microsoft Deployment Toolkit**, and then click **Deployment Workbench**.  

2.  In the Deployment Workbench console tree, go to Deployment Workbench/Deployment Shares/MDT Deployment Share (C:\DeploymentShare$)/Out-of-Box Drivers.  

3.  In the Actions pane, click **Import Drivers**.  

     The Import Driver Wizard starts.  

4.  Complete the Import Driver Wizard using the following information.

    |**On this wizard page**|**Do this**|
    |-|-|  
    |**Specify Directory**|In **Driver source directory**, type ***driver_path*** (where *driver_path* is the fully qualified path to the folder containing the device drivers), and then click **Next**.|  
    |**Summary**|Click **Next**.|  
    |Progress|The progress for importing the device drivers is displayed.|  
    |**Confirmation**|Click **Finish**.|  

 The Import Driver Wizard finishes. The device drivers are added to the list of operating systems in the details pane and are copied to the *deployment_share*\Out-of-box Drivers folder (where *deployment_share* is the deployment share you created earlier in the process).  

###  <a name="CreateTaskSequence"></a> Step 3-4: Create a Task Sequence for the Reference Computer  
 Create MDT task sequences in the Task Sequences node in the Deployment Workbench using the New Task Sequence Wizard. MDT includes the Standard Client Task Sequence template, which you can use to deploy the target operating system to the reference computer (WDG-REF-01).  

 **To create a task sequence for deploying the reference computer**  

1.  Click **Start**, and then point to **All Programs**. Point to **Microsoft Deployment Toolkit**, and then click **Deployment Workbench**.  

2.  In the Deployment Workbench console tree, go to Deployment Workbench/Deployment Shares/MDT Deployment Share (C:\DeploymentShare$)/Task Sequences  

3.  In the Actions pane, click **New Task Sequence**.  

     The New Task Sequence Wizard starts.  

4.  Complete the New Task Sequence Wizard using the following information. Accept the default values unless otherwise specified.

    |**On this wizard page**|**Do this**|  
    |-|-|  
    |**General Settings**|1.  In **Task sequence ID**, type **WIN8_REFERENCE**.<br />2.  In **Task sequence name**, type **Deploy Windows 8.1 to Reference Computer**.<br />3.  In **Task sequence comments**, type **Task sequence for deploying Windows 8.1 to the reference computer (WDG-REF-01)**.<br />4.  Click **Next**.|  
    |**Select Template**|In **The following task sequence templates are available. Select the one you would like to use as a starting point**, select **Standard Client Task Sequence**, and then click **Next**.|  
    |**Select OS**|In **The following operating system images are available to be deployed with this task sequence**. **Select one to use**, select **Windows 8.1 *edition*** (where *edition* is the edition of Windows 8.1 added to the Operating Systems node in the Deployment Workbench), and then click **Next**.|  
    |**Specify Product Key**|Click **Do not specify a product key at this time**, and then click **Next**.|  
    |**OS Settings**|1.  In **Full Name**, type **Woodgrove Bank Employee**.<br /><br /> 2.  In **Organization**, type **Woodgrove Bank**.<br /><br /> 3.  In **Internet Explorer Home Page**, type **http://www.woodgrovebank.com**.<br /><br /> 4.  Click **Next**.|  
    |**Admin Password**|In **Administrator Password** and **Please confirm Administrator Password**, type **P@ssw0rd**, and then click **Next**.|  
    |**Summary**|Click **Next**.|  
    |**Progress**|The progress for creating the task sequence is displayed.|  
    |**Confirmation**|Click **Finish**.|  

 The Import Task Sequence Wizard finishes, and the **Deploy Windows 8.1 to Reference Computer** task sequence is added to the list of task sequences.  

###  <a name="EnableLTIDeployMonitor"></a> Step 3-5: Enable LTI Deployment Process Monitoring  
 Prior to deploying the reference computer (WDG-REF-01) with the LTI bootable media you created earlier in the process, enable monitoring of the LTI deployment process. You monitor the LTI deployment process in the Monitoring node in the deployment share. You enable monitoring on the **Monitoring** tab on the deployment share properties sheet. Later in the process, you will monitor the LTI deployment process.  

 **To enable monitoring of the LTI deployment process**  

1.  Click **Start**, and then point to **All Programs**. Point to **Microsoft Deployment Toolkit**, and then click **Deployment Workbench**.  

2.  In the Deployment Workbench console tree, go to Deployment Workbench/Deployment Shares.  

3.  In the details pane, click **MDT Deployment Share (C:\DeploymentShare$)**.  

4.  In the Actions pane, click **Properties**  

     The **MDT Deployment Share (C:\DeploymentShare$) Properties** dialog box opens.  

5.  In the **MDT Deployment Share (C:\DeploymentShare$) Properties** dialog box, on the **Monitoring** tab, select the **Enable monitoring for this deployment share** check box, and then click **Apply**.  

6.  In the **MDT Deployment Share (C:\DeploymentShare$) Properties** dialog box, on the **Rules** tab, notice that the **EventService** property has been added to the CustomSettings.ini file, and then click **OK**.  

7.  Close all open windows and dialog boxes.  

###  <a name="UpdateDeployShare"></a> Step 3-6: Update the Deployment Share  
 After configuring the deployment share, update it. Updating the deployment share updates all the MDT configuration files and generates a customized version of Windows PE. You use the customized version of Windows PE to start the reference computer and initiate LTI deployment.  

 **To update the deployment share in the Deployment Workbench**  

1.  Click **Start**, and then point to **All Programs**. Point to **Microsoft Deployment Toolkit**, and then click **Deployment Workbench**.  

2.  In the Deployment Workbench console tree, go to Deployment Workbench/Deployment Shares.  

3.  In the details pane, click **MDT Deployment Share (C:\DeploymentShare$)**.  

4.  In the Actions pane, click **Update Deployment Share**.  

     The Update Deployment Share Wizard starts.  

5.  Complete the Update Deployment Share Wizard using the following information. Accept the default values unless otherwise specified.

    |**On this wizard page**|**Do this**|  
    |-|-|  
    |**Options**|Click **Next**.|  
    |**Summary**|Click **Next**.|  
    |**Progress**|The progress for updating the deployment share is displayed.|  
    |**Confirmation**|Click **Finish**.|  

 The Deployment Workbench starts updating the MDT Deployment Share (C:\DeploymentShare$) deployment share. The Deployment Workbench also creates the LiteTouchPE_x64.iso and LiteTouchPE_x64.wim files (for 64-bit target computers) or LiteTouchPE_x86.iso and LiteTouchPE_x86.wim files (for 32-bit target computers) in the *deployment_share*\Boot folder (where *deployment_share* is the network shared folder used as the deployment share).  

## Step 4: Deploy Windows 8.1 and Capture an Image of the Reference Computer  
 After creating the task sequence to deploy Windows 8.1 to the reference computer, initiate operating system deployment and image capture by starting the reference computer with the LTI bootable media.  

 Deploy Windows 8.1 and capture an image of the reference computer by:  

-   Creating the LTI bootable media as described in [Step 4-1: Create the LTI Bootable Media](#CreateLTIBootable)  

-   Starting the reference computer with the LTI bootable media and monitoring the LTI deployment process as described in [Step 4-2: Start the Reference Computer with the LTI Bootable Media](#StartRefCompwithLTIBootable)  

###  <a name="CreateLTIBootable"></a> Step 4-1: Create the LTI Bootable Media  
 You need to provide a method for starting the computer with the customized version of Windows PE you created when you updated the deployment share. The Deployment Workbench creates the LiteTouchPE_x64.iso and LiteTouchPE_x64.wim files (for 64-bit target computers) or LiteTouchPE_x86.iso and LiteTouchPE_x86.wim files (for 32-bit target computers) in the *deployment_share*\Boot folder (where *deployment_share* is the network shared folder used as the deployment share). Create the appropriate LTI bootable media from one of these images.  

 **To create the LTI bootable media**  

1.  In Windows Explorer, go to C:\DeploymentShare$\Boot.  

2.  Based on the type of computer used for the reference computer (WDG-REF-01), perform one of the following tasks:  

    -   If the reference computer is a physical computer, create a physical CD or DVD of the LiteTouchPE_x64.iso or LiteTouchPE_x86.iso file.  

    -   If the reference computer is a VM, start the VM directly from the LiteTouchPE_x64.iso or LiteTouchPE_x86.iso file or from a CD or DVD of the International Standard Organization (ISO) files.  

###  <a name="StartRefCompwithLTIBootable"></a> Step 4-2: Start the Reference Computer with the LTI Bootable Media  
 Start the reference computer (WDG-REF-01) with the LTI bootable media you created earlier in the process. The LTI bootable media starts Windows PE on the reference computer and initiates deployment. At the end of the MDT deployment process, Windows 8.1 is deployed on the reference computer.  

> [!NOTE]
>  You can use a 32-bit boot image to deploy both 32-bit and 64-bit operating systems; however, a 64-bit boot image can only be used to deploy 64-bit operating systems.  

 You could also initiate the process by starting the target computer from Windows Deployment Services. For more information, see the section, "Preparing Windows Deployment Services", in the MDT document, *Using the Microsoft Deployment Toolkit*.  

 **To start the reference computer with the LTI bootable media**  

1.  Start WDG-REF-01 with the LTI bootable media you created earlier in the process.  

     Windows PE starts, and then the Windows Deployment Wizard starts.  

2.  Complete the Windows Deployment Wizard using the following information. Accept the default values unless otherwise specified.  

    |**On this wizard page**|**Do this**|  
    |-|-|  
    |**Welcome**|Click **Run the Deployment Wizard to install a new Operating System**.|  
    |**Credentials**|1.  In **User Name**, type **Administrator**.<br />2.  In **Password**, type **P@ssw0rd**.<br />3.  In **Domain**, type **MDT2013**.<br />4.  Click **OK**.|  
    |**Task Sequence**|Click **Deploy Windows 8.1 to Reference Computer**, and then click **Next**.|  
    |**Computer Details**|In **Computer name**, **type WDG-REF-01**, and then click **Next**.|  
    |**Move Data and Settings**|Click **Next**.|  
    |**User Data (Restore)**|Click **Next**.|  
    |**Locale and Time**|Click **Next**.|  
    |**Capture Image**|Click **Capture an image of this reference computer**, and then click **Next**.|  
    |**Ready**|1.  Click **Details** to view the information provided in the wizard.<br />2.  Click **Begin**.|  

 **To monitor the reference computer deployment process, complete the following steps on WDG-MDT-01**  

1.  On WDG-MDT-01, click **Start**, and then point to **All Programs**. Point to **Microsoft Deployment Toolkit**, and then click **Deployment Workbench**.  

2.  In the Deployment Workbench console tree, go to Deployment Workbench/Deployment Shares/MDT Deployment Share (C:\DeploymentShare$)/Monitoring.  

3.  In the details pane, view the deployment process for **WDG-REF-01**.  

4.  In the Actions pane, periodically click **Refresh**.  

     The status of the deployment process is updated in the details pane.  

     Continue to monitor the deployment process until the process is complete.  

5.  In the details pane, click **WDG-REF-01**.  

6.  In the Actions pane, click **Properties**.  

     The **WDG-REF-01 Properties** dialog box is displayed.  

7.  In the **WDG-REF-01 Properties** dialog box, on the **Identity** tab, view the monitoring information provided about the deployment process as described in the following table.

    |**Information**|**Description**|  
    |-|-|  
    |**ID**|Unique identifier for the computer being deployed.|  
    |**Computer Name**|The name of the computer being deployed.|  
    |**Deployment status**|The current status of the computer being deployed; the status can be one of the following:<br /><br /> -   **Running**. The task sequence is healthy and running.<br />-   **Failed**. The task sequence failed, and the deployment process was unsuccessful.<br />-   **Completed**. The task sequence has finished.<br />-   **Unresponsive**. The task sequence has not updated its status in the past four hours and is assumed to be nonresponsive.|  
    |**Step**|The current task sequence step being run.|  
    |**Progress**|The overall progress of the task sequence. The progress bar indicates how many task sequence steps have been run out of the total number of task sequence steps.|  
    |**Start**|The time the deployment process started.|  
    |**End**|The time the deployment process ended.|  
    |**Elapsed**|The length of time the deployment process has been running or took to run if the deployment process has finished.|  
    |**Errors**|The number of errors encountered during the deployment process.|  
    |**Warnings**|The number of warnings encountered during the deployment process.|  
    |**Remote Desktop**|This button allows you to establish a remote desktop connection with the computer being deployed using the Windows Remote Desktop feature. This method assumes that:<br /><br /> -   The target operating system is running and has remote desktop support enabled<br />-   **mstsc.exe** is in the path **Note:**  This button is always visible but may not be able to establish a remote desktop session if the monitored computer is running Windows PE, has not completed installation of the target operating system, or does not have the Remote Desktop feature enabled.|  
    |**VM Connection**|This button allows you to establish a remote desktop connection to a VM running in HyperV®. This method assumes that:<br /><br /> -   The deployment is being performed to a VM running on Hyper-V<br />-   **vmconnect.exe** is located in the %ProgramFiles%\Hyper-V folder **Note:**  This button appears when ZTIGather.wsf detects that Hyper-V integration components are running on the monitored computer. Otherwise, this button will not be visible.|  
    |**DaRT Remote Control**|This button allows you to establish a remote control session using the remote viewer feature in the Diagnostics and Recovery Toolkit (DaRT).<br /><br /> This method assumes that:<br /><br /> -   DaRT has been deployed to the target computer and is currently running<br />-   **DartRemoteViewer.exe** is located in the %ProgramFiles%\Microsoft DaRT 7\v7 folder **Note:**  This button appears when ZTIGather.wsf detects that DaRT is running on the monitored computer. Otherwise, this button will not be visible.|  
    |**Automatically refresh this information every 10 seconds**|Check box that controls whether the information in the dialog box is automatically refreshed. If the check box is:<br /><br /> -   Selected, the information is refreshed every 10 seconds<br />-   Cleared, the information is not automatically refreshed and must be manually refreshed using the **Refresh Now** button|  
    |**Refresh Now**|This button immediately refreshes the information displayed in the dialog box.|  

8.  In the **WDG-REF-01 Properties** dialog box, click **OK**.  

9. Close the Deployment Workbench.  

 To complete the reference computer deployment process, perform the following steps on WDG-REF-01:  

1.  On WDG-REF-01, in the **Deployment Summary** dialog box, click **Details**.  

     If any errors or warnings occur, review the errors or warnings, and record any diagnostic information.  

2.  In the **Deployment Summary** dialog box, click **Finish**.  

 Windows 8.1 is now installed on the reference computer, and the captured Windows Imaging Format (WIM) file of the reference computer (WIN7_REFERENCE.wim) is stored in the *deployment_share*\Captures folder (where *deployment_share* is the shared folder used as the deployment share).If errors or warnings occur, consult the MDT document *Troubleshooting Reference*.  

## Step 5: Configure MDT to Deploy Windows 8.1 to the Target Computer  
 When you have captured an image of the reference computer (MDT-REF-01), deploy it to the target computer (MDT-CLI-01). You import the captured image into the Deployment Workbench using the Import Operating System Wizard. Then, you create a task sequence to deploy the captured image to the target computer.  

 Configure MDT to deploy Windows 8.1 to the target computer by:  

-   Adding the captured image of the reference computer to the Deployment Workbench as described in [Step 5-1: Add the Captured Image of the Reference Computer to the Deployment Workbench](#AddCapturedImagetoDeployWB)  

-   Creating a task sequence for the target computer as described in [Step 5-2: Create a Task Sequence for the Target Computer](#CreateTaskSequenceforTarget)  

###  <a name="AddCapturedImagetoDeployWB"></a> Step 5-1: Add the Captured Image of the Reference Computer to the Deployment Workbench  
 To deploy the captured image of the reference computer to the target computer, add the captured image to the list of operating systems in the Operating Systems node in the Deployment Workbench. The Import Operating System Wizard copies the operating system files to the *deployment_share*\Operating Systems\\*operating_system* folder (where *deployment_share* is the deployment share folder created earlier in the process and *operating_system* is the name of the operating system added to the deployment share).  

 **To add the captured image of the reference computer to the Deployment Workbench**  

1.  Click **Start**, and then point to **All Programs**. Point to **Microsoft Deployment Toolkit**, and then click **Deployment Workbench**.  

2.  In the Deployment Workbench console tree, go to Deployment Workbench/Deployment Shares/MDT Deployment Share (C:\DeploymentShare$)/Operating Systems.  

3.  In the Actions pane, click **Import Operating system**.  

     The Import Operating System Wizard starts.  

4.  Complete the Import Operating System Wizard using the information in the following table.

    |**On this wizard page**|**Do this**|  
    |-|-|  
    |**OS Type**|Click **Custom image file**, and then click **Next**.|  
    |**Image**|In **Source file**, type **C:\DeploymentShare$\Captures\WIN8_REFERENCE.wim**, and then click **Next**.|  
    |**Setup**|Click **Next**.|  
    |**Destination**|Click **Next**.|  
    |**Summary**|Click **Next**.|  
    |**Progress**|The progress for importing the operating system is displayed.|  
    |**Confirmation**|Click **Finish**.|  

     The Import Operating System Wizard finishes. The captured image of the reference computer (WDG-REF-01) operating system is added to the list of operating systems in the details pane and is copied to the *deployment_share*\Operating Systems\\*operating_system* folder (where *deployment_share* is the deployment share folder created earlier in the process and *operating_system* is the name of the operating system added to the deployment share).  

5.  Close all open windows and dialog boxes.  

###  <a name="CreateTaskSequenceforTarget"></a> Step 5-2: Create a Task Sequence for the Target Computer  
 Create an MDT task sequence for the target computer in the Task Sequences node in the Deployment Workbench using the New Task Sequence Wizard. This task sequence is used to deploy the captured image of the reference computer to the target computer.  

 **To create a task sequence for deploying the captured image to the target computer**  

1.  Click **Start**, and then point to **All Programs**. Point **to Microsoft Deployment Toolkit**, and then click **Deployment Workbench**.  

2.  In the Deployment Workbench console tree, go to Deployment Workbench/Deployment Shares/MDT Deployment Share (C:DeploymentShare$)/Task Sequences.  

3.  In the Actions pane, click **New Task Sequence**.  

     The New Task Sequence Wizard starts.  

4.  Complete the New Task Sequence Wizard using the following information. Accept the default values unless otherwise specified.

    |**On this wizard page**|**Do this**|  
    |-|-|  
    |**General Settings**|1.  In **Task sequence ID**, type **WIN8_TARGET**.<br />2.  In **Task sequence name**, type **Deploy Captured Image to Target Computer**.<br />3.  In **Task sequence comments**, type **Task sequence for captured Windows 8.1 image from reference computer (WDG-REF-01) to the target computer (WDG-CLI-01)**.<br />4.  Click **Next**.|  
    |**Select Template**|In **The following task sequence templates are available**. **Select the one you would like to use as a starting point**, select Standard **Client Task Sequence**, and then click **Next**.|  
    |**Select OS**|In **The following operating system images are available to be deployed with this task sequence**. **Select one to use**, select **WIN8_RERENCEDrive in “WIN8_REFERENCE\WIN8_REFERENCE.wim”**, and then click **Next**.|  
    |**Specify Product Key**|Click **Do not specify a product key at this time**, and then click **Next**.|  
    |**OS Settings**|1.  In **Full Name**, type **Woodgrove Bank Employee**.<br />2.  In **Organization**, type **Woodgrove Bank**.<br />3.  In **Internet Explorer Home Page**, type **http://www.woodgrovebank.com**.<br />4.  Click **Next**.|  
    |**Admin Password**|In **Administrator Password** and **Please confirm Administrator Password**, type **P@ssw0rd**, and then click **Next**.|  
    |**Summary**|Click **Next**.|  
    |**Progress**|The progress for creating the task sequence is displayed.|  
    |**Confirmation**|Click **Finish**.|  

     The Import Task Sequence Wizard finishes, and the **WIN8_TARGET** task sequence is added to the list of task sequences.  

5.  Close all open windows and dialog boxes.  

## Step 6: Deploy the Captured Image of the Reference Computer to the Target Computer  
 When you have captured an image of the reference computer and created and configured the appropriate task sequence, deploy the captured image. Configure MDT to provide all the necessary configuration settings for deployment to the target computer. After initiating the deployment process, the image of the reference computer running Windows 8.1 is automatically deployed to the target computer and configured with the settings defined.  

 Deploy the captured image of the reference computer to the target computer by:  

-   Starting the target computer with the LTI bootable media and monitor the LTI deployment process as described in [Step 6-1: Start the Target Computer with the LTI Bootable Media](#StartTargetwithLTIBootable)  

###  <a name="StartTargetwithLTIBootable"></a> Step 6-1: Start the Target Computer with the LTI Bootable Media  
 Start the target computer (WDG-CLI-01) with the LTI bootable media you created earlier in the process. This CD starts Windows PE on the target computer and initiates deployment. At the end of the process, Windows 8.1 is deployed on the target computer.  

> [!NOTE]
>  You can also initiate deployment by starting the target computer from Windows Deployment Services. For more information, see the MDT document *Using the Microsoft Deployment Toolkit*.  

 **To start the target computer with the LTI bootable media**  

1.  Start WDG-CLI-01 with the LTI bootable media you created earlier in the process.  

     Windows PE starts, and then the Windows Deployment Wizard starts.  

2.  Complete the Windows Deployment Wizard using the following information. Accept the default values unless otherwise specified.   

    |**On this wizard page**|**Do this**|  
    |-|-|  
    |**Welcome**|Click **Run the Deployment Wizard to install a new Operating System**.|  
    |**Credentials**|1.  In **User Name**, type **Administrator**.<br />2.  In **Password**, type **P@ssw0rd**.<br />3.  In **Domain**, type **MDT2013**.<br />4.  Click **OK**.|  
    |**Task Sequence**|Click **Deploy Captured Image to Target Computer**, and then click **Next**.|  
    |**Computer Details**|In **Computer name**, type **WDG-CLI-01**, and then click **Next**.|  
    |**Move Data and Settings**|Click **Next**.|  
    |**User Data (Restore)**|Click **Next**.|  
    |**Locale and Time**|**Click Next**.|  
    |**Capture Image**|Click **Next**.|  
    |**BitLocker**|Click **Next**.|  
    |**Ready**|1.  Click **Details** to view the information provided in the wizard.<br />2.  Click **Begin**.|  

 The wizard starts, and then the operating system deployment starts.  

 **To monitor the target computer deployment process, complete the following steps on WDG-MDT-01**  

1.  On WDG-MDT-01, click **Start**, and then point to **All Programs**. Point to **Microsoft Deployment Toolkit**, and then click **Deployment Workbench**.  

2.  In the Deployment Workbench console tree, go to Deployment Workbench/Deployment Shares/MDT Deployment Share (C:\DeploymentShare$)/Monitoring  

3.  In the Actions pane, periodically click **Refresh**.  

4.  In the details pane, view the deployment process for **WDG-CLI-01**.  

5.  In the Actions pane, periodically click **Refresh**.  

     The status of the deployment process is updated in the details pane. Continue to monitor the deployment process until the process is complete.  

6.  Close the Deployment Workbench.  

 **To complete the target computer deployment process, perform the following steps on WDG-CLI-01**  

1.  On WDG-CLI-01, in the **Deployment Summary** dialog box, click **Details**.  

     If any errors or warnings occur, review the errors or warnings, and record any diagnostic information.  

2.  In the **Deployment Summary** dialog box, click **Finish**.  

 At the end of the MDT deployment process, the **Deployment Summary** dialog box appears. The image of Windows 8.1 captured from the reference computer is now installed on the target computer. If any errors or warnings occur, consult the MDT document *Troubleshooting Reference*.
