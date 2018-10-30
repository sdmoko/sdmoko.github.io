---
layout: post
title: Wget Aplikasi Pengunduh Berkas
description: "Wget aplikasi unduh"
comments: true
keywords: "bash, linux, mac, download"
---

**Wget** merupakan salah satu program untuk mengunduh berkas terbaik yang pernah ada. Wget bisa menghandle banyak situasi seperti mengunduh file besar, rekursif, unduh berbarengan, dll.

Nah, sekarang saya mau berbagi tips unduh menggunakan wget. Oke kita mulai yah. :)


**1. Unduh satu berkas dengan wget**

Contoh berikut ini merupakan cara unduh satu berkas dengan wget.
```
$ wget http://kambing.ui.ac.id/iso/ubuntu/releases/14.04/ubuntu-14.04-server-amd64.iso
```

Ketika proses ini berjalan maka akan menampilkan beberapa informasi, seperti :
- persentase unduh berkas (contoh 1% seperti di bawah)
- jumlah bytes yang telah diunduh sejauh ini (contoh 9,139,744 bytes di bawah)
- kecepatan unduh sekarang (contoh 122KB/s di bawah)
- estimasi sisa waktu unduh (contoh 67m 4s di bawah)

```
moko@azkaban:~$ wget http://kambing.ui.ac.id/iso/ubuntu/releases/14.04/ubuntu-14.04-server-amd64.iso
--2015-02-10 21:57:37-- http://kambing.ui.ac.id/iso/ubuntu/releases/14.04/ubuntu-14.04-server-amd64.iso
Resolving kambing.ui.ac.id (kambing.ui.ac.id)... 152.118.24.30, 2403:da00:1:3::1e
Connecting to kambing.ui.ac.id (kambing.ui.ac.id)|152.118.24.30|:80... connected.
HTTP request sent, awaiting response... 200 OK
Length: 591396864 (564M) [application/octet-stream]
Saving to: 'ubuntu-14.04-server-amd64.iso'

1% [ ] 9,139,744 122KB/s eta 67m 4s
```


**2. Unduh dan Simpan Berkas dengan Nama Lain menggunakan wget -O**

Secara default wget akan memilih nama berkas dari kata terakhir setelah slash (/) yang dimana terkadang tidak sesuai.

**Salah** : contoh wget akan mengunduh dan menyimpan berkas dengan nama download_script.php?src_id=7701
```
$ wget http://www.vim.org/scripts/download_script.php?src_id=7701
```

Meskipun berkas yang diunduh merupakan berkas zip, akan disimpan sebagai berikut.
```
$ ls
download_script.php?src_id=7701
```
**Benar** : berikut contoh yang benar menggunakan opsi -O
```
$ wget -O taglist.zip http://www.vim.org/scripts/download_script.php?src_id=7701
```


**3. Unduh dengan Membatasi Kecepatan Unduh Berkas**

Saat menjalankan wget, secara default wget akan mengunduh dengan menggunakan seluruh bandwith. Hal ini tidak boleh dilakukan jika dijalankan pada mesin server produksi. Oleh karena itu butuh dilakukan pembatasan pada kecepatan unduh.
```
$ wget --limit-rate=200k http://www.openss7.org/repos/tarballs/strx25-0.9.2.1.tar.bz2
```


**4. Meneruskan Proses Unduh yang Gagal**

Pada saat mengunduh berkas yang besar mungkin saja terjadi kegagalan, tapi itu bisa diteruskan dengan wget.
```
$ wget -c http://www.openss7.org/repos/tarballs/strx25-0.9.2.1.tar.bz2
```


**5. Menjalankan Proses Unduh di Background Menggunakan wget -b**

Untuk unduh yang besar, jalankan proses unduh di background menggunakan wget opsi -b seperti di bawah.
```
$ wget -b http://www.openss7.org/repos/tarballs/strx25-0.9.2.1.tar.bz2
Continuing in background, pid 1984.
Output will be written to `wget-log'.
```
Itu akan menjalankan proses unduh dan kita tetap bisa mengecek progres unduh dengan menggunakan tail -f seperti di bawah.
```
$ tail -f wget-log
Saving to: `strx25-0.9.2.1.tar.bz2.4'

     0K .......... .......... .......... .......... ..........  1% 65.5K 57s
    50K .......... .......... .......... .......... ..........  2% 85.9K 49s
   100K .......... .......... .......... .......... ..........  3% 83.3K 47s
   150K .......... .......... .......... .......... ..........  5% 86.6K 45s
   200K .......... .......... .......... .......... ..........  6% 33.9K 56s
   250K .......... .......... .......... .......... ..........  7%  182M 46s
   300K .......... .......... .......... .......... ..........  9% 57.9K 47s
```


**6. Menggunakan wget sebagai Mask User Agent dan Seperti Browser Menggunakan wget --user-agent**

Beberapa website bisa menolak kita untuk mengunduh berkas dengan mengidentifikasi user agent yang bukan browser. Jadi kita bisa membuat seolah-olah wget berjalan sebagai user agent dengan menggunakan opsi -user-agent.
```
$ wget --user-agent="Mozilla/5.0 (X11; U; Linux i686; en-US; rv:1.9.0.3) Gecko/2008092416 Firefox/3.0.3" URL-TO-DOWNLOAD
```


