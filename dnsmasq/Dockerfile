FROM alpine

ARG RESPONSE_IPv4="127.0.0.1"
ARG RESPONSE_IPv6="::"

ENV DIRECTORY="/Server-Dockers/dnsmasq/dns_blocks"
ENV EXEC_SHELL="/Server-Dockers/dnsmasq/MalwareBlockDNS_dnsmasq.sh"

RUN apk update && \
apk add bash git dnsmasq && \ 
rm -rf /var/cache/apk/* 

#キャッシュ回避
ADD MalwareBlockDNS_dnsmasq.sh /data/
RUN git clone https://github.com/MisoChan/Server-Dockers 

run mkdir -p /etc/default/
RUN echo -e "ENABLED=1\nIGNORE_RESOLVCONF=yes" > /etc/default/dnsmasq && \ 
echo -e addn-hosts=${DIRECTORY}/hostnames.txt >> /etc/dnsmasq.conf && \
echo -e conf-file=${DIRECTORY}/domains.txt >> /etc/dnsmasq.conf && \
bash $EXEC_SHELL $


CMD ["dnsmasq","--no-daemon"]


