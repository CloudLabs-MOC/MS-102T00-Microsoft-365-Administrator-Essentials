# Learning Path 2 - Lab 2 - Exercise 1 - Manage Administration Delegation

## Lab scenario

In this exercise, you will continue in your role as Holly Dickson, Adatum's new Microsoft 365 Administrator. As part of Adatum's Microsoft 365 pilot project, you will manage administration delegation by assigning Microsoft 365 administrator roles to several of the Microsoft 365 user accounts that were created by your lab hosting provider. You will assign these roles using both the Microsoft 365 admin center and Windows PowerShell; this will give you the added experience of using PowerShell to perform these administrative functions. Once you have assigned Microsoft 365 admin roles to several of the existing user accounts, you will then test those assignments by verifying the users have the permissions to act in accordance with their roles. 

### Task 1 - Assign Delegated Administrators in the Microsoft 365 Admin Center 

1. On **LON-CL1**, in the **Microsoft 365 admin center** in your Edge browser, you should still be logged in as Holly Dickson from a prior lab exercise. In the left-hand navigation pane, select **Users** and then select **Active Users**. 

1. In the **Active users** list, select **Diego Siciliani**.  

	>**Note:** Select Diego’s name; do not select the check box to the left of his name. The check box is typically used for selecting multiple users when you want to perform one of the user-related actions on the menu bar that appears above the list of users, such as **Manage product licenses** and **Manage roles**. Selecting a user’s name opens a property pane specifically for that user.

1. In the **Diego Siciliani** pane that appears, the **Account** tab is displayed by default. In this tab, scroll down to the **Roles** section and select **Manage roles**. 

	![](../Images/deigosales.png)

1. In the **Manage admin roles** window, the **User (no admin center access)** option is currently selected by default. Now that you want to assign Diego an administrator role, select the **Admin center access (1)** option. This enables a list of commonly used admin roles for selection. 

1. Diego has been promoted to Billing Administrator, but since this role does not appear in the list of commonly used roles, scroll down and select **Show all by category (2)**. 

	![](../Images/ms-102-59.png)

1. In the list of roles that are sorted by category, scroll down to the **Other** category, select the **Billing Administrator (1)** check box, and then select **Save changes (2)**. Note the **Admin roles updated** message that appears at the top of the pane once the changes are saved.

	![](../Images/ms-102-60.png)

1. On the **Manage admin roles** window, select the **X** in the upper-right corner of the screen to close it. This returns you to the **Active users** list. 

1. In the **Active users** list, select **Lynne Robbins**. 

1. In the **Lynne Robbins** pane that appears, the **Account** tab is displayed by default. In this tab, scroll down to the **Roles** section and select **Manage roles**. 

1. In the **Manage admin roles** window, select the **Admin center access** option. This enables the list of commonly used admin roles for selection. 
 
1. In the list of commonly used admin roles, select the **User Administrator (1)** role and then select **Save changes (2)**.

	![](../Images/ms-102-61.png)

1. Close the **Manage admin roles** window once the message appears indicating Lynne's admin roles were updated. 

1. Remain logged into LON-CL1 and the Microsoft 365 admin center as Holly Dickson.

### Task 2 - Assign Delegated Administrators with Windows PowerShell  

1. On LON-CL1, select the **Windows PowerShell** icon on the taskbar that you left open from a prior lab. If you closed the PowerShell window, then open an elevated instance of it using the same instruction as before. 

1. Your PowerShell session should still be connected to Microsoft Graph PowerShell from the prior lab in which you recovered a deleted group using PowerShell. However, if you previously closed PowerShell and just reopened it, then import the Microsoft.Graph.Identity.DirectoryManagement sub-module using the steps from the prior lab exercise. 

1. To perform Microsoft 365 user maintenance tasks in Microsoft Graph PowerShell, you must first import the Microsoft.Graph.Users sub-module and request Read/Write permissions. To import this sub-module, type the following command at the command prompt and then press Enter: 

	```powershell
	Import-Module Microsoft.Graph.Users
	```
1. In the earlier lab exercise, you connected to Microsoft Graph and requested "Directory.ReadWrite.All" permissions to run the cmdlets that restored the deleted group. To update User and role objects in this task, Holly must now request Read/Write permissions for each object. To request these permissions, type the following command at the command prompt and then press Enter:  

	```powershell
	Connect-MgGraph -Scopes 'User.ReadWrite.All', 'RoleManagement.ReadWrite.Directory'
	```

