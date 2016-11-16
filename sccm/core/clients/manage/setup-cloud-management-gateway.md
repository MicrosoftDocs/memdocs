---
title: "Set up Cloud Management Gateway | System Center Configuration Manager"
description: ""
author: mtillman
manager: angrobe
ms.author: mtillman
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service:
ms.technology:
  - configmgr-client
ms.assetid: e0ec7d66-1502-4b31-85bb-94996b1bc66f
---

# Set up cloud management gateway for Configuration Manager

*Applies to: System Center Configuration Manager (Current Branch)*

Beginning in version 1610, the process for setting up cloud management gateway in Configuration Manager includes the following steps:

## Step 1: Create a custom SSL certificate

You can create a custom SSL certificate for cloud management gateway in the same way you would do it for a cloud-based distribution point. Follow the instructions for [Deploying the Service Certificate for Cloud-Based Distribution Points](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012) but do the following things differently:

-   When setting up the new certificate template, give **Read** and **Enroll** permissions to the security group that you set up for Configuration Manager servers.

## Step 2: Export the client certificate's root

The easiest way to get export the root of the client certificates used on the network, is to open a client certificate on one of the domain-joined machines that has one and copy it.

> \[!NOTE\] Client certificates are required on any computer you want to manage with cloud management gateway and on the site system server hosting the cloud management gateway connector point. If you need to add a client certificate to any of these machines, see [Deploying the Client Certificate for Windows Computers](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#deploying-the-client-certificate-for-windows-computers).

1.  In the Run window, type **mmc** and press Return.

2.  On the File menu in the management console, click **Add/Remove Snap-in...**.

3.  In the Add or Remove Snap-ins dialog box, click **Certificates**, click **Add &gt;**, click **Computer account**, click **Next**, click **Local computer**, and then click **Finish**. Click **OK** to close the dialog box.

4.  Go to **Certificates &gt; Personal &gt; Certificates**.

5.  Double-click the certificate for client authentication on the computer, click the Certification Path tab, and double-click the root authority (at the top of the path).

6.  Click the Details tab, and click **Copy to File...**.

7.  Complete the Certificate Export Wizard using the default certificate format. Make note of the name and location of the root certificate you create. You will need it to configure cloud management gateway in a [later step](#step-4-set-up-cloud-management-gateway).

## Step 3: Upload the management certificate to Azure

An Azure management certificate is required for Configuration Manager to access the Azure API and configure cloud management gateway. For more information and instructions for how to upload a management certificate, see the following articles in the Azure documentation:

- [Certificates overview for Azure Cloud Services](https://azure.microsoft.com/documentation/articles/cloud-services-certs-create/)

- [Upload an Azure Management API Management Certificate](https://azure.microsoft.com/documentation/articles/azure-api-management-certs/)

>[!IMPORTANT]
>Make sure to copy the subscription ID associated with the management certificate. You will need it for configuring cloud management gateway in the Configuration Manager console in the [next step](#step-4-set-up-cloud-management-gateway).

## Step 4: Set up cloud management gateway

1. In the Configuration Manager console, go to **Administration > Cloud Services > Cloud Management Gateway**.
2. Click **Create Cloud Management Gateway**.

3. In Create Cloud Management Gateway Wizard, enter your Azure subscription ID (copied from the Azure management portal), click Browse, and select the certificate file you used to upload as an Azure management certificate. Click **Next**. Wait a few moments for the console to connect to Azure.

4. Fill out the additional details in the wizard:

    - Specify the name for the service which will run in Azure.

    - Choose the Azure region you want the service to run in.

    - Specify the number of virtual machines you want to use for the service. The default is 1, but you can run up to 16 virtual machines for the service.

    >[!NOTE]
    >If you use an internet proxy for the cloud management gateway connection point, you need to increase the number of ports on the proxy by the number of virtual machines you use, starting at port 10124.

    - Specify the private key (.pfx file) that you exported from the custom SSL certificate.

    - Specify the root certificate exported from the client certificate.

    -   Specify the same service name FQDN that you used when you created the new certificate template. You must use the following prefixes for the FQDN service name and the Azure platform you are using:

    Azure platform | FQDN prefix
    --------------|-------------
    Public (commercial) cloud | .cloudapp.net    
    Government cloud | .usgovcloudapp.net

  - Clear the box next to **Verify Client Certificate Revocation** (unless you're publicly publishing your CRL information).

  - Click **Next** when you're done.

5. If you want to monitor cloud management gateway traffic with a 14-day threshold, click check box to turn on the threshold alert. Then, specify the threshold (in GB) and the percentage at which to raise the different alert levels. Click **Next** when your done.

6. Review the settings, and click **Next**. Configuration Manager starts setting up the service. When the wizard completes, you can click **Close**, however it will take between 5 to 15 minutes to provision the service completely in Azure. Check the **Status** column for the newly setup cloud management gateway to determine when the service is ready.

## Step 5: Configure primary site for client certification authentication

1. In the Configuration Manager console, go to **Administration > Site Configuration > Sites**.

2. Select the primary site for the clients you want to manage through cloud management gateway, and click **Properties**.

3. On the Client Computer Communications tab of the primary site property sheet, check the box next to **Use PKI client certificate (client authentication) when available**.

4. Make sure to clear the box next to **Clients check the certificate revocation list (CRL) for site systems**. This option would only be required if you were publicly publishing your CRL.

5. Click **OK**.

## Step 6: Add the cloud management gateway connector point

The cloud management gateway connector point is a new site system role for communicating with cloud management gateway. To add the cloud management gateway connector point, follow the instructions in [Add site system roles for System Center Configuration Manager](/sccm/core/servers/deploy/configure/add-site-system-roles).

## Step 7: Configure roles for cloud management gateway traffic

The final step in setting up cloud management gateway is to configure the site system roles to accept cloud management gateway traffic. For Tech Preview 1606, only the management point, distribution point, and software update point roles are supported for cloud management gateway. You must configure each role separately.

1. In the Configuration Manager console, go to **Administration > Site Configuration > Servers and Site System Roles**.

2. Click the site system server for the role you want to configure for cloud management gateway traffic.

3. Click the role, and then click **Properties**.

4. In the role Properties sheet, under Client Connections, choose **HTTPS**, check the box next to **Allow Configuration Manager cloud management gateway traffic**, and then click **OK**. Repeat these steps for the remaining roles.

## Step 8: Configure clients for cloud management gateway

After the cloud management gateway and site system roles are completely configured and running, clients will get the location of the cloud management gateway service automatically on the next location request. Clients must be on the corporate network to receive the location of the cloud management gateway service. The polling cycle for location requests is every 24 hours. If you don't want to wait for the normally scheduled location request, you can force the request by restarting the SMS Agent Host service (ccmexec.exe) on the computer.

With the location of the cloud management gateway service configured on the client, it can automatically determine whether it’s on the intranet or the Internet. If the client can contact the domain controller or the on-premises management point, it will use it for communicating with Configuration Manager, Otherwise, it will consider it’s on the Internet and use the location of the cloud management gateway service to communicate.

>[!NOTE]
> You can force the client to always use cloud management gateway regardless of whether it’s on the intranet or Internet. To do that, you set the following registry key on the client computer:\
>
> `HKEY\_LOCAL\_MACHINE\\SOFTWARE\\Microsoft\\CCM\\Security, ClientAlwaysOnInternet = 1`

To verify that clients can contact Configuration Manager, you can run the following PowerShell command on the client computer:

`gwmi -namespace root\\ccm\\locationservices -class SMS\_ActiveMPCandidate`

This command displays the management points the client can contact including the cloud management gateway service.

## Next steps

[Monitor clients for cloud management gateway](monitor-clients-cloud-management-gateway.md)
