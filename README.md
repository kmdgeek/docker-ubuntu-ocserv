# docker-ubuntu-ocserv

A docker for ocserv.

## Preparation

Since this docker does **not** automatically generate any configuration files or TLS certificate, you must prepare for these file before starting the container. 

You can place all necessary files in a folder as below and mount this folder to `/etc/ocserv` when you run the container. By default ocserv looks for its [configuration file](https://gitlab.com/ocserv/ocserv/blob/master/doc/sample.config) at `/etc/ocserv/ocserv.conf`

```
ocserv/
├── certs
│	├── ca.crt
│	├── server.crt
│	└── server.key
├── config-per-group
│	├── group1
│	└── group2
├── ocpasswd
└── ocserv.conf
```

## Example

Start a container:

```shell
docker run --name ocserv \
	-d --privileged \
	-p 443:443 -p 443:443/udp \
	-v /some-path/ocserv:/etc/ocserv:rw \
	kmdgeek/ubuntu-ocserv
```

Create a user in group1:

```shell
docker exec -it ocserv \
	ocpasswd --passwd=/etc/ocserv/ocpasswd --groupname=group1 user1
```

