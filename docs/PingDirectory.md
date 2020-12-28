# PingDirectory Install

## OS Setup
1. useradd pinguser
1. mkdir /data /data/ping /data/java
1. Download jdk-11.0.9_linux-x64_bin.tar to /data/java
1. Download PingDirectory-8.1.0.2.zip and PingDirectory-8.2-Production.lic to /data/ping
1. chown -R pinguser:pinguser /data

## Setup Java
1. cd /data/java
1. tar -xxvf jdk-11.0.9_linux-x64_bin.tar.gz
1. echo "export JAVA_HOME=/data/java/jdk-11.0.9" >> /etc/profile.d/java.sh
1. echo "export PATH=$JAVA_HOME/bin:$PATH" >> /etc/profile.d/java.sh
1. Verify by logging out and back in
    1. `which java` and `java -version` should display installed java and version.

## Install PingDirectory
1. su pinguser
1. cd /data/ping
1. unzip PingDirectory-8.1.0.2.zip
1. mv PingDirectory-8.2-Production.lic PingDirectory
1. cd PingDirectory
1. ./setup
1. 