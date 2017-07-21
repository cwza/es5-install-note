# Install elasticsearch 5.x cluster and x-pack and kibana
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

## Install es5.x
``` sh
curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.4.1.deb
sudo dpkg -i elasticsearch-5.4.1.deb
```

## File Location
* elasticsearch - /usr/share/elasticsearch
* config - /etc/elasticsearch
* init script - /etc/init.d/elasticsearch
* data - /var/lib/elasticsearch
* logs - /var/log/elasticsearch

## install x-pack plugin
``` sh
sudo /usr/share/elasticsearch/bin/elasticsearch-plugin install x-pack
```

## es settings
* edit /etc/elasticsearch/elasticsearch.yml. see [elasticsearch.yml](elasticsearch.yml)
* edit /etc/elasticsearch/jvm.options.
``` sh
-Xms3800m # half of the physical memory
-Xmx3800m
```
https://www.elastic.co/guide/en/elasticsearch/reference/current/setting-system-settings.html
* Add /etc/systemd/system/elasticsearch.service.d/elasticsearch.conf
```
[Service]
LimitMEMLOCK=infinity
```

## start es
* logout and login
``` sh
sudo systemctl enable elasticsearch.service
sudo systemctl daemon-reload
sudo systemctl restart elasticsearch
```

## userful command
``` sh
curl -XPUT -H 'Content-Type:application/json' -d @mappings.json http://localhost:9200/2910eb12_d64a_49cc_b2be_54201441e27b
curl -XDELETE http://localhost:9200/2910eb12_d64a_49cc_b2be_54201441e27b
journalctl -f -u elasticsearch 
```

-------------------------------

# Install Kibana
``` sh
wget https://artifacts.elastic.co/downloads/kibana/kibana-5.4.1-amd64.deb
sudo dpkg -i kibana-5.4.1-amd64.deb
```

## file location
* kibana - /usr/share/kibana
* config - /etc/kibana/kibana.yml
* data - /var/lib/kibana

## install x-pack plugin
``` sh
sudo /usr/share/kibana/bin/kibana-plugin install x-pack
```

## configure
edit /etc/kibana/kibana.yml. see [kibana.yml](kibana.yml)

## start kibana
``` sh
sudo systemctl daemon-reload
sudo systemctl enable kibana.service
sudo systemctl start kibana.service
```

## trouble shoot
```
FATAL { Error: EACCES: permission denied, open '/usr/share/kibana/optimize/bundles/monitoring.
sudo chown -R kibana:kibana /usr/share/kibana/
```

-------------------------------

# Install x-pack license
https://www.elastic.co/subscriptions
* update license(Run at each node)
``` sh
curl -XPUT 'http://localhost:9200/_xpack/license?acknowledge=true' -H "Content-Type: application/json" -d @/tmp/license.json
```
* view license
``` sh
curl -XGET 'http://localhost:9200/_xpack/license'
```

-------------------------------


## install go
``` sh
sudo add-apt-repository ppa:longsleep/golang-backports
sudo apt-get update
sudo apt-get install golang-go
```
