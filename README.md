# Local monitoring stack

A Docker Compose stack to monitor a local development machine, using Prometheus, Netdata and Grafana.

## Utilization

Start the stack with docker-compose:
```
docker-compose up -d
```

## Accessing

To access the resources through the NGINX proxy, add the following to your `/etc/hosts` file:
```
127.0.0.1       monitoring.local
127.0.0.1       grafana.local
127.0.0.1       netdata.local
127.0.0.1       prometheus.local
```

And access through a web browser regularly, e.g. [http://monitoring.local](http://monitoring.local).

Alternatively, if you don't want to edit your host files, you can access through the dynamically allocated port for a service, e.g.:

```
$~ docker-compose port prometheus 9090
0.0.0.0:49153
```

Then access through the browser, e.g. [http://0.0.0.0:49153](http://0.0.0.0:49153)

## Troubleshooting 

When starting the stack, if you encounter the following error message:

```
ERROR: for local-monit-stack_proxy_1  Cannot start service proxy: driver failed programming external connectivity on endpoint local-monit-stack_proxy_1 (aabb11): Bind for 0.0.0.0:80 failed: port is already allocated
```

It means you already have a service running on port 80. It could be another container, or a webserver installed in your machine (eg. Apache or NGINX). In this case you can remove the `80:80` port binding in the `docker-compose.yaml` file and access the stack through the dynamically allocated ports, as explained above.