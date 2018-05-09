---
title: Technical Preview 1805
titleSuffix: Configuration Manager
description: Learn about new features available in the Configuration Manager Technical Preview version 1805.
ms.date: 05/11/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 7996b3eb-5259-483b-af40-adae2943d123
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Capabilities in Technical Preview 1805 for System Center Configuration Manager

*Applies to: System Center Configuration Manager (Technical Preview)*

This article introduces the features that are available in the Technical Preview for Configuration Manager, version 1805. You can install this version to update and add new capabilities to your technical preview site. 

Review the [Technical Preview](/sccm/core/get-started/technical-preview) article before installing this update. That article familiarizes you with the general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback.     


<!--  Known Issues Template
## Known Issues in this Technical Preview

### <a name="bkmk_ANCHOR"></a> Known issue title
<!--bugID--
Issue description and cause.

#### Workaround
Steps to workaround, if any.  
-->



</br>

**The following are new features you can try out with this version.**  



## Create a phased deployment with manually configured phases for a task sequence
<!--1358148--> 
You can now create a phased deployment with manually configured phases for a task sequence. You can also add up to 10 additional phases from the **Phases** tab on **Create Phased Deployment** wizard. 

### Try it out!
Follow the instructions to create a phased deployment where you manually configure all phases. Add additional phases from the **Phases** tab on **Create Phased Deployment** wizard using steps 4 though 9. You can configure up to 10 phases. Send [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) letting us know how it worked. 

1. In the **Software Library** workspace, expand **Operating Systems**, and select **Task Sequences**.  

2. Right-click on an existing task sequence and select **Create Phased Deployment**.  

3. On the **General** tab, give the phased deployment a name, description (optional), and select **Manually configure all phases**.  

4. On the **Phases** tab, click on **Add**.  

5. Populate the **Phase Collection** for your first phase and choose if you want to **pre-download content for this task sequence**.  

6. On the **Phase Settings** tab, choose one option for each of the scheduling settings and select **Next** when complete.  
    - **Criteria for success of the previous phase** (This option is disabled for the first phase.)
        - **Deployment success percentage**: Specify percent of devices that successfully complete the deployment for the previous phase success criteria. 
        - **Number of devices successfully deployed**: Specify number of devices that successfully complete the deployment for previous phase success criteria. 
    - **Conditions for beginning this phase of deployment after success of the previous phase** 
        - **Automatically begin this phase after a deferral period (in days)**: Choose the number of days to wait before beginning the next phase after the success of the previous phase. 
        - **Manually begin this phase of deployment**: Don't begin this phase automatically after success of the previous phase. 
    - **Interval for targeting devices in this phase (in days)**: The number of days to span targeting of device deployments across for this phase. 
    - **Once a device is targeted, install the software**
        - **As soon as possible**: Sets the deadline for installation on the device as soon as the device is targeted.
        - **Deadline time (relative to the time device is targeted)**: Sets deadline for installation a certain number of days after device is targeted.  
     
7. Specify **User Experience** such as **User Notifications** and **Write filter handling for Windows Embedded devices**.  

8. Specify **Distribution Point** settings for the phase. Verify the summary for the phase.  

9. On the **Phases** tab, add, edit, remove, or reorder any  phases as needed then click **Next**.  

10. The **Stop Criteria** tab allows you to specify when to automatically stop deploying for all phases.
    - **Criteria for automatic stop of deployments in all phases**
        - **Percentage of deployments failed across all phases**: Select the percentage of deployment failures to stop deployments in all phases. 
        - **Number of devices with failed deployments across all phases**: Choose the number of devices that failed the deployment to stop deployments in all phases.  

11. Confirm your selections on the **Summary** tab. Then click **Next** and proceed though the wizard.  



