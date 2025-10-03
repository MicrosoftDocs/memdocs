---
title: Use Endpoint Privilege Management to transition users from administrator to standard user
description: Understand the steps and phases for using Endpoint Privilege Management to transition users from administrators to standard users.
author: brenduns
ms.author: brenduns
ms.date: 09/10/2025
ms.topic: how-to
ms.reviewer: mikedano
ms.collection:
- tier 1
- M365-identity-device-management
- sub-intune-suite
---

# Use Endpoint Privilege Management to transition users from administrator to standard user

[!INCLUDE [intune-add-on-note](../includes/intune-add-on-note.md)]

[!INCLUDE [intune-epm-overview](includes/intune-epm-overview.md)]

A common scenario for customers who want to use Endpoint Privilege Management is to reduce the number of local administrators in their environment. This scenario adheres to the Zero Trust principle of least privilege. This document steps through the steps a customer could follow to use EPM to move users from administrators to standard users with minimal disruption.

## Phase 1: Auditing

Regardless of whether you're migrating from another endpoint privilege management product or starting fresh, we recommend enabling auditing as the first step. Enabling auditing enables the EPM client and devices to send diagnostic data to Intune, where it can be viewed in various reports. Gathering this elevation data provides insights into which processes users are seeking to elevate, and help to identify common patterns. Ideally, these align to your personas, such as developers, IT support technicians, etc. The deployment of this policy for auditing is seamless, and can be targeted to a group of users or devices of your choosing, as per any regular Intune policy assignment.

> [!NOTE]
> Once enabled, usage data can take 24 hrs to be returned and for the Intune portal reports to be updated. Depending on usage patterns, you might want to view reporting data over a period of many weeks to gather a better understanding of your environment.

**Steps to create the policy:**

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Endpoint Security** > **Endpoint Privilege Management** > **Policies**
3. Select **Create Policy**. Enter the following details:
   - **Platform:** Windows
   - **Profile:** Elevation settings policy
4. Select **Create**
5. Provide name for the policy, such as: EPM settings policy – Audit only
6. Select **Next**
7. Expand the 'Privilege management elevation client settings' section and ensure the following values are set:
   - **Endpoint Privilege Management:** Enabled
   - **Default elevation response:** Not Configured
   - **Send elevation data for reporting:** Yes
   - **Reporting scope:** Diagnostic data and all endpoint elevations
8. Select **Next**
9. Leave the **Scope tags** and select **Next**
10. Add a group of devices or users that you want to target the policy to
11. Select **Next**
12. Select **Create** to create the policy

**To confirm that the rule is functioning as expected:**

- Sign in to the Windows device with the standard user credentials.
- **Start** > **Run** > **Services.msc** > Ok
- Check that the *'Microsoft EPM Agent Service'* is present, Running, and set to Automatic startup type.
- Close the Services snap-in.
- **Start** > **Run** > `C:\Program Files\` > Ok
- Verify that there's a folder called: *Microsoft EPM Agent*

**After 24 hrs or more have passed:**

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Endpoint Security** > **Endpoint Privilege Management** > **Reports**
3. Select **Elevation report**
4. Review the details of the elevation report

Identify groups of users (ideally aligning with the personas you identified earlier) who have similar elevation requirements. Identifying both usage patterns and user groups assists with subsequent steps.

> [!TIP]
> This report includes some default Windows processes in the File column (for example `C:\Windows\System32\Dism\dismhost and c:\Windows\System32\conhost.exe`) which can be ignored.

## Phase 2: Persona identification

Using user personas in the design of Microsoft Intune Endpoint Privilege Management (EPM) policies is a strategic way to align elevation settings and rules with real-world user needs.

### What Are User Personas in EPM?

User personas are data-driven representations of different user types within your organization. Each persona reflects a group of users with similar roles, responsibilities, and application needs.

Example persona mapping:

| Persona Type     | Example Roles             | Elevation Strategy                                | Default Elevation |
|------------------|---------------------------|---------------------------------------------------|-------------------|
| Power Users      | IT Support Technicians, IT Power Users | Automatic elevation for defined rules             | Deny all requests |
| Developers       | Engineering               | Automatic elevation for defined low risk apps; User justified for higher risk apps | Support Approved  |
| Standard Users   | Finance, HR               | Automatic elevation for defined rules             | Deny all requests or support approved |

### How do personas help design elevation settings and rules?

Mapping out the user needs allows you to define elevation strategy for each user cohort.

## Phase 3: Create rules

EPM rules consist of two fundamental elements: a detection and an elevation action.

Detections are defined as the set of attributes used to identify an application or binary. These attributes include file name, file version, and signature properties. Elevation actions are the resulting elevation that occurs after an application or binary is detected.

### Best practices

- Use strong attributes or multiple attributes to increase detection strength.
- Either a file hash or certificate is mandatory.

For more security recommendations, see [Security Recommendations](epm-plan.md#security-recommendations).

### Steps to create a rule using elevation report data

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Endpoint Security** > **Endpoint Privilege Management** > **Policies**
3. Select **Elevation report**
4. Select an application or process (for example. `C:\Program Files\Notepad++\`)
5. Select **Create a rule with these details**:
   - Create a new policy
   - **Type:** User-confirmed
   - **Child process behavior:** Require rule to elevate
   - **Require the same file path as this elevation:** selected
6. Select **OK**
7. Provide a Policy name (for example `EPM rule – Notepad++ User Confirmed`)
8. Select **Yes**
9. Navigate to the list of EPM policies and select the policy
10. Under **Assignments**, select **Edit**
11. Select **Add groups**
12. Assign to a group (for example Developers)
13. **Select**, **Review**, and **Save**

For more details on creating a rule, see [Create elevation rules](epm-elevation-rules.md).

### Confirm the rule is functioning

- Sign in to the Windows device with standard user credentials.
- Right-click the application (for example `Notepad++`) and select **'Run with elevated access'**
- On the Endpoint Privilege Management pop-up, select **Continue**
- Verify the application launches with elevated permissions

## Phase 4: Remove local admin rights

1. Sign in to the [Microsoft Intune admin center](https://go.microsoft.com/fwlink/?linkid=2109431).
2. Select **Endpoint Security** > **Account protection**
3. Select Create Policy:
   - **Platform:** Windows
   - **Profile:** Local user group membership
4. Provide name for the policy (for example `Remove local admin rights (developers)`)
5. Select Add:
   - **Local group**: Administrators
   - **Group and user action**: Add (Replace)
   - **User selection type:** Manual
6. Select **users(s)**
7. Add the two Security Identifiers (SIDs) for:
   - Global Administrator
   - Microsoft Entra Joined Device Local Administrator

    > Use Lusrmgr.msc on an Entra-joined device to find SIDs starting with S-1-12-1-

8. Assign to a group (for example `Developers`)
9. Select **Save**

For more information on the Local Users and Groups profiles, see [Account protection](endpoint-security-account-protection-policy.md)

## Phase 5: Monitoring

- Regularly review elevation reports
- Add unmanaged elevations to rules or deny them
- Monitor support-approved requests for delays or patterns
- Update rules when file versions or certs change
- Retire or tighten outdated rules

---

## Next steps

> [!div class="nextstepaction"]
> [Next: Support approved requests >](epm-support-approved.md)
