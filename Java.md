# Java

# Install Java 8 SDK

```
sudo apt install openjdk-8-jdk openjdk-8-jre
java -version
.
openjdk version "1.8.0_252"
OpenJDK Runtime Environment (build 1.8.0_252-8u252-b09-1ubuntu1-b09)
OpenJDK 64-Bit Server VM (build 25.252-b09, mixed mode)
```

# Set JAVA_HOME

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
