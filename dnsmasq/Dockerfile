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
bash $EXEC_SHELL && \
cat $DIRECTORY/hostnames_raw.txt $DIRECTORY/static_blockhosts.txt >> $DIRECTORY/hostnames.txt &&\
cat $DIRECTORY/malware.txt |grep -E '^address'|sed -e  "s/127.0.0.1/$RESOLUTION/g" >> $DIRECTORY/domains.txt && \
cat $DIRECTORY/pgl.txt |grep -E '^address'|sed -e "s/127.0.0.1/$RESOLUTION/g" >> $DIRECTORY/domains.txt && \
cat $DIRECTORY/warui_host.txt >> $DIRECTORY/hostnames.txt && \
cat $DIRECTORY/static_blockdomain.txt >> $DIRECTORY/domains.txt && \
cat $DIRECTORY/static_blockhosts.txt >> $DIRECTORY/hostnames.txt && \
sed -i  "s/127\.0\.0\.1 /$RESPONSE_IPv4 /g" $DIRECTORY/hostnames.txt  && \
sed -i  "s/0\.0\.0\.0 /$RESPONSE_IPv4 /g" $DIRECTORY/hostnames.txt && \
sed -i  "s/:: /$RESPONSE_IPv6 /g" $DIRECTORY/hostnames.txt && \
sed -i  "s/127\.0\.0\.1/$RESPONSE_IPv4/g" $DIRECTORY/domains.txt && \
sed -i  "s/0\.0\.0\.0/$RESPONSE_IPv4/g" $DIRECTORY/domains.txt 

CMD ["dnsmasq","--no-daemon"]


