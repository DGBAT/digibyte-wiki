---
title: Install DigiByte Core
description: Guides for installing the official DigiByte Core software wallet.
published: true
date: 2022-11-04T10:51:47.731Z
tags: 
editor: markdown
dateCreated: 2022-11-02T11:57:05.444Z
---

# Linux

## Snapcraft
*Install using Snapcraft*
> These commands must be performed with root privileges.
{.is-warning}
```bash
snap install digibyte-core
```
[View on Snapcraft](https://snapcraft.io/digibyte-core)


## Docker
*Run a containerized image using Docker*
> You must have [Docker](https://docs.docker.com/desktop/install/linux-install/) installed on your system to run a Docker containerized image.
{.is-warning}

- **1**: Clone 'Dockerfile' from the repository
> If you don't have/want Git on your system, download or make a copy of the Dockerfile from the Github repository and put it inside of a folder.
{.is-info}
```
git clone https://github.com/DigiByte-Core/digibyte-docker
```
---
- **2**: Edit 'Dockerfile' variables to configure image for your machine and application.

> Hint: Make sure you set the correct version in the <kbd>VERSION</kbd> variable. ^(Line^ ^7)^
Usually this means the latest stable version. Reference [releases](https://github.com/DigiByte-Core/digibyte/releases).
{.is-info}

```bash
FROM ubuntu:focal
USER root
WORKDIR /data
ARG ROOTDATADIR=/data
ARG RPCUSERNAME=user
ARG RPCPASSWORD=pass
ARG VERSION=7.17.2
ARG ARCH=x86_64
# Enable below for ARM CPU such as RPi etc or certain Synology NAS systems
#ARG ARCH=aarch64

ARG MAINP2P=12024
ARG MAINRPC=14022
ARG TESTP2P=12026
ARG TESTRPC=14023

# Set to 1 for running it in testnet mode
ARG TESTNET=0

# Do we want any blockchain pruning to take place? Set to 4096 for a 4GB blockchain prune.
# Alternatively set size=1 to prune with RPC call 'pruneblockchainheight <height>'
ARG PRUNESIZE=0
```
---
- 3: Navigate to your folder containing the Dockerfile and build the image.
```bash
cd digibyte-docker
docker build -t digibyte-docker:0.1 .
```
---
- 4: Run the container.
```
docker run digibyte-docker:0.1
```
[View on Github](https://github.com/DigiByte-Core/digibyte-docker)

## Standard

**Download and extract the latest package.**
> Reference [releases](https://github.com/DigiByte-Core/digibyte/releases).
{.is-info}

#### Using Wget
```bash
wget https://github.com/DigiByte-Core/digibyte/releases/download/v7.17.3/digibyte-7.17.3-x86_64-linux-gnu.tar.gz | tar -xz
```

#### Using cURL
```bash
curl https://github.com/DigiByte-Core/digibyte/releases/download/v7.17.3/digibyte-7.17.3-x86_64-linux-gnu.tar.gz | tar -xz
```
---

### Add DigiByte Core to application browser (optional)
> This is a third-party script and could pose a danger to your person's or system's integrity.
Always review untrusted code before using it.
{.is-danger}

> Compatible with all Linux Distributions using [freedesktop](https://specifications.freedesktop.org/desktop-entry-spec/latest/)
{.is-info}

Using the DigiByte Desktop Install script, DigiByte Core will be added to your distro's application browser.
The script can install DigiByte Core for you using Snapcraft.

**For Snapcraft install, or existing install with custom path**:

> 'Current path' won't work using this method. Refer to Github repository for more information.
{.is-info}

```bash
curl -sSL https://github.com/Sbosvk/digibyte-desktop-install/raw/main/desktop-install.sh | bash
```
Follow the on-screen instructions.

> Congratulations!
Now you should be able to launch the DigiByte Core GUI (QT) wallet from your application browser.
{.is-success}

[View on Github](https://github.com/Sbosvk/digibyte-desktop-install/).

---



### Start DigiByte Core GUI (QT)
> If you added DigiByte Core to your application browser in the previous step, you can skip this.
{.is-info}
```bash
cd digibyte-7.17.3/bin/
./digibyte-qt &
```
> The ampersand (&) in line 2 above is optional and makes the process run in the background.
{.is-info}


# Windows

# macOS

# Configuration