FROM quay.io/kairos/ubuntu:24.04-standard-amd64-generic-v3.2.0-rc1-k3sv1.31.1-k3s1

# COPY rootfs/ /

RUN apt-get update && \
    apt-get install -y \
    bc=1.07.* \
    bluetooth=5.72-* \
    bluez-firmware=1.2-* \
    dbus-broker=35-* \
    # firmware-iwlwifi=20230210-* \
    # for i915
    fancontrol=1:3* \
    # firmware-misc-nonfree=20230210-* \
    # firmware-realtek=20230210-* \
    htop=3.3* \
    iotop=0.6-* \
    nethogs=0.8.7* \
    iscsiuio=2.1.9-* \
    nethogs=0.8.7* \
    open-iscsi=2.1.9-* \
    smartmontools=7.4-* \
    usbutils=1:017-* \
    wget=1.21.* \
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