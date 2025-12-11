FROM quay.io/kairos/kairos-init:v0.6.5 AS kairos-init
FROM debian:12.12
# kairos-io/kairos
ENV KAIROS_VERSION=3.5.10
# k3s-io/k3s
ENV K8S_VERSION=v1.33.6+k3s1

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

# Uncomment for testing
# RUN echo 'root:root' | chpasswd

COPY --from=kairos-init /kairos-init /kairos-init
RUN /kairos-init \
    -l debug \
    -v standard \
    -m generic \
    -t false \
    -p k3s \
    --version "${KAIROS_VERSION}" \
    --provider-k3s-version "${K8S_VERSION}" \
    && \
    rm /kairos-init