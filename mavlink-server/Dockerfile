FROM debian:bookworm-slim

RUN apt-get update && apt-get install -y --no-install-recommends \
    curl ca-certificates \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Define arguments for target platform
# These arguments are defined automatically by buildx when using `--platform`
ARG TARGETARCH
ARG TARGETVARIANT

ARG PLATFORM
ENV PLATFORM=${PLATFORM:-$TARGETARCH}
ENV TARGETARCH=$TARGETARCH

RUN echo "Platform: ${PLATFORM} ${TARGETARCH}"

RUN if [ "${PLATFORM}" = "amd64" ]; then \
        curl -L -o /usr/local/bin/mavlink-server https://github.com/bluerobotics/mavlink-server/releases/download/0.1.0/mavlink-server-x86_64-unknown-linux-musl; \
    elif [ "${PLATFORM}" = "arm" ]; then \
        curl -L -o /usr/local/bin/mavlink-server https://github.com/bluerobotics/mavlink-server/releases/download/0.1.0/mavlink-server-armv7-unknown-linux-musleabihf; \
    elif [ "${PLATFORM}" = "arm64" ]; then \
        curl -L -o /usr/local/bin/mavlink-server https://github.com/bluerobotics/mavlink-server/releases/download/0.1.0/mavlink-server-aarch64-unknown-linux-musl; \
    fi \
    && chmod +x /usr/local/bin/mavlink-server

ENTRYPOINT ["/usr/local/bin/mavlink-server"]
