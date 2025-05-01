# Learning Path 4 - Lab 4 - Exercise 3 - PIM Self-Approval

## Lab scenario

Since taking on her role as Adatum's Microsoft 365 Administrator, Holly Dickson has been interrupted on several occasions with user support requests that have taken her attention away from the company's Microsoft 365 pilot project. Because Holly does not have the bandwidth to respond to the requests in a timely manner, she wants Alex Wilber and Joni Sherman to begin responding to these requests. This will require that Alex and Joni have Helpdesk Administrator role permissions.  However, Holly does not want to permanently assign this role to Alex and Joni, since this is not their regular role, and she doesn't want this role to impact other services. Holly also doesn't want Alex and Joni to submit approval requests each time they need to be assigned the Helpdesk Admin role.

Given these requirements, Holly wants to take advantage of the Privileged Identity Management (PIM) feature that enables users to self-activate an Microsoft Entra role on an as-needed basis. Instead of requiring a Global admin (such as Holly) or a Privileged Role Administrator to assign a role to multiple people individually, PIM enables an organization to create a security group and then enable the group to be eligible for that specific role. When people are assigned as members of the group, they indirectly become eligible to be assigned the role. Holly wants to employ this feature at Adatum by creating a security group of eligible users (Alex and Joni) for the Helpdesk administrator role. This opportunity will be a good test of this feature in Holly's pilot project.

Once Alex and Joni are made eligible for this role, whenever they must respond to their first user request, they will self-activate, or self-approve the role assignment. By doing so, they will have Helpdesk administrator control for a predetermined time period. In this case, Holly wants them to remain assigned to the role for 15 days. 

In addition, Holly doesn't want to be forced to approve the role assignment whenever Alex and Joni require this role assignment. Instead, Holly simply wants to be notified whenever Alex or Joni self-approve the role. PIM can send email notifications to selected individuals when important events occur in their Azure Active Directory organization, such as when a role is assigned or activated.  


### Task 1 - Create an eligible group for the Helpdesk Admin role

In this task, you will create a group that is eligible to be assigned the Helpdesk Admin role, allowing users within this group to perform Helpdesk administrative tasks.

1. You should still be logged into **LON-CL1** and in your Edge browser, you should still be logged into Microsoft 365 as Holly Dickson.

1. In your Edge browser, select the tab containing the **Microsoft Entra admin center**, which should still be open from the prior lab exercise. 

1. In the **Microsoft Entra admin center**, in the left-hand navigation pane, under **Identity (1)**, select **Groups (2)** and then select **All groups (3)**.

    ![](../Images/L4E2T1S3.png)

1. In the **Groups | All groups** window, select **New group** in the menu bar.

    ![](../Images/L4E2T1S4.png)

1. In the **New group** window, enter the following information:

    - Group type - **Security (1)**

    - Group name - **PIM-Helpdesk-Administrators (2)**

    - Group description - **Group of eligible users who can be assigned to the Helpdesk Administrator role in PIM (3)**

    - Microsoft Entra roles can be assigned to the group - **Yes (4)**

    - Membership type - **Assigned (5)**

    - Owners - Select **No owners selected**. In the **Add owners** pane, enter **Holly@otuwamocZZZZZZ.onmicrosoft.com (6)** in the **Search** field and select the **Holly**'s user account.

    - Members - Select **No members selected (7)**. In the **Add members** pane, Enter **Alex** in the search field and then select **Alex Wilber**. Enter **Joni** in the Search field, and then select **Joni Sherman**.

     - In the **New group** window, select the **Create (8)** button at the bottom of the page.

          ![](../Images/L4E2T1S6.png)

          >**Note:** For example, in **odl_user_@otuwamocZZZZZZ.onmicrosoft.com**, the highlighted portion **(otuwamocZZZZZZ.onmicrosoft.com)** represents the domain name or tenant prefix, which you can replace with your desired tenant prefix.

1. A dialog box appears at the top of the page that says: **Creating a group to which Microsoft Entra roles can be assigned is a setting that cannot be changed later. Are you sure that you want to add this capability?**. Select **Yes**.

     ![](../Images/L4E2T1S7.png)

1. In the **Groups | All groups** window, if the **PIM-Helpdesk-Administrators** group does not appear, click **Refresh** on the menu bar.

     ![](../Images/L4E2T1S8.png)

1. You must now make the **PIM-Helpdesk-Administrators** group eligible for role assignment. In the left-hand navigation pane, select **Identity Governance (1)** to expand the section, and then select **Privileged Identity Management (2)**.

     ![](../Images/ms-102-92.png)

