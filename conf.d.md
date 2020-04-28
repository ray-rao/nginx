#### gitlab.conf
```
upstream gitlab {
    server 192.168.1.136:8090;
}

server {
    listen 80;
    server_name gitlab.jskj.com;
    charset utf-8;
    location / {
        proxy_pass http://gitlab;
        proxy_set_header Host $host;
    }
}
[root@ecs-1067 conf.d]# ls
gitlab.conf  jenkins.conf  nacos.conf  nexus.conf  svc.conf
[root@ecs-1067 conf.d]# more gitlab.conf 
upstream gitlab {
    server 192.168.1.136:8090;
}

server {
    listen 80;
    server_name gitlab.jskj.com;
    charset utf-8;
    location / {
        proxy_pass http://gitlab;
        proxy_set_header Host $host;
    }
}
```
### jenkins.conf
```
upstream jenkins {
    server 192.168.1.136:8080;
}

server {
    listen 80;
    server_name jenkins.jskj.com;
    charset utf-8;
    location / {
        proxy_pass http://jenkins;
        proxy_set_header Host $host;
    }
}
```
### nexus.conf
```
upstream nexus {
    server 192.168.1.136:8081;
}

upstream docker-registry {
    server 192.168.1.136:8082;
}

upstream mq {
    server 192.168.1.236:15672;
}

server {
    listen 80;
    server_name nexus.jskj.com;
    charset utf-8;
    
    location / {
        proxy_pass http://nexus;
        proxy_set_header Host $host;
    }
}

server {
    listen 80;
    server_name registry.jskj.com;
    charset utf-8;
    location / {
        proxy_pass http://docker-registry;
        proxy_set_header Host $host;
    }
}

server {
    listen 80;
    server_name mq.jskj.com;
    charset utf-8;
    location / {
        proxy_pass http://mq;
        proxy_set_header Host $host;
     }
}

```
### svc.conf
```
upstream eureka {
    server 192.168.1.136:8761;
}
upstream api {
    server 192.168.1.136:5020;
}
upstream web {
    server 192.168.1.136:8100;
}

server {
    listen 80;
    server_name eureka-server.qdjy.com eureka-server;
    charset utf-8;
    
    location / {
        proxy_pass http://eureka;
        proxy_set_header Host $host;
    }
}

server {
    listen 80;
    server_name api.qdjy.com;
    charset utf-8;
    location / {
        proxy_pass http://api;
        proxy_set_header Host $host;
    }
}

server {
    listen 80;
    server_name www.qdjy.com;
    charset utf-8;
    location / {
        proxy_pass http://web;
        proxy_set_header Host $host;
    }
}

```
