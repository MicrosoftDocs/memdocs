---
title: "Certificates and security"
titleSuffix: "Configuration Manager"
description: "Manage certificates and security for System Center Updates Publisher"
ms.custom: na
ms.date: 4/29/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
  - configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a7f91e63-4750-402e-9970-dd14be7f76a3
caps.latest.revision: 1
author: mstewart
ms.author: mstewart
manager: angrobe
robots: NOINDEX, NOFOLLOW
---
# Manage certificates and security for Updates Publisher

*Applies to: System Center Configuration Manager (Current Branch)*

The following procedures can help you to configure the certificate store on the update server, configure a self-signing certificate on the client computer, and to configure the Group Policy to allow the Windows Update Agent on computers to scan for published updates.

## Configure the certificate store on the update server
 Updates Publisher uses a digital certificate to sign the updates in the catalogs it publishes. Before a catalog can be published to the update server, that certificate must be in the certificate store on the update server, and in the certificate store of the Updates Publisher computer if that computer is remote from the update server.

The following procedure is one of several possible methods to add the certificate to the certificate store on the update server.

### To configure the certificate store
1.  On a computer that can access both the Updates Publisher computer and the update server, Click **Start**, click **Run**, type **MMC** in the text box, and then click **OK** to open the Microsoft Management Console (MMC).

2.  Click **File**, click **Add/Remove Snap-in**, click **Add**, click **Certificates**, click **Add**, select **Computer account**, and then click **Next**.

3.  Select **Another computer**, type the name of the update server or click **Browse** to find the update server computer, click **Finish**, click **Close**, and then click **OK**.

4.  Expand **Certificates (*update server name*)**, expand **WSUS**, and then click **Certificates**.

5.  In the results pane, right-click the desired certificate, click **All Tasks**, and then click **Export**.

6.  In the Certificate Export Wizard, use the default settings to create an export file with the name and location specified in the wizard. This file must be available to the update server before proceeding to the next step.

7.  Right-click **Trusted Publishers**, click **All Tasks**, and then click **Import**. Complete the Certificate Import Wizard using the exported file from step 6.

8.  If a self-signed certificate is used, such as **WSUS Publishers Self-signed**, right-click **Trusted Root Certification Authorities**, click **All Tasks**, and then click **Import**. Complete the Certificate Import Wizard using the exported file from step 6.

9.  Right-click **Certificates (*update server name*)**, click **Connect to another computer**, enter the computer name for the Updates Publisher computer, and click **OK**.

10. If Updates Publisher is remote from the update server, repeat steps 7 through 9 to import the certificate to the certificate store on the Updates Publisher computer.



## Configure a self-signing certificate on client computers
On client computers, the Windows Update Agent (WUA) will scan for the updates from the catalog. This process will fail to install updates when the agent cannot locate that digital certificate in the Trusted Publishers store on the local computer. If a self-signed certificate was used to publishing the updates catalog, such as **WSUS Publishers Self-signed**, the certificate must also be in the Trusted Root Certification Authorities certificate store on the local computer so that the agent can verify the validity of the certificate.

You can use one of several methods for configuring certificates on client computers, like using Group Policy and the **Certificate Import Wizard** or by using the Certutil tool and software distribution.

The following is provided as one example of how to configure the signing certificate on client computers.

### To configure a self-signing certificate on client computers
1.  On a computer with access to the update server, click **Start**, click **Run**, type **MMC** in the text box, and then click **OK** to open the Microsoft Management Console (MMC).

2.  Click **File**, click **Add/Remove Snap-in**, click **Add**, click **Certificates**, click **Add**, select **Computer account**, and then click **Next**.

3.  Select **Another computer**, type the name of the update server or click **Browse** to find the update server computer, click **Finish**, click **Close**, and then click **OK**.

4.  Expand **Certificates (*update server name*)**, expand **WSUS**, and then click **Certificates**.

5.  Right-click the certificate in the results pane, click **All Tasks**, and then click **Export**. Complete the **Certificate Export Wizard** using the default settings to create an export certificate file with the name and location specified in the wizard.

6.  Use one of the following methods to add the certificate used to sign the updates catalog to each client computer that will use WUA to scan for the updates in the catalog. Add the certificate on the client computer as follows:

    -   For self-signed certificates: Add the certificate to the **Trusted Root Certification Authorities** and **Trusted Publishers** certificate stores.

    -   For certification authority (CA) issued certificates: Add the certificate to the **Trusted Publishers** certificate store.

    > [!NOTE]
    > The WUA also checks whether the **Allow signed content from intranet Microsoft update service location** Group Policy setting is enabled on the local computer. This policy setting must be enabled for WUA to scan for the updates that were created and published with Updates Publisher. For more information about enabling this Group Policy setting, see [How to Configure the Group Policy on Client Computers](https://technet.microsoft.com/library/bb530967.aspx(d=robot).



## Configuring Group Policy to allow WUA on computers to scan for published updates
Before the Windows Update Agent (WUA) on computers will scan for updates that were created and published with Updates Publisher, a policy setting must be enabled to allow signed content from an intranet Microsoft update service location. When the policy setting is enabled, WUA will accept updates received through an intranet location if the updates are signed in the **Trusted Publishers** certificate store on the local computer. There are several methods for configuring Group Policy on computers in the environment.

For computers that are not on the domain, a registry key setting can be configured that allows signed content from an intranet Microsoft Update service location.

The following procedures provide the basic steps that can be used to configure Group Policy for computers on the domain and a registry key value on computers that are not on the domain.

### To configure Group Policy to allow WUA to scan for published updates
1.  Open the Group Policy Object Editor Microsoft Management Console (MMC) snap-in with a user that has the appropriate security rights to configure Group Policy.

2.  Click **Browse** and select the domain, OU, or GPOs linked to the site where the configured Group Policy will propagate to the desired client computers. Click **OK**, click **Finish**, click **Close**, and then click **OK**.

3.  Expand the selected policy setting in the console tree, expand **Computer Configuration**, expand **Administrative Templates**, expand **Windows Components**, and then click **Windows Update**.

4.  In the results pane, right-click **Allow signed content from intranet Microsoft update service location**, click **Properties**, click **Enabled**, and then click **OK**.
