---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.reviewer: madakeva
ms.subservice: autopilot
ms.service: windows-client
ms.topic: include
ms.date: 01/21/2025
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

pre-provisioning/hybrid-azure-ad-join-intune-connector
user-driven/hybrid-azure-ad-join-intune-connector

Headings are driven by article context. -->

> [!IMPORTANT]
>
> Starting with Intune 2501, Intune uses an updated Intune Connector that strengths security and follows least privilege principles by using a [Managed Service Account (MSA)](/windows-server/identity/ad-ds/manage/group-managed-service-accounts/group-managed-service-accounts/group-managed-service-accounts-overview). When the Intune Connector is downloaded, the updated Intune Connector is downloaded. The previous legacy Intune Connector is no longer available for download. The previous legacy Intune Connector will continue to work through the end of March 2025, but needs to be updated to the updated Intune Connector before then to avoid loss of functionality. For more information, see [blog]().

Select the tab that corresponds to the version of the Intune Connector that is being installed:

### [:::image type="icon" source="/autopilot/images/icons/software-18.svg"::: **Updated Connector**](#tab/updated-connector)

Before beginning the installation, make sure that all of the [Intune connector server requirements](/autopilot/windows-autopilot-hybrid?tabs=intune-connector-requirements#requirements) are met.

#### Turn off Internet Explorer Enhanced Security Configuration

By default Windows Server has Internet Explorer Enhanced Security Configuration turned on. Internet Explorer Enhanced Security Configuration might cause problems signing into the Intune Connector for Active Directory. Since Internet Explorer is deprecated and in most instances, not even installed on Windows Server, Microsoft recommends turning off Internet Explorer Enhanced Security Configuration. To turn off Internet Explorer Enhanced Security Configuration:

1. Sign into the server where the Intune Connector is being installed with an account that has local administrator rights.

1. Open **Server Manager**.

1. In the left pane of Server Manager, select **Local Server**.

1. In the right **PROPERTIES** pane of Server Manager, select the **On** or **Off** link next to **IE Enhanced Security Configuration**.

1. In the **Internet Explorer Enhanced Security Configuration** window, select **Off** under **Administrators:**, and then select **OK**.

#### Download the Intune Connector

1. On the server where the Intune Connector is being installed, sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left hand pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, under **Device onboarding**, select **Enrollment**.

1. In the **Windows | Windows enrollment** screen, under **Windows Autopilot**, select **Intune Connector for Active Directory**.

1. In the **Intune Connector for Active Directory** screen, select **Add**.

1. In the **Add connector** window that opens, under **Configuring the Intune connector for Active Directory**, select **Download the on-premises Intune Connector for Active Directory**. The link downloads a file called **ODJConnectorSetupMsi.msi**.

#### Install the Intune Connector on the server

1. If the previous legacy Intune Connector is installed, uninstall it first before installing the updated Intune Connector. For more information, see [Uninstall the ODJ Connector](/autopilot/windows-autopilot-hybrid#uninstall-the-odj-connector).

1. Open the **ODJConnectorSetupMsi.msi** file that downloaded to launch the **Intune Connector for Active Directory Setup** install.

1. Step through the **Intune Connector for Active Directory Setup** install.

1. At the end of the install, select the checkbox **Launch Intune connector for Active Directory**.

    > [!NOTE]
    >
    > If **Intune Connector for Active Directory Setup** install is accidentally closed without selecting the checkbox **Launch Intune connector for Active Directory**, the **Intune Connector for Active Directory** configuration can be reopened by selecting **Intune connector for Active Directory** > **Intune connector for Active Directory** from the **Start** menu.

#### Sign in to the Intune Connector

1. In the **Intune connector for Active Directory** window, under the **Enrollment** tab, select **Sign In**.

1. Under the **Sign In** tab, sign in with the credentials of an Intune administrator role. The user account must have an assigned Intune license. The sign in process might take a few minutes to complete.

    > [!NOTE]
    >
    > The account used to enroll the Intune connector is only a temporary requirement at the time of installation. The account isn't used going forward after the server is enrolled.

1. Once the sign in process completes:

   1. A **The Intune connector for Active Directory successfully enrolled** confirmation window appears. Select **OK** to close the window.
   1. An **A Managed Service Account with name "<MSA_name>" was successfully set up** confirmation window appears. Notate the name of the MSA that was created, and then select **OK** to close the window.

1. The **Enrollment** tab shows **Intune connector for Active Directory is enrolled**. The **Sign In** button is greyed out and **Configure Managed Service Account** is enabled.

1. Close the **Intune connector for Active Directory** window.

#### Verify the Intune Connector is active

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
> - Inactive Intune connectors still appear in the Intune Connectors page and will automatically be cleaned up after 30 days.

After the Intune Connector for Active Directory is installed, it will start logging in the **Event Viewer** under the path **Applications and Services Logs** > **Microsoft** > **Intune** > **ODJConnectorService**. Under this path, **Admin** and **Operational** logs can be found.

#### Configure the MSA to allow creating objects in OUs

By default, MSAs only have access to create computer objects in the **Computers** container. MSAs don't have access to create computer objects in Organizational Units (OUs). To allow the MSA to create objects in OUs, the OUs need to be added to the `ODJConnectorEnrollmentWiazard.exe.config` XML file found in `ODJConnectorEnrollmentWizard` directory where the Intune Connector was installed, normally `C:\Program Files\Microsoft Intune\ODJConnector\`.

To configure the MSA to allow creating objects in OUs, follow these steps:

1. On the server where the Intune Connector is installed, navigate to `ODJConnectorEnrollmentWizard` directory where the Intune Connector was installed, normally `C:\Program Files\Microsoft Intune\ODJConnector\`.

1. In the `ODJConnectorEnrollmentWizard` directory, open the `ODJConnectorEnrollmentWiazard.exe.config` XML file in a text editor, for example, **Notepad**.

1. In the `ODJConnectorEnrollmentWiazard.exe.config` XML file, add in any desired OUs that the MSA should have access to create computer objects in. The OU name should be the distinguished name and if applicable, needs to be escaped.

1. Once all desired OUs are added, save the `ODJConnectorEnrollmentWiazard.exe.config` XML file.

1. Open the **Intune connector for Active Directory** by navigating to **Intune connector for Active Directory** > **Intune connector for Active Directory** from the **Start** menu.

1. Under the **Enrollment** tab in the **Intune connector for Active Directory** window, select **Configure Managed Service Account**.

1. An **A Managed Service Account with name "<MSA_name>" was successfully set up** confirmation window appears. Select **OK** to close the window.

### [:::image type="icon" source="/autopilot/images/icons/software-18.svg"::: **Legacy Connector**](#tab/legacy-connector)

> [!IMPORTANT]
>
> The legacy Intune Connector is deprecated and no longer available for download. These instructions assume that the legacy Intune Connector is already installed or is already downloaded. Best practice is to download and install the [updated Intune Connector](/autopilot/windows-autopilot-hybrid?tabs=updated-connector#install-the-intune-connector).

Before beginning the installation, make sure that all of the [Intune connector server requirements](/autopilot/windows-autopilot-hybrid?tabs=intune-connector-requirements#requirements) are met.

#### Disable Internet Explorer Enhanced Security Configuration

By default Windows Server has Internet Explorer Enhanced Security Configuration turned on. Internet Explorer Enhanced Security Configuration might cause problems signing into the Intune Connector for Active Directory. Since Internet Explorer is deprecated and in most instances, not even installed on Windows Server, Microsoft recommends turning off Internet Explorer Enhanced Security Configuration. To turn off Internet Explorer Enhanced Security Configuration:

1. Sign into the server where the Intune Connector is being installed with an account that has local administrator rights.

1. Open **Server Manager**.

1. In the left pane of Server Manager, select **Local Server**.

1. In the right **PROPERTIES** pane of Server Manager, select the **On** or **Off** link next to **IE Enhanced Security Configuration**.

1. In the **Internet Explorer Enhanced Security Configuration** window, select **Off** under **Administrators:**, and then select **OK**.

#### Install the legacy Intune Connector on the server

1. Open the previously downloaded **ODJConnectorBootstrapper.exe** file to launch the **Intune Connector for Active Directory Setup** install.

    > [!NOTE]
    >
    > If the legacy Intune Connector is already installed, go to the **Start** menu > **Intune Connector for Active Directory** > **Intune Connector for Active Directory**, and then proceed to [Sign in to the legacy Intune Connector](#sign-in-to-the-legacy-intune-connector).

1. In the **Intune Connector for Active Directory Setup** installer window, select **I agree to the license terms and conditions**, and then select **Install**.

    > [!NOTE]
    >
    > If an install location other than the default of **C:\Program Files\Microsoft Intune\ODJConnector** is desired, select **Options** and specify the desired install location.

1. When the install completes, select **Configure Now** in the **Intune Connector for Active Directory Setup** installer window.

    > [!NOTE]
    >
    > If **Close** is accidentally selected or the **Intune Connector for Active Directory Setup** installer window is accidentally closed, the **Intune Connector for Active Directory** configuration can be accessed by selecting **Intune connector for Active Directory** > **Intune connector for Active Directory** from the **Start** menu.

#### Sign in to the legacy Intune Connector

1. In the **Intune connector for Active Directory** window, under the **Enrollment** tab, select **Sign In**.

1. Under the **Sign In** tab, sign in with the credentials of an Intune administrator role. The user account must have an assigned Intune license. The sign in process might take a few minutes to complete.

    > [!NOTE]
    >
    > The account used to enroll the Intune connector is only a temporary requirement at the time of installation. The account isn't used going forward after the server is enrolled.

1. Once the sign in process is complete, a **The Intune connector for Active Directory successfully enrolled** confirmation window appears. Select **OK** to close the window.

1. The **Enrollment** tab shows **Intune connector for Active Directory is enrolled** and the **Sign In** button is greyed out.

1. Close the **Intune connector for Active Directory** window.

#### Verify the legacy Intune Connector is active

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
> - Inactive Intune connectors still appear in the Intune Connectors page and will automatically be cleaned up after 30 days.

After the Intune Connector for Active Directory is installed, it will start logging in the **Event Viewer** under the path **Applications and Services Logs** > **Microsoft** > **Intune** > **ODJConnectorService**. Under this path, **Admin** and **Operational** logs can be found.

---
