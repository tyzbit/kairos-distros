FROM quay.io/kairos/kairos-init:v0.7.0 AS kairos-init
FROM debian:12.12
# kairos-io/kairos
ENV KAIROS_VERSION=3.7.2
ARG DEBUG_ROOT_PASSWORD
# k3s-io/k3s
ENV K8S_VERSION=v1.35.0-k3s3

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
    parted \
    smartmontools \
    usbutils \
    wget \
    && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Uncomment for testing
RUN echo "root:$DEBUG_ROOT_PASSWORD" | chpasswd

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