1. In the **Privileged Identity Management | Quick start** window, in the middle pane under the **Manage** section, select **Microsoft Entra roles**.

     ![](../Images/L4E2T1S10.png)

1. In the **Adatum Corporation | Quick start** window, under the **Assign** section, select the **Assign Eligibility** button.

     ![](../Images/L4E2T1S11.png)

1. In the **Adatum Corporation | Roles (1)** window, scroll down through the list of roles and select **Helpdesk Administrator (2)**.

     ![](../Images/L4E2T1S12.png)

1. In the **Helpdesk Administrator | Assignments** window, select **+ Add assignments** on the menu bar. 

     ![](../Images/L4E2T1S13.png)

1. In the **Add assignments** window, the **Membership** tab is displayed by default. Under **Select member(s)**, select **No member selected (1)**.

1. In the **Select a member** pane that appears on the right, enter **PIM (2)** in the **Search** field. This will display the list of eligible users and groups whose name starts with **PIM**. Select the **PIM-Helpdesk-Administrators (3)** group that appears, and then select the **Select (4)** button.

     ![](../Images/L4E2T1S15.png)

1. In the **Add assignments** window, select **Next >** (this does the same thing as selecting the **Setting** tab). 

     ![](../Images/L4E2T1S16.png)

1. In the **Add assignments** window, under the **Setting** tab, verify the **Assignment type** option is set to **Eligible**. Also verify the **Permanently eligible** check box is selected (if not, then do so now), and then select **Assign**. 

1. In the **Helpdesk Administrator | Assignments** window, note that the **PIM-Helpdesk-Administrators** group is an eligible assignment to the Helpdesk Administrator role. Because **PIM-Helpdesk-Administrators** is a group, it means that all members of this group (which consists of Alex Wilber and Joni Sherman) are now eligible to be assigned the Helpdesk Administrator role.

     ![](../Images/L4E2T1S18.png)

    >**Note:** Lab testing has shown that it can sometimes take up to 30 minutes for new assignments to appear under the **Eligible assignments** tab. If **PIM-Helpdesk-Administrators** doesn't appear immediately, wait a few minutes and then select the **Refresh** option on the menu bar. Continue to select the **Refresh** option every few minutes until **PIM-Helpdesk-Administrators** appears in the list of **Eligible assignments**.
   
1. Leave all browser tabs open for the next task.

### Task 2 - Configure the Helpdesk Administrator role for self-activation

In this task, you will configure the Helpdesk Administrator role to allow users to activate it themselves through self-service.

Next, Holly wants to configure the Helpdesk administrator role settings and notification settings in Microsoft Entra ID. Privileged Identity Management (PIM) lets you know when important events occur in your Microsoft Entra ID organization, such as when a role is assigned or activated. PIM keeps you informed by sending you and other participants email notifications. These emails can also include links to relevant tasks, such activating or renewing a role. In this task, Holly wants to update the notifications to ensure that self-approvals are tracked in real-time in a proactive manner.

In the prior lab exercise involving the Global administrator role, Holly updated the role so that she had to approve any activation requests for the role. However, for the Helpdesk admin role, Holly is less concerned about eligible users abusing the role permissions given the more limited scope of the role as compared to the Global Admin role. Holly trusts that Alex and Joni won't activate the role unless they're required to do so to respond to support requests. Therefore, Holly will only require that Alex and Joni provide justification whenever they must activate the role. Holly wants the role to be active for Alex and Joni for 15 days. This way, they won't be waiting for Holly to approve their activation requests, and they can simply provide justification and get started whenever they must take on this role.

1. On **LON-CL1**, in your Edge browser, you should still be logged into Microsoft 365 as Holly Dickson from the prior task.

2. In your browser, you should still have the **Microsoft Entra admin center** open from the prior task. In the left-hand navigation pane, under the **Identity Governance** section, select **Privileged Identity Management**.

3. In the **Privileged Identity Management | Quick start** window, in the middle pane under the **Manage** section, select **Microsoft Entra roles**.

4. In the **Adatum Corporation | Quick start** window, in the middle pane under the **Manage** section, select **Settings**. 

5. In the **Adatum Corporation | Settings** window, select the **Helpdesk Administrator** role.

    **>Tip:** If the roles are not displayed in alphabetical order, select the **Role** heading to sort them in ascending alphabetical order. This will make it easier to locate the Helpdesk administrator role.

6. In the **Role setting details -  Helpdesk Administrator** window, scroll through the page and review the information for role activation, assignment, and notification. Then select **Edit** on the menu bar at the top of the page.

