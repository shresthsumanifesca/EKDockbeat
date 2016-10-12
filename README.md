# Da solution

This solution can be used to get some metrics about docker-engines and docker containers.
It's purely metrology and provide a lot of informations like CPU and mem usage, as well as network metrics ; per host, per engine, per containers. 

- ElasticSearch (elasticsearch:latest)
- Kibana (rebuild FROM kibana:latest)
- Dockbeat (FROM alpine:latest, inspired by https://hub.docker.com/r/redmatter/dockbeat/)
- This implementation is using static strings to get Dockbeat and Dockbeat's glibc
  - You actually need to change a few env vars in dockbeatuild/Dockerfile to change these versions
- And also, it's mounting /var/run/docker.sock to get informations about docker-engine and his containers

# Usage

- ``` $ cd EKDockbeat && docker-compose up -d ```
- Now open a browser and go ```http://localhost:5601``` and you should get Kibana's UI
- Specify ```dockbeat-*``` in the "*Index name or pattern*" field
- And then select the @timestamp filter to create the new index pattern
- There you go :)

# Customization

- Dockbeat's configuration is in config/dockbeat.yml
- Kibana's is in kibana/config/kibana.yml
- Dockbeat is linked with ES using docker links, as well as Kibana
- Each and every port is publicly exposed on host (9200 & 9300 for EL, 5601 for Kibana)
