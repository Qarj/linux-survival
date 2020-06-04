# Tomcat.md

https://linuxconfig.org/ubuntu-20-04-tomcat-installation

## Install

```
sudo apt update
sudo apt-cache search tomcat
sudo apt install tomcat9 tomcat9-admin
```

Verify that it is running

```
ss -ltn
.
State      Recv-Q     Send-Q         Local Address:Port           Peer Address:Port     Process
LISTEN     0          4096           127.0.0.53%lo:53                  0.0.0.0:*
LISTEN     0          5                  127.0.0.1:631                 0.0.0.0:*
LISTEN     0          50                         *:8080                      *:*
LISTEN     0          5                      [::1]:631                    [::]:*
```

Start on Ubuntu boot

```
sudo systemctl enable tomcat9
```

Open firewall

```
sudo ufw allow from any to any port 8080 proto tcp
```

```
systemctl status tomcat9
.
 tomcat9.service - Apache Tomcat 9 Web Application Server
     Loaded: loaded (/lib/systemd/system/tomcat9.service; enabled; vendor preset: enabled)
     Active: active (running) since Thu 2020-06-04 19:27:17 BST; 21min ago
       Docs: https://tomcat.apache.org/tomcat-9.0-doc/index.html
   Main PID: 11464 (java)
      Tasks: 22 (limit: 6992)
     Memory: 374.8M
     CGroup: /system.slice/tomcat9.service
             └─11464 /usr/lib/jvm/java-8-openjdk-amd64/bin/java -Djava.util.logging.config.file=/var/lib/tomcat9/conf/logging.propertie
```

http://localhost:631/

Check folder

```
cd /var/lib/tomcat9
ll
.
total 20
drwxr-xr-x  5 root   root   4096 Jun  4 19:27 ./
drwxr-xr-x 69 root   root   4096 Jun  4 19:27 ../
lrwxrwxrwx  1 root   root     12 Feb 24 22:37 conf -> /etc/tomcat9/
drwxr-xr-x  2 tomcat tomcat 4096 Feb 24 22:37 lib/
lrwxrwxrwx  1 root   root     17 Feb 24 22:37 logs -> ../../log/tomcat9/
drwxr-xr-x  2 root   root   4096 Jun  4 19:27 policy/
drwxrwxr-x  3 tomcat tomcat 4096 Jun  4 19:27 webapps/
lrwxrwxrwx  1 root   root     19 Feb 24 22:37 work -> ../../cache/tomcat9/
```

## Change the port to 9090

See ports in use

```
sudo lsof -i -P -n | grep LISTEN
.
systemd-r  571 systemd-resolve   13u  IPv4  23586      0t0  TCP 127.0.0.53:53 (LISTEN)
cupsd      701            root    6u  IPv6  21650      0t0  TCP [::1]:631 (LISTEN)
cupsd      701            root    7u  IPv4  21651      0t0  TCP 127.0.0.1:631 (LISTEN)
java       915         jenkins  163u  IPv6  21946      0t0  TCP *:8080 (LISTEN)
```

https://www.baeldung.com/tomcat-change-port

Visual Studio Code does not have permission to open `server.xml`

```
sudo systemctl disable tomcat9
sudo start gedit /var/lib/tomcat9/conf/server.xml
```

Replace all 8080 with 9090 (3 occurences)

Fix firewall and renable

```
sudo ufw allow from any to any port 9090 proto tcp
sudo systemctl enable tomcat9
sudo systemctl restart tomcat9
```

http://127.0.0.1:9090/

```
It works !

If you're seeing this page via a web browser, it means you've setup Tomcat successfully. Congratulations!

This is the default Tomcat home page. It can be found on the local filesystem at: /var/lib/tomcat9/webapps/ROOT/index.html

Tomcat veterans might be pleased to learn that this system instance of Tomcat is installed with
CATALINA_HOME in /usr/share/tomcat9 and
CATALINA_BASE in /var/lib/tomcat9, following the rules from
/usr/share/doc/tomcat9-common/RUNNING.txt.gz.
```
