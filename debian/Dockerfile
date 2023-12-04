FROM quay.io/kairos/kairos-debian:v2.4.1-k3sv1.27.3-k3s1

COPY rootfs/ /

RUN apt-get update && \
    apt-get install -y \
    bc=1.07.* \
    bluez=5.70-* \
    htop=3.2.2* \
    iotop=0.6-* \
    smartmontools=7.3-* \
    wget=1.21.* \
    && \
    apt-get clean && rm -rf /var/lib/apt/lists/* && \
    echo "TYZBIT_HOME_URL=https://github.com/tyzbit/kairos-distros" >> os-release && \
    echo "TYZBIT_VARIANT=debian" >> os-release

# RTL 8125
WORKDIR /lib/firmware/rtl_nic
RUN wget -r -nd -e robots=no -A '*.fw' --accept-regex '/plain/' \
    https://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git/tree/rtl_nic?h=20231030

# Specific to Intel UHD 770 / 13th gen Intel GPUs
WORKDIR /lib/firmware/i915
RUN wget -r -nd -e robots=no -A '*.bin' --accept-regex '/plain/' \
    https://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git/tree/i915?h=20231030

# Update kernel modules
RUN kernel=$(ls /lib/modules | head -n1) && \
    dracut -v -f "/boot/initrd-${kernel}" "${kernel}" && \
    ln -sf "initrd-${kernel}" /boot/initrd && \
    kernel=$(ls /lib/modules | head -n1) &&\
    depmod -a "${kernel}"