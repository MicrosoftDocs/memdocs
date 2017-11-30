---
title: "Capabilities in Technical Preview 1606"
titleSuffix: "Configuration Manager"
description: "Learn about features available in the Technical Preview for System Center Configuration Manager, version 1606."
ms.custom: na
ms.date: 01/23/2017
ms.prod: configuration-manager
ms.technology:
  - configmgr-other
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 134a2f60-811e-4dc9-a8f5-1ce0018c5c12
caps.latest.revision: 31
author: erikjems.author: erikjemanager: angrobe
---
# Capabilities in Technical Preview 1606 for System Center Configuration Manager*Applies to: System Center Configuration Manager (Technical Preview)*
This article introduces the features that are available in the Technical Preview for System Center Configuration Manager, version 1606. You can install this version to update and add new capabilities to your Configuration Manager technical preview site.      Before installing this version of the technical preview, review the introductory topic, [Technical Preview for System Center Configuration Manager](../../core/get-started/technical-preview.md), to become familiar with general requirements and limitations for using a technical preview, how to update between versions, and how to provide feedback about the features in a technical preview.    

**Known Issues in this Technical Preview:**  
*  When you update from Technical Preview 1604 to 1605, and then to version 1606, the update might fail and an error similar to the following is logged in the **cmupdate.log**:

       ERROR: Failed to execute SQL Server command:  ~ ~-- Create site boundary group ~IF  dbo.fnIsCasOrStandalonePrimary() = 1 ~BEGIN ~   PRINT N'Create site boundary group during upgrade' ~   EXEC dbo.spBuildDefaultBoundaryGroups @UserName = N'SYSTEM' ~END          

    If this occurs, in the **Updates and Servicing** node click **Check for updates**, and then **Retry** the update installation.
    ***

**The following are new features you can try out with this version.**  

## <a name="dmp_category"></a> Automatically categorize devices into collections
You can create device categories, which can be used to automatically place devices in device collections when you are using Configuration Manager with Microsoft Intune. Users are then required to choose a device category when they enroll a device in Intune. You can additionally change the category of a device from the Configuration Manager console.

**Important:** This capability works with the **June 2016** release of Microsoft Intune. Ensure that you have been updated to this release before you try out these procedures.

### Try it out!

### Create a set of device categories
1.  In the **Assets and Compliance** workspace of the Configuration Manager console, expand **Overview**, then click **Device Collections**.
2.  On the **Home** tab, in the **Categories** group, click **Manage Device Categories**.
3.  In the **Manage Device Categories** dialog box, you can create, edit, or remove categories. Try creating a new category.

### Associate a collection with a device category
When you associate a collection with a device category, all devices in the category you specify will be added to that collection.
1.  In the **Properties** dialog for a device collection, click **Add Rule** > **Device Category Rule**.
2.  In the **Create Device Category Membership Rule** dialog box, select the category that will be applied to all devices in the collection.
3.  Close the **Create Device Category Membership Rule** dialog box and the collection properties dialog box.

### Change the category of a device
1.  In the **Assets and Compliance** workspace of the Configuration Manager console, expand **Overview**, then click **Devices**.
2.  Select a device from the **Devices** list and then, in the **Home** tab, in the **Device** group, click **Change Category**.
3.  In the **Edit Device Category** dialog box, choose the category to apply to this device, then click **OK**.

## <a name="dmp_grace"></a> Enforcement grace period for required application and software update deployments

In some cases, you might want give users more time to install required application deployments or software updates beyond any deadlines you configured. This might typically be required when a computer has been turned off for an extended period of time and needs to install a large number of application or update deployments.
For example, if an end user has just returned from vacation, they might have to wait for a long while as overdue application deployments are installed.
To help solve this problem, you can now define an enforcement grace period by deploying Configuration Manager client settings to a collection.

### Try it out!

To configure the grace period, take the following actions:

1.  On the **Computer Agent** page of client settings, configure the new property **Grace period for enforcement after deployment deadline (hours)** with a value between **1** and **120** hours.
2.  In a new required application deployment, or in the properties of an existing deployment, on the **Scheduling** page, select the checkbox **Delay enforcement of this deployment according to user preferences**, up to the grace period defined in client settings.
All deployments that have this check-box selected and are which are targeted to devices to which you also deployed the client setting will use the enforcement grace period.

If you configure an enforcement grace period and select the checkbox, once the application install deadline is reached, it will be installed in the first non-business window that the user configured up to that grace period. However, the user can still open Software Center and install the application at any time they want. Once the grace period expires, enforcement reverts to normal behavior for overdue deployments.
Similar options have been added to the software updates deployment wizard, automatic deployment rules wizard, and properties pages.

