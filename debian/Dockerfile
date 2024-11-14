FROM quay.io/kairos/debian:testing-standard-amd64-generic-v3.2.3-k3sv1.31.2-k3s1

COPY rootfs/ /

# To solve temporary dependency hell, downgrade some packages
RUN apt-get update && \
    apt-get install --allow-downgrades -y \
    libncursesw6=6.4-4 \
    libpython3-stdlib=3.11.2-1+b1 \
    libtinfo6=6.4-4 \
    ncurses-bin=6.4-4 \
    python3=3.11.2-1+b1 \
    python3-greenlet=2.0.2-1 \
    python3-minimal=3.11.2-1+b1 \
    python3-msgpack=1.0.3-2+b1 && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

RUN apt-get update && \
    apt-get install -y \
    bc=1.07.1* \
    # bluetooth=5.66-* \
    # bluez-firmware=1.2-* \
    dbus-broker=33-* \
    # firmware-iwlwifi=20230210-* \
    firmware-realtek=20230210-* \
    fancontrol=1:3.6.0* \
    # for i915
    firmware-misc-nonfree=20230210-5* \
    htop=3.2.2-* \
    iotop=0.6-* \
    intel-media-va-driver=23.1.1+* \
    iscsiuio=2.1.8-* \
    nethogs=0.8.7* \
    smartmontools=7.3-* \
    usbutils=1:014-* \
    wget=1.21.3-* \
    && \
    apt-get clean && rm -rf /var/lib/apt/lists/* && \
    echo "TYZBIT_HOME_URL=https://github.com/tyzbit/kairos-distros" >> /etc/os-release && \
    echo "TYZBIT_VARIANT=debian" >> /etc/os-release && \
    systemctl enable dbus-broker.service

# Update kernel modules
RUN kernel=$(ls /lib/modules | head -n1) && \
    depmod -a "${kernel}" && \
    dracut -f "/boot/initrd-${kernel}" "${kernel}" && \
    ln -sf "initrd-${kernel}" /boot/initrd