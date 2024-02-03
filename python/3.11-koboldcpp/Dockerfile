# Building from python 3.11-slim image
FROM --platform=$TARGETOS/$TARGETARCH python:3.11-slim

# update image and install necessary packages
RUN apt-get update && apt-get upgrade -y \
    && apt-get -y install \
    ocl-icd-opencl-dev opencl-headers clinfo \
    libclblast-dev libopenblas-dev git gcc g++ ca-certificates \
    dnsutils curl iproute2 ffmpeg procps tini \
    && apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* \
    && useradd -m -d /home/container container

USER container
ENV USER=container HOME=/home/container
WORKDIR /home/container

STOPSIGNAL SIGINT

COPY --chown=container:container ./../entrypoint.sh /entrypoint.sh
RUN chmod +x /entrypoint.sh
ENTRYPOINT ["/usr/bin/tini", "-g", "--"]
CMD ["/entrypoint.sh"]
