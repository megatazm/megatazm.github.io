---
layout: post
title: Akses Raspberry Pi Secara Remote Melalui Laptop atau Desktop
date: 2018-10-14 13:32:20 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: iot-background-imej.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Camaner, How to]
---
Kebolehan untuk mengakses komputer secara remote melalui internet sangat penting dalam menjalankan pengurusan sistem komputer dengan berkesan dan efisien. Bayangkan jika awak ditugaskan untuk mengawal selia 100 buah sistem komputer yang berada di merata-rata tempat. Pengaksesan secara remote bukan sahaja memudahkan tugasan awak, ia juga menjimatkan kos operasi syarikat. Bila kos operasi rendah, syarikat memperoleh keuntungan lebih, bonus pun dapat lebih. Untuk membolehkan raspberry pi menerima akses secara remote melalui wifi router dari komputer lain, aplikasi SSH perlu diaktifkan terlebih dahulu. Selepas itu awak perlu menyambungkan wifi raspberry pi ke wifi router tanpa memerlukan keyboard, mouse dan monitor, gimana dong?. Berikut adalah langkah-langkahnya:-

* Perkakas yang diperlukan ialah, Wifi router, kabel ethernet, raspberry pi beserta wifi adapter, 5V USB power supply/power bank, SD card mini 16GB + Raspbian OS ([Camaner nak buat]({% post_url 2018-11-13-Memasang-raspbian-os-ke-sd-card %})) dan komputer/laptop.
* Download dan install perisian [Angry IP Scanner](https://angryip.org/download/) ke dalam komputer. Awak akan gunakan perisian ini untuk mengimbas dan mendapatkan IP address raspberry pi. Setiap komputer mesti memerlukan IP address iaitu suatu nombor ID yang unik untuk berkomunikasi. Bayangkan awak memanggil Rahman! di sebuah shopping komplex, mungkin ada lebih dari seorang akan menyahut. Berita baik, jika awak menginap di penjara, awak akan diberikan nombor id yang unik!
* Jika awak menggunakan MS Windows. Saya cadangkan awak download perisian [MobaXterm](http://download.mobatek.net/1092018073012523/MobaXterm_Installer_v10.9.zip). Perisian ini memudahkan awak mengakses raspberry pi secara remote dari komputer windows.
* Masukkan SD card yang telah dimuat dengan Raspbian OS melalui SD Card reader ke komputer. 
* Klik masuk ke dalam SD card tersebut, seterusnya klik masuk ke dalam direktori /boot. Kemudian ciptakan satu text file kosong yang dinamakan ssh.
* Ini membolehkan aplikasi ssh diaktifkan secara automatik apabila Raspbian OS beroperasi. Aplikasi ssh membolehkan komputer dari luar mengakses masuk ke dalam raspberry pi.
* Cucuk masuk power supply 5V pada raspberry pi untuk menghidupkan (boot up) Raspbian OS. Tunggu sehingga led hijau tidak berkelip-kelip lagi.
* Cucuk kabel ethernet pada raspberry pi ethernet port, kemudian sambungkan hujung kabel ethernet itu pada port ethernet wifi router yang telah dihidupkan (Jika wifi router awak cuma ada satu sahaja port, belilah mini switch port).
* Sambungkan wifi connection komputer/laptop awak pada wifi router tersebut. Dengan ini komputer/laptop awak berada di dalam lingkungan jaringan komunikasi yang sama dengan raspberry pi. Run aplikasi Angry IP Scanner. Klik pada start dan biar sehingga semua julat IP address habis di imbas (192.168.1.0 ~ 192.168.1.255). Dalam kes saya julat IP address adalah (10.10.1.0 ~ 10.10.1.255.) Selepas itu scroll ke bawah sehingga awak terjumpa dengan hostname bernama raspberry, dalam kes saya saya sudah namanya raspberry pi kepada pi2-1. Daripada screen shot di bawah tertera butang biru dengan ip 10.10.1.25 yang merujuk pada hostname raspi2-1.local. Jika awak ada terjumpa hostname raspberry pi awak, ingat nombor IP addressnya.
  
  <br/>
  <br/>
![Angry Ip Scanner]({{site.baseurl}}/assets/img/angryipscan.jpg){: .center-image }

<br/>

Syabas, awak sudah boleh mula untuk mengakses raspberry pi secara remote. Terus maju!

Seterusnya, Run Terminal jika awak menggunakan linux atau mac, type command:-

```bash
ssh pi@10.10.1.25   // Tekan ENTER. (pastikan masukkan ip address yang awak perolehi)
Password: raspberry // Masukkan password, tekan ENTER
```

Kemudian, tekan Enter.

Awak sepatutnya telah berjaya mengakses masuk raspberry pi. Untuk windows, run MobaXterm. Aplikasi MobaXterm seperti gambar di bawah akan dipaparkan. klik pada "Session".
<br/>
<br/>

![MobaXterm]({{site.baseurl}}/assets/img/mobaxterm.jpg){: .center-image }
<br/>
<br/>
Kemudian klik SSH seperti gambar di bawah dan masukkan maklumat berikut:-
<br/>
<br/>

```javascript
Remote host: 10.10.1.25  // (pastikan masukkan ip address yang awak perolehi)
Username: pi
Port: 22
Klik Ok
Login password: raspberry
```
<br/>
<br/>

![MobaXterm]({{site.baseurl}}/assets/img/mobaxterm-ssh.jpg){: .center-image }
<br/>
<br/>

Awak juga boleh secara terus access melalui terminal mobaxterm tanpa perlu mengakses melalui session page. Masukkan command berikut pada terminal mobaxterm.
<br/>
```javascript
ssh pi@10.10.1.25 // Tekan ENTER. (pastikan masukkan ip address yang awak perolehi)
Password: raspberry // Masukkan password, tekan ENTER
```
<br/>
Awak sepatutnya sudah boleh mengakses raspberry pi!

Setelah awak mengakses masuk ke dalam raspberry pi. Awak boleh mengawalnya seolah-olah raspberry pi awak berada di dalam laptop. Namun, awak hanya boleh mengawal melalui Command Line Interface (CLI). Iaitu hanya melalui text command, tiada kawalan melalui interface grafik. Tambahan lagi, awak masih belum mengakses raspberry pi tanpa bolhe mencabut kabel network raspi ke router. Awak mahu raspi awak bebas ke internet tanpa wayar. Hmmm.. saya rasa lebih mudah mengaktifkan raspberry pi untuk menyambungkannya ke wifi melalui interface grafik. Berita baik! Kita boleh mengaktifkan VNC server servis di raspberry pi melalui ssh akses. Dengan ini paparan grafik desktop Raspbian OS akan dipaparkan pada komputer/laptop awak. [Camaner yek caranya]({% post_url 2018-11-8-Akses-secara-remote-ke-raspberry-pi-melalui-VNC %})  

