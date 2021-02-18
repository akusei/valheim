FROM ubuntu:latest

COPY entrypoint /usr/bin/entrypoint

RUN apt-get update && apt-get install -y lib32gcc1 curl && \
    chmod a+x /usr/bin/entrypoint && \
    mkdir -p /steam /config/unity3d/IronGate && \
    cd /steam && \
    curl -sqL "https://steamcdn-a.akamaihd.net/client/installer/steamcmd_linux.tar.gz" | tar zxvf - && \
    useradd --no-create-home --system --user-group valheim && \
    rm -rf /var/lib/apt/lists/*

EXPOSE 2456 2457 2458
VOLUME /server /data

ENTRYPOINT ["/usr/bin/entrypoint"]
