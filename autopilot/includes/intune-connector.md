---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.reviewer: madakeva
ms.subservice: autopilot
ms.service: windows-client
ms.topic: include
ms.date: 01/31/2025
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

pre-provisioning/hybrid-azure-ad-join-intune-connector
user-driven/hybrid-azure-ad-join-intune-connector
windows-autopilot-hybrid.md

Headings are driven by article context. -->

The purpose of the Intune Connector for Active Directory, also known as the Offline Domain Join (ODJ) Connector, is to join computers to an on-premises domain during the Windows Autopilot process. The Intune Connector for Active Directory creates computer objects in a specified Organizational Unit (OU) in Active Directory during the domain join process.

> [!IMPORTANT]
>
> Starting with Intune 2501, Intune uses an updated Intune Connector for Active Directory that strengths security and follows least privilege principles by using a [Managed Service Account (MSA)](/windows-server/identity/ad-ds/manage/understand-service-accounts#standalone-managed-service-accounts). When the Intune Connector for Active Directory is downloaded from within Intune, the updated Intune Connector for Active Directory is downloaded. The previous legacy Intune Connector for Active Directory is still available for download at [Intune Connector for Active Directory](https://www.microsoft.com/download/details.aspx?id=105392&msockid=3cb707200c316b2c119712450d8b6a5d), but Microsoft recommends using the updated Intune Connector for Active Directory installer going forward. The previous legacy Intune Connector for Active Directory will continue to work through sometime in May 2025. However, it needs to be updated to the updated Intune Connector for Active Directory before then to avoid loss of functionality. For more information, see [Intune Connector for Active Directory with low-privileged account for Autopilot Hybrid Microsoft Entra join deployments]().

Select the tab that corresponds to the version of the Intune Connector for Active Directory that is being installed:

### [:::image type="icon" source="/autopilot/images/icons/software-18.svg"::: **Updated Connector**](#tab/updated-connector)

Before beginning the installation, make sure that all of the [Intune connector server requirements](/autopilot/windows-autopilot-hybrid?tabs=intune-connector-requirements#requirements) are met.

> [!TIP]
>
> It's preferable, but not required, that the administrator installing and configuring the Intune Connector for Active Directory has appropriate domain rights as documented in [Intune Connector for Active Directory requirements](../windows-autopilot-hybrid.md?tabs=intune-connector-requirements#requirements). This requirement allows the Intune Connector for Active Directory installer and configuration process to properly set permissions for the MSA on the **Computer** container or OUs where computer objects are created. If the administrator doesn't have these permissions, an administrator that does have the appropriate permissions needs to follow the section [Increase the computer account limit in the Organizational Unit](../windows-autopilot-hybrid.md?tab=updated-connector#increase-the-computer-account-limit-in-the-organizational-unit).

#### Turn off Internet Explorer Enhanced Security Configuration

By default Windows Server has Internet Explorer Enhanced Security Configuration turned on. Internet Explorer Enhanced Security Configuration might cause problems signing into the Intune Connector for Active Directory. Since Internet Explorer is deprecated and in most instances, not even installed on Windows Server, Microsoft recommends turning off Internet Explorer Enhanced Security Configuration. To turn off Internet Explorer Enhanced Security Configuration:

1. Sign into the server where the Intune Connector for Active Directory is being installed with an account that has local administrator rights.

1. Open **Server Manager**.

1. In the left pane of Server Manager, select **Local Server**.

1. In the right **PROPERTIES** pane of Server Manager, select the **On** or **Off** link next to **IE Enhanced Security Configuration**.

1. In the **Internet Explorer Enhanced Security Configuration** window, select **Off** under **Administrators:**, and then select **OK**.

#### Download the Intune Connector for Active Directory

1. On the server where the Intune Connector for Active Directory is being installed, sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left hand pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, under **Device onboarding**, select **Enrollment**.

1. In the **Windows | Windows enrollment** screen, under **Windows Autopilot**, select **Intune Connector for Active Directory**.

1. In the **Intune Connector for Active Directory** screen, select **Add**.

1. In the **Add connector** window that opens, under **Configuring the Intune Connector for Active Directory**, select **Download the on-premises Intune Connector for Active Directory**. The link downloads a file called `ODJConnectorBootstrapper.exe`.

#### Install the Intune Connector for Active Directory on the server

> [!IMPORTANT]
>
> The Intune Connector for Active Directory installation needs to be done with an account that has the following domain rights:
>
> - **Required** - Create **msDs-ManagedServiceAccount** objects in the Managed Service Accounts container.
> - **Optional** - Modify permissions in OUs in Active Directory - if the administrator installing the updated Intune Connector for Active Directory doesn't have this right, additional configuration steps are required by an administrator who has these rights. For more information, see the step/section **Increase the computer account limit in the Organizational Unit**.

1. If the previous legacy Intune Connector for Active Directory is installed, uninstall it first before installing the updated Intune Connector for Active Directory. For more information, see [Uninstall the Intune Connector for Active Directory](/autopilot/windows-autopilot-hybrid#uninstall-the-intune-connector-for-active-directory).

    > [!IMPORTANT]
    >
    > When uninstalling the previous legacy Intune Connector for Active Directory, make sure to run the legacy **Intune Connector for Active Directory** installer as part of the uninstall process. If the legacy Intune Connector for Active Directory installer prompts to **Uninstall** it when it's run, select to uninstall it. This step ensures that the previous legacy Intune Connector for Active Directory is fully uninstalled. The legacy Intune Connector for Active Directory installer can be downloaded from [Intune Connector for Active Directory](https://www.microsoft.com/download/details.aspx?id=105392&msockid=3cb707200c316b2c119712450d8b6a5d).

    > [!TIP]
    >
    > In domains with only a single Intune Connector for Active Directory, Microsoft recommends first installing the updated Intune Connector for Active Directory on another server. Installing the updated Intune Connector for Active Directory on another server should be done before uninstalling the legacy Intune Connector for Active Directory on the current server. Installing the Intune Connector for Active Directory on another first avoids any downtime while the Intune Connector for Active Directory is being updated on the current server.

1. Open the `ODJConnectorBootstrapper.exe` file that downloaded to launch the **Intune Connector for Active Directory Setup** install.

1. Step through the **Intune Connector for Active Directory Setup** install.

1. At the end of the install, select the checkbox **Launch Intune Connector for Active Directory**.

    > [!NOTE]
    >
    > If **Intune Connector for Active Directory Setup** install is accidentally closed without selecting the checkbox **Launch Intune Connector for Active Directory**, the **Intune Connector for Active Directory** configuration can be reopened by selecting **Intune Connector for Active Directory** > **Intune Connector for Active Directory** from the **Start** menu.

#### Sign in to the Intune Connector for Active Directory

1. In the **Intune Connector for Active Directory** window, under the **Enrollment** tab, select **Sign In**.

1. Under the **Sign In** tab, sign in with the Microsoft Entra ID credentials of an Intune administrator role. The user account must have an assigned Intune license. The sign in process might take a few minutes to complete.

    > [!NOTE]
    >
    > The account used to enroll the Intune Connector for Active Directory is only a temporary requirement at the time of installation. The account isn't used going forward after the server is enrolled.

1. Once the sign in process completes:

   1. A **The Intune Connector for Active Directory successfully enrolled** confirmation window appears. Select **OK** to close the window.
   1. An **A Managed Service Account with name "<MSA_name>" was successfully set up** confirmation window appears. The name of the MSA is in the format `msaODJ#####` where **#####** are five random characters. Notate the name of the MSA that was created, and then select **OK** to close the window. The name of the MSA might be needed later to configure the MSA to allow creating computer objects in OUs.

1. The **Enrollment** tab shows **Intune Connector for Active Directory is enrolled**. The **Sign In** button is greyed out and **Configure Managed Service Account** is enabled.

1. Close the **Intune Connector for Active Directory** window.

#### Verify the Intune Connector for Active Directory is active

After authenticating, the Intune Connector for Active Directory finishes installing. Once it finishes installing, verify that it's active in Intune by following these steps:

1. Go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) if it's still open. If the **Add connector** window is still displayed, close it.

    If the **Microsoft Intune admin center** isn't still open:

   1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

   1. In the **Home** screen, select **Devices** in the left hand pane.

   1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

   1. In the **Windows | Windows devices** screen, under **Device onboarding**, select **Enrollment**.

   1. In the **Windows | Windows enrollment** screen, under **Windows Autopilot**, select **Intune Connector for Active Directory**.

1. In the **Intune Connector for Active Directory** page:

    - Confirm that the server is displayed under **Connector name** and shows as **Active** under **Status**
    - For the updated Intune Connector for Active Directory, make sure the version is greater than **6.2407.2000.8**.

    If the server isn't displayed, select **Refresh** or navigate away from the page, and then navigate back to the **Intune Connector for Active Directory** page.

> [!NOTE]
>
> - It can take several minutes for the newly enrolled server to appear in the **Intune Connector for Active Directory** page of the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). The enrolled server only appears if it can successfully communicate with the Intune service.
>
> - Inactive Intune Connectors for Active Directory still appear in the **Intune Connector for Active Directory** page and will automatically be cleaned up after 30 days.

After the Intune Connector for Active Directory is installed, it will start logging in the **Event Viewer** under the path **Applications and Services Logs** > **Microsoft** > **Intune** > **ODJConnectorService**. Under this path, **Admin** and **Operational** logs can be found.

#### Configure the MSA to allow creating objects in OUs (optional)

By default, MSAs only have access to create computer objects in the **Computers** container. MSAs don't have access to create computer objects in Organizational Units (OUs). To allow the MSA to create objects in OUs, the OUs need to be added to the `ODJConnectorEnrollmentWiazard.exe.config` XML file found in `ODJConnectorEnrollmentWizard` directory where the Intune Connector for Active Directory was installed, normally `C:\Program Files\Microsoft Intune\ODJConnector\`.

To configure the MSA to allow creating objects in OUs, follow these steps:

1. On the server where the Intune Connector for Active Directory is installed, navigate to `ODJConnectorEnrollmentWizard` directory where the Intune Connector for Active Directory was installed, normally `C:\Program Files\Microsoft Intune\ODJConnector\`.

1. In the `ODJConnectorEnrollmentWizard` directory, open the `ODJConnectorEnrollmentWiazard.exe.config` XML file in a text editor, for example, **Notepad**.

1. In the `ODJConnectorEnrollmentWiazard.exe.config` XML file, add in any desired OUs that the MSA should have access to create computer objects in. The OU name should be the distinguished name and if applicable, needs to be escaped. The following example is an example XML entry with the OU distinguished name:

    ```xml
      <appSettings>

        <!-- Semicolon separated list of OUs that will be used for Hybrid Autopilot, using LDAP distinguished name format.
            The ODJ Connector will only have permission to create computer objects in these OUs.
            The value here should be the same as the value in the Hybrid Autopilot configuration profile in the Azure portal - https://learn.microsoft.com/en-us/mem/intune/configuration/domain-join-configure

            Usage example (NOTE: PLEASE ENSURE THAT THE DISTINGUISHED NAME IS ESCAPED PROPERLY):
            Domain contains the following OUs:
              - OU=HybridDevices,DC=contoso,DC=com
              - OU=HybridDevices2,OU=IntermediateOU,OU=TopLevelOU,DC=contoso,DC=com

            Value: "OU=HybridDevices,DC=contoso,DC=com;OU=HybridDevices2,OU=IntermediateOU,OU=TopLevelOU,DC=contoso,DC=com" -->

        <add key="OrganizationalUnitsUsedForOfflineDomainJoin" value="OU=SubOU,OU=TopLevelOU,DC=contoso,DC=com;OU=Mine,DC=contoso,DC=com" />
      </appSettings>
    ```

1. Once all desired OUs are added, save the `ODJConnectorEnrollmentWiazard.exe.config` XML file.

1. As an administrator that has appropriate permissions to modify OU permissions, open the **Intune Connector for Active Directory** by navigating to **Intune Connector for Active Directory** > **Intune Connector for Active Directory** from the **Start** menu.

    > [!IMPORTANT]
    >
    > If the administrator installing and configuring the Intune Connector for Active Directory doesn't have permissions to modify OU permissions, then the section/steps **Increase the computer account limit in the Organizational Unit** need to be followed instead by an administrator that does have permissions to modify OU permissions.

1. Under the **Enrollment** tab in the **Intune Connector for Active Directory** window, select **Configure Managed Service Account**.

1. An **A Managed Service Account with name "<MSA_name>" was successfully set up** confirmation window appears. Select **OK** to close the window.

### [:::image type="icon" source="/autopilot/images/icons/software-18.svg"::: **Legacy Connector**](#tab/legacy-connector)

> [!IMPORTANT]
>
> The legacy Intune Connector for Active Directory is deprecated. These instructions assume that the legacy Intune Connector for Active Directory is already installed or is already downloaded. Best practice is to download and install the [updated Intune Connector for Active Directory](/autopilot/windows-autopilot-hybrid?tabs=updated-connector#install-the-intune-connector).

Before beginning the installation, make sure that all of the [Intune connector server requirements](/autopilot/windows-autopilot-hybrid?tabs=intune-connector-requirements#requirements) are met.

#### Disable Internet Explorer Enhanced Security Configuration

By default Windows Server has Internet Explorer Enhanced Security Configuration turned on. Internet Explorer Enhanced Security Configuration might cause problems signing into the Intune Connector for Active Directory. Since Internet Explorer is deprecated and in most instances, not even installed on Windows Server, Microsoft recommends turning off Internet Explorer Enhanced Security Configuration. To turn off Internet Explorer Enhanced Security Configuration:

1. Sign into the server where the Intune Connector for Active Directory is being installed with an account that has local administrator rights and domain admin rights. Domain admin rights are required so that the Intune Connector for Active Directory installer can properly create an MSA.

1. Open **Server Manager**.

1. In the left pane of Server Manager, select **Local Server**.

1. In the right **PROPERTIES** pane of Server Manager, select the **On** or **Off** link next to **IE Enhanced Security Configuration**.

1. In the **Internet Explorer Enhanced Security Configuration** window, select **Off** under **Administrators:**, and then select **OK**.

#### Install the legacy Intune Connector for Active Directory on the server

1. Open the previously downloaded `ODJConnectorBootstrapper.exe` file to launch the **Intune Connector for Active Directory Setup** install.

    > [!NOTE]
    >
    > If the legacy Intune Connector for Active Directory is already installed, go to the **Start** menu > **Intune Connector for Active Directory** > **Intune Connector for Active Directory**, and then proceed to [Sign in to the legacy Intune Connector for Active Directory](#sign-in-to-the-legacy-intune-connector).

1. In the **Intune Connector for Active Directory Setup** installer window, select **I agree to the license terms and conditions**, and then select **Install**.

    > [!NOTE]
    >
    > If an install location other than the default of **C:\Program Files\Microsoft Intune\ODJConnector** is desired, select **Options** and specify the desired install location.

1. When the install completes, select **Configure Now** in the **Intune Connector for Active Directory Setup** installer window.

    > [!NOTE]
    >
    > If **Close** is accidentally selected or the **Intune Connector for Active Directory Setup** installer window is accidentally closed, the **Intune Connector for Active Directory** configuration can be accessed by selecting **Intune Connector for Active Directory** > **Intune Connector for Active Directory** from the **Start** menu.

#### Sign in to the legacy Intune Connector

1. In the **Intune Connector for Active Directory** window, under the **Enrollment** tab, select **Sign In**.

1. Under the **Sign In** tab, sign in with the credentials of an Intune administrator role. The user account must have an assigned Intune license. The sign in process might take a few minutes to complete.

    > [!NOTE]
    >
    > The account used to enroll the Intune Connector for Active Directory is only a temporary requirement at the time of installation. The account isn't used going forward after the server is enrolled.

1. Once the sign in process is complete, a **The Intune Connector for Active Directory successfully enrolled** confirmation window appears. Select **OK** to close the window.

1. The **Enrollment** tab shows **Intune Connector for Active Directory is enrolled** and the **Sign In** button is greyed out.

1. Close the **Intune Connector for Active Directory** window.

#### Verify the legacy Intune Connector for Active Directory is active

After authenticating, the Intune Connector for Active Directory finishes installing. Once it finishes installing, verify that it's active in Intune by following these steps:

1. Go to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) if it's still open. If the **Add connector** window is still displayed, close it.

    If the **Microsoft Intune admin center** isn't still open:

   1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

   1. In the **Home** screen, select **Devices** in the left hand pane.

   1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

   1. In the **Windows | Windows devices** screen, under **Device onboarding**, select **Enrollment**.

   1. In the **Windows | Windows enrollment** screen, under **Windows Autopilot**, select **Intune Connector for Active Directory**.

1. In the **Intune Connector for Active Directory** page, confirm that the server is displayed under **Connector name** and shows as **Active** under **Status**. If the server isn't displayed, select **Refresh** or navigate away from the page, and then navigate back to the **Intune Connector for Active Directory** page.

> [!NOTE]
>
> - It can take several minutes for the newly enrolled server to appear in the **Intune Connector for Active Directory** page of the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). The enrolled server only appears if it can successfully communicate with the Intune service.
>
> - Inactive Intune Connectors for Active Directory still appear in the **Intune Connector for Active Directory** page and will automatically be cleaned up after 30 days.

After the Intune Connector for Active Directory is installed, it will start logging in the **Event Viewer** under the path **Applications and Services Logs** > **Microsoft** > **Intune** > **ODJConnectorService**. Under this path, **Admin** and **Operational** logs can be found.

---
