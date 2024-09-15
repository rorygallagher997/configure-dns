<p align="center">
<img src="https://github.com/user-attachments/assets/d94d84c1-be28-4ba7-85fc-617fb835c09f"/>
</p>

<h1>Configuring DNS settings within Azure</h1>
This tutorial outlines the implementation of DNS settings within Azure Virtual Machines.<br />

<h2>Environments and Technologies Used</h2>

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop
- Active Directory Domain Services
- DNS Manager

<h2>Operating Systems Used </h2>

- Windows Server 2022
- Windows 10 (22H2)

<h2>High-Level Deployment and Configuration Steps</h2>

- A-Record Exercise
- Local DNS Cache Exercise
- CNAME Record Exercise

<h2>Deployment and Configuration Steps</h2>

<p>
<img src="https://github.com/user-attachments/assets/777ce3be-5066-4b7c-89b7-b506fed1594b" height="50%" width="50%"/>
</p>
<p>
This is a continuation of the Active Directory project. Ping "mainframe" on Client-1 and notice it can't resolve.
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/d24355a3-cd35-4419-8419-51a859c73b70" height="50%" width="50%"/>
</p>
<p>
Go to Server Manager on DC-1. Under tools, Select "DNS".
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/91322820-8062-45de-beb1-6c5e8b7bca01" height="50%" width="50%"/>
</p>
<p>
Click on DC-1 then Foward Lookup Zones and then mydomain.com.
</p>
<br />


<p>
<img src="https://github.com/user-attachments/assets/98a0b9b5-26d9-4891-a89c-5fcf653b34e1" height="50%" width="50%"/>
</p>
<p>
Right click and select New Host (A or AAAA).
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/4a770e72-bf8b-4efd-aecd-59dce401e6f0" height="50%" width="50%"/>
</p>
<p>
Create a new host called Mainframe. For this example, I just used the same IP address as DC-1.
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/fa2061dd-30c3-4210-9e51-f366483bf6fa" height="50%" width="50%"/>
</p>
<p>
After successfully creating an A Record for "mainframe", we can now receive a ping response on Client-1.
</p>
<br />

<p>
<img src="https://github.com/user-attachments/assets/431cb40f-b5af-482f-a2cf-26f0b4da8376" height="50%" width="50%"/>
</p>
<p>
To view the DNS cache, use the command "ipconfig /displaydns". Notice how mainframe is now in the DNS cache.
<br />

<p>
<img src="https://github.com/user-attachments/assets/620d0668-e125-4a68-8c81-a5eec9233e0b" height="50%" width="50%"/>
</p>
<p>
We are now going to change the IP address for mainframe. Go back to DC-1's DNS Manager and select mainframe. Change the IP address to 8.8.8.8.
<br />

<p>
<img src="https://github.com/user-attachments/assets/7d1a0dea-2515-4689-b93c-15429c41e8e8" height="50%" width="50%"/>
</p>
<p>
Now go back to to Client-1 and ping mainframe again. Notice how even after changing the IP address of mainframe, it is still resolving to the original IP of 10.0.0.4. We need to clear the DNS cache.
<br />

<p>
<img src="https://github.com/user-attachments/assets/fca17a99-5fe9-45c4-ab87-158c1417a506" height="50%" width="50%"/>
</p>
<p>
Let's now clear the DNS cache on Client-1. You need elevated permissions to do it, so close the commmand prompt and open again as an administrator.
<br />

<p>
<img src="https://github.com/user-attachments/assets/196da338-9039-4206-9811-52895d859d70" height="50%" width="50%"/>
</p>
<p>
Use the command "ipconfig /flushdns". The cache has been successfully cleared.
<br />

<p>
<img src="https://github.com/user-attachments/assets/2486b489-e435-40a3-9d03-afb010324a37" height="50%" width="50%"/>
</p>
<p>
We can see now mainframe is resolving to the new IP address, 8.8.8.8
<br />

<p>
<img src="https://github.com/user-attachments/assets/ca52d837-5d68-4c43-8926-e098a4c132e9" height="50%" width="50%"/>
</p>
<p>
As an exercise, we are going to create a CNAME record named "search" to match www.google.com. First, ping "search" and notice nothing resolves.
<br />

<p>
<img src="https://github.com/user-attachments/assets/d742513f-0ae6-4bf7-840e-7e9fa93fbcbf" height="50%" width="50%"/>
</p>
<p>
Go back to DC-1's DNS Manager and right click to create the record. Select "New Alias(CNAME)".
<br />

<p>
<img src="https://github.com/user-attachments/assets/632d6b87-a3b2-45d8-a571-e7000b6ef5e1" height="50%" width="50%"/>
</p>
<p>
Name the record "search" for this example and map it to www.google.com.
<br />

<p>
<img src="https://github.com/user-attachments/assets/7513a085-92ed-4f61-a171-138dbb330d06" height="50%" width="50%"/>
</p>
<p>
Go back to Client-1 and ping "search". Notice how it now resolves to www.google.com.
<br />















