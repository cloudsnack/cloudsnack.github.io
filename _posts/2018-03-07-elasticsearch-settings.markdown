---
layout: post
title:  "Elasticsearch system settings on CentOS"
date:   2018-03-07 15:04:00 +0900
comments: true
categories: tech
---

in /etc/security/limits.d/99-elasticsearch.conf

```
elasticsearch soft nofile 65536
elasticsearch hard nofile 65536

elasticsearch soft memlock unlimited
elasticsearch hard memlock unlimited

elasticsearch soft nproc 4096
elasticsearch hard nproc 4096
```

sysctl

```
echo 262144 > /proc/sys/vm/max_map_count
```


in /etc/logrotate.d/elasticsearch

```
/path/to/log/*.log {
    daily
    rotate 100
    size 50M
    copytruncate
    compress
    delaycompress
    missingok
    notifempty
    create 644 elasticsearch elasticsearch
}
```
