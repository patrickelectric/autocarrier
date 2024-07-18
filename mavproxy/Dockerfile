FROM python:3.11-slim-bookworm

RUN apt-get update && apt-get install -y --no-install-recommends \
    ca-certificates python3-dev python3-opencv python3-wxgtk4.0 python3-pip python3-matplotlib python3-lxml python3-pygame \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

RUN pip3 install PyYAML mavproxy --break-system-packages --extra-index-url=https://www.piwheels.org/simple
ENTRYPOINT ["/usr/local/bin/mavproxy.py"]
