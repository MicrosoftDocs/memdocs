---
title: Tutorial - Enable co-management for internet devices
titleSuffix: Configuration Manager
description: Learn how to configure co-management for new internet-based Windows 10 or later devices by using Configuration Manager and Microsoft Intune.
author: gowdhamankarthikeyan
ms.author: gokarthi
manager: apoorvseth
ms.date: 08/24/2021
ms.topic: tutorial
ms.subservice: co-management
ms.service: configuration-manager
ms.localizationpriority: medium
#Customer intent: As a Configuration Manager admin, I want enable co-management so I can manage some client workloads from Intune and others from Configuration Manager.
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Tutorial: Enable co-management for new internet-based devices

When you're investing in the cloud through the use of Intune for security and modern provisioning, you might not want to lose your well-established processes for using Configuration Manager to manage PCs in your organization. With co-management, you can keep that process in place.

In this tutorial, you set up co-management of Windows 10 or later devices in an environment where you use both Microsoft Entra ID and on-premises Active Directory but don't have a [hybrid Microsoft Entra ID](/azure/active-directory/devices/concept-azure-ad-join-hybrid) instance. The Configuration Manager environment includes a single primary site with all site system roles located on the same server, the site server. This tutorial begins with the premise that your Windows 10 or later devices are already enrolled with Intune.

If you have a hybrid Microsoft Entra instance that joins on-premises Active Directory with Microsoft Entra ID, we recommend following our companion tutorial, [Enable co-management for Configuration Manager clients](tutorial-co-manage-clients.md).

Use this tutorial when:
  
- You have Windows 10 or later devices to bring into co-management. These devices might have been provisioned through Windows Autopilot or might be direct from your hardware OEM.
- You have Windows 10 or later devices on the internet that you currently manage with Intune, and you want to add the Configuration Manager client to them.

In this tutorial, you will:  
> [!div class="checklist"]  
> * Review prerequisites for Azure and your on-premises environment.
> * Request a public SSL certificate for the cloud management gateway  (CMG).
> * Enable Azure services in Configuration Manager.
> * Deploy and configure a CMG.  
> * Configure the management point and clients to use the CMG.
> * Enable co-management in Configuration Manager.
> * Configure Intune to install the Configuration Manager client.

## Prerequisites  

### Azure services and environment

