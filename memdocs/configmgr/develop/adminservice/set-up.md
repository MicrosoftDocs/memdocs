---
title: How to set up the admin service
titleSuffix: Configuration Manager
description: Use the steps in this article to set up the administration service on your SMS Provider
ms.date: 11/30/2020
ms.prod: configuration-manager
ms.technology: configmgr-sdk
ms.topic: how-to
ms.assetid: 829eb4a4-8791-4746-a777-1fb0382b6d7c
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# How to set up the administration service in Configuration Manager

*Applies to: Configuration Manager (current branch)*

Use the steps in this article to set up the administration service on your SMS Provider. Before you start, read the administration service [Prerequisites](overview.md#prerequisites).

## Enable secure HTTPS communication

Configure the administration service to use a secure HTTPS connection to protect the data in transit across the network.

Starting in version 2010,<!--8613105--> you no longer need to enable IIS on the SMS Provider for the administration service. The site creates a self-signed certificate for the SMS Provider, and automatically binds it without requiring IIS. If you previously had IIS installed on the SMS Provider, you can remove it. Then restart the SMS_REST_PROVIDER component. Remember that you need to open HTTPS port 443 on your firewall. 

Starting in version 2002,<!--5728365--> the administration service automatically uses the site's self-signed certificate. This change helps reduce the friction for easier use of the administration service. The site always generates this certificate. Now the administration service ignores the Enhanced HTTP site setting, as it always uses the site's certificate even if no other site system is using Enhanced HTTP. You can still manually bind a PKI-based server authentication certificate. If you've already bound a PKI certificate to port 443 on the SMS Provider server, the administration service uses that existing certificate.

In version 1910 and earlier, use one of the following options:

- Enable the site to use Enhanced HTTP (recommended)

- Manually bind a server authentication certificate to port 443 in IIS on the server that hosts the SMS Provider role. This certificate can come from your organization's PKI, or from a third-party certificate provider.

### Enable Enhanced HTTP

> [!NOTE]
> The configuration in this section applies to version 1910 and earlier.
>
> Starting in version 2002, the administration service automatically uses the site's self-signed certificate. The Enhanced HTTP site setting to **Use Configuration Manager-generated certificates for HTTP site systems** only controls whether site systems use it or not. Now the administration service ignores this site setting, as it always uses the site's certificate even if no other site system is using Enhanced HTTP.

If you enable [Enhanced HTTP](../../core/plan-design/hierarchy/enhanced-http.md), the site generates certificates for site system roles like the SMS Provider. The site server issues and signs these certificates with its self-signed **SMS Issuing** root certificate. This option doesn't require a public key infrastructure (PKI). Configuration Manager creates and manages the certificates, and binds them to the IIS services as needed.

When the site creates a certificate for the SMS Provider, clients won't trust it by default. If you try to access the administration service from a web browser on a client, you may see a security warning. Export the SMS Issuing root certificate from the Configuration Manager site, and install it on clients in the Trusted Root Certification Authorities store.

1. In the Configuration Manager console, go to the **Administration** workspace. Expand the **Security** node, and select **Certificates**.

1. Search for the **SMS Issuing** certificate. You can also locate it by this name in the **Issued To** column.

1. If there's more than one SMS Issuing certificate, select the current valid certificate.

1. In the ribbon, on the **Home** tab, select **Properties**. This action opens the standard Windows certificate properties.

1. To easily add the certificate to the local computer, select **Install Certificate**.

    1. In the Certificate Import Wizard, select **Local Machine** for the store location. To continue, you need to have local administrative rights on the computer.
    1. Select **Place all certificates in the following store** and then select **Browse**. Select **Trusted Root Certification Authorities**.
    1. Finish the certificate import wizard.

    > [!NOTE]
    > This action only imports the SMS Issuing certificate to the local computer where you're currently running the Configuration Manager console.

1. To install the certificate on multiple computers, first export it to a file. In the certificate properties window, switch to the **Details** tab. Select **Copy to File**.

    1. On the **Export File Format** page of the Certificate Export Wizard, select the default certificate format, **DER encoded binary X.509 (.CER)**.
    1. On the **File to Export** page, specify a path and file name with the `.cer` file extension.
    1. Finish the certificate export wizard.

    > [!IMPORTANT]
    > Store this exported certificate in a secure location. Any device with this root certificate trusts any certificate that the Configuration Manager site issues.

1. Distribute and import the root certificate to the Trusted Root Certification Authorities store on any computer that you want to access the administration service.

    - Manually import the certificate where you need it. See the steps above for the Certificate Import Wizard.
    - Use Configuration Manager to distribute and install the certificate using a custom script. For example, use the [Import-Certificate](/powershell/module/pkiclient/import-certificate) PowerShell cmdlet.
    - Use the following Active Directory group policy: **Computer Configuration\Policies\Windows Settings\Security Settings\Public Key Policies\Trusted Root Certification Authorities**

### Use a server authentication certificate

> [!NOTE]
> Starting in version 2002, by default the administration service automatically uses the site's self-signed certificate. You can still manually bind a PKI-based server authentication certificate. Before you can bind your PKI-based certificate, manually unbind the site's self-signed certificate from port 443 on the SMS Provider.

There are two primary methods of using a server authentication certificate:

- From your organization's public key infrastructure (PKI)

  - If your environment already has a PKI, you can use it to issue a server authentication certificate for the SMS Provider. This certificate is similar to the certificate you would use for a management point or distribution point. For more information, see [PKI certificate requirements](../../core/plan-design/network/pki-certificate-requirements.md#BKMK_PKIcertificates_for_servers).

  - Most enterprise PKI implementations add the trusted root CAs to Windows clients. For example, using Active Directory Certificate Services with group policy. If you issue the certificate from a CA that your clients don't automatically trust, add the CA trusted root certificate to clients. You can scope this trust to only the clients that need to access the administration service.

- Use a certificate from a public and globally trusted certificate provider. For example, but not limited to, DigiCert, Thawte, or VeriSign. Windows clients include trusted root certificate authorities (CAs) from these providers. By using a server authentication certificate issued by one of these providers, your clients automatically trust it.  

Once you have a server authentication certificate for the SMS Provider, you need to manually bind it to port 443 in IIS on the server that hosts the SMS Provider role.

First, add the certificate to the server. Import the certificate into the local machine's **Personal** store. Then use one of the following options to bind the certificate:

#### Bind the certificate with IIS

If the server with the SMS Provider role has the IIS Management Console, use the **Edit Bindings** action on the default web site. Add port 443, and specify your certificate from the machine's certificate store.

> [!NOTE]
> The SMS Provider role doesn't require IIS. This procedure is using the IIS console to bind the certificate. These certificate bindings are for the machine, not any specific service.

#### Bind the certificate with netsh

Use the netsh command line to bind the certificate:

`netsh http add sslcert ipport=0.0.0.0:443 certhash=<thumbprint> appid={<GUID>}`

Where `<thumbprint>` is the thumbprint of the installed certificate, and `<GUID>` is a random GUID.

> [!TIP]
> Use the Windows PowerShell cmdlet `New-Guid` to generate a random GUID.

For example:

`netsh http add sslcert ipport=0.0.0.0:443 certhash=5aef9c1f348d4d1c8675309ca3363c2a5d3b617d appid={e9f0631d-6d1c-41b4-9617-454705f9c011}`

## Enable internet access

You can use the administration service on-premises only, or you can enable it for access through the cloud management gateway (CMG). Some scenarios require access to the administration service from the internet, such as tenant attach or app approvals via email.

Before you can configure the SMS Provider to allow CMG traffic, first set up a CMG. For more information, see [Overview of CMG](../../core/clients/manage/cmg/overview.md).

Then use the following process to enable the administration service through the CMG:

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Servers and Site System Roles** node.  

2. Select the server with the **SMS Provider** role.  

    > [!TIP]
    > On the ribbon, in the **Home** tab, select **Servers with Role** and then select **SMS Provider**. This action shows you the site systems with that role.

3. In the details pane, select the **SMS Provider** role, and select **Properties** in the ribbon on the **Site Role** tab.  

4. Select the option to **Allow Configuration Manager cloud management gateway traffic for administration service**.  

To access the administration service from the internet, replace the SMS Provider FQDN with the CMG endpoint. For example:

`https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500/AdminService`

> [!TIP]
> To get the value for this endpoint, use the following steps:
>
> - Create a CMG. For more information, see [Set up a CMG](../../core/clients/manage/cmg/setup-cloud-management-gateway.md).
> - On an active client, open a Windows PowerShell command prompt as an administrator.
> - Run the following command:
>
>    ```PowerShell
>    (Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}).MP
>    ```

## Enable console usage

<!--4223683-->
Enable some nodes of the Configuration Manager console to use the administration service. This change allows the console to communicate with the SMS Provider over HTTPS instead of via WMI.

1. In the Configuration Manager console, go to the **Administration** workspace, expand **Site Configuration**, and select the **Sites** node. In the ribbon, select **Hierarchy Settings**.

1. On the **General** page, select the option to **Enable the Configuration Manager console to use the administration service**.

This change only affects the following nodes under the **Security** node in the **Administration** workspace:

- Administrative Users
- Security Roles
- Security Scopes
- Console Connections

When you select one of these nodes, if the following error message displays:

*Configuration Manager can't connect to the administration service*

Review the information below the error. Then verify that the administration service is enabled, configured, and functional. For more information including log files to review, see the [Verify](#verify) section.

## Verify

When the site installs the administration service, it logs activity to the **RESTPROVIDERSetup.log** file in the Configuration Manager installation directory. By default this path is `C:\Program Files\Microsoft Configuration Manager\logs`.

The site tracks the health state of the administration service in the **SMS_REST_PROVIDER.log** file. You can see the service start and information about the certificate.

Test the administration service by doing a simple query in a web browser, for example:

`https://smsprovider.contoso.com/adminservice/v1.0/$metadata`

The administration service logs its activity to the **adminservice.log** file on the SMS Provider server in the Configuration Manager installation directory.

For the above metadata query, the log file shows the following lines:

```log
Processing incoming request for resource [https://smsprovider.contoso.com/adminservice/v1.0/%24metadata], method: [GET], User - [CONTOSO\jqadmin]
...
Completing request with response code [200] reason [OK]
```

## Next steps

> [!div class="nextstepaction"]
> [How to use the administration service](usage.md)
