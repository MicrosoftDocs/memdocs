---
title: Server event logs
titleSuffix: Configuration Manager
description: A technical reference for the possible BitLocker (MBAM) server entries in the Windows event log
ms.date: 11/29/2019
ms.prod: configuration-manager
ms.technology: configmgr-protect
ms.topic: reference
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.localizationpriority: medium
---

# Server event logs

*Applies to: Configuration Manager (current branch)*

<!--3601034-->

Use the Windows Event Viewer to view event logs for the following BitLocker management server components in Configuration Manager:

- Recovery service on the management point
- Self-service portal
- Administration and monitoring website

On a server hosting one or more of these components, open the Event Viewer. Then go to **Applications and Services Logs**, **Microsoft**, **Windows**, and expand **MBAM-Web**. By default, there are [Admin](#admin) and [Operational](#operational) event logs.

The following sections contain messages and troubleshooting information for event IDs that can occur with the BitLocker management server components.

## Admin

### 1: WebAppSpnError

Application: {SiteName}{VirtualDirectory} is missing the following Service Principal Names (SPNs):{ListOfSpns} Register the required SPNs on the account: {ExecutionAccount}.

For integrated Windows Authentication to succeed, necessary SPNs need to be in place. This message indicates that the SPN required for the application isn't correctly configured. Details contained in this event should provide more information.

<!-- See "Service Principal Name (SPN)" in MBAM 2.5 Server Prerequisites for Stand-alone and Configuration Manager Integration Topologies for more information. -->

### 100: AdminServiceRecoveryDbError

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

### 101: AdminServiceComplianceDbError

Possible error messages:

- GetRecoveryKey: An error occurred while logging an audit event to the compliance database.
- GetRecoveryKeyIds: An error occurred while logging an audit event to the compliance database.
- GetTpmHashForUser: An error occurred while logging an audit event to the compliance database.
- QueryRecoveryKeyIdsForUser: An error occurred while logging an audit event to the compliance database.
- QueryDriveRecoveryData: An error occurred while logging an audit event to the compliance database.

This message is logged whenever there's an exception while communicating with the compliance database. Read through the information contained in the trace to get specific details about the exception.

### 102: AgentServiceRecoveryDbError

This message indicates an exception when the service tries to communicate with the recovery database. Read through the message contained in the event to get specific information about the exception.

Verify that the MBAM app pool account has required permissions to connect to the recovery database.

### 103: AgentServiceError

Possible error messages:

- Unable to detect client machine account or data migration user account.

    Whenever a call is made to the `PostKeyRecoveryInfo`, `IsRecoveryKeyResetRequired`, `CommitRecoveryKeyRest`, or `GetTpmHash` web methods, it retrieves the caller context to obtain caller credentials. If the caller context is null or empty, the service logs this message.

- Account verification failed for caller identity.

    This message is logged if the web method is expecting the caller to be a computer account and it's not. It can also be caused if the web method is expecting the caller to be a user account, and it's not a user account or a member of a data migration group account.

### 104: StatusServiceComplianceDbConfigError

The compliance database connection string in the registry is empty.

This message is logged whenever the compliance db connection string is invalid. Verify the value at the registry key `HKLM\Software\Microsoft\MBAM Server\Web\ComplianceDBConnectionString`.

### 105: StatusServiceComplianceDbError

This error indicates that the websites or web services were unable to connect to the compliance database. Verify that the IIS app pool account can connect to the database.

### 106: HelpdeskError

Known errors and possible causes:

- The request to URL caused an internal error.

    An unhandled exception was raised in the application for the administration and monitoring website (helpdesk). Review the log entries in the **Admin** event log to find the specific exception.

- An error occurred while obtaining execution context information. Unable to verify Service Principal Name (SPN) registration.

    During the initial helpdesk website load operation, it checks the SPN. To verify the SPN, it requires account information, IIS Sitename, and ApplicationVirtualPath corresponding to the helpdesk website. It logs this error message when one or more of these attributes are invalid or missing.

- An error occurred while verifying Service Principal Name (SPN) registration.

    This message indicates that a security exception is thrown when verifying the SPN. Refer to the exception contained in the event details.

### 107: SelfServicePortalError

Known errors and possible causes:

- An error occurred while getting recovery key for a user

    Indicates that an unexpected exception was thrown when a request was made to retrieve a recovery key. Refer to the exception message in the event details. If tracing is enabled on the helpdesk app, refer to trace data to obtain detailed exception messages.

- An error occurred while obtaining execution context information. Unable to verify Service Principal Name (SPN) registration

    During an initial load operation, the self-service portal retrieves account information, IIS Sitename, and ApplicationVirtualPath for the self-service website to verify the SPN. This error message is logged when one or more of these attributes are invalid.

- An error occurred while verifying Service Principal Name (SPN) registration. EventDetails:{ExceptionMessage}

    This message indicates that a security exception was thrown while verifying the SPN. Refer to the exception contained in the event details.

### 108: DomainControllerError

Known errors and possible causes:

- An error occurred while resolving domain name {DomainName}, a memory allocation failure occurred.

    To resolve domain name, it calls the `DsGetDcName` Windows API. This message is logged when this API returns `ERROR_NOT_ENOUGH_MEMORY`, which indicates a memory allocation failure.

- Could not invoke DsGetDcName method

    This message indicates that the `DsGetDcName` API is unavailable on the host.

### 109: WebAppRecoveryDbError

Known errors and possible causes:

- An error occurred while reading the configuration of the Recovery database. The connection string to the Recovery database is not configured.

    This message indicates that recovery database connection string information at `HKLM\Software\Microsoft\MBAM Server\Web\RecoveryDBConnectionString` is invalid. Verify the given registry key value.

If you see any of the following messages, verify whether  the app pool credentials from the IIS server can make a connection to the recovery database:

- DoesUserHaveMatchingRecoveryKey: an error occurred while getting recovery key Ids for a user.
- QueryDriveRecoveryData: an error occurred while getting drive recovery data.
- QueryRecoveryKeyIdsForUser: an error occurred while getting recovery key Ids for a user.
- An error occurred while getting TPM password hash from the Recovery database.

### 110: WebAppComplianceDbError

Known errors and possible causes:

- An error occurred while reading the configuration of the Compliance database. The connection string to the Compliance database is not configured.

    This message indicates that compliance database connection string information at `HKLM\Software\Microsoft\MBAM Server\Web\ComplianceDBConnectionString` is invalid. Verify the value of this registry key.

If you see any of the following messages, verify whether the app pool credentials from the IIS server can make a connection to the compliance database:

- GetRecoveryKeyForCurrentUser: an error occurred while logging an audit event to the Compliance database.
- QueryRecoveryKeyIdsForUser: an error occurred while logging an audit event to the Compliance database.
- QueryRecoveryKeyIdsForUser: an error occurred while logging an audit event to the compliance database.

### 111: WebAppDbError

These errors indicate one of the following two conditions

- MBAM websites/webservices were unable to either connect to compliance or recovery database
- MBAM websites/webservices execution account (app pool account) could not run the `GetVersion` stored procedure on compliance or recovery database

The message contained in the event provides more details about the exception.

Verify that the app pool account can connect to the compliance or recovery databases. Confirm that it has permissions to run the `GetVersion` stored procedure.

### 112: WebAppError

An error occurred while verifying Service Principal Name (SPN) registration.

To verify the SPN, it queries Active Directory to retrieve a list of SPNs mapped execution account. It also queries the `ApplicationHost.config` to get the website bindings. This error message indicates that it couldn't communicate with Active Directory, or it couldn't load the `ApplicationHost.config` file.

Verify that the app pool account has permissions to query Active Directory or the `ApplicationHost.config` file. Also verify the site binding entries in the `ApplicationHost.config` file.

## Operational

### 4: PerformanceCounterError

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

### 200: HelpDeskInformation

The administration website application successfully found and connected to a supported version of the recovery/compliance database.

Indicates successful connection to the recovery or compliance database from the helpdesk website.

### 201: SelfServicePortalInformation

The self-service portal application successfully found and connected to a supported version of the recovery/compliance database.

Indicates successful connection to the recovery or compliance database from the self-service portal.

### 202: WebAppInformation

Application has its SPNs registered correctly.

Indicates that the SPNs required for the helpdesk website are correctly registered against the executing account.

## See also

For more information on using these logs, see [BitLocker event logs](about-event-logs.md).

For more troubleshooting information, see [Troubleshoot BitLocker](troubleshoot.md).

For more information on installing these websites, see [Set up BitLocker reports and portals](../../deploy-use/bitlocker/setup-websites.md).
