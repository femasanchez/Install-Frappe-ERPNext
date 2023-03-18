# Update and Upgrade Packages
sudo apt-get update && sudo apt-get upgrade -y
sudo apt-get install tesseract-ocr-all imagemagick libmagickwand-dev ghostscript imagemagick libtesseract-dev python3-ghdiff websocket-client markdown beautifulsoup4 lxml -y
pip install pytesseract pillow wand tesserocr requests pyspellchecker six paytmchecksum paytmchecksum~=1.7.0 razorpay~=1.2.0 stripe~=2.56.0 braintree~=4.8.0  ShopifyAPI==8.2.0 boto3~=1.18.65 responses==0.20.0 rembg==2.0.29 pandas==1.5.1 SQLAlchemy==1.4.43 ShopifyAPI==8.2.0 boto3~=1.18.65 rembg==2.0.29 taxjar~=1.9.2

# Create a new user – (bench user)
sudo adduser frappe
sudo usermod -aG sudo frappe
su - frappe 

# Install Required Packages
# Install GIT
sudo apt-get install git -y

# Install Python
sudo apt-get install python3 python3-dev python3-setuptools python3-pip python3-distutils -y

# Install Python Virtual Environment
sudo apt-get install python3-venv -y

# Install Software Properties Common
sudo apt-get install software-properties-common -y

# Install Redis Server
sudo apt-get install redis-server -y

# Install other packages
sudo apt-get install xvfb libfontconfig wkhtmltopdf libmysqlclient-dev -y

# Install MariaDB
sudo apt install mariadb-server mariadb-client -y
# Configure MYSQL Server
sudo mysql_secure_installation
    Enter current password for root: (Enter your SSH root user password)
    Switch to unix_socket authentication [Y/n]: Y
    Change the root password? [Y/n]: Y
    It will ask you to set new MySQL root password at this step. This can be different from the SSH root user password.
    Remove anonymous users? [Y/n] Y
    Disallow root login remotely? [Y/n]: N
    This is set as N because we might want to access the database from a remote server for using business analytics software like Metabase / PowerBI / Tableau, etc.
    Remove test database and access to it? [Y/n]: Y
    Reload privilege tables now? [Y/n]: Y
# Edit MYSQL default config file
sudo nano /etc/mysql/my.cnf
# Masukan baris paling bawah:
[mysqld]
character-set-client-handshake = FALSE
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci

[mysql]
default-character-set = utf8mb4
# Restart the MYSQL Server
sudo service mysql restart

# Instal CURL
sudo apt install curl -y

# Install Node
curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash
source ~/.profile
nvm install --lts

# Install NPM
sudo apt-get install npm -y

# Install Yarn
sudo npm install -g yarn

# Install Frappe Bench
sudo pip3 install frappe-bench
# Initialize Frappe Bench
bench init --frappe-branch version-14 frappe-bench
# Switch directories into the Frappe Bench directory
cd frappe-bench
# Change user directory permissions
chmod -R o+rx /home/frappe
# Create a New Site
bench new-site example.com
# Install ERPNext and other Apps
bench get-app --branch version-14 erpnext
# Install all the apps on our site
bench --site example.com install-app erpnext
# Use site 
bench use example.com
# Start bench 
bench start

# Add frappe apps
# Payments
bench get-app payments
bench --site example.com install-app payments

# Health
bench get-app healthcare
bench --site example.com install-app healthcare

# HRMS
bench get-app hrms
bench --site example.com install-app hrms
cd apps/hrms
git fetch upstream version-14:version-14
git checkout version-14
cd ../..
bench --site example.com migrate
bench build

# Drive
bench get-app https://github.com/frappe/drive
bench --site example.com install-app drive
cd apps/drive
yarn dev
	URL http://ip-address:8000/drive
# LMS
bench get-app lms
bench --site example.com install-app lms

# Helpdesk
bench get-app https://github.com/frappe/desk
bench --site example.com install-app frappedesk
	URL http://ip-address:8000/frappedesk
	
