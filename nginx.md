# Install nginx

Installing on Ubuntu 20.04.

```
lsb_release -a
.
No LSB modules are available.
Distributor ID:	Ubuntu
Description:	Ubuntu 20.04.3 LTS
Release:	20.04
Codename:	focal
```

```
cd ~/Downloads
wget http://nginx.org/keys/nginx_signing.key
sudo apt-key add nginx_signing.key
sudo nano /etc/apt/sources.list.d/nginx.list
```

Copy paste

```
deb [arch=amd64] http://nginx.org/packages/mainline/ubuntu/ focal nginx
```

```
sudo apt update
sudo apt install nginx
systemctl status nginx
.
● nginx.service - nginx - high performance web server
     Loaded: loaded (/lib/systemd/system/nginx.service; enabled; vendor preset: enabled)
     Active: inactive (dead)
       Docs: https://nginx.org/en/docs/
```

```
nginx -V
.
nginx version: nginx/1.21.3
built by gcc 9.3.0 (Ubuntu 9.3.0-10ubuntu2)
built with OpenSSL 1.1.1f  31 Mar 2020
TLS SNI support enabled
configure arguments: --prefix=/etc/nginx --sbin-path=/usr/sbin/nginx --modules-path=/usr/lib/nginx/modules --conf-path=/etc/nginx/nginx.conf --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --pid-path=/var/run/nginx.pid --lock-path=/var/run/nginx.lock --http-client-body-temp-path=/var/cache/nginx/client_temp --http-proxy-temp-path=/var/cache/nginx/proxy_temp --http-fastcgi-temp-path=/var/cache/nginx/fastcgi_temp --http-uwsgi-temp-path=/var/cache/nginx/uwsgi_temp --http-scgi-temp-path=/var/cache/nginx/scgi_temp --user=nginx --group=nginx --with-compat --with-file-aio --with-threads --with-http_addition_module --with-http_auth_request_module --with-http_dav_module --with-http_flv_module --with-http_gunzip_module --with-http_gzip_static_module --with-http_mp4_module --with-http_random_index_module --with-http_realip_module --with-http_secure_link_module --with-http_slice_module --with-http_ssl_module --with-http_stub_status_module --with-http_sub_module --with-http_v2_module --with-mail --with-mail_ssl_module --with-stream --with-stream_realip_module --with-stream_ssl_module --with-stream_ssl_preread_module --with-cc-opt='-g -O2 -fdebug-prefix-map=/data/builder/debuild/nginx-1.21.3/debian/debuild-base/nginx-1.21.3=. -fstack-protector-strong -Wformat -Werror=format-security -Wp,-D_FORTIFY_SOURCE=2 -fPIC' --with-ld-opt='-Wl,-Bsymbolic-functions -Wl,-z,relro -Wl,-z,now -Wl,--as-needed -pie'
```

# Start nginx

```
sudo systemctl start nginx
.
Job for nginx.service failed because the control process exited with error code.
See "systemctl status nginx.service" and "journalctl -xe" for details.
```

Will not work if port 80 already in use.

# Create localhost entries for local development sites

```
sudo nano /etc/hosts
```

Add lines

```
127.0.0.1 www.totaljobs.local.com
127.0.0.1 www.caterer.local.com
127.0.0.1 www.cwjobs.local.co.uk
127.0.0.1 local.stepstone.de
127.0.0.1 local.stepstone.fr
```

# Create self signed certificate for local.com

https://www.digitalocean.com/community/tutorials/how-to-create-a-self-signed-ssl-certificate-for-nginx-in-ubuntu-20-04-1

Don not use domains `.dev` or `.app` - they are owned by Google and HSTS is permanently enabled!

```
sudo openssl req -x509 -nodes -days 825 -newkey rsa:2048 -keyout /etc/ssl/private/localdev-selfsigned.key -out /etc/ssl/certs/localdev-selfsigned.crt
```

Answer questions

