FROM alpine:3.12.1

RUN apk update \
 && apk add jq \
 && rm -rf /var/cache/apk/*

ENTRYPOINT ["/usr/bin/jq"]
