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
    image: mysql:8.0
    container_name: fivem-mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: rootpass
      MYSQL_DATABASE: fivemdb
      MYSQL_USER: fivem
      MYSQL_PASSWORD: fivempass
    volumes:
      - ./mysql:/var/lib/mysql
    ports:
      - "3306:3306"

  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    container_name: fivem-phpmyadmin
    restart: always
    environment:
      PMA_HOST: mysql
      MYSQL_ROOT_PASSWORD: rootpass
    ports:
      - "8080:80"

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
mkdir -p ~/fivem/server2
cd ~/fivem/server2

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





7. ufw allow 22/tcp     # SSH
ufw allow 30120/tcp  # FiveM
ufw allow 30120/udp  # FiveM
ufw allow 40120/tcp  # txAdmin
ufw enable
ufw status
