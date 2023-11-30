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
Assuming you have your server ready and you connected to it with your user: 

**Step1: Edit the SSH Configuration File**
1) Type this to open SSH configuration file:
```
sudo vim /etc/ssh/sshd_config
```
2) Type your password if prompted to.

**Step2: Disable Root Login**
1) Find a line in the file that says: ```PermitRootLogin yes```, Change it to:
```
PermitRootLogin no
```
Note: If this line is commented uncomment this or if it doesn't exist, add this to your file. 
2) Type ```;``` and Type wq (it writes the changes and quits the file).
3) Press Enter. 

**Step3: Restart the SSH Service**
1) Restart the SSH service:
```
sudo systemctl restart sshd
```
2) Type **"exit"** in your server terminal and exit the server.
3) Type this in your machine terminal to connect to root:
```
ssh root@your_server_ip
```
It should be denied.

Congrats, you just prevented the root user from connecting to the server via SSH.

# Install nginx

**Step1: Update Your Server**
Assuming you are connected to your server with your user account. 
1) Type this into the terminal.
```
sudo apt update
```
This is to update the package lists. 
2) Optionally, you can upgrade all your installed packages to their latest versions:
```
sudo apt upgrade
```

**Step2: Install Nginx**
1) Type this command to install Nginx:
```
sudo apt install nginx
```
2) Type this to check the status of the Nginx service:
```
sudo systemctl status nginx
```

**Step3: Check it in your browser**
1) Open your web browser.
2) Enter your server's IP address.
3) You should see the Nginx welcome page.

Congrats you just installed Nginx, on your server. 

# Configure nginx to serve a sample website

**Step1: Create a Directory for Your Website**
1) create a directory to hold your website's files using this command:
```
sudo mkdir -p /var/www/your-site
```
Notes:
   - The directory will be in the **"/var/www/"** directory. 
   - Replace **"your-site"** with your domain name.
2) Create your HTML page in **"your-site"** directory:
```
sudo vim /var/www/your-site/index.html
```
3) Add some content to your index.html.
4) Type ```;``` and Type wq (it writes the changes and quits the file).

**Step2: Create a Server Block for Your Website**
1) Type this to create a new server block for your website:
```
sudo vim /etc/nginx/sites-available/example.com
```
2) Paste the following configuration into this file:
```
server {
    listen 80;
    server_name example.com www.example.com;

    root /var/www/your-site;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```
Note: Change ```your-site``` with the directory name that you made in the first step.
3) Type ```;``` and Type wq (it writes the changes and quits the file).

**Step 3: Enable the Server Block**
1) Type this command to create a symbolic link to the sites-enabled directory:
```
sudo ln -s /etc/nginx/sites-available/example.com /etc/nginx/sites-enabled/
```
2) Test your configuration for syntax errors
```
sudo nginx -t
```
Note: It should give you a prompt like this:
```
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```
3) Restart Nginx to apply the changes:
```
sudo systemctl restart nginx
```
**Step 4: Access Your Website**
1) Open your web browser and navigate to your domain.
2) You should see the sample webpage you created.

Congrats, you configured Nginx to serve a sample website. 





