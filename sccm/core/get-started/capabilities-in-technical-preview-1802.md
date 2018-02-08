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

## Transition Endpoint Protection workload to Intune using co-management    
<!-- 1357365 -->
In this release, you can now transition the Endpoint Protection workload from Configuration Manager to Intune after co-management is enabled. To transition the Endpoint Protection workload, go to the co-management properties page and move the slider bar from Configuration Manager to **Pilot** or **All**. For details, see [Co-management for Windows 10 devices](/sccm/core/clients/manage/co-management-overview).
 
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



## Deployment templates for task sequences
<!-- 1357391 -->
The deployment wizard for task sequences can now create a deployment template. The deployment template can be saved and applied to an existing or new task sequence to create a deployment. 

### Try it out!  
Try to complete the tasks. Then send **Feedback** from the **Home** tab of the ribbon letting us know how it worked. 

 **Create a deployment template for a new task sequence deployment** <br/> 
1. In the **Software Library** workspace, expand **Operating Systems**, and select **Task Sequences**.
2. Right-click on a task sequence and select **Deploy**. 
3. On the **General** tab, note there is now an option to **Select Deployment Template**. 
4. Continue through the **Deploy Software Wizard** selecting the deployment settings for the task sequence. 
5. When you reach the **Summary** tab of the **Deploy Software Wizard**, click on **Save As Template**.
6. Give the template a name and select the settings to save in the template. 
7. Click **Save**. The template is now available for use from the **Select Deployment Template** option.



## Product Lifecycle dashboard
<!--1319632-->
The new Product Lifecycle dashboard shows the state of the Microsoft Product Lifecycle policy for Microsoft products installed on devices managed with Configuration Manager. The dashboard provides you with information about Microsoft products in your environment, supportability state, and support end dates. You can use the dashboard to understand the availability of support for each product. 

To access the Lifecycle Dashboard, in the Configuration Manager console, go to **Assets and Compliance** >**Asset Intelligence** >**Product Lifecycle**



## Improvements to reporting
<!--1357653-->
As a result of [your feedback](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/32434147-new-builtin-reports-about-windows-10-versions-and) we added a new report, **Windows 10 Servicing details for a specific collection**. This report shows Resource ID, NetBIOS name, OS name, OS release name, build, OS branch, and servicing state for Windows 10 devices. To access the report, go to **Monitoring** >**Reporting** >**Reports** >**Operating Systems** >**Windows 10 Servicing details for a specific collection**.