7. In the **Edit role setting - Helpdesk Administrator** window, the **Activation** tab is displayed by default. In this tab, the slider for the **Activation maximum duration (hours)** setting is set to **8**. Holly wants to increase this to the maximum allowable time, which is **24** hours. You can either move the slider to the end of the line, or you can type **24** in the field next to the slider. 

    >**Note:** If you try to enter any value greater than 24, it will automatically reset to 24.

8. Below the activation slider, set the **On activation, require** setting to **None**.

    >**Note:** In the prior lab exercise, Holly required that Patti Fernandez sign in using Microsoft Entra MFA when she requested activation of the Global admin role. In doing so, Holly verified the Microsoft Enrtra MFA sign-in worked. However, for the purpose of the pilot project, Holly will not require verification using multi-factor authentication when activating the Helpdesk administrator role (and since you already tested this MFA feature in the prior lab exercise, there's no reason to take time in class to do it again). 

9. The screen then displays a group of three settings, each with a check box. Verify that all three check boxes are blank. If any check box is selected by default, then un-check (clear) it now. 

    >**Note:** For the pilot project, Holly does not want the **Require justification on activation** check box selected. Holly knows that Alex and Joni will only activate the role when needed, so she doesn't require a justification from them to activate the role assignment (however, in the next step, Holly will require justification when they assign the role to themselves). Leaving the **Require approval to activate** setting unchecked will enable an eligible user to self-approve, or self-activate without requiring another user's approval.

10. You're currently in the **Activation** tab. Select the **Next: Assignment**. When this role is assigned to Alex or Joni, Holly wants the assignment to expire after 15 days. To implement this requirement, configure the following settings on this tab:

    - Uncheck (clear) the **Allow permanent active assignment** check box. Then select the **Expire active assignments after** field, and in the drop-down menu that appears, select **15 days**.

    - Verify the **Require justification on active assignment** check box is selected (if not, select it now).

11. Select the **Next: Notification**.

12. On the **Notification** tab, note the three activities that can trigger a notification being sent: **Send notifications when...**

    - members are assigned as eligible to this role
    - members are assigned as active to this role
    - eligible members activate this role
    - Under the **Send notifications when eligible members activate this role (1)** section, Holly wants to be notified when Alex or Joni self-approve this role. Therefore:

    - Verify the **Role activation alert** check box is selected.
    - The default recipient for the **Role activation alert** is **Admin**. This refers to the Global Administrators (Holly) and any Privileged Role Administrators. 
    - Un-check (clear) the **Notification to activated user (requestor)**. Since Alex and Joni will be self-approving, they don't need to receive a notification when they do so.

13. Select the **Update (2)** button at the bottom of the window.

     ![](../Images/ms-102-93.png)

14. Leave all browser tabs open for the next task.

### Task 3 - Self-activate the Helpdesk Admin role

In this task, you will activate the Helpdesk Admin role for yourself through self-service, enabling you to take on the administrative responsibilities associated with this role.

At this point in Holly's pilot project, the PIM-Helpdesk-Administrators group has been made eligible for the Helpdesk administrator role. The members of the group (Alex Wilber and Joni Sherman) can now be assigned the Helpdesk Administrator role using Microsoft Entra Privileged Identity Management. Holly wants to test out the PIM process in her pilot project. In this task, you will take on the role of Alex Wilber, who will submit a request to self-approve assigning the Helpdesk Administrator role to his user account.

1. In LON-CL1, right-click on the **Edge** icon on the taskbar and in the menu that appears, select **New InPrivate window**. 

2. In your InPrivate browsing session, enter the following URL in the address bar: **[Azure Portal](https://portal.azure.com)**

3. You're now going to log into Azure as Alex Wilber. In the **Sign in** window, enter the username as **alex.wilber@otuwamocZZZZZZ.onmicrosoft.com** and then select **Next**. In the **Enter password** window, enter the **<inject key="AzureAdUserPassword"></inject>** and then select **Sign in**. In the **Stay signed in?** dialog box, select the **Don't show this again** check box and then select **Yes**.

     >**Note:** For example, in **odl_user_@otuwamocZZZZZZ.onmicrosoft.com**, the highlighted portion **(otuwamocZZZZZZ.onmicrosoft.com)** represents the domain name or tenant prefix, which you can replace with your desired tenant prefix.

4. In the **Welcome to Microsoft Azure** dialog box that appears, select **Maybe later** to skip the tour.

5. In the **Microsoft Azure** portal, in the middle of the screen is the section of **Azure services**. This section displays a row of Azure services and their associated icons. At the end of the row, select **More services** (with the forward arrow icon). This opens the **All services** window.

6. In the **All services** window, enter **Privileged** in the **Filter services** search box at the top of the page. In the list of search results, select **Microsoft Entra Privileged Identity Management**.

7. In the **Privileged Identity Management | Quick start** window, in the **Tasks** section in the left-hand navigation pane, select **My Roles**.

8. In the **My roles | Microsoft Entra roles** window, the **Eligible assignments** tab is displayed by default. Remember, in the prior task Holly assigned Alex as a member of the **PIM-Helpdesk-Administrators** group, which Holly later assigned as an eligible group for the Helpdesk Administrator role. As such, this role appears in the list of **Eligible assignments** for Alex. Select the **Active assignments** tab. Note that no Microsoft Entra roles have yet to be assigned to Alex's account. 

9. Alex is now ready to self-approve, or self-activate the Helpdesk administrator role. Select the **Eligible assignments** tab. Under the **Action** column for the **Helpdesk Administrator** role, select **Activate**.

10. In the **Activate - Helpdesk Administrator** pane that appears, enter **Support requests from Sales team members that require resolution** in the **Reason** field. This is the reason why Alex wants to self-activate this role. Then select the **Activate** button at the bottom of the pane. Note the three stages of activation that appear in the **Activate - Helpdesk Administrator** pane and the progress made on each stage. Wait for all three stages to automatically complete (Stage 2 typically takes the longest). After the final stage is completed, the **Activate - Helpdesk Administrator** pane will automatically close, and you will be returned to the **My roles | Microsoft Entra roles** window.

11. On the **My roles | Microsoft Entra roles** window, note that you're still in the **Eligible assignments** tab. Also note the message at the top of the window indicating **Your active roles have changed. Click here to view your active roles**. Select this message. This simply displays the **Active assignments** tab, which you could have selected yourself instead of selecting the message. 

     ![](../Images/ms-102-94.png)

12. In the **Active assignments** tab, note the **Helpdesk Administrator** role now appears. Prior to activating this role, remember that you checked this tab earlier and no Microsoft Entra roles appeared. Now that Alex has self-approved the **Helpdesk Administrator** role, it's now been assigned to his user account. 

13. Close the InPrivate browser session. This should return you to the **Microsoft Entra admin center**, which should be displaying the **Adatum Corporation | Settings** page.

14. Leave your browser and all tabs open for the next task.

As Alex Wilber, you have now self-approved the Helpdesk Administrator role. This has automatically assigned the role to Alex's user account.


### Task 4 -  Verify a PIM notification was issued

In this task, you will check to ensure that a notification was sent through Privileged Identity Management (PIM) confirming the activation of the Helpdesk Admin role.

When you earlier configured the Helpdesk Administrator role, you set up the notification feature so that Holly would be notified any time an eligible user activated the role. Since Alex Wilber just self-activated the role, Holly should receive a notification of this activity. This task will verify that Holly received a notification.

1. On **LON-CL1**, in your Edge browser, you should still be logged into Microsoft 365 as Holly Dickson. In your Edge browser, select the **Home | Microsoft 365 Copilot** tab.

2. On the **Welcome to Microsoft 365 Copilot** page, select the **App Launcher (1)** on the left-side of the screen, select the **Outlook (2)** icon. This will open Outlook for Holly Dickson's mailbox in a new tab.

     ![](../Images/ms-102-95.png)

3. In Holly's Outlook mailbox, her **Inbox** is displayed by default. Verify that Holly received a PIM generated email indicating that **Alex Wilber activated the Helpdesk Administrator role for the Adatum Corporation Directory**. 

     ![](../Images/ms-102-96.png)

4. Select the email to open it. Review the information in the email and then close it. 

5. To review the audited list of activities related to Alex's self-approval of the Helpdesk Administrator role, select the **Microsoft Entra admin center** tab in your Edge browser. 

6. In the **Microsoft Entra admin center**, the **Adatum Corporation | Settings** page should be displayed. This is where you left off in the prior task. In the middle pane, under the **Activity** section towards the bottom of the page, select **Resource audit**.

7. In the **Adatum Corporation | Resource audit** page, review the list of PIM activities. Note the two most recent activities, which include Alex's request to be assigned to the Helpdesk Administrator role, and the completion of Alex's request. 

     ![](../Images/ms-102-97.png)

8. Leave your browser and all tabs open for the next task.

## Review

In this lab, you have:

- Created an eligible group for the Helpdesk Admin role.
- Configured the Helpdesk Administrator role for self-activation.
- Self-activated the Helpdesk Admin role.
- Verified a PIM notification was issued.

## The lab has been completed successfully. Click **Next >>** to proceed to the next exercise.