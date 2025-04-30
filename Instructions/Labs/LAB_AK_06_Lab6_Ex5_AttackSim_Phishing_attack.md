# Learning Path 6 - Lab 6 - Exercise 5 - Conduct a Spear Phishing attack using Attack Simulation training

## Lab scenario

Holly Dickson is concerned that some users at Adatum may require education about phishing attacks. As part of her pilot project, Holly has decided to use the Microsoft 365 Attack simulation training feature to determine her users' susceptibility to phishing attacks.


### Task 1: Enable Multifactor Authentication for the Global Admin

>**Important:** To implement MFA, you will need to use your mobile phone to receive a verification code so that you can enter it into your tenant as a second form of authentication. If you do not have a phone, you will have to skip this lab. If this is the case, notify your instructor, who can potentially partner you with another student to follow along through this lab.

1. On LON-CL1, in your Edge browser, you should still be logged into Microsoft 365 as **Holly Dickson**.  

1. To enable MFA for Holly Dickson's user account, select the **Microsoft 365 admin center** tab in your browser, and then in the left hand-navigation pane, select **Users** and then select **Active users**.

1. In the **Active users** window, on the menu bar at the top of the user list, select **Multi-factor authentication**. If this option does not appear on the menu bar, select the **ellipsis (More actions)** icon, and in the drop-down menu that appears, select  **Multi-factor authentication**.

	![](../Images/ms-102-103.png)

1. A **Configure multifactor authentication (MFA)** window appears in a new Edge browser tab. Below the paragraph of text at the top of the page is an Information box that displays the message **Not what you're looking for? To configure MFA on an individual per-users level, select Legacy per-user MFA.** Select the **Legacy per-user MFA** link in this message. 

	![](../Images/mfa1.png)

1. On the **multi-factor authentication** page that appears, the **users** tab at the top of the page is displayed by default. Note the MFA status for all existing user accounts is **Disabled**. 

	![](../Images/mfa2.png)

1. Select the check box for **Holly Dickson**, select **Enable MFA** from the top-menu bar.

	>**Tip:** There are so many users, select the view dropdown, select **Global administrators**, now you can see **Holly Dickson** account.

1. On the **Enable multifactor authentication** dialog box that appears, select the **Enable** button. 

1. When the **Updates successful** dialog box appears, select **close**. In the **multi-factor authentication** window, verify Holly's MFA Status has changed to **Enabled**. Close the **Multi-factor authentication** tab in your Edge browser. This should return you to the **Microsoft 365 admin center** tab.

1. You must now sign out of Microsoft 365 as Holly, close your browser session (to clear cache), open a new session, and then log back in as Holly using MFA. The first time you sign back in after having MFA enabled for your user account, you will be asked for the authentication information needed for MFA, such as your phone number and authentication options. You will then be texted a verification code to validate the authentication process works. You will perform these steps in the remaining portion of this task. You must begin by signing out of Microsoft 365 as Holly, so select the **HD** user icon in the upper right corner of the browser and in the **Holly Dickson** window that appears, select **Sign out**. 

1. Once you are signed out, close all the browser tabs. This will close your Edge browser.

1. Select the **Edge** icon on your taskbar to open a new browser session. In your browser go to the **Microsoft Office Home** page by entering the following URL in the address bar: **https://portal.office.com/** 

1. In the **Pick an account** window, select **Holly**'s account and then select **Next**. In the **Enter password** window, enter **<inject key="AzureAdUserPassword"></inject>** and select **Sign in**.

1. Because MFA is enabled for Holly, a **Action Required** window appears. Select **Next**.

	![](../Images/actionrequired.png)

1. On the **Microsoft Authenticator** page, you have to install the Microsoft Authenticator app in your phone. Select **Next**, on the **Start by getting the app** page. On **Set up your account** page, select **Next**. 

	![](../Images/mfa3.png)

1. On **Set up your account** page, select **Next**.

1. On **Scan the QR code**, first scan the code from your phone using Authenticator app, after scanning select **Next**, on the **Scan the QR code** page. On **Let's try it out** page, enter the code in your phone, after entering the code as you can see the **Notification approved** message, select **Next**.

	![](../Images/mfa4.png)

1. In the **Phone** window that appears, under **What phone number would you like to use?** field, select your country or region, and then in the field next to it, enter your phone number (use your country specific formatting). Verify the **Receive a code** option is selected and then select **Next**.

1. Retrieve the verification code from the text message that is sent to your phone.

1. In the **Phone** window, enter the 6-digit verification code in the code field and then select **Next**. When the Phone window displays a message indicating your phone was registered successfully, select **Next**.

