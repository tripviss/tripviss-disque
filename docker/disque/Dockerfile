FROM quay.io/tripviss/disque:1.0-rc1-alpine

# persistent / runtime deps
RUN apk add --no-cache --virtual .persistent-deps \
		ca-certificates \
		curl

ENV CONFD_VERSION 0.11.0

RUN curl -fSL https://github.com/kelseyhightower/confd/releases/download/v$CONFD_VERSION/confd-$CONFD_VERSION-linux-amd64 -o /usr/local/bin/confd \
	&& chmod +x /usr/local/bin/confd

COPY confd /usr/local/etc/confd/

RUN mkdir -p /usr/local/etc/disque

COPY docker-healthcheck /usr/local/bin/
RUN chmod +x /usr/local/bin/docker-healthcheck

HEALTHCHECK CMD ["docker-healthcheck"]

COPY docker-start /usr/local/bin/
RUN chmod +x /usr/local/bin/docker-start

CMD ["docker-start"]
