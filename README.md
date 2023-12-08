# Infotrixs
Task: Deploy application in monolithic and microservices architecture
Description:
- For monolithic : 1 EC2 instance, deploy wordpress and MYSQL on the same instances
- For microservices: 2 EC2 instance, 1 for wordpress and 1 for MYSQL
- Configure the necessary security group for the instances
- EC2 instance type: t2-micro, AMI: ubuntu-*
A Monolithic architecture refers to a traditional software architecture where all components of an application are tightly integrated into a single codebase and deployed as a single unit
Scenario: Deploying a wordpress and MySQL Database on a single AWS EC2 Instance
Step 1: Create an Amazon EC2 Instance
Log in to AWS Console:

Log in to your AWS Management Console.
Navigate to EC2:

Go to the EC2 service.
Launch Instance:

Click on the "Launch Instance" button.
Choose an Amazon Machine Image (AMI):

Select an Amazon Machine Image (AMI), such as Amazon Linux or Ubuntu.
Choose an Instance Type:
Choose an instance type based on your resource requirements i have choosen micro which is free tier
Configure Instance Details:
Configure the instance details, including the number of instances, network settings, and other options.
Add Storage:
Add storage as per your requirements. The default settings may be sufficient for this scenario.
Add Tags:
Add any tags if needed for better organization.
Configure Security Group:
Create a new security group or use an existing one. Open ports 80 (HTTP), 443 (HTTPS), and 3306 (MySQL) for inbound traffic.
Review and Launch:
Review your configurations and click "Launch."
Key Pair:
Choose an existing key pair or create a new one to securely connect to your instance.
Launch Instance:
Click "Launch Instance."
![Screenshot 2023-12-07 171524](https://github.com/Bhargavi412100/Infotrixs/assets/139414716/db4732c4-5530-4620-99e2-4b1d91c9e46e)

Step 2: Connect to the EC2 Instance
After succesfully connected to ec2 mechine, firstly update the mechine with the cmd sudo apt-get update
when the mechine successfully updated as we want wordpress to run in it we wnat a wenserver for that we need to install apache2 
sudo apt install apache2 -y
![Screenshot 2023-12-07 171725](https://github.com/Bhargavi412100/Infotrixs/assets/139414716/bb1d23dc-171f-47c8-a670-96a862132cbc)
after successfully installed the webserver, we need to install php with sql pluggin for that i have used a cmd
sudo apt install php-mysql
![Screenshot 2023-12-07 172010](https://github.com/Bhargavi412100/Infotrixs/assets/139414716/b5ca95d0-c37b-4ad9-b208-69b43cde2090)
now get awordpress downloadable tar file for that i have used a cmd
cd /tmp
wget https://wordpress.org/latest.tar.gz
Unzip
tar -xvf latest.tar.gz
Move wordpress folder to apache document root
sudo mv wordpress/ /var/www/html
Command to restart/reload apache server
sudo systemctl restart apache2
OR
sudo systemctl reload apache2
Install MySQL server
sudo apt install mysql-server 
Login to MySQL server
sudo mysql -u root
Change authentication plugin to mysql_native_password (change the password to something strong)
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password by 'Testpassword@123';
Create a new database user for wordpress (change the password to something strong)
CREATE USER 'purvi'@localhost IDENTIFIED BY 'Testpassword@123';
Create a database for wordpress
CREATE DATABASE wordpress;
Grant all privilges on the database 'wp' to the newly created user
GRANT ALL PRIVILEGES ON wp.* TO 'purvi'@localhost;
![Screenshot 2023-12-07 185941](https://github.com/Bhargavi412100/Infotrixs/assets/139414716/534429de-5ce7-4325-94f8-6e7d2959fa40)

