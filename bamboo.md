# Atlassian Bamboo

# Download and Unpack

Go to https://www.atlassian.com/software/bamboo/download and find latest version

Download Bamboo

```
cd ~/Downloads
wget https://product-downloads.atlassian.com/software/bamboo/downloads/atlassian-bamboo-8.0.5.tar.gz
mkdir /home/$USER/bamboo
tar xvzf atlassian-bamboo-8.0.5.tar.gz -C /home/$USER/bamboo --strip-components=1
```

# Examine install instructions

```
cd /home/$USER/bamboo
cat README.txt
.
---------------------------------------------------------------------
Bamboo 8.0.5-#80013 README
---------------------------------------------------------------------

Thank you for downloading Bamboo 8.0.5 - Server distribution.  This
distribution comes with a built-in Tomcat 8.5.70-atlassian-hosted web server and H2
database, so it runs (almost) out the box.


BRIEF INSTALL GUIDE
-------------------


1. Install Java Development Kit (JDK) version 1.8 from

   http://www.oracle.com/technetwork/java/javase/downloads/index.html

2. Set the JAVA_HOME variable to where you installed Java (JDK not JRE inside it).


3. Set your Bamboo Home directory.
   Instructions how to set your Bamboo Home directory can be found here: https://confluence.atlassian.com/display/BAMBOO/Installing+and+upgrading


4. Run bin/start-bamboo.sh (*nix) or bin\start-bamboo.bat (Windows).
   Check that there are no errors on the console.  See below for troubleshooting advice.


5. Point your browser at http://localhost:8085/
   You should see Bamboo's Setup Wizard.


Full documentation is available online at:

  https://confluence.atlassian.com/display/BAMBOO/Installing+and+upgrading


PROBLEMS?
---------
A common startup problem is when another program has claimed port 8085, which
Bamboo is configured to run on by default.  To avoid this port conflict, Bamboo's
port can be changed in conf/server.xml.

If you have installation (or other) problems, please see the resources
listed at https://support.atlassian.com



QUESTIONS?
----------
Questions? Try the docs at:

   https://confluence.atlassian.com/display/BAMBOO/Bamboo+Documentation

Alternatively ask on the forums at:

   https://community.atlassian.com/

or ask Atlassian directly - see the contact info at
https://support.atlassian.com


-----------------------------------------------------------
Thank you for using Bamboo!
- The Atlassian Team
-----------------------------------------------------------
```

# Follow instructions

## Install Java 8 SDK

```
sudo apt install openjdk-8-jdk openjdk-8-jre
java -version
.
openjdk version "1.8.0_252"
OpenJDK Runtime Environment (build 1.8.0_252-8u252-b09-1ubuntu1-b09)
OpenJDK 64-Bit Server VM (build 25.252-b09, mixed mode)
```

## Set JAVA_HOME

```
ls /usr/lib/jvm/java-8-openjdk-amd64/
.
ASSEMBLY_EXCEPTION  bin  docs  include  jre  lib  man  src.zip  THIRD_PARTY_README
```

```
gedit /home/$USER/.bashrc
.
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
.
source /home/$USER/.bashrc
.
echo $JAVA_HOME
.
/usr/lib/jvm/java-8-openjdk-amd64
```

## Set Bamboo Home

Create Bamboo home directory for config and data

```
mkdir /home/$USER/bamboo-home
```

Use hard coded path

```
gedit /home/$USER/bamboo/atlassian-bamboo/WEB-INF/classes/bamboo-init.properties
.
bamboo.home=/home/test/bamboo-home
```

# Start Bamboo

```
/home/test/bamboo/bin/start-bamboo.sh
.
To run Bamboo in the foreground, start the server with start-bamboo.sh -fg

Server startup logs are located in /home/test/bamboo/logs/catalina.out

Bamboo Data Center
   Version : 8.0.5


If you encounter issues starting or stopping Bamboo Server, please see the Troubleshooting guide at https://confluence.atlassian.com/display/BAMBOO/Installing+and+upgrading+Bamboo

Using CATALINA_BASE:   /home/test/bamboo
Using CATALINA_HOME:   /home/test/bamboo
Using CATALINA_TMPDIR: /home/test/bamboo/temp
Using JRE_HOME:        /usr/lib/jvm/java-8-openjdk-amd64
Using CLASSPATH:       /home/test/bamboo/bin/bootstrap.jar:/home/test/bamboo/bin/tomcat-juli.jar
Using CATALINA_OPTS:
Tomcat started.
```

# Complete Bamboo Wizard

http://localhost:8085/
