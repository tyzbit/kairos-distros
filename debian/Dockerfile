FROM quay.io/kairos/kairos-init:v0.4.2 AS kairos-init
FROM debian:12.10
ENV KAIROS_VERSION=v3.3.2
ENV K8S_VERSION=v1.31.6+k3s1

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
    --version "${KAIROS_VERSION}" \
    --k8sversion "${K8S_VERSION}+1" \
    -r "ghcr.io/tyzbit/kairos-distros" \
    && \
    rm /kairos-init