1. In the **Pick an account** window that appears, select Holly Dickson's account, i.e. Holly@otuwamocZZZZZZ.onmicrosoft.com (where ZZZZZZ is the tenant prefix provided by your lab hosting provider), For the password, sign-in with the same **Microsoft 365 Tenant Password** 
	
	- Password:- <inject key="AzureAdUserPassword"></inject>

		>**Note:** For example, in **odl_user_<inject key="DeploymentID" enableCopy="false"/>@otuwamocZZZZZZ.onmicrosoft.com**, the highlighted portion (**otuwamocZZZZZZ.onmicrosoft.com**) represents the domain name or tenant prefix, which you can replace with your desired tenant prefix.

1. On the **Permissions requested** dialog box that appears, select the **Consent on behalf of your organization (1)** check box, and then select **Accept (2)**.

	![](../Images/ms-102-56.png)

1. Holly wants to assign **Patti Fernandez** to the **Service Support Administrator** role. To assign this role using Microsoft Graph PowerShell, you must first obtain the object ID of the Service Support Administrator role so that you can assign it to Patti. However, in Microsoft Graph PowerShell, you can only assign roles that have been "enabled". Enabled roles are roles that were either enabled from a role template, or they have already been assigned to users through PowerShell or the Microsoft 365 admin center.

1. To view all the enabled roles in Microsoft 365, enter the following command at the command prompt and then press Enter:
	
	```powershell
	Get-MgDirectoryRole
	```

	>**Note:** This command displays the roles that have been enabled thus far in Microsoft 365. If the Service Support Administrator role appeared in this list, you could proceed directly to step 13 to assign the role to Patti. However, since the Service Support Administrator is not included in this list of enabled roles, you must perform steps 8-12 to enable the role from its corresponding role template before you can assign Patti to the role in step 13. 

1. To enable a role in Microsoft Graph PowerShell, you must first locate its template to obtain the template's object ID. You need to know the template's object ID to enable the role from the template. To view the list of role templates along with their object ID and display name, type in the following command and then press Enter:

	```powershell
	Get-MgDirectoryRoleTemplate | Format-List Id, DisplayName  
	```

