---
title: Step 1. Create Microsoft Entra Conditional Access with Microsoft Edge for Business
description: Step 1. Create Microsoft Entra Conditional Access with Microsoft Edge for Business.
ms.date: 11/07/2025
ms.topic: how-to
ms.reviewer: samarti
ms.custom:
ms.collection:
- highpri
- highseo
- FocusArea_Apps_AppManagement
---

# Microsoft Entra Conditional Access with Microsoft Edge for Business

The modern security perimeter extends beyond an organization's network boundary to include user and device identity. Conditional Access brings identity-driven signals together to enforce organizational policies as part of a Zero Trust security model. It evaluates signals such as user risk, device compliance, and application context to determine whether access should be granted.

Conditional Access policies at their simplest follow *if-then* logic. If a user attempts to access a Microsoft 365 resource, then they may be required to complete an action such as multifactor authentication (MFA).

Identity-driven signals may include:

- User or group membership  
- IP location information  
- Device compliance state  
- Target application  
- Real-time and calculated risk detection  

Conditional Access is evaluated after authentication is completed. It is not intended to mitigate denial-of-service (DoS) attacks directly, but it can use signals from such events when making access decisions.

## Conditional Access compliance

Protecting organizational data requires preventing access from unprotected devices. Data Loss Prevention (DLP) is only effective when data cannot be accessed from systems that do not meet your organization’s minimum security requirements.

App protection policies (APP) work with Conditional Access to ensure that protected resources can only be accessed from managed or APP-protected applications, such as Microsoft Edge for Business. This enables end users on personal Windows, Android, and iOS devices to access Microsoft Entra resources without full device management.

This solution uses three Conditional Access policies to secure Microsoft Edge for Business along with a companion policy that keeps Windows desktop apps limited to compliant devices:

- **Level 1 – Basic:** Browser access for Windows, Android, and iOS users who rely on app protection policies.  
- **Level 2 – Enhanced Zero Trust:** Adds risk-based access controls, continuous verification, and device compliance requirements.  
- **Level 3 – High Zero Trust:** Enforces the strictest access posture with managed devices only, password resets for risky sign-ins, and frequent reauthentication.  
- **Browser-only companion policy:** Restricts Windows desktop apps such as Outlook or Word to managed, compliant devices.

## Before you begin

- Confirm that your tenant has the necessary Microsoft Entra ID Premium and Microsoft Intune licenses for Conditional Access and app protection policies.  
- Ensure the Microsoft Entra security groups `SEB-Level1-Users`, `SEB-Level2-Users`, and `SEB-Level3-Users` exist; these groups are used for assignments throughout the secure enterprise browser deployment. For step-by-step guidance, see [Use groups to organize users and devices for Microsoft Intune](../fundamentals/groups-add.md).  
- Define trusted locations, device filters, and risk integrations (for example, Microsoft Defender for Endpoint or another Mobile Threat Defense provider) before assigning the policies.  
- Plan to run each policy in **Report-only** mode first so you can validate the impact before enforcing it.

## Level 1 – Basic Conditional Access policy

Use this policy to secure browser access from Windows, Android, and iOS devices that rely on app protection policies instead of full device management.

