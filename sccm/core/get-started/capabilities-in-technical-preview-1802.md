---
title: "Technical Preview 1802 | Microsoft Docs"
titleSuffix: "Configuration Manager"
description: "Learn about features available in the Technical Preview version 1802 for System Center Configuration Manager."
ms.custom: na
ms.date: 02/09/2018 
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4884a2d3-13ce-44e5-88c4-a66dc7ec6014
author: aczechowski
ms.author: aaroncz
manager: dougeby
---
# Capabilities in Technical Preview 1802 for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*

This article introduces the features that are available in the Technical Preview for System Center Configuration Manager, version 1802. You can install this version to update and add new capabilities to your Configuration Manager technical preview site. 

Review [Technical Preview for System Center Configuration Manager](/sccm/core/get-started/technical-preview) before installing this version of the technical preview. That article familiarizes you with the general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback.     


<!--  Known Issues Template   
**Known Issues in this Technical Preview:**
-   **Issue Name**. Details
    Workaround details.
**Known Issues in this Technical Preview:**
-->
**Known Issues in this Technical Preview:**
-   **Update to a new preview version fails when you have a site server in passive mode**. If you have a [primary site server in passive mode](/sccm/core/get-started/capabilities-in-technical-preview-1706#site-server-role-high-availability), then you must uninstall the passive mode site server before updating to this new preview version. You can reinstall the passive mode site server after your site completes the update.

  To uninstall the passive mode site server:
  1. In the Configuration Manager console, go to **Administration** > **Overview** > **Site Configuration** > **Servers and Site System Roles**, and then select the passive mode site server.
  2. In the **Site System Roles** pane, right-click on the **Site server** role, and then choose **Remove Role**.
  3. Right-click on the passive mode site server, and then choose **Delete**.
  4. After the site server uninstalls, on the active primary site server restart the service **CONFIGURATION_MANAGER_UPDATE**.
<!--sms 489412-->


**The following are new features you can try out with this version.**  

<!--  Section Template
##  FEATURE
<-- TFS ID - need to fix comment md here
### Procedure 1
### Try it out!  
 Try to complete the tasks. Then send **Feedback** from the **Home** tab of the ribbon letting us know how it worked.
 -  Task 1
 -  Task 2              
-->



## Configure Windows Delivery Optimization to use Configuration Manager boundary groups
<!-- 1324696 -->
You use Configuration Manager boundary groups to define and regulate content distribution across your corporate network and to remote offices. [Windows Delivery Optimization](/windows/deployment/update/waas-delivery-optimization) is a cloud-based, peer-to-peer technology to share content between Windows 10 devices. Starting in this release, configure Delivery Optimization to use your boundary groups when sharing content among peers. A new client setting applies the boundary group identifier as the Delivery Optimization group identifier on the client. When the client communicates with the Delivery Optimization cloud service, it uses this identifier to locate peers with the desired content. 

### Prerequisites
- Delivery Optimization is only available on Windows 10 clients

### Try it out!
 Try to complete the tasks. Then send **Feedback** from the **Home** tab of the ribbon letting us know how it worked.

1. In the Configuration Manager console, **Administration** workspace, **Client Settings** node, create a custom client device settings policy.
2. Select the new **Delivery Optimization** group.
3. Enable the setting **Use Configuration Manager Boundary Groups for Delivery Optimization Group ID**.

For more information, see the **Group** delivery mode option in [Delivery Optimization options](/windows/deployment/update/waas-delivery-optimization#group-id).



## Windows 10 in-place upgrade task sequence via cloud management gateway
<!-- 1357149 -->

The Windows 10 [in-place upgrade task sequence](/sccm/osd/deploy-use/upgrade-windows-to-the-latest-version) now supports deployment to Internet-based clients managed through the [cloud management gateway](/sccm/core/clients/manage/plan-cloud-management-gateway). This ability allows remote users to more easily upgrade to Windows 10 without needing to connect to the corporate network. 

Ensure all of the content referenced by the in-place upgrade task sequence is distributed to a [cloud distribution point](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point). Otherwise devices cannot run the task sequence.

When you deploy an upgrade task sequence, use the following settings:
- **Allow task sequence to run for client on the Internet**, on the User Experience tab of the deployment.
- **Download all content locally before starting task sequence**, on the Distribution Points tab of the deployment. Other options such as **Download content locally when needed by the running task sequence** do not work in this scenario. The task sequence engine is currently unable to obtain content from a cloud distribution point. The Configuration Manager client must download the content from the cloud distribution point before starting the task sequence.
- (*Optional*) **Pre-download content for this task sequence**, on the General tab of the deployment. For more information, see [Configure pre-cache content](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content).



## Improvements to Windows 10 in-place upgrade task sequence
<!-- 1357425 -->
The default task sequence template for Windows 10 in-place upgrade now includes additional groups with recommended actions to add before and after the upgrade process. These actions are common among many customers who are successfully upgrading devices to Windows 10. 

### New groups under **Prepare for Upgrade**
- **Battery checks**: Add steps in this group to check whether the computer is using battery, or wired power. This action requires a custom script or utility to perform this check.
- **Network/wired connection checks**: Add steps in this group to check whether the computer is connected to a network, and is not using a wireless connection. This action requires a custom script or utility to perform this check.
- **Remove incompatible applications**: Add steps in this group to remove any applications that are incompatible with this version of Windows 10. The method to uninstall an application varies. If the application uses Windows Installer, copy the **Uninstall program** command line from the **Programs** tab on the Windows Installer deployment type properties of the application. Then add a **Run Command Line** step in this group with the uninstall program command line. For example: </br>`msiexec /x {150031D8-1234-4BA8-9F52-D6E5190D1CBA} /q`</br> 
- **Remove incompatible drivers**: Add steps in this group to remove any drivers that are incompatible with this version of Windows 10.
- **Remove/suspend third-party security**: Add steps in this group to remove or suspend third-party security programs, such as antivirus.
   - If you are using a third-party disk encryption program, provide its encryption driver to Windows Setup with the **/ReflectDrivers** [command-line option](/windows-hardware/manufacture/desktop/windows-setup-command-line-options). Add a [Set Task Sequence Variable](/sccm/osd/understand/task-sequence-steps#BKMK_SetTaskSequenceVariable) step to the task sequence in this group. Set the task sequence variable to **OSDSetupAdditionalUpgradeOptions**. Set the value to **/ReflectDriver** with the path to the driver. This [task sequence action variable](/sccm/osd/understand/task-sequence-action-variables#upgrade-operating-system) appends the Windows Setup command-line used by the task sequence. Contact your software vendor for any additional guidance on this process.

### New groups under **Post-Processing**
- **Apply setup-based drivers**: Add steps in this group to install setup-based drivers (.exe) from packages.
- **Install/enable third-party security**: Add steps in this group to install or enable third-party security programs, such as antivirus. 
- **Set Windows default apps and associations**: Add steps in this group to set Windows default apps and file associations. First prepare a reference computer with your desired app associations. Then run the following command line to export: </br>`dism /online /Export-DefaultAppAssociations:"%UserProfile%\Desktop\DefaultAppAssociations.xml"`</br>Add the XML file to a package. Then add a [Run Command Line](/sccm/osd/understand/task-sequence-steps#BKMK_RunCommandLine) step in this group. Specify the package that contains the XML file, and then specify the following command line: </br>`dism /online /Import-DefaultAppAssociations:DefaultAppAssocations.xml`</br> For more information, see [Export or import default application associations](/windows-hardware/manufacture/desktop/export-or-import-default-application-associations).
- **Apply customizations and personalization**: Add steps in this group to apply Start menu customizations, such as organizing program groups. For more information, see [Customize the Start screen](/windows-hardware/manufacture/desktop/customize-the-start-screen).

### Additional recommendations
- Review Windows documentation to [Resolve Windows 10 upgrade errors](/windows/deployment/upgrade/resolve-windows-10-upgrade-errors). This article also includes detailed information about the upgrade process.
- On the default **Check Readiness** step, enable **Ensure minimum free disk space (MB)**. Set the value to at least **16384** (16 GB) for a 32-bit OS upgrade package, or **20480** (20 GB) for 64-bit. 
- Use the **SMSTSDownloadRetryCount** [built-in task sequence variable](/sccm/osd/understand/task-sequence-built-in-variables) to retry downloading policy. Currently by default, the client retries twice; this variable is set to two (2). If your clients are not on a wired corporate network connection, additional retries help the client obtain policy. Using this variable causes no negative side effect, other than delayed failure if it cannot download policy.<!-- 501016 --> Also increase the **SMSTSDownloadRetryDelay** variable from the default 15 seconds.
- Perform an inline compatibility assessment. 
   - Add a second **Upgrade Operating System** step early in the **Prepare for Upgrade** group. Name it *Upgrade assessment*. Specify the same upgrade package, and then enable the option to **Perform Windows Setup compatibility scan without starting upgrade**. Enable **Continue on error** on the Options tab. 
   - Immediately following this *Upgrade assessment* step, add a **Run Command Line** step. Specify the following command line:</br> `cmd /c exit %_SMSTSOSUpgradeActionReturnCode%`</br>On the **Options** tab, add the following condition: </br>`Task Sequence Variable _SMSTSOSUpgradeActionReturnCode not equals 3247440400` </br>This return code is the decimal equivalent of MOSETUP_E_COMPAT_SCANONLY (0xC1900210), which is a successful compatibility scan with no issues. If the *Upgrade Assessment* step succeeds and returns this code, this step is skipped. Otherwise, if the assessment step returns any other return code, this step fails the task sequence with the return code from the Windows Setup compatibility scan.
   - For more information, see [Upgrade operating system](/sccm/osd/understand/task-sequence-steps#BKMK_UpgradeOS).
- If you want to change the device from BIOS to UEFI during this task sequence, see [Convert from BIOS to UEFI during an in-place upgrade](/sccm/osd/deploy-use/task-sequence-steps-to-manage-bios-to-uefi-conversion#convert-from-bios-to-uefi-during-an-in-place-upgrade).

Send **Feedback** from the **Home** tab of the ribbon if you have further recommendations or suggestions.



## Improvements to PXE-enabled distribution points
<!-- 1357580 -->
To clarify the behavior of [new PXE functionality](/sccm/core/get-started/capabilities-in-technical-preview-1706#pxe-network-boot-support-for-ipv6) first introduced in Technical Preview version 1706, we renamed the **Support IPv6** option. On the **PXE** tab of the distribution point properties, check **Enable a PXE responder without Windows Deployment Service**. 

This option enables a PXE responder on the distribution point, which does not require Windows Deployment Services (WDS). If you enable this new option on a distribution point that is already PXE-enabled, Configuration Manager suspends the WDS service. If you disable this new option, but still **Enable PXE support for clients**, then the distribution point enables WDS again.

Because WDS is not required, the PXE-enabled distribution point can be a client or server operating system, including Windows Server Core. This new PXE responder service continues to support IPv6, and also enhances the flexibility of PXE-enabled distribution points in remote offices.

> [!NOTE]
> This service uses the same fundamental technology as the [Client-based PXE responder service](/sccm/core/get-started/capabilities-in-technical-preview-1712#client-based-pxe-responder-service) in Technical Preview version 1712. That feature does not require the overhead of the distribution point role.

### Multicast
To enable and configure multicast on the **Multicast** tab of the distribution point properties, the distribution point must use WDS. 
- If you **Enable PXE support for clients** and **Enable multicast to simultaneously send data to multiple clients**, then you cannot **Enable a PXE responder without Windows Deployment Service**.
- If you **Enable PXE support for clients** and **Enable a PXE responder without Windows Deployment Service**, then you cannot **Enable multicast to simultaneously send data to multiple clients**






## Next steps
For information about installing or updating the technical preview branch, see [Technical Preview for System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
