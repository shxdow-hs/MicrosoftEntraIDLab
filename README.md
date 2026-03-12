<h1>Microsoft Entra ID Lab</h1>


<h2>Description</h2>
In this lab I'll be working in a Microsoft Entra ID tenant I configured. I will be simulating IAM responsibilities by performing onboarding of new accounts, assigning a user to a new group, utilizing RBAC, enabling/enforcing MFA (Conditional Access) and secure offboarding.
<br />
<br />
This lab has exposed me to working with an enterprise identity environment and showcase my understanding of tasks and responsibilities IAM professionals carry out on a daily basis.

<h2>Programs and Utilities Used</h2>

- <b>Microsoft Entra ID</b>
- <b>Microsoft Power Automate</b> 
- <b>Microsoft Forms</b>

<h2>Lab Walkthrough:</h2>

<p>
<h3>Step 1: Microsoft Forms - New Employee Onboarding Form</h3>
Within my Microsoft environment, I utilized Microsoft Forms to simulate a company's onboarding process. In this form the new employee will be required to input their information such as their full name, job title, department and manager's name to help me sort and categorize the new user appropriately. 
I also require the new employee to notify us of their intended start date and their work laptop of choice. In a real-world situation, the user's account will be setup and enabled the day of their start date and their workstation will be imaged and ready for pickup.
<br />
<br />
  
<img src="https://i.imgur.com/ap3CHtz.png" height="80%" width="80%" alt="Onboarding Form"/><br/>
<i> New Employee Onboarding Form</i>
<br />
<br />

<h3>Step 2: Power Automate - Automating New User Creation (Joiner)</h3>
Using Power Automate, I have created a workflow to ingest new submission data from my employee onboarding form and create a new user account based off the information submitted.
This automated process ensures new user accounts can be accessed on day 1. Attributes such as Department and Job Title will be evaluated by the workflow to assign birthright access.
This process is better known as the Joiner process in the JML Lifecycle.
<br />
<br />

<img src="https://i.imgur.com/ATRJyCy.png" height="80%" width="80%" alt="Getting the form"/><br/>
The workflow begins when a new response to the onboarding form is submitted.
<br />
<br />
<img src="https://i.imgur.com/3mjuCv6.png" height="80%" width="80%" alt="Response ID"/><br/>
After the form is submitted, the workflow will get the response details and assign it a response id.
<br />
<br />
<img src="https://i.imgur.com/6vpzmjf.png" height="80%" width="80%" alt="New Submission Email"/><br/>
Using the response, I will craft an email after each submission. Here you'll see the "send email" function parse the form and fill out the information in the format specified.
<br/>
<br/>
<img src="https://i.imgur.com/CiF1hHq.png" height="80%" width="80%" alt="Email response"/><br/>
An email is sent to my inbox indicating there has been a new form submission. The email is populated with the employee's information they provided.
<br />
<br />
<img src="https://i.imgur.com/d44Dtxy.png" height="80%" width="80%" alt="Creating a User"/><br/>
The account is created after the email notification is sent.
Each newly created account will be disabled by default. New accounts will be enabled on the employee's start date after the account has been reviewed by the IAM analyst.
A default password is assigned to the new account and I utilize the employee's email submission to create the User Principal Name (UPN).
Using the Department submission, the user will be assigned to a Security Group associated with it.
The employee's Job Title and Mobile Phone number will also be populated.
<br />
<br />
<img src="https://i.imgur.com/3kcT8wv.png" height="80%" width="80%" alt="Account Created Notification"/><br/>
After the account is created in the Entra ID tenant an email is sent to my inbox indicating the new user account has been created.
<br />
<br />

<h3>Step 3: Access the Entra ID tenant - Create a Security Group</h3>
After creating my employee onboarding form and automated the onboarding process, I accessed the Microsoft Entra Admin Center to create a dynamic security group I'll use later in the lab.
<br />
<br />
On the left side of the screen, navigate to Entra ID --> Groups. 
<br />
<br />
At the top of the Groups Overview page click on New Group.
<br />
<br />
<img src="https://i.imgur.com/DJbVuLM.jpeg" height="80%" width="80%" alt="Groups Page"/>
Select Security under the Group Type.
<br />
<br />
HelpDesk will be the Group Name in this case.
<br />
<br />
I selected No to the Entra roles option as I want this group to have a Dynamic User Membership type to work with the workflow I created.
<br />
<br />
<img src="https://i.imgur.com/Rk3vKSj.jpeg" height="80%" width="80%" alt="Groups Page"/>
Click Add dynamic query.
<br />
<br />
In the new window, select Department under Property.
<br />
<br />
Equals under Operator and enter HelpDesk in the Value text box.
<br />
<br />
<img src="https://i.imgur.com/VIPn5vX.jpeg" height="80%" width="80%" alt="Groups Page"/>
Anytime a user account is given the Department name HelpDesk they will be added to this HelpDesk Security Group.
<br />
<br />

