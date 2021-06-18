---
# required metadata

title: Install the Certificate Connector for Microsoft Intune - Azure | Microsoft Docs
description: Learn how to install and configure the unified Certificate Connector for Microsoft Intune, which supports SCEP, PKCS, imported PKCS, and certificate revocation. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 06/21/2021
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high
ms.technology:
ms.assetid:

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: M365-identity-device-management
---

# Install the Certificate Connector for Microsoft Intune
 

## Download and install the connector software

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Tenant administration** > **Connectors and tokens** > **Certificate connectors** > **Add**.

3. Select the *certificate connector* link to download the connector software. Save the file to a location that’s accessible from the server where you're going to install the connector.

   :::image type="content" source="./media/certificate-connector-install/download-certificate-connector.png" alt-text="Download the certificate connector software.":::

4. Sign in to the Windows Server that will host the certificate connector and confirm that the [prerequisites for the certificate connector](../protect/certificate-connector-prerequisites.md) are installed.

   If you’ll use SCEP with a Microsoft Certification Authority (CA), confirm that the Network Device Enrollment Service (NDES) role is installed.

5. Use an account with admin permissions to the server to run the installer (**IntuneCertificateConnector.exe**). The installer also installs the policy module for NDES and the IIS Certificate Registration Point (CRP) Web Service. The CRP Web Service, CertificateRegistrationSvc, runs as an application in IIS.

   When you install NDES for standalone Intune, the CRP service automatically installs with the Certificate Connector.

6. Review and agree to the license terms and conditions, and then select **Install** to continue. Select**Options** to choose a different installation folder.
7. The connector installation takes only a moment.  After installation, the setup presents two options:

   - **Configure Now** – Select this option to close the connector installation and open the *Certificate Connector for Microsoft Intune* wizard, which you use to [configure the certificate connector](#configure-the-certificate-connector) on the local server.

   - **Close** - This option closes the connector installation without configuring the connector. If you choose to *Close* the install at this time, later you can run the **Certificate Connector for Microsoft Intune** wizard to launch the connector configuration program. By default, the wizard is found in *C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Microsoft Intune*.

After a connector installs, you can run the installation program again to uninstall the connector.  

## Configure the certificate connector

To configure the certificate connector, you use the **Certificate Connector for Microsoft Intune** wizard.  This can be started automatically when you choose*Configure Now* at the end of a certificate connector install, or manually by going to  *C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Microsoft Intune*.

After you’ve configured a connector, you can run the wizard again to modify that connectors configuration. If you want to uninstall the connector, you need to run the installation program you used to first install the connector on the Windows Server.

Each time **Certificate Connector for Microsoft Intune** starts on a server you’ll see the following *Welcome* page:

:::image type="content" source="./media/certificate-connector-install/begin-connector-configuration.png" alt-text="Welcome page of the Certificate Connector for Microsoft Intune wizard.":::

> [!TIP]
> When you run **Certificate Connector for Microsoft Intune** to modify a previously configure connector, you won’t see the *Azure AD Sign In* page. This is because the connector has already been authenticated to your Azure Active Directory.

Use the following procedure to both configure a new connector and modify a previously configured connector.

1. On the *Welcome* page of **Microsoft Intune Certificate Connector**, select **Next**.

2. On *Features*, select the checkbox for each connector feature you want to install on this server, and then select **Next**. Options include:

   - **SCEP**: Select this option to enable certificate delivery to devices from a Microsoft Active Directory Certification Authority using the SCEP protocol.

   - **PKCS**: Select this option to enable certificate delivery to devices from a Microsoft Active Directory Certification Authority in PKCS format.  Ensure you’ve set up all the necessary prerequisites.

   - **PKCS imported certificates**: Select this option to enable certificate delivery to devices for pfx certificates that you have imported to Intune.  Ensure you’ve set up all the necessary prerequisites.

   - **Certificate revocation**: Select this option to enable automatic certificate revocation for certificates issued from a Microsoft Active Directory Certification Authority.

3. On *Service Account*, select the type of account to use for the service account of this connector. The account you select must have the permissions described in prerequisites for the [certificate connector service account](../protect/certificate-connector-prerequisites.md#certificate-connector-service-account).

   Options include:

   - **SYSTEM**

   - **Managed service account** – To you this option, you will first need to create a [group managed service account (gMSA)](/azure/active-directory-domain-services/create-gmsa) in Azure Active Directory .

   - **Domain account** – Use any domain account that has the required permissions.

4. On the *Proxy* page, add details for your proxy server if you require a proxy for internet access.

5. On the *Prerequisites* page, Microsoft Intune Certificate Connector runs several checks before proceeding. Review and resolve any errors or warnings before you proceed.

6. On the *Azure AD Sign In* page, select the environment that hosts your Azure Active Directory, and then select **Sign In**.  You’ll then be asked to authenticate your access.

   Unless you use a government cloud, use the Environment default of **Public Commercial Cloud**.

   :::image type="content" source="./media/certificate-connector-install/authenticate-to-azure-ad.png" alt-text="Authenticate to your Azure Active Directory.":::

   After you successfully authenticate to your Azure Active Directory, select **Next** to continue:

   :::image type="content" source="./media/certificate-connector-install/azure-ad-sign-in-success.png" alt-text="Successful sign-in to Azure Active Directory.":::

7. On the *Configure* page, Intune applies your selections to the connector. If successful, the utility continues to the *Finish* page where you select **Exit** to complete configuration of the connector.

   :::image type="content" source="./media/certificate-connector-install/connector-configuration-complete.png" alt-text="Successful configuration of the certificate connector.":::

   If configuration isn’t successful, the wizard displays details about the errors to help you resolve the problem.

After the configuration completes successfully and the wizard closes, the Certificate Connector for Microsoft Intune is now ready for use.

## Modify the connector configuration

After you configure a Certificate Connector for Microsoft Intune on a server, you can [run the configuration wizard](#configure-the-certificate-connector) on that server to modify the connectors configuration.

## Remove the connector

To uninstall the Certificate Connector for Microsoft Intune form a Windows Server, on the server run  **IntuneCertificateConnector.exe**, which is the same [software you use to install the connector](#download-and-install-the-connector-software). When run on a server that has the connector installed, the only available option is to remove the current connector installation.
## Next steps

Deploy:
- [SCEP certificate profiles](../intune/protect/certificates-profile-scep.md)
- [PKCS certificates](../intune/protect/certificates-pfx-configure.md)
- [Imported PKCS certificates](../intune/protect/certificates-imported-pfx-configure.md)
