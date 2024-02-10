
> These steps assume you want to install Bench in developer mode. If you want
> install in production mode, follow the [latest recommended installation methods](https://github.com/frappe/bench#installation).

> Learn more about the architecture [here](/ParaLogicTech/frappe/wiki/Frappe-Architechture).

## System Requirements

This guide assumes you are using a personal computer, VPS or a bare-metal server. You also need to be on a *nix system, so any Linux Distribution and MacOS is supported. However, we officially support only the following distributions.

1. Debian / Ubuntu

This guide is tested on Ubuntu 20.04

### Pre-requisites

```
Python 3.10+ (For v14) / Python 3.7 (For v12)
Node.js 16
Redis 6                                       (caching and realtime updates)
MariaDB 10.6.6+                               (Database backend)
yarn 1.12+                                    (js dependency manager)
pip 20+                                       (py dependency manager)
wkhtmltopdf (version 0.12.6 with patched qt)  (for pdf generation)
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
sudo apt install python3 python3-dev python3.10-dev python3-setuptools python3-pip python3-distutils python3.10-venv
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
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
source ~/.bashrc
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
npm install -g yarn
```

**Install wkhtmltopdf**

Download wkhtmltopdf dependencies and fonts

```bash
sudo apt install xvfb libfontconfig xfonts-75dpi
```

Download wkhtmltopdf from https://wkhtmltopdf.org/downloads.html

Ubuntu 22.04 amd64 file

```bash
curl https://github.com/wkhtmltopdf/packaging/releases/download/0.12.6.1-2/wkhtmltox_0.12.6.1-2.jammy_amd64.deb -L -o wkhtmltox_0.12.6.1-2.jammy_amd64.deb
sudo dpkg -i wkhtmltox_0.12.6.1-2.jammy_amd64.deb
```
https://github.com/wkhtmltopdf/packaging/releases/download/0.12.6.1-2/wkhtmltox_0.12.6.1-2.jammy_amd64.deb

## Install and Configure MariaDB

**Install MariaDB** (mariadb-server-10.6+)

If you are on version Ubuntu 20.04, then MariaDB is available in default repo and you can directly run the below commands to install it:

```bash
sudo apt install mariadb-server-10.6
```

During this installation you'll be prompted to set the MySQL root password. If you are not prompted, you'll have to initialize the MySQL server setup yourself. You can do that by running the command:

```bash
sudo mysql_secure_installation
```

> Remember: only run it if you're not prompted the password during setup.

It is really important that you remember this password, since it'll be useful later on. You'll also need the MySQL database development files.

```bash
sudo apt install mariadb-client
```

Now, edit the MariaDB configuration file.

```bash
sudo nano /etc/mysql/mariadb.cnf
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
sudo service mariadb restart
```


## Install Bench CLI

Install bench via pip3

```bash
sudo pip3 install frappe-bench
```

Confirm the bench installation by checking version

```bash
bench --version
```

## Setup a new bench environment

Create a directory for all frappe projects

```bash
cd ~
mkdir frappe
cd frappe
```

Create your first bench environment / folder

```bash
bench init frappe-bench --frappe-path https://github.com/ParaLogicTech/frappe.git --frappe-branch version-14 --python python3.10
cd frappe-bench
```

After the frappe-bench folder is created, download frappe applications (optional)

```bash
bench get-app payments
bench get-app https://github.com/ParaLogicTech/erpnext.git --branch version-14
```

Setup a new site (database)

```bash
bench new-site paralogic.v14 --db-name paralogic_v14_erp
```

Set the `paralogic.v14` site as the default site for this bench

```bash
bench use paralogic.v14
```

Add site in `hosts` file

```bash
sudo nano /etc/hosts
```

and add the line

```
127.0.0.1       paralogic.v14
```
or use bench command to add site to hosts file
```bash
bench add-to-hosts
```

Install applications on site `paralogic.v14`

```bash
bench install-app erpnext
```

## Start bench (development mode)

While inside your bench directory you can run bench commands. To start the bench servers run the command 

```bash
bench start
```

After starting the bench you will see that web server will be running on port 8000 or higher
```
22:46:32 web.1            |  * Running on all addresses (0.0.0.0)
22:46:32 web.1            |  * Running on http://127.0.0.1:8000
22:46:32 web.1            |  * Running on http://10.0.2.15:8000
```

Access the site using a web browser from the hostname you set in hosts file

```
http://paralogic.v14:8000
```

Congratulations, your bench is now installed and working on your system.

## Enable developer_mode configuration

```bash
nano sites/common_site_config.json
```

Change `developer_mode` value to `1`
or use bench command to enable developer_mode
```bash
bench set-config developer_mode 1
```