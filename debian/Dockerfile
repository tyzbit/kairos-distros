FROM quay.io/kairos/kairos-debian:v2.4.1-k3sv1.27.3-k3s1

COPY rootfs/ /

RUN apt-get update && \
    apt-get install -y \
    firmware-realtek \
    && \
   # update-initramfs -u && \
    apt-get clean && rm -rf /var/lib/apt/lists/* 
    # && \
    # https://kairos.io/docs/advanced/customizing/
    # kernel=$(ls /lib/modules | head -n1) && \
    # dracut -v -f "/boot/initrd-${kernel}" "${kernel}" && \
    # ln -sf "initrd-${kernel}" /boot/initrd && \
    # kernel=$(ls /lib/modules | head -n1) && \
    # depmod -a "${kernel}"