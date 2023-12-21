---
title: Run a open full node
description: Runnning a full node is an easy way to contribute to DigiByte and help maintain the consensus on the Blockchain.
published: true
date: 2023-10-22T11:32:22.734Z
tags: 
editor: markdown
dateCreated: 2023-10-22T08:36:51.458Z
---


# Run a open full node

The software DigiByte Core is open-sourced under MIT License, and is the foundation framework of your blockchain application.

## Prerequisites

|     | Minimum ^Personal^ | Recommended ^Personal^ | Recommended ^Applications^ |
| --- | --- | --- | --- |
| RAM | <5 GB | \>8 GB | \>32 GB |
| Allocation space | 40 GB minimum | \>500 GB | \>5 TB |
| Network | Stable internet connection | Unlimited bandwidth |     |
| Architecture | 64-Bit | 64-Bit | 64-Bit |

# Linux

> The following commands are line based, no GUI is required.
{.is-info}


> Basic Linux system administration knowledge is assumed and you may need to install additional packages if an error is encountered.
{.is-warning}


## Create Swap Space

If you are using the minimum of 4GB RAM on your system, it is recommended to have at least 8GB of swap space available. To check the current swap, run the free command.

```plaintext
free -h
```

If you are using the minimum of 4GB RAM on your system, create a swap file with the following commands.

> These commands must be performed with root privileges.
{.is-warning}


```plaintext
fallocate -l 8G /swap
chmod 0600 /swap
mkswap /swap
swapon /swap
```

Use the free command again to verify the changes.

```plaintext
free -h
```

Make the swap changes permanent by adding required information to the fstab file.

```plaintext
echo "/swap swap swap defaults 0 0" >> /etc/fstab
```

## Create user

If a non-root user does not already exist, create the new user name, `digibyte`, and login with the following commands.

> These commands must be performed with root privileges.
{.is-warning}

### CentOS

```plaintext
useradd -G wheel digibyte -m -s /bin/bash
```

---

### Ubuntu

```plaintext
useradd -G sudo digibyte -m -s /bin/bash
```
---

## Complete User profile
Set a password for the new user

```plaintext
passwd digibyte
```

Login as user `digibyte`

```plaintext
su - digibyte
```

## Create config file

First create the directory to put the config file in.

```plaintext
mkdir -vp ~/.digibyte
```

Create the basic DigiByte configuration file.

```plaintext
cat <<EOF > ~/.digibyte/digibyte.conf
daemon=1
maxconnections=300
disablewallet=1
EOF
```

> Since we are running a server, wallet functionality is disabled with the above config.  
> If you want wallet functionality, change the value of `disablewallet on line 4 to` 0.
{.is-info}


If your data bandwidth is limited, it is recommended lower the amount of `maxconnections on line` 3.

### Install DigiByte Core

Navigate to your home folder then download and decompress the DigiByte Core software.

> If your system is ARM architecture, use the `digibyte-7.17.2-aarch64-linux-gnu.tar.gz` package instead.
{.is-info}

