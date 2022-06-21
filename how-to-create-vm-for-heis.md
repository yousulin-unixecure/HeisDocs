How to create a VM for H.E.I.S.
===
## Prerequisite
- VMware Workstation Pro installed.
- Minimal version of CentOS 7 .iso file downloaded.

## Create VM
1. Create a virtual machine via VMware Workstation.
2. Install minimal version of CentOS 7.
3. Install essential packages like OpenSSH, wget, etc.
4. (Optional) [Install VMware tool and required packages.](https://hackmd.io/@7TZefwuTSiKVqThXzQqdJw/rkBHyiKYc)

## [Prepare for web application environments](https://hackmd.io/@7TZefwuTSiKVqThXzQqdJw/BkBJJS_tc)
### OpenJDK 8
`sudo yum install java-1.8.0-openjdk`
### Apache Tomcat 9.0.46
#### 1. Download binary files of Apache Tomcat
- `wget https://archive.apache.org/dist/tomcat/tomcat-9/v9.0.46/bin/apache-tomcat-9.0.46.zip`
- `unzip apache-tomcat-9.0.46.zip`
#### 2. Configure for Tomcat
- Create `tomcat.service` under `/usr/lib/systemd/system`.
- Make `tomcat.service` executing when startup by `systemctl enable tomcat.service`
- Run `tomcat.service` by `systemctl start tomcat.service`
#### 3. Deploy `.war` file of `heis_on_premise`
### MySQL
#### 1. Enable MySQL Repository by `.rpm` file
`yum install -y https://dev.mysql.com/get/mysql80-community-release-el7-3.noarch.rpm`
#### 2. Install Mysql Server from the MySQL Repository just enabled
`yum install -y mysql-community-server`

if appears message: `The GPG keys listed for the "MySQL 8.0 Community Server" repository are already installed but they are not correct for this package.`, then run `rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022` to update the valid key.

#### Add user for web application

## [Configure the firewall for web application]((https://hackmd.io/@7TZefwuTSiKVqThXzQqdJw/S1Nz03Cd5))
1. Add port `22/tcp` for OpenSSH, and port number for web application, `3306/tcp` for MySQL.
2. Reload firewall.

## Prepare for running python application
### Create `.sh` to run python application
### Setup a Cron Job to run `.sh` files

## Manage log files with `logrotate.conf`

## Deploy the VM on VMware ESXI

## [Configure the static IP](https://hackmd.io/@7TZefwuTSiKVqThXzQqdJw/S1Nz03Cd5)
1. Use `nmcli` to configure the static IP, including `ipv4.address` with prefix, `gateway`.
2. Restart NetworkManager.
