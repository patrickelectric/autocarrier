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

RUN mkdir -p "/tmp/mavp2p" \
    && if [ "${PLATFORM}" = "amd64" ]; then \
        curl -sL https://github.com/bluenviron/mavp2p/releases/download/v1.1.1/mavp2p_v1.1.1_linux_amd64.tar.gz | tar -zxf - -C "/tmp/mavp2p"; \
    elif [ "${PLATFORM}" = "arm" ]; then \
        curl -sL https://github.com/bluenviron/mavp2p/releases/download/v1.1.1/mavp2p_v1.1.1_linux_armv7.tar.gz | tar -zxf - -C "/tmp/mavp2p"; \
    elif [ "${PLATFORM}" = "arm64" ]; then \
        curl -sL https://github.com/bluenviron/mavp2p/releases/download/v1.1.1/mavp2p_v1.1.1_linux_arm64v8.tar.gz | tar -zxf - -C "/tmp/mavp2p"; \
    fi \
    && echo $(ls "/tmp/mavp2p") \
    && echo $(ls "/usr/local/bin") \
    && mv "/tmp/mavp2p/mavp2p" "/usr/local/bin/mavp2p" \
    && rm -rf "/tmp/mavp2p" \
    && chmod +x "/usr/local/bin/mavp2p"

ENTRYPOINT ["/usr/local/bin/mavp2p"]