1. Go to the [Microsoft Intune admin center](https://intune.microsoft.com).
2. Select **Endpoint security** > **Manage** > **Conditional Access** > **Create new policy**.
3. Configure the policy for the `SEB-Level1-Users` group:

         - **Name:** CA Edge Level 1 – Basic  
         - **Target resources:** **Cloud apps** > **Microsoft 365** (Office 365)  
         - **Conditions:**  
            - **Device platforms:** Include **Windows**, **Android**, and **iOS**  
            - **Client apps:** Select **Browser**  
            - **Filter for devices:** **Exclude** devices where *is Compliant equals True* to focus on unmanaged/BYOD endpoints  
         - **Grant:**  
            - **Require multifactor authentication**  
            - **Require app protection policy**  
         - **Session:** Leave unconfigured for Level 1

    > [!NOTE]
    > Keep the policy in **Report-only** mode until you verify that it routes unmanaged devices through Microsoft Edge for Business with app protection.

4. Select **Create** to save the policy.

## Level 2 – Enhanced Zero Trust Conditional Access policy

Level 2 adds continuous verification with risk-based signals and requires that devices are both compliant and protected by app protection policies.

1. Go to the [Microsoft Intune admin center](https://intune.microsoft.com).
2. Select **Endpoint security** > **Manage** > **Conditional Access** > **Create new policy**.
3. Configure the policy for the `SEB-Level2-Users` group:

         - **Name:** CA Edge Level 2 – Enhanced Zero Trust  
         - **Target resources:** **Cloud apps** > **All cloud apps**  
         - **Conditions:**  
            - **Device platforms:** Include **Windows**, **Android**, and **iOS**  
            - **Client apps:** Select **Browser**  
            - **Sign-in risk:** Set to **Medium and above**  
            - **Device risk:** Set to **Medium and above** (requires an integrated Mobile Threat Defense or Microsoft Defender for Endpoint signal)  
            - **Locations:** Include **All locations** and **Exclude** your trusted named locations  
            - **Filter for devices:** **Exclude** devices where *is Compliant equals True* so only noncompliant or unmanaged devices are subject to app protection enforcement  
         - **Grant:**  
            - **Require multifactor authentication**  
            - **Require app protection policy**  
            - **Require device to be marked as compliant**  
         - **Session:**  
            - **Use Conditional Access App Control** > **Monitor only**  
            - **Sign-in frequency:** Set to **Every 4 hours**  
            - **Persistent browser session:** Select **Never persistent**

    > [!NOTE]
    > Run the policy in **Report-only** mode and review the Monitoring workbooks to confirm the impact before switching it to **On**.

4. Select **Create** to save the policy.

## Level 3 – High Zero Trust Conditional Access policy

Level 3 enforces the strictest access posture by allowing only managed, compliant devices to reach Microsoft 365 resources while applying additional safeguards for risky sign-ins.

1. Go to the [Microsoft Intune admin center](https://intune.microsoft.com).
2. Select **Endpoint security** > **Manage** > **Conditional Access** > **Create new policy**.
3. Configure the policy for the `SEB-Level3-Users` group:

         - **Name:** CA Edge Level 3 – High Zero Trust  
         - **Target resources:** **Cloud apps** > **All cloud apps**  
         - **Conditions:**  
            - **Device platforms:** Include **Windows**, **Android**, and **iOS**  
            - **Client apps:** Select **Browser**  
            - **Sign-in risk:** Set to **Low and above**  
            - **User risk:** Set to **Low and above**  
            - **Device risk:** Set to **Any risk level**  
            - **Locations:** Include **All locations** and exclude only your most trusted named locations  
            - **Filter for devices:** Configure a **Include** filter that requires *is Managed equals True* **and** *is Compliant equals True* so only managed, compliant devices meet the policy  
         - **Grant:**  
            - **Require multifactor authentication**  
            - **Require app protection policy**  
            - **Require device to be marked as compliant**  
            - **Require password change** (for risky sign-ins)  
            - **Require approved client app**  
         - **Session:**  
            - **Use Conditional Access App Control** > **Monitor and block downloads**  
            - **Sign-in frequency:** Set to **Every 1 hour**  
            - **Persistent browser session:** Select **Never persistent**  
            - Enable **Continuous access evaluation**

    > [!NOTE]
    > Keep this policy in **Report-only** mode while you validate device filters, risk signals, and session controls with a small pilot group.

4. Select **Create** to save the policy.

## Browser-only access for Windows desktop apps

Use this companion policy to ensure that desktop applications on Windows devices are only available when the device meets your management and compliance requirements.

1. Go to the [Microsoft Intune admin center](https://intune.microsoft.com).
2. Select **Endpoint security** > **Manage** > **Conditional Access** > **Create new policy**.
3. Configure the policy and assign it to the `SEB-Level1-Users`, `SEB-Level2-Users`, and `SEB-Level3-Users` groups:

         - **Name:** CA Desktop Apps – Compliance Required  
         - **Target resources:** **Cloud apps** > **Microsoft 365**  
         - **Conditions:**  
            - **Device platforms:** Include **Windows**  
            - **Client apps:** Select **Mobile apps and desktop clients**  
         - **Grant:**  
            - **Require device to be marked as compliant**  
            - (Optional) **Require multifactor authentication** for additional assurance

    > [!NOTE]
    > If you allow legacy authentication clients, create a separate policy to block or restrict them so they cannot bypass the browser protections.

4. Leave the policy in **Report-only** mode until you confirm that desktop apps remain accessible only from enrolled and compliant devices, then switch it to **On**.

## Validate the policies

- Monitor the built-in Conditional Access insights while the policies run in report-only mode for at least one to two weeks.  
- Pilot the policies with a small user group before broad rollout and adjust exclusions or trusted locations if needed.  
- Review sign-in logs to verify that risky or unmanaged scenarios are challenged with multifactor authentication, app protection requirements, or blocked outright.  
- Document the final configuration so helpdesk teams can troubleshoot sign-in denials quickly.

## Next step

[:::image type="content" source="./media/securing-data-edge-for-business/securing-data-edge-for-business-steps-02.png" alt-text="Step 2 to create an app protection policy.":::](mamedge-2-app.md)

Continue with [Step 2](mamedge-2-app.md) to create an app protection policy.
