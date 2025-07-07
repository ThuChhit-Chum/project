# Fivem
# Step
# 1.
sudo apt update && sudo apt upgrade -y
      Update Version
   
# 3.
sudo apt install curl wget git unzip screen -y
   គឺត្រូវដើម្បីដំឡើង tools និង services ដែលត្រូវការ សម្រាប់ដំណើរការ FiveM Server លើ Ubuntu VPS
   
# 4. 
sudo apt install ca-certificates curl gnupg -y
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y

# ត្រួតពិនិត្យ docker
docker --version

# 5.
mkdir -p ~/fivem-docker/mysql
cd ~/fivem-docker
nano docker-compose.yml

# 6.
version: '3.8'

services:
  mysql:
    image: mariadb
    container_name: fivem-mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: "Chhit$2605"
      MYSQL_DATABASE: siemreapcity
      MYSQL_USER: siemreapcity
      MYSQL_PASSWORD: siemreapcity  
    volumes:
      - ./mysql:/var/lib/mysql
    ports:
      - "8989:3306"

  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    container_name: fivem-phpmyadmin
    restart: always
    environment:
      PMA_HOST: mysql
      MYSQL_ROOT_PASSWORD: Chhit$2605
    ports:
      - "8899:80"

- docker compose up -d
- docker compose down

# 6. setup fivem
- mkdir -p ~/fivem/server
- cd ~/fivem/server

- curl -s https://runtime.fivem.net/artifacts/fivem/build_proot_linux/master/ > builds.html

- grep -Po '7290-[0-9a-f]+' builds.html | sort -u

- wget https://runtime.fivem.net/artifacts/fivem/build_proot_linux/master/7290-a654bcc2adfa27c4e020fc915a1a6343c3b4f921/fx.tar.xz -O fx.tar.xz
- nano start.sh:
#!/bin/bash
cd ~/fivem/server
./run.sh +exec server.cfg

# 8.
chmod +x start.sh

# 7. 
   cd ~/fivem/server
   ./run.sh



sv_hostname "Siem Reap RP Server 1"
sets sv_projectName "Siem Reap City"
sets sv_projectDesc "Server #1 - Cambodia RP"

set mysql_connection_string "mysql://fivem:fivempass@127.0.0.1/siemreapcitytest"

# Enable OneSync
set onesync on

# Server token
sv_licenseKey "cfxk_1iOKyQbHUbU56vQdYTryF_40RMjz"
sv_maxclients 48

#!/bin/bash
cd ~/fivem/server1
./run.sh +set serverProfile server1 +set txAdminPort 40121 +set sv_licenseKey "cfxk_1iOKyQbHUbU56vQdYTryF_40RMjz" +set sv_port 30121 +exec server.cfg



# Create folder
mkdir -p ~/fivem/server1
cd ~/fivem/server1

# Download and extract FXServer build
wget https://runtime.fivem.net/artifacts/fivem/build_proot_linux/master/7290-a654bcc2adfa27c4e020fc915a1a6343c3b4f921/fx.tar.xz -O fx.tar.xz
tar -xf fx.tar.xz && rm fx.tar.xz

# Make run.sh executable
chmod +x run.sh

nano ~/fivem/server2/start.sh

#!/bin/bash
cd ~/fivem/server2
./run.sh +set serverProfile server2 +set txAdminPort 40122 +set sv_port 30122

chmod +x ~/fivem/server2/start.sh

rm -rf ~/fivem/server2/txData

~/fivem/server2/start.sh



# ដំឡើង screen (បើមិនទាន់មាន)
 - sudo apt update
 - sudo apt install screen -y
# បើក FXServer នៅក្នុង screen
 - screen -S fxserver1
 - cd ~/fivem/server1
 - ./start.sh

# ចាកចេញពី screen ដោយមិនបិទ FXServer
 - Ctrl + A  បន្ទាប់បញ្ចក់ D

# ចូលមកវិញ
 - screen -r fxserver1






7. ufw allow 22/tcp     # SSH
ufw allow 30120/tcp  # FiveM
ufw allow 30120/udp  # FiveM
ufw allow 40120/tcp  # txAdmin
ufw enable
ufw status







🧱 STEP ONE: Create Servers One-by-One
This is perfect if you want to:
-Set up and test each server individually
-Customize each one step-by-step
✅ 1. Prepare VPS (Only Once)

      sudo apt update && sudo apt upgrade -y
      sudo apt install curl wget git unzip screen nano gnupg ca-certificates lsb-release -y

✅ 2. Install Docker & Docker Compose (Once)

      sudo install -m 0755 -d /etc/apt/keyrings
      curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
      
      echo \
      "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
      $(lsb_release -cs) stable" | \
      sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
      
      sudo apt update
      sudo apt install docker-ce docker-ce-cli containerd.io docker-compose-plugin -y

