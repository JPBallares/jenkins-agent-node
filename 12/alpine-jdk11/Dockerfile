FROM jenkins/agent:alpine-jdk11

EXPOSE 3000

# update the version and match the checksum
# check https://unofficial-builds.nodejs.org/download/release/
ENV NODE_VERSION 12.22.5
ENV CHECKSUM 1c8ce0d58828faff84486dc116ec817595841c8578ed01266eb69e5383c73201
ENV ARCH x64

USER root
RUN addgroup -g 1001 node \
  && adduser -u 1001 -G node -s /bin/sh -D node \
  && apk add --no-cache libstdc++ \
  && apk add --no-cache --virtual .build-deps curl \
  && apk add --no-cache make

RUN set -eu; \
  curl -fsSLO --compressed "https://unofficial-builds.nodejs.org/download/release/v$NODE_VERSION/node-v$NODE_VERSION-linux-$ARCH-musl.tar.xz"; \
  echo "$CHECKSUM  node-v$NODE_VERSION-linux-$ARCH-musl.tar.xz" | sha256sum -c - \
  && tar -xJf "node-v$NODE_VERSION-linux-$ARCH-musl.tar.xz" -C /usr/local --strip-components=1 --no-same-owner \
  && ln -s /usr/local/bin/node /usr/local/bin/nodejs;

USER jenkins
