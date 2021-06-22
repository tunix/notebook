# Installing Ubuntu inside QEMU

First create a disk image:

```
$ qemu-img create -f qcow2 u2104.qcow2 10g
```

Install:

```
$ qemu-system-x86_64 -hda u2104.qcow2 \
    -boot d \
    -cdrom ~/Downloads/ubuntu-21.04-desktop-amd64.iso \
    -smp 2 \
    -m 2G \
    -enable-kvm
```

Create snapshot:

```
$ qemu-img create -f qcow2 -b u2104.qcow2 u2104-snapshot.qcow2
```

Start:

```
$ qemu-system-x86_64 \
    -hda u2104-snapshot.qcow2 \
    -full-screen \
    -smp 2 \
    -m 2G \
    -enable-kvm \
    -soundhw hda \
    -vga virtio \
    -nic user,hostfwd=tcp::2222-:22
```