# datatable
yarn add frappe-datatable or npm install frappe-datatable

# wiki
bench get-app https://github.com/frappe/wiki
bench --site example.com install-app wiki

# insights
bench get-app https://github.com/frappe/insights
bench --site example.com install-app insights
	URL http://ip-address:8000/insights
	
# ecommerce_integrations
bench get-app https://github.com/frappe/ecommerce_integrations.git
bench --site example.com install-app ecommerce_integrations

# gameplan 
bench get-app gameplan
cd apps/gameplan
yarn
	http://ip-addresst:8080
	
# education
bench get-app education
bench --site example.com install-app education

# hospitality
bench get-app hospitality
bench --site example.com install-app hospitality

# grantt
npm install frappe-gantt

# webshop
bench get-app webshop
bench --site example.com install-app webshop

# charts
npm install frappe-charts
# waba_integration

bench get-app NagariaHussain/waba_integration
bench --site example.com install-app waba_integration

# Chat 
bench get-app chat
bench --site example.com install-app chat

# biometric-attendance-sync-tool 
pip install requests pickleDB pyzk PyQt5 
bench get-app https://github.com/frappe/biometric-attendance-sync-tool.git
python3 -m venv venv
source venv/bin/activate
pip install -r requirements.txt 
OR
Step 1 – Create Sample Python Application (sudo nano /usr/bin/myscript.py)
Add the following content to the script. You can use your own Python script as per requirements:
#!/usr/bin/python3

import socket
s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
s.bind(("localhost", 9988))
s.listen(1)
 
while True:
    conn, addr = s.accept()
    data = conn.recv(1024)
    conn.close()
    my_function_that_handles_data(data)
Step 2 – Create a Systemd Service File (sudo nano /lib/systemd/system/myscript.service)
Add the following content to it. Change the Python script filename and location:
[Unit]
Description=Custom Python Service
After=multi-user.target
Conflicts=getty@tty1.service
 
[Service]
Type=simple
ExecStart=/usr/bin/python3 /usr/bin/myscript.py
StandardInput=tty-force
 
[Install]
WantedBy=multi-user.target
Step 3 – Enable and Start Service (sudo systemctl daemon-reload), (sudo systemctl enable myscript.service), (sudo systemctl start myscript.service)
Step 4 – Check Service Status (sudo systemctl status myscript.service)

# taxjar
bench get-app https://github.com/frappe/taxjar_integration.git
bench --site example.com install-app taxjar_integration

# event_streaming
bench get-app https://github.com/frappe/event_streaming.git
bench --site example.com install-app event_streaming

# nextcloud-integration
bench get-app https://github.com/frappe/nextcloud-integration.git
bench --site example.com install-app nextcloud_integration

# frappe_system_monitor
bench get-app https://github.com/mymi14s/frappe_system_monitor
bench --site example.com install-app frappe_system_monitor

# facility_management
bench get-app https://github.com/mymi14s/facility_management.git
bench --site example.com install-app facility_management

# POS-Awesome
bench get-app https://github.com/yrestom/POS-Awesome.git
bench setup requirements
bench build --app posawesome
bench restart
bench --site example.com install-app posawesome
bench --site example.com migrate

# meeting 
bench get-app https://github.com/inayatkh/meetings.git
bench --site example.com install-app meetings

# frappe_whatsapp
bench get-app https://github.com/shridarpatil/frappe_whatsapp
bench --site example.com install-app frappe_whatsapp
Get your whats app credentials : https://developers.facebook.com/docs/whatsapp/cloud-api/get-started

# pdf_on_submit
bench get-app https://github.com/tueit/pdf_on_submit.git
bench --site example.com install-app pdf_on_submit

# contract-payment
bench install-app https://github.com/morghim/contract-payment.git
bench --site example.com install-app contract-payment

# Frappe Telegram
pip install python-telegram-bot==13.7
pip intsall crossplane==0.5.7
bench get-app https://github.com/afarran3/frappe_telegram.git
bench --site example.com install-app frappe_telegram
