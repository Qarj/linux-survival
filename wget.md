# wget

```
sudo wget --directory-prefix /etc/ssl/certs http://curl.haxx.se/ca/cacert.pem
```

# wget maven

```
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

# wget AuctioneerSuite

Put desired regex in variable for higher compatibility.

```bash
cd /home/tim/Downloads
auctioneer_versions=$(wget -qO- https://www.auctioneeraddon.com/zip/versions.json)
regex="nightly[^]]+AuctioneerSuite[^]]+version[^0-9]+([0-9.]+)"
[[ $auctioneer_versions =~ $regex ]]
echo ${BASH_REMATCH[1]}
latest_auctioneer=${BASH_REMATCH[1]}
wget https://www.auctioneeraddon.com/zip/AuctioneerSuite-$latest_auctioneer.zip
unzip AuctioneerSuite-$latest_auctioneer.zip -d AuctioneerSuite-$latest_auctioneer
```
