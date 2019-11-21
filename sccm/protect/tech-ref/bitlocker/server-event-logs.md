---
title: Server event logs
titleSuffix: Configuration Manager
description: A technical reference for the possible BitLocker (MBAM) server entries in the Windows event log
ms.date: 11/25/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: conceptual
ms.collection: M365-identity-device-management
ms.assetid: c3279b7d-654d-444b-bd17-1262894590c3
author: aczechowski
ms.author: aaroncz
manager: dougeby
---

# Server event logs

*Applies to: Configuration Manager (current branch)*

<!--3601034-->

When you install the BitLocker self-service portal or the administration and monitoring website, use the Windows Event Viewer to view server event logs. Go to **Applications and Services Logs**, **Microsoft**, **Windows**. During initial setup, use [MBAM-Server](#bkmk-server). When the service is running, use [MBAM-Web](#bkmk_web).

For more information on installing these websites, see [Set up BitLocker reports and portals](/configmgr/protect/deploy-use/bitlocker/setup-bitlocker-admin).

## <a name="bkmk_server"></a> Set up logs (MBAM-Server)

The following sections contain messages and troubleshooting information for event IDs that can happen when you configure the BitLocker websites.

### MBAM-Server - Admin

#### 300: CmdletError

Failed in removing folder. A terminating error occurred while running a task. To further diagnose set up, look at other event messages in the log.

#### 301: cmdletUnexpectedError

Unexpected cmdlet error.

#### 302: CmdletWarning

Cmdlet warning.

#### 400: ConfiguratorError

An error occurred while running the MBAM Configurator. Make sure that the user has adequate privileges to launch the MBAM Configurator.

#### 401: ConfiguratorUnexpectedError

A terminating error occurred while running an MBAM Configurator task. The error message will contain more details about the error. To further diagnose set up, look at other event messages in the log.

Known errors:

- Failure to retrieve or validate a Certificate that was selected by the user
- Failure to parse the Reports URL
- Failure to open Event Logs for the user

#### 402: ConfiguratorWarning

An MBAM Configurator task didn't complete as expected, but didn't fail completely. For example:

- You configured a certificate for the web application, but it's missing from the `LocalMachine\My` store
- A pending task timed out

#### 500: WebProviderUnexpectedError

An error occurred while enabling and configuring a web site or web service in IIS.

Known errors:

- Failure to find IIS WWW root folder
- Failure to access IIS configuration in web.config due to malformed files or missing settings
- Failure to create or remove a web application
- IIS access violation
- Failure to access Active Directory to validate user accounts

Possible causes to verify:

- IIS is installed, correctly configured, and the IIS service is running
- Verify all [prerequisites](/configmgr/protect/plan-design/plan-for-bitlocker#prerequisites)
- The user has the correct permissions to create web applications on the IIS instance
- The user has access to read user account objects in Active Directory

#### 501: WebProviderError

Web application provider unexpected error. An error occurred while enabling, disabling, or configuring a web site or web service in IIS.

Known errors:

- Failure to read basic or WSHttp binding information from IIS
- Missing identity section or DNS entry in identity section in IIS config files
- Failure to open registry key `HKLM\SOFTWARE\Microsoft\InetStp`
- Failure to read value `PathWWWRoot` from registry key `HKLM\SOFTWARE\Microsoft\InetStp`
- User is trying to specify a virtual directory name with a BitLocker reserved name

Possible causes to verify:

- IIS is installed and correctly configured
- The registry key `HKLM\SOFTWARE\Microsoft\InetStp:PathWWWRoot` exists and is accessible
- The binding information in IIS isn't corrupt

#### 502: WebProviderWarning

Web application provider warning. A non-terminating error occurred while enabling a web site or web service.

Known errors:

- Failure to access AD to validate the Service Principal Name (SPN) on the app pool account
- Failure to validate SPN because it's assigned to multiple accounts in AD
- Failure to register an SPN on the app pool account in AD
- SPN is registered on an account other than the app pool in AD
- Failure to remove SPN from the app pool account in AD during a rollback operation
- Failure to check if the **IIS_IUSRS** group has the **Logon as batch** privilege on the IIS server

The event message will contain more information about the specific error.

Possible causes to verify:

- AD is reachable from the server where setup is running
- The user running setup has read permissions on the app pool account in AD
- If an SPN is already registered on the app pool account in AD, then make sure that it isn't registered on other accounts

#### 600: SetupUnexpectedError

Unexpected setup error. A terminating error occurred while enabling, disabling, or configuring a feature.

Known errors:

- Failure to rollback a task after an error
- Failure to read from the registry
- Failure to create or delete a folder in the file system
- Failure to read SQL version information
- Failure to register VSS writer in SQL

The event message will contain more information about the specific error.

Possible causes to verify:

- Verify all [prerequisites](/configmgr/protect/plan-design/plan-for-bitlocker#prerequisites)
- Make sure the MBAM registry path `HKLM\SOFTWARE\Microsoft\MBAM Server` exists and you can read all the subkeys
- AD is reachable from the server where setup is running
- The user running setup has read permissions in AD
- For a successful VSS writer registration, verify that a supported version of SQL is installed and an instance is accessible to the user running setup
- If disabling or uninstalling a feature, verify that all files are closed. Setup needs to remove its web sites and web services. These files include log files and web.config files.

#### 601: SetupError

A terminating error occurred while enabling, disabling, or configuring a feature.

Known errors:

- Failure to read MBAM configuration in IIS
- Corrupt `appSettings` section in IIS configuration or misconfigured settings
- Failure to validate host name
- Failure to read SQL version information
- Failure to register VSS writer in SQL

The event message will contain more information about the specific error.

Possible causes to verify:

- IIS is installed and configured correctly
- Verify all [prerequisites](/configmgr/protect/plan-design/plan-for-bitlocker#prerequisites)
- For a successful VSS writer registration, verify that a supported version of SQL is installed and an instance is accessible to the user running setup

#### 602: SetupWarning

A non-terminating error occurred while enabling, disabling, or configuring a feature.

Known errors:

- Failure to delete MBAM reports from Configuration Manager reporting services point
- Failure to resolve a host name from the domain controller

The event message will contain more information about the specific error.

Possible causes to verify:

- AD is reachable from the server where setup is running
- The user running setup has **remove** permissions on the SQL Server Reporting Services instance that you configure as the Configuration Manager reporting services point

#### 605: WebProviderSoftwareCheckFailure

Setup can't enable the web application because one or more software dependencies aren't met. During web site or web service installation, setup verifies if necessary prerequisites are in place. To get more information about missing prerequisites, see the error messages preceding this message in the event log.

For more information, see [prerequisites](/configmgr/protect/plan-design/plan-for-bitlocker#prerequisites).

#### 606: SetupParameterValidationFailure

The parameter that's needed to enable the server feature was either not specified or it didn't pass the validation.

#### 607: SetupParameterValidationFailureWithError

Setup hit an error while trying to validate the specified parameter that's needed to enable the server feature.

#### 700: DbProviderUnexpectedError

DB provider unexpected error.

#### 701: DbProviderError

The message contained in the EventDetails section should provide more information about actual error.

Possible causes to verify:

- Setup failed to connect to the database using the provided connection information. Verify the connection string details in setup.
- Setup couldn't connect to the given database using the supplied domain account credentials. Verify that domain account user name and password are valid. Also verify that it has the necessary permissions to connect to site database.

#### 702: DbProviderWarning

DB provider warning.

<!-- ACzechowski: I don't think these apply in ConfigMgr

#### 704: DbProviderDacError

An error occurred while deploying the Data-Tier Application. MBAM packages its databases as data tier applications and tries to register them using Microsoft.SqlServer.Dac.DacServices. The error message in context is reported by DAC service. The event should contain detailed information about what caused it. Read the information in the error message to troubleshoot and fix the issue.

#### 705: DbProviderDacWarning

A warning occurred while deploying the Data-Tier Application. MBAM packages its databases as data tier application and tries to register them using Microsoft.SqlServer.Dac.DacServices. The warning message in context is reported by DAC service. The event should contain detailed information about what caused it. Read the information in the warning message to troubleshoot and fix the issue.
 -->

#### 800: ReportProviderUnexpectedError

##### File or directory exceptions

- An error occurred while getting the name of directory '{directoryName}'
- An exception occurred while getting files for directory '{directoryName}'
- An exception occurred while enumerating directories in directory '{directoryName}'
- An exception occurred while reading all bytes for file '{fileName}'

During installation, setup unzips all the report files to the specified installation path. As a part of report installation, it tries to access the unzipped report files at that path, and communicates with SQL Reporting Services to publish the report files. The above errors occur when it can't access the files or folders at the unzipped installation path.

Possible causes to verify:

- Registry key `HKLM\SOFTWARE\Microsoft\MBAM Server\InstallationPath` is present and accessible to your account.
- The path to the report files doesn't exceed 248 characters.
- The setup files haven't been modified since installation.
- The user running setup is authorized to read from and write to the installation folder.

##### Reporting Services connectivity failed

During reports installation, setup tries to communicate with SQL Server Reporting Services (SSRS) to create folders and publish reports. This message indicates that setup couldn't find or communicate with SSRS web services.

Possible causes to verify:

- SSRS is installed on the specified machine.
- SSRS is enabled and running.
- The user running setup is authorized to access SSRS.

##### Failed to remove the MBAM Reports using Reporting Services instance URL

When installation fails or when you disable reporting features, setup removes SSRS reports. This message indicates that setup failed to remove the SSRS reports.

Possible causes to verify:

- SSRS is installed on the specified machine.
- SSRS is enabled and running.
- The user running setup is authorized to access SSRS.

##### An error occurred while publishing reports

During reports installation, setup tries to communicate with SSRS web services to create folders and publish reports. This message indicates that the SSRS web service reported an exception while publishing reports.

Possible causes to verify:

- SSRS is enabled and running.
- The user running setup is authorized to access and publish reports to SSRS.

##### An error occurred while validating access to SSRS

As part of the prerequisite check, setup verifies if the user has necessary permissions to access and create folders under SSRS. This error message indicates that an exception has occurred while verifying access to SSRS. Refer to the exception details for troubleshooting tips.

##### A SOAP error occurred while checking the SSRS URL

Make sure SSRS is enabled and running.

##### A web error occurred while checking the SSRS URL

Make sure SSRS is enabled and running.

##### An http/https error occurred while checking the SSRS URL

Make sure SSRS is enabled and running.

##### An error occurred while checking the SSRS URL

As part of the prerequisite check, setup retrieves URLs associated with the supplied SSRS instance. It then tries to communicate with the SSRS web service. This error message indicates that the SSRS web service at the given URL threw an exception. For more information, see the exception details.

Possible causes to verify:

- SSRS is installed on the specified machine.
- SSRS is enabled and running.
- The user running setup is authorized to access SSRS.

##### An error occurred while retrieving the SSRS version

As part of the prerequisite check, setup queries WMI to retrieve the version number associated to the supplied SSRS instance. This error message indicates that an exception occurred while querying WMI. For more information, see the exception details.

Possible causes to verify:

- SSRS with given instance name is installed on the specified machine.
- SSRS is enabled and running.
- The user running setup is authorized to query SSRS class under WMI namespace.

##### The current user is not authorized to access the WMI namespace

Make sure the user running setup is authorized to query SSRS class under WMI namespace.

##### An error occurred while enumerating the namespace '{ssrsWMINamespace}'. RPC server for SSRS WMI provider on the local host is not found

Make sure SSRS is installed on the specified machine.

##### An error occurred while enumerating the namespace '{ssrsNamespace}'. Unable to find an instance of SSRS on the local host

Make sure SSRS is installed on the specified machine.

##### An error occurred while accessing WMI. RPC server for instance '{ssrsInstance}' was not found

Make sure SSRS is installed on the specified machine.

##### An error occurred while accessing WMI. Instance name '{ssrsInstanceName}' is not correct

Make sure SSRS is installed on the specified machine.

##### An error occurred while accessing WMI. Unable to find instance '{ssrsInstanceName}' on the local host

As part of the prerequisite check, setup queries WMI to retrieve the WMI namespace for the given instance. This error message indicates that an exception occurred while querying WMI. For more information, see the exception details.

Possible causes to verify:

- SSRS with given instance name is installed on the specified machine.
- SSRS is enabled and running.
- The user running the setup is authorized to access and query SSRS class under WMI namespace.

#### 801: ReportProviderError

Report provider unexpected error. Given the SQL Server Reporting Services instance name, setup tries to find and connect to the WMI namespace corresponding to the reporting instance. This error occurs if setup hits an exception when it searches for or tries to connect to the SSRS WMI namespace. For more information, look for other errors in the event log before this one.

Possible causes to verify:

- SSRS with the given instance name is enabled running
- The user account running setup has the necessary permissions to query and connect to the SSRS WMI namespace

#### 802: ReportProviderWarning

Report provider warning.

#### 900: CMProviderUnexpectedError

A terminating error occurred while enabling, disabling, or configuring the components in Configuration Manager:

Known errors:

- Failure to connect to the site server via the SMS Provider
- Failure to read from the registry
- Failure to create or delete a folder in the file system
- Failure to locate the Configuration Manager console installation on the local machine
- Failure to retrieve information for the SSRS instance that's configured as the reporting services points

The event message will contain more information about the specific error.

Possible causes to verify:

- Verify all [prerequisites](/configmgr/protect/plan-design/plan-for-bitlocker#prerequisites)
- You can read the registry path `HKLM\SOFTWARE\Microsoft\MBAM Server` and all the subkeys
- Configuration Manager version 1910 or later
- The Configuration Manager console is installed on the machine where you run setup. You can use the console to connect to the target site server.
- You've configured a valid SSRS instance as a reporting services point.
- The user running setup has read and write permissions on the SSRS instance.

#### 901: CMProviderError

A terminating error occurred while enabling, disabling, or configuring Configuration Manager.

Known errors:

- Failure to connect to the site server via the SMS Provider
- Failure to read from the registry
- Failure to create or delete a folder in the file system
- Failure to locate the Configuration Manager console installation on the local machine
- Missing ConfigMgr folder in SSRS as the root folder for the reports on the reporting services point
- Missing ConfigMgr shared data source in SSRS
- Failure to deploy SSRS reports in the SSRS instance that's configured as a reporting service point

The event message will contain more information about the specific error.

Possible causes to verify:

- Verify all [prerequisites](/configmgr/protect/plan-design/plan-for-bitlocker#prerequisites)
- You can read the registry path `HKLM\SOFTWARE\Microsoft\MBAM Server` and all the subkeys
- Configuration Manager version 1910 or later
- The Configuration Manager console is installed on the machine where you run setup. You can use the console to connect to the target site server.
- You've configured a valid SSRS instance as a reporting services point.
- The user running setup has read and write permissions on the SSRS instance.

#### 902: CMProviderWarning

A non-terminating error occurred while configuring Configuration Manager.

Known errors:

The event message will contain more information about the specific error. Some operations that cause this warning are retried. If after several retries the error persists, then an actual error may occur. Inspect other event messages in the log to further diagnose the problem.

### MBAM-Server - Operational

#### 103: VssRegistrationException

An exception was thrown during VSS registration.

#### 104: VssDeregistrationException

An exception was thrown during VSS deregistration.

#### 303: CmdletInformation

Informational only; no troubleshooting required. The event indicates that a task is happening. For example, enabling or disabling a feature, or canceling an operation.

#### 410: ConfiguratorInformation

Informational only; no troubleshooting required. The event indicates that the Configurator is running a task:

- Launching the configurator
- Checking software prerequisites for a feature
- Validating parameters for a feature
- Enabling, disabling, or committing a feature
- Generating a PowerShell script from the configurator

#### 503: WebProviderInformation

Informational only; no troubleshooting required. The event indicates that setup is running a task:

- Getting IIS configuration such as binding information and root site
- Configuring the service principal name (SPN)

#### 603: SetupInformation

Informational only; no troubleshooting required.

#### 703: DbProviderInformation

Informational only; no troubleshooting required.

<!--
#### 706: DbProviderDacInformation

A message was raised while deploying the Data-Tier Application. Informational only; no troubleshooting required.
-->

#### 803: ReportProviderInformation

Informational only; no troubleshooting required.

#### 903: CMProviderInformation

Informational only; no troubleshooting required.

## <a name="bkmk_web"></a> Runtime logs (MBAM-Web)

The following sections contain messages and troubleshooting information for event IDs that can occur while the BitLocker websites are running.

### MBAM-Web - Admin

#### 1: WebAppSpnError

Application: {SiteName}{VirtualDirectory} is missing the following Service Principal Names (SPNs):{ListOfSpns} Register the required SPNs on the account: {ExecutionAccount}.

For integrated Windows Authentication to succeed, necessary SPNs need to be in place. This message indicates that the SPN required for the application isn't correctly configured. Details contained in this event should provide more information.

<!-- See “Service Principal Name (SPN)” in MBAM 2.5 Server Prerequisites for Stand-alone and Configuration Manager Integration Topologies for more information. -->

#### 100: AdminServiceRecoveryDbError

Possible error messages:

- GetMachineUsers: An error occurred while getting user information from the database.
- GetRecoveryKey: an error occurred while getting recovery key from the database.
- GetRecoveryKey: an error occurred while getting user information from the database.
- GetRecoveryKeyIds: an error occurred while getting recovery key Ids from the database.
- GetTpmHashForUser: An error occurred while getting TPM hash data from the recovery database.
- GetTpmHashForUser: An error occurred while getting TPM hash data from the recovery database.
- QueryDriveRecoveryData: An error occurred while getting drive recovery data from the database.
- QueryRecoveryKeyIdsForUser: An error occurred while getting recovery key Ids from the database.
- QueryVolumeUsers: An error occurred while getting user information from the database.

This message is logged whenever there's an exception while communicating with the recovery database. Read through the information contained in the trace to get specific details about the exception.

#### 101: AdminServiceComplianceDbError

Possible error messages:

- GetRecoveryKey: An error occurred while logging an audit event to the compliance database.
- GetRecoveryKeyIds: An error occurred while logging an audit event to the compliance database.
- GetTpmHashForUser: An error occurred while logging an audit event to the compliance database.
- QueryRecoveryKeyIdsForUser: An error occurred while logging an audit event to the compliance database.
- QueryDriveRecoveryData: An error occurred while logging an audit event to the compliance database.

This message is logged whenever there's an exception while communicating with the compliance database. Read through the information contained in the trace to get specific details about the exception.

#### 102: AgentServiceRecoveryDbError

This message indicates an exception when the service tries to communicate with the recovery database. Read through the message contained in the event to get specific information about the exception.

Verify that the MBAM app pool account has required permissions to connect to the recovery database.

#### 103: AgentServiceError

Possible error messages:

- Unable to detect client machine account or data migration user account.

    Whenever a call is made to the `PostKeyRecoveryInfo`, `IsRecoveryKeyResetRequired`, `CommitRecoveryKeyRest`, or `GetTpmHash` web methods, it retrieves the caller context to obtain caller credentials. If the caller context is null or empty, the service logs this message.

- Account verification failed for caller identity.

    This message is logged if the web method is expecting the caller to be a computer account and it's not. It can also be caused if the web method is expecting the caller to be a user account, and it's not a user account or a member of a data migration group account.

#### 104: StatusServiceComplianceDbConfigError

The compliance database connection string in the registry is empty.

This message is logged whenever the compliance db connection string is invalid. Verify the value at the registry key `HKLM\Software\Microsoft\MBAM Server\Web\ComplianceDBConnectionString`.

#### 105: StatusServiceComplianceDbError

This error indicates that the websites or web services were unable to connect to the compliance database. Verify that the IIS app pool account can connect to the database.

#### 106: HelpdeskError

Known errors and possible causes:

- The request to URL caused an internal error.

    An unhandled exception was raised in the application for the administration and monitoring website (helpdesk). Review the log entries in the **Admin** event log to find the specific exception.

- An error occurred while obtaining execution context information. Unable to verify Service Principal Name (SPN) registration.

    During the initial helpdesk website load operation, it checks the SPN. To verify the SPN, it requires account information, IIS Sitename, and ApplicationVirtualPath corresponding to the helpdesk website. It logs this error message when one or more of these attributes are invalid or missing.

- An error occurred while verifying Service Principal Name (SPN) registration.

    This message indicates that a security exception is thrown when verifying the SPN. Refer to the exception contained in the event details.

#### 107: SelfServicePortalError

Known errors and possible causes:

- An error occurred while getting recovery key for a user

    Indicates that an unexpected exception was thrown when a request was made to retrieve a recovery key. Refer to the exception message in the event details. If tracing is enabled on the helpdesk app, refer to trace data to obtain detailed exception messages.

- An error occurred while obtaining execution context information. Unable to verify Service Principal Name (SPN) registration

    During an initial load operation, the self-service portal retrieves account information, IIS Sitename, and ApplicationVirtualPath for the self-service website to verify the SPN. This error message is logged when one or more of these attributes are invalid.

- An error occurred while verifying Service Principal Name (SPN) registration. EventDetails:{ExceptionMessage}

    This message indicates that a security exception was thrown while verifying the SPN. Refer to the exception contained in the event details.

#### 108: DomainControllerError

Known errors and possible causes:

- An error occurred while resolving domain name {DomainName}, a memory allocation failure occurred.

    To resolve domain name, it calls the `DsGetDcName` Windows API. This message is logged when this API returns `ERROR_NOT_ENOUGH_MEMORY`, which indicates a memory allocation failure.

- Could not invoke DsGetDcName method

    This message indicates that the `DsGetDcName` API is unavailable on the host.

#### 109: WebAppRecoveryDbError

Known errors and possible causes:

- An error occurred while reading the configuration of the Recovery database. The connection string to the Recovery database is not configured.

    This message indicates that recovery database connection string information at `HKLM\Software\Microsoft\MBAM Server\Web\RecoveryDBConnectionString` is invalid. Verify the given registry key value.

If you see any of the following messages, verify whether  the app pool credentials from the IIS server can make a connection to the recovery database:

- DoesUserHaveMatchingRecoveryKey: an error occurred while getting recovery key Ids for a user.
- QueryDriveRecoveryData: an error occurred while getting drive recovery data.
- QueryRecoveryKeyIdsForUser: an error occurred while getting recovery key Ids for a user.
- An error occurred while getting TPM password hash from the Recovery database.

#### 110: WebAppComplianceDbError

Known errors and possible causes:

- An error occurred while reading the configuration of the Compliance database. The connection string to the Compliance database is not configured.

    This message indicates that compliance database connection string information at `HKLM\Software\Microsoft\MBAM Server\Web\ComplianceDBConnectionString` is invalid. Verify the value of this registry key.

If you see any of the following messages, verify whether the app pool credentials from the IIS server can make a connection to the compliance database:

- GetRecoveryKeyForCurrentUser: an error occurred while logging an audit event to the Compliance database.
- QueryRecoveryKeyIdsForUser: an error occurred while logging an audit event to the Compliance database.
- QueryRecoveryKeyIdsForUser: an error occurred while logging an audit event to the compliance database.

#### 111: WebAppDbError

These errors indicate one of the following two conditions

- MBAM websites/webservices were unable to either connect to compliance or recovery database
- MBAM websites/webservices execution account (app pool account) could not run the `GetVersion` stored procedure on compliance or recovery database

The message contained in the event provides more details about the exception.

Verify that the app pool account can connect to the compliance or recovery databases. Confirm that it has permissions to run the `GetVersion` stored procedure.

#### 112: WebAppError

An error occurred while verifying Service Principal Name (SPN) registration.

To verify the SPN, it queries Active Directory to retrieve a list of SPNs mapped execution account. It also queries the `ApplicationHost.config` to get the website bindings. This error message indicates that it couldn't communicate with Active Directory, or it couldn't load the `ApplicationHost.config` file.

Verify that the app pool account has permissions to query Active Directory or the `ApplicationHost.config` file. Also verify the site binding entries in the `ApplicationHost.config` file.

### MBAM-Web - Operational

#### 4: PerformanceCounterError

An error occurred while retrieving a performance counter.

The trace message contains the actual exception message, some of which are listed here:

- ArgumentNullException: This exception is thrown if the category, counter, or instance of requested Performance counter is invalid.
- System.InvalidOperationException: categoryName is an empty string (""). counterName is an empty string("").
- The read/write permission setting requested is invalid for this counter.
- The category specified does not exist (if readOnly is true).
- The category specified is not a .NET Framework custom category (if readOnly is false).
- The category specified is marked as multi-instance and requires the performance counter to be created with an instance name.
- instanceName is longer than 127 characters.
- categoryName and counterName have been localized into different languages.
- System.ComponentModel.Win32Exception: An error occurred when accessing a system API.
- System.UnauthorizedAccessException: Code that is executing without administrative privileges attempted to read a performance counter.

The message in the event provides more details on the exception.

For the `System.UnauthorizedAccessException`, verify that the app pool account has access to performance counter APIs.

#### 200: HelpDeskInformation

The administration website application successfully found and connected to a supported version of the recovery/compliance database.

Indicates successful connection to the recovery or compliance database from the helpdesk website.

#### 201: SelfServicePortalInformation

The self-service portal application successfully found and connected to a supported version of the recovery/compliance database.

Indicates successful connection to the recovery or compliance database from the self-service portal.

#### 202: WebAppInformation

Application has its SPNs registered correctly.

Indicates that the SPNs required for the helpdesk website are correctly registered against the executing account.
