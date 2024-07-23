FROM fedora:41@sha256:815d788d6610a41d9ed4e1aeb1fed52fc4937a55253be144786f932c01cd45df

RUN dnf install 'dnf-command(download)' cpio xz -y
# https://dl.fedoraproject.org/pub/fedora/linux/releases/37/Everything/x86_64/os/Packages/k/kernel-6.0.7-301.fc37.x86_64.rpm
# https://dl.fedoraproject.org/pub/fedora/linux/releases/37/Everything/x86_64/os/Packages/k/kernel-modules-6.0.7-301.fc37.x86_64.rpm
RUN dnf download kernel-core-6.0.7-301.fc37 kernel-modules-6.0.7-301.fc37 -y

RUN rpm2cpio kernel-core-*.rpm | cpio -t && \
    rpm2cpio kernel-core-*.rpm | cpio -idmv ./lib/modules/6.0.7-301.fc37.x86_64/vmlinuz

RUN rpm2cpio kernel-modules-*.rpm | cpio -t && \
    rpm2cpio kernel-modules-*.rpm | cpio -idmv ./lib/modules/6.0.7-301.fc37.x86_64/kernel/drivers/tty/ttynull.ko.xz

RUN unxz /lib/modules/6.0.7-301.fc37.x86_64/kernel/drivers/tty/ttynull.ko.xz

FROM scratch

COPY --from=0 /lib/modules/6.0.7-301.fc37.x86_64/vmlinuz /lib/modules/6.0.7-301.fc37.x86_64/vmlinuz
COPY --from=0 /lib/modules/6.0.7-301.fc37.x86_64/kernel/drivers/tty/ttynull.ko /lib/modules/6.0.7-301.fc37.x86_64/kernel/drivers/tty/ttynull.ko
