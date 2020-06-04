# Maven

```
sudo apt remove maven

https://github.com/wolf99/dotfiles/blob/master/how-to-update-maven.md

cd ~/Downloads

latest_maven=$(wget -qO- https://maven.apache.org/download.cgi | grep -Po "(?<=Apache Maven )[^ ]+(?= is the latest)")
echo $latest_maven
wget http://www-eu.apache.org/dist/maven/maven-3/$latest_maven/binaries/apache-maven-$latest_maven-bin.tar.gz
tar xvf apache-maven-$latest_maven-bin.tar.gz
sudo rm -r /opt/maven/
sudo mv apache-maven-$latest_maven /opt/maven/
ls /opt/maven
```

```
sudo vi /etc/profile.d/maven.sh
```

SHIFT-INS to paste:

```
export MAVEN_HOME=/opt/maven
export PATH=${MAVEN_HOME}/bin:${PATH}
```

```
sudo chmod +x /etc/profile.d/maven.sh
source /etc/profile.d/maven.sh
mvn --version
.
Apache Maven 3.6.3 (cecedd343002696d0abb50b32b541b8a6ba2883f)
Maven home: /opt/maven
Java version: 1.8.0_252, vendor: Private Build, runtime: /usr/lib/jvm/java-8-openjdk-amd64/jre
Default locale: en_GB, platform encoding: UTF-8
OS name: "linux", version: "5.4.0-31-generic", arch: "amd64", family: "unix"
```

Check `MAVEN_HOME`

```
printenv | grep MAVEN
.
MAVEN_HOME=/opt/maven
```
