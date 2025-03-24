# v3.3.1-k3sv1.32.2-k3s1
FROM quay.io/kairos/kairos-init:latest AS kairos-init
FROM debian:12.10

COPY rootfs/ /

RUN apt-get update && \
    apt-get install --allow-downgrades -y \
    bc \
    fancontrol \
    firmware-misc-nonfree \
    firmware-realtek \
    intel-media-va-driver \
    open-iscsi \
    smartmontools \
    usbutils \
    wget \
    && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

COPY --from=kairos-init /kairos-init /kairos-init
RUN /kairos-init \
    --version "${version}" && \
    rm /kairos-init