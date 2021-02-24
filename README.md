# prometheus-grafana-alertmanager

This project contains the docker configuration needed to lunch prometheus, grafana, and alert manager with docker-compose.
This stack is used to monitor, trace and observe the behaviour of our microservices and alert us if something happens.

## Integration example

1 - Add this dependency to the project you want to monitor :

```xml
 <dependency>
    <groupId>io.micrometer</groupId>
    <artifactId>micrometer-registry-prometheus</artifactId>
 </dependency>
```

2 - Add this configuration to your application.yml of the project you want to monitor

```
management:
  endpoint:
    metrics:
      enabled: true
    prometheus:
      enabled: true
  endpoints:
    web:
      exposure:
        include: prometheus
  metrics:
    export:
      prometheus:
        enabled: true
```

3 - Update configuration files of this project. In particular, URLs and alert manager rules.

4 - Run prometheus, grafana and alertmanager using docker-compose

```dockerfile 
docker-compose up -d --build
```

5 - URLs :

Prometheus :
http://192.168.99.100:9090/

Grafana :
http://192.168.99.100:3000/

Alertmanager :
http://192.168.99.100:9093/