
# App Protection Policy

App protection policies (APP) are rules that ensure an organization's data remains safe or contained in a managed app. A policy can be a rule that is enforced when the user attempts to access or move corporate data, or a set of actions that are prohibited or monitored when the user is inside the app. A managed app is an app that has app protection policies applied to it and can be managed by Intune.


## App Protection Policy Framework

When configuring App protection policies, there are many various settings and options to enable organizations to tailor the protection to their specific needs. Due to this flexibility, it may not be obvious which combination of policy settings are required to implement a complete scenario. To help organizations prioritize client endpoint hardening efforts, Microsoft has introduced a new taxonomy for security configurations in Windows, and Intune is using a similar taxonomy for its APP data protection framework for mobile app management.

The APP data protection configuration framework is organized into three distinct configuration scenarios:

1. **Level 1 enterprise basic data protection**
 Microsoft recommends this configuration as the minimum data protection configuration for an enterprise device.

2. **Level 2 enterprise enhanced data protection**
    Microsoft recommends this configuration for devices where users access sensitive or confidential information. This configuration is applicable to most mobile users accessing work or school data. Some of the controls may impact user experience.

3. **Level 3 enterprise high data protection**
    Microsoft recommends this configuration for devices run by an organization with a larger or more sophisticated security team, or for specific users or groups who are at uniquely elevated risk (users who oversee sensitive data where unauthorized disclosure causes considerable material loss to the organization). An organization likely to be targeted by well-funded and sophisticated adversaries should aspire to this configuration.

### Data Protection Framework deployment methodology
With any deployment of new software, features or settings, Microsoft recommends investing in a ring methodology for testing validation prior to deploying the APP data protection framework. Defining deployment rings is a one-time event (or at least infrequent), but IT should revisit these groups to ensure that the sequencing is still correct.

For more information about Framework Settings, see [App protection framework](..\apps\app-protection-framework.md).

### App Protection Policy for Microsoft Edge for Business (Windows)

**App protection policies for Windows**: This feature provides secure and compliant access to work resources on personal computers with Data Loss Prevention (DLP) controls.

Having gained a comprehensive understanding of the app protection policy framework, we're now prepared to establish our initial app protection policy for Windows. In this instance, we'll be formulating a **Level 3** policy. As highlighted in this document, the framework allows for the creation of various levels to cater to our specific requirements. So, the forthcoming example may only be applicable to the **Level 3** policy that we have recommended. It's crucial to replicate these steps for each level, ensuring that the values are adjusted in accordance with the recommendations provided. This approach guarantees that each policy level is accurately configured to meet our distinct needs.

**Let us begin:**

1. Go to <https://intune.microsoft.com/>. Once authenticated select on Apps on the left menu.

2. Select on **App protection policies**.

:::image type="content" alt-text="Apps Overview - Microsoft Intune Admin Center." source="./media/securing_data_edge_for_business7.png" lightbox="./media/securing_data_edge_for_business7.png":::

3. Select on **Create policy** \> **Windows**.

:::image type="content" alt-text="Apps Overview - Microsoft Intune Admin Center." source="./media/securing_data_edge_for_business8.png" lightbox="./media/securing_data_edge_for_business8.png":::

4. On the Create policy Fill in the details as shown in

> **Name:** Level 3 secure enterprise browser Policy
>
> **Description:** The following is a Level 3 App Protection Framework
> policy for secure enterprise browser
>
> **Platform:** Windows

:::image type="content" alt-text="Apps -- App protection policies - Create policy - Microsoft Intune Admin Center" source="./media/securing_data_edge_for_business9.png" lightbox="./media/securing_data_edge_for_business9.png":::

Once filled with the data select **Next.**

5. On the **Apps** \> select Select **Apps** \> **Microsoft Edge** and select
**Select**, after that select **Next*.

:::image type="content" alt-text="Apps -- App protection policies -- Create policy -- Select Apps -- Microsoft Intune Admin Center" source="./media/securing_data_edge_for_business10.png" lightbox="./media/securing_data_edge_for_business10.png":::

6. **Data Protection**

Following the recommendation from Level 3, configure this section with the following values \>. Then select **Next.**

:::image type="content" alt-text="Apps -- App protection policies -- Create policy -- Data Protection -- Microsoft Intune Admin Center" source="./media/securing_data_edge_for_business11.png" lightbox="./media/securing_data_edge_for_business11.png":::

7. **Health Check**.

Follow the recommendation from Level 3 Health Checks \> Once completed select **Next.**


:::image type="content" alt-text="Apps -- App protection policies -- Create policy -- Health Checks -- Microsoft Intune Admin Center" source="./media/securing_data_edge_for_business12.png" lightbox="./media/securing_data_edge_for_business12.png":::

8. **Scope Tags**:

Here you can create a new scope tag or select **Default. It's important to review it and select the proper scope tag for your environment and the roles that have access to the following policy.

You can create a new scope tag and call it **"Browser Config"**\>. Then select **Next.**

:::image type="content" alt-text="Apps -- App protection policies - Create policy -- Scope tags - Microsoft Intune Admin Center" source="./media/securing_data_edge_for_business13.png" lightbox="./media/securing_data_edge_for_business13.png":::

9. **Assignments**

Select on **Add Group** and select the desired group. For this example, select all VPN Users since they're BYOD type users. However, it's recommended to create a new group that will fit those browser config Users for **Level 3** \> Once you select the group you can select **Next.**

:::image type="content" alt-text="Apps -- App protection policies - Create policy -- Assignments - Microsoft Intune Admin Center" source="./media/securing_data_edge_for_business14.png" lightbox="./media/securing_data_edge_for_business14.png":::

10. **Review + create**.

Review each item and ensure the **level 3** configuration is correct. After you have reviewed it, \>, select **Next** to create the policy.

:::image type="content" alt-text="Apps -- App protection policies - Create policy -- Review + create - Microsoft Intune Admin Center" source="./media/securing_data_edge_for_business15.png" lightbox="./media/securing_data_edge_for_business15.png":::

We have now created our first MAM for Windows Policy and it should be available on the Admin Portal.

:::image type="content" alt-text="Policy Successfully created message - Microsoft Intune Admin Center" source="./media/securing_data_edge_for_business16.png" lightbox="./media/securing_data_edge_for_business16.png":::
