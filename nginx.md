# nginx

## Install nginx

Installing on Ubuntu 24.04.

```sh
lsb_release -a
.
No LSB modules are available.
Distributor ID:	Ubuntu
Description:	Ubuntu 24.04.2 LTS
Release:	24.04
Codename:	noble
```

```sh
sudo apt install nginx
```

```sh
sudo apt update
sudo apt install nginx
systemctl status nginx
.
● nginx.service - A high performance web server and a reverse proxy server
     Loaded: loaded (/usr/lib/systemd/system/nginx.service; enabled; preset: enabled)
     Active: active (running) since Thu 2025-04-03 20:34:29 BST; 37s ago
       Docs: man:nginx(8)
    Process: 1401626 ExecStartPre=/usr/sbin/nginx -t -q -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
    Process: 1401628 ExecStart=/usr/sbin/nginx -g daemon on; master_process on; (code=exited, status=0/SUCCESS)
```

```sh
nginx -V
.
nginx version: nginx/1.24.0 (Ubuntu)
built with OpenSSL 3.0.13 30 Jan 2024
TLS SNI support enabled
configure arguments: --with-cc-opt='-g -O2 -fno-omit-frame-pointer -mno-omit-leaf-frame-pointer -ffile-prefix-map=/build/nginx-5QYLpr/nginx-1.24.0=. -flto=auto -ffat-lto-objects -fstack-protector-strong -fstack-clash-protection -Wformat -Werror=format-security -fcf-protection -fdebug-prefix-map=/build/nginx-5QYLpr/nginx-1.24.0=/usr/src/nginx-1.24.0-2ubuntu7.3 -fPIC -Wdate-time -D_FORTIFY_SOURCE=3' --with-ld-opt='-Wl,-Bsymbolic-functions -flto=auto -ffat-lto-objects -Wl,-z,relro -Wl,-z,now -fPIC' --prefix=/usr/share/nginx --conf-path=/etc/nginx/nginx.conf --http-log-path=/var/log/nginx/access.log --error-log-path=stderr --lock-path=/var/lock/nginx.lock --pid-path=/run/nginx.pid --modules-path=/usr/lib/nginx/modules --http-client-body-temp-path=/var/lib/nginx/body --http-fastcgi-temp-path=/var/lib/nginx/fastcgi --http-proxy-temp-path=/var/lib/nginx/proxy --http-scgi-temp-path=/var/lib/nginx/scgi --http-uwsgi-temp-path=/var/lib/nginx/uwsgi --with-compat --with-debug --with-pcre-jit --with-http_ssl_module --with-http_stub_status_module --with-http_realip_module --with-http_auth_request_module --with-http_v2_module --with-http_dav_module --with-http_slice_module --with-threads --with-http_addition_module --with-http_flv_module --with-http_gunzip_module --with-http_gzip_static_module --with-http_mp4_module --with-http_random_index_module --with-http_secure_link_module --with-http_sub_module --with-mail_ssl_module --with-stream_ssl_module --with-stream_ssl_preread_module --with-stream_realip_module --with-http_geoip_module=dynamic --with-http_image_filter_module=dynamic --with-http_perl_module=dynamic --with-http_xslt_module=dynamic --with-mail=dynamic --with-stream=dynamic --with-stream_geoip_module=dynamic
```

## Start nginx

```sh
sudo systemctl start nginx
```

Will not work if port 80 already in use.

## Create localhost entries for local development sites

```sh
sudo nano /etc/hosts
```

Add lines

```
127.0.0.1 local.com
```

## Create self signed certificate for iridium.home

https://www.digitalocean.com/community/tutorials/how-to-create-a-self-signed-ssl-certificate-for-nginx-in-ubuntu-20-04-1

Do not use domains `.dev` or `.app` - they are owned by Google and HSTS is permanently enabled! Full list:

```
1. **.dev**
2. **.app**
3. **.page**
4. **.foo**
5. **.zip**
6. **.mov**
7. **.phd**
8. **.prof**
9. **.nexus**
```

```sh
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

Generate strong security (takes a while)

```sh
sudo openssl dhparam -out /etc/nginx/dhparam.pem 4096
```

Create a config snippet to point to the SSL Key and Certificate

```sh
sudo mkdir /etc/nginx/snippets
sudo nano /etc/nginx/snippets/localdev-self-signed.conf
```

Copy paste into `localdev-self-signed.conf`

```txt
ssl_certificate /etc/ssl/certs/localdev-selfsigned.crt;
ssl_certificate_key /etc/ssl/private/localdev-selfsigned.key;
```

```sh
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

## Configure nginx

First examine the default configuration.

