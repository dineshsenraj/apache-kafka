# Apache Kafka on Ubuntu

## Installation

Once Logged in to the Machine switch to root user using ```bash sudo -i``` command

### Install Java

Install Java 16 Manually using below commands

```bash
mkdir /opt/jdk-16
cd /opt/jdk-16/
wget https://download.java.net/java/GA/jdk16.0.1/7147401fd7354114ac51ef3e1328291f/9/GPL/openjdk-16.0.1_linux-x64_bin.tar.gz
tar -zxf openjdk-16.0.1_linux-x64_bin.tar.gz 
cd jdk-16.0.1/
ls -lsa
sudo update-alternatives --install /usr/bin/java java /opt/jdk-16/jdk-16.0.1/bin/java 100
sudo update-alternatives --config java
java -version
```