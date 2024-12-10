# Learning Path 6 - Lab 6 - Exercise 3 - Implement SharePoint Permission Alert

## Lab scenario

In this exercise you will configure and test an alert that notifies Lynne Robbins when a user is added as a site collection administrator for a SharePoint site collection.

### Task 1 – Create a SharePoint Permissions Alert

1. At the end of the prior lab, you were logged into LON-CL2. This lab will use LON-CL1. Switch to **LON-CL1**.

2. On **LON-CL1**, in your Edge browser, you should still be logged into Microsoft 365 as **Holly Dickson**. In your Edge browser, select the **Alert policy - Microsoft 365 security** tab, which displays the **Microsoft 365 Defender** portal.

3. In the **Microsoft 365 Defender** tab, you should still be in the **Alert policy** window from the prior lab exercise (if not, then in the left-hand navigation pane, select **Policies & rules** and then select **Alert policy**).

4. In the **Alert policy** window, select **+ New Alert Policy** on the menu bar. This initiates the **New Alert Policy** wizard.

5. On the **Name your alert, categorize it, and choose a severity** window, enter the following information:

	- Name: **Add user as a site collection administrator**

	- Description: **This alert notifies Lynne Robbins when a user is added to the site collection administrators on a SharePoint site collection.**

	- Severity: **Medium**

	- Category: **Permissions**

6. Select **Next**.

7. On the **Choose an activity, conditions and when to trigger the alert** window, enter the following information:

	- Activity is: select the **Select an activity** field, then in the menu that appears, scroll down to the **Site administration activities** section and select **Added site collection admin**

	- How do you want the alert to be triggered? **Every time an activity matches the rule**

8. Select **Next**.

9. On the **Decide if you want to notify people when this alert is triggered** window, enter the following information:

	- Email recipients: Remove **Holly Dickson** and add **Lynne Robbins**

	- Daily notification limit: **No limit**

10. Select **Next**.

11. On the **Review your settings** page, under the **Do you want to turn the policy on right away?** option, select **Yes, turn it on right away** and then select **Submit**. 

12. On the **New Alert Policy** window, select **Done**.

13. Verify your new alert policy appears in the list on the **Alert policy** page, its **Type** is set to **Custom**, and its **Status** in **On**.

14. Leave all the Edge browser tabs open for the next task.

You have now configured an additional alert policy that monitors when a user is added as a site collection administrator for a SharePoint Online site collection.

### Task 2 – Validate the  SharePoint Permissions Alert

>**Note:** This task is currently read-only because alert emails intended for Lynne's inbox are not appearing. This issue originates from Microsoft's end, and we are actively working to resolve it.

In the prior task, you configured an alert designed to notify Lynne Robbins when a user is added as a site collection administrator for a site collection. In this task, you will test this alert by adding Alex Wilber as a site collection admin to the global SharePoint Communication site. This activity should trigger the alert policy that you created, which should send an alert notification email to Lynne Robbins’ mailbox.

1. On LON-CL1, in your Edge browser, you should still be logged into Microsoft 365 as **Holly Dickson**. 

1. In your **Microsoft Edge** browser, open a new tab and enter the following URL in the address bar: **https://otuwamocZZZZZZ.sharepoint.com/_layouts/15/settings.aspx (replace ZZZZZZ with the tenant prefix provided by your lab hosting provider)**. This opens the **Site Settings** for the global SharePoint Communication site.

1. On the **Site Settings** window, under the **Users and Permissions** section, select **Site permissions**. 

1. In the ribbon at the top of the page, the **Permissions** tab is displayed by default. Under the **Manage** drop-down, select **Site Collection Administrators**.

	![](../Images/sitecollection.png)

1. In the **Site Collection Administrators** dialog box, the Global administrator account that was assigned by default to this role group is displayed in the data entry field. To the right of this account, enter **Alex**, select **Alex Wilber** from the list of users that appears, and then select **OK**. 

1. Once the email arrives in Lynne's Inbox, open the email and review the contents. Scroll to the bottom of the email and select the **View alert details** button. This opens the **Microsoft 365 Defender** portal in a new tab.

	>**Note:** If you are unable to login to outlook, then we need to assign assign Microsoft 365 Business Premium license. To assign the license please follow the below steps.

   	- i. Go to **Microsoft 365 admin center** tab, from the left pane select **Users** then **Active users**. Select **Lynne Robbins** from the list.
 
   	- ii. Select **Licenses and apps**, then **Microsoft 365 Business Premium** and click on **Save changes**.

   >**Note:** It takes up to 24 hours after creating or updating an alert policy before alerts can be triggered by the policy. This is because the policy has to be synced to the alert detection engine.

1. Once the email arrives in Lynne's Inbox, open the email and review the contents. Scroll to the bottom of the email and select the **View alert details** button. This opens the **Microsoft 365 Defender** portal in a new tab.

1. The **Microsoft 365 Defender** portal displays the **Alerts** window, and it automatically opens the **Site collection admin permissions** pane for this alert activity that triggered the email notification to Lynne. <br/>

	Scroll down through the **Site collection admin permissions** pane and review all the information for this alert activity. When you are done, select **Close** to close the pane.

1. Leave your LON-CL1 and LON-CL2 VMs open for the remaining exercise in this lab.

You have now successfully tested the SharePoint alert to monitor site collection admin permissions on SharePoint sites.  

## Review

In this lab, you have:

- Created a SharePoint Permissions Alert.
- Validated the  SharePoint Permissions Alert.

## Proceed to the next exercise.
