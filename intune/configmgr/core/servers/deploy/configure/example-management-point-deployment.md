---
title: Example management point deployment in an untrusted domain
description: Follow a step-by-step example to learn how to install a Configuration Manager management point on a server in an untrusted Active Directory domain.
ms.date: 05/13/2026
ms.subservice: core-infra
ms.topic: install-set-up-deploy
ms.collection: tier3
---

# Step-by-step example deployment of a management point in an untrusted Active Directory domain

*Applies to: Configuration Manager (current branch)*

This example shows how to install a Configuration Manager management point (MP) on a server in an Active Directory domain that doesn't have a two-way trust with the domain that contains the site server. This scenario is common when you need to extend management to a perimeter network (DMZ), a partner domain, or another network segment that you don't fully trust.

Review your organization's network and Active Directory documentation for procedures and best practices that apply to your environment. Use the steps in this article as a proof-of-concept reference. For production guidance, see [Communications across Active Directory forests](../../../plan-design/hierarchy/communications-between-endpoints.md#Plan_Com_X-Forest).

> [!NOTE]
> This scenario applies to a site system connected to a primary site only. Secondary sites require a two-way domain trust between the secondary site's domain and the parent primary site's domain. Installing a secondary site in a domain without the required trust is not supported.

## <a name="BKMK_mp_testenvironment"></a> Test environment

The step-by-step instructions in this article use the following test environment:

- **Trusted domain** (`corp.contoso.com`): Contains the Configuration Manager primary site server (`SiteServer`) and the SQL Server site database (`SQLServer`). The site code is **P01**.

- **Untrusted domain** (`branch.fabrikam.com`): Contains the server that hosts the management point (`DMZ-MP`). No Active Directory trust exists between the two domains.

- Both domains use Windows Server DNS, and DNS conditional forwarders are configured in both directions so that each domain can resolve FQDNs in the other domain.

- You can sign in as a domain administrator in both domains to perform all procedures.

## <a name="BKMK_mp_overview"></a> Overview of the deployment steps

The following table summarizes this deployment and explains why each step is required.

