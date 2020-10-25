# Expanding Disks

A disk may have partition table of one the following options:

* MBR
* GPT

MBR is the older one and has some limitations such as the max number of primary partitions (4) per disk. It also limits
the maximum allowed disk size to 2 TB.

For higher needs, one must choose GPT for the partition table.

If a disk is expanded in place (when no additional disks are added but the existing one has more capacity), it cannot be
automatically discovered by Linux kernel unless it's notified with some tools. Most of the time, the server is rebooted
in such cases. (**TODO:** check CLI tools for a way without reboot)

After a reboot, additional capacity can be seen inside fdisk/parted output:

```
$ sudo fdisk /dev/sdb

fdisk (util-linux 2.34)'e hoşgeldiniz.
Değişiklikler siz onları yazmaya karar verene kadar sadece bellekte kalacak.
Yaz komutunu kullanmadan önce dikkat ediniz.


Komut (yardım için m): p
Disk /dev/sdb: 250 GiB, 268435456000 bayt, 524288000 sektör
Disk model: Virtual disk
Birimler: sektör'i 1 * 512 = 512 baytın
Sektör boyutu (montıksal/fiziksel): 512 bayt / 512 bayt
G/Ç boyutu (en düşük/en uygun): 512 bayt / 512 bayt
Disketikeri tipi: dos
Disk belirleyicisi: 0x0d0916f8

Aygıt      Açılış Başlangıç       Son    Sektör Boyut ld Türü
/dev/sdb1              2048 104857599 104855552   50G 83 Linux

Komut (yardım için m): q
```

Notice above that the capacity is 250 GB while the partition itself is 50 GB. In our case, we have LVM defined for this
disk. To resize, we must go through the following steps:

* Delete the partition & recreate it (it'll automatically use the latest sector)
* Expand PV: `sudo pvresize /dev/sdb1`
* Finally expand LV: `sudo lvextend -r -l +100%FREE /dev/my-vg/my-lv`

You should now be able to see expanded volume inside the following command's output:

* `sudo pvdisplay`
* `sudo lvdisplay`
* `df -h`
