# ubuntu_mc_server
Setting up Java Minecraft Server on an ubuntu PC
## Folders and dependances
```sudo apt install openjdk-21-jdk-headless```
```sudo mkdir /opt/minecraft'''
```wget https://piston-data.mojang.com/v1/objects/4707d00eb834b446575d89a61a11b5d548d8c001/server.jar```
```sudo mv server.jar /opt/minecraft```
```cd /opt/minecraft```
```sudo java -jar server.jar --nogui &```
```sleep 10```
```pkill -f server.jar```
```sudo java -jar server.jar --nogui &```
```echo 'eula=true' | sudo tee eula.txt```
```sudo adduser --system --home /opt/minecraft minecraft
sudo groupadd minecraft
sudo adduser minecraft minecraft```
```sudo chown -R minecraft:minecraft /opt/minecraft```
```echo '[Unit]
Description=start and stop the minecraft-server

[Service]
WorkingDirectory=/opt/minecraft
User=minecraft
Group=minecraft
Restart=on-failure
RestartSec=20 5
ExecStart=/usr/bin/java -Xmx16384M -Xms16300M -jar server.jar --nogui

[Install]
WantedBy=multi-user.target' | sudo tee /etc/systemd/system/minecraft.service```
```sudo systemctl daemon-reload```
```sudo systemctl enable minecraft.service```
```sudo systemctl restart minecraft.service```
```sudo journalctl -fu minecraft.service```




## References 
https://minecraft.wiki/w/Tutorial:Setting_up_a_Java_Edition_server
https://www.minecraft.net/en-us/download/server
https://jmcglock.substack.com/p/how-to-run-a-minecraft-server-on
