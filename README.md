# ELK-stack-docker_compose
Elasticsearch, Logstash, Kibana combined to docker-compose file.

### Beats you can use with ELK stack to monitoring your environment
* Filebeat
* Packetbeat
* And many more
### How to use
#### Clone repo to your destination
```git clone git@github.com:vkv0220/ELK-stack-docker_compose.git```
#### Config your environment in .env file</p>
```vi .env```
#### Build and run stack
```cd ELK-stack-docker_compose && docker-compose up -d```

You can choose how to add autostart stack depends on your system (example below for systemd systems):

```
#/etc/systemd/system/elk-docker-compose-app.service
[Unit]
Description=Docker Compose Application Service
Requires=docker.service
After=docker.service

[Service]
Type=oneshot
RemainAfterExit=yes
WorkingDirectory=/opt/ELK-stack-docker_compose
ExecStart=/usr/local/bin/docker-compose up -d
ExecStop=/usr/local/bin/docker-compose down
TimeoutStartSec=0

[Install]
WantedBy=multi-user.target
```

```systemctl daemon-reload && systemctl enable elk-docker-compose-app```



### Filebeat config could be used with this stack:
```
#/etc/filebeat/filebeat.yml
#output to elasticsearch:
output.elasticsearch:
  #Array of hosts to connect to.
  hosts: ["elasticsearch-ip:9200"]
  protocol: "https"
  username: "elastic"
  password: "elastic"
  ssl.verification_mode: none
#or output to logstash
output.logstash:
  #The Logstash hosts
  hosts: ["logstash-ip:5044"]
```