AWS EC2 Nginx Shopping Website
---------------------------------

Overview
----------

This project demonstrates the deployment of a static shopping website on **Amazon EC2** using **Amazon Linux 2023** and **Nginx** as the web server.

The EC2 instance is configured with a public IP address and a Security Group that allows HTTP traffic on port 80. The website is hosted from the Nginx web root and can be accessed through the EC2 public IPv4 address.

Objective
-----------

* Amazon EC2
* Amazon Linux 2023
* Security Groups
* SSH
* Linux system administration
* Nginx web server
* HTTP
* Static website deployment
* AWS networking fundamentals


Architecture
------------


                         INTERNET
                             |
                             | HTTP :80
                             |
                             v
                  +---------------------+
                  |    AWS EC2 Instance |
                  |  Amazon Linux 2023  |
                  +----------+----------+
                             |
                             v
                         Nginx
                             |
                             v
                    /usr/share/nginx/html
                             |
                             v
                         index.html
                             |
                             v
                  Vanshika Shopping Complex




AWS Services Used
-------------------

| Service             | Purpose                               |
| ------------------- | ------------------------------------- |
| Amazon EC2          | Hosts the web server                  |
| Amazon VPC          | Provides networking                   |
| Security Group      | Controls inbound/outbound traffic     |
| Elastic/Public IPv4 | Provides public access to the website |
| Nginx               | Web server                            |
| Amazon Linux 2023   | Operating system                      |


       STEPS TO PERFORM 
       ================
       
Step 1 — Launch EC2 Instance

Navigate to:

**AWS Console → EC2 → Instances → Launch Instance**

Configure the instance:

| Configuration         | Value             |
| --------------------- | ----------------- |
| Name                  | Shopping-Website  |
| AMI                   | Amazon Linux 2023 |
| Instance Type         | t2.micro          |
| Key Pair              | shopping-key      |
| Auto-assign Public IP | Enabled           |

The key pair is used to securely connect to the EC2 instance through SSH.

---

Step 2 — Configure Security Group

Create or select a Security Group with the following inbound rules:

| Type  | Protocol | Port | Source    |
| ----- | -------- | ---: | --------- |
| SSH   | TCP      |   22 | My IP     |
| HTTP  | TCP      |   80 | 0.0.0.0/0 |
| HTTPS | TCP      |  443 | 0.0.0.0/0 |



**Port 22 — SSH**

Used to securely connect to the EC2 instance.

**Port 80 — HTTP**

Allows users on the internet to access the website.

**Port 443 — HTTPS**

Reserved for HTTPS traffic. HTTPS is not configured in this basic version of the project.

For a production deployment, HTTPS should be configured using TLS/SSL.


Step 3 — Connect to EC2

After launching the instance, obtain its **Public IPv4 address** from:

**EC2 → Instances → Shopping-Website**


cd Downloads
dir
Connect using SSH:
ssh -i shopping-key.pem ec2-user@YOUR_PUBLIC_IP

Step 4 — Update the System

sudo dnf update -y

Step 5 — Install Nginx

Install Nginx:

sudo dnf install nginx -y

Start the Nginx service:

sudo systemctl start nginx


Enable Nginx to start automatically after a reboot:

sudo systemctl enable nginx

Check the service:
sudo systemctl status nginx

Expected status:

Active: active (running)

Step 6 — Test Nginx

Open a browser and enter:
http://YOUR_PUBLIC_IP

If Nginx is working correctly, the default Nginx page should appear.

Step 7 — Locate the Nginx Web Root

Nginx serves website files from:

/usr/share/nginx/html

Navigate to the directory:
cd /usr/share/nginx/html

pwd

Expected:

/usr/share/nginx/html


ls -la


Step 8 — Replace the Default Website

Remove the default Nginx page:

sudo rm index.html

Create the custom website:

sudo nano index.html

Paste the HTML code from:


website/index.html

Save the file

Step 9 — Restart Nginx

Restart the web server:

sudo systemctl restart nginx

Verify:

sudo systemctl status nginx

Confirm that:

Active: active (running)

Step 10 — Test the Shopping Website


http://YOUR_PUBLIC_IP

     **Vanshika Shopping Complex**

=> Check web root


ls -la /usr/share/nginx/html


=> Test locally from EC2


curl http://localhost

http://YOUR_PUBLIC_IP




=>️ Troubleshooting


Check the Nginx service:


sudo systemctl status nginx


Check whether port 80 is listening:


sudo ss -tulnp | grep :80


Check the Security Group and make sure HTTP port 80 is allowed.



NOTE: Nginx is not running

    


sudo systemctl restart nginx

sudo systemctl status nginx


Check Nginx configuration:


sudo nginx -t


=>  Permission issues

Check the website directory:


ls -ld /usr/share/nginx/html

Check the website file:


ls -l /usr/share/nginx/html/index.html


Recommended screenshots:

1. EC2 instance running
2. Security Group inbound rules
3. SSH connection
4. Nginx service running
5. Nginx web root
6. Final shopping website in browser


=> Skills :

* AWS EC2
* Amazon Linux 2023
* Linux Administration
* SSH
* Security Groups
* Networking
* HTTP
* Nginx
* Web Server Configuration
* Static Website Deployment
* Troubleshooting



# Future Improvements


* HTTPS using SSL/TLS
* Route 53 custom domain
* Application Load Balancer
* Auto Scaling Group
* Launch Template
* CloudWatch monitoring
* S3 integration
* CI/CD pipeline
* Docker containerization
* AWS ECS deployment


 Author

**Vanshika Chauhan**

