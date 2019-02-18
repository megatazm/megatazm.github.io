---
layout: post
title: Projek IoT, Sistem Pengecaman Plat Kereta - Bahagian 1
date: 2019-2-6 13:32:20 +0300
description:  # Add post description (optional)
img: iot-background-imej.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Belajar Melalui Projek, Learning Through Project, IoT]
---
Moh kita belajar IoT melalui contoh iaitu membina sistem pengecaman plat kereta menggunakan komputer kecil RaspberryPi dan perisian Node-Red. Orang putih selalu cakap **“Learning by doing, doing through example”**. Orang jepun pula kata **“Karada de oboero, genba genbutsu genjitsu da”** Oleh itu saya terfikir membinanya sambil memperoleh ilmu dan menyumbang untuk kegunaan keselamatan di taman perumahan tempat saya menginap. Ini kerana kadang-kadang ada beberapa buah kereta yang tidak dikenali menyelinap masuk ke kawasan perumahan kami, meninjau untuk aktiviti yang tidak baik. Yalah memandangkan servis pengawal keselamatan hanya mampu kami bayar untuk sesi malam sahaja. Dengan sistem yang mudah ini harapannya dapatlah dijadikan sebagai pengganti mata pengawal yang tidak tahu lelap di siang hari demi keselamatan warga taman kami tanpa perlu mengutip yuran bulanan tambahan yang sukar dikutip. 

Bunyinya macam susah jer untuk membina sistem ni, tapi mujurlah ada banyak contoh sistem pengecaman menggunakan **raspberrypi** dan **node-red** yang boleh dirujuk di **google.com** dan juga **youtube**. Namun memandangkan bahan rujukan tersebut rata-ratanya adalah dalam bahasa Inggeris, saya terpanggil untuk mengkongsikan ilmu ini dalam bahasa Melayu, bahasa Malaysia yang terpinggir dari dunia ilmuwan ICT. Ini kerana bahasa Inggeris terlalu meluas digunakan sebagai bahasa untuk belajar dan mengajar di Malaysia, maka kurang lah bahan rujukan dalam bahasa melayu, kalau ada pun bahasa Indonesia ada lah. Walaupun bahasa Inggeris sangat meluas digunakan di Malaysia tapi saya berpendapat tidak ramai masyarakat muda yang masih di bangku sekolah mampu untuk mencerna bahan-bahan rujukan ini kerana tahap bahasa Inggeris yang diperlukan agak tinggi. 

Ada kalanya walaupun ianya dalam bahasa Inggeris, tetapi ada juga yang urutan tutorialnya sangat mudah difahami dan step by step,namun mungkin kerana ianya bukan dalam bahasa ibunda maka gagal untuk menarik minat anak-anak muda. Saya rasa adalah sangat rugi kita menunggu ramai anak-anak kita mengenal IoT hanya setelah mereka mencapai di tahap universiti, bersedia dengan ilmu asas sains dan tahap bahasa Inggeris yang masih juga ramai tidaklah juga seberapa pun. Teknologi ICT sangat pantas berubah, teknologi ICT adalah hak untuk semua warga anak muda kita, maka mereka mesti didedahkan pada teknologi ini seawal mungkin. Oleh itu kita perlu menyediakan bahan-bahan pembelajaran dan rujukan untuk mereka dalam bahasa Malaysia. Saya sudi berkhidmat semampu mungkin, dan awak pula sudah bersedia? Jom! ᕕ( ᐛ )ᕗ

Awak sudah bersedia kan? Lepasi halangan kedua dahulu. Ya, halangan pertama telahpun bermula, iaitu awak telah membaca hingga ke titik ini, teruskan membaca tanpa jemu. Seterusnya, awak perlukan komitmen seperti berikut. Amacam ada brani?


### Raspberry Pi 

