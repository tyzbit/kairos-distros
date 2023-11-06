FROM quay.io/kairos/kairos-debian:v2.4.1-k3sv1.27.3-k3s1

COPY rootfs/ /

RUN apt-get update && \
    apt-get install -y \
    bc=1.07.1-3+b1 \
    bluez=5.70-1 \
    intel-media-va-driver=23.3.5+dfsg1-1 \
    smartmontools=7.3-1+b1 \
    && \
    apt-get clean && rm -rf /var/lib/apt/lists/*