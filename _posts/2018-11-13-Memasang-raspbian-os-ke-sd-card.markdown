---
layout: post
title: Memasang Raspbian OS ke Dalam SD Card
date: 2018-11-8 13:32:20 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: i-rest.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Camaner, How to, IoT]
---
Cucuk masukkan SD Card awak pada komputer. Sediakan USB SD card reader (kalau takda kena belilah) jika tiada port untuk SD card tersebut pada komputer awak. Sekiranya awak menggunakan MacOS, awak boleh ikut arahan seperti berikut. Jika menggunakan Windows, sila skrol terus ke bawah merujuk pada arahan untuk Windows.

### Untuk Mac OS
 
Buka aplikasi "Disk Utility" dan cari SD card yang awak cucuk tadi. Untuk membukanya dengan pantas, klik "Sportlight Search" di hujung kanan atas skrin retina display. Taipkan "Disk Utility" kemudian ENTER.

<br/>
{:refdef: style="text-align: center;"}
![disk-utility-mac]({{site.baseurl}}/assets/img/disk-utility-mac.jpg)
{: refdef}
<br/>

Awak perlu memformat kad SD ke FAT-32. Untuk melakukannya, awak perlu mengklik pada "Apple SDXC Reader"  (maklumat ini berbeza pada komputer awak) di column kiri Disk Utility seperti gambar di atas. Pastikan klik SD card betul-betul, jangan awak format hardisk MacOS pulak.
<br/>
```javascript
1. Klik tab "Erase".
2. Namakan SD card (Namakan dengan nama yang awak suka). 
3. Untuk jenis formatnya, pilih MS-DOS (FAT).
4. Klik "Erase".
```
<br/>
{:refdef: style="text-align: center;"}
![disk-utility-mac2]({{site.baseurl}}/assets/img/disk-utility-mac2.jpg)
{: refdef}
<br/>
Selesai format SD cards? Awak akan dipaparkan dengan maklumat seperti gambar di atas. Ok, download "Raspbian Stretch with Desktop" OS dari [sini](https://www.raspberrypi.org/downloads/raspbian/). Satu lagi software yang perlu di download dan install, ialah [Etcher](https://www.balena.io/etcher/). Etcher seperti gambar di bawah digunakan untuk "flash" atau menyalin fail imej Rapbian OS yang awak download tadi ke dalam SD card supaya ianya "bootable" (boleh dibootkan oleh raspi). 
<br/>
```javascript
1. Klik  "Select Image".
2. Pastikan nama SD card adalah betul. 
3. Jika ingin menukar SD Card. Klik "Change".
4. Klik "Flash!"
```
<br/>
{:refdef: style="text-align: center;"}
![disk-utility-mac2]({{site.baseurl}}/assets/img/Etcher.png)
{: refdef}
<br/>

SD card awak sekarang sudah berintikan Rasbian OS!

### Untuk Windows

Untuk Windows, [SDFormater](https://www.sdcard.org/downloads/formatter_4/) digunakan untuk memformat SD card dan [Win32 Disk Imager](https://sourceforge.net/projects/win32diskimager/) pula (Guna [Etcher](https://www.balena.io/etcher/) pun boleh) untuk awak "flash" SD card  supaya ianya berisikan Raspbian OS dan membolehkan dibootkan oleh raspi. Download dan install kedua-dua software tersebut dan pastikan awak juga download "Raspbian Stretch with Desktop" OS dari [sini](https://www.raspberrypi.org/downloads/raspbian/).

<br/>
{:refdef: style="text-align: center;"}
![disk-utility-mac2]({{site.baseurl}}/assets/img/sdformatter.png)
{: refdef}
<br/>

Sekarang buka SDFormatter dan pilih Drive SD card yang awak masukkan tadi. Pilih "Quick Format, Format Size Adjustment ON". Klik "Format" dan tunggu sehingga selesai.

<br/>
{:refdef: style="text-align: center;"}
![disk-utility-mac2]({{site.baseurl}}/assets/img/win32diskimager-1.png)
{: refdef}
<br/>

Setelah SD card telah diformatkan, awak boleh mula "Flash" imej Raspbian. Jalankan Win32DiskImager, pilih imej Raspbian OS yang awak telah downloadkan tadi dan pilih Drive SD card yang betul. Kemudian klik "Write" dan sahkan dengan mengklik "Yes".

<br/>
{:refdef: style="text-align: center;"}
![disk-utility-mac2]({{site.baseurl}}/assets/img/win32diskimager-2.png)
{: refdef}
<br/>

Selepas proses selesai, awak boleh mengeluarkan SD card itu kemudian memasukkannya ke RaspberryPi untuk digunakan, [Camaner nak guna?]({% post_url 2018-10-14-Akses-secara-remote-ke-raspberry-pi-melalui-laptop-atau-desktop %})











