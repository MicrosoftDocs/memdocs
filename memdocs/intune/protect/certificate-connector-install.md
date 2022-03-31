---
# required metadata

title: Install the Certificate Connector for Microsoft Intune - Azure | Microsoft Docs
description: Learn how to install and configure the unified Certificate Connector for Microsoft Intune, which supports SCEP, PKCS, imported PKCS, and certificate revocation. 
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 03/30/2022
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:

ms.reviewer: lacranda
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection: 
  - M365-identity-device-management
  - highpri
---

# Install the Certificate Connector for Microsoft Intune

To support your use of certificates with Intune, you can install the Certificate Connector for Microsoft Intune on any Windows Server that meets the [connector prerequisites](../protect/certificate-connector-prerequisites.md). The following sections will help you install and then configure the connector. This article also explains how to modify a previously installed connector, and how to remove the connector from a server.

## Download and install the connector software

1. Sign in to the [Microsoft Endpoint Manager admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

2. Select **Tenant administration** > **Connectors and tokens** > **Certificate connectors** > **Add**.

3. Select the *certificate connector* link to download the connector software. Save the file to a location that’s accessible from the server where you're going to install the connector.

   :::image type="content" source="./media/certificate-connector-install/download-certificate-connector.png" alt-text="Download the certificate connector software.":::

4. Sign in to the Windows Server that will host the certificate connector and confirm that the [prerequisites for the certificate connector](../protect/certificate-connector-prerequisites.md) are installed.

   If you’ll use SCEP with a Microsoft Certification Authority (CA), confirm that the Network Device Enrollment Service (NDES) role is installed.

5. Use an account with admin permissions to the server to run the installer (**IntuneCertificateConnector.exe**). The installer also installs the policy module for NDES. The policy module runs as an application in IIS.

   > [!NOTE]  
   > When **IntuneCertificateConnector.exe** runs to install a new connector or an existing connector auto upgrades while the Windows Event Viewer is open, the installation process logs a message similar to the following with an Event ID 1000 from the source *Microsoft-Intune-CertificateConnectors cannot be found*:
   >
   > - Either the component that raises this event is not installed on your local computer or the installation is corrupted. You can install or repair the component on the local computer.
   >
   > You can safely ignore this message. This message displays because the event viewer manifest for the connector could not load while the event viewer is open. After the event viewer closes and then reopens, the correct messages display.

6. Review and agree to the license terms and conditions, and then select **Install** to continue. Select **Options** to choose a different installation folder.

7. The connector installation takes only a moment. After installation, the setup presents two options:

   - **Configure Now** – Select this option to close the connector installation and open the *Certificate Connector for Microsoft Intune* wizard, which you use to [configure the certificate connector](#configure-the-certificate-connector) on the local server.

   - **Close** - This option closes the connector installation without configuring the connector. If you choose to *Close* the install at this time, later you can run the **Certificate Connector for Microsoft Intune** wizard to launch the connector configuration program. By default, the wizard is found in *C:\ProgramData\Microsoft\Windows\Start Menu\Programs\Microsoft Intune*.

After a connector installs, you can run the installation program again to uninstall the connector.

## Configure the certificate connector

To configure the certificate connector, you use the **Certificate Connector for Microsoft Intune** wizard. The configuration can start automatically when you choose *Configure Now* at the end of a certificate connector install, or manually by opening an elevated command prompt and running **C:\Program Files\Microsoft Intune\PFXCertificateConnector\ConnectorUI\PFXCertificateConnectorUI.exe**. An example is provided below. The command must be run as an administrator.

   ``` command
   C:\Program Files\Microsoft Intune\PFXCertificateConnector\ConnectorUI\PFXCertificateConnectorUI.exe
   ```

Each time **Certificate Connector for Microsoft Intune** starts on a server you’ll see the following *Welcome* page:

:::image type="content" source="./media/certificate-connector-install/begin-connector-configuration.png" alt-text="Welcome page of the Certificate Connector for Microsoft Intune wizard.":::

> [!TIP]
> When you run **Certificate Connector for Microsoft Intune** to modify a previously configure connector, you won’t see the *Azure AD Sign In* page. This is because the connector has already been authenticated to your Azure Active Directory.

Use the following procedure to both configure a new connector and modify a previously configured connector.

1. On the *Welcome* page of **Microsoft Intune Certificate Connector**, select **Next**.

2. On *Features*, select the checkbox for each connector feature you want to install on this server, and then select **Next**. Options include:

   - **SCEP**: Select this option to enable certificate delivery to devices from a Microsoft Active Directory Certification Authority using the SCEP protocol. Devices that submit a certificate request will generate a private/public key pair and submit only the public key as part of that request.

   - **PKCS**: Select this option to enable certificate delivery to devices from a Microsoft Active Directory Certification Authority in PKCS #12 format.  Ensure you’ve set up all the necessary prerequisites.

   - **PKCS imported certificates**: Select this option to enable certificate delivery to devices for pfx certificates that you've imported to Intune. Ensure you’ve set up all the necessary prerequisites.

   - **Certificate revocation**: Select this option to enable automatic certificate revocation for certificates issued from a Microsoft Active Directory Certification Authority.

3. On *Service Account*, select the type of account to use for the service account of this connector. The account you select must have the permissions described in prerequisites for the [certificate connector service account](../protect/certificate-connector-prerequisites.md#certificate-connector-service-account).

   Options include:

   - **SYSTEM**
   - **Domain user account** – Use any domain user account that is an administrator on the Windows Server.

4. On the *Proxy* page, add details for your proxy server if you require a proxy for internet access. For example, `http://proxy.contoso.com`.
   > [!TIP]  
   > Be sure to include the HTTP or HTTPS prefix, which is a change from proxy configurations for previous connectors.

5. On the *Prerequisites* page, the wizard runs several checks on the server before the configuration can begin. Review and resolve any errors or warnings before you continue.

6. On the *Azure AD Sign In* page, select the environment that hosts your Azure Active Directory, and then select **Sign In**. You’ll then be asked to authenticate your access. This user account must be a Global Admin or an Intune Admin with an Intune license assigned and the user must be a synchronized account from your local Active Directory.

   Unless you use a government cloud, use the default of **Public Commercial Cloud** for *Environment*.

   :::image type="content" source="./media/certificate-connector-install/authenticate-to-azure-ad.png" alt-text="Authenticate to your Azure Active Directory.":::

   After you successfully authenticate to your Azure Active Directory, select **Next** to continue:

   :::image type="content" source="./media/certificate-connector-install/azure-ad-sign-in-success.png" alt-text="Successful sign in to Azure Active Directory.":::

7. On the *Configure* page, Intune applies your selections to the connector. If successful, the utility continues to the *Finish* page where you select **Exit** to complete configuration of the connector.

   :::image type="content" source="./media/certificate-connector-install/connector-configuration-complete.png" alt-text="Successful configuration of the certificate connector.":::

   If configuration isn’t successful, the wizard displays details about the errors to help you resolve the problem.

After the configuration completes successfully and the wizard closes, the Certificate Connector for Microsoft Intune is now ready for use.

> [!TIP]
> It might be helpful to rename the connector to reference the server the connector is installed on. 
> 
> To rename the connector, in the Microsoft Endpoint Manager portal, select **Tenant administration** > **Connectors and tokens** > **Certificate connectors**. Select the connector you want to rename. In **Name**, enter the name you want to use, and then select **save**.

## Modify the connector configuration

After you configure a Certificate Connector for Microsoft Intune on a server, you can [run the configuration wizard](#configure-the-certificate-connector) on that server to modify the connectors configuration.

## Remove the connector

To uninstall the Certificate Connector for Microsoft Intune from a Windows Server, on the server run **IntuneCertificateConnector.exe**, which is the same [software you use to install the connector](#download-and-install-the-connector-software). When run on a server that has the connector installed, the only available option is to remove the current connector installation.
## Next steps

Deploy:
- [SCEP certificate profiles](../protect/certificates-profile-scep.md)
- [PKCS certificates](../protect/certificates-pfx-configure.md)
- [Imported PKCS certificates](../protect/certificates-imported-pfx-configure.md)
