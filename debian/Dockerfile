FROM quay.io/kairos/debian:bookworm-standard-amd64-generic-v3.2.0-k3sv1.30.5-k3s1

COPY rootfs/ /

RUN apt-get update && \
    apt-get install -y \
    bc=1.07.* \
    bluetooth=5.66-* \
    bluez-firmware=1.2-* \
    dbus-broker=33-* \
    firmware-iwlwifi=20230210-* \
    # for i915
    fancontrol=1:3* \
    firmware-misc-nonfree=20230210-* \
    firmware-realtek=20230210-* \
    htop=3.2.2* \
    iotop=0.6-* \
    iscsiuio=2.1.8-1 \
    nethogs=0.8.7* \
    open-iscsi=2.1.8-1 \
    smartmontools=7.3-* \
    usbutils=1:014-* \
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
    ln -sf "initrd-${kernel}" /boot/initrd && \
    update-grub
