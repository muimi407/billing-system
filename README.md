PHPNuxBill - Billing System

Overview
PHPNuxBill is a billing system designed for managing user accounts, services, and invoices. This guide provides step-by-step instructions to set up and run PHPNuxBill using Docker.

Prerequisites
Ensure you have the following installed on your system:
•	Docker & Docker Compose
•	WSL (Windows Subsystem for Linux) (if using Windows)

Installation and Setup

1. Clone the Repository
cd /mnt/c/Users/Administrator/Desktop/web/
git clone <your-repo-url> billing-system
cd billing-system

3. Install Docker (If Not Installed)
sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

5. Start the Docker Containers
sudo docker-compose up -d --build
This will start two containers:
•	nuxbill (PHP application)
•	mysql (Database)

7. Check Running Containers
sudo docker ps
Ensure both nuxbill and mysql containers are running.

9. Configure the Database
Access the MySQL container and create the required database and user:
sudo docker exec -it mysql mysql -u root -p
Then run the following SQL commands:
CREATE DATABASE IF NOT EXISTS nuxbill;
CREATE USER IF NOT EXISTS 'nuxbill'@'%' IDENTIFIED BY '12345678';
GRANT ALL PRIVILEGES ON nuxbill.* TO 'nuxbill'@'%';
FLUSH PRIVILEGES;
EXIT;

11. Install PHPNuxBill
Open your browser and go to:
http://localhost
Follow the on-screen instructions and enter the database credentials:
•	Database Host: mysql
•	Database Username: nuxbill
•	Database Password: 12345678
•	Database Name: nuxbill

12. Post-Installation Steps
•	Rename pages_example to pages (if it exists)
mv pages_example pages
•	Delete the installation directory for security:
rm -rf system/install
•	Access the Admin Panel:
o	URL: http://localhost/admin
o	Username: admin
o	Password: admin

Troubleshooting
•	If you encounter database connection issues, restart the containers:
sudo docker-compose down && sudo docker-compose up -d
•	To check logs for debugging:
sudo docker logs nuxbill
sudo docker logs mysql

License
This project is licensed under the MIT License.

