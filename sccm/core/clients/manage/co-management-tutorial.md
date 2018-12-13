---
# required metadata

title: Tutorial - Configure co-management for devices using PKI
titleSuffix: Configuration Manager 
description: Configure co-management of Windows 10 devices for Configuration Manager and Intune. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 12/10/2018
ms.topic: tutorial
ms.prod:
ms.service:  
ms.technology:
ms.assetid: 

# optional metadata
---


# Enable co-management for Microsoft Intune and System Center Configuration Manager

In this tutorial, you’ll set up co-management of your Windows 10 devices.  

With co-management, you can retain your well-established processes for using Configuration Manager to manage PCs in your organization, while investing in the cloud through use of Intune for security and modern provisioning.

This tutorial begins with the premise that you already use Configuration Manager to manage your Windows 10 devices.  

Before we enable co-management from the Configuration Manager console, we'll set up a public SSL certificate as a server authentication certificate and configure Azure and DNS. After we enable co-management, we'll set up Intune to support autoenrollment and to deploy the Configuration Manager client to newly enrolled devices. Configuration Manager can automatically enroll clients into Intune based on the Azure Active Directory (AD) tenant information.

The following are configurations we'll use to simplify the tasks and complexity of enabling co-management:  
- In Configuration Manager, we'll use the Azure Resource Manager deployment for Azure Services. Using this deployument for cloud management removes the need for an Azure management certificate. In Azure, its's Cloud services (classic) that  hosts the cloud management gateway. 
- We'll use Configuration Manager’s Enhanced HTTP feature. This feature first appears as a pre-release feature in version 1806 and is a full feature beginning with 1810. Use of enhanced HTTP removes several certificate requirements.  
- The cloud management gateway we deploy to Azure uses  a server authentication certificate from a trusted third-party provider. Public certificates will already be trusted by Windows 10 devices, further simplifying our tasks. While it's possible to use self-signed certificates, doing so creates complexity and limits access to your cloud-based infrastructure from devices that are on the internet.  
- When we configure the cloud management gateway, we'll also install a cloud distribution point. While a cloud distribution point isn't required, it's almost always of use. We'll use a checkbox option to deploy it with the cloud management gateway which removes the need to configure separate certificates.  


**In this tutorial you will:**
> [!div class="checklist"]
> * Review prerequisites for Azure and your on-premises environment  
> * Configure the PKI environment  
> * Enable Azure services in Configuration Manager  
> * Deploy and configure a cloud management gateway in Azure  
> * Configure clients to use the cloud management gateway  
> * Enable co-management in Configuration Manager 
> * Configure Intune to autoenroll devices and to deploy the Configuration Manager client  