**7. Uji URL Unduh dengan Menggunakan Using wget --spider**

Ketika kita ingin menjalankan proses unduh berjadwal, kita harus memeriksa apakah proses unduh akan berjalan dengan baik atau tidak pada waktu yang dijadwalkan. Untuk mengujinya jalankan opsi `--spider` sebelum URL unduh berkas.
```
$ wget --spider DOWNLOAD-URL
```
Jika URL yang diberikan benar maka akan muncul seperti di bawah.
```
$ wget --spider download-url
Spider mode enabled. Check if remote file exists.
HTTP request sent, awaiting response... 200 OK
Length: unspecified [text/html]
Remote file exists and could contain further links,
but recursion is disabled -- not retrieving.
```
Ini akan menjamin proses unduh akan berjalan sukses pada jadwalnya. Tetapi, jika URL unduh salah maka akan menampilkan pesan.
```
$ wget --spider download-url
Spider mode enabled. Check if remote file exists.
HTTP request sent, awaiting response... 404 Not Found
Remote file does not exist -- broken link!!!
```
Kamu dapat menjalankan opsi spier dengan beberapa skenario:

- Uji sebelum proses unduh.
- Mengamati apakah website tersedia atau tidak pada beberapa rentang waktu.
- Memeriksa dari daftar halaman yang disimpan, dan mencari tahu apakah masih bisa diakses atau tidak.


**8. Menambahkan Jumlah Pengulangan Kesempatan Unduh dengan wget --tries**

Jika koneksi internet bermasalah (baca: putus-putus), dan jika berkas yang di unduh besar dan ada kemungkinan gagal dalam proses unduh. Secara default wget mencoba pengulangan sampai 20 kali untuk membuat proses unduh berjalan sukses.

Jika dibutuhkan, kita dapat menambahkan jumlah pengulangan menggunakan opsi --tries.
```
$ wget --tries=75 DOWNLOAD-URL
```

**9. Download Multiple Files / URLs Using Wget -i**

Pertama, simpan semua URL berkas di dalam text file.
```
$ cat > download-file-list.txt
URL1
URL2
URL3
URL4
```
Selanjutnya,  berikan download-file-list.txt sebagai argumen wget menggunakan opsi -i.
```
$ wget -i download-file-list.txt
```

**10. Unduh Full Website Menggunakan wget --mirror**

Berikut ini perintah untuk mengunduh full website dan membuat bisa dilihat dari lokal.
```
$ wget --mirror -p --convert-links -P ./LOCAL-DIR WEBSITE-URL
```

- `--mirror` : mengaktifkan opsi untuk mirroring.
- `-p` : unduh semua berkas yang dibutuhkan untuk menampilkan halaman HTML.
- `–convert-links` : setelah diunduh, ubah links di berkas untuk dilihat secara lokal.
- `-P ./LOCAL-DIR` : menyimpan semua berkas di dalam direktori tertentu.


**11. Menolak Jenis Berkas ketika Unduh Menggunakan wget --reject**

Kita menemukan website yang penting, namun kita tidak ingin mengunduh gambar bisa dilakukan seperti di bawah.
```
$ wget --reject=gif WEBSITE-TO-BE-DOWNLOADED
```


**12. Simpan Pesan Log ke berkas Log Spesifik Menggunakan wget -o**

Ketika kita ingin log disimpan ke berkas log daripada di terminal.
```
$ wget -o download.log DOWNLOAD-URL
```


**13. Keluar dari Proses Unduh jika Melebihi Ukuran Tertentu Menggunakan wget -Q**

Ketika kita ingin menghentikan proses unduh ketika melebihi 5MB, kita dapat menggunakan opsi berikut.
```
$ wget -Q5m -i FILE-WHICH-HAS-URLS
```
**Note**: Kuota ini tidak akan berefek ketika kita melakukan unduh satu berkas. Itu terlepas dari ukuran kuota semuanya akan bisa diunduh ketika kita menentukan satu berkas. Kuota ini hanya berlaku untuk download rekursif.


**14. Unduh hanya Jenis Berkas Tertentu Menggunakan wget -r -A**

Kita dapat menggunakannya dengan beberapa skenario:

Unduh semua gambar dari website
Unduh semua video dari website
Unduh semua PDF dari website
```
$ wget -r -A.pdf http://url-to-webpage-with-pdfs/
```


**15. Unduh FTP dengan wget**

Kita dapat menggunakan wget untuk menjalankan FTP.

Anonymous FTP menggunakan Wget.
```
$ wget ftp-url
```
FTP menggunakan wget dengan username dan password authentication.
```
$ wget --ftp-user=USERNAME --ftp-password=PASSWORD DOWNLOAD-URL
```


**16. Unduh Rekursif dengan wget**

Kita bisa mengunduh berkas dalam satu folder dengan menggunakan wget.
```
$ wget -r -l 5 DOWNLOAD-URL
```
**Note**: Maksimal kedalaman level direktori adalah 5.

 
Sumber : [http://www.thegeekstuff.com/2009/09/the-ultimate-wget-download-guide-with-15-awesome-examples/](http://www.thegeekstuff.com/2009/09/the-ultimate-wget-download-guide-with-15-awesome-examples/)