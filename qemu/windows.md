# Installing Windows inside QEMU

First create a disk image:

```
$ qemu-img create -f qcow2 win10.qcow2 40g
```

Install:

```
$ qemu-system-x86_64 -hda win10.qcow2 \
    -boot d \
    -cdrom ~/Downloads/Win10_20H2_v2_English_x64.iso \
    -smp 2 \
    -m 4G \
    -enable-kvm
```

Create snapshot:

```
$ qemu-img create -f qcow2 -b win10.qcow2 win10-snapshot.qcow2
```

Start:

```
$ qemu-system-x86_64 \
    -hda win10-snapshot.qcow2 \
    -full-screen \
    -smp 2 \
    -m 4G \
    -enable-kvm \
    -device intel-hda -device hda-duplex \
    -vga virtio \
    -usb -device usb-tablet
```
