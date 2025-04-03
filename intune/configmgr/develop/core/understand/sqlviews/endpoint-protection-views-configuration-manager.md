---
title: Endpoint protection views
titleSuffix: Configuration Manager
description: Information about the status of Endpoint Protection clients and malware activity in your Configuration Manager site.
ms.date: 04/30/2019
ms.subservice: sdk
ms.service: configuration-manager
ms.topic: reference
ms.assetid: 5f6b3676-b5d8-48f7-92c7-35366169a855
author: Banreet
ms.author: banreetkaur
manager: apoorvseth
ms.localizationpriority: low
ms.collection: tier3
ms.reviewer: mstewart,aaroncz 
---

# Endpoint protection views in Configuration Manager

The Configuration�Manager�Endpoint�Protection views provide information about the status of Endpoint Protection clients and malware activity in your Configuration Manager site.

The following sections provide detailed information about the Endpoint Protection views.

## Endpoint protection views

The Endpoint Protection views are described in this section.

### v_AM_NormalizedDetectionHistory

No description.

### v_OverallThreatActivity

This view lists each collection in the Configuration Manager site, by collection ID. For each collection, information such as the number of infected computers, the computers that require a restart and information about any malware that was recently removed are listed.
This view can be joined to other views by using the **CollectionID** column.

### v_OverallThreatActivity_History

This view lists each collection in the Configuration Manager site, by collection ID. For each collection, historical information such as the number of infected computers, the computers that require a restart and information about any malware that was recently removed are listed.
This view can be joined to other views by using the **CollectionID** column.

### v_EndpointProtectionCollections

Contains the collection ID and collection name of all collections that have the option **View this collection in the Endpoint Protection dashboard** checked on the **Alerts** tab of the *collection name*�**Properties** dialog box.
This view can be joined to other views by using the **CollectionID** and **CollectionName** columns.

### v_EndpointProtectionHealthStatus

Lists the collections protected by Endpoint Protection with information about the number of clients in each collection, clients that are considered at risk, clients that haven't been installed yet, clients that aren't supported and more.
This view can be joined to other views by using the **CollectionID** column.

### v_EndpointProtectionHealthStatus_History

Lists historical information about the collections protected by Endpoint Protection with information about the number of clients in each collection, clients that are considered at risk, clients that haven't been installed yet, clients that aren't supported and more.
This view can be joined to other views by using the **CollectionID** column.

### v_GS_AntimalwareHealthStatus

Lists information about the antimalware client installed on each Configuration Manager client computer, including whether the antimalware and antivirus components are enabled, the last scan time and date, the antimalware engine version, and more.
This view can be joined to other views by using the **ResourceID** column.

### v_GS_AntimalwareInfectionStatus

Lists information about the status of clients protected by Endpoint Protection, such as the status of the computer, whether it's pending a full scan or a restart, whether manual steps are required to resolve a malware infection, and more.
This view can be joined to other views by using the **ResourceID** column.

### v_EndpointProtectionStatus

Provides an overall summary of the status of Endpoint Protection clients for each computer, sorted by resource ID. This includes whether the client is protected, whether it's considered at risk, whether it supports Endpoint Protection, whether it requires a restart, and more.
This view can be joined to other views by using the **ResourceID** column.

### v_GS_Threats

Lists threats discovered on clients, sorted by resource ID.
This view can be joined to other views by using the **ResourceID** column.

### v_TopThreatsDetected

Lists, by collection ID, the top malware threats found on client computers. Includes the threat name, the number of computers in the collection that are affected, and more.
This view can be joined to other views by using the **CollectionID** column.

### v_ThreatSummary

Lists the possible descriptions of each malware threat that can be detected by Endpoint Protection.
It's unlikely that this view will be joined to other views.

### v_ThreatSeverities

Lists the threat severities, by severity ID that can be displayed in the Endpoint Protection dashboard to indicate the severity of discovered malware.
It's unlikely that this view will be joined to other views.

### v_ThreatDefaultActions

Lists the default actions, by default action ID that can be taken when malware is discovered on client computers.
It's unlikely that this view will be joined to other views.

### v_ThreatCategories

Lists the available threat categories, by category ID, that malware can be sorted into, such as trojans and spyware.
It's unlikely that this view will be joined to other views.

### v_ThreatCatalog

Lists all known threats, by threat ID. Includes the name, severity, and summary for the threat, together with the action that Endpoint Protection will take if the threat is discovered on client computers.
This view can be joined to other views by using the **ThreatID**, **SeverityID**, **CategoryID** and **DefaultActionID** columns.

### v_GS_EPDeploymentState

Lists, by resource ID, the current state of the Endpoint Protection client deployment to computers. Includes the last status sent by the client, the state of the deployment, and any errors that have been generated.
This view can be joined to other views by using the **ResourceID** column.

### v_CurrentThreatOutbreak

Lists, by resource ID, the malware threats that have been detected on client computers. This includes the threat ID, the threat name, when the threat was first detected and when it was last detected.
This view can be joined to other views by using the **ResourceID** column.

## See also

[SQL Server views in Configuration Manager](sql-server-views-configuration-manager.md)  