## Cloud distribution point support for Azure Resource Manager
<!--1322209-->
When creating an instance of the [cloud distribution point](/sccm/core/servers/deploy/configure/install-cloud-based-distribution-points-in-microsoft-azure), the wizard now provides the option to create an **Azure Resource Manager deployment**. [Azure Resource Manager](/azure/azure-resource-manager/resource-group-overview) is a modern platform for managing all solution resources as a single entity, called a [resource group](/azure/azure-resource-manager/resource-group-overview#resource-groups). When deploying a cloud distribution point with Azure Resource Manager, the site uses Azure Active Directory (Azure AD) to authenticate and create the necessary cloud resources. This modernized deployment does not require the classic Azure management certificate.  

The cloud distribution point wizard still provides the option for a **classic service deployment** using an Azure management certificate. To simplify the deployment and management of resources, we recommend using the Azure Resource Manager deployment model for all new cloud distribution points. If possible, redeploy existing cloud distribution points through Resource Manager.

Configuration Manager does not migrate existing classic cloud distribution points to the Azure Resource Manager deployment model. Create new cloud distribution points using Azure Resource Manager deployments, and then remove classic cloud distribution points. 

> [!IMPORTANT]  
> This capability does not enable support for Azure Cloud Service Providers (CSP). The cloud distribution point deployment with Azure Resource Manager continues to use the classic cloud service, which the CSP does not support. For more information, see [available Azure services in Azure CSP](/azure/cloud-solution-provider/overview/azure-csp-available-services).  


### Prerequisites  
- Integration with [Azure AD](/sccm/core/clients/deploy/deploy-clients-cmg-azure). Azure AD user discovery is not required.  

- The same [requirements for a cloud distribution point](/sccm/core/plan-design/hierarchy/use-a-cloud-based-distribution-point#BKMK_PrereqsCloudDP), except for the Azure management certificate.  


### Try it out!  
 Try to complete the tasks. Then send [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) letting us know how it worked.

1. In the Configuration Manager console, **Administration** workspace, expand **Cloud Services**, and select **Cloud Distribution Points**. Click **Create Cloud Distribution Point** in the ribbon.   

2. On the **General** page, select **Azure Resource Manager deployment**. Click **Sign in** to authenticate with an Azure subscription administrator account. The wizard auto-populates the remaining fields from the Azure AD subscription information stored during the integration prerequisite. If you own multiple subscriptions, select the desired subscription to use. Click **Next**.  

3. On the **Settings** page, provide the server PKI **Certificate file** as usual. This certificate defines the cloud distribution point **Service FQDN** used by Azure. Select the **Region**, and then select a resource group option to either **Create new** or **Use existing**. Enter the new resource group name, or select an existing resource group from the drop-down list.  

4. Complete the wizard.  

> [!NOTE]  
> For the selected Azure AD server app, Azure assigns the subscription **contributor** permission.  

Monitor the service deployment progress with **cloudmgr.log** on the service connection point.



## Take actions based on management insights
<!--1357930-->
Some [management insights](/sccm/core/servers/manage/management-insights) now have the option to take an action. Depending upon the rule, this action exhibits one of the following behaviors:  

- Automatically navigate in the console to the node where you can take further action. For example, if the management insight recommends changing a client setting, taking action navigates to the Client Settings node. You can take further action by modifying the default or a custom client settings object.  

- Navigate to a filtered view based on a query. For example, taking action on the empty collections rule shows just these collections in the list of collections. Here you can take further action, such as deleting a collection or modifying its membership rules.  

The following management insight rules have actions in this release:
- Security
    - Unsupported antimalware client versions
- Software Center
    - Use the new version of Software Center
- Applications
    - Applications without deployments
- Simplified Management
    - Non-CB Client Versions
- Collections
    - Empty Collections 
- Cloud Services
    - Update clients to the latest Windows 10 version



## Transition device configuration workload to Intune using co-management
<!--1357903-->

You can now transition the device configuration workload from Configuration Manager to Intune after enabling co-management. Transitioning this workload lets you use Intune to deploy MDM polices, while continuing to use Configuration Manager for deploying applications. 

To transition this workload, go to the co-management properties page and move the slider bar from Configuration Manager to **Pilot** or **All**. For more information, see [Co-management for Windows 10 devices](/sccm/core/clients/manage/co-management-overview).

> [!Note]  
> Moving this workload also moves the **Resource Access** and **Endpoint Protection** workloads, which are a subset of the device configuration workload.

You can make exceptions in a specific configuration baseline. When creating a configuration baseline in Configuration Manager, enable the option to **Always apply this baseline even for co-managed clients**.



## Enable distribution points to use network congestion control
<!--1358112-->

Windows Low Extra Delay Background Transport (LEDBAT) is a feature of Windows Server to help manage background network transfers. For distribution points running on supported versions of Windows Server, you can enable an option to help adjust network traffic. Clients only use network bandwidth when it's available. 

For more information on Windows LEDBAT, see the [New transport advancements](https://blogs.technet.microsoft.com/networking/2016/07/18/announcing-new-transport-advancements-in-the-anniversary-update-for-windows-10-and-windows-server-2016/) blog post.


### Prerequisites
- A distribution point on Windows Server, version 1709.  

- A client device running at least Windows 10, version 1607.


### Try it out!
 Try to complete the tasks. Then send [Feedback](#bkmk_feedback) letting us know how it worked.

1. In the Configuration Manager console, go to the **Administration** workspace. Select the **Distribution Points** node. Select the target distribution point, and click **Properties** in the ribbon.  

2. On the **General** tab, enable the option to **Adjust the download speed to use the unused network bandwidth (Windows LEDBAT)**.  



## CMTrace installed with client
<!--1357971-->

The CMTrace log viewing tool is now automatically installed along with the Configuration Manager client. It's added to the client installation directory, which by default is `%WinDir%\ccm\cmtrace.exe`.

> [!Note]  
> CMTrace is *not* automatically registered with Windows to open the .log file extension.



## Improvement to the Configuration Manager console
<!--1358202-->
We've made the following improvement to the Configuration Manager console:

- Device lists under Assets and Compliance, Devices, now by default display the currently logged on user. This value is as current as the [client status](/sccm/core/clients/manage/monitor-clients#bkmk_indStatus). The value is cleared when the user logs off. If no user is logged on, the value is blank. 



## Improvements to console feedback
<!--1357542-->
This release includes the following improvements to the new [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) mechanism in the Configuration Manager console:  

- The feedback dialog now remembers your previous settings, such as the selected options and your email address.  

- It now supports offline feedback. Save your feedback from the console, and then upload to Microsoft from an internet-connected system. Use the new offline feedback uploader tool located in `cd.latest\SMSSETUP\Tools\UploadOfflineFeedback\UploadOfflineFeedback.exe`. To see the available and required command-line options, run the tool with the `--help` option. The connected system needs access to **petrol.office.microsoft.com**.



## Improvements to PXE-enabled distribution points
<!--1357580-->

This release includes the following additional improvements when you use the option to [**Enable a PXE responder without Windows Deployment Service**](/sccm/core/get-started/capabilities-in-technical-preview-1802#improvements-to-pxe-enabled-distribution-points) on a distribution point:  

- Windows Firewall rules are automatically created on the distribution point when you enable this option  
- Improvements to component logging



## Improvement to hardware inventory for large integer values
<!--1357880-->
Hardware inventory currently has a limit for integers larger than 4,294,967,296 (2^32). This limit can be reached for attributes such as hard drive sizes in bytes. The management point doesn't process integer values above this limit, thus no value is stored in the database. Now in this release the limit is increased to 18,446,744,073,709,551,616 (2^64). 

For a property with a value that doesn't change, like total disk size, you may not immediately see the value after upgrading the site. Most hardware inventory is a delta report. The client only sends values that change. To work around this behavior, add another property to the same class. This action causes the client to update all properties in the class that changed. 



## Improvement to WSUS maintenance
<!--1357898-->

The WSUS cleanup wizard now declines updates that are either expired or superseded according to the supersedence rules. These rules are defined on the software update point component properties.

### Try it out!
Try to complete the tasks. Then send [Feedback](capabilities-in-technical-preview-1804.md#bkmk_feedback) letting us know how it worked.

1. In the Configuration Manager console, go to the **Administration** workspace. Expand **Site Configuration** and select **Sites**. Select the top-level site, click **Configure Site Components** in the ribbon, and select **Software Update Point**.  

2. Switch to the **Supersedence Rules** tab. Enable the option to **Run WSUS cleanup wizard**. Specify the desired supersedence behavior.  

3. Review the WSyncMgr.log file.



## Improvement to support for CNG certificates
<!--1357314-->
In this release, use [CNG certificates](/sccm/core/plan-design/network/cng-certificates-overview) for the following additional HTTPS-enabled server roles:  
- Certificate registration point, including the NDES server with the Configuration Manager policy module



## Next steps
For information about installing or updating the technical preview branch, see [Technical Preview for System Center Configuration Manager](/sccm/core/get-started/technical-preview).    
