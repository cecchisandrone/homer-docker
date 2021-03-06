FROM debian:jessie
MAINTAINER L. Mangani <lorenzo.mangani@gmail.com>
# v.5.02

# Default baseimage settings
ENV HOME /root
ENV DEBIAN_FRONTEND noninteractive

# Update and upgrade apt
RUN apt-get update -qq

# Kamailio + sipcapture module
RUN apt-key adv --recv-keys --keyserver hkp://keyserver.ubuntu.com:80 0xfb40d3e6508ea4c8
RUN echo "deb http://deb.kamailio.org/kamailio jessie main" >> etc/apt/sources.list
RUN echo "deb-src http://deb.kamailio.org/kamailio jessie main" >> etc/apt/sources.list
RUN apt-get update -qq && apt-get install -f -yqq curl kamailio rsyslog kamailio-outbound-modules kamailio-geoip-modules kamailio-sctp-modules kamailio-tls-modules kamailio-websocket-modules kamailio-utils-modules kamailio-mysql-modules kamailio-extra-modules && rm -rf /var/lib/apt/lists/*

COPY kamailio.cfg /etc/kamailio/kamailio.cfg
RUN chmod 775 /etc/kamailio/kamailio.cfg

RUN ln -s /usr/lib64 /usr/lib/x86_64-linux-gnu/

# GeoIP (http://dev.maxmind.com/geoip/legacy/geolite/)
RUN cd /usr/share/GeoIP && curl http://geolite.maxmind.com/download/geoip/database/GeoLiteCity.dat.gz > GeoLiteCity.dat.gz && gunzip GeoLiteCity.dat.gz

COPY run.sh /run.sh

# HEP
EXPOSE 9060

ENTRYPOINT ["/run.sh"]
