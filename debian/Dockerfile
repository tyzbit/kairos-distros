FROM quay.io/kairos/kairos-debian:v2.4.1-k3sv1.27.3-k3s1

COPY rootfs/ /

RUN apt-get update && \
    apt-get install -y \
    bc=1.07.1-3+b1 \
    bluez=5.70-1 \
    smartmontools=7.3-1+b1 \
    wget=1.21.3-1+b2 \
    && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Specific to Intel UHD 770 / 13th gen Intel GPUs
WORKDIR /lib/firmware/i915
RUN wget -r -nd -e robots=no -A '*.bin' --accept-regex '/plain/' \
    https://git.kernel.org/pub/scm/linux/kernel/git/firmware/linux-firmware.git/tree/?h=20231030
RUN kernel=$(ls /lib/modules | head -n1) && \
    dracut -v -f "/boot/initrd-${kernel}" "${kernel}" && \
    ln -sf "initrd-${kernel}" /boot/initrd && \
    kernel=$(ls /lib/modules | head -n1) &&\
    depmod -a "${kernel}"