```
UK
England
London
Local Developer
IT
local.com
admin@local.local
```

Generate strong security

```
sudo openssl dhparam -out /etc/nginx/dhparam.pem 4096
```

Create a config snippet to point to the SSL Key and Certificate

```
sudo mkdir /etc/nginx/snippets
sudo nano /etc/nginx/snippets/localdev-self-signed.conf
```

Copy paste into `localdev-self-signed.conf`

```
ssl_certificate /etc/ssl/certs/localdev-selfsigned.crt;
ssl_certificate_key /etc/ssl/private/localdev-selfsigned.key;
```

```
sudo nano /etc/nginx/snippets/ssl-params.conf
```

Copy paste

```bash
ssl_protocols TLSv1.2;
ssl_prefer_server_ciphers on;
ssl_dhparam /etc/nginx/dhparam.pem; # commented out since we have not enabled strong encryption
ssl_ciphers ECDHE-RSA-AES256-GCM-SHA512:DHE-RSA-AES256-GCM-SHA512:ECDHE-RSA-AES256-GCM-SHA384:DHE-RSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-SHA384;
ssl_ecdh_curve secp384r1; # Requires nginx >= 1.1.0
ssl_session_timeout  10m;
ssl_session_cache shared:SSL:10m;
ssl_session_tickets off; # Requires nginx >= 1.5.9
ssl_stapling on; # Requires nginx >= 1.3.7
ssl_stapling_verify on; # Requires nginx => 1.3.7
resolver 8.8.8.8 8.8.4.4 valid=300s;
resolver_timeout 5s;
# Disable strict transport security for now. You can uncomment the following
# line if you understand the implications.
# add_header Strict-Transport-Security "max-age=63072000; includeSubDomains; preload";
# add_header X-Frame-Options DENY;
# add_header X-Content-Type-Options nosniff;
# add_header X-XSS-Protection "1; mode=block";
```

# Configure nginx

First examine the default configuration.

```
cd /etc/nginx
cat nginx.conf
.
user  nginx;
worker_processes  auto;

error_log  /var/log/nginx/error.log notice;
pid        /var/run/nginx.pid;


events {
    worker_connections  1024;
}


http {
    include       /etc/nginx/mime.types;
    default_type  application/octet-stream;

    log_format  main  '$remote_addr - $remote_user [$time_local] "$request" '
                      '$status $body_bytes_sent "$http_referer" '
                      '"$http_user_agent" "$http_x_forwarded_for"';

    access_log  /var/log/nginx/access.log  main;

    sendfile        on;
    #tcp_nopush     on;

    keepalive_timeout  65;

    #gzip  on;

    include /etc/nginx/conf.d/*.conf;
}
```

The last line tells us that we can add configuration files to the `/etc/nginx/conf.d` folder and they'll automatically get included.

Disable the nginx `default.conf`

```
sudo mv /etc/nginx/conf.d/default.conf /etc/nginx/conf.d/default.conf.disabled
```

# Simple configuration example

Create the local development nginx configuration

```
sudo subl /etc/nginx/conf.d/localdev.conf
```

Copy Paste