1. In the list of role templates, locate the template record for the **Service Support Administrator** role (as of this writing, it's the seventh role in the list). Highlight the **ID** for the **Service Support Administrator** template (for example, fe930be7-5e62-47db-91af-98c3a49a38b1) and press **Ctrl+C** to copy it to the clipboard (when you copy it, the highlight disappears).

1. You will now create a variable that captures the attributes for the Service Support Administrator template. When you type in the following command, press **Ctrl+V** to paste in the Service Support Administrator template ID that you copied to the clipboard in the prior step. At the command prompt, type the following command and press Enter: 

	```powershell
	$ServiceSupportRoleTemplate = @{ RoleTemplateID = "paste in template ID here" }
	```

	>**Note:** For example: $ServiceSupportRoleTemplate = @{ RoleTemplateID = "fe930be7-5e62-47db-91af-98c3a49a38b1" }

1. To verify the Service Support Administrator role has been enabled, type in the following command and press enter. This command will display the list of enabled role:  
			
	```powershell
	Get-MgDirectoryRole	
	```

	>**Note:** This command displays the object ID of the Service Support Administrator role, which you will later copy and paste in step 15 when assigning Patti to this role.

	![](../Images/adminroles.png)

1. To assign Patti Fernandez to the newly enabled Service Support Administrator role, you must first obtain the object ID for Patti's user account. To do so, type the following command and press Enter: 

	```powershell
	Get-MgUser | Format-List ID, DisplayName
	```

1. Now that you know the object ID of the recently enabled Service Support Administrator role and the object ID of Patti's user account, you can assign the role to Patti. Perform the following steps to complete this process: 

	- a. In the previous command, you displayed the list of active users. Highlight the **Id** for Patti's account and copy it (**Ctrl+C**) to the clipboard. The highlight disappears once it's copied to the clipboard.  

	- b. Run the following command that creates a variable containing the directory object for Patti's user account. When typing in this command, paste in (**Ctrl+V**) the ID that you just copied for Patti's user account. 

		```powershell
		$UserObject = @{ "@odata.id" = "https://graph.microsoft.com/v1.0/directoryObjects/paste Patti's user account ID here" }	
		```

		>**For example:** $UserObject = @{ "@odata.id" = "https://graph.microsoft.com/v1.0/directoryObjects/22fddbf7-42d2-4698-be65-ebc972a023e3" }

	- c. In step 12, you displayed the list of enabled roles. Highlight the ID for the Service Support Administrator role and copy it (**Ctrl+C**) to the clipboard. 

	- d. Run the following command that assigns the variable containing Patti's user account ($UserObject) to the directory role. When typing in this command, paste in (**Ctrl+V**) the ID that you just copied for for the Service Support Administrator role.  

		```powershell
		New-MgDirectoryRoleMemberByRef -DirectoryRoleId 'paste the ID of the role here' -BodyParameter $UserObject
		```
				
1. You now want to verify that Patti has been assigned to the Service Support Administrator role. You previously copied the Object ID of this role to the clipboard, and you pasted it in the prior command. You should paste it into this command as well. Type the following command and press Enter:
	
	```powershell
	Get-MgDirectoryRoleMember -DirectoryRoleId 'paste the ID of the role here'
	``` 

	![](../Images/ms-102-62.png)
				
1. The prior command only displays the IDs of the users assigned to the selected role. However, you can match the ID that's displayed with Patti's ID to verify that her account has been assigned the **Service Support Administrator** role. As you can see, Patti is the only user assigned to the role.

	![](../Images/ms-102-63.png)

1. Let's now repeat this process to see all the users assigned to the Global Administrator role. Repeat step 15 to verify how many Adatum users have been assigned to the **Global Administrator** role. To complete this command, you must first copy (**Ctrl+C**) the ID of the Global Administrator role to the clipboard. You can find this ID in the list of enabled roles when you ran step 12. 

	>**Warning:** Copy the ID of the Global Administrator role and NOT the ID of the Global Administrator role template.

1. Verify there are multiple Adatum users who've been assigned the Global Administrator role. In a real-world scenario, the Microsoft 365 Administrator would use this PowerShell command to monitor how many global admins exist in their Microsoft 365 deployment. They would then remove the Global Administrator role from any users who truly shouldn't have it (remember, the best practice guideline is to have between 2 to 4 global admins in a Microsoft 365 deployment, depending on the size of the organization).  

	![](../Images/globaladmin.png)

1. In the case of this lab, while your lab hosting provider assigned the Global Administrator role to users other than the ODL user (and you assigned it to Holly Dickson), you'll leave these users as is. In this fictitious Adatum deployment, there's no point in wasting your time removing this role from their accounts. Plus, some of the future lab tasks are based on these users being assigned the Global Administrator role. 

	>**IMPORTANT:** Just remember that in your real-world deployment, the Microsoft 365 Administrator should monitor the Global Administrator role on a periodic basis to keep the number of assigned users between 2 and 4.
	
1. Leave your Windows PowerShell session open for future lab exercises, but minimize it before going on to the next task.


### Task 3 - Verify Delegated Administration  

In this task, you will begin by examining the administrative properties of two users, Joni Sherman and Lynne Robbins. You will then log into the Microsoft 365 home page on the Client 2 VM (LON-CL2) as each user to confirm several of the changes that you made when managing their administrative delegation in the prior tasks. Finally, as Lynne Robbins, you will perform two important user account maintenance tasks - resetting passwords and blocking user accounts.

1. On LON-CL1, you should still be logged into the Microsoft 365 admin center as Holly Dickson.

1. In the **Microsoft 365 admin center**, if you are not displaying the **Active Users**, then navigate to that page now.  

1. In the **Active users** list, select **Joni Sherman**. 

1. In the **Joni Sherman** properties window, the **Account** tab is displayed by default. Under the **Roles** section, it should indicate that Joni has **No administrator access**. Select the **X** in the upper right corner to close Joni's properties window.

	![](../Images/ms-102-64.png)

1. In the **Active users** list, select **Lynne Robbins**. 

1. In **Lynne Robbins's** properties window, it should indicate that Lynne has been assigned the **User Administrator** role. Close Lynne's properties window.

	![](../Images/lynne.png)

1. From the top-menu drop-down, and on the **Connect to LON-CL2** pop-up select **Connect**.

	>**Note:** if required maximize the **LON-CL2** VM.

1. In **LON-CL2**, on the log-in screen, you will log in as the local **Admin** account with a password of **Pa55w.rd**.

	>**Note:** If a **Networks** window appears, select **Yes**.

1. On the taskbar, select the **Microsoft Edge** icon. Maximize your Edge browser window if necessary.

	>**Note:** if any tabs opened close all the tabs.

1. In your **Edge** browser navigate to **https://portal.office.com**. 

1. You will begin by signing into Microsoft 365 as **Joni Sherman**. In the **Sign-in** window, enter **joni.sherman@otuwamocZZZZZZ.onmicrosoft.com (where ZZZZZZ is the tenant prefix provided by your lab hosting provider)**. For the password, sign-in with the same **Microsoft 365 Tenant Password** 
	
	- Password:- <inject key="AzureAdUserPassword"></inject>

		>**Note:** For example, in **odl_user_<inject key="DeploymentID" enableCopy="false"/>@otuwamocZZZZZZ.onmicrosoft.com**, the highlighted portion (**otuwamocZZZZZZ.onmicrosoft.com**) represents the domain name or tenant prefix, which you can replace with your desired tenant prefix.

1. On the **Stay signed in?** window, select the **Don't show this again** check box and then select **Yes**. If a **Save password** window appears, select **Never**.

1. If a **Welcome to Microsoft 365** dialog box appears in the middle of the page, select the forward-arrow (>) twice and then the check mark to close it.

	>**Note:** Close the pop-up which appears.

1. On the **Welcome to Microsoft 365** window, which is Joni's Microsoft 365 home page, a navigation pane appears on the left side of the screen that indicates the applications the user has permission to access. In this **Apps** pane, note how the **Admin** option is not displayed. This is because Joni was never assigned a Microsoft 365 administrator role. 

	![](../Images/ms-102-65.png)

17. You will now sign out of Microsoft 365 as Joni. In **Microsoft Edge**, at the top right of the **Welcome to Microsoft 365** page, select the user icon for **Joni Sherman** (the circle in the bottom left-hand corner), and in the **Joni Sherman** window that appears, select **Sign out.** 

18. You will now sign back into Microsoft 365 as **Lynne Robbins**. In your current **Edge** browser tab, it should display a message indicating **Joni, you're signed out now**. In this window, it gives you the option of signing back in as Joni, or signing in as a different user. Select **Switch to a different account**, and in the **Email address** field that appears, enter **lynne.robbins@otuwamocZZZZZZ.onmicrosoft.com (where ZZZZZZ is the tenant prefix provided by your lab hosting provider)**. For the password, sign-in with the same **Microsoft 365 Tenant Password** 
	
	- Password:- <inject key="AzureAdUserPassword"></inject>

		>**Note:** For example, in **odl_user_<inject key="DeploymentID" enableCopy="false"/>@otuwamocZZZZZZ.onmicrosoft.com**, the highlighted portion (**otuwamocZZZZZZ.onmicrosoft.com**) represents the domain name or tenant prefix, which you can replace with your desired tenant prefix.

19. If a **Welcome to Microsoft 365** dialog box appears, select the forward arrow (>) two times and then select the check mark to close the window.

20. If a **Find more apps** window appears, select the **X** in the upper right-hand corner of the window to close it.

21. On the **Welcome to Microsoft 365** window, which is Lynne's Microsoft 365 home page, note how the **Admin** icon is displayed in the navigation pane on the left side of the screen. This icon appears because Lynne was assigned to a Microsoft 365 administrator role. Select the **Admin** icon to open the Microsoft 365 admin center.

	![](../Images/MS-102-image-11.png)

22. In the **Microsoft 365 admin center**, select **Users (1)** on the navigation pane and then select **Active users (2)**. 

	![](../Images/L2E1T3S21-2904.png)

23. As the **User Administrator**, Lynne has permission to change user passwords. Lynne was recently contacted by **Diego Siciliani** and **Pradeep Gupta**, who each reported that their passwords may have been compromised. Per Adatum's company policy, Lynne must reset their passwords to a temporary value, and then force them to reset their password at their next login.  

24. In the **Active users** list, as you move your mouse from one user account to another, notice the **key (Reset a password)** icon that appears to the right of each user's name. Select the key icon that appears to the right of **Diego Siciliani's** name.

	![](../Images/L2E1T3S23-2904.png)

24. In the **Reset password** window for Diego, if the **Automatically create a password** check box displays a check mark, then select this box to clear it. This will enable Lynne to manually assign Diego a temporary password.  

25. Enter **diego** in the **Password** field. Note to the right of the password, the system displays a message indicating this is a **Weak (1)** password. Also note the message that appears below the field indicating **This password isn't strong enough (2)**. Finally, note how the **Reset password** button at the bottom of the pane is not enabled. **This button will only be enabled once you enter a strong password**.  

	![](../Images/deiogo.png)

26. Verify the **Require this user to change their password when they first sign in (1)** checkbox is selected (if not, then select it now to show a checkmark). Enter **Pa55w.rd** in the **Password** field. Note that the **Password** field indicates this is a **Strong (2)** password. 

	![](../Images/strong.png)

27. However, now select the **Require this user to change their password when they first sign in** checkbox to clear it. Note the error message that appears indicating the password (Pa55w.rd) contains a word, phrase, or series of numbers that makes it easily guessable. In this case, you entered a variation of the word **password**, which will trigger this error. The system allows you enter this password if you force the user to change it at their first sign-in. But if you don't force the user to enter a different password at their first sign-in, then this password isn't allowed.

27. After these two failed password attempts, Lynne has decided to let Microsoft 365 automatically generate a password. Select the **Automatically create a password (1)** check box so that it displays a check mark. 
	
28. The password that's automatically generated will just be a temporary password because Lynne wants to force Diego to change it the next time he logs in. Therefore, verify the **Require this user to change their password when they first sign in (2)** select it so that it displays a check mark.

29. Select **Reset password (3)**.

	>**Note:** If prompted to save the password, select **never** to close the window.

	![](../Images/L2E1T3S30-2904.png)

31. You should receive an error message. In Diego’s case, you assigned him the Billing Administrator role earlier in this lab exercise. Since only Global administrators can change another administrator's password, and because Lynne is not a Global administrator, she will have to ask Holly Dickson to make this change. Select **Close** in the **Reset password** pane. 

	>**Note:** If a survey request window appears, select **Cancel**.

	![](../Images/L2E1T3S31-2904.png)

33. In the **Active users** list, select the **key (Reset a password)** icon for **Pradeep Gupta**. 

34. In the **Reset password** window for Pradeep, verify the **Automatically create a password** check box displays a check mark; if it doesn't, then select this box now so that the system automatically generates a password for Pradeep.  

35. This is just a temporary password because Lynne wants to force Pradeep to change it the next time he logs in. Therefore, verify the **Require this user to change their password when they first sign in** check box displays a check mark; if the box is clear, then select it so that it displays a check mark.
	
35. Select the **Reset password** button.

36. On the **Password has been reset** window, you should receive a message indicating that you successfully reset the password for Pradeep. Select **Close**.

	![](../Images/pradeep.png)

37. Management has recently discovered that Alex Wilber's username may have been compromised. As a result, Lynne has been asked to block Alex's account so that no one can sign in with his username until management is able to determine the extent of the issue. In the **Active users** list, select the check box to the left of **Alex Wilber's** name (do NOT select Alex’s name itself).  

	>**Important:** Since you are going to run a global command rather than a command associated with Alex's account, you only want Alex's account selected in the list of active users. If any other user account is selected, you must unselect that user account before proceeding. Scroll through the list of active users and verify that no other user account is selected. If an account other than Alex is selected, select the account's check box to clear it. **Only Alex Wilber's account should be selected.**

38. In the menu bar at the top of the page, select the **ellipsis icon (...) (1)** to display a drop-down menu of additional actions. In the menu that appears, select **Edit sign-in status (2)**.

	![](../Images/MS-102-image-13.png)

39. In the **Block sign-in** pane that appears, verify Alex's email address appears below the **Block sign-in** heading. Select the **Block this user from signing in** check box, and then select **Save changes.** 

40. The **Block sign-in** window should display a message indicating that Alex is now blocked from signing in (and no one can sign in with Alex's username in the event that his username was actually compromised). In addition, Alex will automatically be signed out of Microsoft services within 60 minutes. Select the **X** in the upper right-hand corner of the pane to close it. 

	![](../Images/blocksign.png)

41. Lynne has just been informed that **Nestor Wilke's** username has also been potentially compromised. Repeat steps 37 through 40 to block Nestor from signing in (and to block anyone else from using his username to sign in). 

42. When you tried to block Nestor's sign in, you should have received an error message indicating **Changes could not be saved**. The reason that you received this error is that Nestor is a Global Administrator, and Lynne is not. Only a Global Administrator can block another Global Admin from being able to sign in. Lynne will need to ask Holly Dickson to make this change. Close the **Block sign-in** pane.

	![](../Images/changes.png)

42. You previously blocked Alex Wilber from being able to sign in. To verify whether he is blocked, you will attempt to sign in as Alex. Log out of Microsoft 365 by selecting the user icon for **Lynne Robbins** (the circle in the upper right-hand corner), and in the **Lynne Robbins** window that appears, select **Sign out.** 

43. As a best practice, close all your browser tabs except for the **Sign out** tab once you have been signed out. On the **Sign out** tab, navigate to **https://portal.office.com**. 

44. In the **Pick an account** window, select **Use another account**. In the **Sign in** window, enter **Alex.wilber@otuwamocZZZZZZ.onmicrosoft.com (where ZZZZZZ is the tenant prefix provided by your lab hosting provider)**. For the password, sign-in with the same **Microsoft 365 Tenant Password** 
	
	- Password:- <inject key="AzureAdUserPassword"></inject>

		>**Note:** For example, in **odl_user_<inject key="DeploymentID" enableCopy="false"/>@otuwamocZZZZZZ.onmicrosoft.com**, the highlighted portion (**otuwamocZZZZZZ.onmicrosoft.com**) represents the domain name or tenant prefix, which you can replace with your desired tenant prefix.

45. The **Pick an account** window should appear, and it should display an error message indicating **Your account has been locked. Contact your support person to unlock it, then try again.** You have just verified that Alex (or someone who has obtained Alex's username and password) cannot log in. 

	>**Note:** It can take a few minutes for the account block to fully implement. Until the block has been implemented in the system, Alex may still be able to log on, but none of the Microsoft 365 services will be available to him, and they will not appear in the Microsoft 365 portal. Once an account is unblocked, the services will become available again. 
	
	>**Note:** If you can sign in as Alex, sign back out and wait a few minutes. This may be a good time to take a short break. Then attempt to sign back in as Alex. By this time, you should hopefully receive the error message that indicates Alex's account has been blocked from signing in. 

	![](../Images/locked.png)
	
45. Minimize the Client-2 VM i.e. **LON-CL2**. You'll be on the **Hyper-V Manager** page, (if not search for Hyper-V Manager, in the windows search bar and open it). Open **Microsoft Edge** on the **LON-CL1**. 

46. In **LON-CL1**, you should still be logged into **Microsoft 365** as Holly Dickson in your Edge browser. The **Active users** list should be displayed in the **Microsoft 365 admin center** from earlier in this task. 

47. Upon further investigation, Adatum's CTO has determined that Alex Wilber's account has, in fact, not been compromised; therefore, the CTO has asked Holly to remove the block on Alex's user account. Repeat steps 37 through 40 to unblock his account. Note how the **Block sign-in** window from step 39 now displays the **Unblock sign-in** window instead.  

48. In the **Unblock sign-in** window, the **Block this user from signing in** check box is currently selected. Select this check box to clear it, and then select **Save changes**. 
	
	>**IMPORTANT:** A warning message is displayed indicating it can take up to 15 minutes before Alex can sign in again. Given the time constraints with the training, you will **NOT** try to verify whether Alex can log back in. If you want, you can try logging in as Alex at a later time if you're on a break or have spare time and you want to test this out. For now, remain on LON-CL1 and simply close the **Unblock sign-in** window.

	![](../Images/unblockalex.png)
	
48. On LON-CL1, leave your browser and all tabs open and proceed to the next exercise. 

## Review

In this lab, you have:

- Assigned Delegated Administrators in the Microsoft 365 Admin Center.
- Assigned Delegated Administrators with Windows PowerShell.
- Verified Delegated Administration.

## ## The lab has been completed successfully. Click **Next >>** to proceed to the next exercise.