<h3>Step 4: Enabling Multi-Factor Authentication (MFA) </h3>
Multi-Factor Authentication is essential to strengthening authentication, reducing account compromise and unauthorized access. Passwords alone are not sufficient to protect enterprise identities.
<br />
<br />
To access the Authentication Methods navigate to Entra ID --> Protection --> Authentication Methods.
<br />
<br />
<img src="https://i.imgur.com/dgPqbQW.jpeg" height="80%" width="80%" alt="Groups Page"/>
To ensure strong authentication methods are used, I have enabled the following:
<br />
<br />
- Microsoft Authenticator
<br />
<br />
- Temporary Access Pass
<br />
<br />
- Software OATH Tokens
<br />
<br />
- Email OTP
<br />
<br />
Now that the authentication methods have been set they must be enforced through with a Conditional Access policy.
<br />
<br />
Navigate to ID Protection --> Risk-based Conditional Access --> New Policy.
<br />
<br />
<img src="https://i.imgur.com/4XkHpHH.jpeg" height="80%" width="80%" alt="Groups Page"/>
Next, I gave the new policy name and assigned 3 controls used to enforce the Multi-Factor Authentication. 
<br />
<br />
Under Assignments, this policy will apply to all users.
<br />
<br />
<img src="https://i.imgur.com/XR116cn.jpeg" height="80%" width="80%" alt="Groups Page"/>
In Target Resources, MFA will be enforced when accessing the Microsoft Admin Portals.
<br />
<br />
<img src="https://i.imgur.com/pRJaMNV.jpeg" height="80%" width="80%" alt="Groups Page"/>
Under Access Controls, access is to be granted and requires multifactor authentication 
<br />
<br />
Enable the policy and Save
<img src="https://i.imgur.com/FY0qqyr.jpeg" height="80%" width="80%" alt="Groups Page"/>


<h3>Step 5: Onboarding/Provisioning Walkthrough</h3>
Time to create a new user now that the Onboarding form is created, the automated workflow is configured and the Entra ID environment is ready to go.
<br />
<br />
<p><b>5.1) Submitting the New Employee Onboarding Form</b></p>
Here is a simulated new employee onboarding form submission. 
<br/>
<br/>
Jon Snow will be joining the company as an IT Support Analyst apart of the HelpDesk Department. 
<img src="https://i.imgur.com/lAR27yh.png" height="80%" width="80%" alt="Groups Page"/>

<p><b>5.2) Verify the new account in Entra ID</b></p>
After submission the new employee's account is created in Entra ID.
<br/>
<br/>
Navigate to Entra ID --> Users --> All Users.
<br/>
<br/>
Click on the new user and review the information.
<br/>
<br/>
The account can be seen populated with the employee's Full Name, Email Address, UPN, Identity, Group Membership and Account Status.
<br/>
<br/>
The account is disabled for now until after account verification and role assignment have been completed.
<img src="https://i.imgur.com/K0mY7yT.jpeg" height="80%" width="80%" alt="Groups Page"/>
While in the account profile, click on Groups to see the account group memberships.
<img src="https://i.imgur.com/nuq50FP.jpeg" height="80%" width="80%" alt="Groups Page"/>

<p><b>5.3) Role Assignment and RBAC</b></p>
After validating the newly provisioned account, a role must be assigned to the individual's account to enforce the principle of least privilege and role-based access control.
<br/>
<br/>
Since this user will be apart of the Helpdesk team, the predefined Helpdesk Administrator role will be assigned.
<br/>
<br/>
The user will have the ability to reset user passwords, force change passwords, invalidate refresh tokens, manage service requests and monitor service health.
<br/>
<br/>
While in the account profile, click on Assigned Roles.
<br/>
<br/>
Click Add assignments.
<br/>
<br/>
Search for Helpdesk Administrator and click add to assign it.
<img src="https://i.imgur.com/75vFBDx.jpeg" height="80%" width="80%" alt="Groups Page"/>

<p><b>5.4) Enabling the account</b></p>
The final step after completing validation and role assignment is enabling the account.
<br/>
<br/>
Once the account is enabled, the user may logon and conduct their daily tasks as needed.
<br/>
<br/>
Navigate to Entra ID --> Users --> Jon Snow --> Overview
<br/>
<br/>
Under Account Status --> Click Edit
<br/>
<br/>
Account Enabled --> toggle the checkmark and save
<img src="https://i.imgur.com/GPB5AdW.jpeg" height="80%" width="80%" alt="Groups Page"/>
The new user account is now provisioned and ready for use.

<h3>Step 6: Offboarding/Deprovisioning Walkthrough</h3>
Offboarding and deprovisioning accounts are essential to maintain a secure environment. Accounts left unaccounted for may cause breaches due to accounts left enabled with lingering access after the employee has left the organization.
<br/>
<br/>
<p><b>6.1) Remove Assigned Roles</b></p>
Navigate to Entra ID --> Users --> Jon Snow --> Assigned Roles
<br/>
<br/>
Check off Helpdesk Administrator --> click Remove assignments
<img src="https://i.imgur.com/kSAc6BY.jpeg" height="80%" width="80%" alt="Groups Page"/>

<p><b>6.2) Disable User Account</b></p>
Navigate to Entra ID --> Users --> Jon Snow --> Overview
<br/>
<br/>
Under Account Status --> Click Edit
<br/>
<br/>
Account Enabled --> toggle off the checkmark and save
<img src="https://i.imgur.com/SXHAPRV.jpeg" height="80%" width="80%" alt="Groups Page"/>

<h3>Conclusion</h3>
In this lab I've demonstrated my understanding of the Identity Lifecycle Management within Entra ID
<br/>
<br/>
- Account Provisioning 
<br/>
<br/>
- Role-based access control
<br/>
<br/>
- Authentication & Authorization
<br/>
<br/>
- Governance and compliance
<br/>
<br/>
- Account Deprovisioning 







</p>
