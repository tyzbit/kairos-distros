# FROM quay.io/kairos/debian:testing-standard-amd64-generic-v3.3.1-k3sv1.32.1-k3s1
FROM quay.io/kairos/kairos-init:latest AS kairos-init
FROM quay.io/kairos/debian:testing-standard-amd64-generic-v3.3.1-k3sv1.32.1-k3s1

COPY rootfs/ /

# To solve temporary dependency hell from htop, downgrade some packages
RUN apt-get update && \
    apt-get install --allow-downgrades -y \
    libncursesw6=6.4-4 \
    libtinfo6=6.4-4 \
    ncurses-bin=6.4-4 && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

RUN apt-get update && \
    apt-get install --allow-downgrades -y \
    bc \
    dbus-broker \
    fancontrol \
    firmware-misc-nonfree \
    firmware-realtek \
    htop \
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
RUN /kairos-init &&\
    rm /kairos-init