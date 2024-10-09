FROM quay.io/kairos/debian:bookworm-standard-amd64-generic-v3.2.1-k3sv1.30.5-k3s1

COPY rootfs/ /

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    bc \
    bluetooth \
    bluez-firmware \
    dbus-broker \
    # firmware-iwlwifi=20230210-* \
    fancontrol \
    # for i915
    firmware-misc-nonfree \
    firmware-realtek \
    htop  \
    iotop \
    intel-media-va-driver \
    iscsiuio \
    nethogs \
    open-iscsi \
    smartmontools \
    usbutils \
    wget \
    && \
    apt-get clean && rm -rf /var/lib/apt/lists/* && \
    echo "TYZBIT_HOME_URL=https://github.com/tyzbit/kairos-distros" >> /etc/os-release && \
    echo "TYZBIT_VARIANT=debian" >> /etc/os-release && \
    systemctl enable dbus-broker.service && \
    # echo "done"
    kernel=$(ls /lib/modules | head -n1) && \
    depmod -a "${kernel}" && \
    dracut -f "/boot/initrd-${kernel}" "${kernel}" && \
    ln -sf "initrd-${kernel}" /boot/initrd
