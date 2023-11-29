# Linux-assignment3

# How to Create a fresh Debian server and connect to it?
1) Click this link: https://www.digitalocean.com/
2) Click Sign up if you don't have an account, and create yours, or if you have sign in.
3) Click Create, Droplets, Choose your region, go down, and in the OS part, Click on Debian, and then, at the end, click Create Droplet.
4) Copy your Droplet address, and go to your Terminal.
5) Paste this command into your command line and change ```<Your-server-IP>``` with the IP address you copied.
   ```
   ssh -i .ssh/do-key root@<Your-server-IP>
   ```
Congrats, you are now connected to your new server!


# How to Create a New Regular User:
   - User can perform administrative tasks
   - User has bash as login shell
   - User can access the server via SSH
After that, you are connected to your server:
**Step1: Create a New User** 
1) Type this code into your server command line:
```
useradd <username>
```
2) The new user is now created.

**Step2: Give the user Admin privileges**
(Replace ```<username>``` with the name you want to put as username)
1) Type this command to give the user, Admin privileges:
```
usermod -aG sudo username
```
**Step3: Set bash as login Shell**
(Replace ```<username>``` with the name you want to put as username)
1) Type this command to set bash as login for the user: 
```
chsh -s /bin/bash username
```
(Again, replace ```<username>``` with the name you want to put as username)
**Step4: Enable SSH Access for the New User**
1) On your local machine, generate a SSH key pair by using this command:
```
ssh-keygen
```
2) Copy the public key to your Debian server with this command:
```
ssh-copy-id username@your_server_ip
```
3) Login to your username with this command:
```
ssh username@your_server_ip 
```
Congrats, now you are connected to your new user in your new server using shell and you have admin privileges. 

# How to Prevent the root user from connecting to the server via SSH?


پ






