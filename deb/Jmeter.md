# Jmeter remote load test
## Install JDK8
``` sh
sudo add-apt-repository ppa:webupd8team/java
sudo apt-get update
sudo apt-get install oracle-java8-installer
```
edit /etc/environment configuration file and add following entries to set JAVA_HOME and JRE_HOME environment variables
``` sh
JAVA_HOME=/usr/lib/jvm/java-8-oracle
JRE_HOME=/usr/lib/jvm/java-8-oracle/jre
```

## Install Jmeter
``` sh
curl -L -O http://apache.stu.edu.tw/jmeter/binaries/apache-jmeter-3.2.tgz
tar xvf apache-jmeter-3.2.tgz
```

## jmeter gui
use jmeter gui to create testplan

## jmeter cluster
### jmeter worker
``` sh
JVM_ARGS="-Xms1920m -Xmx1920m" ./jmeter-server
```
### jmeter client
edit bin/jmeter.properties
``` sh
remote_hosts=127.0.0.1,10.240.0.3,10.240.0.2
```
``` sh
JVM_ARGS="-Xms1920m -Xmx1920m" ./jmeter -n -t ../testplan/search.jmx
./stoptest.sh -R 10.240.0.3,10.240.0.2
```