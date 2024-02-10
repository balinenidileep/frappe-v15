**Install supervisor and nginx**

```bash
sudo apt install supervisor
sudo apt install nginx
```

**Enable DNS Multitenancy**

```bash
bench config dns_multitenant on
```

**Add supervisor configuration**

```bash
bench setup supervisor
sudo ln -s `pwd`/config/supervisor.conf /etc/supervisor/conf.d/frappe-bench.conf
```

**Reload supervisor configuration**

```bash
sudo supervisorctl reread
sudo supervisorctl update
```

**Add nginx configuration**

```bash
bench setup nginx
sudo ln -s `pwd`/config/nginx.conf /etc/nginx/conf.d/frappe-bench.conf
```

**Configure nginx**

Open the file `/etc/nginx/nginx.conf` in a text editor of choice

Add the below piece of code inside http as shown in the section following the code snippet:

```
log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';
```

**Reload nginx configuration**

```bash
sudo service nginx reload
```

**Configure Lets Encrypt SSL**

```bash
sudo bench setup lets-encrypt site_name
```
