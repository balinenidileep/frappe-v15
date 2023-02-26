
> These steps assume you want to install Bench in developer mode. If you want
> install in production mode, follow the [latest recommended installation methods](https://github.com/frappe/bench#installation).

> Learn more about the architecture [here](/ParaLogicTech/frappe/wiki/Frappe-Architechture).

## System Requirements

This guide assumes you are using a personal computer, VPS or a bare-metal server. You also need to be on a *nix system, so any Linux Distribution and MacOS is supported. However, we officially support only the following distributions.

1. Debian / Ubuntu

## Pre-requisites

```
Python 3.10+ (v14)
Node.js 16
Redis 6                                       (caching and realtime updates)
MariaDB 10.6.6+                               (Database backend)
yarn 1.12+                                    (js dependency manager)
pip 20+                                       (py dependency manager)
wkhtmltopdf (version 0.12.5 with patched qt)  (for pdf generation)
cron                                          (bench's scheduled jobs: automated certificate renewal, scheduled backups)
NGINX                                         (proxying multitenant sites in production)
```

## Install Required Packages

**Install `git`**

```bash
sudo apt install git
```

**Install `curl`**

```bash
sudo apt install curl
```

**Install Python** (python3.10+)

```bash
sudo apt install python3-dev python3.10-dev python3-setuptools python3-pip python3-distutils python3.10-venv
```

**Install Redis Server**

```bash
sudo apt install redis-server
```

**Install Software Properties Common** (for repository management)

```bash
sudo apt install software-properties-common
```

**Install Node**

We recommend installing node using [nvm](https://github.com/creationix/nvm)

```bash
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash
```

After nvm is installed, you may have to close your terminal and open another one. Now run the following command to install node.

```bash
nvm install 16
```

Verify the installation, by running:

```bash
node -v
```

**Install yarn using `npm`**

```bash
sudo npm install -g yarn
```

**Install wkhtmltopdf**

Download wkhtmltopdf dependencies and fonts

```bash
sudo apt install xvfb libfontconfig
```

Download wkhtmltopdf from https://wkhtmltopdf.org/downloads.html

Ubuntu 22.04 amd64 file

https://github.com/wkhtmltopdf/packaging/releases/download/0.12.6.1-2/wkhtmltox_0.12.6.1-2.jammy_amd64.deb

## Install and Configure MariaDB

**Install MariaDB** (mariadb-server-10.6+)

If you are on version Ubuntu 20.04, then MariaDB is available in default repo and you can directly run the below commands to install it:

```bash
sudo apt install mariadb-server
```

During this installation you'll be prompted to set the MySQL root password. If you are not prompted, you'll have to initialize the MySQL server setup yourself. You can do that by running the command:

```bash
mysql_secure_installation
```

> Remember: only run it if you're not prompted the password during setup.

It is really important that you remember this password, since it'll be useful later on. You'll also need the MySQL database development files.

```bash
sudo apt install mariadb-client
```

Now, edit the MariaDB configuration file.

```bash
nano /etc/mysql/mariadb.cnf
```

And add this configuration at the END of the file

```hljs
[mysqld]
character-set-client-handshake = FALSE
character-set-server = utf8mb4
collation-server = utf8mb4_unicode_ci

[mysql]
default-character-set = utf8mb4
```

Now, just restart the mysql service and you are good to go.

```bash
sudo service mysql restart
```


## Install Bench CLI

Install bench via pip3

```bash
pip3 install frappe-bench
```

Confirm the bench installation by checking version

```bash
bench --version
```

## Setup a new bench

Create your first bench folder.

```bash
cd ~
mkdir frappe
cd frappe
bench init frappe-bench
cd frappe-bench
```

After the frappe-bench folder is created, change your directory to it and run this command

```bash
bench start
```

Congratulations, you have installed bench on to your system.
