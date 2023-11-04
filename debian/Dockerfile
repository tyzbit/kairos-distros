FROM quay.io/kairos/kairos-debian:v2.4.1-k3sv1.27.3-k3s1

COPY rootfs/ /

RUN apt-get update && \
    apt-get install -y \
    bluez \
    dbus-broker \
    && \
    apt-get clean && rm -rf /var/lib/apt/lists/* && \
    systemctl enable dbus-broker.service