##  <a name="dmp_devg"></a>Using Configuration Manager as a managed installer with Device Guard

Device Guard is a Windows 10 feature that uses hardware and software features to strictly control what is allowed to run on the device.

You can read a detailed overview of what Device Guard does, and how it works at [this Technet article](https://technet.microsoft.com/itpro/windows/whats-new/device-guard-overview).

In this release, Configuration Manager can interoperate with Device Guard and [Windows AppLocker](https://technet.microsoft.com/library/dd723678(v=ws.10).aspx) so that executable and DLL files that are deployed with Configuration Manager are automatically trusted as they come from a Managed Installer, meaning that they will be allowed to run on the target device and other software will not be allowed to run unless explicitly allowed to run by other AppLocker rules.  

At present, this capability is not configurable from the Configuration Manager console. To configure the policy requires you to configure a registry key on each client, and configure Windows services on the client.
Once this is done, configure the AppLocker policy file. After you configure the policy file, you can deploy it to any compatible client device.


Like all AppLocker policies, policies with Managed Installer rules can run in two modes:

- Audit mode – Applications are note prevented from running, but any applications that would have been blocked are reported in a log file (This will be supported in a later release of Configuration Manager).
- Enforcement enabled – Applications are blocked from running.

Further information about how to use Device Guard with Configuration Manager can be found on the [Enterprise Mobility and Security blog](https://blogs.technet.microsoft.com/enterprisemobility/2016/06/20/configmgr-as-a-managed-installer-with-win10).

Further reading:

- [Device Guard introduction](https://technet.microsoft.com/itpro/windows/keep-secure/introduction-to-device-guard-virtualization-based-security-and-code-integrity-policies)
- [Device Guard certification and compliance](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-certification-and-compliance)
- [Device Guard deployment guide](https://technet.microsoft.com/itpro/windows/keep-secure/device-guard-deployment-guide)

 ##  <a name="dmp_onprem"></a> Multiple device management points for On-premises Mobile Device Management  
 With Technical Preview 1606, On\-premises Mobile Device Management (MDM) supports a new capability in Windows 10 Anniversary Update that automatically configures an enrolled device to have more than one device management point available for use. This capability allows the device to fallback to another device management point when the one it normal uses is not available. This capability only works for PCs with Windows 10 Anniversary Update installed.  

### Try it out!  

1.  Install more than one device management point in your hierarchy.  

2.  Enroll a  Windows 10 Anniversary Update device for On\-premises Mobile Device Management.  

For information on how to prepare your site and enroll devices for On\-premises Mobile Device Management, see [Manage mobile devices with on-premises infrastructure in System Center Configuration Manager](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md).  

## <a name="cloud_proxy"></a>Cloud Proxy Service for managing clients on the Internet

Cloud Proxy Service provides a simple way to manage Configuration Manager clients on the Internet. The service, which is deployed to Microsoft Azure and requires an Azure subscription, connects to your on-premises Configuration Manager infrastructure using a new role called the cloud proxy connector point. Once it's completely deployed and configured, clients will be able to access on-premises Configuration Manager site system roles regardless of whether they're connected to the internal private network or on the Internet.

You use the Configuration Manager console to deploy the service to Azure, add the cloud proxy connector point role, and configure site system roles to allow cloud proxy traffic. Cloud Proxy Service currently only supports the management point, distribution point, and software update point roles.

Client certificates and Secure Socket Layer (SSL) certificates are required to authenticate computers and encrypt communications between the different layers of the service. Client computers typically receive a client certificate through group policy enforcement. To encrypt the traffic between clients and site system server hosting the roles, you need to create a custom SSL certificate from the CA. In addition to these two types of certificates, you also need set up a management certificate on Azure that allows Configuration Manager to deploy Cloud Proxy Service.  

### Requirements for Cloud Proxy Service in TP 1606
- Client computers and the site system server running the cloud proxy connector point.
- Custom SSL certificates from the internal CA - used to encrypt communication from the client computers and authenticate the identity of Cloud Proxy Service.
- Azure subscription for cloud services.
- Azure management certificate - used to authenticate Configuration Manager with Azure.

### Limitations of Cloud Proxy Service in TP 1606

- Only supports the management point, distribution point, and software update point roles.
- User policies are not supported.
- Cannot be used with [On-premises Mobile Device Management](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md) in Configuration Manager.
- Only supported on the Azure's public cloud platform.


### Try it out!

The process for deploying Cloud Proxy Service includes the following steps:

1. Create and issue a custom SSL certificate for Cloud Proxy Service.
1. Export the client certificate's root.
2. Upload the management certificate to Azure.
3. Set up Cloud Proxy Service in the Configuration Manager console.
4. Configure the primary site to use client certificate authentication.
5. Add the cloud proxy connector point to your site.
6. Configure the site system roles to accept cloud proxy traffic.

The following sections provide more information for completing these steps.

#### Create a custom SSL certificate

You can create a custom SSL certificate for Cloud Proxy Service in the same way you would do it for a cloud-based distribution point. Follow the instructions for [Deploying the Service Certificate for Cloud-Based Distribution Points](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012) but do the following things differently:

* When setting up the new certificate template, give **Read** and **Enroll** permissions to the security group that you set up for Configuration Manager servers.

#### Export the client certificate's root

The easiest way to get export the root of the client certificates used on the network, is to open a client certificate on one of the domain-joined machines that has one and copy it.

>[!NOTE]
>Client certificates are required on any computer you want to manage with Cloud Proxy Service and on the site system server hosting the cloud proxy connector point. If you need to add a client certificate to any of these machines, see [Deploying the Client Certificate for Windows Computers](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012).

1. In the Run window, type **mmc** and press Return.
2. On the File menu in the management console, click **Add/Remove Snap-in...**.
3. In the Add or Remove Snap-ins dialog box, click **Certificates**, click **Add >**, click **Computer account**, click **Next**, click **Local computer**, and then click **Finish**. Click **OK** to close the dialog box.
4. Go to **Certificates > Personal > Certificates**.
5. Double-click the certificate for client authentication on the computer, click the Certification Path tab, and double-click the root authority (at the top of the path).
6.  Click the Details tab, and click **Copy to File...**.
7. Complete the Certificate Export Wizard using the default certificate format. Make note of the name and location of the root certificate you create. You will need it to configure Cloud Proxy Service in a later step.

#### Upload the management certificate to Azure

An Azure management certificate is required for Configuration Manager to access the Azure API and configure Cloud Proxy Service. For more information and instructions for how to upload a management certificate, see the following articles in the Azure documentation:
- [Certificates overview for Azure Cloud Services](https://azure.microsoft.com/documentation/articles/cloud-services-certs-create/)
- [Upload an Azure Management API Management Certificate](https://azure.microsoft.com/documentation/articles/azure-api-management-certs/).

Make sure to copy the subscription ID associated with the management certificate. You will need it for configuring Cloud Proxy Service in the Configuration Manager console.

#### Set up Cloud Proxy Service

1. In the Configuration Manager console, go to **Administration > Cloud Services > Cloud Proxy Service**.
2. Click **Create Cloud Proxy Service**.
3. In Create Cloud Proxy Service Wizard, enter your Azure subscription ID (copied from the Azure management portal), click Browse, and select the certificate file you used to upload as an Azure management certificate. Click **Next**. Wait a few moments for the console to connect to Azure.
4. Fill out the additional details in the wizard:
    - Specify the private key (.pfx file) that you exported from the custom SSL certificate.
    - Specify the root certificate exported from the client certificate.
    - Specify the same service name FQDN that you used when you created the new certificate template.
    - Clear the box next to **Verify Client Certificate Revocation** (unless you're publicly publishing your CRL information).
    - Click **Next** when you're done.
5. Review the settings, and click **Next**. Configuration Manager starts setting up the service. When the wizard completes, you can click **Close**, however it will take between 5 to 15 minutes to provision the service completely in Azure. Check the **Status** column for the newly setup Cloud Proxy Service to determine when the service is ready.

#### Configure primary site for client certification authentication

1. In the Configuration Manager console, go to **Administration > Site Configuration > Sites**.
2. Select the primary site for the clients you want to manage through Cloud Proxy Service, and click **Properties**.
3. On the Client Computer Communications tab of the primary site property sheet, check the box next to **Use PKI client certificate (client authentication) when available**.
4. Make sure to clear the box next to **Clients check the certificate revocation list (CRL) for site systems**. This option would only be required if you were publicly publishing your CRL.
5. Click **OK**.

#### Add the cloud proxy connector point

The cloud proxy connector point is a new site system role for communicating with Cloud Proxy Service. To add the cloud proxy connector point, follow the instructions in [Add site system roles for System Center Configuration Manager](../../core/servers/deploy/configure/add-site-system-roles.md).

#### Configure roles for cloud proxy traffic

The final step in setting up Cloud Proxy Service is to configure the site system roles to accept cloud proxy traffic. For Tech Preview 1606, only the management point, distribution point, and software update point roles are supported for Cloud Proxy Service. You must configure each role separately.

1. In the Configuration Manager console, go to **Administration > Site Configuration > Servers and Site System Roles**.
2. Click the site system server for the role you want to configure for cloud proxy traffic.
3. Click the role, and then click **Properties**.
4. In the role Properties sheet, under Client Connections, choose **HTTPS**, check the box next to **Allow Configuration Manager Cloud Proxy traffic**, and then click **OK**. Repeat these steps for the remaining roles.

#### Check status on a client on the Internet

After the service and roles are completely configured, internal clients will get the location of Cloud Proxy Service on the next location request. Clients with updated location information can then communicate with Configuration Manager on the Internet. The polling cycle for location requests is every 24 hours. If you don't want to wait for the normally scheduled location request, you can force the request by restarting the SMS Agent Host service (ccmexec.exe) on the computer.

After clients have the new location information for Cloud Proxy Service, try checking the status of clients that are no longer on the internal private network but have Internet access. You can also monitor traffic on Cloud Proxy Service by going to **Administration > Cloud Services > Cloud Proxy Service**, selecting the service in the list pane, and viewing the traffic information in the details pane.   

## <a name="manage_o365"></a>Manage the Office 365 client agent in Configuration Manager  

Starting Technical Preview 1606, you can use a Configuration Manager client agent setting, instead of group policy, to enable Office 365 clients to receive updates from Configuration Manager. After you configure this setting and deploy Office 365 updates, the Configuration Manager client agent communicates with the Office 365 client agent to download Office 365 updates from a distribution point and install them. Configuration Manager also takes inventory of the client agent setting.

For more information, see [Manage Office 365 ProPlus updates](https://technet.microsoft.com/library/mt741983.aspx).

### Set the Configuration Manager client setting to manage the Office 365 client agent
1.  In the Configuration Manager console, click **Administration** > **Overview** > **Client Settings**.
2. Open the appropriate device settings to enable the client agent. For more information about default and custom client settings, see [How to configure client settings in System Center Configuration Manager](../../core/clients/deploy/configure-client-settings.md).
3. Click **Software Updates** and select **Yes** for the **Enable management of the Office 365 Client Agent** setting.  


## <a name="osdpreservedriveletter"></a>The OSDPreserveDriveLetter task sequence variable has been deprecated
The OSDPreserveDriveLetter task sequence variable determines whether or not the task sequence uses the drive letter captured in the operating system image WIM file when applying that image to a destination computer.
- This task sequence variable has been deprecated in Technical Preview 1606.

During an operating system deployment, by default, Windows Setup now determines the best drive letter to use (typically C:). If you want to specify a different drive to use, you can change the location in the Apply Operating System task sequence step. Go to the **Select the location where you want to apply this operating system** setting, select **Specific logical drive letter**, and choose the drive that you want to use. There must be a drive assigned with the letter you choose on the destination computer. 

## <a name="updatesandservicing"></a>Changes for the Updates and Servicing Node
With Technical Preview 1606 several changes have been introduced that apply to Updates and Servicing in the Configuration Manager console:
- **Node name change:**

    In the **Monitoring** workspace, the **Site Servicing status** node has been renamed to **Updates and Servicing Status**.
- **More installation status:**

    When you view the update installation status for a site, the console now displays separate details for the following actions:
    - **Download**  (This applies only to the top-tier site where the service connection point site system role is installed)
    - **Replication**
    - **Prerequisites Check**
    - **Installation**

  Additionally, there is now more detailed information for each step, including in which log file you can view for more information.  
-   **New option to retry prerequisite failures:**

    In both the **Administration** and **Monitoring** workspaces, the **Updates and Servicing** node includes a new button on the Ribbon named **Ignore prerequisite warnings**.

    When you install updates without using the option to Ignore prerequisite warnings (from within the Updates Wizard), and that update installation halts with a State of **Prereq warning**, you can then select **Ignore prerequisite warnings** from the ribbon to trigger an automatic continuation of that update install that ignores the prerequisite warnings.  



- **Cleaner view of updates:**

    When you view the **Updates and Servicing** node, you now see only the most recently installed update, and any new updates that are available for you to install. To view previously installed updates, you click the new **History** button which appears in the Ribbon.  

-   **Renamed option for pre-production:**

    In the Updates and Servicing node, the button what was named **Client options** is now renamed to **Promote Pre-production Client**.
