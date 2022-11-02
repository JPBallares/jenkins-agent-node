FROM jenkins/agent:alpine-jdk11

# update the version and match the checksum
# check https://unofficial-builds.nodejs.org/download/release/
ENV NODE_VERSION 14.21.0
ENV CHECKSUM b7d90dae42a75531ff4b29f3c843927c63677f7dbd30dda299ac3d3da65f828b
ENV ARCH x64

USER root
RUN addgroup -g 1001 node \
  && adduser -u 1001 -G node -s /bin/sh -D node \
  && apk add --no-cache libstdc++ \
  && apk add --no-cache --virtual .build-deps curl

RUN set -eu; \
  curl -fsSLO --compressed "https://unofficial-builds.nodejs.org/download/release/v$NODE_VERSION/node-v$NODE_VERSION-linux-$ARCH-musl.tar.xz"; \
  echo "$CHECKSUM  node-v$NODE_VERSION-linux-$ARCH-musl.tar.xz" | sha256sum -c - \
  && tar -xJf "node-v$NODE_VERSION-linux-$ARCH-musl.tar.xz" -C /usr/local --strip-components=1 --no-same-owner \
  && ln -s /usr/local/bin/node /usr/local/bin/nodejs;

USER jenkins
