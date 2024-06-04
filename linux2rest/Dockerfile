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

RUN if [ "${PLATFORM}" = "x86_64" ]; then \
        curl -L -o /usr/local/bin/linux2rest https://github.com/patrickelectric/linux2rest/releases/download/v0.6.0/linux2rest-x86_64-unknown-linux-gnu; \
    elif [ "${PLATFORM}" = "arm" ]; then \
        curl -L -o /usr/local/bin/linux2rest https://github.com/patrickelectric/linux2rest/releases/download/v0.6.0/linux2rest-armv7-unknown-linux-gnueabihf; \
    elif [ "${PLATFORM}" = "arm64" ]; then \
        curl -L -o /usr/local/bin/linux2rest https://github.com/patrickelectric/linux2rest/releases/download/v0.6.0/linux2rest-aarch64-unknown-linux-gnu; \
    fi \
    && chmod +x /usr/local/bin/linux2rest

ENTRYPOINT ["/usr/local/bin/linux2rest"]