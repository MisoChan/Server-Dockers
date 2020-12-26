## 1. What is this
A DNS server that cannot resolve URLs that are reported as dangerous sites, ad trackings, and armful content.

## 2. How to use
Execute commands on this directory
```
docker build .

docker docker run --name=dns_server --restart=always -p 53:53/udp -itd [image-SHA]
```

## 3. URL Lists Source

* pgl.yoyo.org  
https://pgl.yoyo.org/

* 悪いインターネット  
https://warui.intaa.net

* Malwarelist  
https://www.malwaredomainlist.com
