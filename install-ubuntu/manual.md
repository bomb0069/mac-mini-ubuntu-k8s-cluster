# Manual Install Ubuntu (Mac-mini)

## Overviews

- [Manual Install Ubuntu (Mac-mini)](#manual-install-ubuntu-mac-mini)
  - [Overviews](#overviews)
  - [Create Ubuntu Installer Boot Disk](#create-ubuntu-installer-boot-disk)
  - [Install Ubuntu Server](#install-ubuntu-server)
  - [Setup Wireless Network](#setup-wireless-network)

## Create Ubuntu Installer Boot Disk

reference [Create a bootable USB stick on macOS](https://ubuntu.com/tutorials/create-a-usb-stick-on-macos)

## Install Ubuntu Server

reference [Install Ubuntu Server](https://ubuntu.com/tutorials/install-ubuntu-server)

## Setup Wireless Network

- Setup Wireless Adaptor

  1. run command `ifconfig` it's should be command not found

     ```shell
     ifconfig
     ```
  
     ```shell
     Command 'ifconfig' not found, but ca be installed with
 
     sudo apt install net-tools
     ```

  2. install `net-tools` to enabled `ifconfig` command

     ```shell
     sudo apt install net-tools
     ```
  
  3. get network information from `ifconfig` command it's should not been wireless connections

     ```shell
      ifconfig
     ```
  
     ```shell
      enp3s0f0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
            inet 192.168.2.2  netmask 255.255.255.0  broadcast 192.168.2.255
            inet6 fd5a:3360:ca7:ece1:3ac9:86ff:fe04:e157  prefixlen 64  scopeid 0x0<global>
            inet6 fe80::3ac9:86ff:fe04:e157  prefixlen 64  scopeid 0x20<link>
            ether 38:c9:86:04:e1:57  txqueuelen 1000  (Ethernet)
            RX packets 405  bytes 276760 (276.7 KB)
            RX errors 0  dropped 0  overruns 0  frame 0
            TX packets 258  bytes 39638 (39.6 KB)
            TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
            device interrupt 19  

      lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
            inet 127.0.0.1  netmask 255.0.0.0
            inet6 ::1  prefixlen 128  scopeid 0x10<host>
            loop  txqueuelen 1000  (Local Loopback)
            RX packets 190  bytes 14616 (14.6 KB)
            RX errors 0  dropped 0  overruns 0  frame 0
            TX packets 190  bytes 14616 (14.6 KB)
            TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
     ```

  4. Run `iwconfig` command  it's should be command not found

     ```shell
     iwconfig
     ```
  
     ```shell
     Command 'iwconfig' not found, but can be installed with:

     sudo apt install wireless-tools
     ```

  5. install `wireless-tools` to enabled `iwconfig` command

     ```shell
     sudo apt install wireless-tools
     ```

  6. Run `iwconfig` command to find the name of your wireless interface. it's still not found wireless interface
  
     ```shell
     iwconfig
     ```
  
     ```shell
     enp3s0f0  no wireless extensions.

     lo        no wireless extensions.
     ```

  7. install BCM Wifi driver for Mac-Mini

     ```shell
     sudo apt-get install --reinstall bcmwl-kernel-source
     ```

  8. Run `iwconfig` command again. it should be found wireless interface
  
     ```shell
     iwconfig
     ```
  
     ```shell
     enp3s0f0  no wireless extensions.

     wlp2s0    IEEE 802.11  ESSID:off/any  
               Mode:Managed  Access Point: Not-Associated   
               Retry short limit:7   RTS thr:off   Fragment thr:off
               Power Management:off
          
     lo        no wireless extensions.
     ```

  9. `wlan0` used to be a common name for wireless network interface on Linux systems without Systemd. Because Ubuntu uses Systemd, you are going to find that your wireless network interface is named something like `wlp2s0`. You can also see that it’s not associated with any access point right now.

     ```shell
     iwconfig
     ```
  
     ```shell
     wlp2s0    IEEE 802.11  ESSID:off/any  
               Mode:Managed  [Access Point: Not-Associated]
               Retry short limit:7   RTS thr:off   Fragment thr:off
               Power Management:off
     lo        no wireless extensions.

     enp3s0f0  no wireless extensions.
     ```

  10. Establish a Wireless Connection. First, determine the name of the WiFi interface:

      ```shell
      nmcli d
      ```

      ```shell
      Command 'nmcli' not found, but can be installed with:
      
      sudo apt install network-manager
      ```

  11. Install Network-Manager to enable `nmcli` commands.

      ```shell
      sudo apt install network-manager
      ```

  12. Make sure the WiFi radio is on (which is its default state):

      ```shell
      nmcli r wifi on
      ```

  13. you will see wireless information when run `ifconfig` command
  
      ```shell
      ifconfig
      ```

      ```shell
      enp3s0f0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
            inet 192.168.2.2  netmask 255.255.255.0  broadcast 192.168.2.255
            inet6 fd5a:3360:ca7:ece1:3ac9:86ff:fe04:e157  prefixlen 64  scopeid 0x0<global>
            inet6 fe80::3ac9:86ff:fe04:e157  prefixlen 64  scopeid 0x20<link>
            ether 38:c9:86:04:e1:57  txqueuelen 1000  (Ethernet)
            RX packets 46613  bytes 68185749 (68.1 MB)
            RX errors 0  dropped 0  overruns 0  frame 0
            TX packets 7256  bytes 723057 (723.0 KB)
            TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
            device interrupt 19  

      lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
            inet 127.0.0.1  netmask 255.0.0.0
            inet6 ::1  prefixlen 128  scopeid 0x10<host>
            loop  txqueuelen 1000  (Local Loopback)
            RX packets 218  bytes 17336 (17.3 KB)
            RX errors 0  dropped 0  overruns 0  frame 0
            TX packets 218  bytes 17336 (17.3 KB)
            TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

      wlp2s0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
            ether 78:9f:70:79:c5:3e  txqueuelen 1000  (Ethernet)
            RX packets 0  bytes 0 (0.0 B)
            RX errors 0  dropped 0  overruns 0  frame 0
            TX packets 0  bytes 0 (0.0 B)
            TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
            device interrupt 18
      ```

- Manual Connect to Wi-fi Netrwork

  1. Then find your wireless network name by scanning nearby networks with the command below. Replace `wlp2s0` with your own wireless interface name. ESSID is the network name identifier.

     ```shell
     sudo iwlist wlp2s0 scan | grep ESSID
     ```

     ```shell
         ESSID:"WIFI_Network_Home"
         ESSID:"WIFI_Network_Home_5g"
     ```

  2. Now install wpa_supplicant on Ubuntu 18.04/20.04 from the default software repository.

     ```shell
     sudo apt install wpasupplicant
     ```

  3. We need to create a file named `wpa_supplicant.conf` using the `wpa_passphrase` utility. `wpa_supplicant.conf` is the configuration file describing all networks that the user wants the computer to connect to. Run the following command to create this file. Replace ESSID and Wi-Fi passphrase with your own.

     ```shell
     wpa_passphrase ${your-ESSID} ${your-wifi-passphrase} | sudo tee /etc/wpa_supplicant.conf
     ```

     ```shell
     network={
        ssid="${your-ESSID}"
        #psk="${your-wifi-passphrase}"
        psk=24f508ef2946032b65ed981fae766c657cff471945086abb55c9a02d09a4bf08
     }
     ```

     The output of wpa_passphrase command will be piped to tee, and then written to the /etc/wpa_supplicant.conf file.

  4. Now use the following command to connect your wireless card to wireless access point.

     ```shell
     sudo wpa_supplicant -c /etc/wpa_supplicant.conf -i wlp2s0
     ```

     The following output indicates your wireless card is successfully connected to an access point.

     ```shell
     Successfully initialized wpa_supplicant
     wlp2s0: Trying to associate with 70:f8:2b:cf:c4:d5 (SSID='${your-ESSID}' freq=5200 MHz)
     wlp2s0: Associated with 70:f8:2b:cf:c4:d5
     wlp2s0: CTRL-EVENT-SUBNET-STATUS-UPDATE status=0
     wlp2s0: CTRL-EVENT-REGDOM-CHANGE init=COUNTRY_IE type=COUNTRY alpha2=US
     wlp2s0: WPA: Key negotiation completed with 70:f8:2b:cf:c4:d5 [PTK=CCMP GTK=TKIP]
     wlp2s0: CTRL-EVENT-CONNECTED - Connection to 70:f8:2b:cf:c4:d5 completed [id=0 id_str=]
     ```

     Note that if you are using Ubuntu desktop edition, then you need to stop Network Manager with the following command, otherwise it will cause a connection problem when using wpa_supplicant.

  5. open `new terminal` to check wifi connection

     ```shell
     iwconfig
     ```

     ```shell
     wlp2s0    IEEE 802.11  ESSID:"${your-ESSID}"  
               Mode:Managed  Frequency:5.2 GHz  Access Point: 70:F8:2B:CF:C4:D5   
               Retry short limit:7   RTS thr:off   Fragment thr:off
               Power Management:off

     lo        no wireless extensions.

     enp3s0f0  no wireless extensions.
     ```

  6. Stop Network Manager with the following command

     ```shell
     sudo systemctl stop NetworkManager
     ```

  7. Disable NetworkManager auto-start at boot time by executing the following command.

     ```shell
     sudo systemctl disable NetworkManager-wait-online NetworkManager-dispatcher NetworkManager
     ```

     ```shell
     Removed /etc/systemd/system/dbus-org.freedesktop.nm-dispatcher.service.
     Removed /etc/systemd/system/multi-user.target.wants/NetworkManager.service.
     Removed /etc/systemd/system/network-online.target.wants/NetworkManager-wait-online.service.
     ```

  8. By default, wpa_supplicant runs in the foreground. If the connection is completed, then open up another terminal window and run

     ```shell
     iwconfig
     ```

     ```shell
     wlp2s0    IEEE 802.11  ESSID:off/any  
               Mode:Managed  Frequency:5.2 GHz  Access Point: 70:F8:2B:CF:C4:D5   
               Retry short limit:7   RTS thr:off   Fragment thr:off
               Power Management:off

     lo        no wireless extensions.

     enp3s0f0  no wireless extensions.
     ```

  9. go back to `original terminal` and use `Ctrl + C` to stop current `wpa_supplicant` process

  10. run it in the background by adding the -B flag.

      ```shell
      sudo wpa_supplicant -B -c /etc/wpa_supplicant.conf -i wlp2s0
      ```

      ```shell
      Successfully initialized wpa_supplicant
      ```

  11. Although we’re authenticated and connected to a wireless network, we don’t have an IP address yet. To obtain a private IP address from DHCP server, use the following command:

      ```shell
      sudo dhclient wlp2s0
      ```

  12. Now your wireless interface has a private IP address, which can be shown with:

      ```shell
      ip addr show wlp2s0
      ```

      ubuntu dhclient obtain private ip addres

      ```shell
      3: wlp2s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
         link/ether 78:9f:70:79:d3:48 brd ff:ff:ff:ff:ff:ff
         inet 192.168.1.57/24 brd 192.168.1.255 scope global dynamic wlp2s0
            valid_lft 86375sec preferred_lft 86375sec
         inet6 2001:fb1:20:dc97:f035:d516:fdc0:962d/64 scope global temporary dynamic 
            valid_lft 259153sec preferred_lft 86037sec
         inet6 2001:fb1:20:dc97:7a9f:70ff:fe79:d348/64 scope global dynamic mngtmpaddr 
            valid_lft 259153sec preferred_lft 172753sec
         inet6 fe80::7a9f:70ff:fe79:d348/64 scope link 
            valid_lft forever preferred_lft forever
      ```

      `Note:` Now you can access the Internet. To release the private IP address, run

      ```shell
      sudo dhclient wlp2s0 -r
      ```

- Setup Auto-Connect to Wi-fi At Boot Time

  To automatically connect to wireless network at boot time, we need to edit the `wpa_supplicant.service` file. It’s a good idea to copy the file from `/lib/systemd/system/` directory to `/etc/systemd/system/` directory, then edit the file content, because we don’t want a newer version of wpa_supplicant to override our modifications.

  1. Copy `wpa_supplicant.service` from lib folder

     ```shell
     sudo cp /lib/systemd/system/wpa_supplicant.service /etc/systemd/system/wpa_supplicant.service
     ```

  2. Edit the file with a command-line text editor, such as VI, Nano.

     ```shell
     sudo vi /etc/systemd/system/wpa_supplicant.service
     ```

     Find the following line.

     ```properties
     [Unit]
     Description=WPA supplicant
     Before=network.target
     After=dbus.service
     Wants=network.target
     IgnoreOnIsolate=true

     [Service]
     Type=dbus
     BusName=fi.w1.wpa_supplicant1
     ExecStart=/sbin/wpa_supplicant -u -s -O /run/wpa_supplicant # <--- Line to be change

     [Install]
     WantedBy=multi-user.target
     Alias=dbus-fi.w1.wpa_supplicant1.service
     ```

  3. Change it to the following.
  
     Here we added the configuration file and the wireless interface name to the ExecStart command.

     ```properties
     ExecStart=/sbin/wpa_supplicant -u -s -c /etc/wpa_supplicant.conf -i wlp2s0
     ```

     It’s recommended to always try to restart wpa_supplicant when failure is detected. Add the following right below the ExecStart line.

     ```properties
     Restart=always
     ```

     If you can find the following line in this file, comment it out (Add the # character at the beginning of the line).

     ```properties
     Alias=dbus-fi.w1.wpa_supplicant1.service
     ```

     Save and close the file. Updated version should be

     ```properties
     [Unit]
     Description=WPA supplicant
     Before=network.target
     After=dbus.service
     Wants=network.target
     IgnoreOnIsolate=true
     
     [Service]
     Type=dbus
     BusName=fi.w1.wpa_supplicant1
     ExecStart=/sbin/wpa_supplicant -u -s -c /etc/wpa_supplicant.conf -i wlp2s0
     Restart=always
     
     [Install]
     WantedBy=multi-user.target
     #Alias=dbus-fi.w1.wpa_supplicant1.service
     ```

  4. Then reload systemd and Enable wpa_supplicant service to start at boot time.

     ```shell
     sudo systemctl daemon-reload
     ```

     Enable wpa_supplicant service to start at boot time.

     ```shell
     sudo systemctl enable wpa_supplicant.service
     ```

  5. Start dhclient at boot time to obtain a private IP address from DHCP server. This can be achieved by creating a systemd service unit for dhclient.

     Edit `dhclient.service`

     ```shell
     sudo vi /etc/systemd/system/dhclient.service
     ```

     Put the following text into the file.

     ```shell
     [Unit]
     Description= DHCP Client
     Before=network.target
     After=wpa_supplicant.service

     [Service]
     Type=forking
     ExecStart=/sbin/dhclient wlp2s0 -v
     ExecStop=/sbin/dhclient wlp2s0 -r
     Restart=always
     
     [Install]
     WantedBy=multi-user.target
     ```

     Save and close the file. Then enable this service.

     ```shell
     sudo systemctl enable dhclient.service
     ```

  6. Restart Ubuntu Server to Take effect

     ```shell
     sudo shutdown -r now
     ```
  
- Reduced Boot time when `A start job is running for Wait for Network to be Configured` still waiting 2 minutes

  1. Run `ifconfig` command to find the name of your ethernet interface.

     ```shell
     ifconfig
     ```

     ```shell
     enp3s0f0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
           ether 38:c9:86:04:e1:57  txqueuelen 1000  (Ethernet)
           RX packets 0  bytes 0 (0.0 B)
           RX errors 0  dropped 0  overruns 0  frame 0
           TX packets 0  bytes 0 (0.0 B)
           TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
           device interrupt 19  

     lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
           inet 127.0.0.1  netmask 255.0.0.0
           inet6 ::1  prefixlen 128  scopeid 0x10<host>
           loop  txqueuelen 1000  (Local Loopback)
           RX packets 516  bytes 37252 (37.2 KB)
           RX errors 0  dropped 0  overruns 0  frame 0
           TX packets 516  bytes 37252 (37.2 KB)
           TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

     wlp2s0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
     ...
     ```

  2. Run `ls` to find yaml configuration file in `/etc/netplan`

     ```shell
     ls -lt /etc/netplan
     
     total 4
     -rw-r--r-- 1 root root 140 Oct  7 09:27 00-installer-config.yaml
     ```
  
  3. Update internet config by add `optional` into ethernet interface

     ```shell
     sudo vi /etc/netplan/00-installer-config.yaml
     ```

     ```yaml
     network:
        ethernets:
           enp3s0f0:  # <-- Network interface name
                dhcp4: true
                optional: true # <-- add optional
        version: 2
     ```

  4. Restart Ubuntu Server to Take effect

     ```shell
     sudo shutdown -r now
     ```

- reference

  - [Configure WiFi Connections](https://ubuntu.com/core/docs/networkmanager/configure-wifi-connections)
  - [Installing Broadcom Wireless Drivers for "Chip ID": BCM4360, "PCI-ID": 14e4:43a0 (rev 03) on Ubuntu 14.04](https://askubuntu.com/questions/592555/installing-broadcom-wireless-drivers-for-chip-id-bcm4360-pci-id-14e443a0)
  - [Connect to Wi-Fi From Terminal on Ubuntu 18.04/20.04 with WPA Supplicant](https://www.linuxbabe.com/ubuntu/connect-to-wi-fi-from-terminal-on-ubuntu-18-04-19-04-with-wpa-supplicant)
  - [แก้ไขบู๊ต Ubuntu 18.04 ช้า ค้างที่ข้อความ A start job is running for Wait for Network to be Configured](https://spalinux.com/2019/01/fix-slow-boot-ubuntu-18-04-with-a-start-job-is-running-for-wait-for-network-to-be-configured)

- may be help

  - [Wireless connection troubleshooter](https://help.ubuntu.com/stable/ubuntu-help/net-wireless-troubleshooting-hardware-check.html.en)
  - [How to Enable Wi-Fi on MacBook, Mac Mini, MacBook Air for Ubuntu/Linux OS](https://gist.github.com/niftylettuce/5619c2be9906bcbd893e1e1a25b9d795)
