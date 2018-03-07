---
layout: post
title:  "NGINX reverse proxy setting with Elasticsearch-KIBANA"
date:   2018-03-07 14:39:25 +0900
comments: true
categories: tech
---

in /etc/nginx/conf.d/<vhost>.conf

```
location /analytics/ {
	rewrite /analytics/(.*) /$1 break;
	proxy_pass http://localhost:19901;	# configured kibana port

	proxy_ignore_client_abort on;
	proxy_set_header X-Real-IP $remote_addr;
	proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
	proxy_set_header Host $http_post;

	allow x.x.x.0/24;	# ACL
	deny all;

	auth_ldap "blah blah";
	auth_ldap_servers <ldap_server>;
}
```

in /etc/kibana/kibana.yml

```
server.port: 19901
server.host: "localhost"
server.basePath: "/analytics"
```

