---
title: Windows Autopilot user-driven hybrid Azure AD join - Step 2 of 8 - Install the Intune Connector
description: How to - Windows Autopilot user-driven hybrid Azure AD join - Step 2 of 8 - Install the Intune Connector(ESP).
ms.prod: windows-client
ms.localizationpriority: medium
author: frankroj
ms.author: frankroj
ms.reviewer: jubaptis
manager: aaroncz
ms.date: 02/13/2023
ms.topic: tutorial
ms.collection: 
  - tier1
  - highpri
ms.technology: itpro-deploy
---

# User-driven hybrid Azure AD join: Install the Intune Connector

Autopilot user-driven hybrid Azure AD join steps:
- Step 1: [Set up Windows automatic Intune enrollment](hybrid-azure-ad-join-automatic-enrollment.md)
> [!div class="checklist"]
> - **Step 2: Install the Intune Connector**
- Step 3: [Increase the computer account limit in the Organizational Unit (OU)](hybrid-azure-ad-join-computer-account-limit.md)
- Step 4: [Register devices as Autopilot devices](hybrid-azure-ad-join-register-device.md)
- Step 5: [Create a device group](hybrid-azure-ad-join-device-group.md)
- Step 6: [Configure and assign Autopilot Enrollment Status Page (ESP)](hybrid-azure-ad-join-esp.md)
- Step 7: [Create and assign hybrid Azure AD join Autopilot profile](hybrid-azure-ad-join-autopilot-profile.md)
- Step 8: [Configure and assign domain join profile](hybrid-azure-ad-join-domain-join-profile.md)

For an overview of the Windows Autopilot hybrid user-driven Azure AD join workflow, see [Windows Autopilot user-driven hybrid Azure AD join overview](hybrid-azure-ad-join-workflow.md)

## Install the Intune Connector

1. Sign into the server where the Intune Connector will be installed with an account that has local administrator rights.

2. Turn off Internet Explorer Enhanced Security Configuration on the server. By default Windows Server has Internet Explorer Enhanced Security Configuration turned on. To turn off Internet Explorer Enhanced Security Configuration:

   1. On the server where the Intune Connector will be installed, open **Server Manager**.
   2. In the left pane of Server Manager, select **Local Server**.
   3. In the right **PROPERTIES** pane of Server Manager, select the **On** or **Off** link next to **IE Enhanced Security Configuration**.
   4. In the **Internet Explorer Enhanced Security Configuration** window, select **Off** under **Administrators:**, and then select **OK**.

3. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431) on the server where the Intune Connector will be installed.

4. In the **Home** screen, select **Devices**.

5. In the **Devices | Overview** screen, under **By platform**, select **Windows**.

6. In the **Windows | Windows devices** screen, select > **Windows enrollment**.

7. Under **Windows Autopilot Deployment Program**, select **Intune Connector for Active Directory**.

8. In the **Intune Connector for Active Directory** page, select **Add**.

9. In the **Add connector** page, select **Download the on-premises Intune Connector for Active Directory** under step 2 of **Configuring the Intune connector for Active Directory**.

10. Open the **ODJConnectorBootstrapper.exe** file that downloaded to launch the Intune Connector install.

11. In the **Intune Connector for Active Directory Setup** installer window, select **I agree to the license terms and conditions**, and then select **Install**.

    > [!NOTE]
    >
    > If an install location other than the default of **C:\Program Files\Microsoft Intune\ODJConnector** is desired, select **Options** and specify the desired install location.

12. When the install completes, select **Configure Now** in the **Intune Connector for Active Directory Setup** installer window.

    > [!NOTE]
    >
    > If **Close** is accidentally selected or the **Intune Connector for Active Directory Setup** installer window is accidentally closed, the **Intune Connector for Active Directory** configuration can be accessed by selecting **Intune connector for Active Directory** > **Intune connector for Active Directory** from the Start menu.

13. In the **Intune connector for Active Directory** window, under the **Enrollment** tab, select **Sign In**.

14. Under the **Sign In** tab, sign in with the Global administrator or with the credentials of an Intune administrator role. The user account must have an assigned Intune license. The sign in process may take a few minutes to complete.

15. Once the sign in process is complete, a window will appear saying **The Intune connector for Active Directory successfully enrolled**. Select **OK** to close the window. The **Enrollment** tab will now show **Intune connector for Active Directory is enrolled** and the **Sign In** button will be greyed out.

16. Close the **Intune connector for Active Directory** window.

17. In the Microsoft Intune admin center, close the **Add connector** pane if it is still displayed. In the **Intune Connector for Active Directory** page, confirm that the server is displayed under **Connector name** and shows as **Active** under **Status**. If the server is not displayed, select **Refresh** or navigate away from the page and then navigate back to the **Intune Connector for Active Directory** page.

> [!NOTE]
>
> - The Global administrator role is a temporary requirement at the time of installation.
> - After you sign in to the Intune connector, it can take several minutes to appear in the **Intune Connector for Active Directory** page of the Microsoft Intune admin center. It appears only if it can successfully communicate with the Intune service.

After installing the Intune Connector, it will start logging in the **Event Viewer** under the path **Applications and Services Logs** > **Microsoft** > **Intune** > **ODJConnectorService**. Under this path you will find **Admin** and **Operational** logs.

## Next step: Increase the computer account limit in the Organizational Unit (OU)

> [!div class="nextstepaction"]
> [Step 3: Increase the computer account limit in the Organizational Unit (OU)](hybrid-azure-ad-join-computer-account-limit.md)

## More information

For more information on the Intune connector, see the following article(s):

- [Install the Intune Connector](/mem/autopilot/windows-autopilot-hybrid#install-the-intune-connector)
