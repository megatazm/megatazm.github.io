---
layout: post
title: Pengenalan Aplikasi Node-RED
date: 2018-11-8 13:32:20 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: iot-background-imej.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Camaner, How to, IoT]
---
Apa itu Node-Red? Ia adalah "Open Source Software" yang boleh digunakan secara percuma untuk membina aplikasi IoT. "Open Source" bermaksud kod pengaturcaraan software itu didedahkan kepada awam. Ia menggalakkan pembentukkan satu komuniti sukarela, khas untuk aktiviti-aktiviti pembangunan, penambahbaikan dan penyelengaraan sesuatu "Open Source Software". Apa yang menariknya, Node-Red merupakan sebuah editor yang membolehkan pengaturcaraan dilakukan secara visual. Node-Red membolehkan aplikasi yang ringkas disiapkan dengan pantas tanpa sebaris kod! Namun untuk aplikasi IoT yang komplex awak masih perlu menulis kod java script, tapi tidaklah serumit yang perlu awak lakukan jika melalui editor tradisional. 

Ada sebab namanya bermula dari perkataan "Node" atau nod dalam Bahasa Malaysia. Sistem ini mengandungi "Node" yang di sambung antara nod dan nod dengan wayar virtual untuk membentuk satu "Flow", di bina dengan operasi "Click, Drag and Drop" ke atas kanvas (Klik, Seret dan Lepas). Setiap Node menawarkan fungsi berbeza yang boleh melakukan pelbagai operasi pemprosesan. Seperti contoh, "Debug Node" digunakan untuk memudahkan awak dapat melihat proses yang berlaku di antara satu "Node" ke satu "Node" yang lain dalam "Flow". Melalui "Raspberry Pi Node" pula ia membolehkan awak membaca dan menulis (Read & Write) data melalui pin GPIO raspberry pi. 

 Untuk pengetahuan awak, Node-Red sudah siap sedia dilengkapi bersama-sama Raspbian Desktop OS. [Sila ke sini]({% post_url 2018-11-13-Memasang-raspbian-os-ke-sd-card %}) jika awak ndak tau camaner "flash" kan Raspbian Desktop OS pada SD Card. Untuk mengaktifkan Node-Red, awak perlu masuk ke dalam raspberry pi terlebih dahulu. Oleh itu, kita gunakan VNC Client untuk mengakses masuk (guna SSH pun boleh). ([rujuk di sini]({% post_url 2018-11-8-Akses-secara-remote-ke-raspberry-pi-melalui-VNC %}) jika awak nak tau camaner nak aktifkan servis VNC pada raspberry pi). Kemudian jalankan node-red, klik > Progamming > Node-RED seperti gambar di bawah.

 <br/>
{:refdef: style="text-align: center;"}
![nodered-interface]({{site.baseurl}}/assets/img/nodered-start-gui.png)
{: refdef}
<br/>
 
Kemudian awak kini boleh mula menggunakan aplikasi Node-Red ini melalui internet browser komputer awak tanpa perlu melalui VNC Viewer lagi (untuk paparan yang lebih jitu dan lancar). Type IP address raspberry pi awak pada internet browser itu diikuti dengan ":1880". Seperti contoh:-

```javascript
http://192.168.1.25:1880
```

Aplikasi Node-Red akan muncul di internet browser komputer awak.

<br/>
{:refdef: style="text-align: center;"}
![nodered-interface]({{site.baseurl}}/assets/img/nodered-interface.png)
{: refdef}
<br/>
Di sebelah kiri paparan Node-Red adalah palet yang terdiri daripada pelbagai nod input dan output. Awak boleh scroll ke bawah untuk memilih lebih banyak jenis nod mengikut kesesuaian projek. Di atas kanvas, ada tiga jenis nod (inject node, function node, dan debug node) yang telah saya "Klik, Seret, dan Lepas", kemudian saya telah juga sambungkan wayar di antara ketiga-tiga nod ini melalui proses "Klik, Seret, dan Lepas" juga. Ketiga-tiga nod ini menghasilkan satu proses "Flow" yang dinamakan "Flow 2". 

Setelah saya klik pada "Inject Node", saya juga telah klik pada ikon "i" di menu yang berada di sebelah atas dan kanan node-red. Ini bertujuan untuk memperolehi info berkenaan "Inject Node" itu. Untuk mengetahui info berkenaan nod function dan debug, awak cuma perlu klik pada nod tersebut. Jika awak perhatikan pada bucu atas kanan nod debug, awak akan dapati ada bulatan kecil berwarna biru. Ini bermaksud nod debug baharu sahaja di akses atau di edit setting nya. Pada masa yang sama, butang berwarna merah "Deploy" yang di lokasi atas kanan node-red, bermaksud yang awak perlu klikkannya untuk memastikan segala yang telah di edit pada nod-nod itu akan ditetapkan pada status terkini (tiada bulatan biru pada mana-mana nod).

