# ActiveDirectoryLab
Walkthrough of my setup and changes I made within an Active Directory environment.
<h2>Changes made</h2>

- <b>Organizational Units created and added</b> 
- <b>Group Policy Objects created and added to OU's</b>
- <b>Security Groups added with specific users and delegated controls</b>

<h2>Environments Used </h2>

- <b>Windows 11</b>
- <b>Windoiws Server 2019</b>
- <b>VirtualBox</b>

<h2>Active Directory walk-through:</h2>
<h3>Creation of OU's and moving users to a OU</h3>
<p align="center">
Adding the user "bglasgow" to the Finance OU: <br/>
<img src="https://image2url.com/images/1761091079502-039bd6a3-1b1b-4f09-b607-9b5b35d7ec4f.png" height="80%" width="80%" alt="AD Steps"/>
<br />
<br />
Moving the user to the correct OU: <br/>
<img src="https://image2url.com/images/1761091057696-2c3cc686-921a-4e7b-8cac-45a7428c098d.png" height="80%" width="80%" alt="AD Steps"/>
<br/>
<br/>
Confirming that user "bglasgow" was added to the Finance OU: <br/>
<img src="https://image2url.com/images/1761090882083-ef752754-5cd8-44be-886a-6b854bd70592.png" height="80%" width="80%" alt="AD Steps"/>
<br/>
<br/>
Creation of a new OU that is titled IT Department: <br/>
<img src="https://image2url.com/images/1761090841153-24d46971-bd55-4a56-8ba5-b771de456c81.png" height="80%" width="80%" alt="AD Steps"/>
<br/>
<img src="https://image2url.com/images/1761090238333-4d890e61-d25f-466d-a1e3-d44580fd1121.png" height="80%" width="80%" alt="AD Steps"/>
<br/>
<br/>
<h3>Security Groups</h3>
<p align="center">
Creation of a global "IT Managers" security group in the IT Department:  <br/>
<img src="https://image2url.com/images/1761090141164-23b2586c-6fac-4676-8821-ebdd679be4b7.png" height="80%" width="80%" alt="AD Steps"/>
<br/>
<img src="https://image2url.com/images/1761089885244-b026f6bb-6126-446c-a07e-ad6e54366121.png" height="80%" width="80%" alt="AD Steps"/>
<br/>
<br/>
Here I am displaying that the "Members" of the IT Managers Group contains different users than that of the IT Department. Seperating any privelaged access that the IT Managers security group gets: <br/>
<img src="https://image2url.com/images/1761089092419-c45627ee-9615-493f-afe4-71b65df4f6ab.png" height="80%" width="80%" alt="AD Steps"/>
<br />
<br />
I then created a domain local "ACCT_PERM" security group that I add the "IT Managers" to, allowing the permissions that I assign to the "ACCT_PERM" to be applied to all of the "IT Managers" without having to individually assign each user the authorized permissions:  <br/>
<img src="https://image2url.com/images/1761090196638-817c1b99-8a4c-4a97-8f81-d8ae2e6bced8.png" height="80%" width="80%" alt="AD Steps"/>
<br/>
<br/>
Because I want to give the IT Managers certain permissions, I used the delegation wizard to delegate control over the Finance to them. Since they are a in the security group ACCT_PERM, that is who I will delegate the control to:  <br/>
<img src="https://image2url.com/images/1761090017071-bcc7af69-b182-4d2c-805a-b12d797d4665.png" height="80%" width="80%" alt="AD Steps"/> <br/>
<br/>
I delegated the ability to reset passwords for user accounts in Finance: <br/>
<img src="https://image2url.com/images/1761156341161-fb3fee6c-0935-415a-9da3-32882b149697.png" height="80%" width="80%" alt="AD Steps"/>
<br/>
<img src="https://image2url.com/images/1761089930362-d008aed9-af43-4203-a785-28f67810a271.png" height="80%" width="80%" alt="AD Steps"/>
<br />
<br />
<h3>Creating and editing GPO's</h3>
<p align="center">
Here I have opened the Group Policy Management Editor to create a new GPO for the Finance OU. In the GPO, I disabled access to the command prompt, disabled the use of removable storage drives, and disabled the ability to access the control panel and PC setting. Providing more security and less privelage to the users within this OU:  <br/>
<img src="https://image2url.com/images/1761091122445-8f9cd10b-e2cb-4f80-b587-50d6d16e7794.png" height="80%" width="80%" alt="AD Steps"/>
<br/>
<img src="https://image2url.com/images/1761091135358-61a738fb-61ee-4989-bb12-2c3fb0498ab9.png" height="80%" width="80%" alt="AD Steps"/>
<br/>
<img src="https://image2url.com/images/1761091180761-4f3ddb66-6af4-4c6a-83a8-d18bed0f1629.png" height="80%" width="80%" alt="AD Steps"/>
<br/>
<br/>
Displaying the GPO's settings or what it includes and that is enforced:  <br/>
<img src="https://image2url.com/images/1761091108408-1767ea3e-0085-4980-84cc-d544a66fab4f.png" height="80%" width="80%" alt="AD Steps"/>
<br/>
<img src="https://image2url.com/images/1761091094835-7d2b61e3-84ae-4257-8757-1e25e5e2add7.png" height="80%" width="80%" alt="AD Steps"/>
<br/>
<br/>
To confirm that it was enforced and enabled I logged into my Client computer as the user "aabrev" who is apart of the Finance OU and attempted to pull up the command prompt. I was met with a message stating that it was disabled by an administrator:  <br/>
<img src="https://image2url.com/images/1761153773024-898e9ddf-89d7-4c50-a704-b4d56a5dbc02.png" height="80%" width="80%" alt="AD Steps"/>
<br />
<br />
For the default domain GPO, I went in and set an invalid login attempts limit because initially there was not one. Upon changing this, it changed the other surrounding policies, ultimately enabling an administrator lockout as well. For the purposes of my lab i went back and disabled this policy.:  <br/>
<img src="https://image2url.com/images/1761091258779-bda2da67-9369-4471-b83f-af96773b6dd9.png" height="80%" width="80%" alt="AD Steps"/>
<br/>
<br/>
I set the failed attempts before account lockout to 5:  <br/>
<img src="https://image2url.com/images/1761091246455-27991690-6ba9-45e5-b3c4-c4d3fccdd25a.png" height="80%" width="80%" alt="AD Steps"/>
<br/>
<br/>
Disabling the administrator account lockout:  <br/>
<img src="https://image2url.com/images/1761091204849-d371e7f1-fbee-4499-ad65-5b12947e2a6d.png" height="80%" width="80%" alt="AD Steps"/>
<br/>
<br/>
Defined GPO settings of the changes made:  <br/>
<img src="https://image2url.com/images/1761091151067-f2b9f509-9c2b-4af9-87e2-42bb2b15c05c.png" height="80%" width="80%" alt="AD Steps"/>
<br />
<br />
24:  <br/>
<img src="" height="80%" width="80%" alt="AD Steps"/>
<br />
<br />
25:  <br/>
<img src="" height="80%" width="80%" alt="AD Steps"/>
<br />
<br />
26:  <br/>
<img src="" height="80%" width="80%" alt="AD Steps"/>
<br />
<br />
27:  <br/>
<img src="" height="80%" width="80%" alt="AD Steps"/>
<br />
<br />
28:  <br/>
<img src="" height="80%" width="80%" alt="AD Steps"/>
<br />
<br />
29:  <br/>
<img src="" height="80%" width="80%" alt="AD Steps"/>
<br />
<br />
30:  <br/>
<img src="" height="80%" width="80%" alt="AD Steps"/>
<br />
<br />
31:  <br/>
<img src="" height="80%" width="80%" alt="AD Steps"/>
<br />
<br />
32:  <br/>
<img src="" height="80%" width="80%" alt="AD Steps"/>
<br />
<br />
33:  <br/>
<img src="" height="80%" width="80%" alt="AD Steps"/>
<br />
<br />
:  <br/>
<img src="" height="80%" width="80%" alt="AD Steps"/>
<br />
<br />
:  <br/>
<img src="" height="80%" width="80%" alt="AD Steps"/>
<br />
<br />
:  <br/>
<img src="" height="80%" width="80%" alt="AD Steps"/>
<br />
<br />
:  <br/>
<img src="" height="80%" width="80%" alt="AD Steps"/>
<br />
<br />
:  <br/>
<img src="" height="80%" width="80%" alt="AD Steps"/>
<br />
<br />



</p>

