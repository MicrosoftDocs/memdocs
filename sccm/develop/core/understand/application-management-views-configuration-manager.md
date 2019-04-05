---
title: Application Management Views in Configuration Manager
TOCTitle: Application Management Views in Configuration Manager
ms:assetid: 567c2de3-44c1-4754-b5a3-09ba6b3fd831
ms:mtpsurl: https://technet.microsoft.com/en-us/library/Dn581963(v=TechNet.10)
ms:contentKeyID: 60772027
ms.date: 07/27/2015
mtps_version: v=TechNet.10
---

<div data-xmlns="http://www.w3.org/1999/xhtml">

<div class="topic">

<div>

# Application Management Views in Configuration Manager

</div>

<div id="mainSection">

<div id="mainBody">

<div class="introduction">

The Configuration Manager application management views can be used to query for information about applications, packages and programs, deployments, distribution points, and more. These views will most often be joined to other views by using the **AdvertisementID**, **PackageID**, or **CollectionID** columns. Many of the status views also provide information about the status for applications and deployments. For more information about Configuration Manager applications, see [Application Management in Configuration Manager](gg699373\(v=technet.10\).md).

The following sections provide detailed information about application management views and application management status views.

</div>

<div>

## Application Management Views

<div class="section">

The application management views are described in the following table.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Application management View</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>v_Advertisement</strong></p></td>
<td><p>Lists information about the deployment of packages and programs, including the deployment ID (<strong>AdvertisementID</strong>), deployment name (<strong>AdvertisementName</strong>), package ID, program name, collection ID, schedule information, and more. The <strong>v_Advertisement</strong> view is similar to the <strong>v_AdvertisementInfo</strong> view, but with additional time and flag data.</p>
<p>The view can be joined to other views by using the <strong>AdvertisementID</strong>, <strong>PackageID</strong>, and <strong>CollectionID</strong> columns.</p></td>
</tr>
<tr class="even">
<td><p><strong>v_AdvertisementInfo</strong></p></td>
<td><p>Lists information about deployed packages and programs, including the deployment ID (<strong>AdvertisementID</strong>), deployment name (<strong>AdvertisementName</strong>), package ID, program name, collection ID, schedule information and more. The <strong>v_AdvertisementInfo</strong> view is similar to the <strong>v_Advertisement</strong> view, but with additional package data.</p>
<p>The view can be joined to other views by using the <strong>AdvertisementID</strong>, <strong>PackageID</strong>, and <strong>CollectionID</strong> columns.</p></td>
</tr>
<tr class="odd">
<td><p><strong>v_CurrentAdvertisementAssignments</strong></p></td>
<td><p>Lists the current application deployments, by advertisement ID, and the resource ID that is assigned the advertisement.</p>
<p>The view can be joined to other views by using the <strong>AdvertisementID</strong> or <strong>ResourceID</strong> columns.</p></td>
</tr>
<tr class="even">
<td><p><strong>v_DistributionPoint</strong></p></td>
<td><p>Lists the distribution points and the application and software updates packages contained on each in the Configuration Manager site hierarchy. This view also provides the package ID, NAL path to the distribution point, site code, site name, source site, last refresh time, status, and more.</p>
<p>The view can be joined to other views by using the <strong>PackageID</strong> and <strong>ServerNALPath</strong> columns.</p></td>
</tr>
<tr class="odd">
<td><p><strong>v_DistributionPointInfo</strong></p></td>
<td><p>Lists the distribution points in the Configuration Manager site hierarchy, including server name, share name, NAL path, site code, whether it is a branch distribution point, whether it is a pull distribution point and more.</p>
<p>The view can be joined to other views by using the <strong>ServerName</strong> and <strong>NALPath</strong> columns.</p></td>
</tr>
<tr class="even">
<td><p><strong>V_MDMApplications</strong></p></td>
<td><p>Lists information about applications created for mobile devices including the application name, description, publisher and more.</p>
<p>It is unlikely that this view will be joined to other views.</p></td>
</tr>
<tr class="odd">
<td><p><strong>v_OS_Details</strong></p></td>
<td><p>Lists the Configuration Manager supported platforms, including operating system, architecture, and versions, on which each specified software distribution program can run. The view contains the package ID, program name, operating system name, platform, and minimum and maximum operating system versions.</p>
<p>The view can be joined to other views by using the <strong>PackageID</strong> column.</p></td>
</tr>
<tr class="even">
<td><p><strong>v_SMSPackage</strong></p></td>
<td><p>Lists the packages in the Configuration Manager site hierarchy, including package ID, package name, the path of the package source files, source site, priority, package flags, last refresh time, and so forth. All packages are listed, including software deployment packages, boot image packages, and more.</p>
<p>The view can be joined to other views by using the <strong>PkgID</strong> column.</p></td>
</tr>
<tr class="odd">
<td><p><strong>v_Program</strong></p></td>
<td><p>Lists the programs for each package in the Configuration Manager site hierarchy, including program name, package ID, program command line, dependent programs, program flags, and so forth.</p>
<p>The view can be joined to other views by using the <strong>PackageID</strong> column.</p></td>
</tr>
<tr class="even">
<td><p><strong>v_UserTargetedApps</strong></p></td>
<td><p>Lists each Configuration Manager application that has been deployed to a user. Includes the application ID (<strong>CI_ID</strong>), the collection to which the application has been deployed (if any), and whether the application requires approval.</p>
<p>This view can be joined to other views by using the <strong>CI_ID</strong> or <strong>CollectionID</strong> columns.</p></td>
</tr>
<tr class="odd">
<td><p><strong>v_UserTargetedClassicApps</strong></p></td>
<td><p>Lists each package and program that has been deployed to users. Includes the program ID, the category, the publisher, the package and program name and more.</p>
<p>This view can be joined to other views by using the <strong>ProgramID</strong>, <strong>PackageID</strong>, or <strong>CollectionID</strong> columns.</p></td>
</tr>
<tr class="even">
<td><p><strong>v_DeploymentSummary</strong></p></td>
<td><p>Lists all deployments that are currently active at the site. Includes the collection to which the deployment was targeted, the name of the deployment, the deployment time, deployment statistics and more.</p>
<p>This view can be joined to other views by using the <strong>CollectionID</strong> or <strong>PackageID</strong> columns.</p></td>
</tr>
<tr class="odd">
<td><p><strong>v_ApplicationModelInfo</strong></p></td>
<td><p>Lists the applications, by <strong>CI_ID</strong> that have been created. Also lists the deployment type technology and any secured key for the application.</p>
<p>This view can be joined to other views by using the <strong>CI_ID</strong> column.</p></td>
</tr>
<tr class="even">
<td><p><strong>v_AppModelTargetingDeploymentInfo</strong></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p><strong>v_AppModelTargetingInfo</strong></p></td>
<td></td>
</tr>
<tr class="even">
<td><p><strong>v_Package</strong></p></td>
<td><p>Returns all packages that contain content for an application, package and program, or a task sequences at this site.</p>
<p>This view can be joined to other views by using the <strong>PackageID</strong> column.</p></td>
</tr>
<tr class="odd">
<td><p><strong>v_ClassicAppTargetingDeploymentInfo</strong></p></td>
<td></td>
</tr>
<tr class="even">
<td><p><strong>v_ClassicAppTargetingInfo</strong></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p><strong>v_ClassicDeploymentAssetDetails</strong></p></td>
<td><p>Lists information and status for standard package and program deployments by deployment ID. This includes the program name, package name, collection to which it has been deployed, and more.</p>
<p>This view can be joined to other views by using the <strong>DeploymentID</strong>, <strong>PackageID</strong>, <strong>CollectionID</strong> and <strong>DeviceID</strong> columns.</p></td>
</tr>
<tr class="even">
<td><p><strong>v_AppDeploymentSummary</strong></p></td>
<td><p>Lists deployment statistics for about Configuration Manager applications that have been deployed to clients. This includes the <strong>CI_ID</strong>, target collection, localized display name, description and more.</p>
<p>This view can be joined to other views by using the <strong>CI_ID</strong>, <strong>AssignmentID</strong> and <strong>TargetCollectionID</strong> columns.</p></td>
</tr>
<tr class="odd">
<td><p><strong>v_AppDTDeploymentSummary</strong></p></td>
<td><p>Lists information about deployment types that have been deployed to devices, by <strong>CI_ID</strong>. This includes the deployment type name, the target collection, and status information about the deployment.</p>
<p>This view can be joined to other views by using the <strong>CI_ID</strong>, <strong>AssignmentID</strong> and <strong>TargetCollectionID</strong> columns.</p></td>
</tr>
<tr class="even">
<td><p><strong>v_AppDTLaunchSummary</strong></p></td>
<td><p>Lists information, by <strong>AppCI</strong>, about deployment types that have run on client devices. This includes the assignment ID, the collection, the deployment type technology and more.</p>
<p>This view can be joined to other views by using the <strong>AppCI</strong> column.</p></td>
</tr>
<tr class="odd">
<td><p><strong>v_AppEvalErrors</strong></p></td>
<td><p>Lists all devices, by machine ID where the application evaluation failed, for example, if the application failed any requirements rules.</p>
<p>This view can be joined to other views by using the <strong>MachineID</strong> column.</p></td>
</tr>
<tr class="even">
<td><p><strong>v_AppInTaskSequenceDeployment</strong></p></td>
<td><p>Lists, by task sequence name, all deployed task sequences that contain an application deployment. This includes the collection to which the task sequence was deployed and the deployment ID.</p>
<p>This view can be joined to other views by using the <strong>Name</strong> column.</p></td>
</tr>
<tr class="odd">
<td><p><strong>v_AppIntentAssetData</strong></p></td>
<td><p>Lists for each computer (and each user if deployed to a user), compliance state information by <strong>AssignmentID</strong> and Application ID (<strong>AppCI</strong>). State information includes <strong>ComplianceState</strong>, <strong>EnforcementState</strong>, applicability, and desired compliance state.</p>
<p>This view can be joined to other views by using the <strong>ID</strong> columns and to <strong>vAppStatSummary</strong> by using the <strong>AppCI</strong> column.</p></td>
</tr>
<tr class="even">
<td><p><strong>v_AppInTSDeployment</strong></p></td>
<td><p>Lists, by name, all applications that are deployed by a task sequence.</p>
<p>This view can be joined to other views by using the <strong>Name</strong> column.</p></td>
</tr>
<tr class="odd">
<td><p><strong>v_ApplicationAssignment</strong></p></td>
<td><p>Lists detailed information about Configuration Manager application deployments, by <strong>AssignmentID</strong>. This includes the name of the application, the collection to which it was deployed, the creation time and more.</p>
<p>This view is particularly useful when you want to examine the status of your <strong>cmshort</strong> deployments.</p>
<p>This view can be joined to other views by using the <strong>AssignmentID</strong> and <strong>CollectionID</strong> columns.</p></td>
</tr>
<tr class="even">
<td><p><strong>v_CatalogAppModelProperties</strong></p></td>
<td></td>
</tr>
<tr class="odd">
<td><p><strong>v_CatalogClassicAppProperties</strong></p></td>
<td></td>
</tr>
<tr class="even">
<td><p><strong>v_UserAppRequests</strong></p></td>
<td><p>Lists details about users requests for applications, sorted by <strong>CI_UniqueID</strong>. This includes the application ID, the name of the user requesting the application, the display name of the application and the device from which the request was made.</p>
<p>This view can be joined to other views by using the <strong>CI_UniqueID</strong>, <strong>Unique_User_Name0</strong> and <strong>Netbios_Name0</strong> columns.</p></td>
</tr>
<tr class="odd">
<td><p><strong>v_UserAppsLocalizedPropsForCatalog</strong></p></td>
<td></td>
</tr>
</tbody>
</table>