| Step | What you do | Why it's required |
|------|-------------|-------------------|
| [Step 1](#BKMK_mp_step1) | Create service accounts in the untrusted domain | The site system installation account and the MP database connection account must exist in the domain where the MP server resides, or as global accounts resolvable from both domains. |
| [Step 2](#BKMK_mp_step2) | Grant SQL Server database permissions | The MP database connection account must have the permissions to read data in the site database so the management point can query client policy and inventory data. |
| [Step 3](#BKMK_mp_step3) | Configure firewall rules | Normally, all network traffic between the MP and the site server and site database must be explicitly permitted through firewalls. |
| [Step 4](#BKMK_mp_step4) | Install management point prerequisites on the site system server | Ensures that `DMZ-MP` has the Windows features and SQL connectivity components required before Configuration Manager installs the role. |
| [Step 5](#BKMK_mp_step5) | Install the management point role on `DMZ-MP` | Creates the site system server object and installs the management point role by using the accounts and settings prepared in earlier steps. |
| [Step 6](#BKMK_mp_step6) | Verify the management point installation | Confirms that the management point is healthy and that clients in the untrusted forest can communicate with it. |

## <a name="BKMK_mp_step1"></a> Step 1: Create domain accounts

Use two dedicated user accounts. Configure both accounts with non-expiring passwords, and don't grant unnecessary privileges.

| Account | Domain | Purpose | Required permissions |
|---------|--------|---------|----------------------|
| `branch.fabrikam.com\svc-cm-dmzmpinstall` | Untrusted (`branch.fabrikam.com`) | **Site system installation account** — the site server uses this account to connect to `DMZ-MP` and install the management point role. | Member of the local **Administrators** group on `DMZ-MP`. |
| `corp.contoso.com\svc-cm-dmzmpdbconnect` | Trusted (`corp.contoso.com`) | **Management point connection account** — the management point uses this account to read and write data to the site database. | SQL Server login on `SQLServer` instance with the `smsdbrole_MP` and `smsdbrole_MPUserSvc` roles assigned in the SQL database of the site (granted in Step 2). |

### To create the site system installation account in the untrusted domain

1. Sign in to a domain controller in `branch.fabrikam.com` using a domain administrator account.

2. Open **Active Directory Users and Computers**.

3. In the navigation pane, expand **branch.fabrikam.com**, right-click the **Service Accounts** organizational unit (OU), and then choose **New** > **User**.

   > [!TIP]
   > If a dedicated Service Accounts OU doesn't exist, create one first or place the accounts in a suitable OU. Don't place service accounts in the default **Users** container in a production environment.

4. Complete the **New Object – User** wizard with the following settings, and then choose **Finish**:

   - **First name**: `svc-cm-dmzmpinstall`
   - **User logon name**: `svc-cm-dmzmpinstall`
   - **Password**: Use a strong, non-expiring password.
   - Select **Password never expires** and clear **User must change password at next logon**.

5. Close **Active Directory Users and Computers**.

### To create the MP database connection account in the trusted domain

1. Sign in to a domain controller in `corp.contoso.com` using a domain administrator account.

2. Open **Active Directory Users and Computers**.

3. In the navigation pane, expand **corp.contoso.com**, right-click the **Service Accounts** organizational unit (OU), and then choose **New** > **User**.

4. Complete the **New Object – User** wizard with the following settings, and then choose **Finish**:

   - **First name**: `svc-cm-dmzmpdbconnect`
   - **User logon name**: `svc-cm-dmzmpdbconnect`
   - **Password**: Use a strong, non-expiring password.
   - Select **Password never expires** and clear **User must change password at next logon**.

5. Close **Active Directory Users and Computers**.

### To add the installation account to the local Administrators group on management point server

1. Sign in to `DMZ-MP` using a local or domain administrator account.

2. Open **Computer Management**, expand **Local Users and Groups**, and then choose **Groups**.

3. Right-click **Administrators**, and then choose **Add to Group**.

4. In the **Administrators Properties** dialog box, choose **Add**.

5. In the **Select Users, Computers, Service Accounts or Groups** dialog box, enter `FABRIKAM\svc-cm-dmzmpinstall` in the object name box, choose **Check Names** to validate, and then choose **OK**.

6. Choose **OK** to close **Administrators Properties**.

## <a name="BKMK_mp_step2"></a> Step 2: Grant SQL Server database permissions for the MP connection account

The management point must be able to read and write data in the site database. Grant this access by adding the `svc-cm-dmzmpdbconnect` account as a SQL Server login and assigning the required database roles.

> [!IMPORTANT]
> The MP database connection account must reside in the **trusted domain** (`corp.contoso.com`) because it connects to SQL Server (`SQLServer`) in that domain. Specify the account as a Windows login using the NetBIOS domain name `CORP\svc-cm-dmzmpdbconnect`. If name resolution fails, use the FQDN format `corp.contoso.com\svc-cm-dmzmpdbconnect`. For more information, see [Management point connection account](../../../plan-design/hierarchy/accounts.md#management-point-connection-account).

### To create the SQL Server login and assign database roles

1. Sign in to `SQLServer` using a SQL Server administrator account, and open **SQL Server Management Studio**.

2. In **Object Explorer**, expand **Security**, right-click **Logins**, and then choose **New Login**.

3. In the **Login – New** dialog box, on the **General** page, complete the following settings:

   - **Login name**: Enter `CORP\svc-cm-dmzmpdbconnect`.
   - Select **Windows authentication**.

4. In the left pane of the **Login – New** dialog box, choose **User Mapping**.

5. In the **Users mapped to this login** list, select the check box next to the Configuration Manager site database (for example, **CM_P01**).

6. In the **Database role membership** section at the bottom of the page, select the following roles:

   - **smsdbrole_MP**
   - **smsdbrole_MPUserSvc**

7. Choose **OK** to create the login.

8. Close **SQL Server Management Studio**.

## <a name="BKMK_mp_step3"></a> Step 3: Configure firewall rules

The following table lists the minimum firewall rules required for this deployment. Configure these rules on all network firewalls and host-based Windows Firewall profiles between `corp.contoso.com` and `branch.fabrikam.com`.

| Source | Direction | Destination | Protocol | Port | Purpose |
|--------|-----------|-------------|----------|------|---------|
| `SiteServer` (site server) | → | `DMZ-MP` (management point) | TCP | 135 | RPC endpoint mapper |
| `SiteServer` (site server) | → | `DMZ-MP` (management point) | TCP | 49152–65535 | RPC dynamic ports |
| `SiteServer` (site server) | ↔ | `DMZ-MP` (management point) | TCP | 445 | SMB (file transfer) |
| `DMZ-MP` (management point) | → | `SQLServer` (site database) | TCP | 1433 | SQL Server (MP database connection) |

> [!TIP]
> If your SQL Server uses a named instance or a non-default port, update the SQL Server row in the table accordingly. For more information about all ports that Configuration Manager uses, see [Ports used in Configuration Manager](../../../plan-design/network/configure-firewalls-ports-domains.md).

The following connections are required so the management point can authenticate to domain controllers in the CORP forest, and vice versa. DNS ports aren't included.

| Source | Direction | Destination | Protocol | Port | Purpose |
|--------|-----------|-------------|----------|------|---------|
| `SiteServer` (site server) | → | `DC.branch.fabrikam.com` (BRANCH Domain Controller) | UDP | 389 | CLDAP |
| `SiteServer` (site server) | → | `DC.branch.fabrikam.com` (BRANCH Domain Controller) | TCP | 88 | Kerberos authentication |
| `DMZ-MP` (management point) | → | `DC.corp.contoso.com` (CORP Domain Controller) | UDP | 389 | CLDAP |
| `DMZ-MP` (management point) | → | `DC.corp.contoso.com` (CORP Domain Controller) | TCP | 88 | Kerberos authentication |

> [!TIP]
> Both the site server and the management point must be able to locate a Kerberos Key Distribution Center (KDC) in the other domain. To do this, each server must be able to resolve DNS SRV records such as `_kerberos._tcp.dc._msdcs.corp.contoso.com` and `_kerberos._tcp.dc._msdcs.branch.fabrikam.com`.

## <a name="BKMK_mp_step4"></a> Step 4: Install prerequisites on management point server

Before you add the management point role, install the required Windows features and supporting components on `DMZ-MP`. For the complete and current list, see [Site and site system prerequisites](../../../plan-design/configs/site-and-site-system-prerequisites.md#management-point).

For this example, prepare `DMZ-MP` with these Windows roles and features:

- **Web Server (IIS)** role and auto-selected features.
- **.NET Framework 3.5** feature.
- **.NET Framework 4.8** feature. Windows Server 2022 and later include this version by default.
- **IIS Server Extension** (in **Background Intelligent Transfer Service (BITS)**). Select the feature and all automatically selected options.
- **Web Server (IIS)** role services: **Windows Authentication**, **ISAPI Extensions**, **IIS 6 Metabase Compatibility**, and **IIS 6 WMI Compatibility**

### To install the required Windows features

1. Sign in to `DMZ-MP` using a local or domain administrator account.

2. Open an elevated Windows PowerShell session.

3. Run the following command:

   ```powershell
   Install-WindowsFeature NET-Framework-Features, NET-Framework-Core, BITS, BITS-IIS-Ext, Web-Server, Web-WebServer, Web-Common-Http, Web-Default-Doc, Web-Dir-Browsing, Web-Http-Errors, Web-Static-Content, Web-Health, Web-Http-Logging, Web-Log-Libraries, Web-Request-Monitor, Web-Http-Tracing, Web-Performance, Web-Stat-Compression, Web-Security, Web-Filtering, Web-Windows-Auth, Web-App-Dev, Web-ISAPI-Ext, Web-Http-Redirect, Web-Mgmt-Tools, Web-Mgmt-Console, Web-Mgmt-Compat, Web-Metabase, Web-WMI -IncludeManagementTools
   ```

> [!NOTE]
> The .NET Framework 3.5 feature payload is removed from the base OS image on modern Windows Server versions.
>
> For offline environments, you can install .NET Framework 3.5 by using either method:
>
> - **PowerShell**: Mount Windows Server installation media and run `Install-WindowsFeature Net-Framework-Core -Source D:\sources\sxs` (replace `D:` with your media drive).
> - **Add Roles and Features Wizard**: In **Server Manager** > **Add Roles and Features**, select **.NET Framework 3.5 Features**. On **Confirm installation selections**, choose **Specify an alternate source path** and enter `D:\sources\sxs`.
>
> Use installation media that matches the same Windows Server version as `DMZ-MP`. For more information, see [Enable .NET Framework 3.5 by using the Add Roles and Features Wizard](/windows-hardware/manufacture/desktop/enable-net-framework-35-by-using-the-add-roles-and-features-wizard) and [Enable .NET Framework 3.5 by using PowerShell](/windows-hardware/manufacture/desktop/enable-net-framework-35-by-using-windows-powershell).

4. Restart `DMZ-MP` if Windows prompts for a restart.

## <a name="BKMK_mp_step5"></a> Step 5: Install the management point role

This procedure installs the management point role on `DMZ-MP` by using the **Create Site System Server** wizard. The wizard lets you specify the cross-forest accounts and settings required by the role.

1. In the Configuration Manager console, go to the **Administration** workspace. Expand **Site Configuration**, and then choose **Servers and Site System Roles**.

2. On the **Home** tab, in the **Create** group, choose **Create Site System Server**.

3. On the **General** page, complete the following settings, and then choose **Next**:

   - **Name**: Enter the FQDN of the management point server: `DMZ-MP.branch.fabrikam.com`.
   - **Site code**: Select **P01** (or the appropriate site code for your environment).
   - **Site system installation account**: Choose **Specify an account**, and then enter `FABRIKAM\svc-cm-dmzmpinstall`.

     > [!IMPORTANT]
     > You must specify a **Site System Installation Account** when the target server is in an untrusted forest. The site server can't use its own computer account to authenticate to a server in a forest without trust. For more information, see [Site system installation account](../../../plan-design/hierarchy/accounts.md#site-system-installation-account).

4. On the **General** page, select **Require the site server to initiate connections to this site system**.

   > [!IMPORTANT]
   > `DMZ-MP` lacks permissions to connect back to the site server. With this option selected, all data transfers are initiated by the site server and use the same [Site system installation account](../../../plan-design/hierarchy/accounts.md#site-system-installation-account).

5. On the **Proxy** page, configure a proxy server if `DMZ-MP` requires one to reach internet endpoints. Otherwise, choose **Next**.

6. On the **System Role Selection** page, select **Management point**, and then choose **Next**.

7. On the **Management Point** page, complete the following settings, and then choose **Next**:

   - **Client connections**: Choose **HTTPS** to require encrypted client communication (requires a PKI web server certificate bound to the IIS Default Web Site on `DMZ-MP`) or **EHTTP**.
   - **Generate alert when the management point is not healthy**: Optionally select this to receive in-console alerts when the management point is unhealthy.
   - Leave other options at their default settings.

8. On the **Management Point Database Connection** page, complete the following settings, and then choose **Next**:

   - **Use the site database**: This is the default configuration. You don't need to specify the SQL Server instance because the site already has this information.
   - **Management point database connection**: Choose **Specify an account**, and then enter `corp.contoso.com\svc-cm-dmzmpdbconnect`. Use the FQDN format to ensure that the management point can resolve the account in the trusted domain and authenticate to SQL Server successfully.
     > [!IMPORTANT]
     > You must specify the **Management point connection account** when the management point is in an untrusted domain or forest because it authenticates directly to SQL Server in the trusted domain. Specifying the account in the format `DomainFQDN\UserName` (for example, `corp.contoso.com\svc-cm-dmzmpdbconnect`) helps with name resolution during Kerberos authentication. For more information, see [Management point connection account](../../../plan-design/hierarchy/accounts.md#management-point-connection-account).

9. Review the summary on the **Summary** page, and then choose **Next** to complete the wizard.

10. Choose **Close** on the **Completion** page.

   > [!NOTE]
   > After you close the wizard, Configuration Manager creates the site system server object and begins the background installation of the management point role on `DMZ-MP`. The installation can take several minutes to complete. Monitor the progress as described in Step 6.

## <a name="BKMK_mp_step6"></a> Step 6: Verify the management point installation

After the wizard finishes, verify that the management point installed successfully and is healthy before directing clients to it.

### To verify the management point status in the Configuration Manager console

1. In the Configuration Manager console, go to the **Monitoring** workspace. Expand **System Status**, and then choose **Component Status**.

2. Locate the **SMS_MP_CONTROL_MANAGER** component on `DMZ-MP.branch.fabrikam.com`. In the **Status** column, confirm that the status is **OK**.

   > [!NOTE]
   > It can take up to 30 minutes after the wizard closes for the management point to appear healthy. If the status is **Warning** or **Critical**, right-click the component, choose **Show Messages** > **All**, and review the failure details. Then review the log files described below.

3. Repeat the check for the **SMS_MP_FILE_DISPATCH_MANAGER** component.

### To verify the management point installation by reviewing log files

1. Sign in to `DMZ-MP`, and locate the `SMS` folder at the root of one of the drives.

2. If the folder doesn't exist, review `SiteComp.log` on the site server to confirm that the site server connected to `DMZ-MP` and started the installation by using the [Site system installation account](../../../plan-design/hierarchy/accounts.md#site-system-installation-account). If the `SMS` folder is missing, the site server likely can't communicate with `DMZ-MP` or doesn't have permissions to create the folder and install the role.

3. Review the following log files on `DMZ-MP` for messages related to management point installation and configuration:

   | Log file | Location on `DMZ-MP` | What to look for |
   |----------|------------------|-----------------|
   | `MPSetup.log` | `\SMS\Logs` | High-level prerequisite and MP installation messages: in particular, `CcmSetup`, `msoledbsql.msi`, IIS-ASPNET45 feature and `mp.msi`. |
   | `MPMSI.log` | `\SMS\Logs` | Details about MP installation and MSI rollback state. If installation fails with error `1603`, search this file for the detailed error message. |
   | `CCMSetup.log` | `%Windir%\CCMSetup\Logs` | Client binary installation messages and related prerequisites (for example, vcredist and Microsoft Policy Platform). Installation should complete with return code `0`. |
   | `BGBSetup.log` | `\SMS\Logs` | Client Notification Server installation messages: look for successful completion. |

4. After the MP is installed, the `SMS_CCM` folder should appear on the same drive as `SMS`. This folder might not appear if the client was installed before the management point. In that case, review the `CCM\Logs` folder for the installed client. Then review the following log files on `DMZ-MP` for messages related to management point communication with the site server and site database:

   | Log file | Location on `DMZ-MP` | What to look for |
   |----------|------------------|-----------------|
   | `MpControl.log` | `\SMS\Logs` | Regular Management Point and User Service availability checks. The successful check resembles `Call to HttpSendRequestSync succeeded for port 443 with status code 200, text: OK`. |
   | `BGBServer.log` | `\SMS\Logs` | Client Notification (fast channel) server reporting. Typical entries include the number of connected clients, such as `Total online clients: 100 (TCP: 99 HTTP: 1)~~`. |
   | `MPFDM.log` | `\SMS\Logs` | On `DMZ-MP`, this log should show minimal activity and include `Remote site is in pull-mode.`. On the site server, the same log should show file-move activity, with entries similar to `~Moved file...`. |
   | `MP_Framework.log` | `\SMS_CCM\Logs` | Database connection messages that use the [Management point connection account](../../../plan-design/hierarchy/accounts.md#management-point-connection-account), such as `Loaded MP settings cache from reg key HKLM\Software\Microsoft\SMS\MP: Database Settings:`. If errors occur, look for failed authentication or SQL Server connectivity issues. |

### To test client communication with the new management point

1. On a client computer in `branch.fabrikam.com`, copy the client installation files to a local folder. Open an elevated Command Prompt in that folder, and run the following command to manually assign the client to the new management point:

   ```cmd
   ccmsetup.exe SMSSITECODE=P01 SMSMP=DMZ-MP.branch.fabrikam.com
   ```

   > [!NOTE]
   > If the MP is configured for HTTPS, make sure the client has an enrolled PKI client certificate and include the `/UsePKICert` switch with `ccmsetup.exe`. For more information, see [About client installation properties](../../../clients/deploy/about-client-installation-properties.md).

2. Review `%Windir%\CCMSetup\Logs\CCMSetup.log` to confirm the successful installation.

3. Review `\SMS_CCM\Logs\ClientIDManagerStartup.log` to confirm successful client registration. Look for messages similar to `[RegTask] - Client is registered. Server assigned ClientID is GUID:0B1F5036-9CE1-41A1-B417-063582728464. Approval status 1`.

4. Verify that the client appears in the Configuration Manager console and shows an **Online** icon. Add the **Management Point** column to the console view to confirm that the client is assigned to `DMZ-MP.branch.fabrikam.com`.

## More information

- [Add site system roles](add-site-system-roles.md)
- [Install site system roles](install-site-system-roles.md)
- [Site and site system prerequisites for Configuration Manager](../../../plan-design/configs/site-and-site-system-prerequisites.md)
- [Communications across Active Directory forests](../../../plan-design/hierarchy/communications-between-endpoints.md#Plan_Com_X-Forest)
- [Accounts used in Configuration Manager](../../../plan-design/hierarchy/accounts.md)
- [PKI certificate requirements for Configuration Manager](../../../plan-design/network/pki-certificate-requirements.md)