Versi terkini adalah **Raspberry Pi 3 model B+**. Maklumat berkenaan model-model yang lain yang boleh di rujuk di [sini](https://www.raspberrypi.org/products/). Kalau tak mampu ke Jalan Pasar, KL,  Bolehlah tanya pakcik google ataupun encik Lazada. Kalau ndak belajar duit boleh diusahakan. Alang-alang belilah model terkini. Cubalah minta dari mak atau bapak, saya yakin mereka akan belikan, daripada awak minta mereka belikan IPhone, jangan harap lah.

<br/>
<br/>
![Raspberry pi interface]({{site.baseurl}}/assets/img/raspi-interface.jpg){: .center-image }
<br/>
<br/>

### Wifi usb adapter 

Kalau awak beli Rapsberry Pi 3, Wifi disertakan. Selain dari model ini awak kena beli wifi adapter yang sesuai, silalah tanya pakcik google, **“usb wifi for raspberrypi”**. untuk maklumat awak, saya menggunakan usb wifi adapter **Aztech WL55USB** (seperti gambar di bawah) dicucuk pada raspberrypi 2, sangat bagus resepsinya. Kalau nak beli jenis lain, belilah batang antenanya yang panjang jangan beli yang pendek sebab resepsinya mungkin lemah. Saya ada beli 2 bijik **edimax usb wifi adapter**, nampak cun tapi awak toksah beli lah yang ini.

{:refdef: style="text-align: center;"}
![usbwifiadapter]({{site.baseurl}}/assets/img/usbwifiadapter.jpg)
{: refdef}

### SD Card 16Gb 

Memory card ini perlu untuk kita pasangkan Sistem Operasinya, Kita akan guna Raspbian OS, bukan Microsoft Windows OS tau!. Awak kena tahu macam mana nak set up sistem operasi raspbian ke dalam SD card, kalau tak tahu bolehlah ikut arahannya di sini. 

### 5V 2A mini USB power adapter 

Kita perlukan ini untuk power up raspberry pi. Kalau awak ada usb power bank atau android handphone charger. Kira jimatlah, takyah beli. Kalau takda pinjam mak atau bapak punya dahulu.

### Camera module 

Camera modul untuk menangkap gambar kereta kemudian dihantar ke sistem pengecaman nombor plate. Kita beli yang versi paling murah pun ok, **Camera Module V1.3 , 5MP**.

{:refdef: style="text-align: center;"}
![pi-camera]({{site.baseurl}}/assets/img/pi-camera.jpg)
{: refdef}

### HC-SR501 PIR Sensor atau Ultrasonic HC-SR04 sensor

**PIR sensor** ini digunakan untuk mengesan kehadiran objek yang mengeluarkan haba bergerak dalam lingkungan jarak **3 - 7 meter**. Selain itu ia juga boleh mengesan manusia atau haiwan. Apabila ada objek yang bergerak dikesan oleh pir sensor ini, raspberry pi melalui aplikasi node-red akan menerima isyarat tersebut kemudian mengarahkan camera untuk menangkap gambar. Namun memandangkan ia mengesan kehadiran objek dalam linkungan ruang yang besar, pir sensor ini mungkin akan kerap mengesan objek-objek di persekitaran. Oleh itu saya rasa adalah lebih baik kita mengguna ultrasonic sensor. 

{:refdef: style="text-align: center;"}
![hcsr04]({{site.baseurl}}/assets/img/hcsr04.jpeg)
{: refdef}

Ultrasonic sensor pada setiap detik tertentu memancar gelombang bunyi dengan lebih fokus ke arah sesuatu objek yang hendak kita kesan di hadapan. Gelombang bunyi ini akan terpantul kembali kepada ultrasonic sensor jika pancaran gelombang tersebut mengenai sesuatu objek. Dengan menggunakan formula fizik iaitu **Jarak = Laju x Masa**. Kita boleh mengukur jarak objek tersebut dengan mengukur masa gelombang itu terpantul kembali ke ultrasonic sensor. Bagi memperoleh jaraknya, masa tersebut didarabkan dengan kelajuan gelombang bunyi, seperti contoh:
```
Jika, 
masa (pergi dan balik) = 2 saat ,
Kelajuan bunyi = 343 meter sesaat.

Jarak perjalanan gelombang = 2 s x 343 m/s
                                        = 686 m (jarak pergi balik)
Oleh itu jarak di antara objek dan sensor = 686 m ÷ 2
                                          = 343 meter
```
Secara teorinya jaraknya adalah **343 meter** apabila pantulan gelombang bunyi mengambil masa **1 saat** (masa gelombang pergi dan balik = **2 saat**, dibahagi **2 = 1 saat**). Namun **ultrasonic sensor HC-SR04** beroperasi dalam julat **2cm(0.02m) - 400cm (4m)**. Dalam projek ini kita akan menyelidik dalam penetapkan jarak yang sesuai untuk memicu kamera menangkap gambar plat kereta. Inilah kelebihan ultrasonic sensor berbanding pir sensor yang tidak boleh mengukur jarak objek yang dikesan. Ciri Ini penting untuk memperoleh gambar plat kereta yang memberikan hasil pengecaman plat kereta yang jitu.

### Komputer Desktop atau Laptop

Kalau ada baguslah, sekurang-kurangnya komputer desktop (ber-Wifi). Mesti ada kan? kalau tak macam mana awak nak main game kesukaan awak tu. Tapi kalau macam mana pun takda juga, belilah keyboard, mouse dan kabel **HDMI**, di cucuk masuk pada raspberry pi awak. Tapi awak masih perlukan screen monitor komputer dan **VGA** adapter untuk disambungkan dengan HDMI cable. Sila rujuk disini caranya. Saya tak pastilah boleh ker di cucuk terus ke HDMI port di screen LED TV? Awak cuba lah ye.

### PVC casing box 

Bekas untuk awak masukkan raspberry pi, camera modul, motion sensor, 5v power supply. Saya beli **“Dummy Fake Security CCTV Simulation Surveillance”**, RM40. 

{:refdef: style="text-align: center;"}
![dummycameracase]({{site.baseurl}}/assets/img/dummycameracase.jpg)
{: refdef}

Kalau nak murah sikit carilah kotak PVC yang bersesuaian. Kalau awak tak ndak pasang betul-betul lagi, cuma nak try jer dulu, takyah beli lah.

### Camera Box Stand

Kalau pasang kotak PVC tu nanti, kena lah ada kakinya. Kita fikir lah nanti yer, camaner nak bikin. Tak pun lekat jer kat batang pokok di tepi jalan.

### Extension Cable

Disebabkan pokok tidak menghasilkan tenaga letrik, awak kena panjangkan kabel dari sumber letrik daripada rumah. Paling mudah belilah extension cabel yang boleh di gulung-gulung tu. Ingat, minta kebenaran mak dan bapak dulu. Buat masa ni untuk testing, pakai power bank jer dulu.

### WIFI internet connection

Zaman lani kalau tak dak internet mana boleh hidup. Kalau rumah awak takda Uni-Fi, Streamyx ataupun IPTV, pakai jer handphone awak, set kan tethering wifi hotspot. Zaman lani budak sekolah pun dah ada handphone sendiri, tak pun minta mak atau bapak awak kongsikan internet hotspot. 

### Jumper cable
Jumper cable ini perlu untuk menyambung raspberry pi dengan sensor PIR dan lampu LED. Bermula dari kiri, adalah kumpulan kabel hujung penyambung jenis **female-female**, **male-male** dan **male-female**. Sila siap sedia ketiga-tiga jenis kabel penyambung ini, awak akan perlukannya untuk situasi tertentu.

{:refdef: style="text-align: center;"}
![jumpercable]({{site.baseurl}}/assets/img/jumpercable.jpg)
{: refdef}

### Breadboard

Awak akan mengunakan breadboard dan jumper cable untuk memudahkan awak membina litar yang menyambungkan raspberry pi dengan peranti input seperti sensor pir dan peranti output seperti lampu LED. Kebiasaannya, **breadboard** digunakan ketika testing sahaja. Setelah selesai dengan proses testing, untuk proses implementasi, awak perlu mematerikan litar itu di papan litar. Saya rasa awak beli lah yang bersaiz kecil seperti gambar di bawah jer dulu.

{:refdef: style="text-align: center;"}
![breadboard]({{site.baseurl}}/assets/img/breadboard.jpeg)
{: refdef}

### Ethernet cable

Awak perlukan kabel ini jika awak hendak mengakses masuk untuk mengawal raspberry pi menggunakan laptop atau desktop melalui wifi. Jika awak nak tau cara untuk mengakses masuk raspberry pi secara remote, boleh lah rujuk [di sini]({% post_url 2018-10-14-Akses-secara-remote-ke-raspberry-pi-melalui-laptop-atau-desktop %}). 

{:refdef: style="text-align: center;"}
![ethernetcable]({{site.baseurl}}/assets/img/ethernetcable.jpg)
{: refdef}

### Raspbian with Node-red

Perisian node-red ini telah siap sedia dipasang pada sistem operasi Raspbian. Node-red adalah aplikasi yang dicipta sebagai alat pengaturcaraan secara visual dengan konsep **click, drag, drop, connect**, set dan lancarkan tanpa perlu melakukan sebarang pengaturcaraan. Namun untuk membina sesuatu sistem yang komplex, anda masih perlu melakukan pengaturcaraan, tetapi ia boleh dilakukan dengan pantas dan mudah. Jika anda ingin tahu secara asas berkenaan node-red, sila lah rujuk [di sini]({% post_url 2018-11-13-Pengenalan-aplikasi-node-red %}).

### Daftar akaun platerecognizer.com

Kita bernasib baik sebab telah adanya servis perisian pengecaman nombor plat kereta percuma (percuma **2500 ~ 5000** permintaan untuk pengecaman dalam sebulan) melalui cloud API request. [Camaner tu..]({% post_url 2018-10-17-Projek-IoT-Sistem-Pengecaman-Plat-Kereta %})

### Notification push account (Twitter, email or others using node-red)

Saya sudah ada akaun gmail.com untuk kegunaan harian selain akaun email tempat kerja saya. Untuk menghantar notifikasi daripada aplikasi node-red, saya cadangkan awak buka akaun yahoo mail yang baru. Selain notifikasi melalui emel, node-red juga membolehkan anda menghantar notifikasi ke akaun twitter.


Ok sampai di sini sahaja untuk bahagian 1. Untuk bahagian 2 tunggu ya..