</div>

</div>

<div>

## Application Management Status Views

<div class="section">

The application management status views contain status and status summary information about application deployments, applications and packages and programs. For more information about status views, see [Status and Alert Views in Configuration Manager](dn581980\(v=technet.10\).md). The status views that contain application management information are described in the following table.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Application management view</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>v_AdvertisementStatusInformation</strong></p></td>
<td><p>Lists all advertisement status message IDs, the message state, and the message name, such as succeeded, expired, failed, and retrying.</p>
<p>The view can be joined to other advertisement status views by using the <strong>MessageID</strong> column.</p></td>
</tr>
<tr class="even">
<td><p><strong>v_ClientAdvertisementStatus</strong></p></td>
<td><p>Lists all package and program deployments with the associated status for resources that have been targeted.</p>
<p>The view can be joined to other views by using the <strong>AdvertisementID</strong>, <strong>ResourceID</strong>, and <strong>LastStatusMessageID</strong> columns.</p></td>
</tr>
<tr class="odd">
<td><p><strong>v_ClientOfferSummary</strong></p></td>
<td><p>Lists the package and program deployments, by <strong>OfferID</strong>, the count of Configuration Manager client computers that have been targeted, and the count of computers reporting not started, waiting, running, retrying, failed, and succeeded status for the advertisement.</p>
<p>The view can be joined to other views by using the <strong>OfferID</strong> column, which is the same as the <strong>AdvertisementID</strong> column in other views, and <strong>PkgID</strong> column, which is the same as the <strong>PackageID</strong> column in other views.</p></td>
</tr>
<tr class="even">
<td><p><strong>v_PackageStatus</strong></p></td>
<td><p>Lists the status for all software distribution and software update deployment packages, as well as the package server location, last update time, last status and more.</p>
<p>The view can be joined to other views by using the <strong>PackageID</strong> column.</p></td>
</tr>
<tr class="odd">
<td><p><strong>v_PackageStatusDetailSumm</strong></p></td>
<td><p>Lists all applications and packages and programs, by Package ID, the originating site code, package name, site name, source version, the date for the summary information, the targeted count for each package, and the count for installed, retrying, and failed status.</p>
<p>The view can be joined to other views by using the <strong>PackageID</strong> column.</p></td>
</tr>
<tr class="even">
<td><p><strong>v_PackageStatusDistPointsSumm</strong></p></td>
<td><p>Lists all packages, by package ID, and the installation status for the package source files on all associated distribution points. The view also provides information such as the site code, path to the distribution point, path to source location, time of last copy, and so on.</p>
<p>The view can be joined to other views by using the <strong>PackageID</strong> and <strong>ServerNALPath</strong> columns.</p></td>
</tr>
<tr class="odd">
<td><p><strong>v_PackageStatusRootSummarizer</strong></p></td>
<td><p>Lists all applications and packages and programs, by package ID, the package name, source version, source date, the source site, size of the source files, the targeted count for each package, and the count for installed, retrying, and failed status.</p>
<p>The view can be joined to other views by using the <strong>PackageID</strong> column.</p></td>
</tr>
<tr class="even">
<td><p><strong>v_PeerDPStatusInfo</strong></p></td>
<td><p>Lists the peer distribution point states and associated state names.</p>
<p>It is unlikely that this view will be joined to other views.</p></td>
</tr>
<tr class="odd">
<td><p><strong>v_ProgramOffers</strong></p></td>
<td><p>Lists all programs that have been deployed as part of a package and program. This is sorted by package ID and the program name.</p>
<p>The view can be joined to other views by using the <strong>PkgID</strong> column.</p></td>
</tr>
</tbody>
</table>