## Improvements to Software Center
<!--1357592-->
As a result of [your feedback](https://configurationmanager.uservoice.com/forums/300492-ideas/suggestions/13002684-software-center-show-only-available-software-hid) installed applications can now be hidden in Software Center. Applications that are already installed will no longer show in the Applications tab when this option is enabled. 

### Try it out!
Enable the **Hide Installed Applications in Software Center** setting in the Software Center client settings. Observe the behavior on Software Center when the end user installs an application.



## Improvements to Run Scripts
<!--1236459-->
The [Run Scripts](/sccm/apps/deploy-use/create-deploy-scripts) feature now returns script output using JSON formatting. This format consistently returns a readable script output. Scripts that fail to run may not get output returned. 



## Boundary group fallback for management points
<!-- 1324594 -->
Starting in this release, you can configure fallback relationships for management points between [boundary groups](/sccm/core/servers/deploy/configure/boundary-groups). This behavior provides greater control for the management points that clients use. On the **Relationships** tab of the boundary group properties, there is a new column for management point. When you add a new fallback boundary group, the fallback time for the management point is currently always zero (0). This behavior is the same for the **Default Behavior** on the site default boundary group.

Previously, a common problem occurs when you have a protected management point in a secure network. Clients on the main corporate network receive policy that includes this protected management point, even though they cannot communicate with it across a firewall. To address this problem, use the **Never fallback** option to ensure that clients only fallback to management points with which they can communicate.

When upgrading the site to this version, Configuration Manager adds all non-Internet-facing management points into the site default boundary group. This upgrade behavior ensures that older client versions continue to communicate with management points. In order to take full advantage of this feature, move your management points to the desired boundary groups.

Management point boundary group fallback does not change the behavior during client installation (ccmsetup). If the command line does not specify the initial management point using the /MP parameter, the new client receives the full list of available management points. For its initial bootstrap process, the client uses the first management point it can access. Once the client registers with the site, it receives the management point list properly sorted with this new behavior. 

### Prerequisites
- Enable [preferred management points](/sccm/core/servers/deploy/configure/boundary-groups#preferred-management-points). In the Configuration Manager console, go to the **Administration** workspace. Expand **Site Configuration** and select **Sites**. Click **Hierarchy Settings** in the ribbon. On the **General** tab, enable **Clients prefer to use management points specified in boundary groups**. 

### Known issues
- Operating system deployment processes are not aware of boundary groups.

### Troubleshooting
New entries appear in the **LocationServices.log**. The **Locality** attribute identifies one of the following states:
- 0: Unknown
- 1: The specified management point is only in the site default boundary group for fallback
- 2: The specified management point is in a remote or neighbor boundary group. When the management point is in both a neighbor and site default boundary groups, the locality is 2.
- 3: The specified management point is in the local or current boundary group. When the management point is in both the current and a neighbor or site default boundary groups, the locality is 3. If you do not enable the preferred management points setting in Hierarchy Settings, the locality is always 3 no matter which boundary group the management point is in.

Clients use local management points first (locality 3), remote second (locality 2), then fallback (locality 1). 

When a client receives five errors in ten minutes and fails to communicate with a management point in its current boundary group, it tries to contact a management point in a neighbor or site default boundary group. If the management point in the current boundary group later comes back online, the client will return to the local management point on the next refresh cycle. The refresh cycle is 24 hours, or when the Configuration Manager agent service restarts.



## Improved support for CNG certificates
<!-- 1357314 -->
Configuration Manager (current branch) version 1710 supports [Cryptography: Next Generation (CNG) certificates](/sccm/core/plan-design/network/cng-certificates-overview). Version 1710 limits support to client certificates in several scenarios. 

Starting in this technical preview release, use CNG certificates for the following HTTPS-enabled server roles:
- Management point
- Distribution point
- Software update point

The list of [unsupported scenarios](/sccm/core/plan-design/network/cng-certificates-overview#unsupported-scenarios) remains the same.



## Cloud management gateway support for Azure Resource Manager
<!-- 1324735 -->
When creating an instance of the [cloud management gateway](/sccm/core/clients/manage/plan-cloud-management-gateway) (CMG), the wizard now provides the option to create an **Azure Resource Manager deployment**. [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) is a modern platform for managing all solution resources as a single entity, called a [resource group](/azure/azure-resource-manager/resource-group-overview#resource-groups). When deploying CMG with Azure Resource Manager, the site uses Azure Active Directory (Azure AD) to authenticate and create the necessary cloud resources. This modernized deployment does not require the classic Azure management certificate.  

The CMG wizard still provides the option for a **classic service deployment** using an Azure management certificate. To simplify the deployment and management of resources, we recommend using the Azure Resource Manager deployment model for all new CMG instances. If possible, redeploy existing CMG instances through Resource Manager.

Configuration Manager does not migrate existing classic CMG instances to the Azure Resource Manager deployment model. Create new CMG instances using Azure Resource Manager deployments, and then remove classic CMG instances. 

> [!IMPORTANT]
> This capability does not enable support for Azure Cloud Service Providers (CSP). The CMG deployment with Azure Resource Manager continues to use the classic cloud service, which the CSP does not support. For more information, see [available Azure services in Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services).  

### Prerequisites
- Integration with [Azure AD](/sccm/core/clients/deploy/deploy-clients-cmg-azure). Azure AD user discovery is not required.
- The same [requirements for cloud management gateway](/sccm/core/clients/manage/plan-cloud-management-gateway#requirements-for-cloud-management-gateway), except for the Azure management certificate.

### Try it out!  
 Try to complete the tasks. Then send **Feedback** from the **Home** tab of the ribbon letting us know how it worked.

1. In the Configuration Manager console, **Administration** workspace, expand **Cloud Services**, and select **Cloud Management Gateway**. Click **Create Cloud Management Gateway** in the ribbon. 
2. On the **General** page, select **Azure Resource Manager deployment**. Click **Sign in** to authenticate with an Azure subscription administrator account. The wizard auto-populates the remaining fields from the Azure AD subscription information stored during the integration prerequisite. If you own multiple subscriptions, select the desired subscription to use. Click **Next**.  
3. On the **Settings** page, provide the server PKI certificate file as usual. This certificate defines the CMG service name in Azure. Select the **Region**, and then select a resource group option to either **Create new** or **Use existing**. Enter the new resource group name, or select an existing resource group from the drop-down list. 
4. Complete the wizard.

> [!NOTE] 
> For the selected Azure AD server app, Azure assigns the subscription **contributor** permission. 

Monitor the service deployment progress with **cloudmgr.log** on the service connection point.



## Approve application requests for users per device
<!-- 1357015 -->
Starting in this release, when a user requests an application that requires approval, the specific device name is now a part of the request. If the administrator approves the request, the user is only able to install the application on that device. The user must submit another request to install the application on another device. 

### Prerequisites
- Upgrade the Configuration Manager client to the latest version
- Enable the client setting **Use new Software Center** in the [Computer agent](/sccm/core/clients/deploy/about-client-settings#computer-agent) group

### Try it out!
 Try to complete the tasks. Then send **Feedback** from the **Home** tab of the ribbon letting us know how it worked.

1. Deploy an application as available to a user collection.
2. On the **Deployment Settings** page, enable the option **An administrator must approve a request for this application on the device**.

View **Approval Requests** under **Application Management** in the **Software Library** workspace of the Configuration Manager console. There is now a **Device** column in the list for each request. When you take action on the request, the Application Request dialog also includes the device name from which the user submitted the request.



## Use Software Center to browse and install user-available applications on Internet-based clients
<!-- 1322613 -->
If you deploy applications as available to users, they can now browse and install them through Software Center on Internet-based clients. The Configuration Manager client uses the cloud management gateway to communicate with the on-premises application catalog website point role.

### Prerequisites
- [Cloud management gateway](/sccm/core/clients/manage/plan-cloud-management-gateway) with [Azure Active Directory (Azure AD) integration](/sccm/core/clients/deploy/deploy-clients-cmg-azure)
- An application deployed as available to a user collection
- Enable the client setting **Use new Software Center** in the [Computer agent](/sccm/core/clients/deploy/about-client-settings#computer-agent) group
- Enable the client setting **Enable user policy requests from Internet clients** in the [Client Policy](/sccm/core/clients/deploy/about-client-settings#client-policy) group
- The client must be: 
   - Windows 10
   - Azure AD-joined, also known as cloud-domain joined. 

### Known issues
- This functionality does not yet support hybrid domain joined. A hybrid device is joined to both Azure AD and on-premises Active Directory.
- When an Internet-based client roams back to the corporate network, Software Center does not display user-available applications.



## Report on Windows AutoPilot device information
<!-- 1351442 -->
Windows AutoPilot is a solution for onboarding and configuring new Windows 10 devices in a modern way. For more information, see an [overview of Windows AutoPilot](https://docs.microsoft.com/windows/deployment/windows-autopilot/windows-10-autopilot). One method of registering existing devices with Windows AutoPilot is to upload device information to the Microsoft Store for Business and Education. This information includes the device serial number, Windows product identifier, and a hardware identifier. Use Configuration Manager to collect and report this device information. 

### Prerequisites
- This device information only applies to clients on Windows 10, version 1703, and later

### Try it out!
 Try to complete the tasks. Then send **Feedback** from the **Home** tab of the ribbon letting us know how it worked.

1. In the Configuration Manager console, **Monitoring** workspace, expand the **Reporting** node, expand **Reports**, and select the **Hardware - General** node.
2. Run the new report, **Windows AutoPilot Device Information** and view the results. 
3. In the report viewer click the **Export** icon, and select **CSV (comma delimited)** option.
4. After saving the file, upload the data to the Microsoft Store for Business and Education. For more information, see [add devices in Microsoft Store for Business and Education](https://docs.microsoft.com/microsoft-store/add-profile-to-devices#add-devices-and-apply-autopilot-deployment-profile). 



## Next steps
For information about installing or updating the technical preview branch, see [Technical Preview for System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