> This guide may be outdated, make sure you download the [latest](https://github.com/DigiByte-Core/digibyte/releases) and current release of DigiByte Core.
{.is-danger}



```plaintext
cd ~/
wget -c https://github.com/digibyte-core/digibyte/releases/download/v7.17.2/digibyte-7.17.2-x86_64-linux-gnu.tar.gz -O - | tar xz
```

## Add service file {.tabset}

> If you don't plan on running DigiByte Core as a service, this step can be skipped.  
> Perform this step if you want DigiByte Core to start automatically on system boot.
{.is-info}


> These commands must be performed with root privileges.
{.is-warning}

**Select your OS from the tabs below**


### CentOS

```plaintext
cat <<EOF > /usr/lib/systemd/system/digibyted.service
[Unit]
Description=DigiByte's distributed currency daemon
After=network.target

[Service]
User=digibyte
Group=digibyte

Type=forking
PIDFile=/home/digibyte/.digibyte/digibyted.pid
ExecStart=/home/digibyte/digibyte-7.17.2/bin/digibyted -daemon -pid=/home/digibyte/.digibyte/digibyted.pid \
-conf=/home/digibyte/.digibyte/digibyte.conf -datadir=/home/digibyte/.digibyte -disablewallet

Restart=always
PrivateTmp=true
TimeoutStopSec=60s
TimeoutStartSec=2s
StartLimitInterval=120s
StartLimitBurst=5

[Install]
WantedBy=multi-user.target
EOF
```

### Ubuntu

```plaintext
cat <<EOF > /etc/systemd/system/digibyted.service
[Unit]
Description=DigiByte's distributed currency daemon
After=network.target

[Service]
User=digibyte
Group=digibyte

Type=forking
PIDFile=/home/digibyte/.digibyte/digibyted.pid
ExecStart=/home/digibyte/digibyte-7.17.2/bin/digibyted -daemon -pid=/home/digibyte/.digibyte/digibyted.pid \
-conf=/home/digibyte/.digibyte/digibyte.conf -datadir=/home/digibyte/.digibyte -disablewallet

Restart=always
PrivateTmp=true
TimeoutStopSec=60s
TimeoutStartSec=2s
StartLimitInterval=120s
StartLimitBurst=5

[Install]
WantedBy=multi-user.target
EOF
```

## Service on boot
Enable the service on boot.

```plaintext
systemctl enable digibyted.service
```

Start the service.

```plaintext
systemctl start digibyted.service
```

## Run your node

If you haven't already started your DigiByte Core open full node as a service from the previous step, start your node using the following commands.

```plaintext
cd ~/digibyte/digibyte-7.17.2/bin/
./digibyted &
```

> The ampersand (&) in line `2` above is optional and makes the process run in the background.
{.is-info}


## Checking log file

You can check the logs of your DigiByte Core open full node with the tail command.

```plaintext
tail -f ~/.digibyte/debug.log
```

## Upgrade tip

Make future upgrades easier by creating a symbolic link and pointing it to the current DigiByte directory.

```plaintext
cd ~/
ln -s digibyte-7.17.2 digibyte
```

In the service file you created, replace any occurrences of `/home/digibyte/digibyte-7.17.2/` with `/home/digibyte/digibyte/`

When the time for upgrade comes, stop the `digibyted.service`, download and decompress the new release, delete and re-create the symbolic link pointing to the new DigiByte directory and start the `digibyted.service`.

# Raspberry Pi

> You can also use [DigiNode Tools](https://diginode.tools/) to setup and manage a DigiByte Node on a Raspberry Pi.
{.is-info}

> A Raspberry Pi 4 or later is required. Raspberry Pi 3 and older are not supported. It's always recommended to have active fan cooling on the Raspberry Pi.
{.is-info}


## Prerequisites

| Requirements | Minimum | Recommended |
| --- | --- | --- |
| Hardware | Raspberry Pi 4 4Gb | Raspberry Pi 5 8Gb or better |
| micro SD card | \>32 GB SD Card | 16 GB SD Card + 500 GB External Drive (HDD/SDD) |
| Architecture | 64-Bit Linux/Windows/macOS |     |
| Disk image | 64-bit system image | [Ubuntu Server](https://ubuntu.com/download/raspberry-pi) is recommended and will be used in this guide. |
| Software | [Balena Etcher.](https://www.balena.io/etcher/) |     |
| Internet | Stable internet connection. | Unlimited bandwidth. |

## Prepare the SD card

It's time to flash the SD card with our 64-bit disk image.  
You can do this in a variety of ways, but throughout this guide we will be using Balena Etcher to flash our SD card.

**Balena Etcher**

> Balena Etcher is a third-party software and is not provided by DigiByte or the contributors of this wiki.
{.is-info}


1. Download and open the Balena Etcher software.

2. Click on **Flash from file** and select your disk image.

3. Click on **Select target**, select your SD card, and then click on the **Flash!** button.

4. Wait for the writing to complete.

> Your SD card is now ready.
{.is-success}


## Set up the RPi

> The following commands are line based, no GUI is required.
{.is-info}


Connect a keyboard, mouse & display to your RPi.  
Insert the SD card and boot your device.

### Log in

Login with the default credentials, since we're using Ubuntu Server our default username and password is `ubuntu` . On first login you will be prompted to change the password.

Upgrade your system to latest using the following command.

```plaintext
sudo apt update && sudo apt upgrade -y
```

Wait for it to finish, then restart your system.

```plaintext
sudo reboot
```

> The rest of the steps in this RPi 4 guide can be completed using [SSH](https://www.openssh.com/manual.html).
{.is-info}


## Swap space

If you are using the minimum of 4GB RAM on your system, it is recommended to have at least 8GB of swap space available. To check the current swap, run the free command.

```plaintext
free -h
```

If you are using the minimum of 4GB RAM on your system, create a swap file with the following commands.

> These commands must be performed with root privileges.
{.is-warning}


```plaintext
fallocate -l 8G /swap
chmod 0600 /swap
mkswap /swap
swapon /swap
```

Use the free command again to verify the changes.

```plaintext
free -h
```

Make the swap changes permanent by adding required information to the fstab file.

```plaintext
echo "/swap swap swap defaults 0 0" >> /etc/fstab
```

## Create config file

First create the directory to put the config file in.

```plaintext
mkdir -vp ~/.digibyte
```

Create the basic DigiByte configuration file.

```plaintext
cat <<EOF > ~/.digibyte/digibyte.conf
daemon=1
maxconnections=300
disablewallet=1
EOF
```

> Since we are running a server, wallet functionality is disabled with the above config.  
> If you want wallet functionality, change the value of `disablewallet on line 4 to` 0.
{.is-info}


If your data bandwidth is limited, it is recommended lower the amount of `maxconnections on line` 3.

## Install DigiByte Core

Navigate to your home folder then download and decompress the DigiByte Core software.

```plaintext
cd ~/
wget -c https://github.com/digibyte-core/digibyte/releases/download/v7.17.2/digibyte-7.17.2-aarch64-linux-gnu.tar.gz -O - | tar xz
```

### Add service file

> If you don't plan on running DigiByte Core as a service, this step can be skipped.  
> Perform this step if you want DigiByte Core to start automatically on system boot.
{.is-info}


> These commands must be performed with root privileges.
{.is-warning}


```plaintext
cat <<EOF > /etc/systemd/system/digibyted.service
[Unit]
Description=DigiByte's distributed currency daemon
After=network.target

[Service]
User=digibyte
Group=digibyte

Type=forking
PIDFile=/home/digibyte/.digibyte/digibyted.pid
ExecStart=/home/digibyte/digibyte-7.17.2/bin/digibyted -daemon -pid=/home/digibyte/.digibyte/digibyted.pid \
-conf=/home/digibyte/.digibyte/digibyte.conf -datadir=/home/digibyte/.digibyte -disablewallet

Restart=always
PrivateTmp=true
TimeoutStopSec=60s
TimeoutStartSec=2s
StartLimitInterval=120s
StartLimitBurst=5

[Install]
WantedBy=multi-user.target
EOF
```

Enable the service on boot.

```plaintext
systemctl enable digibyted.service
```

Start the service.

```plaintext
systemctl start digibyted.service
```

## Run your node

If you haven't already started your DigiByte Core open full node as a service from the previous step, start your node using the following commands.

```plaintext
cd ~/digibyte/digibyte-7.17.2/bin/
./digibyted &
```

> The ampersand (&) in line `2` above is optional and makes the process run in the background.
{.is-info}


### View log file

You can check the logs of your DigiByte Core open full node with the tail command.

```plaintext
tail -f ~/.digibyte/debug.log
```

### Upgrade tip

Make future upgrades easier by creating a symbolic link and pointing it to the current DigiByte directory.

```plaintext
cd ~/
ln -s digibyte-7.17.2 digibyte
```

In the service file you created, replace any occurrences of `/home/digibyte/digibyte-7.17.2/` with `/home/digibyte/digibyte/`

When the time for upgrade comes, stop the `digibyted.service`, download and decompress the new release, delete and re-create the symbolic link pointing to the new DigiByte directory and start the `digibyted.service`.

# Port Forwarding
A DigiByte open full node requires port `12024` on your router to be opened, a process called [_port forwarding_](https://en.wikipedia.org/wiki/Port_forwarding).

> Without the port forwarded you can not relay the blockchain to other nodes and can't be found on the network.
{.is-danger}


## Find your LAN IP

A local area network (LAN) IP, is the IP address your network devices use to communicate with each other in their local environment, e.g those devices connected to your router.  
We're going to tell the router to forward the incoming traffic of port `12024` to this IP address.

# Your OS IP {.tabset}

## Linux

You need the `net-tools` package for the following step.  
It can be installed with `sudo apt install net-tools`

Find your LAN IP using the ifconfig command.

```plaintext
ifconfig
```

You will receive an output that looks something like in the code block below.

```plaintext
enp0s25: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        ether 00:26:18:55:bd:77  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
        device interrupt 20  memory 0xfbcc0000-fbce0000  

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 13178  bytes 1129714 (1.1 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 13178  bytes 1129714 (1.1 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

wlxf81a6718dc39: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 10.0.0.169  netmask 255.0.0.0  broadcast 10.255.255.255
        inet6 fe80::89fe:fe67:4f60:826c  prefixlen 64  scopeid 0x20<link>
        ether f8:1a:67:18:dc:39  txqueuelen 1000  (Ethernet)
        RX packets 92321  bytes 82390304 (82.3 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 72648  bytes 9875771 (9.8 MB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

One line 1, 9 & 18, we are seeing interface names.  
These might be named something different for you.

What we are looking for is a local IP address on a line that starts with `inet`.

In order, we can first see the ethernet interface which does not have an `inet` address, so in this case this interface can be ignored.

The next interface, the `lo`, is a typical interface called the `loopback` , this can also be ignored since it it only provides us with a localhost IP.

The next interface we see is a wireless device interface, because this system is connected through WiFi.  
If we look on line `19` above, we can find what we are looking for and see that our local IPv4 address is `10.0.0.169`.

## macOS

In the top left corner of your desktop, click the **Apple** icon -> **System** **Preferences**.

Click on **Network**

Select your connection device (WiFi or Ethernet) to reveal your LAN IP address.

## Windows

Open up a run window by pressing the keyboard shortcut Start[^\[1\]^](#fn1) + R and entering `cmd` in the text field, click OK. A **cmd** window will appear.

Use the **ipconfig** command.

```plaintext
ipconfig
```

The address will be the IPv4 address in the listed output.

**Select your OS from the tabs below**

# Complete port forwarding

1.  Go to your routers local IP address in a web browser and login with sufficient privileges.
2.  Select the **TCP** protocol.
3.  Enter port `12024` into the port field.
4.  Enter your DigiByte Core open full node's LAN IP address into the IP address field.
5.  Save your changes.

There's a lot of different routers with a lot of different user interfaces. It is very hard to make a generic guide for a subject like port forwarding, fortunately enough [portforward.com](http://portforward.com) offers guides for some of the most common brands.

If you don't know how to port forward your router, try finding your router brand and model on the link below.

---

Start key is known also as the "Windows" key. [↩︎](#fnref1)