FROM quay.io/kairos/debian:testing-standard-amd64-generic-v3.3.0-k3sv1.32.0-k3s1

COPY rootfs/ /

# To solve temporary dependency hell from htop, downgrade some packages
RUN apt-get update && \
    apt-get install --allow-downgrades -y \
    libncursesw6=6.4-4 \
    libtinfo6=6.4-4 \
    ncurses-bin=6.4-4 && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

RUN apt-get update && \
    apt-get install -y \
    bc=1.07.1* \
    dbus-broker=33-* \
    fancontrol=1:3.6.0* \
    firmware-misc-nonfree=20230210-* \
    firmware-realtek=20230210-* \
    htop=3.2.2-* \
    iotop-c=1.23-* \
    intel-media-va-driver=23.1.1+* \
    iscsiuio=2.1.8-* \
    nethogs=0.8.7-* \
    open-iscsi=2.1.10-* \
    smartmontools=7.3-* \
    usbutils=1:014-* \
    wget=1.21.3-* \
    && \
    apt-get clean && rm -rf /var/lib/apt/lists/* && \
    systemctl enable dbus-broker.service && \
    echo "TYZBIT_HOME_URL=https://github.com/tyzbit/kairos-distros" >> /etc/os-release && \
    echo "TYZBIT_VARIANT=debian" >> /etc/os-release

# Update kernel modules
RUN kernel=$(ls /lib/modules | head -n1) && \
    depmod -a "${kernel}" && \
    dracut -f "/boot/initrd-${kernel}" "${kernel}" && \
    ln -sf "initrd-${kernel}" /boot/initrd