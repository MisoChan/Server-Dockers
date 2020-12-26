## 1. What is this
A DNS server that cannot resolve URLs that are reported as dangerous sites.

## 2. How to use
Execute commands on this directory
```
docker build .

docker docker run --name=dns_server --restart=always -p 53:53/udp -itd [image-SHA]
```
