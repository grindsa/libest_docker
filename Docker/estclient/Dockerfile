FROM ubuntu:20.04
LABEL maintainer="grindelsack@gmail.com"

RUN apt-get update
RUN DEBIAN_FRONTEND="noninteractive" apt-get -y install tzdata

RUN apt-get install --no-install-recommends -y \
    openssl \
    curl \
    ca-certificates \
    && rm -rf /var/lib/apt/lists/*

# download libest
RUN curl https://raw.githubusercontent.com/grindsa/libest_docker/main/deb/estclient_3.2.0-1_amd64.deb --output /tmp/client.deb \
    && dpkg -i /tmp/client.deb \
    && rm -rf /tmp/client.deb \
    && ln -s /usr/local/est/bin/estclient /usr/local/bin/estclient.cisco \
    && mkdir -p /usr/local/go/bin

# install gobalsign go client
# WORKDIR /tmp
# RUN pwd && ls -la

ADD go /usr/local/go

RUN ln -s /usr/local/go/bin/estclient /usr/local/bin/estclient.globalsign

RUN printf "%b" '#!'"/usr/bin/env sh\n \
exec \"\$@\"\n \
" >/entrypoint.sh && chmod +x /entrypoint.sh

ENTRYPOINT ["/entrypoint.sh"]