✅ 3. Run MySQL + phpMyAdmin (Shared DB for all servers)

      mkdir -p ~/fivem-docker/mysql
      cd ~/fivem-docker
      nano docker-compose.yml

- Paste:

version: '3.8'

services:
  mysql:
    image: mariadb
    container_name: fivem-mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: ThouChhit$2605
      MYSQL_DATABASE: siemreapcity
      MYSQL_USER: siemreapcity
      MYSQL_PASSWORD: Chhit$2605
    volumes:
      - ./mysql:/var/lib/mysql
    ports:
      - "8989:3306"

  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    container_name: fivem-phpmyadmin
    restart: always
    environment:
      PMA_HOST: mysql
      MYSQL_ROOT_PASSWORD: ThouChhit$2605
    ports:
      - "8899:80"


                  
Start:

      docker compose up -d
- Access PHPMyAdmin:
http://your-vps-ip:8899/

✅ 4. Download FXServer Build (One Time)

mkdir -p ~/fivem/base
cd ~/fivem/base

wget https://runtime.fivem.net/artifacts/fivem/build_proot_linux/master/7290-a654bcc2adfa27c4e020fc915a1a6343c3b4f921/fx.tar.xz
tar -xf fx.tar.xz
rm fx.tar.xz
chmod +x run.sh


✅ 5. Create First Server (Server1)

      mkdir -p ~/fivem/siemreapcity
      cp -r ~/fivem/base/* ~/fivem/siemreapcity
Create start.sh:

      nano ~/fivem/siemreapcity/start.sh
Paste:
      
#!/bin/bash
cd ~/fivem/siemreapcity
./run.sh +set serverProfile siemreapcity +set txAdminPort 40121


Make executable:

      chmod +x ~/fivem/siemreapcity/start.sh
      
Run:

      screen -S siemreapcity
      ~/fivem/siemreapcity/start.sh
      screen -r siemreapcity

- Open browser:
http://your-vps-ip:40121/

➡️ Use txAdmin Wizard:

Set password

Register server

Add license key

Configure MySQL connection (optional)

Done!

✅ 6. Repeat for Server 2–6 (Change ports)
Server	Folder	txAdmin Port
1	server1	40121
2	server2	40122
3	server3	40123
4	server4	40124
5	server5	40125
6	server6	40126

Follow same method, change:

serverProfile

txAdminPort

screen name

Use separate license keys from keymaster


🧱 STEP TWO: Automatically Setup 6 Servers on One VPS
Here’s how to automate it:
✅ 1. Create Script

      mkdir -p ~/fivem/setup
      nano ~/fivem/setup/create_servers.sh

Paste this:

      #!/bin/bash
      
      echo "Creating 6 FiveM servers with txAdmin setup..."
      
      for i in {1..6}; do
        echo "Creating server$i..."
        mkdir -p ~/fivem/server$i
        cp -r ~/fivem/base/* ~/fivem/server$i
      
        cat > ~/fivem/server$i/start.sh <<EOF
      #!/bin/bash
      cd ~/fivem/server$i
      ./run.sh +set serverProfile server$i +set txAdminPort 4012$i
      EOF
      
        chmod +x ~/fivem/server$i/start.sh
      
        echo "Start server$i using: screen -S fxserver$i ~/fivem/server$i/start.sh"
      done
      
Make it executable:

      chmod +x ~/fivem/setup/create_servers.sh

Run it:

      ~/fivem/setup/create_servers.sh

✅ 2. Start All Servers
Start each in its own screen:

      screen -S fxserver1 ~/fivem/server1/start.sh
      screen -S fxserver2 ~/fivem/server2/start.sh
      screen -S fxserver3 ~/fivem/server3/start.sh
      screen -S fxserver4 ~/fivem/server4/start.sh
      screen -S fxserver5 ~/fivem/server5/start.sh
      screen -S fxserver6 ~/fivem/server6/start.sh

Then open these URLs in browser to set up via txAdmin:

Server	txAdmin URL
1	http://your-ip:40121
2	http://your-ip:40122
3	http://your-ip:40123
4	http://your-ip:40124
5	http://your-ip:40125
6	http://your-ip:40126

✅ 3. Open Firewall Ports

sudo ufw allow OpenSSH
sudo ufw allow 40121:40126/tcp
sudo ufw allow 30121:30126/tcp
sudo ufw allow 30121:30126/udp
sudo ufw enable

✅ Final Folder Structure

      ~/fivem
      ├── base/
      ├── docker-compose.yml
      ├── server1/
      ├── server2/
      ├── server3/
      ├── server4/
      ├── server5/
      └── server6/
