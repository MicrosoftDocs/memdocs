---
title: Use Endpoint Privilege Management to transition users from administrator to standard user
description: Understand the steps and phases for using Endpoint Privilege Management to transition users from administrators to standard users.
keywords:
author: brenduns
ms.author: brenduns
manager: dougeby
ms.date: 07/22/2025
ms.topic: how-to
ms.service: microsoft-intune
ms.subservice: protect
ms.localizationpriority: high

# optional metadata

#ROBOTS:
#audience:
 
ms.reviewer: mikedano
ms.suite: ems
search.appverid: MET150
#ms.tgt_pltfrm:
ms.custom: intune-azure
ms.collection:
- tier 1
- M365-identity-device-management
- sub-intune-suite
---

# Use Endpoint Privilege Management to transition users from administrator to standard user

[!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)]

A common scenario for customers who want to use Endpoint Privlege Management is to reduce the number of local administrators in their environment. This adheres to the Zero Trust principle of least privelege. This document steps through the steps a customer could follow to leverage EPM to move users from administrators to standard users with minimal disruption.

Applies to:

- Windows 10
- Windows 11

## Phase 1: Auditing

Regardless of whether you are migrating from another endpoint privilege management product or starting fresh, it is recommended to enable auditing as the first step. Enabling auditing will enable the EPM client and devices will send diagnostic data to Intune, where it can be viewed in a variety of reports. Gathering this elevation data will provide insights into which processes users are leveraging elevation for, and help to identify common patterns – ideally aligned to the personas that you have defined, such as developers, IT support technicians, etc. The deployment of this policy for auditing is seamless, and can be targeted to a group of users or devices of your choosing, as per any regular Intune policy assignment.

Once enabled, usage data can take 24 hrs to be returned and for the Intune portal reports to be updated. Depending on usage patterns, you may want to view reporting data over a period of many weeks to gather a better understanding of your environment.

**Steps to create the policy:**

1. Logon to the Intune portal
2. Select Endpoint Security > Endpoint Privilege Management > Policies
3. Select Create Policy. Enter the following details:
   - Platform: Windows
   - Profile: Elevation settings policy
4. Select Create
5. Provide name for the policy, such as: EPM settings policy – Audit only
6. Select Next
7. Expand the 'Privilege management elevation client settings' section and ensure the following values are set:
   - Endpoint Privilege Management: Enabled
   - Default elevation response: Not Configured
   - Send elevation data for reporting: Yes
   - Reporting scope: Diagnostic data and all endpoint elevations
8. Select Next
9. Leave the Scope tags and select Next
10. Add a group of devices or users that you want to target the policy to
11. Select Next
12. Select Create to create the policy

**To confirm that the rule is functioning as expected:**

- Logon to the Windows 10 / 11 device with the standard user credentials.
- Start > Run > Services.msc > Ok
- Check that the 'Microsoft EPM Agent Service' is present, Running and set to Automatic startup type.
- Close the Services snap-in.
- Start > Run > C:\Program Files\ > Ok
- Verify that there is a folder called: Microsoft EPM Agent

**After 24 hrs or more have passed:**

- Logon to the Intune portal
- Select Endpoint Security > Endpoint Privilege Management > Reports
- Select Elevation report
- Review the details of the elevation report

Identify groups of users (ideally aligning with the personas you identified earlier) who have similar elevation requirements. Identifying both usage patterns and user groups will assist with subsequent steps which involve building rules and targeting those rule settings policies.

This report will include some default Windows processes in the File column (e.g. C:\Windows\System32\Dism\dismhost and c:\Windows\System32\conhost.exe) which can be ignored.

## Phase 2: Persona identification

Using user personas in the design of Microsoft Intune Endpoint Privilege Management (EPM) policies is a strategic way to align elevation settings and rules with real-world user needs.

**What Are User Personas in EPM?**

User personas are fictional but data-driven representations of different user types within your organization. Each persona reflects a group of users with similar roles, responsibilities, and application needs.

**How do personas help design elevation settings and rules?**

Mapping out the user needs allows you to define elevation strategy for each user cohort. This design allows for flexibility by offering different default elevation responses for each cohort. This is useful, for example, if you have groups of trusted users that you need any elevation not defined by a rule to follow a particular elevation response.

| Persona Type     | Example Roles             | Elevation Strategy                                | Default Elevation |
|------------------|---------------------------|---------------------------------------------------|-------------------|
| Power Users      | IT Support Technicians, IT Power Users | Automatic elevation for defined rules             | Deny all requests |
| Developers       | Engineering               | Automatic elevation for defined low risk apps; User justified for higher risk apps | Support Approved  |
| Standard Users   | Finance, HR               | Automatic elevation for defined rules             | Deny all requests |

**Consider augmenting your elevation rules with deny rules**

Using deny rules on top of your personas for applications or processes considered high risk or legacy will take precedence over any default elevation setting.

## Phase 3: Create rules

EPM rules consist of two fundamental elements: a detection and an elevation action.

Detections are defined as the set of attributes used to identify an application or binary. These attributes include file name, file version, and signature properties. Elevation actions are the resulting elevation that occurs after an application or binary is detected.

**Best practices:**

- Use strong attributes or multiple attributes to increase detection strength.
- Either a file hash or certificate is mandatory.

**Steps to create a rule using elevation report data:**

1. Logon to the Intune Admin Center
2. Select Endpoint Security > Endpoint Privilege Management > Policies
3. Select Elevation report
4. Click on an application or process (e.g. C:\Program Files\Notepad++\)
5. Select Create a rule with these details:
   - Create a new policy
   - Type: User-confirmed
   - Child process behaviour: Require rule to elevate
   - Require the same file path as this elevation: selected
6. Select OK
7. Provide a Policy name (e.g. EPM rule – Notepad++ User Confirmed)
8. Select Yes
9. Navigate to the list of EPM policies and select the policy
10. Under Assignments, select Edit
11. Select Add groups
12. Assign to a group (e.g. Developers)
13. Select, Review and Save

**To confirm the rule is functioning:**

- Logon to the Windows 10 / 11 device with standard user credentials.
- Right-click the application (e.g. Notepad++) and select 'Run with elevated access'
- On the Endpoint Privilege Management pop-up, select Continue
- Verify the application launches with elevated permissions

## Phase 4: Remove local admin rights

**Steps:**

1. Logon to the Intune Admin Center
2. Select Endpoint Security > Account protection
3. Select Create Policy:
   - Platform: Windows
   - Profile: Local user group membership
4. Provide name for the policy (e.g. Remove local admin rights (developers))
5. Select Add:
   - Local group: Administrators
   - Group and user action: Add (Replace)
   - User selection type: Manual
6. Click Select users(s)
7. Add the 2 Security Identifiers (SID's) for:
   - Global Administrator
   - Microsoft Entra Joined Device Local Administrator

    > Use Lusmgr.msc on an Entra-joined device to find SIDs starting with S-1-12-1-

8. Assign to a group (e.g. Developers)
9. Select Save

## Phase 5: Monitoring

- Regularly review elevation reports
- Add unmanaged elevations to rules or deny them
- Evaluate ROI of EPM
- Monitor support-approved requests for delays or patterns
- Update rules when file versions or certs change
- Retire or tighten outdated rules

## Next steps

> [!div class="nextstepaction"]
> [Next: Create an elevation settings policy >](epm-elevation-settings.md)
