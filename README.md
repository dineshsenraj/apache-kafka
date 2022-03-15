# Apache Kafka on Ubuntu

## Installation

Once Logged in to the Machine switch to root user using ```sudo -i``` command

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

### Download Kafka

Try the command to download kafka from apache website, always download **Binary** files and not the **Source**

```bash
mkdir kafka
cd kafka
wget https://www.apache.org/dyn/closer.cgi?path=/kafka/3.1.0/kafka_2.13-3.1.0.tgz
```
If the command gives certificate error add ```--no-check-certificate``` to the command.

If still it returns any error like 403 Forbidden, Download the file in your local and copy to the server through SFTP.

### Install Kafka

Extract the binary file to install

```bash
tar xzf kafka_2.13-3.0.0.tgz
mv kafka_2.13-3.0.0 /usr/local/kafka
```

### Setup Systemd file for Kafka

```bash
cd /etc/systemd/system
touch zookeeper.service
vi zookeeper.service
```

Add the below lines

```
[Unit]
Description=Apache Zookeeper server
Documentation=http://zookeeper.apache.org
Requires=network.target remote-fs.target
After=network.target remote-fs.target

[Service]
Type=simple
ExecStart=/usr/local/kafka/bin/zookeeper-server-start.sh /usr/local/kafka/config/zookeeper.properties
ExecStop=/usr/local/kafka/bin/zookeeper-server-stop.sh
Restart=on-abnormal

[Install]
WantedBy=multi-user.target
```