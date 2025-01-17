---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.reviewer: madakeva
ms.subservice: autopilot
ms.service: windows-client
ms.topic: include
ms.date: 01/17/2025
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

pre-provisioning/hybrid-azure-ad-join-intune-connector.md
user-driven/hybrid-azure-ad-join-intune-connector.md

Headings are driven by article context. -->

## Install the Intune Connector

> [!IMPORTANT]
>
> Intune 2501 uses an updated Intune Connector that strengths security and follows least privilege principles by using a [Managed Service Account (MSA)](/windows-server/identity/ad-ds/manage/group-managed-service-accounts/group-managed-service-accounts/group-managed-service-accounts-overview). When downloading the Intune Connector, the updated Intune Connector is downloaded. The previous legacy Intune Connector is no longer available for download. The previous legacy Intune Connector will still continue to work through the end of March 2025, but needs to be updated to the updated Intune Connector before then to avoid loss of functionality. For more information, see [blog]().

### [:::image type="icon" source="images/icons/software-18.svg"::: **Updated Connector**](#tab/updated-connector)

Before beginning the installation, make sure that all of the [Intune connector server requirements](../../windows-autopilot-hybrid.md?tabs=intune-connector-requirements#requirements) are met.

#### Install steps for the updated Intune connector

#### Turn off Internet Explorer Enhanced Security Configuration

By default Windows Server has Internet Explorer Enhanced Security Configuration turned on. Internet Explorer Enhanced Security Configuration might cause problems signing into the Intune Connector for Active Directory. Since Internet Explorer is deprecated and in most instances, not even installed on Windows Server, Microsoft recommends to turn off Internet Explorer Enhanced Security Configuration.  To turn off Internet Explorer Enhanced Security Configuration:

1. On the server where the Intune Connector is being installed, open **Server Manager**.

1. In the left pane of Server Manager, select **Local Server**.

1. In the right **PROPERTIES** pane of Server Manager, select the **On** or **Off** link next to **IE Enhanced Security Configuration**.

1. In the **Internet Explorer Enhanced Security Configuration** window, select **Off** under **Administrators:**, and then select **OK**.

### Download the Intune Connector

1. On the server where the Intune Connector is being installed, sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left hand pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, under **Device onboarding**, select **Enrollment**.

1. In the **Windows | Windows enrollment** screen, under **Windows Autopilot**, select **Intune Connector for Active Directory**.

1. In the **Intune Connector for Active Directory** screen, select **Add**.

1. In the **Add connector** window that opens, under **Configuring the Intune connector for Active Directory**, select **Download the on-premises Intune Connector for Active Directory**. The link downloads a file called **ODJConnectorSetupMsi.msi**.

### Install the Intune Connector on the server

1. If the previous legacy Intune Connector is installed, uninstall it first before installing the updated Intune Connector. For more information, see [Uninstall the ODJ Connector](../../windows-autopilot-hybrid.md#uninstall-the-odj-connector).

1. Open the **ODJConnectorSetupMsi.msi** file that downloaded to launch the **Intune Connector for Active Directory Setup** install.

1. Step through the **Intune Connector for Active Directory Setup** install. At the end of the install, select the checkbox **Launch Intune connector for Active Directory**.

    > [!NOTE]
    >
    > If **Intune Connector for Active Directory Setup** install is accidentally closed without selecting the checkbox **Launch Intune connector for Active Directory**., the **Intune Connector for Active Directory** configuration can be accessed by selecting **Intune connector for Active Directory** > **Intune connector for Active Directory** from the **Start** menu.

1. In the **Intune connector for Active Directory** window, select **Sign In**.

1. Enter the credentials of an Intune administrator role. The user account must have an assigned Intune license.

    > [!NOTE]
    >
    > The Intune administrator role is a temporary requirement at the time of installation.

After authenticating, the Intune Connector for Active Directory finishes installing. Once it finishes installing, verify that it is active in Intune by following these steps:

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left hand pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, under **Device onboarding**, select **Enrollment**.

1. In the **Windows | Windows enrollment** screen, under **Windows Autopilot**, select **Intune Connector for Active Directory**.

1. Confirm that the connection status in the **Status** column is **Active**.

> [!NOTE]
>
> After signing into the Connector, it can take several minutes to appear in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). It appears only if it can successfully communicate with the Intune service.

After the Intune Connector for Active Directory is installed, it will start logging in the **Event Viewer** under the path **Applications and Services Logs** > **Microsoft** > **Intune** > **ODJConnectorService**. Under this path, **Admin** and **Operational** logs can be found.

### [:::image type="icon" source="images/icons/software-18.svg"::: **Legacy Connector**](#tab/legacy-connector)

> [!IMPORTANT]
>
> The legacy Intune Connector is deprecated and no longer available for download. These instructions assume that the legacy Intune Connector is already downloaded or installed. Best practices is to download and install the [updated Intune Connector](../../windows-autopilot-hybrid.md?tabs=updated-connector#install-the-intune-connector).

Before beginning the installation, make sure that all of the [Intune connector server requirements](../../windows-autopilot-hybrid.md?tabs=intune-connector-requirements#requirements) are met.

#### Install steps for the legacy Intune connector

#### Turn off Internet Explorer Enhanced Security Configuration

By default Windows Server has Internet Explorer Enhanced Security Configuration turned on. Internet Explorer Enhanced Security Configuration might cause problems signing into the Intune Connector for Active Directory. Since Internet Explorer is deprecated and in most instances, not even installed on Windows Server, Microsoft recommends to turn off Internet Explorer Enhanced Security Configuration.  To turn off Internet Explorer Enhanced Security Configuration:

1. On the server where the Intune Connector is being installed, open **Server Manager**.

1. In the left pane of Server Manager, select **Local Server**.

1. In the right **PROPERTIES** pane of Server Manager, select the **On** or **Off** link next to **IE Enhanced Security Configuration**.

1. In the **Internet Explorer Enhanced Security Configuration** window, select **Off** under **Administrators:**, and then select **OK**.

### Install the Intune Connector on the server

1. Open the previously downloaded Connector setup file, *ODJConnectorBootstrapper.exe*, to install the legacy Intune Connector.

> [!NOTE]
>
> If the legacy Intune Connector is already installed, go to the **Start** menu > **Intune Connector for Active Directory** > **Intune Connector for Active Directory**.

1. At the end of the setup, select **Configure Now**.

1. Select **Sign In**.

1. Enter the credentials of an Intune administrator role. The user account must have an assigned Intune license.

> [!NOTE]
>
> The Intune administrator role is a temporary requirement at the time of installation.

After authenticating, the Intune Connector for Active Directory finishes installing. Once it finishes installing, verify that it is active in Intune by following these steps:

1. Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left hand pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, under **Device onboarding**, select **Enrollment**.

1. In the **Windows | Windows enrollment** screen, under **Windows Autopilot**, select **Intune Connector for Active Directory**.

1. Confirm that the connection status in the **Status** column is **Active**.

> [!NOTE]
>
> After signing into the Connector, it can take several minutes to appear in the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). It appears only if it can successfully communicate with the Intune service.

After the Intune Connector for Active Directory is installed, it will start logging in the **Event Viewer** under the path **Applications and Services Logs** > **Microsoft** > **Intune** > **ODJConnectorService**. Under this path, **Admin** and **Operational** logs can be found.



---







### Turn off Internet Explorer Enhanced Security Configuration

1. Sign into the server where the Intune Connector is being installed with an account that has local administrator rights.

1. Turn off **Internet Explorer Enhanced Security Configuration** on the server. By default Windows Server has **Internet Explorer Enhanced Security Configuration** turned on. To turn off **Internet Explorer Enhanced Security Configuration**:

   1. On the server where the Intune Connector is being installed, open **Server Manager**.

   1. In the left pane of Server Manager, select **Local Server**.

   1. In the right **PROPERTIES** pane of Server Manager, select the **On** or **Off** link next to **IE Enhanced Security Configuration**.

   1. In the **Internet Explorer Enhanced Security Configuration** window, select **Off** under **Administrators:**, and then select **OK**.

### Download the Intune Connector

1. On the server where the Intune Connector is being installed, sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

1. In the **Home** screen, select **Devices** in the left hand pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, under **Device onboarding**, select **Enrollment**.

1. In the **Windows | Windows enrollment** screen, under **Windows Autopilot**, select **Intune Connector for Active Directory**.

1. In the **Intune Connector for Active Directory** page, select **Add**.

1. In the **Add connector** window that opens, select **Download the on-premises Intune Connector for Active Directory** under step 2 of **Configuring the Intune connector for Active Directory**. The link downloads a file called **ODJConnectorBootstrapper.exe**.

### Install the Intune Connector on the server

1. Open the **ODJConnectorBootstrapper.exe** file that downloaded to launch the Intune Connector install.

1. In the **Intune Connector for Active Directory Setup** installer window, select **I agree to the license terms and conditions**, and then select **Install**.

    > [!NOTE]
    >
    > If an install location other than the default of **C:\Program Files\Microsoft Intune\ODJConnector** is desired, select **Options** and specify the desired install location.

1. When the install completes, select **Configure Now** in the **Intune Connector for Active Directory Setup** installer window.

    > [!NOTE]
    >
    > If **Close** is accidentally selected or the **Intune Connector for Active Directory Setup** installer window is accidentally closed, the **Intune Connector for Active Directory** configuration can be accessed by selecting **Intune connector for Active Directory** > **Intune connector for Active Directory** from the **Start** menu.

1. In the **Intune connector for Active Directory** window:

   1. Under the **Enrollment** tab, select **Sign In**.

   1. Under the **Sign In** tab, sign in with the credentials of an Intune administrator role. The user account must have an assigned Intune license. The sign in process might take a few minutes to complete.

   1. Once the sign in process is complete, a **The Intune connector for Active Directory successfully enrolled** confirmation window appears. Select **OK** to close the window. The **Enrollment** tab shows **Intune connector for Active Directory is enrolled** and the **Sign In** button is greyed out.

   1. Close the **Intune connector for Active Directory** window.

1. In the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431), close the **Add connector** window if it's still displayed.

1. In the **Intune Connector for Active Directory** page, confirm that the server is displayed under **Connector name** and shows as **Active** under **Status**. If the server isn't displayed, select **Refresh** or navigate away from the page, and then navigate back to the **Intune Connector for Active Directory** page.

> [!NOTE]
>
> - The account used to enroll the Intune connector is only a temporary requirement at the time of installation. The account isn't used going forward after the server is enrolled.
>
> - It can take several minutes for the newly enrolled server to appear in the **Intune Connector for Active Directory** page of the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431). The enrolled server only appears if it can successfully communicate with the Intune service.

After the Intune Connector is installed, it will start logging in the **Event Viewer** under the path **Applications and Services Logs** > **Microsoft** > **Intune** > **ODJConnectorService**. Under this path, the **Admin** and **Operational** logs are found.
