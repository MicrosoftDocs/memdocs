---
author: frankroj
ms.author: frankroj
manager: aaroncz
ms.subservice: autopilot
ms.service: windows-client
ms.topic: include
ms.date: 06/28/2024
ms.localizationpriority: medium
---

<!-- This file is shared by the following articles:

pre-provisioning/hybrid-azure-ad-join-intune-connector.md
user-driven/hybrid-azure-ad-join-intune-connector.md

Headings are driven by article context. -->

### Turn off Internet Explorer Enhanced Security Configuration

1. Sign into the server where the Intune Connector is being installed with an account that has local administrator rights.

1. Turn off **Internet Explorer Enhanced Security Configuration** on the server. By default Windows Server has **Internet Explorer Enhanced Security Configuration** turned on. To turn off **Internet Explorer Enhanced Security Configuration**:

   1. On the server where the Intune Connector is being installed, open **Server Manager**.

   1. In the left pane of Server Manager, select **Local Server**.

   1. In the right **PROPERTIES** pane of Server Manager, select the **On** or **Off** link next to **IE Enhanced Security Configuration**.

   1. In the **Internet Explorer Enhanced Security Configuration** window, select **Off** under **Administrators:**, and then select **OK**.

### Download the Intune Connector

1. On the server where the Intune Connector is being installed, Sign into the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).

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