```bash
server {
    # handle very large response headers
    proxy_busy_buffers_size     512k;
    proxy_buffers             4 512k;
    proxy_buffer_size           256k;

    listen 443 ssl;                                  # ip v4
    listen [::]:443 ssl;                             # ip v6
    server_name www.totaljobs.local;
    include snippets/localdev-self-signed.conf;
    include snippets/ssl-params.conf;

    # divert /about to a locally running service
    location /about/ {
        add_header X-Local "/about/ pointing to local port";            # add response header
        proxy_set_header Host "www.totaljobs.local";
        proxy_set_header X-Origin-Host "www.totaljobs.local";
        proxy_pass http://localhost/;
    }


    # go to the development environment for everything else
    location / {
        add_header X-Local "From upstream development environment";     # add response header

        proxy_set_header Accept-Encoding "";                            # turn off encoding so we can rewrite the html with the sub_filter
        sub_filter www.totaljobs.com www.totaljobs.local;               # fix any absolute links in the html
        sub_filter_once off;                                            # replace all matches, not just first
        sub_filter_types text/html application/json;

        proxy_set_header Referer "https://www.totaljobs.com";
        proxy_pass https://www.totaljobs.com/;

        # overwriting the existing header might need to be done after the proxy_pass
        proxy_hide_header strict-transport-security;
        #add_header Strict-Transport-Security "max-age=0; includeSubDomains" always;  # to force browser to overwrite previously stored value
    }

}

# redirect http:// to https:// - change ports from 8090 to 80
server {
    listen 8090;
    listen [::]:8090;
    server_name www.totaljobs.local
    return 302 https://$server_name$request_uri;
}
```

# Test the config

```
sudo nginx -t
.
nginx: [warn] "ssl_stapling" ignored, issuer certificate not found for certificate "/etc/ssl/certs/localdev-selfsigned.crt"
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```

# Restart nginx

```
sudo systemctl restart nginx
```

# Test & Debug

Navigate to https://www.totaljobs.local/

Accept self signed cert.

If there is HSTS error

-   make sure the `Strict-Transport-Security` is being removed
-   might need to clear HSTS status in the browser (supercookie)
-   https://www.py4u.net/discuss/1218270

Use curl to see the response header

```
curl --insecure --head https://www.totaljobs.local/
```

See the error log

```
cat /var/log/nginx/error.log
```

# Advanced nginx example - handle multiple servers with regex

```bash
server {
    # handle very large response headers
    proxy_busy_buffers_size   512k;
    proxy_buffers   4 512k;
    proxy_buffer_size   256k;

    listen 443 ssl;                                  # ip v4
    listen [::]:443 ssl;                             # ip v6
    server_name ~^www\.(caterer|cwjobs|totaljobs)\.local\.(com|co\.uk)$;
    include snippets/localdev-self-signed.conf;
    include snippets/ssl-params.conf;

    # divert /about to a locally running service
    location /about/ {
        add_header X-Local "/about/ pointing to local port";            # add response header
        proxy_set_header Host "www.$1.local";
        proxy_set_header X-Origin-Host "www.$1.local";
        proxy_pass http://localhost/;
    }

    # go to the development environment for everything else
    location / {
        add_header X-Local "From upstream development environment";     # add response header

        proxy_set_header Accept-Encoding "";                            # turn off encoding so we can rewrite the html with the sub_filter
        sub_filter www.$1.$2 www.$1.local.$2;                           # fix any absolute links in the html
        sub_filter_once off;                                            # replace all matches, not just first
        sub_filter_types text/html application/json;

        proxy_pass https://www.$1.$2/$uri;                              # note $uri is needed - proxy_pass works differently with variables
        proxy_redirect https://www.$1.$2 https://www.$1.local.$2;       # rewrite 302 header host e.g. cwjobs sign in requires this

        # remove hsts - this code required *AFTER* proxy_pass (maybe?)
        proxy_hide_header strict-transport-security;
        #add_header Strict-Transport-Security "max-age=0; includeSubDomains" always;  # to force browser to overwrite previously stored value
    }

}

# redirect http:// to https:// - in real life change ports from 8090 to 80
server {
    listen 8090;
    listen [::]:8090;
    server_name ~^www\.(caterer|cwjobs|totaljobs)\.local\.(com|co\.uk)$;
    return 302 https://www.$1.local.$2$request_uri;
}
```

# Test advanced example

https://www.caterer.local.com/
http://www.caterer.local.com:8090/

https://www.cwjobs.local.co.uk/
http://www.cwjobs.local.co.uk:8090/

https://www.totaljobs.local.com/
http://www.totaljobs.local.com:8090/

Login as a jobseeker to prove it all hangs together.
