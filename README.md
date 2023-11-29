# Linux-assignment3

**How to Create a fresh Debian server and connect to it?** 
1) Click this link: https://www.digitalocean.com/
2) Click Sign up if you don't have an account, and create yours, or if you have sign in.
3) Click Create, Droplets, Choose your region, go down, and in the OS part, Click on Debian, and then, at the end, click Create Droplet.
4) Copy your Droplet address, and go to your Terminal.
5) Paste this command into your command line and change ```<Your-server-IP>``` with the IP address you copied.
   ```
   ssh -i .ssh/do-key root@<Your-server-IP>
   ```
Congrats, you are now connected to your new server!