1. Once it shows the **Verification complete. Your phone has been registered.**, select **Next**.

	![](../Images/mfa5.png)

1. On the **Success!** page, select **Done**.

1. If a **Stay signed in?** dialog box appears, select the **Don’t show this again** check box and then select **Yes.** 

1. On the **Microsoft Office Home** tab, select the **Admin** icon that appears in the column of app icons on the left-side of the screen. This opens the **Microsoft 365 admin center** in a new browser tab. This will prepare you for the next lab exercise when you disable MFA for Holly Dickson after completing the Attack simulation training.

1. In the **Microsoft 365 admin center**, select **Show all** in the navigation pane. Under **Admin centers**, select **Security**. This will open the **Microsoft 365 Defender** portal. You will resume from here in the next task when you launch a spear phishing attack using Attack simulation training.  

1. You have now configured MFA for Holly Dickson, you have signed into the **Office 365** portal as Holly using MFA, you have opened the Microsoft 365 admin center for future labs, and you are ready to run the Attack simulator training in the Microsoft 365 Defender portal. Leave everything as is in your VM and proceed to the next task.


### Task 2: Configure and launch a Spear Phishing attack

Microsoft 365 includes an Attack simulation training feature that enables you to create simulations and run them against all your users or a select group of users. Each phishing attack includes what is referred to as the "payload", which is the message in the system-generated email that contains the malicious component hackers use to gather information, deposit malicious code, and so on. The Attack simulation training feature includes a number of payload templates that you can choose from, and you can create your own payload if you so desire.

In this lab exercise, you will use one of the existing payload templates. In the next lab exercise, you will create your own custom payload.

1. On LON-CL1, in your Edge browser, you should still be logged into Microsoft 365 as Holly Dickson.

1. You should still have the Microsoft Defender portal open in your Edge browser from the prior task. If not, enter https://security.microsoft.com in the address bar, and then if you receive a dialog box asking for a second form of authentication, proceed through the verification process. If not, sign-in as Holly using the Administrative username and Administrative password provided by your lab-hosting provider and if required, complete the MFA sign-in process.

1. In the **Microsoft 365 Defender** portal, under the **Email & collaboration** section in the left-hand navigation pane, select **Attack simulation training**. If a **Welcome to Attack simulation training** window appears, select **Close**.

1. On the **Attack simulation training** page, Holly has decided to conduct a simulated account breach in which she will use a URL to try and obtain usernames and passwords. This is referred to in the Attack Simulator as a **Credentials Harvest** attack. 

	>**Note:** Notice the tabs that appear across the top of the **Attack simulation training** page (where the **Overview** tab is displayed by default).You can launch this attack either from **Simulations** tab by selecting the **+ Launch a simulation**. Since the **Overview** tab has additional information and is the default page when selecting the **Attack simulation training** service, it is recommended that you launch it from there so that you can learn about the specifics of this type of attack. 
	
1. On the **Overview** tab, scroll down to the **Recommendations** section. Under the **Launch a phishing simulation using other social engineering techniques** recommendation, select **Create another simulation with new technique**. This initiates the **Create Simulation** wizard.

	![](../Images/ms-102-104.png)

1. On the **Select technique** page, review the specific information related to the **Credentials Harvest** attack type option. At the bottom of the **Credential Harvest** option, select the **View details of Credential harvest** link. This opens a **Credential Harvest** pane on the right. Review the **Description** and the **Simulation steps** for this type of attack. When you're done, close the **Credential Harvest** pane.

1. On the **Select Technique** page, select the **Credentials Harvest** attack type if it's not already selected by default, and then select **Next**.

1. In the **Simulation** wizard, the steps involved in the simulation are displayed in the left-hand pane. While you can manually create a phishing campaign, it is recommended that you take advantage of the available templates that will prefill most of the information for you. The key to a successful phishing attack is to create a very intriguing, real-world looking email, and the templates provide very creative solutions. 

	On the **Name Simulation** page, provide the following information: 
	- Simulation Name: **PhishingTest1**
	- Description: **This simulation provides insight on targeted email threats against users inside the company**

1. Select **Next**.

1. On the **Select payload and login page** window, select the check box to the left of the **Payment for Package** payload. Select **Next**.

    >**Note:** If the Payment for Package payload does not appear, select another Payload of your choice. A payload is the link or attachment in the simulated phishing email message that's presented to users. In the real-world, you'd want to use a payload that works best for your organization.

1. On the **Target Users** page, select the **Include all users in my organization** option. This will display all of Adatum's users. Select **Next**, and then on the **Exclude users** page, select **Next** again.

1. On the **Assign Training** page, under the **Preferences** section, the **Assign training for me (Recommended)** option should be selected by default (if not, select it). Select the **Due Date** field. In the drop-down menu that appears, select **7 days after Simulation ends** and then select **Next**.

