FROM debian:bookworm-slim

RUN apt-get update && apt-get install -y --no-install-recommends \
    jq curl ca-certificates \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# Define arguments for target platform
# These arguments are defined automatically by buildx when using `--platform`
ARG TARGETARCH
ARG TARGETVARIANT

ARG PLATFORM
ARG VEHICLETYPE
ENV PLATFORM=${PLATFORM:-$TARGETARCH}
ENV TARGETARCH=$TARGETARCH
ENV VEHICLETYPE=${VEHICLETYPE:-Sub}

RUN echo "Platform: ${PLATFORM} ${TARGETARCH}"
RUN echo "VehicleType: ${VEHICLETYPE}"

RUN if [ "${PLATFORM}" = "x86_64" ]; then \
        echo "SITL_x86_64_linux_gnu" > /arch; \
    elif [ "${PLATFORM}" = "arm" ]; then \
        echo "SITL_arm_linux_gnueabihf" > /arch; \
    elif [ "${PLATFORM}" = "arm64" ]; then \
        echo "SITL_arm_linux_gnueabihf" > /arch; \
    fi

# Download the manifest file
ADD https://firmware.ardupilot.org/manifest.json /tmp/manifest.json

# Extract firmware URL and download firmware
RUN FIRMWARE_URL=$(cat /tmp/manifest.json | jq -r ".firmware[] | select(.latest == 1) | select(.platform | contains(\"$(cat /arch)\")) | select(.vehicletype | contains(\"${VEHICLETYPE}\")) | .url") \
    && curl -L -o /usr/local/bin/firmware $FIRMWARE_URL \
    && chmod +x /usr/local/bin/firmware

ENTRYPOINT ["/usr/local/bin/firmware"]