</div>

</div>

<div>

## User Device Affinity Views

<div class="section">

The user device affinity views contain information about configured relationships between users and primary devices. The views that contain user device affinity information are described in the following table.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>User device affinity view</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>v_UsersPrimaryMachines</strong></p></td>
<td><p>Lists, by user resource ID, the primary devices for that user.</p>
<p>This view can be joined to other views by using the <strong>MachineID</strong> or <strong>UserResourceID</strong> columns.</p></td>
</tr>
<tr class="even">
<td><p><strong>v_UserMachineIntelligence</strong></p></td>
<td><p>Lists information, by resource ID about user logons to devices. This information can be used by user device affinity to create automatic affinities. The information collected includes the user name, device name, client type, number of logons, and time spent for each session.</p>
<p>This view can be joined to other views by using the <strong>MachineResourceID</strong> column.</p></td>
</tr>
<tr class="odd">
<td><p><strong>v_UserMachineRelation</strong></p></td>
<td><p>Lists detailed information about user device relationships in the Configuration Manager site including the relationship ID, the user name, the device ID, the creation time and more.</p>
<p>This view can be joined to other views by using the <strong>MachineResourceID</strong> column.</p></td>
</tr>
<tr class="even">
<td><p><strong>v_UserMachineRelationship</strong></p></td>
<td><p>Lists information about users and their primary devices in the site. Includes the user name, the device resource ID, the time the relationship was created, and more.</p>
<p>This view can be joined to other views by using the <strong>UniqueUserName</strong> or <strong>MachineResourceID</strong> columns.</p></td>
</tr>
<tr class="odd">
<td><p><strong>v_UserMachineSourceRelation</strong></p></td>
<td><p>Lists all user device affinity relationships, by relationship resource ID, when they were created, and who created them.</p>
<p>This view can be joined to other views by using the <strong>RelationshipResourceID</strong> column.</p></td>
</tr>
<tr class="even">
<td><p><strong>v_UserMachineTypeRelation</strong></p></td>
<td><p>Lists user and device relationships by relationship resource ID, relationship type, and creation time.</p>
<p>It is unlikely that this view will be joined to other views.</p></td>
</tr>
</tbody>
</table>

</div>

</div>

<div>

## See Also

[SQL Server Views in Configuration Manager](sql-server-views-configuration-manager.md)  

</div>

</div>

</div>

</div>

</div>

