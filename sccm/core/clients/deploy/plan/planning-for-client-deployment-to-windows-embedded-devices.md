---
title: "Planning client deployment to Windows Embedded devices | Microsoft Docs"
description: "Plan for client deployment to Windows Embedded devices in System Center Configuration Manager."
ms.custom: na
ms.date: 04/23/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-client
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 038e61f9-f49d-41d1-9a9f-87bec9e00d5d
caps.latest.revision: 7
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe

---
# Planning for client deployment to Windows Embedded devices in System Center Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

<a name="BKMK_DeployClientEmbedded"></a> If your Windows Embedded device does not include the System Center Configuration Manager client, you can use any of the client installation methods if the device meets the required dependencies. If the embedded device supports write filters, you must disable these filters before you install the client, and then re-enable the filters again after the client is installed and assigned to a site.  

 Note that when you disable the filters, you should not disable the filter drivers. Typically these drivers are started automatically when the computer is started. Disabling the drivers will either prevent installation of the client, or interfere with write filter orchestration which will cause client operations to fail. These are the services associated with each write filter type that must remain running:  

|Write Filter Type|Driver|Type|Description|  
|-----------------------|------------|----------|-----------------|  
|EWF|ewf|Kernel|Implements sector-level I/O redirection on protected volumes.|  
|FBWF|fbwf|File system|Implements file-level I/O redirection on protected volumes.|  
|UWF|uwfreg|Kernel|UWF Registry Redirector|  
|UWF|uwfs|File System|UWF File Redirector|  
|UWF|uwfvol|Kernel|UWF Volume Manager|  

 Write filters control how the operating system on the embedded device is updated when you make changes, such as when you install software. When write filters are enabled, instead of making the changes directly to the operating system, these changes are redirected to a temporary overlay. If the changes are only written to the overlay, they are lost when the embedded device shuts downs. However, if the write filters are temporarily disabled, the changes can be made permanent so that you do not have to make the changes again (or reinstall software) every time that the embedded device restarts. However, temporarily disabling and then re-enabling the write filters requires one or more restarts, so that you typically want to control when this happens by configuring maintenance windows so that restarts occur outside business hours.  

 You can configure options to automatically disable and re-enable the write filters when you deploy software such as applications, task sequences, software updates, and the Endpoint Protection client. The exception is for configuration baselines with configuration items that use automatic remediation. In this scenario, the remediation always occurs in the overlay so that it is available only until the device is restarted. The remediation is applied again at the next evaluation cycle, but only to the overlay, which is cleared at restart. To force Configuration Manager to commit the remediation changes, you can deploy the configuration baseline and then another software deployment that supports committing the change as soon as possible.  

 If the write filters are disabled, you can install software on Windows Embedded devices by using Software Center. However, if the write filters are enabled, the installation fails and Configuration Manager displays an error message that you have insufficient permissions to install the application.  

> [!WARNING]  
>  Even if you do not select the Configuration Manager options to commit the changes, the changes might be committed if another software installation or change is made that commits changes. In this scenario, the original changes will be committed in addition to the new changes.  

 When Configuration Manager disables the write filters to make changes permanent, only users who have local administrative rights can log on and use the embedded device. During this period, low-rights users are locked out and see a message that the computer is unavailable because it is being serviced. This helps protect the device while it is in a state where changes can be permanently applied, and this servicing mode lockout behavior is another reason to configure a maintenance window for a time when users will not log on to these devices.  

 Configuration Manager supports managing the following types of write filters:  

-   File-Based Write Filter (FBWF) -  For more information, see [File-Based Write Filter](http://go.microsoft.com/fwlink/?LinkID=204717).  

-   Enhanced Write Filter (EWF) RAM - For more information, see [Enhanced Write Filter](http://go.microsoft.com/fwlink/?LinkId=204718).  

-   Unified Write Filter (UWF) - For more information, see [Unified Write Filter](http://go.microsoft.com/fwlink/?LinkId=309236).  

 Configuration Manager does not support write filter operations when the Windows Embedded device is in EWF RAM Reg mode.  

> [!IMPORTANT]  
>  If you have the choice, use File-Based Write Filters (FBWF) with Configuration Manager for increased efficiency and higher scalability.
>
> **For devices that use FBWF only:** Configure the following exceptions to persist client state and inventory data between device restarts:  
>   
>  -   CCMINSTALLDIR\\*.sdf  
> -   CCMINSTALLDIR\ServiceData  
> -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\StateSystem  
>   
>  Devices that run Windows Embedded 8.0 and later do not support exclusions that contain wildcard characters. On these devices, you must configure the following exclusions individually:  
>   
>  -   All files in CCMINSTALLDIR with the extension .sdf, typically:  
>   
>     -   UserAffinityStore.sdf  
>     -   InventoryStore.sdf  
>     -   CcmStore.sdf  
>     -   StateMessageStore.sdf  
>     -   CertEnrollmentStore.sdf  
> -   CCMINSTALLDIR\ServiceData  
> -   HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\StateSystem  
>   
> **For devices that use FBWF and UWF only:**
> When clients in a workgroup use certificates for authentication to management points, you must also exclude the private key to ensure the client continues to communicate with the management point. On these devices, configure the following exceptions:  
>   
>  -   c:\Windows\System32\Microsoft\Protect  
> -   c:\ProgramData\Microsoft\Crypto  
> -   HKEY_LOCAL_MACHINE\Software\Microsoft\SystemCertificates\SMS\Certificates  

 For an example scenario to deploy and manage write-filter-enabled Windows Embedded devices in Configuration Manager see [Example scenario for deploying and managing System Center Configuration Manager clients on Windows Embedded devices](../../../../core/clients/deploy/example-scenario-for-deploying-and-managing-clients-on-windows-embedded-devices.md).  

 For more information about how to build images for Windows Embedded devices and configure write filters, see your Windows Embedded documentation, or contact your OEM.  

> [!NOTE]  
>  When you select the applicable platforms for software deployments and configuration items, these display the Windows Embedded families rather than specific versions. Use the following list to map the specific version of Windows Embedded to the options in the list box:  
>   
>  -   **Embedded Operating Systems based on Windows XP (32-bit)** includes the following:  
>   
>      -   Windows XP Embedded  
>     -   Windows Embedded for Point of Service  
>     -   Windows Embedded Standard 2009  
>     -   Windows Embedded POSReady 2009  
> -   **Embedded operating systems based on Windows 7 (32-bit)** includes the following:  
>   
>      -   Windows Embedded Standard 7 (32-bit)  
>     -   Windows Embedded POSReady 7 (32-bit)  
>     -   Windows ThinPC  
> -   **Embedded operating systems based on Windows 7 (64-bit)** includes the following:  
>   
>      -   Windows Embedded Standard 7 (64-bit)  
>     -   Windows Embedded POSReady 7 (64-bit)
