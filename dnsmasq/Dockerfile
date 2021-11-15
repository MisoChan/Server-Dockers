FROM alpine

ARG RESPONSE_IPv4="192.168.1.5"
ARG RESPONSE_IPv6="::"
ARG FORWARDER_PRIMARY_IP="5.2.75.75"
ARG FORWARDER_SECONDARY_IP="45.67.219.208"

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
echo "domain-needed" >> /etc/dnsmasq.conf && \
echo "bogus-priv" >> /etc/dnsmasq.conf && \
echo "no-resolv" >> /etc/dnsmasq.conf && \
echo "no-poll" >> /etc/dnsmasq.conf && \
echo -e server=${FORWARDER_PRIMARY_IP} >> /etc/dnsmasq.conf && \
echo -e server=${FORWARDER_SECONDARY_IP} >> /etc/dnsmasq.conf && \
bash $EXEC_SHELL 


CMD ["dnsmasq","--no-daemon"]


