## softether-install
Set up SoftEther VPN server on Debian, Ubuntu, Fedora, CentOS or Arch Linux.

#0 Change ssh port
```bash
nano /etc/ssh/sshd_config
```



#1 Update the ubuntu serverserver
```bash
apt update && apt upgrade -y
```



#2 Install dependency
```bash
apt-get -y install build-essential wget make curl gcc  wget zlib1g-dev tzdata git libreadline-dev libncurses-dev libssl-dev
```



#3 Download Sofether installer file
```bash
wget https://github.com/SoftEtherVPN/SoftEtherVPN_Stable/releases/download/v4.41-9782-beta/softether-vpnserver-v4.41-9782-beta-2022.11.17-linux-x64-64bit.tar.gz
```



#4 Extract the installer file & remove installer file
```bash
tar xzf softether-vpnserver-v4.41-9782-beta-2022.11.17-linux-x64-64bit.tar.gz
rm softether-vpnserver-v4.41-9782-beta-2022.11.17-linux-x64-64bit.tar.gz
```



#5 Po to the program folder
```bash
cd vpnserver
```



#6 Compile the program
```bash
make
```



#7 Back to the main directory
```bash
cd ..
```



#8 Move vpnserver to new folder
```bash
mv vpnserver /usr/local
```


#9 Change directory to new folder
```bash
cd /usr/local/vpnserver/
```



#10 Access control
```bash
chmod 600 *
chmod 700 vpnserver vpncmd
```



#11 Start vpnserver
```bash
./vpnserver start
```


#12 Open command line management panel
```bash
./vpncmd
```


#13 Set password for softether panel
```bash
serverPasswordSet
```


#14 Preparing the service (copy and paste the entire command below)
```bash
sudo cat >> /lib/systemd/system/vpnserver.service << EOF
[Unit]
Description=SoftEther VPN Server
After=network.target
[Service]
Type=forking
ExecStart=
ExecStart=/usr/local/vpnserver/vpnserver start
ExecStop=/usr/local/vpnserver/vpnserver stop
[Install]
WantedBy=multi-user.target
EOF
```


#15 Enabling and start vpnserver
```bash
systemctl enable vpnserver
systemctl start vpnserver
```


#16 Reboot system
```bash
reboot
```

#16 Check vpnserver status
```bash
systemctl status vpnserver
```

#18 Setup firewall settings and enabling firewall
```bash
ufw allow 2222
ufw allow 1194
ufw allow 443
ufw allow 992
ufw allow 1701
ufw allow 5555
ufw allow 500
ufw allow 4500
ufw allow 500,4500/udp
ufw allow 80
ufw enable
```


#19 Enable IPv4 forwadring 
```bash
echo 1 > /proc/sys/net/ipv4/ip_forward
cat /proc/sys/net/ipv4/ip_forward
```


#20 Install google BBR
```bash
wget https://raw.githubusercontent.com/teddysun/across/master/bbr.sh
chmod +x bbr.sh
./bbr.sh
```
```bash
sysctl -p
reboot
```