1. On the **Select Phish landing page** window, the **Global landing pages** tab should be displayed by default. This tab displays a list of predefined landing page templates. Select the **Microsoft Landing Page Template 1** name to preview the page. 

1. A preview of the **Microsoft landing page** for this template appears in a new pane. This preview pane provides an example of what the landing page will look like when someone experiences a phishing attack and the simulation uses **Microsoft Landing Page Template 1**. Scroll down through this preview panel and review the features. When you're finished, select the **Close** button at the bottom of the preview pane. 

1. You will now look at some of the other landing page templates until you find one that you want to use for this simulation. On the **Select Phish landing page** window, select one of the other templates (select the name of the template and not its checkbox). Examine the preview pane and note how the landing page for this template is different from **Microsoft Landing Page Template 1**. When you're finished, select the **Close** button at the bottom of the preview pane.

1. Repeat the prior step and select another template. Note how this template is different from the other two you looked at. 

1. Repeat this step as many times as you would like until you find a template that you want to use for this simulation. When you're finished reviewing templates, select the checkbox for the template that you want to use on the **Select Phish landing page** and then select **Next**.

1. On the **Select end user notification** page, choose how you want the end user to be notified. For the purpose of this lab, select **Microsoft default notification (recommended)**. In the list of notifications that appears, configure the following notifications:

	 - Microsoft default positive reinforcement notification - set **Delivery preferences** to **Deliver after simulation ends**
	 - Microsoft default training reminder notification - set **Delivery preferences** to  **Weekly**

1. Select **Next**.

1. On the **Launch Details** page, select the **Launch this simulation as soon as I'm done** option and then select **Next**.

1. On the **Review Simulation** page, review the entered information. If anything needs to be changed, select the appropriate **Edit** option to make the change. Once everything is correct, select **Submit**. It may take a few minutes before you receive a confirmation stating **Simulation has been scheduled for launch**. Select **Done**.


### Task 3: Review the attack simulation results

1. Switch to **LON-CL2**, where you should be logged into the machine as the local **adatum\administrator** account.

1. In Lynne's Outlook Inbox, you should see the spear phishing email that was sent by the Attack Simulator. The subject of the message should be **Payment for Package**. Select the email to open it and review the details in the body of the message. 

     >**NOTE:** It can take up to 15 minutes for the email to arrive.  Wait for the email before proceeding. In the email, note the message that appears. Again, the message may vary depending on the payload you selected when setting up the spear phishing simulation. For example, it may say something like: **Our server has detected some errors delivering 2 new message to your Inbox due to the synchronization delay. Click on View Returned Messages below to retrieve these messages.** Regardless of the exact message, keep in mind that its purpose is to trick the user into thinking this is a legitimate email, when in fact, it's a spear phishing attack.

1. Select the **Pay Now** button in the email. Even though you know this is a spear phishing attack, this will enable you to see the effect of doing so in the Attack Simulator report that tracks the results of the spear phishing campaign.

1. In the **Sign in** dialog box that appears, enter **lynne.robbins@otuwamoc101832.onmicrosoft.com**' as username, and then enter the password as **<inject key="AzureAdUserPassword"></inject>** in the **Enter password** window. Select **Sign in**. 

1. This displays a web page that explains how you have been redirected to it as part of a Phishing awareness test being run by your organization. Read through the contents of this site, which uses the landing page template that you selected in the prior task when setting up the attack simulation.

	![](../Images/ms-102-105.png)

1. Leave the Outlook tab open for Lynne's mailbox in your Edge browser. Do **NOT** sign out or close it. You will access Lynne's mailbox on LON-CL2 in the next lab exercise. 

1. Switch back to **LON-CL1**.

1. In LON-CL1, in your Edge browser session where you are logged in as Holly Dickson, you should still be on the **Attack simulation training** page. If the **PhishingTest1** simulation does not appear in the **Recent Simulations** list, select the **Refresh** icon to the left of the URL on the address bar. The **PhishingTest1** simulation should now appear. Select the **PhishingTest1** simulation to view the diagnostic results that were captured for this simulation.

1. A **PhishingTest1** page should appear. Review all the information collected for this simulated attack. When you're finished, select the **X** in the upper right-hand corner of the window to close it. 

1. Leave your browser open in LON-CL1 and do not close any of the tabs.

## Review

In this lab, you have:

- Enabled Multifactor Authentication for the Global Admin.
- Configured and launch a Spear Phishing attack.
- Reviewed the attack simulation results.

## The lab has been completed successfully. Click **Next >>** to proceed to the next exercise.