Ok, mari kita cuba lihat apakah dapatan yang "Flow 2" hasilkan. Mula-mula, klik ikon "serangga" yang berada di sebelah ikon "i" tadi. Ini akan menukarkan panel info kepada panel debug. Kemudian, klik kotak segi empat yang berada di sebelah kiri nod inject bernama "timestamp" itu. Awak akan memperolehi maklumat seperti berikut di panel debug:-
<br/>
```javascript
20/11/2018, 23:43:30 node: 2a7a8c89.dbc494
msg.payload : string[38]
"Selamat Berkenalan. Nama saya Node-Red."
```
<br/>
{:refdef: style="text-align: center;"}
![nodered-interface]({{site.baseurl}}/assets/img/nodered-debug.png)
{: refdef}
<br/>

"Function Node" adalah nod yang telah saya programkan menggunakan bahasa pengaturcaraan java script untuk menghasilkan perkataan "Selamat Berkenalan, Nama saya Node-Red". Ini adalah contoh yang mudah sahaja. Ok, klik dua kali "Function Node" tersebut untuk melihat kod yang telah saya masukkan.

<br/>
{:refdef: style="text-align: center;"}
![nodered-interface]({{site.baseurl}}/assets/img/nodered-function-node.png)
{: refdef}
<br/>
Apa yang awak buka sebentar tadi ialah "Node Properties", atau "ciri-ciri nod" dalam Bahasa Malaysia. Di nod ini ada tiga ciri-ciri yang boleh awak edit. "Name" untuk menamakan node ini, saya namakannya "Send My Text". "Function" adalah tempat awak menulis kod bagi menjalankan proses tertentu. Manakala "Outputs" pula membolehkan awak menetapkan kuantiti "Output", saluran keluar hasil daripada pemprosesan "Function Node" ini. Dalam kes ini saya setkan hanya satu sahaja output yang disambungkan pada "Debug Node". Sila lihat pada ruangan "Function". Saya telah tuliskan dua baris kod seperti di bawah.
<br/>

```javascript
1 msg.payload="Selamat Berkenalan. Nama saya Node-Red.";
2 return msg;
```
<br/>
Ok. Merujuk pada kod di atas, msg adalah suatu objek. Jika awak pernah belajar "Object Oriented Programming", awak mungkin faham maksudnya. Tapi, kalau awak tak pernah tahu, tak apa. Awak cuma anggap secara analoginya setiap objek contohnya seperti sebuah motorsikal ada sifat-sifat dan kebolehannya. Sifat-sifatnya seperti warna, saiz tayar, jenis enjin, jenis cc dan lain-lain lagi. Manakala kebolehannya pula adalah seperti whelly, ramming, tukar gear, memecut, memekak dan macam-macam lagi kan. Dalam kes di atas msg.payload bermaksud kebolehan menyimpan perkataan "Selamat Berkenalan, Nama saya Node-Red" di dalam "payload" atau kantung objek msg. Kemudian "return msg" membawa objek msg yang berintikan perkataan itu tadi keluar melalui wayar virtual masuk ke dalam "Debug Node". "Debug Node" kemudian mempamirkan perkataan tadi di panel debug.

Jom kita tambah nilai fungsi Flow 2 ini. Skrol palet ke bawah, cari nod email. Klik, seret dan lepaskan pada kanvas. Kemudian sambungkan wayar virtual dari nod function ke nod email tadi seperti gambar di bawah. 

<br/>
{:refdef: style="text-align: center;"}
![nodered-interface]({{site.baseurl}}/assets/img/nodered-email-node.png)
{: refdef}
<br/>


Kemudian klik dua kali pada nod email dan isikan maklumat seperti di bawah. Oh ya, sebelum itu pastikan awak ada akaun email yahoo.com sebagai penghantar email.

```javascript
To: emailaddressawak@gmail.com
Server: smtp.mail.yahoo.com
Port: 465
Userid: useridyahooawak
Password: passwordyahooemailawak
Name: Send To Email
```

<br/>
{:refdef: style="text-align: center;"}
![nodered-interface]({{site.baseurl}}/assets/img/nodered-email-info.png)
{: refdef}
<br/>

Jika sudah selesai dengan nod email, klik dua kali pada nod function "Send My Text" untuk membuka "Node Properties". Kemudian tambah kod seperti di bawah. Tujuan "msg.topic" ini supaya email yang awak hantar itu ada maklumat pada subjek emelnya nanti.

```javascript
msg.topic="Hello Node-Red";
```
<br/>
{:refdef: style="text-align: center;"}
![nodered-interface]({{site.baseurl}}/assets/img/nodered-email-topic.png)
{: refdef}
<br/>

Setelah selesai mengisi maklumat tersebut, pastikan awak klik "Deploy". Kemudian klik kotak segiempat nod inject "timestamp"yang di sebelah kiri itu . Check email box awak, ada terima email? 

Nod inject ini boleh awak gantikan dengan nod raspberry pi yang disambungkan dengan sensor. Awak boleh set supaya email di hantar jika sensor itu mengesan sesuatu melewati nilai yang ditetapkan. Takpa, awak boleh cuba nanti. Begitulah secara asasnya sebagai pengenalan kepada Node-Red. Seterusnya saya akan pemperjelaskan lagi melalui contoh yang menggunakan raspberry pi pin GPIO. Ya belajar melalui contoh, Learning by Doing!. [Camaner tu.. sila ke sini.]({% post_url 2018-11-30-Membina-aplikasi-mudah-dengan-nodered-dan-raspi%})












