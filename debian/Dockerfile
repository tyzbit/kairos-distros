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

# Force enp3s0
RUN grub2-editenv - \
    set "$(grub2-editenv - list | grep kernelopts) ip=eth0:dhcp"

# https://kairos.io/docs/advanced/customizing/#customizing-the-kernel
# Create the kernel symlink
RUN kernel=$(ls /boot/vmlinuz-* | head -n1) && \
    ln -sf "${kernel#/boot/}" /boot/vmlinuz

# Regenerate the initrd, in openSUSE we could just use "mkinitrd"
RUN kernel=$(ls /lib/modules | head -n1) && \
    dracut -v -f "/boot/initrd-${kernel}" "${kernel}" && \
    ln -sf "initrd-${kernel}" /boot/initrd

# Update the module dependencies
RUN kernel=$(ls /lib/modules | head -n1) && \
    depmod -a "${kernel}"