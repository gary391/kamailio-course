FROM debian:trixie-20230725

RUN apt-get update \
  && apt-get install -y --no-install-recommends ca-certificates gcc g++ make build-essential git pkg-config libxtables-dev libavfilter-dev \
  libevent-dev libpcap-dev libxmlrpc-core-c3-dev bash\
  libjson-glib-dev default-libmysqlclient-dev libhiredis-dev libssl-dev libjwt-dev libiptc-dev \
  libcurl4-openssl-dev libavcodec-extra gperf libspandsp-dev libwebsockets-dev libpcre2-dev libopus-dev libmosquitto-dev libwebsockets-dev libbcg729-dev\
  libmnl-dev libnftnl-dev libncurses5-dev libncursesw5-dev\
  && cd /usr/local/src \
  && git clone https://github.com/sipwise/rtpengine.git \
  && cd rtpengine \
  && make -C daemon rtpengine \
  && cp /usr/local/src/rtpengine/daemon/rtpengine /usr/local/bin/rtpengine \
  && rm -Rf /usr/local/src/rtpengine \
  && apt-get purge -y --quiet --force-yes --auto-remove \
  ca-certificates gcc g++ make build-essential git \
  && rm -rf /var/lib/apt/* \
  && rm -rf /var/lib/dpkg/* \
  && rm -rf /var/lib/cache/* \
  && rm -Rf /var/log/* \
  && rm -Rf /usr/local/src/* \
  && rm -Rf /var/lib/apt/lists/* 

VOLUME ["/tmp"]

EXPOSE 23000-32768/udp 22222/udp

COPY ./entrypoint.sh /entrypoint.sh

#ENTRYPOINT ["/entrypoint.sh"]

#CMD ["rtpengine", "--config-file", "/etc/rtpengine/rtpengine.conf"]
CMD ["tail", "-f", "/dev/stdout"]
