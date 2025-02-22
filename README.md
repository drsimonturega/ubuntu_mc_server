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
```sudo adduser --system --home /opt/minecraft minecraft \
sudo groupadd minecraft \
sudo adduser minecraft minecraft```
```sudo chown -R minecraft:minecraft /opt/minecraft```
```echo '[Unit]\
Description=start and stop the minecraft-server\

[Service]\
WorkingDirectory=/opt/minecraft\
User=minecraft\
Group=minecraft\
Restart=on-failure\
RestartSec=20 5\
ExecStart=/usr/bin/java -Xmx16384M -Xms16300M -jar server.jar --nogui\

[Install]\
WantedBy=multi-user.target' | sudo tee /etc/systemd/system/minecraft.service```
```sudo systemctl daemon-reload```
```sudo systemctl enable minecraft.service```
```sudo systemctl restart minecraft.service```
```sudo journalctl -fu minecraft.service```

## Installing Minecraft client
The deb file was downloaded from ```https://www.minecraft.net/en-us/download```
from ```/home/simon/Downloads```
```mv Minecraft.deb /home/simon/Minecraft.deb```
```cd ..```
```sudo dpkg -i Minecraft.deb```
Oh no we get missing depandances possibly not got right Java installed, we will solve these missing dependances for now.
```dpkg: dependency problems prevent configuration of minecraft-launcher:\
 minecraft-launcher depends on default-jre; however:\
  Package default-jre is not installed.\
 minecraft-launcher depends on libgdk-pixbuf2.0-0 (>= 2.22.0); however:\
  Package libgdk-pixbuf2.0-0 is not installed.```
```sudo apt install default-jre```
```The following packages have unmet dependencies.\
 default-jre : Depends: default-jre-headless (= 2:1.11-72build2) but it is not going to be installed\
               Depends: openjdk-11-jre but it is not going to be installed\
 minecraft-launcher : Depends: libgdk-pixbuf2.0-0 (>= 2.22.0) but it is not going to be installed\
E: Unmet dependencies. Try 'apt --fix-broken install' with no packages (or specify a solution).```
```sudo apt --fix-broken install```
This solved both issues.

now to try minecraft-launcher
```minecraft-launcher``







## References 
https://minecraft.wiki/w/Tutorial:Setting_up_a_Java_Edition_server
https://www.minecraft.net/en-us/download/server
https://jmcglock.substack.com/p/how-to-run-a-minecraft-server-on
