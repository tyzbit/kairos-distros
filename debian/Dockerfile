# v3.3.2-k3sv1.32.2-k3s1
FROM quay.io/kairos/kairos-init:latest AS kairos-init
FROM debian:12.10
ARG VERSION
ARG K8SVERSION

COPY rootfs/ /

RUN apt-get update && \
    apt-get install --allow-downgrades -y \
    bc \
    fancontrol \
    firmware-misc-nonfree \
    firmware-realtek \
    iotop-c \
    intel-media-va-driver \
    iscsiuio \
    nethogs \
    open-iscsi \
    smartmontools \
    usbutils \
    wget \
    && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

COPY --from=kairos-init /kairos-init /kairos-init
RUN /kairos-init \
    -l debug \
    -v standard \
    -m generic \
    -t false \
    -k k3s \
    --version "${VERSION}" \
    --k8sversion "${K8SVERSION}" \
    -r "ghcr.io/tyzbit/kairos-distros" \
    && \
    rm /kairos-init