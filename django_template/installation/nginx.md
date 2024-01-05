# Install Nginx

We will be using Nginx on Ubuntu for reverse proxy on test and production
servers. Nginx is also installed in a Docker container for local network reverse
proxy. It is not neccessary to install Nginx for local development. To install
Nginx for test or production servers, you can follow the steps below.

Because Nginx is available in Ubuntu's default repositories, it is possible to
install it from these repositories using the apt packaging system.

```bash
sudo apt update
sudo apt install nginx
```

Before testing Nginx, the firewall software needs to be adjusted to allow access
to the service. Nginx registers itself as a service with `ufw` upon
installation, making it straightforward to allow Nginx access. You can enable
HTTPS by typing:

```bash
sudo ufw allow 'Nginx HTTPS'
```

You can verify the change by typing:

```bash
sudo ufw status
```

The output will indicated which HTTP traffic is allowed:

```bash
Output
Status: active

To                         Action      From
--                         ------      ----
OpenSSH                    ALLOW       Anywhere
Nginx HTTP                 ALLOW       Anywhere
OpenSSH (v6)               ALLOW       Anywhere (v6)
Nginx HTTP (v6)            ALLOW       Anywhere (v6)
```

Check your web server:

```bash
sudo systemctl status nginx
```

```bash
Output
● nginx.service - A high performance web server and a reverse proxy server
   Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
   Active: active (running) since Fri 2020-04-20 16:08:19 UTC; 3 days ago
     Docs: man:nginx(8)
 Main PID: 2369 (nginx)
    Tasks: 2 (limit: 1153)
   Memory: 3.5M
   CGroup: /system.slice/nginx.service
           ├─2369 nginx: master process /usr/sbin/nginx -g daemon on; master_process on;
           └─2380 nginx: worker process
```
