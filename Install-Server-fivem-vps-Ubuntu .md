# Fivem
# Step
1. sudo apt update && sudo apt upgrade -y
   Update Version
3. sudo apt install -y git wget curl screen unzip mysql-server ufw
   គឺត្រូវដើម្បីដំឡើង tools និង services ដែលត្រូវការ សម្រាប់ដំណើរការ FiveM Server លើ Ubuntu VPS
4. sudo mysql_secure_installation
   កំណត់សុវត្ថិភាព MySQL
   -Set root password? (Y/n): Y (បើមិនទាន់មាន)
   -Remove anonymous users? Y
   -Disallow root login remotely? Y
   -Remove test database? Y
   -Reload privilege tables? Y*/
5. sudo mysql
   ប្រសិនបើអ្នកមិនបានបង្កើត root password នៅ mysql_secure_installation,
6. sudo mysql -u root -p
   បង្កើត Database និង User សម្រាប់ FiveM
7. CREATE DATABASE fivemdb;
  CREATE USER 'fivemuser'@'localhost' IDENTIFIED BY 'your_db_password';
  GRANT ALL PRIVILEGES ON fivemdb.* TO 'fivemuser'@'localhost';
  FLUSH PRIVILEGES;
  EXIT;
8. mkdir -p /opt/fivem/server
  cd /opt/fivem/server
  -បង្កើត Folder សម្រាប់ FiveM Server


9. ufw allow 22/tcp     # SSH
ufw allow 30120/tcp  # FiveM
ufw allow 30120/udp  # FiveM
ufw allow 40120/tcp  # txAdmin
ufw enable
ufw status
