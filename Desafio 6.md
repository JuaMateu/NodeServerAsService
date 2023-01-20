history
   26  git clone https://github.com/roxsross/challenge-linux-bash
   28  sudo apt install nodejs npm
   36  curl -sL https://deb.nodesource.com/setup_14.x -o node_setup.sh
   37  sudo bash node_setup.sh
sudo apt install gcc g++ make
sudo apt install -y nodejs
sudo adduser nodejs
sudo nano /lib/systemd/system/devops.service
node server.js
sudo apt install npm
npm init
vim package.json
sudo chwon nodejs:nodejs server.js
ls -larth
systemctl enable devops.service
sudo chmod 755 server.js
systemctl status devops.service
 
mv challenge-linux-bash /home
sudo chmod nodejs:nodejs challenge-linux-bash/
sudo chown nodejs:nodejs challenge-linux-bash/

sudo vim /lib/systemd/system/devops.service
sudo systemctl enable devops.service
systemctl status devops.service
reboot
sudo reboot
```jmateu@ubuntuserver2:~$ sudo cat /lib/systemd/system/devops.service
[sudo] password for jmateu: 
[Unit]
Description=Balanceo para desafio Final
Documentation=https://github.com/roxsross/challenge-linux-bash
After=network.target

[Service]
Enviroment=NODE_PORT=3000
Type=simple
User=jmateu
WorkingDirectory=//home/challenge-linux-bash
ExecStart=/usr/bin/node /home/challenge-linux-bash/server.js
Restart=on-failure

[Install]
WantedBy=multi-user.target```

