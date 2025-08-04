<p align="center">
<img width="auto" height="auto" alt="AD" src="https://github.com/user-attachments/assets/8997adb8-3e38-4019-9da5-6fadf4bab369" />
</p>

# Creating Users with PowerShell
*This lab will demonstrate how to configure Remote Desktop access for non-administrative users on Client-1 by allowing "domain users" to connect. It will also include the creation of multiple user accounts via PowerShell on DC-1 and testing their login capabilities on Client-1, ensuring proper access and functionality.*


## Lab Prerequisites

- [Lab Architecture: Preparing Active Directory Infrastructure in Azure](https://github.com/EddieJIV/Lab-Architecture-Preparing-Active-Directory-Infrastructure-in-Azure/blob/main/README.md)
- [Deploying & Configuring Active Directory](https://github.com/EddieJIV/Deploying-and-Configuring-Active-Directory)

## Lab Enviorments

-  Microsoft Azure
-  Windows Domain Controller
-  Windows 10
- Remote Desktop Protocol 
- Active Directory Users and Computers
- PowerShell ISE

## Setting up Remote Desktop for non-administrative users on Client-1:

<img width="auto" height="auto" alt="login" src="https://github.com/user-attachments/assets/25d50219-f149-4ce2-a5d4-ee5d8f6e5285" />




- First things first, log on to Client-1 as Jane_admin.
  - mydomain.com\Jane_admin
  - Cyberlab123!


<img width="700" height="700" alt="Client-1 System" src="https://github.com/user-attachments/assets/313632cb-ef3c-44ab-ab29-978f797ad9ca" />


- Navigate to System Properties.
  - You can type "System" into the search bar for quick access.
  - Again, this is where you can verify youre operating on the correct VM as well by double checking the Windows Specifications and noting that it is running Windows 10 pro.
- Click on Remote Desktop.

<img width="700" height="700" alt="RD Settings" src="https://github.com/user-attachments/assets/c8a9a1f1-2857-46f0-a334-9b6995ba881e" />

- Within Remote Desktop, under User accounts, click on Select users that can remotely access this PC.

<img width="auto" height="auto" alt="image" src="https://github.com/user-attachments/assets/47390dc9-17d5-450c-9d18-392198edeec3" />

- Click Add...

<table>
  <tr>
    <td>
      <img width="1000" height="1000" alt="Precheck" src="https://github.com/user-attachments/assets/7473e23c-d902-43d5-8b33-329dcdf4fb71" />
    </td>
    <td>
      <img width="1000" height="1000" alt="Checked" src="https://github.com/user-attachments/assets/d380a575-6fbe-44c9-87ca-2824591540fb" />
    </td>
  </tr>
</table>


- Within the text box "Enter the object names to select" we are going to add "domain users" then click on Check Names
- Once you click on check names you'll notice that it underlines and highlights domain users.
- Once you've done so, go ahead and click OK.

<img width="auto" height="auto" alt="Allow Domain Users" src="https://github.com/user-attachments/assets/dc1fd6ea-7006-4ade-bbf8-54ba42e45a59" />


- From here simply click OK
- Now, all domain users by default will be allowed to log into this computer, or in other words you can log into Client-1 as a normal, non-administrative user now.
  - Normally this is something that is done is Gropup Policy but we are going to do it here for the sake of the lab and do some practicing with Group Policy in the next lab!

## Part 2: Create additional users and attempt to log into Client-1 with one of the users 

- Now, log into DC-1 as Jane_admin if you havent already.
- Once you've logged into DC-1 as Jane_admin:

<img width="700" height="700" alt="image" src="https://github.com/user-attachments/assets/04b77fc8-7675-419e-8b5d-c9e0e1e92b45" />

- In the search bar, type in PowerShell, and RIGHT CLICK on Powershell ISE and RUN IT AS ADMINISTRATOR.
  - I apologize for the caps. It is important that you run PowerShell ISE as an administrator and not simply open it.

<img width="700" height="700" alt="Opening PowerShell ISE" src="https://github.com/user-attachments/assets/6baadcbc-b8c0-4f7b-b5e7-45ec38ddfaa8" />




- When you open PowerShell, you should see that you are running it as an administrator, if you are, go ahead and click on the icon in the top left corner below the word file to open up a new script.
  - Or: Click on File > New
- Paste the contents of [this script](https://github.com/joshmadakor1/AD_PS/blob/master/Generate-Names-Create-Users.ps1) into the new file.

<img width="700" height="700" alt="Script Edit" src="https://github.com/user-attachments/assets/f6d0f417-6c1e-4353-bd37-613c1cea2fc7" />


- We are going to make one simple edit to this script prior to running it, on line 3, it says number of accounts to create: 10000. We are going to change that number to 100 for the sake of this lab.
- Also, in the line above, take note that all the passwords for these users will be Password1. This is important for later on in the lab.


<img width="900" height="900" alt="Save as" src="https://github.com/user-attachments/assets/fe27022b-ddba-4fe3-a01f-d13c0b0df562" />

- Once you've made the edit, you can click file > Save as and name it "create-accounts" and simply save it to your desktop.

<img width="700" height="700" alt="Run Script" src="https://github.com/user-attachments/assets/9b2d02e3-ee8d-4a8e-8747-28513287e05b" />

- Once we saved our script, we can go ahead and click on run script!

<img width="700" height="700" alt="Ran Script" src="https://github.com/user-attachments/assets/11268f33-8321-45d3-a362-f1ecb09ccf76" />

From here you'll get to see our script work its magic and add 100 new users to our _EMPLOYEES folder in Active Directory Users and Computers! 

<img width="500" height="800" alt="AD UC" src="https://github.com/user-attachments/assets/2c6fc820-7e7a-4370-9342-30f553d7bdee" />

- Navigate to Active Directory Users and Computers > mydomain.com > _EMPLOYEES to observe all our new users!
- Pick a user of your choice from your list and attempt to log into Client-1 using their username and Password1.

<img width="299" height="362" alt="image" src="https://github.com/user-attachments/assets/31e25107-5a46-4b6a-8e7a-cdee649ea092" />

- I am going to use bob.saja for this example
- So, for the full username, to get into our domain, I will put mydomain.com\bob.saja & Password1 for the password into the Client-1 login.
  - You will essentially be doing the same thing with the user you chose from your _EMPLOYEES file.
 
img

- Once you connect, you can open up command line and youll see that there is a local profile for the user you logged into as

![Uploading image.png…]()


- You can also open up file explorer and go to This PC > Windows C: Drive > Users youll be able to see the users profile as well!

---
This effectively concludes the Creating Users with Powershell lab! As always, if you are done for the day, remember to stop your VM's on Azure until the next time you log in.






















<table>
  <tr>
    <td>
      <img width="1000" alt="Img1" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
    <td>
      <img width="1000" alt="Img2" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
  </tr>
</table>

<table>
  <tr>
    <td>
      <img width="1000" alt="Img1" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
    <td>
      <img width="1000" alt="Img2" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
  </tr>
</table>


<table>
  <tr>
    <td>
      <img width="1000" alt="Img1" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
    <td>
      <img width="1000" alt="Img2" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
  </tr>
</table>

<table>
  <tr>
    <td>
      <img width="1000" alt="Img1" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
    <td>
      <img width="1000" alt="Img2" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
  </tr>
</table>


<table>
  <tr>
    <td>
      <img width="1000" alt="Img1" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
    <td>
      <img width="1000" alt="Img2" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
  </tr>
</table>

<table>
  <tr>
    <td>
      <img width="1000" alt="Img1" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
    <td>
      <img width="1000" alt="Img2" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
  </tr>
</table>


<table>
  <tr>
    <td>
      <img width="1000" alt="Img1" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
    <td>
      <img width="1000" alt="Img2" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
  </tr>
</table>

<table>
  <tr>
    <td>
      <img width="1000" alt="Img1" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
    <td>
      <img width="1000" alt="Img2" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
  </tr>
</table>


<table>
  <tr>
    <td>
      <img width="1000" alt="Img1" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
    <td>
      <img width="1000" alt="Img2" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
  </tr>
</table>

<table>
  <tr>
    <td>
      <img width="1000" alt="Img1" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
    <td>
      <img width="1000" alt="Img2" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
  </tr>
</table>


<table>
  <tr>
    <td>
      <img width="1000" alt="Img1" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
    <td>
      <img width="1000" alt="Img2" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
  </tr>
</table>

<table>
  <tr>
    <td>
      <img width="1000" alt="Img1" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
    <td>
      <img width="1000" alt="Img2" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
  </tr>
</table>


<table>
  <tr>
    <td>
      <img width="1000" alt="Img1" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
    <td>
      <img width="1000" alt="Img2" src="https://i.imgur.com/DJmEXEB.png" />
    </td>
  </tr>
</table>
