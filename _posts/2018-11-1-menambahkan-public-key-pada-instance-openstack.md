---
layout: post
title: "Menambahkan public key pada instances OpenStack"
description: "Menambahkan public key pada instances OpenStack"
comments: false
keywords: "OpenStack, instances, public key"
---

Terkadang saat membuat instances pada OpenStack user bisa lupa menambahkan public key ataupun terkadang jika kondisi scheduller sedang tidak sehat jadi public key tidak terinject pada instances.

Jadi untuk memperbaikinya kita harus melakukan langkah-langkah seperti menjalankan live cd pada instances. Tapi bagaimana caranya jika di OpenStack.

Langkah-langkah memperbakinya:
1. Kita harus memiliki image yang 
berisi iso livecd, jika tidak ada unggah dahulu iso sebagai livecd.
2. Rescue instance dengan menggunakan livecd, agar boot ke dalam livecd.
```
openstack server rescue --password <password> --image <image-id> <instance-id>
```
3. Akses instance melalui console di horizon.
4. Buka terminal pada console instance di horizon dan lakukan langkah-langkah berikut.
```
fdisk -l
mount /dev/vdb1 /mnt/
chroot /mnt/
sudo -i
useradd user
chmod 600 /etc/shadow
vi /etc/shadow 
# Ubah user ! menjadi *
passwd user
# Allow sementara ssh dengan password
exit
umount /mnt
```
5. Unrescue instance agar booting normal ke dalam harddisk lagi.
```
openstack server unrescue <instance-id>
```
6. SSH kedalam instance
7. Tambahkan public key ke dalam user.
8. Selesai, ujicoba akses ssh dengan key.
9. Jika bisa, matikan akses allow ssh dengan password.

Berikut tadi merupakan langkah-langkah jika lupa menambahkan/ada masalah public key hilang.

Salam,
Moko yang lagi nulis lagi.