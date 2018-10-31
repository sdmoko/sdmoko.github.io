---
layout: post
title: "Memasang Container OpenVZ di Proxmox"
description: "Memasang Container openVZ"
comments: false
keywords: "container, openVZ, proxmox"
---

Artikel kali ini merupakan request dari om [Saputro](https://www.facebook.com/saputroaryulianto) yang minta diajari cara masang container OpenVZ di Proxmox. Oke mungkin nanti akan dijelasin lebih jauh tentang container OpenVZ dan Proxmox tapi sekarang saya mau menjelaskan cara memasang container dulu yah. :)

1. Pastikan kita sudah punya template container OpenVZ jika belum punya bisa dicari dan diunduh dari [sini](http://openvz.org/Download/template/precreated)
2. Jika sudah punya atau unduh template OpenVZ simpan berkasnya di direktori `/var/lib/vz/template/cache` di dalam Proxmox.
3. Oke sekarang masuk ke webpanel Proxmox kita. Masukan https://ipproxmox:8006 port 8006 merupakan port standar webpanel Proxmox.
![https://sdmokonote.files.wordpress.com/2015/02/1.png](https://sdmokonote.files.wordpress.com/2015/02/1.png)
4. Setelah masuk ke webpanel Proxmox, klik "Create CT" untuk membuat container. Isikan hostname dan password sesuai yang dkehendaki. Jika sudah klik Next.
![https://sdmokonote.files.wordpress.com/2015/02/3.png](https://sdmokonote.files.wordpress.com/2015/02/3.png)
5. Selanjutnya pilih template yang ingin digunakan. Klik Next.
![https://sdmokonote.files.wordpress.com/2015/02/4.png](https://sdmokonote.files.wordpress.com/2015/02/4.png)
6. Konfigurasi jumlah memory, swap, disk size dan CPU sesuai kebutuhan. Klik Next.
![https://sdmokonote.files.wordpress.com/2015/02/5.png](https://sdmokonote.files.wordpress.com/2015/02/5.png)
7. Selanjutnya konfigurasi Network sesuai kebutuhan. Klik Next.
![https://sdmokonote.files.wordpress.com/2015/02/6.png](https://sdmokonote.files.wordpress.com/2015/02/6.png)
8. Konfigurasikan DNS. Klik Next.
![https://sdmokonote.files.wordpress.com/2015/02/7.png](https://sdmokonote.files.wordpress.com/2015/02/7.png)
9. Pastikan kembali semua konfigurasi, jika sudah benar klik Finish.
![https://sdmokonote.files.wordpress.com/2015/02/8.png](https://sdmokonote.files.wordpress.com/2015/02/8.png)
10. Jika muncul output seperti berikut maka proses sudah selesai dan container siap untuk digunakan.
![https://sdmokonote.files.wordpress.com/2015/02/9.png](https://sdmokonote.files.wordpress.com/2015/02/9.png)

Demikian, jika belum mengerti silahkan tinggalkan komentar. Cheers.