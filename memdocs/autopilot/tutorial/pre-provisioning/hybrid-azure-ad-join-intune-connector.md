---
title: Windows Autopilot for pre-provisioned deployment hybrid Azure AD join - Step 2 of 11 - Install the Intune Connector
description: How to - Windows Autopilot for pre-provisioned deployment hybrid Azure AD join - Step 2 of 11 - Install the Intune Connector(ESP).
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 04/11/2023
ms.topic: tutorial
ms.collection: 
  - tier1
  - highpri
ms.technology: itpro-deploy
appliesto:
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 11</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/supported-versions-windows-client" target="_blank">Windows 10</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/windows-server-release-info" target="_blank">Windows Server 2022</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/windows-server-release-info" target="_blank">Windows Server 2019</a>
  - ✅ <a href="https://learn.microsoft.com/windows/release-health/windows-server-release-info" target="_blank">Windows Server 2016</a>
---

# Pre-provision hybrid Azure AD join: Install the Intune Connector

Windows Autopilot for pre-provisioned deployment hybrid Azure AD join steps:
- Step 1: [Set up Windows automatic Intune enrollment](hybrid-azure-ad-join-automatic-enrollment.md)
> [!div class="checklist"]
> - **Step 2: Install the Intune Connector**
- Step 3: [Increase the computer account limit in the Organizational Unit (OU)](hybrid-azure-ad-join-computer-account-limit.md)
- Step 4: [Register devices as Autopilot devices](hybrid-azure-ad-join-register-device.md)
- Step 5: [Create a device group](hybrid-azure-ad-join-device-group.md)
- Step 6: [Configure and assign Autopilot Enrollment Status Page (ESP)](hybrid-azure-ad-join-esp.md)
- Step 7: [Create and assign hybrid Azure AD join Autopilot profile](hybrid-azure-ad-join-autopilot-profile.md)
- Step 8: [Configure and assign domain join profile](hybrid-azure-ad-join-domain-join-profile.md)
- Step 9: [Assign Autopilot device to a user (optional)](hybrid-azure-ad-join-assign-device-to-user.md)
- Step 10: [Technician flow](hybrid-azure-ad-join-technician-flow.md)
- Step 11: [User flow](hybrid-azure-ad-join-user-flow.md)

For an overview of the Windows Autopilot for pre-provisioned deployment hybrid Azure AD join workflow, see [Windows Autopilot for pre-provisioned deployment hybrid Azure AD join overview](hybrid-azure-ad-join-workflow.md)

> [!NOTE]
>
> If you've already set up the Intune Connector as part of the [Windows Autopilot user-driven hybrid Azure AD join](../user-driven/hybrid-azure-ad-join-workflow.md) scenario, you can skip this step and move on to [Step 3: Increase the computer account limit in the Organizational Unit (OU)].

## Install the Intune Connector

1. Sign into the server where the Intune Connector is being installed with an account that has local administrator rights.

1. Turn off Internet Explorer Enhanced Security Configuration on the server. By default Windows Server has Internet Explorer Enhanced Security Configuration turned on. To turn off Internet Explorer Enhanced Security Configuration:

   1. On the server where the Intune Connector is being installed, open **Server Manager**.

   1. In the left pane of Server Manager, select **Local Server**.

   1. In the right **PROPERTIES** pane of Server Manager, select the **On** or **Off** link next to **IE Enhanced Security Configuration**.

   1. In the **Internet Explorer Enhanced Security Configuration** window, select **Off** under **Administrators:**, and then select **OK**.

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) on the server where the Intune Connector is being installed.

1. In the **Home** screen, select **Devices** in the left pane.

1. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

1. In the **Windows | Windows devices** screen, select **Windows enrollment**.

1. Under **Windows Autopilot Deployment Program**, select **Intune Connector for Active Directory**.

1. In the **Intune Connector for Active Directory** page, select **Add**.

1. In the **Add connector** window that opens, select **Download the on-premises Intune Connector for Active Directory** under step 2 of **Configuring the Intune connector for Active Directory**. This download should download a file called **ODJConnectorBootstrapper.exe**.

1. Open the **ODJConnectorBootstrapper.exe** file that downloaded to launch the Intune Connector install.

1. In the **Intune Connector for Active Directory Setup** installer window, select **I agree to the license terms and conditions**, and then select **Install**.

    > [!NOTE]
    >
    > If an install location other than the default of **C:\Program Files\Microsoft Intune\ODJConnector** is desired, select **Options** and specify the desired install location.

1. When the install completes, select **Configure Now** in the **Intune Connector for Active Directory Setup** installer window.

    > [!NOTE]
    >
    > If **Close** is accidentally selected or the **Intune Connector for Active Directory Setup** installer window is accidentally closed, the **Intune Connector for Active Directory** configuration can be accessed by selecting **Intune connector for Active Directory** > **Intune connector for Active Directory** from the Start menu.

1. In the **Intune connector for Active Directory** window:

   1. Under the **Enrollment** tab, select **Sign In**.

   1. Under the **Sign In** tab, sign in with the Global administrator or with the credentials of an Intune administrator role. The user account must have an assigned Intune license. The sign in process may take a few minutes to complete.

   1. Once the sign in process is complete, a **The Intune connector for Active Directory successfully enrolled** confirmation window appears. Select **OK** to close the window. The **Enrollment** tab shows **Intune connector for Active Directory is enrolled** and the **Sign In** button is greyed out.

   1. Close the **Intune connector for Active Directory** window.

1. In the Microsoft Intune admin center, close the **Add connector** window if it's still displayed.

1. In the **Intune Connector for Active Directory** page, confirm that the server is displayed under **Connector name** and shows as **Active** under **Status**. If the server isn't displayed, select **Refresh** or navigate away from the page, and then navigate back to the **Intune Connector for Active Directory** page.

> [!NOTE]
>
> - The Global administrator role is a temporary requirement at the time of installation.
> - After you sign in to the Intune connector, it can take several minutes to appear in the **Intune Connector for Active Directory** page of the Microsoft Intune admin center. It appears only if it can successfully communicate with the Intune service.

After the Intune Connector is installed, it will start logging in the **Event Viewer** under the path **Applications and Services Logs** > **Microsoft** > **Intune** > **ODJConnectorService**. Under this path, the **Admin** and **Operational** logs are found.

## Next step: Increase the computer account limit in the Organizational Unit (OU)

> [!div class="nextstepaction"]
> [Step 3: Increase the computer account limit in the Organizational Unit (OU)](hybrid-azure-ad-join-computer-account-limit.md)

## More information

For more information on the Intune connector, see the following article(s):

- [Install the Intune Connector](/mem/autopilot/windows-autopilot-hybrid#install-the-intune-connector)
