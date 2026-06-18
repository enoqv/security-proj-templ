# syntax=docker/dockerfile:1.24@sha256:87999aa3d42bdc6bea60565083ee17e86d1f3339802f543c0d03998580f9cb89
FROM alpine:3.21

RUN apk add --no-cache \
      squid \
      inotify-tools \
      curl \
      ca-certificates \
      bash \
      netcat-openbsd

# Ensure runtime directories exist and are owned by the squid user that
# the `squid` package creates. On Alpine the effective user is `squid`
# (not `proxy` as on Debian).
RUN mkdir -p /var/log/squid /var/spool/squid /var/cache/squid /run/squid && \
    chown -R squid:squid /var/log/squid /var/spool/squid /var/cache/squid /run/squid

COPY entrypoint.sh /usr/local/bin/squid-entrypoint.sh
RUN chmod +x /usr/local/bin/squid-entrypoint.sh

EXPOSE 3128
ENTRYPOINT ["/usr/local/bin/squid-entrypoint.sh"]