```sh
cd /etc/nginx
cat nginx.conf
.
user www-data;
worker_processes auto;
pid /run/nginx.pid;
error_log /var/log/nginx/error.log;
include /etc/nginx/modules-enabled/*.conf;

events {
	worker_connections 768;
	# multi_accept on;
}

http {

	##
	# Basic Settings
	##

	sendfile on;
	tcp_nopush on;
	types_hash_max_size 2048;
	# server_tokens off;

	# server_names_hash_bucket_size 64;
	# server_name_in_redirect off;

	include /etc/nginx/mime.types;
	default_type application/octet-stream;

	##
	# SSL Settings
	##

	ssl_protocols TLSv1 TLSv1.1 TLSv1.2 TLSv1.3; # Dropping SSLv3, ref: POODLE
	ssl_prefer_server_ciphers on;

	##
	# Logging Settings
	##

	access_log /var/log/nginx/access.log;

	##
	# Gzip Settings
	##

	gzip on;

	# gzip_vary on;
	# gzip_proxied any;
	# gzip_comp_level 6;
	# gzip_buffers 16 8k;
	# gzip_http_version 1.1;
	# gzip_types text/plain text/css application/json application/javascript text/xml application/xml application/xml+rss text/javascript;

	##
	# Virtual Host Configs
	##

	include /etc/nginx/conf.d/*.conf;
	include /etc/nginx/sites-enabled/*;
}


#mail {
#	# See sample authentication script at:
#	# http://wiki.nginx.org/ImapAuthenticateWithApachePhpScript
#
#	# auth_http localhost/auth.php;
#	# pop3_capabilities "TOP" "USER";
#	# imap_capabilities "IMAP4rev1" "UIDPLUS";
#
#	server {
#		listen     localhost:110;
#		protocol   pop3;
#		proxy      on;
#	}
#
#	server {
#		listen     localhost:143;
#		protocol   imap;
#		proxy      on;
#	}
#}
```

The `include /etc/nginx/conf.d/*.conf;` line tells us that we can add configuration files to the `/etc/nginx/conf.d` folder and they'll automatically get included.

```sh
sudo ls -asl /etc/nginx/conf.d/
.
total 8
4 drwxr-xr-x 2 root root 4096 Mar 31 19:38 .
4 drwxr-xr-x 8 root root 4096 Apr  3 20:46 ..
.
sudo ls -asl /etc/nginx/sites-enabled
.
total 8
4 drwxr-xr-x 2 root root 4096 Apr  3 20:34 .
4 drwxr-xr-x 8 root root 4096 Apr  3 20:46 ..
0 lrwxrwxrwx 1 root root   34 Apr  3 20:34 default -> /etc/nginx/sites-available/default
```

Disable the nginx `default.conf` if it is present

```sh
sudo mv /etc/nginx/conf.d/default.conf /etc/nginx/conf.d/default.conf.disabled
```

## Simple configuration example - totaljobs

Create the local development nginx configuration

```sh
sudo touch /etc/nginx/conf.d/localdev.conf
sudocode /etc/nginx/conf.d/localdev.conf
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

## Simple configuration example - local.com for ib

Create the local development nginx configuration

```sh
sudo touch /etc/nginx/conf.d/localdev.conf
sudocode /etc/nginx/conf.d/localdev.conf
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
    server_name local.com;
    include snippets/localdev-self-signed.conf;
    include snippets/ssl-params.conf;

    # divert /portal
    location /portal/ {
        add_header X-Local "/portal/ pointing to local port";            # add response header
        proxy_set_header Host "local.com";
        proxy_set_header X-Origin-Host "local.com";
        proxy_pass http://127.0.0.1:5500/;
    }


    # pass everything else to port 5000
    location / {
        add_header X-Local "From upstream development environment";     # add response header

        proxy_set_header Accept-Encoding "";                            # turn off encoding so we can rewrite the html with the sub_filter
        proxy_pass https://127.0.0.1:5000/;

        # overwriting the existing header might need to be done after the proxy_pass
        proxy_hide_header strict-transport-security;
        #add_header Strict-Transport-Security "max-age=0; includeSubDomains" always;  # to force browser to overwrite previously stored value
    }

}
```

## Test the config

```sh
sudo nginx -t
.
2025/04/03 21:27:23 [warn] 1411920#1411920: "ssl_stapling" ignored, issuer certificate not found for certificate "/etc/ssl/certs/localdev-selfsigned.crt"
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```

## Restart nginx

```sh
sudo systemctl restart nginx
```

## Test & Debug - totaljobs config

Navigate to https://www.totaljobs.local/

Accept self signed cert.

If there is HSTS error

-   make sure the `Strict-Transport-Security` is being removed
-   might need to clear HSTS status in the browser (supercookie)
-   https://www.py4u.net/discuss/1218270

Use curl to see the response header

```sh
curl --insecure --head https://www.totaljobs.local/
```

See the error log

```sh
cat /var/log/nginx/error.log
```

## Test & Debug - ib config

Navigate to https://local.com/portal/vibePosition-try2-mod.html

Use curl to see the response header

```sh
curl --insecure --head https://local.com/v1/api/iserver/accounts
```

See the error log

```sh
cat /var/log/nginx/error.log
```

## Advanced nginx example - handle multiple servers with regex

```sh
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

## Test advanced example

https://www.caterer.local.com/
http://www.caterer.local.com:8090/

https://www.cwjobs.local.co.uk/
http://www.cwjobs.local.co.uk:8090/

https://www.totaljobs.local.com/
http://www.totaljobs.local.com:8090/

Login as a jobseeker to prove it all hangs together.