- Azure subscription ([free trial](https://azure.microsoft.com/free)).
- Microsoft Entra ID P1 or P2.
- Microsoft Intune subscription, with Intune configured to [auto-enroll devices](tutorial-co-manage-clients.md#configure-auto-enrollment-of-devices-to-intune).

  > [!TIP]  
  > An Enterprise Mobility + Security subscription [free trial](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-trial) includes both Microsoft Entra ID P1 or P2 and Microsoft Intune.  
  >
  > You no longer need to purchase and assign individual Intune or Enterprise Mobility + Security licenses to your users. For more information, see [Product and licensing FAQ](../core/understand/product-and-licensing-faq.yml#what-changes-with-licensing-for-co-management-in-the-microsoft-intune-family-of-products-).

### On-premises infrastructure

- A supported version of Configuration Manager current branch.
  
  This tutorial uses [enhanced HTTP](../core/plan-design/hierarchy/enhanced-http.md) to avoid more complex requirements for a public key infrastructure. When you use enhanced HTTP, the primary site that you use to manage clients must be configured to use Configuration Manager-generated certificates for HTTP site systems.

- Mobile device management (MDM) authority set to Intune.

### External certificates

- CMG server authentication certificate. This SSL certificate is from a public and globally trusted certificate provider.<!-- memdocs#1668 --> You'll export this certificate as a .pfx file with the private key.  

  Later in this tutorial, we provide guidance on how to configure the request for this certificate.

### Permissions

Throughout this tutorial, use the following permissions to complete tasks:

- An account that's a *Global Administrator* for Microsoft Entra ID
- An account that's a *Domain Administrator* on your on-premises infrastructure  
- An account that's a *Full Administrator* for *all* scopes in Configuration Manager

## Request a public certificate for the cloud management gateway

When your devices are on the internet, co-management requires the Configuration Manager CMG. The CMG enables your internet-based Windows devices to communicate with your on-premises Configuration Manager deployment. To establish a trust between devices and your Configuration Manager environment, the CMG requires an SSL certificate.

This tutorial uses a public certificate called a *CMG server authentication certificate* that derives authority from a globally trusted certificate provider. Although it's possible to configure co-management by using certificates that derive authority from your on-premises Microsoft certificate authority, use of self-signed certificates is beyond the scope of this tutorial.

The CMG server authentication certificate is used to encrypt the communications traffic between the Configuration Manager client and the CMG. The certificate traces back to a trusted root to verify the server's identity to the client. The public certificate includes a trusted root that Windows clients already trust.

About this certificate:

- You identify a unique name for your CMG service in Azure and then specify that name in your certificate request.  
- You generate your certificate request on a specific server and then submit the request to a public certificate provider to get the necessary SSL certificate.  
- You import the certificate that you receive from the provider to the system that generated the request. You use the same computer to export the certificate when you later deploy the CMG to Azure.  
- When the CMG is installed, it creates a CMG service in Azure by using the name that you specified in the certificate.  

### Identify a unique name for your cloud management gateway in Azure

we are no longer allowing customers to opt-in for classic cloud services CMG, this area should be updated with VMSS based CMG information for users to understand them easily.

When you request the CMG server authentication certificate, you specify what must be a unique name to identify your cloud service (classic) in Azure. By default, the Azure public cloud uses *cloudapp.net*, and the CMG is hosted within the *cloudapp.net* domain as *\<YourUniqueDnsName>.cloudapp.net*.  

> [!TIP]  
> In this tutorial, the CMG server authentication certificate uses a fully qualified domain name (FQDN) that ends in *contoso.com*.  After you create the CMG, you'll configure a canonical name record (CNAME) in your organization's public DNS. This record creates an alias for the CMG that maps to the name that you use in the public certificate.  

Before you request your public certificate, confirm that the name you want to use is available in Azure. You don't directly create the service in Azure. Instead, Configuration Manager uses the name that's specified in the public certificate to create the cloud service when you install the CMG.  

1. Sign in to the [Microsoft Azure portal](https://portal.azure.com/).  

2. Select **Create a resource**, select the **Compute** category, and then select **Cloud Service**. The **Cloud service (classic)** page opens.

3. For **DNS name**, specify the prefix name for the cloud service that you'll use. 

   This prefix must be the same as what you use later when you request a public certificate for the CMG server authentication certificate. In this tutorial, we use *MyCSG*, which creates the namespace of *MyCSG.cloudapp.net*. The interface confirms whether the name is available or already in use by another service.  

After you confirm the name that you want to use is available, you're ready to submit the certificate signing request (CSR).

### Request the certificate

Use the following information to submit a certificate signing request for your CMG to a public certificate provider. Change the following values to be relevant to your environment:  

- *MyCMG* to identify the service name of the cloud management gateway
- *Contoso* as the company name
- *Contoso.com* as the public domain

We recommend that you use your primary site server to generate the CSR. When you get the certificate, you must enroll it on the same server that generated the CSR. This enrollment ensures that you can export the certificate's private key, which is required.  

Request a version 2 key provider type when you generate a CSR. Only version 2 certificates are supported.  

> [!TIP]
> By default, when you deploy a CMG, the option **Allow CMG to function as a cloud distribution point and serve content from Azure storage** is selected. Even though the cloud-based content isn't required to use co-management, it's useful in most environments.
>
> The cloud-based distribution point (CDP) is deprecated. Starting in version 2107, you can't create new CDP instances.<!-- 10247883 --> To provide content to internet-based devices, enable the CMG to distribute content. For more information, see [Deprecated features](../core/plan-design/changes/deprecated/removed-and-deprecated-cmfeatures.md#deprecated-features).

Here are details for the cloud management gateway's CSR:

- **Common Name**: *CloudServiceNameCMG.YourCompanyPubilcDomainName.com* (example: *MyCSG.contoso.com*)  
- **Subject Alternative Name**: Same as the common name (CN)  
- **Organization**:  The name of your organization  
- **Department**: Per your organization  
- **City**: Per your organization  
- **State**: Per your organization  
- **Country**: Per your organization  
- **Key Size**: **2048**  
- **Provider**: **Microsoft RSA SChannel Cryptographic Provider**  

### Import the certificate

After you receive the public certificate, import it to the local certificate store of the computer that created the CSR. Then export the certificate as a .pfx file so you can use it for your CMG in Azure.  

Public certificate providers typically provide instructions for import of the certificate. The process to import the certificate should resemble the following guidance:  

1. On the computer that the certificate will be imported to, locate the certificate .pfx file.  

2. Right-click the file, and then select **Install PFX**.  

3. When the Certificate Import Wizard starts, select **Next**.  

4. On the **File to Import** page, select **Next**.

5. On the **Password** page, enter the password for the private key in the **Password** box, and then select **Next**.  
  
   Select the option to make the key exportable.

6. On the **Certificate Store page**, select **Automatically select the certificate store based on the type of certificate**, and then select **Next**.  

7. Select **Finish**.

### Export the certificate

Export the CMG server authentication certificate from your server. Re-exporting the certificate makes it usable for your cloud management gateway in Azure.  

1. On the server where you imported the public SSL certificate, run **certlm.msc** to open the Certificate Manager console.  

2. In the Certificate Manager console, select **Personal** > **Certificates**. Then, right-click the CMG server authentication certificate that you enrolled in the previous procedure and select **All Tasks** > **Export**.  

3. In the Certificate Export Wizard, select **Next**, select **Yes, export the private key**, and then select **Next**.  

4. On the **Export File Format** page, select **Personal Information Exchange - PKCS #12 (.PFX)**, select **Next**, and provide a password. 

   For the file name, specify a name like **C:\ConfigMgrCloudMGServer**. You'll reference this file when you create the CMG in Azure.  

5. Select **Next**, and then confirm the following settings before selecting **Finish** to complete the export:  

   - **Export Keys**: **Yes**  
   - **Include all certificates in the certification path**: **Yes**  
   - **File format**: **Personal Information Exchange (*.pfx)**  

6. After you complete the export, locate the .pfx file and place a copy of it in *C:\Certs* on the Configuration Manager primary site server that will manage internet-based clients. 

   The *Certs* folder is a temporary folder to use while you're moving certificates between servers. You access the certificate file from the primary site server when you deploy the CMG to Azure.  

After you copy the certificate to the primary site server, you can delete the certificate from the personal certificate store on the member server.

## Enable Azure cloud services in Configuration Manager

To configure Azure services from within the Configuration Manager console, you use the Configure Azure Services Wizard and create two Microsoft Entra apps:  

- **Server app**: A web app in Microsoft Entra ID.  
- **Client app**: A native client app in Microsoft Entra ID.  

Run the following procedure from the primary site server:  

1. Open the Configuration Manager console, go to **Administration** > **Cloud Services** > **Azure Services**, and then select **Configure Azure Services**.  

   On the **Configure Azure Service** page, specify a friendly name for the cloud management service that you're configuring. For example: **My cloud management service**.

   Then select **Cloud Management** > **Next**.  

   > [!TIP]  
   > For more information about the configurations that you make in the wizard, see [Start the Azure Services Wizard](../core/servers/deploy/configure/Azure-services-wizard.md#start-the-azure-services-wizard).

2. On the **App Properties** page, for **Web app**, select **Browse** to open the **Server App** dialog. Select **Create**, and then configure the following fields:

   - **Application Name**: Specify a friendly name for the app, such as **Cloud Management web app**.  

   - **HomePage URL**: Configuration Manager doesn't use this value, but Microsoft Entra ID requires it. By default, this value is `https://ConfigMgrService`.  

   - **App ID URI**: This value needs to be unique in your Microsoft Entra tenant. It's in the access token that the Configuration Manager client uses to request access to the service. By default, this value is `https://ConfigMgrService`. Change the default to one of the following recommended formats:<!-- 10617402 -->

     - `api://{tenantId}/{string}`, for example, `api://5e97358c-d99c-4558-af0c-de7774091dda/ConfigMgrService`
     - `https://{verifiedCustomerDomain}/{string}`, for example, `https://contoso.onmicrosoft.com/ConfigMgrService`

   Next, select **Sign in**, and specify a Microsoft Entra Global Administrator account. Configuration Manager doesn't save these credentials. This persona doesn't require permissions in Configuration Manager and doesn't need to be the same account that runs the Azure Services Wizard.

   After you sign in, the results appear. Select **OK** to close the **Create Server Application** dialog and return to the **App Properties** page.

3. For **Native Client app**, select **Browse** to open the **Client app** dialog.

4. Select **Create** to open the **Create Client Application** dialog, and then configure the following fields:  

   - **Application Name**: Specify a friendly name for the app, such as **Cloud Management native client app**.

   - **Reply URL**: Configuration Manager doesn't use this value, but Microsoft Entra ID requires it. By default, this value is `https://ConfigMgrClient`.
   
   Next, select **Sign in**, and specify a Microsoft Entra Global Administrator account. Like the web app, these credentials aren't saved and don't require permissions in Configuration Manager.

   After you sign in, the results appear. Select **OK** to close the **Create Client Application** dialog and return to the **App Properties** page. Then, select **Next** to continue.

5. On the **Configure Discovery Settings** page, select the **Enable Microsoft Entra user Discovery** checkbox. Select **Next**, and then complete configuration of the **Discovery** dialogs for your environment.  

6. Continue through the **Summary**, **Progress**, and **Completion** pages, and then close the wizard.  

   Azure services for Microsoft Entra user discovery are now enabled in Configuration Manager. Leave the console open for now.  

7. Open a browser and sign in to the [Azure portal](https://portal.azure.com/).  

8. Select **All services** > **Microsoft Entra ID** > **App registrations**, and then:

   1. Select the web app that you created.

   2. Go to **API Permissions**, select **Grant admin consent for** your tenant, and then select **Yes**.  

   3. Select the native client app that you created.

   4. Go to **API Permissions**, select **Grant admin consent for** your tenant, and then select **Yes**.

9. In the Configuration Manager console, go to **Administration** > **Overview** > **Cloud Services** > **Azure Services**, and select your Azure service. Then, right-click **Microsoft Entra user Discover** and select **Run Full Discovery Now**. Select **Yes** to confirm the action.  

10. On the primary site server, open the Configuration Manager *SMS_AZUREAD_DISCOVERY_AGENT.log* file and look for the following entry to confirm that discovery is working: **Successfully published UDX for Microsoft Entra users**.  

    By default, the log file is in *%Program_Files%\Microsoft Configuration Manager\Logs*.  

## Create the cloud service in Azure

In this section of the tutorial, you'll create the CMG cloud service and then create DNS CNAME records for both services.  

### Create the CMG

Use this procedure to install a cloud management gateway as a service in Azure. The CMG is installed at the top-tier site of the hierarchy. In this tutorial, we continue to use the primary site where certificates have been enrolled and exported.

1. On the primary site server, open the Configuration Manager console. Go to **Administration** > **Overview** > **Cloud Services** > **Cloud Management Gateway**, and then select **Create Cloud Management Gateway**.  

2. On the **General** page:  

   1. Select your cloud environment for **Azure environment**. This tutorial uses **AzurePublicCloud**.  

   2. Select **Azure Resource Manager deployment**.  
  
   3. Sign in to your Azure subscription. Configuration Manager fills in additional information based on the information that you configured when you enabled Azure cloud services for Configuration Manager.  

   Select **Next** to continue.  

3. On the **Settings** page, browse to and select the file named *ConfigMgrCloudMGServer.pfx*. This file is the one that you exported after importing the CMG server authentication certificate. After you specify the password, the **Service name** and **Deployment name** information is automatically filled in, based on the details in the .pfx certificate file.

4. Set the **Region** information.

5. For **Resource Group**, use an existing resource group or create a group with a friendly name that uses no spaces, like **ConfigMgrCloudServices**. If you choose to create a group, the group is added as a resource group in Azure.  

6. Unless you're ready to configure at scale, enter **1** for **VM Instances**. The number of virtual machine (VM) instances allows a single CMG cloud service to scale out to support more client connections. Later, you can use the Configuration Manager console to return and edit the number of VM instances that you use.  

7. Select the **Verify Client Certificate Revocation** checkbox.

8. Select the **Allow CMG to function as a cloud distribution point and serve content from Azure storage** checkbox.

9. Select **Next** to continue.

10. Review the values on the **Alert** page, and then select **Next**.

11. Review the **Summary** page and select **Next** to create the CMG cloud service. Select **Close** to complete the wizard.  

12. In the CMG node of the Configuration Manager console, you can now view the new service.  

### Create DNS CNAME records

When you create a DNS entry for the CMG, you enable your Windows 10 or later devices both inside and outside your corporate network to use name resolution to find the CMG cloud service in Azure.

Our CNAME record example is *MyCMG.contoso.com*, which becomes *MyCMG.cloudapp.net*. In the example:  

- The company name is *Contoso* with a public DNS namespace of *contoso.com*.  

- The CMG service name is *MyCMG*, which becomes *MyCMG.cloudapp.net* in Azure.  

## Configure the management point and clients to use the CMG

Configure settings that enable on-premises management points and clients to use the cloud management gateway.

Because we use enhanced HTTP for client communications, there's no need to use an HTTPS management point.  

### Create the CMG connection point

Configure the site to support enhanced HTTP:  

1. In the Configuration Manager console, go to **Administration** > **Overview** > **Site Configuration** > **Sites**. Open the properties of the primary site.  

2. On the **Communication Security** tab, select the **HTTPS or HTTP** option for **Use Configuration Manager-generated certificates for HTTP site systems**. Then select **OK** to save the configuration.

3. Go to **Administration** > **Overview** > **Site Configuration** > **Servers and Site System Roles**. Select the server with a management point where you want to install the CMG connection point.  

4. Select **Add Site System Roles** > **Next** > **Next**.  

5. Select **Cloud management gateway connection point**, and then select **Next** to continue.  

6. Review the default selections on the **Cloud management gateway connection point** page and make sure the correct CMG is selected. 

   If you have multiple CMGs, you can use the dropdown list to specify a different CMG. You can also change the CMG in use, after installation. 
   
   Select **Next** to continue.

7. Select **Next** to start installation, and then view the results on the **Completion** page.  Select **Close** to complete the installation of the connection point.

8. Go to **Administration** > **Overview** > **Site Configuration** > **Servers and Site System Roles**. Open **Properties** for the management point where you installed the connection point. 

   On the **General** tab, select the **Allow Configuration Manager cloud management gateway traffic** checkbox, and then select **OK** to save the configuration.
   
   > [!TIP]  
   > Although it isn't required to enable co-management, we recommend that you make this same edit for any software update points.

### Configure client settings to direct clients to use the CMG

Use **Client Settings** to configure Configuration Manager clients to communicate with the CMG:  

1. Open **Configuration Manager console** > **Administration** > **Overview** > **Client Settings**, and then edit the **Default Client Settings** information.  

2. Select **Cloud Services**.

3. On the **Default Settings** page, set the following settings to **Yes**:  

   - **Automatically register new Windows 10 domain joined devices with Microsoft Entra ID**  

   - **Enable clients to use a cloud management gateway**

   - **Allow access to cloud distribution point**

4. On the **Client Policy** page, set **Enable user policy requests from internet clients** to **Yes**.

5. Select **OK** to save this configuration.

## Enable co-management in Configuration Manager

With the Azure configurations, site system roles, and client settings in place, you can configure Configuration Manager to enable co-management. However, you'll still need to make a few configurations in Intune after you enable co-management before this tutorial is complete. 

One of those tasks is to configure Intune to deploy the Configuration Manager client. That task is made easier by saving the command line for client deployment that's available from within the Co-management Configuration Wizard. That's why we enable co-management now, before we complete the configurations for Intune.

The term *pilot group* is used throughout the co-management feature and configuration dialogs. A pilot group is a collection that contains a subset of your Configuration Manager devices. Use a pilot group for your initial testing. Add devices as needed, until you're ready to move the workloads for all Configuration Manager devices. 

There's no time limit on how long a pilot group can be used for workloads. You can use a pilot group indefinitely if you don't want to move a workload to all Configuration Manager devices.

We recommend that you create a suitable collection before you start the procedure to create a pilot group. Then you can select that collection without exiting the procedure to do so. You might need multiple collections, because you can assign a different pilot group for each workload.

### Enable co-management for versions 2111 and later

[!INCLUDE [Enable Co-management starting in version 2111](includes/enable-co-management-2111.md)]

### Enable co-management for versions 2107 and earlier

[!INCLUDE [Enable Co-management in version 1906 through 2107](includes/enable-co-management-1906-2107.md)]

## Use Intune to deploy the Configuration Manager client

You can use Intune to install the Configuration Manager client on Windows 10 or later devices that are currently only managed with Intune.  

Then, when a previously unmanaged Windows 10 or later device enrolls with Intune, it automatically installs the Configuration Manager client.
  
> [!NOTE]
> If you're planning to deploy the Configuration Manager client to devices going through Autopilot, we recommend that you target users for the assignment of the Configuration Manager client instead of devices.
>
> This action will avoid a conflict between [installing line-of-business apps and Win32 apps during Autopilot](../../intune/apps/lob-apps-windows.md).

### Create an Intune app to install the Configuration Manager client

1. From the primary site server, sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). Then, go to **Apps** > **All Apps** > **Add**.

2. For app type, select **Line-of-business app** under **Other**.

3. For the **App package file**, browse to the location of the Configuration Manager file *ccmsetup.msi* (for example, *C:\Program Files\Microsoft Configuration Manager\bin\i386\ccmsetup.msi*). Then, select **Open** > **OK**.   

4. Select **App Information**, and then specify the following details:
   
   - **Description**: Enter **Configuration Manager Client**. 

   - **Publisher**: Enter **Microsoft**.  

   - **Command-line arguments**: Specify the `CCMSETUPCMD` command. You can use the command that you saved from the **Enablement** page of the Co-management Configuration Wizard. This command includes the names of your cloud service and additional values that enable devices to install the Configuration Manager client software.  

     The command-line structure should resemble this example, which uses only the `CCMSETUPCMD` and `SMSSiteCode` parameters:  

     ``` Command
     CCMSETUPCMD="CCMHOSTNAME=<ServiceName.CLOUDAPP.NET/CCM_Proxy_MutualAuth/<GUID>" SMSSiteCode="<YourSiteCode>"  
     ```

     > [!TIP]  
     > If you don't have the command available, you can view the properties of `CoMgmtSettingsProd` in the Configuration Manager console to get a copy of the command. The command appears only if you've met all of the prerequisites, such as setting up a CMG.

5. Select **OK** > **Add**. The app is created and becomes available in the Intune console. After the app is available, you can use the following section to assign the app to your devices from Intune.

### Assign the Intune app to install the Configuration Manager client

The following procedure deploys the app for installing the Configuration Manager client that you created in the previous procedure:

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). Select **Apps** > **All Apps**, and then select **ConfigMgr Client Setup Bootstrap**. That's the app that you created to deploy the Configuration Manager client.  

2. Select **Properties**, and then select **Edit** for **Assignments**. Select **Add group** under **Required** assignments to set the Microsoft Entra groups that have users and devices that you want to participate in co-management.  

3. Select **Review + save** > **Save** to save the configuration.
The app is now required by users and devices that you assigned it to. After the app installs the Configuration Manager client on a device, it's managed by co-management.

## Summary

After you complete the configuration steps of this tutorial, you can start co-managing your devices.

## Next steps

- Review the status of co-managed devices by using the [Co-management dashboard](how-to-monitor.md).
- Use [Windows Autopilot](quickstart-autopilot.md) to provision new devices.
- Use [Conditional Access](quickstart-conditional-access.md) and Intune compliance rules to manage user access to corporate resources.
