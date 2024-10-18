from ubuntu:24.04

ARG DEBIAN_FRONTEND=noninteractive

# Define arguments for target platform
# These arguments are defined automatically by buildx when using `--platform`
ARG TARGETARCH
ARG TARGETVARIANT

ARG PLATFORM
ENV PLATFORM=${PLATFORM:-$TARGETARCH}
ENV TARGETARCH=$TARGETARCH

RUN echo "Platform: ${PLATFORM} ${TARGETARCH}"

RUN apt update -y && \
    apt install -y --no-install-recommends \
        ca-certificates \
        curl \
        gnupg \
        gstreamer1.0-libav \
        gstreamer1.0-nice \
        gstreamer1.0-plugins-ugly \
        gstreamer1.0-x \
        htop \
        libgstreamer-plugins-bad1.0-0 \
        libgstreamer-plugins-base1.0-0 \
        libgstreamer1.0-0 \
        libgstrtspserver-1.0-0 \
        wget

# We need libssl.so.1.1
# Note: if the link breaks, find it here: https://packages.ubuntu.com/focal/amd64/libssl1.1/download

RUN set -e; if [ "${PLATFORM}" = "amd64" ]; then \
        wget http://security.ubuntu.com/ubuntu/pool/main/o/openssl/libssl1.1_1.1.1f-1ubuntu2.23_amd64.deb -O /tmp/openssl.deb \
        && curl -L -o /usr/local/bin/mavlink-server https://github.com/mavlink/mavlink-camera-manager/releases/download/t3.16.0/mavlink-camera-manager-linux-desktop; \
    elif [ "${PLATFORM}" = "arm" ]; then \
        wget http://ports.ubuntu.com/ubuntu-ports/pool/main/o/openssl/libssl1.1_1.1.1f-1ubuntu2.23_armhf.deb -O /tmp/openssl.deb \
        && curl -L -o /usr/local/bin/mavlink-server https://github.com/mavlink/mavlink-camera-manager/releases/download/t3.16.0/mavlink-camera-manager-armv7; \
    elif [ "${PLATFORM}" = "arm64" ]; then \
        wget http://ports.ubuntu.com/ubuntu-ports/pool/main/o/openssl/libssl1.1_1.1.1f-1ubuntu2.23_arm64.deb -O /tmp/openssl.deb \
        && curl -L -o /usr/local/bin/mavlink-server https://github.com/mavlink/mavlink-camera-manager/releases/download/t3.16.0/mavlink-camera-manager-aarch64; \
    fi \
    && dpkg -i /tmp/openssl.deb \
    && chmod +x /usr/local/bin/mavlink-server

ENTRYPOINT ["/usr/local/bin/mavlink-server"]