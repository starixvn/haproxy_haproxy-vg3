FROM hub.lumigame.com/base/haproxy/haproxy-ubuntu:2.6-ci
ARG ENV
RUN mkdir -p /root/.ssh/
ADD dockerfiles/rsa /root/.ssh/
RUN chmod -R 600 /root/.ssh/
RUN ssh-keyscan -t rsa git3.nexdev.net >> /root/.ssh/known_hosts
RUN cd /srv/ && git clone git@git3.nexdev.net:haproxy/haproxy-default.git
RUN cd /srv/ && git clone git@git3.nexdev.net:haproxy/haproxy-sc1.git
RUN cd /srv/ && git clone git@git3.nexdev.net:haproxy/haproxy-vg2.git
#RUN cd /srv/haproxy-default && git fetch
#############
COPY configs/$ENV /usr/local/etc/haproxy/configs/$ENV
RUN cp /srv/haproxy-default/configs/$ENV/*.cfg /usr/local/etc/haproxy/configs/$ENV/
RUN cp /srv/haproxy-sc1/configs/$ENV/*.cfg /usr/local/etc/haproxy/configs/$ENV/
RUN cp /srv/haproxy-sc1/configs/$ENV/maps/*.map /usr/local/etc/haproxy/configs/$ENV/maps/
RUN cp /srv/haproxy-vg2/configs/$ENV/*.cfg /usr/local/etc/haproxy/configs/$ENV/
RUN cp /srv/haproxy-vg2/configs/$ENV/maps/*.map /usr/local/etc/haproxy/configs/$ENV/maps/
RUN ls /usr/local/etc/haproxy/configs/$ENV
RUN cat /usr/local/etc/haproxy/configs/$ENV/*.cfg > /usr/local/etc/haproxy/configs/$ENV/haproxy.cfg.tmp
RUN cp /usr/local/etc/haproxy/configs/$ENV/haproxy.cfg.tmp /usr/local/etc/haproxy/haproxy.cfg
RUN cp /srv/haproxy-default/whitelisted.ips /etc/haproxy/whitelisted.ips
RUN cp /srv/haproxy-default/certs/lumigame.com.pem /etc/haproxy/lumigame.com.pem
RUN mkdir /usr/local/etc/haproxy/maps
RUN cat /usr/local/etc/haproxy/configs/$ENV/maps/*.map > /usr/local/etc/haproxy/maps/hosts.map
RUN if [ -e /usr/local/etc/haproxy/configs/$ENV/special-maps ] ; then cp /usr/local/etc/haproxy/configs/$ENV/special-maps/* /usr/local/etc/haproxy/maps/ ; fi ;
RUN if [ -e /srv/haproxy-sc1/configs/$ENV/special-maps ] ; then cp /srv/haproxy-sc1/configs/$ENV/special-maps/* /usr/local/etc/haproxy/maps/ ; fi ;
RUN if [ -e /srv/haproxy-vg2/configs/$ENV/special-maps ] ; then cp /srv/haproxy-vg2/configs/$ENV/special-maps/* /usr/local/etc/haproxy/maps/ ; fi ;