## Prerequisites

 
### Azure services and environment
- Azure Subscription ([free trial](https://azure.microsoft.com/free))  
- Azure Active Directory Premium  

- Microsoft Intune  

- Users who [are assigned licenses for Intune](https://docs.microsoft.com/intune/licenses-assign)  

- *If you use an on-premises domain:* [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-install-select-installation) is configured between your on-premises Active Directory and your Azure Active Directory (AD) tenant

> [!TIP]  
> An Enterprise Mobility + Security (EMS) Subscription includes both Azure Active Directory Premium and Microsoft Intune. EMS Subscription ([free trial](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial)).  


### On-premises infrastructure
- System Center Configuration Manager current branch, version 1810 or later.  

  Version 1810 introduces changes that we use in this tutorial. One is Enhanced HTTP. The second is a change that simplifies the command line for  internet-based installation of the Configuration Manager client.  

- The primary site must be configured to use Configuration Manager-generated certificates for HTTP site systems. For more information, see [Enhanced HTTP](https://docs.microsoft.com/sccm/core/plan-design/hierarchy/enhanced-http).  

- The [MDM Authority](https://docs.microsoft.com/sccm/mdm/deploy-use/change-mdm-authority) must be set to Intune.  

### External certificates:
  - CMG server authentication certificate. 
    
    As part of this tutorial you'll request this certificate from a public and globally trusted certificate provider. For example, but not limited to, DigiCert, Thawte, or VeriSign. This certificate will be exported as .PFX file with Private Key. 

    As part of the section [configure your PKI environment](#configure-your-pki-environment), we'll guide you on how to configure the request for this certificate.  

### Permissions
Throughout this tutorial, you'll need the following permissions to complete tasks:  
- An account that is a *global administrator* in Azure  
- An account that is a *domain admin* on your on-premises infrastructure  
- An account that is a *full administrator* for *all* scopes in Configuration Manager  

## Configure your PKI environment
Co-management uses a cloud management gateway (CMG), which requires an SSL certificate. In this tutorial, we use a public certificate called **CMG server authentication certificate** that derives authority from a globally trusted certificate provider. It's possible to configure Co-management using certificates that derive authority from your on-premises Microsoft certificate authority. Using self-signed certificates is beyond the scope of this tutorial.  

The **CMG server authentication certificate** is used to encrypt traffic between the Configuration Manager client and the CMG. The certificate traces back to a Trusted Root to verify the server's identity to the client. The public certificate includes a Trusted Root that is already trusted by Windows clients. 
 
### Identify a unique name for your cloud management gateway in Azure
When you request the CMG server authentication certificate, you specify what must be a unique name to identify your *Cloud service (classic)* in Azure. By default, the Azure public cloud uses *cloudapp.net*, and the CMG is hosted within the cloudapp.net domain as *\<YourUniqueDnsName>.cloudapp.net*.  

> [!TIP]  
> In this tutorial, the **CMG server authentication certificate** uses an FQDN that ends in *contoso.com*.  After we create the CMG we’ll configure a canonical name record (CNAME) in our organization’s public DNS. This record creates an alias for the CMG that maps to the name that we use in the public certificate.  

Before you request your public certificate, confirm the name you want to use is available in Azure. You don't directly create the service in Azure. Instead, the name that's specified in the public certificate you request is used by Configuration Manager to create the cloud service when you install the CMG.  

1. Sign in to the [Microsoft Azure portal](https://portal.azure.com/).  

2. Select **Create a resource**, choose the **Compute** category, then select **Cloud Service**. The Cloud service (classic) blade opens.

3. For **DNS name**, specify the prefix name for the cloud service you will use. This prefix must be the same as what you use later when you request a publish certificate for the CMG server authentication certificate. We use MyCSG, which creates the namespace of *MyCSG.cloudapp.net*. The interface confirms whether the name is available or already in use by another service.

 

After you confirm the name you want to use is available, you're ready to submit the Certificate Signing Request (CSR).

### Request the certificate
Use the following information to submit a certificate signing request for your CMG to a public certificate provider. Change the following values to be relevant to your environment.  

- *MyCMG* to identify the service name of the cloud management gateway
- *Contoso* as the company name
- *Contoso.com* as the public domain

We recommend you use your primary site server to generate the certificate signing requests (CSR). When you get the certificate, you must enroll it on the same server that generated the CSR or you can't export the certificates private key, which is required.  

Request a version 2 key provider type when you generate a CSR. Only version 2 certificates are supported.  

> [!TIP]  
> When we deploy the CMG, we will also install a cloud distribution point (CDP) at the same time. By default, when you deploy a CMG, the option **Allow CMG to function as a cloud distribution point and serve content from Azure storage** is selected. Co-locating the CDP removes the need for separate certificates and configurations to support the CDP. Even though the CDP isn’t required to use co-management, it is useful in most environments.  
>
> If you will use additional cloud distribution points for co-management, you’ll need to request separate certificates for each additional server. To request a pubic certificate for the CDP, use the same details as for the cloud management gateway CSR. You need only change the common name so that it is unique for each CDP.  

**Details for the cloud management gateway CSR**
- **Common Name**: ClousServiceNameCMG.YourCompanyPubilcDomainName.com  
Example: MyCSG.contoso.com  
- **Subject Alternative Name**: Same as the Common Name (CN)  
- **Organization**:  The name of your organization  
- **Department**: Per your organization  
- **City**: Per your organization  
- **State**: Per your organization  
- **Country**: Per your organization  
- **Key Size: 2048**  
- **Provider: Microsoft RSA SChannel Cryptographic Provider**  

### Import the certificate
After you receive the public certificate, import it to the local certificate store of the computer that created the CSR. Then export the certificate as a .PFX file so you can use it for your CMG in Azure.  

Public certificate providers typically provide instructions for import of the certificate. The process to import the certificate should resemble the following guidance:  

1. On the computer that the certificate is to be imported to, locate the certificate .pfx file.  

2. Right-click the file, and then select **Install PFX**  

3. When the Certificate Import Wizard starts, select **Next**.  

4. On the **File to Import** page, select **Next**. 

5. On the **Password** page, enter the password for the private key in the Password box, and then select **Next**.  
  
   Select the option to make the key exportable.

6. On the **Certificate Store page**, select **Automatically select the certificate store based on the type of certificate**, and then select **Next**.  

7.	Select **Finish**.

### Export the certificate
Export the *CMG server authentication certificate* from your server. Re-exporting the certificate makes it usable for your cloud management gateway in Azure.  

1. On the member server you'll use to manage the cloud-based site system roles, run **certlm.msc** to open the Certificate Manager console.  

2. In the Certificate Manager console, select **Personal > Certificates**. Then, right-click on the *CMG server authentication certificate* you enrolled in the previous procedure, and then select **All Tasks > Export**.  

3. In the Certificate Export Wizard, select **Next**, select **Yes, export the private key**, and then **Next**.  

4. On the Export File Format page, select **Personal Information Exchange - PKCS #12 (.PFX)**, select **Next**, and provide a password. For file name, specify a name like **C:\ConfigMgrCloudMGServer**. You’ll reference this file when you create the CMG in Azure.  

5. Select **Next**, and then confirm the following settings before selecting **Finish** to complete the export:  

   - Export Keys = Yes  
   - Include all certificates in the certification path = Yes  
   - File format = Personal Information Exchange (*.pfx)  

6. After you complete the export, locate the .pfx file and place a copy of it on the Configuration Manager primary site server in **C:\Certs**. The Certs folder is a temporary folder to use while moving certificates between servers. You'll need to access the certificate file from the primary site server when you deploy the cloud management gateway to Azure.  

After you copy the certificate to the primary site server, you can delete the Certificate from the Personal Certificate store on the member server. 

## Enable Azure cloud services in Configuration Manager
To configure Azure services from within the Configuration Manager console, you use the Configure Azure Services wizard and create two Azure Active Directory (Azure AD) apps.  

- **Server app** –  a *Web app* in Azure AD  
- **Client app** – a *Native Client* app in Azure AD  

Run the following procedure from the primary site server that has your exported certificate.  

1. From the primary site server, open the Configuration Manager console and go to **Administration > Cloud Services > Azure Services**, and select **Configure Azure Services**.  

   On the Configure Azure Service page, specify a friendly Name for the cloud management service you’re configuring. For example: *My cloud management gateway*   

   Then select **Cloud Management**, and then select **Next**.  
   
   > [!TIP]  
   > For more information about the configurations you make in the wizard, see [Start the Azure Services wizard](https://docs.microsoft.com/sccm/core/servers/deploy/configure/Azure-services-wizard#start-the-azure-services-wizard)


2. On the **App Properties** page, for **Web app**, select **Browse** to open the **Server App** dialog, and then select **Create**. Configure the following fields:

   - **Application Name**: Specify a friendly name for the app, like *Cloud Management web app*.  

   - **HomePage URL**: This value isn't used by Configuration Manager but is required by Azure AD. By default, this value is https://ConfigMgrService.  
   
   - **App ID URI**: This value needs to be unique in your Azure AD tenant. It is in the access token used by the Configuration Manager client to request access to the service. By default, this value is https://ConfigMgrService.  

   Next, select **Sign in**, and specify an Azure Global Admin account. These credentials aren't saved by Configuration Manager. This persona doesn't require permissions in Configuration Manager and doesn't need to be the same account that runs the Azure Services Wizard. 

   After you sign in, the results display. Select **OK** to close the Create Server Application dialog and return to the App Properties page. 

3. For **Native Client app**, select **Browse** to open the **Client app** dialog. 

4. Select **Create** to open the **Create Client Application** dialog, and then configure the following fields:  

   - **Application Name**: Specify a friendly name for the app, like *Cloud Management native client app*.
   
   - **Reply URL**: This value isn't used by Configuration Manager, but required by Azure AD. By default, this value is https://ConfigMgrClient.
   Next, select **Sign in**, and specify an Azure Global Admin account. Like the Web app, these credentials aren't saved and don't require permissions in Configuration Manager.
   
   After you sign in, the results are display. Select **OK** to close the Create Client Application dialog and return to the App Properties page. Then, select **Next** to continue.

5. On the **Configure Discovery Settings** page, check the box for **Enable Azure Active Directory User Discovery**, select **Next**, and then complete configuration of the Discovery dialogs for your environment.  

6. Continue through the Summary, Progress, and Completion pages, to complete and then close the wizard.  

   Azure Services for Azure AD User discovery is now enabled in Configuration Manager.  Leave the console open for now.  

7. Open a browser and sign in to the [Azure portal](https://portal.azure.com/).  

8. Select **All services > Azure Active Directory > App registrations**, and then:

   1. Select the Web app you created. 

   2. Go to **Settings > Required permissions**, select **Grant permissions**, and then select **Yes**.  

   3. Select the Native Client app you created. 

   4. Go to **Settings > Required permissions**, select **Grant permissions**, and then select **Yes**.  

9. In the Configuration Manager console, go to **Administration > Overview > Cloud Services > Azure Services**, and select your Azure Service. Then right-click on **Azure Active Directory User Discover** and select **Run Full Discovery Now**. Select **Yes** to confirm the action.  

10. On the primary site server, open the Configuration Manager **SMS_AZUREAD_DISCOVERY_AGENT.log** and look for the following entry to confirm that discovery is working:  *Successfully published UDX for Azure Active Directory users*  

    By default, the log file is in *%Program_Files%\Microsoft Configuration Manager\Logs*.  


## Create the cloud services in Azure
**In this section of the tutorial you will**:
- Create the CMG cloud service  

- Create DNS CNAME records for both services  

### Create the CMG
Use this procedure to install a cloud management gateway as a service in Azure. The CMG installs at the top-tier site of the hierarchy. In this tutorial, we continue to use a primary site, where certificates have been enrolled and exported.  

1. On the primary site server, open the Configuration Manager console, and then go **Administration > Overview > Cloud Services > Cloud Management Gateway**, and then select **Create Cloud Management Gateway**.  

2. On the **General** page:  

   1. Select your cloud environment for **Azure environment**. This tutorial uses **AzurePublicCloud**.  
   
   2. Select **Azure Resource Manager deployment**.  
  
   3. **Sign in** to your Azure subscription. Configuration Manager fills in additional information based on the information you configured when you enabled Azure cloud services for Configuration Manager.  

   Select **Next** to continue.  

3. On the **Settings** page, browse to and select the file named **ConfigMgrCloudMGServer.pfx**, which is the file you exported after importing the CMG server authentication certificate. After you specify the password, the **Service name** and **Deployment name** automatically fill in, based on the details in the .pfx certificate file. 

4. set your **Region**.

5. For **Resource Group**, use an existing resource group or create a new group with a friendly name that uses no spaces, like **CofigMgrCloudServices**. If you choose to create a new group, the group is added as a resource group in Azure.  

6. Unless you're ready to configure at scale, use one (1) for the number of **VM Instances**. The number of VM Instances allows a single Cloud Management Gateway (CMG) Cloud service to scale out to support more client connections. Later, you can use the Configuration Manager console to return and edit the number of VM instances you use.  

7. Enable the checkbox for **Verify Client Certificate Revocation**. 

8. Enable the checkbox for **Allow CMG to function as a cloud distribution point and serve content from Azure storage** if you want to deploy a cloud distribution point with the CMG.

9. Select **Next** to continue.

10. Review the values on the **Alert** page, and then select **Next**.

11. Review the **Summary** page and click **Next** to create the cloud management gateway Cloud Service. Select **Close** to complete the Wizard.  

12. In the Cloud Management Gateway node of the Configuration Manager console, you can now view the new service.  

### Create DNS CNAME records

Create a DNS CNAME entry for the CMG service in Azure. The DNS entry enables your Windows 10 devices both inside and outside your corporate network to use name resolution to find the cloud service in Azure.  

Our CNAME record example uses the following details:  

- The company name is **Contoso** with a public DNS namespace of ***Contoso.com***.  

- The CMG service name is **MyCMG**, which becomes ***MyCMG.CloudApp.Net*** in Azure.  

CNAME record example: *MyCMG.contoso.com => My.cloudapp.net*

## Configure the management point and clients to use the CMG
Configure settings that enable management points and clients to use the cloud management gateway.  

There's no need to configure an HTTPS management point as we're using Enhanced HTTP for client communications. [Azure AD-joined devices](https://docs.microsoft.com/azure/active-directory/device-management-introduction#azure-ad-joined-devices) can communicate with a management point configured for *Client Computer Communication*. 

### Create the CMG connection point
Configure the site to support Enhanced HTTP.  

1. In the Configuration Manager console, go to **Administration > Overview > Site Configuration > Sites**, and open the properties of the primary site.  

2. On the **Client Computer Communication** tab, select the *HTTPS or HTTP* option for **Use Configuration Manager-generated certificates for HTTP site systems**, and then select **OK** to save the configuration. 

3. Now go to **Administration > Overview > Site Configuration > Servers and Site System Roles** and select the server with a management point on which you want to install the cloud management gateway connection point.  

4. Select **Add Site System Roles**, and then **Next**> **Next**.  

5.  Select the **Cloud management gateway connection point** and then select **Next** to continue.  

7. Review the default selections on the **Cloud management gateway connection point** page and make sure the correct CMG is selected. If you have multiple cloud management gateways, you can use the dropdown list to specify a different CMG. You can also change the CMG in use, after installation. Select **Next** to continue.

8. Select **Next** to start installation and then view the results on the Completion page.  Select **Close** to complete the installation.




### Configure Client Settings to direct clients to use the CMG
Use Client Settings to configure Configuration Manager clients to communicate with the CMG.  

1.	Open the **Configuration Manager console > Administration > Overview > Client Settings**, and then edit the **Default Client Settings**.  

2.	Select **Cloud Services**.

3.	On the **Default Settings** page, set the following settings to = **Yes**  

    - Automatically register new Windows 10 domain joined devices with Azure Active Directory  

    - Enable clients to use a cloud management gateway  

    - Allow access to cloud distribution point 


 

4.	Select **OK** to save this configuration.  


## Enable co-management in Configuration Manager
With the Azure configurations, site system roles, and client settings in place, you're ready to flip the switch and enable co-management of your Windows 10 devices.

> [!TIP]  
>  In step six of the following procedure, you'll assign a collection as a *Pilot group* for co-management. This is a group that contains a small number of clients to test your co-management configurations. We recommend you create a suitable collection before you start the procedure. Then you can select that collection without exiting the procedure to do so.  
 

1. In the Configuration Manager console, go to **Administration > Overview > Cloud Services > Co-management**.

2. On the Home tab, in the Manage group, select **Configure co-management** to open the Co-management Configuration Wizard.

3. On the Subscription page, select **Sign In** and sign in to your Intune tenant, and then select **Next**.

4. On the Enablement page, from the *Automatic enrollment in Intune* dropdown list, select one of the following options:  

   - **Pilot**  - *(Recommended)* Members of the collection you specify are automatically enrolled into Intune and can then be co-managed. You'll specify the pilot collection on the *Staging* page of this wizard. This option allows you to test co-management on a subset of clients. You can then roll out co-management to additional clients using a phased approach.  

   - **All** - Co-management is enabled for all clients.  

   Next, select **Copy** to copy the *CCMSETUPCMD* command line. You can use this command line later when you configure Intune to deploy the Configuration manager client. Select **Next**.  

5. On the Workloads page you can switch workloads from **Configuration Manager** to one of the following, and then when ready to continue, select **Next**.  
   
   - **Pilot Intune** - Switches a workload only for the devices in the Pilot group. You’ll assign a collection as the Pilot group on the next page of the wizard.  
   
   - **Intune** - Switches the associated workload for all co-managed Windows 10 devices.  

   You don't need to switch any workloads at the time you enable co-management. You can revisit this configuration from the Configuration Manager console later, after co-management is configured.  

   Before you switch a workload, make sure the corresponding workload in Intune is configured and deployed. Doing so will keep the workloads managed.  

6. On the Staging page, specify a collection to use for the **Pilot collection**, and then click **Next**. The collection you specify is used as part of your phased rollout of co-management. You can change the collections in the pilot group at any time from the co-management properties.  

7. On the Summary page, select **Next**, and then **Close** to complete the Wizard.  

With the completion of this procedure, you’ve enabled co-management and your Azure subscription and on-premises infrastructure is configured to support co-management. You can use the [Co-management dashboard](https://docs.microsoft.com/sccm/core/clients/manage/co-management-dashboard) to review the status of co-managed devices.  

## Configure auto-enrollment of devices to Intune   
Next, we’ll set up auto-enrollment of devices with Intune. With automatic enrollment, devices you manage with Configuration Manager will automatically enroll with Intune.

Automatic enrollment also lets users enroll their Windows 10 devices to Intune. Devices enroll when a user adds their work account to their personally owned device, or when a corporate-owned device is joined to Azure Active Directory.  
1. Sign in to the [Azure portal](https://portal.azure.com/) and select **Azure Active Directory > Mobility (MDM and MAM) > Microsoft Intune**.  

2. Configure **MDM user scope**. Specify one of the following to configure which users’ devices are managed by Microsoft Intune and accept the defaults for the URL values.  

   - **Some** - Select the **Groups** that can automatically enroll their Windows 10 devices  

   - **All** - All users can automatically enroll their Windows 10 devices
when set to **None**, MDM automatic enrollment is disabled  

   > [!IMPORTANT]  
   > If both **MAM user scope** and automatic MDM enrollment (**MDM user scope**) are enabled for a group, only MAM is enabled. Only MAM is added for users in that group when they workplace join personal device. Devices are not automatically MDM enrolled.  

3. Select **Save** to complete configuration of automatic enrollment.  

4. Return to **Mobility (MDM and MAM)** and then select **Microsoft Intune Enrollment**.  

5. For MDM user scope, select **All**, and then **Save**.  

 
## Use Intune to deploy the Configuration Manager client  
You can use Intune to install the Configuration Manager client on Windows 10 devices that are only managed with Intune. 

Then, when a previously unmanaged Windows 10 device enrolls with Intune, it automatically installs the Configuration Manager client to become co-managed.  


### Create an Intune app to install the Configuration Manager client
1. From the primary site server, sign in to the [Azure portal](https://portal.azure.com/) and go to the **Intune > Client apps > Apps > Add**.

2. For **App type**: Select **Line-of-business app**.

3. Select **App package file**, and then browse to the location of the Configuration Manager file  **ccmsetup.msi**, and then select **Open > OK**.
For example, *C:\Program Files\Microsoft Configuration Manager\bin\i386\ccmsetup.msi*   

4. Select **App Information**, and then specify the following details:
   - **Description**: Configuration Manager Client  

   - **Publisher**: Microsoft  

   - **Command-line arguments**:  *\<Specify the **CCMSETUPCMD** command line. You can use the command line you saved from the* Enablement *page of the Co-management Configuration Wizard. This command line includes the names of your cloud service and additional values that will enable devices to install the Configuration Manager client software.>*  

     The command-line structure should resemble this example using only the CCMSETUPCMD and SMSSiteCode parameters:  
 
         CCMSETUPCMD="CCMHOSTNAME=<ServiceName.CLOUDAPP.NET/CCM_Proxy_MutualAuth/<GUID>" SMSSiteCode="<YourSiteCode>"  

     > [!TIP]  
     > If you do not have the command line available, you can view the properties of *CoMgmtSettingsProd* in the Configuration Manager console to get a copy of the command line.    

5. Select **OK > Add**.  The app is created and becomes available in the Intune console. After the app is available, you can use the following section to configure Intune to assign it to Windows 10 devices.

### Assign the Intune app to install the Configuration Manager client
The following procedure deploys the app for installing the Configuration Manager client that you created in the previous procedure. After a user’s Windows 10 device that is managed by Intune runs this app to install the Configuration Manager client, the device will be co-managed. 

1. Sign in to the [Azure portal](https://portal.azure.com/).  Select **All services > Intune > Client apps > Apps**, and then select **ConfigMgr Client Setup Bootstrap**, the app you created to deploy the Configuration Manager client.  

2. Select **Assignments > Add group**.  Set **Assignment type** as **Required**, and then use **Included Groups** and **Excluded Groups** to set the Azure Active Directory (AD) groups that have users and devices that you want to participate in co-management.  

3. Select **OK** and then **Save** the configuration.
The app is now required by the users and devices you assigned it to. After the app installs the Configuration Manager client on a device, it's managed by co-management.  


## Next Steps
After you complete the configurations for co-management, you can use co-management to manage devices of users when they enroll their devices with Intune (which installs the Configuration Manager client), or when they sign in to the company portal on a domain joined computer that runs the Configuration Manager client.  

This tutorial for configuring co-management is complete.  

- View the [Co-management dashboard](https://docs.microsoft.com/sccm/core/clients/manage/co-management-dashboard) to review the status of co-managed devices
