---
layout: post
title: Install DNSCrypt di Debian Jessie
description: "Install DNSCrypt di Debian Jessie"
comments: false
keywords: "dnscrypt, debian, jessie"
---
Berhubung saya kebanyakan menggunakan akses internet dari Telkom dan terdapat pembatasan akses ke beberapa situs yang saya kunjungi, saya jadi mencari cara untuk ngakalinnya :D. Dapatlah sebuah cara yaitu menggunakan DNSCrypt.

Pasang library paket yang dibutuhkan untuk memasang dan mengkompilasi DNSCrypt.
```
sudo apt update && sudo apt install build-essential libtool automake libsodium13 pkg-config
```
Unduh versi terbaru DNSCrypt, saat ini versi 1.5.0
```
wget http://download.dnscrypt.org/dnscrypt-proxy/dnscrypt-proxy-1.5.0.tar.gz
```
Ekstrak berkas yang telah diunduh
```
tar zxvf dnscrypt-proxy-1.5.0.tar.gz
```
Pindah ke direktori hasil ekstrak
```
cd dnscrypt-proxy-1.5.0
```
Kompilasi dan pasang DNSCrypt
```
./configure
make
sudo make install
```
Pastikan proses berjalan dengan normal.
Jalankan DNSCrypt dengan perintah:
```
dnscrypt-proxy -R opendns --daemonize
```
Ubah berkas /etc/resolv.conf menjadi
```
nameserver 127.0.0.1
```
Selamat mencoba. Cheers.
Referensi:

[http://jaranguda.com/install-dnscrypt-1-4-di-debian-7/](http://jaranguda.com/install-dnscrypt-1-4-di-debian-7/)[http://mydarkerego.blogspot.com/2015/04/dirty-hacking-dnscrypt-so-it-works-on.html](http://mydarkerego.blogspot.com/2015/04/dirty-hacking-dnscrypt-so-it-works-on.html)

UPDATE
Cukup pasang menggunakan paket manager debian
```
sudo apt install dnscrypt-proxy
```