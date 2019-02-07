---
layout: post
title: Akses Raspberry Pi dengan Keyboard, Mouse dan Monitor
date: 2018-10-12 13:32:20 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: iot-background-imej.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Camaner, How to]
---
Jika awak hendak mengakses raspberry pi secara terus anda perlu menyediakan perkakas berikut:-

* Keyboard
* Mouse
* Screen monitor
* Kabel HDMI
* HDMI - VGA adaptor
* SD card mini 16GB + Raspbian OS
* USB 5V power supply/power bank

Merujuk pada gambar raspberry pi 3 seperti dibawah, sambungkan keyboard, mouse ke port usb dan kabel HDMI ke port HDMI.  

<br/>
<br/>
![Raspberry pi interface]({{site.baseurl}}/assets/img/raspi-interface.jpg){: .center-image }
<br/>
<br/>

Sambungkan HDMI-VGA adaptor pada hujung kabel HDMI, kemudian sambungkannya pada kabel VGA screen monitor. Masukkan SD card mini yang sudah dimuatkan dengan Raspbian OS ([Camaner nak buat?]({% post_url 2018-11-13-Memasang-raspbian-os-ke-sd-card %})). Sambungkan 5V USB power supply/power bank pada raspberry micro usb port. Selepas switch on power supply 5V,  lampu LED hijau raspberry pi akan berkelip-kelip. Pada ketika itu juga awak sepatutnya dapat melihat raspbian desktop seperti gambar di bawah di paparkan di skrin monitor.

<br/>
<br/>
![Raspberry OS]({{site.baseurl}}/assets/img/raspbian-os.jpg){: .center-image }
<br/>
<br/>

Jika raspbian desktop telah dipaparkan, awak sepatutnya boleh mengerakkan mouse cursor dan menggunakan keyboard. Ok, awak sudah berjaya! Tapi kan, kalau awak ada 100 raspberry pi yang setiap satunya berapa di tempat yang berbeza dan berjarak jauh di antara satu sama lain, macam mana? Ketika ini lah akses secara remote melalui internet memudahkan urusan. Awak boleh mengakses kesemua 100 raspberry pi itu dari satu lokasi sahaja. [Camaner yek]({% post_url 2018-10-14-Akses-secara-remote-ke-raspberry-pi-melalui-laptop-atau-desktop %})





