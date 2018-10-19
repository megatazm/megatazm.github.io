---
layout: post
title: Akses raspberry pi secara remote melalui laptop atau desktop
date: 2018-10-14 13:32:20 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: i-rest.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Camaner nak, How to]
---
Kebolehan untuk mengakses komputer secara remote melalui internet sangat penting dalam menjalankan pengurusan sistem komputer dengan berkesan dan efisien. Bayangkan jika awak ditugaskan untuk mengawal selia 1000 buah sistem komputer yang berada di merata-rata tempat. Pengaksesan secara remote bukan sahaja memudahkan tugasan awak, ia juga menjimatkan kos operasi syarikat. Bila kos operasi rendah, syarikat memperoleh keuntungan lebih, bonus pun dapat lebih. Untuk membolehkan raspberry pi menerima akses secara remote melalui wifi router dari komputer lain, aplikasi SSH perlu diaktifkan terlebih dahulu. Selepas itu awak perlu menyambungkan wifi raspberry pi ke wifi router tanpa memerlukan keyboard, mouse dan monitor, gimana dong?. Berikut adalah langkah-langkahnya:-

* Perkakas yang diperlukan ialah, Wifi router, kabel ethernet, raspberry pi beserta wifi adapter, 5V USB power supply/power bank,
  SD card mini 16GB + Raspbian OS dan komputer/laptop.
* Download dan install perisian [Angry IP Scanner](https://angryip.org/download/) ke dalam komputer. Awak akan gunakan perisian ini 
  untuk mengimbas dan mendapatkan IP address raspberry pi. Setiap komputer mesti memerlukan IP address iaitu suatu nombor ID yang unik untuk berkomunikasi. Bayangkan awak memanggil Rahman! di sebuah shopping komplex, mungkin ada lebih dari seorang akan menyahut. Berita baik, jika awak menginap di penjara, awak akan diberikan nombor id yang unik!
* Jika awak menggunakan MS Windows. Saya cadangkan awak download perisian [MobaXterm](http://download.mobatek.net/1092018073012523/MobaXterm_Installer_v10.9.zip). Perisian ini memudahkan awak mengakses
  raspberry pi secara remote dari komputer windows.
* Masukkan SD card yang telah dimuat dengan Raspbian OS melalui SD Card reader ke komputer. 
* Klik masuk ke dalam SD card tersebut, seterusnya klik masuk ke dalam direktori /boot. Kemudian ciptakan satu text file kosong
  yang dinamakan ssh.
* Ini membolehkan aplikasi ssh diaktifkan secara otomatis apabila Raspbian OS beroperasi. Aplikasi ssh membolehkan komputer dari
  luar mengakses masuk ke dalam raspberry pi.
* Cucuk masuk power supply 5V pada raspberry pi untuk menghidupkan (boot up) Raspbian OS. Tunggu sehingga led hijau tidak 
  berkelip-kelip lagi.
* Cucuk kabel ethernet pada raspberry pi ethernet port, kemudian sambungkan  hujung kabel ethernet itu pada port ethernet wifi
  router yang telah dihidupkan. 
* Sambungkan wifi connection komputer/laptop awak pada wifi router tersebut. Dengan ini komputer/laptop awak berada di dalam
  lingkungan jaringan komunikasi yang sama dengan raspberry pi. Run aplikasi Angry IP Scanner. Klik pada start dan biar sehingga semua julat IP address habis di imbas (192.168.1.1 ~ 192.168.1.254). Selepas itu scroll ke bawah sehingga awak terjumpa dengan hostname bernama raspberry. Jika awak ada terjumpa, ambil nombor IP addressnya. Sebagai contoh, seperti gambar di bawah IP nya adalah 192.168.1.64.

![Angry Ip Scanner]({{site.baseurl}}/assets/img/angryipscan.jpg){: .center-image }

Syabas, awak sudah boleh mula untuk mengakses raspberry pi secara remote. Terus maju!

Seterusnya, Run Terminal jika awak menggunakan linux atau mac, type command:-

```bash
ssh pi@192.168.1.64
Password: raspberry
```

Kemudian, tekan Enter.

Awak sepatutnya telah berjaya mengakses masuk raspberry pi. Untuk windows, run MobaXterm. Aplikasi MobaXterm seperti gambar di bawah akan dipaparkan. klik pada "Session".
<br/>

![MobaXterm]({{site.baseurl}}/assets/img/mobaxterm.jpg){: .center-image }
<br/>

Kemudian klik SSH seperti gambar di bawah dan masukkan maklumat berikut:-
<br/>

```bash
Remote host: 192.168.1.64 
Username: pi
Port: 22
Klik Ok
Login password: raspberry
```

![MobaXterm]({{site.baseurl}}/assets/img/mobaxterm-ssh.jpg){: .center-image }


Awak sepatutnya berjaya mengakses raspberry pi!

Setelah awak mengakses masuk ke dalam raspberry pi. Awak boleh mengawalnya seolah-olah ia berada di depan mata. Namun, awak hanya boleh mengawal melalui Command Line Interface (CLI). Iaitu hanya melalui text command, tiada kawalan melalui interface grafik. Hmmm.. saya rasa lebih mudah untuk mengaktifkan dan menyambungkan masuk ke wifi raspberry pi melalui interface grafik. Berita baik! Kita boleh mengaktifkan VNC server pada raspberry pi untuk servis remote desktop. Dengan ini paparan desktop Raspbian OS akan dipaparkan pada komputer/laptop awak. Camaner yek caranya VNC tu.

