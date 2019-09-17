FROM alpine:3.10

RUN sed -i -e 's/v[[:digit:]]\..*\//edge\//g' /etc/apk/repositories

RUN apk update

RUN apk add xvfb xfce4 xfce4-terminal openbox faenza-icon-theme x11vnc chromium

RUN apk add supervisor sudo \
  && addgroup alpine \
  && adduser -G alpine -s /bin/sh -D alpine \
  && echo "alpine:alpine" | /usr/sbin/chpasswd \
  && echo "alpine    ALL=(ALL) ALL" >> /etc/sudoers \
  && mkdir -p /etc/supervisor/conf.d

RUN rm -Rf /tmp/* /var/cache/apk/*

RUN mkdir -p /var/log/supervisord/

ADD /services/supervisord.conf /etc/supervisord.conf
ADD /services/conf.d/* /etc/supervisor/conf.d/

CMD ["/usr/bin/supervisord", "-c", "/etc/supervisord.conf"]
