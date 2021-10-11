# Automatic Installation for Ubuntu 20.04

เนื่องจากผมต้องติดตั้ง Ubuntu Server ลงบน MAC-mini ที่ผมมีทั้ง 7 เครื่อง แถมอาจจะต้อง ล้างเครื่องลงใหม่บ่อย ๆ เพื่อให้สามารถทดลอง Cluster ได้ในหลาย ๆ รูปแบบ และใช้เวลาในการ Install Ubuntu ให้สั้นที่สุด ลดปัญหาจากการกรอกข้อมูลแบบ Manual ให้มาที่สุด แล้วผมก็เจอวิธีการที่สามารถทำได้อยู่ 2 วิธี คือ การใช้ [preseed](https://help.ubuntu.com/lts/installation-guide/s390x/apb.html) และ การใช้ [Automated Server Installs](https://ubuntu.com/server/docs/install/autoinstall) (สำหรับ Ubuntu Server 20.04 ขึ้นไป) จากที่ลองศึกษาดู ถึงแม้ว่า Automated Server Installs พึ่งมาใน Version ล่าสุด แต่ก็เป็นวิธีการที่น่าสนใจ ผมเลยจะลองใช้กับ Project นี้

- [Automatic Installation for Ubuntu 20.04](#automatic-installation-for-ubuntu-2004)
  - [Create Ubuntu Installer Boot Disk with UUByte ISO Editor](#create-ubuntu-installer-boot-disk-with-uubyte-iso-editor)
  - [Setup Automatic Installs to Boot Disk](#setup-automatic-installs-to-boot-disk)
  - [Install Ubuntu Server](#install-ubuntu-server)
  - [Setup Wireless Network](#setup-wireless-network)
  - [Reference](#reference)

## Create Ubuntu Installer Boot Disk with UUByte ISO Editor

เนื่องจากการสร้าง Automatic Installer Boot Disk จำเป็นจะต้องมีการแก้ไข File ที่อยู่ใน ฺUSB Boot Disk ด้วย ซึ่งถ้าใช้ขั้นตอน แบบเดียวกับ [Create a bootable USB stick on macOS](https://ubuntu.com/tutorials/create-a-usb-stick-on-macos) ที่อยู่ใน Official Site ของ Ubuntu เอง จะไม่สามารถเข้าไปแก้ File ใน USB Boot Disk ได้ (เข้าใจว่าเป็นเพราะ Type of Partition ที่ Tools มันใช้ ตัว MacOS ไม่สามารถเปิดได้) ผมจึงหันมาใช้เครื่องมือตัวอื่นแทน แต่ด้วยความรู้อันน้อยนิด เกี่ยวกับ Ubuntu Boot Image เลยจบที่ ยอมจ่ายเงินซื้อ Tools ตัวนึงที่ชื่อ [UUByte ISO Editor](https://www.uubyte.com/iso-editor.html)

ขั้นตอนคร่าว ๆ ของการสร้าง Boot Disk ก็มีดังนี้

- เข้า Program [UUByte ISO Editor](https://www.uubyte.com/iso-editor.html) (ผมไม่ได้เป็น Sale ขายตัวนี้นะครับ)

  ![Application UUByte ISO Editor](./images/uubyte-iso-editor.png)

- กดปุ่ม Burn

  ![Burn - Create a Bootable USB](./images/uubyte-iso-editor.png)

- เลือก ISO Images File ที่ Download ไว้, กำหนดเป็น Create A Bootable USB, เลือก Drive, Partition Type, File System = FAT32  และกำหนดชื่อ Volume Lable = UBUNTU-20

  ![Burn - Create a Bootable USB](./images/uubyte-iso-editor-burn-setup.png)

- สั่ง Burn รอจนเสร็จ กด OK แล้วลองตรวจสอบ USB Drive ของเราจะเห็น Folder ประมาณนี้

  ![Burn - Create a Bootable USB](./images/uubyte-iso-editor-burn-result.png)

## Setup Automatic Installs to Boot Disk

## Install Ubuntu Server

## Setup Wireless Network

## Reference

- [Automated Server Installs - Introduction](https://ubuntu.com/server/docs/install/autoinstall)
- [Autoinstall Quick Start - Providing the autoinstall data over the network](https://ubuntu.com/server/docs/install/autoinstall-quickstart)
- [JSON Schema for autoinstall config](https://ubuntu.com/server/docs/install/autoinstall-schema)
- [Automated Server Install Quickstart - covertsh's comment](https://discourse.ubuntu.com/t/automated-server-install-quickstart/16614/28)
- [How do I install wpa-supplicant on an offline server?](https://askubuntu.com/questions/503397/how-do-i-install-wpa-supplicant-on-an-offline-server)
- [Ubuntu Server Netplan for Wifi and Ethernet](https://askubuntu.com/questions/1042789/ubuntu-server-netplan-for-wifi-and-ethernet)
