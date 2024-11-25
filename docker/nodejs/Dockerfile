ARG NODE_VERSION=20
ARG FIXUID_VERSION=0.6.0

FROM node:${NODE_VERSION}-alpine

ARG FIXUID_VERSION

RUN apk --no-cache add curl

COPY docker-entrypoint /usr/local/bin/

RUN USER=node && \
    GROUP=node && \
    if [[ "$(uname -m)" = "aarch64" ]] ; \
      then \
        curl -SsL https://github.com/boxboat/fixuid/releases/download/v${FIXUID_VERSION}/fixuid-${FIXUID_VERSION}-linux-arm64.tar.gz | tar -C /usr/local/bin -xzf - ;\
      else \
        curl -SsL https://github.com/boxboat/fixuid/releases/download/v${FIXUID_VERSION}/fixuid-${FIXUID_VERSION}-linux-amd64.tar.gz | tar -C /usr/local/bin -xzf - ;\
    fi; \
    chown root:root /usr/local/bin/fixuid && \
    chmod 4755 /usr/local/bin/fixuid && \
    mkdir -p /etc/fixuid && \
    printf "user: $USER\ngroup: $GROUP\n" > /etc/fixuid/config.yml

USER node:node

ENTRYPOINT ["docker-entrypoint"]
