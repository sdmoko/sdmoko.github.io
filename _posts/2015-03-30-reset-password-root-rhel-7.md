---
layout: post
title: Reset Password Root RHEL 7
description: "reset password root rhel 7"
comments: False
keywords: "reset, password, root, rhel7, sysadmin" 
---

Adakalanya kita diserahkan sebuah server tanpa dokumentasi yang lengkap, bahkan kita tidak diberikan akses root padahal kita membutuhkannya. Jika menemui kasus seperti ini biasanya yang mudah kita bertanya ke admin sistem yang terdahulu, namun jika tidak ada jawaban barulah kita coba reset root passwordnya. :)

Tahapan reset password RHEL 7

1. Boot sistem dan tunggu sampai menu GRUB2 muncul.
2. Dalam menu GRUB2, pilih salah satu menu lalu tekan **e** untuk menyuntingnya.
3. Cari baris yang dimulai dengan kata **linux**. Lalu sunting baris tersebut, hapus kata **rhgb** dan tambahkan di akhir baris perintah:
```
init=/bin/sh
```
4. Tekan **F10** atau **ctrl + x** untuk masuk ke sistem yang sudah kita sunting opsi boot tersebut. Jika sudah masuk ke sistem maka akan muncul prompt:
sh-4.2#
5. Load policy SELinux yang sudah terpasang
sh-4.2# /usr/sbin/load_policy -i
6. Remount root partition dengan mode read write
sh-4.2# mount -o remount,rw /
7. Reset root password
sh-4.2# passwd root
8. Remount root partition dengan mode read only
sh-4.2# mount -o remount,r0 /
9. Inisialisasi sistem dan login dengan password baru.
sh-4.2# exec /sbin/init
10. Reboot system.

Referensi: 

[https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-basic-system-recovery.html#sect-rescue-mode-reset-root-password](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Installation_Guide/chap-basic-system-recovery.html#sect-rescue-mode-reset-root-password)