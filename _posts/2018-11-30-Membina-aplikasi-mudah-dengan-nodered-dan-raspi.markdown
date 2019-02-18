---
layout: post
title: Projek IoT, Membina Aplikasi Mudah dengan Node-RED dan Raspi
date: 2018-11-30 13:32:20 +0300
description:  # Add post description (optional)
img: iot-background-imej.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Belajar Melalui Projek, Learning Through Project, IoT]
---

Hari ini kita cuba membina sebuah aplikasi mudah menguna-pakai Node-RED dan Raspi. Jika awak tidak tahu apa itu Node-RED, boleh rujuk [di sini]({% post_url 2018-11-13-Pengenalan-aplikasi-node-red %}). Raspi pun tak tau jugak, [haa, pegi ke sini]({% post_url 2018-10-12-Akses-raspberry-pi-dengan-keyboard-mouse-dan-monitor %}). 

Ok. berkenaan dengan tutorial projek ini, saya nak bagitau awak yang tutorial ini saya ambil dari [sini](https://projects.raspberrypi.org/en/projects/getting-started-with-node-red/11). Kepada yang memang dah mahir Bahasa Inggerisnya bolehlah terus jer ke situ. Saya rasa tutorial ni bagus untuk dikongsikan dalam Bahasa Malaysia. So, saya cuma tolong terjemah dan olahkan sikit-sikit, mana-mana yang patut. 

### Apa yang awak akan buat

Dalam projek ini, awak akan belajar bagaimana menggunakan Node-RED untuk berkomunikasi dengan pin GPIO Raspberry Pi. Awak akan membuat 'FLOW Node-RED' untuk mengawal LED.

### Apa yang awak akan belajar

Dengan menggunakan Node-RED dan Raspberry Pi ini, awak akan belajar:

* Bagaimana untuk membina FLOW Node-RED
* Bagaimana untuk mengawal pin GPIO dengan Node-RED
* Cara menggunakan input, output dan suis Node-RED
* Menggunakan Node-RED untuk mensimulasikan sebuah "NOT GATE" yang bertindakbalas apabila menerima input dari butang input

### Perkakas yang awak perlu sediakan

* Raspberry Pi
* 1 x LED
* 1 x Solderless breadboard
* 4 x Male-to-female jumper leads
* 1 x 330R resistor
* 1 x Tactile push button
* Software Node-RED

Kenapa tak translate jer perkakas-perkakas di atas dalam Bahasa Malaysia. Ohh.. tidak perlu, sebab awak perlu gunakan nama perkakas-perkakas ini dalam Bahasa Inggeris. Copy-paste nama-nama ini pada google search engine dan klik pada "image" untuk melihat gambar-gambarnya. Lagipun kalau awak nak beli perkakas-perkakas di atas itu, nama-nama ini adalah standardnya. Oh ya, jika awak nak tahu macamana ndak menyediakan OS Raspbian (sudah siap ada dengan software Node-RED) ke dalam Raspberry Pi, [sila ke sini]({% post_url 2018-11-13-Memasang-raspbian-os-ke-sd-card %}) 

### GPIO pins

Salah satu ciri yang hebat dari Raspberry Pi adalah barisan pin GPIO di sepanjang bahagian atas papannya. GPIO bermaksud "General-Purpose Input Output". Pin input output untuk kegunaan umum ini adalah interface fizikal antara Raspberry Pi dan dunia luar. Awak boleh andaikannya sebagai suis yang boleh awak on atau off, bertindak sebagai input ke dalam raspberry pi atau output daripada raspberry pi ke dunia luar.

Oleh itu pin GPIO boleh digunakan untuk menyambungkan Raspberry Pi ke alatan elektronik, yang membolehkannya mengawal dan memantau dunia luar. Melalui pin GPIO, Raspberry Pi boleh menghidupkan atau mematikan LED, menjalankan motor, dan melaksanakan banyak lagi operasi lain. Ia juga boleh mengesan dan memantau keadaan luaran, seperti suhu, tahap cahaya, dan sama ada suis yang disambungkan padanya telah ditekan.

Kini ada 40 pin pada Raspberry Pi (model awal cuma ada 26 pin sahaja), dan pin tambahan ini menyediakan pelbagai fungsi yang berbeza. Jika awak mempunyai label pin "RasPiO" (seperti gambar di bawah), ia boleh membantu untuk mengenal pasti penggunaan setiap pin itu. Semasa memasang label pin "RasPiO" itu, pastikan ia diletakkan dalam keadaan yang mana lubang berlingkaran emas atau "keyring" itu bersebelahan dengan port USB seperti gambar di bawah.

<br/>
{:refdef: style="text-align: center;"}
![raspio-ports]({{site.baseurl}}/assets/img/raspio-ports.jpg)
{: refdef}
<br/>

Jika awak takda label pin atau tak ndak beli, boleh sahaja rujuk pada gambar di bawah. Awak jangan konfius. Lubang "keyring" pada gambar di bawah tu adalah lubang untuk screw yang berada di bucu kanan raspberry pi. 

<br/>
{:refdef: style="text-align: center;"}
![raspi-pinout]({{site.baseurl}}/assets/img/raspi-pinout.png)
{: refdef}
<br/>

Merujuk pada gambar di atas, awak akan nampak pin berlabel seperti contoh; 3V3, 5V, GND dan GP2, GP3, dan sebagainya.

|<center>Label</center> | <center>Maksud</center> | <center>Keterangan</center> |
|------ | ----- | ----- |
| <center>3V3</center> | <center>3.3 Volts</center> | Apa-apa yang disambungkan pada pin ini akan sentiasa menerima voltan 3.3V|
| <center>5V</center> | <center>5 volts</center> | Apa-apa yang disambungkan pada pin ini akan sentiasa menerima voltan 5V|
| <center>GND</center> | <center>Ground</center> | Voltan sifar, digunakan untuk melengkapkan litar|
| <center>GP2</center> | <center>GPIO pin 2</center> | Pin ini boleh dikonfigurasikan sebagai pin input atau output|
| <center>ID_SC/ID_SD/DNC</center> | <center>Pin untuk tujuan khas</center> | |

**AMARAN**: jika awak mengikut arahan, maka bermain dengan pin GPIO adalah selamat dan menyeronokkan. Tapi, jika awak main suka-suka jer sambung sana-sini pada pin Raspberry Pi, awak boleh memusnahkannya. Terutamanya jika awak menggunakan pin 5V.

### Menyambung wayar pada LED

Sambungkan kabel dari LED pada "breadboard" ke pin GPIO 17 pada Raspberry Pi seperti gambar di bawah.

<br/>
{:refdef: style="text-align: center;"}
![led-gpio17]({{site.baseurl}}/assets/img/led-gpio17.png)
{: refdef}
<br/>

Perhatikan wayar merah yang bermula dari pin GPIO 17. Kalau awak ada sedikit ilmu teknologi elektrik, awak boleh agak pin GPIO 17 ini merupakan pin output yang bervoltan positive. Oleh itu wayar merah ini perlu disambungkan pada kaki positif LED yang biasanya lebih panjang. Kaki LED yang panjang ini harus dimasukkan ke sebelah kiri breadboard seperti gambar di atas. Kaki LED yang pendek pula perlu disambungkan dengan perintang 330 Ohm untuk menetapkan nilai arus elektrik yang bersesuaian dengan keperluan LED itu. Litar ini dilengkapkan dengan menyambung wayar hitam dari hujung perintang itu ke pin GND pada raspberry pi.

### Start Node-RED

Pertama, awak mestilah boleh mengakses raspberry pi melalui VNC server. Sila [ke sini]({% post_url 2018-11-8-Akses-secara-remote-ke-raspberry-pi-melalui-VNC %}) jika awak  ndak tahu camaner mengaktifkannya. Tetapi sebelum itu awak kena pastikan raspberry pi dan komputer awak disambungkan pada WIFI router yang sama. Silalah [ke sini]({% post_url 2018-10-14-Akses-secara-remote-ke-raspberry-pi-melalui-laptop-atau-desktop %}) jika awak belum lagi melakukannya.

Untuk memulakan Node-RED, Klik pada ikon Raspberry > Programming > Node-RED. 

<br/>
{:refdef: style="text-align: center;"}
![nodered-start-gui]({{site.baseurl}}/assets/img/nodered-start-gui.png)
{: refdef}
<br/>

Awak sepatutnya dapat melihat konsol (seperti gambar di bawah) yang memaparkan maklumat tentang Node-RED sedang bermula.

<br/>
{:refdef: style="text-align: center;"}
![nodered-startup]({{site.baseurl}}/assets/img/nodered-startup.png)
{: refdef}
<br/>

Untuk mengakses sofware Node-RED, awak boleh melakukannya dengan dua cara. Pertama, awak boleh mengaksesnya secara terus atau local dengan, 

```javascript
1. klik Ikon raspberry pi > Internet > Chromium Web Browser
2. kemudian taip, http://localhost:1880 (di url address browser). 
```
<br/>
{:refdef: style="text-align: center;"}
![start-chrome]({{site.baseurl}}/assets/img/start-chromium.png)
{: refdef}
<br/>

{:refdef: style="text-align: center;"}
![nodered-blank]({{site.baseurl}}/assets/img/nodered-blank.png)
{: refdef}
<br/>


Tapi saya lebih suka mengakses software Node-RED secara remote melalui laptop sebab grafiknya lebih jitu dan tangkas. Untuk cara kedua, dilaptop atau komputer awak,

```javascript
 1. Buka internet browser (chrome atau firefox)
 2. Kemudian taip, http://ip-address-raspberrypi-awak:1880 (di url address browser).
 ```

 Syabas! Node-RED, alat untuk membina aplikasi IoT secara visual sudah berada di depan awak. <(^,^)>

### Menyambung ke pin GPIO

Program di Node-RED dipanggil "FLOWS". Jika awak lihat gambar interface Node-RED di atas, awak dapat melihat bahawa halaman kosong itu dilabelkan sebagai FLOW 1 pada tab di atas. Awak boleh membuat seberapa banyak FLOW yang awak mahu dan FLOW itu semua boleh berjalan pada masa yang sama. Tapi untuk projek yang mudah ini, kita hanya memerlukan satu FLOW sahaja.

Blok berwarna yang berada di kiri paparan interface Node-RED adalah pelbagai nod yang boleh awak gunakan untuk membina FLOW yang berguna. Skrol ke bawah sehingga awak berjumpa denga nod berlabel Raspberry Pi.

<br/>
{:refdef: style="text-align: center;"}
![raspi-nodes]({{site.baseurl}}/assets/img/raspberry-pi-nodes.png)
{: refdef}
<br/>

Awak akan nampak ada dua nod dengan label **rpi gpio**. Awak akan gunakan nod ini untuk bercakap dengan pin GPIO di Raspberry Pi. Nod yang ikon raspberrynya di sebelah kiri adalah untuk input. Nod kedua, dengan ikon raspberrynya di sebelah kanan adalah untuk output. Awak akan menggunakan nod input untuk menerima arahan daripada butang suis dari luar rasberry pi. Manakala nod output pula digunakan untuk menghidupkankan LED. Klik, seret dan lepaskan nod output itu tadi keluar ke halaman kanvas kosong Node-RED.

<br/>
{:refdef: style="text-align: center;"}
![drag-output-node]({{site.baseurl}}/assets/img/drag-output-node.png)
{: refdef}
<br/>

Klik dua kali pada nod output itu dan kotak "Edit rpi-gpi out node" akan muncul untuk membolehkan awak mengkonfigurasikan nod itu. Set konfigurasi seperti maklumat dibawah, kemudian klik "Done".

```javascript
GPIO : "Pin 11 - GPIO17"
Type : "Digital Output"
        Check > "Initialise Pin State"
        set   > "initial level of pin - low(0)"
Name : "Green LED"
```
<br/>
{:refdef: style="text-align: center;"}
![setup-output]({{site.baseurl}}/assets/img/set-up-output.png)
{: refdef}
<br/>

### Menyuntik mesej

Sekarang kembali semula ke palet nod dan skrol ke atas atau ke bawah mencari nod input yang boleh digunakan sebagai pencetus untuk menghidupkan dan mematikan LED. Seret masuk "Inject Node" ke dalam Node-RED kanvas Flow 1. Dengan nod ini awak boleh menyuntik mesej sebagai input ke nod yang seterusnya dan menyebabkan berlakunya flow proses. Hasil dapatan akan diperolehi di penghujung nod di dalam Flow ini.

<br/>
{:refdef: style="text-align: center;"}
![inject-node]({{site.baseurl}}/assets/img/inject-node.png)
{: refdef}
<br/>

Klik dua kali pada inject node itu. Gunakan "drop-down" di sebelah **Payload** untuk mengubah jenis data kepada **string** dan taip **1** di dalam kotak **Payload**. Ini akan menjadi mesej yang akan disampaikan ke nod sebelah. Taip **On** di dalam kotak **Nama**. Selepas selesai mengisi maklumat tersebut seperti gambar di bawah, tekan **Done**. 

<br/>
{:refdef: style="text-align: center;"}
![edit-inject]({{site.baseurl}}/assets/img/edit-inject.png)
{: refdef}
<br/>

Ulangi langkah-langkah sebelum ini untuk menyeret masuk satu lagi inject nod. Kali ini taip **0** di dalam kotak **Payload** dan taip **Off** di dalam kotak **Nama**.

<br/>
{:refdef: style="text-align: center;"}
![add-2-nodes]({{site.baseurl}}/assets/img/add-2-nodes.png)
{: refdef}
<br/>

Kemudian, klik dan seret dari titik kelabu nod **On** dan nod **Off** ke titik kelabu pada nod **LED** untuk menyambungkannya.

<br/>
{:refdef: style="text-align: center;"}
![join-nodes]({{site.baseurl}}/assets/img/join-nodes.png)
{: refdef}
<br/>

### Menjalankan Flow

Dengan gabungan tiga nod ini, maka lengkaplah satu "Flow" yang ringkas. Jom kita mula gunakannya. Klik pada butang merah **Deploy** di bahagian atas sebelah kanan skrin. Mesej akan dipaparkan mengatakan “Successfully deployed”. Maksudnya, tiada "syntax error" dan bersedia untuk beraksi.

<br/>
{:refdef: style="text-align: center;"}
![deploy]({{site.baseurl}}/assets/img/deploy.png)
{: refdef}
<br/>

Sekarang klik pada kotak biru di sebelah kiri nod **On** untuk menyuntik mesej **1**. Dengan ini, nod **Green LED** menerima mesej ini dan mengarahkan raspberry pi menyalakan LED di pin GPIO 17. Untuk mematikan LED itu, awak hanya perlu mengklik kotak biru pada nod **Off** pula, yang menyuntikkan mesej **0** kepada nod **Green LED**.

<br/>
{:refdef: style="text-align: center;"}
![deploy-on]({{site.baseurl}}/assets/img/deploy-on.png)
{: refdef}
<br/>

### Debugging Flow

Jika LED awak tidak mau menyala, pastikan awak periksa bahawa komponen-komponen pada "breadboard" itu telah dipasang dengan betul dan kemas. Periksa betul-betul kabel dari **ground** dan **pin 17** pada Raspberry Pi. Saya cadangkan awak guna "multimeter" untuk memeriksa sambungan kabel itu samada ianya lengkap. Setelah yakin sambungan komponen elekrik dan dan kabel itu lengkap, awak boleh gunakan "Debug Node" untuk memeriksa atau "debugging" samada setiap nod yang telah dikonfigurasikan tadi adalah betul.

Untuk menjalankan proses "debugging", seret masuk "Debug Node" ke kanvas. Sambungkannya dari nod **on** dan nod **off** ke nod **Debug**, kemudian klik Deploy. Apabila awak mengklik butang untuk menyuntik mesej, Node-RED akan memaparkan nilai yang disuntik dalam tab **Debug** di sebelah kanan skrin. Klik tab Debug itu untuk melihat mesej.

<br/>
{:refdef: style="text-align: center;"}
![debug-node]({{site.baseurl}}/assets/img/debug-node.png)
{: refdef}
<br/>

Sebagai contoh, tab **Debug**  memaparkan nilai **1** jika awak klik inject pada nod **On**, dan nilai **0** jika di klik inject pada nod **Off**. Ini bermaksud Flow yang awak bina ini beroperasi dengan betul.

<br/>
{:refdef: style="text-align: center;"}
![debug-panel]({{site.baseurl}}/assets/img/debug-panel.png)
{: refdef}
<br/>

### Menambah butang input

Sekarang jom kita tambah butang suis untuk mengawal LED secara fizikal. Pasangkan butang suis dan sambungkannya ke Raspberry Pi seperti yang ditunjukkan pada imej di bawah. Salah satu kaki suis itu disambungkan ke pin **GPIO 4** dan satu lagi ke **ground**. Pastikan LED yang awak pasangkan tadi masih lagi bersambung ke pin **GPIO 17**. 

<br/>
{:refdef: style="text-align: center;"}
![buttonlightsLED]({{site.baseurl}}/assets/img/buttonlightsLED.png)
{: refdef}
<br/>

Oleh kerana kali ini awak akan mengawal LED menggunakan butang suis fizikal, buang nod **On** dan **Off** yang awak buat sebelum ini. Klik pada nod-nod itu dan tekan **Delete** pada keyboard komputer awak.

Sekarang awak perlu menambah nod input **raspi gpio**. Ini adalah nod dengan ikon raspberry di sebelah kiri. Sediakan nod ini untuk menerima input dari butang suis fizikal anda seperti imej di bawah.

<br/>
{:refdef: style="text-align: center;"}
![set-up-input]({{site.baseurl}}/assets/img/set-up-input.png)
{: refdef}
<br/>

 Konfigurasi ***pullup*** bermaksud status voltan PIN GPIO 4 akan ditetapkan ke **HIGH**, dan apabila awak menekan suis butang, status voltan pin itu akan bertukar kepada **LOW**.

Sekarang sambungkan nod input **Button** itu ke nod debug dan nod LED yang sedia ada. Klik **Deploy** dan uji dengan menekan butang suis di breadboard.

<br/>
{:refdef: style="text-align: center;"}
![wrong-button-flow]({{site.baseurl}}/assets/img/wrong-button-flow.png)
{: refdef}
<br/>

Awak akan dapati LED akan dinyalakan sebaik sahaja **Deploy** diklikkan, dan LED akan terpadam jika awak tekan butang suis. Ini tidak seperti yang kita mahukan! Perkara ini berlaku sebab kita menggunakan konfigurasi ***pullup*** seperti yang diterangkan pada langkah sebelum ini. Jadi, pin output **raspi gpio** akan bermula dengan status **HIGH**. Oleh kerana status **HIGH** menghasilkan output mesej **1** kepada nod LED, ia menyebabkan LED itu dihidupkan. Sebaliknya, apabila awak menekan suis, ia akan menyebabkan status berubah kepada **LOW**, menjana output mesej **0** lalu mematikan LED. Oleh itu, awak perlu melakukan sedikit perubahan supaya nod LED menerima mesej **1** apabila suis ditekan dan menerima mesej **0** apabila suis tidak ditekan.

Oleh itu, padamkan sambungan di antara nod output **Button** dan nod **LED** tadi dengan mengklik pada sambungan lalu menekan **delete** pada keyboard komputer. Skrol nod palet ke bahagian **Function** kemudian seret **Switch Node** ke dalam kanvas. Jika awak pernah belajar programming, nod switch ini adalah sama dengan menggunakan penyataan **if elif else**. Jika nod switch menerima mesej **1** atau **0**, awak boleh mengkonfigurasikannya supaya mengubah aliran FLOW kepada nod-nod yang lain. Seperti imej di bawah, awak boleh tambah supaya dua output keluar dari nod switch ini. Setkan supaya jika nilai msg.payload adalah sama dengan **1**, aliran flow akan disalurkan ke output **1**. Sebaliknya jika nilainya disetkan **otherwise** iaitu selain **1**, mesej yang dibawa oleh msg.payload akan dialirkan ke output **2**. 

 Untuk menambah aliran output kedua pada nod switch, Klik butang **+** di bahagian bawah, dan pilih **otherwise** dari butang drop-down. Klik **Done**.

<br/>
{:refdef: style="text-align: center;"}
![switch-node]({{site.baseurl}}/assets/img/switch-node.png)
{: refdef}
<br/>

Jika awak perhatikan nod switch yang baru awak buat tadi, awak akan dapati ada dua titik output di sebelah kanan nod. Kita namakan nod ini **If input is 1** sebagai penerangan sekilas imbas tentang fungsi nod ini.

<br/>
{:refdef: style="text-align: center;"}
![switch-example]({{site.baseurl}}/assets/img/switch-example.png)
{: refdef}
<br/>

Sambungkan nod input GPIO ke sebelah kiri input nod switch. Sekarang seret **Change Node** dari palet bahagian **Function**, kemudian klik dua kali kemudian konfigurasikannya seperti imej di bawah. Nod ini digunakan untuk menukar nilai mesej yang diterima sebelum dihantar kepada nod yang seterusnya. Awak akan menggunakan fungsi nod ini untuk menyelesaikan masalah sebelum ini. Ingat kan?apabila awak tidak menekan suis, nod **Button** akan menghasilkan mesej **1**. Kali ini, nilai **1** ini kan dialirkan keluar oleh nod **Switch** masuk ke dalam nod **Change** di output **1**. Nod **Change** kemudian menukarkan nilai **1** kepada **0** lalu menghantar nilai mesej yang baharu ini kepada nod **LED**. Dengan ini LED tidak akan menyala jika awak tidak menekan suis pada breadboard. 

<br/>
{:refdef: style="text-align: center;"}
![change-node]({{site.baseurl}}/assets/img/change-node.png)
{: refdef}
<br/>

Tekan Selesai, kemudian buat sambungan dari output **1** nod **switch** ke nod **change**. Kemudian hubungkan output nod **change** ke nod **LED** seperti imej di bawah.

<br/>
{:refdef: style="text-align: center;"}
![half-flow]({{site.baseurl}}/assets/img/half-flow.png)
{: refdef}
<br/>

Dengan konfigurasi sekarang, LED langsung tidak akan menyala walapun awak menekan butang suis. Untuk menyalakan LED apabila awak menekan butang suis, tambahkan satu lagi nod **change** (namakannya Change to 1) kemudian kali ini setkan nilai msg.payload ke **1**. Sambungkan nod **change** ini ke output **2** nod **switch**, dan kemudian ke nod **LED**. Lakukan seperti di imej di bawah. Dengan ini apabila awak menekan suis, nod **Button** akan menghasilkan mesej **0**. Kali ini, nilai **0** ini kan dialirkan keluar oleh nod **Switch** masuk ke dalam nod **Change** di output **2**. Nod **Change** kemudian menukarkan nilai **0** kepada **1** lalu menghantar nilai mesej yang baharu ini kepada nod **LED**. Dengan ini LED akan menyala jika awak menekan suis pada breadboard.

<br/>
{:refdef: style="text-align: center;"}
![final-flow]({{site.baseurl}}/assets/img/final-flow.png)
{: refdef}
<br/>

### Cuba lakukan sendiri

Ok. Sekarang apa kata awak cuba lakukan satu tugasan dengan sendiri tanpa perlu merujuk pada panduan dari mana-mana tutorial. Tugasan seperti ini penting bagi mengasah kefahaman, kemahiran dan kreativiti awak untuk membina aplikasi menggunakan Node-RED.

Berpandukan pada contoh FLOW di bawah, apa kata kalau awak bina simulator lampu isyarat jalan raya yang dikawal menggunakan timer. Untuk tujuan ini awak boleh gunakan **Node Delay** dan tambahkan lebih banyak nod change dan nod LED. Oleh itu, berdasarkan pada ilmu yang telah awak perolehi sebelum ini, cubalah selesaikan tugasan ini. InsyaAllah kemahiran awak akan lebih mantap lagi selepas ini.  


<br/>
{:refdef: style="text-align: center;"}
![traffic-lights]({{site.baseurl}}/assets/img/traffic-lights.png)
{: refdef}
<br/>













